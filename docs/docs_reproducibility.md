# Guia de Reprodutibilidade (`docs/reproducibility.md`)

Este documento fornece as instruções passo a passo para re-executar e verificar deterministicamente todas as etapas da Revisão Sistemática da Literatura (RSL) e do pipeline de dados do repositório.

---

## 1. Protocolo de Reprodução da Revisão

### Passo 1: Recuperação de Dados Primários

As buscas sistemáticas brutas ($N_i = 64.878$) podem ser auditadas inspecionando os arquivos em `search_results/` e executando as rotinas de agregação em `search_strategies/`:

```bash
# Executa a consolidação das buscas das 5 bases
python analysis/scripts/consolidate_searches.py
```

### Passo 2: Deduplicação de Registros

A limpeza automatizada de registros idênticos ($D = 9.475$) que gera os $N_1 = 55.403$ estudos únicos é executada por:

```bash
# Roda o algoritmo de deduplicação fuzzy por título e DOI
python screening/deduplication.py --input search_results/ --output prisma/deduplicated-v8.csv
```

### Passo 3: Verificação das Equações de Consistência

A validação matemática do funil PRISMA v8 é auditada rodando o script de controle:

```bash
# Audita a consistência das equações do PRISMA v8
python analysis/scripts/validate_prisma.py
```

---

## 2. As Equações de Validação Determinística

O script `validate_prisma.py` testa a exatidão das seguintes equações em tempo de execução:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad \blacksquare
$$

E a composição de Saída Dupla:

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies 55 = 53_{	ext{(Dissertação)}} + 2_{	ext{(Sistema)}} \quad \blacksquare
$$

---

## 3. Sincronização dos Arquivos de Referências e Extração

Para gerar e sincronizar novamente os arquivos das pastas `bibliography/`, `extraction/` e `studies/`:

```bash
# Re-compila os arquivos references.bib, references.csv e references.ris
python bibliography/scripts/compile_bibliography.py

# Re-compila a matriz de extração extracted_data.csv e o log
python extraction/scripts/compile_extraction.py
```
