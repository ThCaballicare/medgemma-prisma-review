# Camada Bibliográfica e Referências (`bibliography/`)

Este diretório concentra os **artefatos bibliográficos utilizados para organizar, normalizar e documentar as referências da revisão sistemática de literatura** desenvolvida no projeto.

A pasta atua como a camada de padronização bibliográfica do repositório, mantendo separada e estruturada a documentação de citações nos formatos padrão (`.bib`, `.csv`, `.ris`), estabelecendo rastreabilidade total entre os resultados brutos de busca (`search_results/`), as etapas do funil PRISMA (`prisma/`) e os estudos efetivamente incluídos no manuscrito e no sistema.

---

## 1. Objetivo do Diretório

A estrutura de `bibliography/` tem como finalidade:

- **Organizar e Normalizar**: Estruturar os metadados bibliográficos completos (autores, título, periódico/conferência, ano, DOI, PubMed ID, URLs) de todas as referências da pesquisa.
- **Sincronização Multi-formato**: Disponibilizar as referências nos três formatos acadêmicos universais:
    - **`references.bib`**: Formato BibTeX para compilação direta em LaTeX / Overleaf.
    - **`references.csv`**: Formato tabular para auditoria de dados, contagens e integração em scripts Python / Pandas.
    - **`references.ris`**: Formato RIS para importação direta em gerenciadores bibliográficos (Zotero, Mendeley, EndNote).
- **Rastreabilidade e Governança**: Mapear cada citação utilizada na dissertação/artigo diretamente com seu registro no funil PRISMA v8 ($N_f = 55$ estudos científicos incluídos).
- **Consistência de Citação**: Garantir a uniformidade dos identificadores de citação (chaves BibTeX como `sellergren2025medgemma`, `lin2024awq`, `dosso2025avaliacao`, etc.).

---

## 2. Relação com o Fluxo da Revisão Sistemática

A bibliografia é o elo de transição entre o processo de seleção da literatura e a redação acadêmica / implementação técnica:

```text
Estratégias de Busca (search_strategies/)
          │
          ▼
Resultados Brutos das Buscas (search_results/)
          │
          ▼
Deduplicação & Triagem (screening/ & prisma/)
          │
          ▼
Avaliação de Elegibilidade em Texto Completo (N_full = 59)
          │
          ▼
Estudos Científicos Incluídos (N_f = 55)
          │
          ├──────────────────────────────────────────┐
          ▼                                          ▼
Camada Bibliográfica (bibliography/)       Análise e Auditoria (analysis/)
  ├── references.bib                                 │
  ├── references.csv                                 ▼
  └── references.ris                       Redação do Manuscrito / Sistema
```

---

## 3. Estrutura dos Arquivos da Pasta

```text
bibliography/
├── README.md           # Guia de governança e documentação da camada bibliográfica
├── references.bib      # Base de referências em formato BibTeX (LaTeX / Overleaf)
├── references.csv      # Base de referências em formato tabular (Data Audit / Pandas)
└── references.ris      # Base de referências em formato RIS (Zotero / Mendeley / EndNote)
```

---

## 4. Classificação dos Estudos Incluídos (PRISMA v8 - Saída Dupla)

A base de dados bibliográfica registra e cataloga os **55 estudos científicos incluídos** na revisão sistemática, devidamente subdivididos conforme a classificação de **Saída Dupla (Dual-Output PRISMA Flow)**:

| Categoria Metodológica         | Símbolo  | Quantidade ($n$) | Função no Projeto & Mapeamento Bibliográfico                                                                                                                                                                                                      |
| :----------------------------- | :------: | :--------------: | :------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Referencial da Dissertação** | $N_{f1}$ |  **53 estudos**  | Suporte teórico geral: baselines clínicas de radiografia de tórax (BRAX, MIMIC-CXR, CheXpert), calibração de modelos, engenharia de prompt _Reason-then-Summarize_ (CoT) e arquitetura fundacional MedGemma 1.5.                                  |
| **Referencial do Sistema**     | $N_{f2}$ |  **2 estudos**   | Suporte técnico de engenharia de borda: testes físicos de telemetria a 15W na placa NVIDIA Jetson Orin Nano, quantização AWQ por magnitudes de ativação e dequantização dinâmica em C++ via `llama.cpp` (LIN et al., 2024; HASSIJA et al., 2026). |
| **Total de Estudos Incluídos** |  $N_f$   |  **55 estudos**  | Base completa catalogada em `references.bib`, `references.csv` e `references.ris`.                                                                                                                                                                |

---

## 5. Padrões de Normalização e Campos Obrigatórios

Para assegurar a máxima qualidade bibliográfica e facilitar a auditoria, cada registro nos arquivos de referências deve conter os seguintes campos padronizados:

- **`cite_key`**: Identificador único em formato autor-ano-termo (ex.: `sellergren2025medgemma`).
- **`title`**: Título integral da publicação em caixa original.
- **`author`**: Lista completa de autores com nomes padronizados (`Sobrenome, Nome`).
- **`journal` / `booktitle`**: Nome oficial do periódico ou conferência revisada por pares.
- **`year`**: Ano de publicação (intervalo 2020–2026).
- **`doi` / `url`**: Digital Object Identifier oficial e link de acesso permanente.
- **`category`**: Classificação de Saída Dupla (`Dissertation_Reference` ou `System_Reference`).

---

## 6. Governança e Reprodutibilidade

- **Imutabilidade de Chaves**: As chaves de citação (`cite_key`) definidas em `references.bib` são mantidas estáticas para prevenir quebras de compilação no documento LaTeX do artigo/dissertação.
- **Sincronia Automática**: Quaisquer atualizações em metadados de artigos incluídos devem ser replicadas simultaneamente nos três arquivos (`.bib`, `.csv`, `.ris`) através dos scripts de sincronização do repositório.
