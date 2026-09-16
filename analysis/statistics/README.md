# Estatísticas da Revisão Sistemática (`analysis/statistics/`)

Este diretório contém os resultados, métricas quantitativas, tabelas analíticas e artefatos de síntese estatística produzidos durante a auditoria e validação da Revisão Sistemática da Literatura (RSL) sobre a execução local de **Vision-Language Models (VLMs)** em radiologia.

---

## 1. Conteúdo e Finalidade

Os arquivos mantidos neste diretório fornecem a fundamentação quantitativa para o manuscrito e alimentam os painéis de auditoria do repositório, cobrindo os seguintes eixos de análise:

- **Estatísticas Descritivas das Buscas:** Consolidação das frequências absolutas e relativas por base bibliográfica ($B_i$).
- **Distribuição Temporal:** Evolução cronológica das publicações sobre VLMs e otimizações de borda no intervalo de **2020 a 2026**.
- **Análise de Duplicação:** Taxa de sobreposição entre bases de dados e métricas do descarte de duplicatas ($D = 9.475$).
- **Taxas de Rejeição por Etapa:** Indicadores de atrito nas fases de triagem rápida (_coarse screening_), triagem fina (_detailed screening_) e elegibilidade em texto completo (_full-text eligibility_).
- **Tabelas de Validação PRISMA 2020:** Sincronização e auditoria matemática das equações do fluxo **PRISMA v8 (Saída Dupla)**.

---

## 2. Resumo das Estatísticas Descritivas

### 2.1 Distribuição por Base de Dados ($B_i$)

As buscas sistemáticas brutas recuperaram **64.878 registros** distribuídos entre as 5 bases consultadas:

| Base de Dados           | Identificador ($B_i$) | Registros ($n$) | Proporção (%)  |
| :---------------------- | :-------------------: | :-------------: | :------------: |
| **Google Scholar**      |         $B_4$         |    $19.820$     |   $30,55\%$    |
| **arXiv**               |         $B_2$         |    $18.420$     |   $28,39\%$    |
| **PubMed / MEDLINE**    |         $B_1$         |    $14.250$     |   $21,96\%$    |
| **IEEE Xplore**         |         $B_3$         |     $9.150$     |   $14,10\%$    |
| **ACM Digital Library** |         $B_5$         |     $3.238$     |    $4,99\%$    |
| **Total ($N_i$)**       |      $\sum B_i$       |  **$64.878$**   | **$100,00\%$** |

---

### 2.2 Sólido de Filtragem e Métricas do Funil PRISMA (v8)

| Estágio do Funil                     |  Símbolo   | Quantidade ($n$) | Taxa de Retenção | Taxa de Rejeição |
| :----------------------------------- | :--------: | :--------------: | :--------------: | :--------------: |
| **Identificação Bruta**              |   $N_i$    |     $64.878$     |    $100,00\%$    |        —         |
| **Deduplicação**                     |    $D$     |     $9.475$      |    $85,39\%$     |    $14,61\%$     |
| **Registros Únicos Triados**         |   $N_1$    |     $55.403$     |    $100,00\%$    |        —         |
| **Triagem Inicial (Coarse)**         |   $T_1$    |     $55.258$     |     $0,26\%$     |    $99,74\%$     |
| **Triagem Detalhada (Detailed)**     |   $T_2$    |       $86$       |    $40,69\%$     |    $59,31\%$     |
| **Leitura Completa (Elegibilidade)** | $N_{full}$ |       $59$       |    $100,00\%$    |        —         |
| **Excluídos na Leitura Integral**    |    $A$     |       $4$        |    $93,22\%$     |     $6,78\%$     |
| **Estudos Incluídos Final**          |   $N_f$    |     **$55$**     |  **$100,00\%$**  |        —         |

---

### 2.3 Distribuição da Classificação de Saída Dupla (_Dual-Output_)

Os **55 estudos científicos incluídos** na revisão foram categorizados conforme a aplicação metodológica no projeto:

- **Referencial da Dissertação ($N_{f1} = 53$ estudos / $96,36\%$):** Suporte teórico abrangendo baselines clínicas de radiografia de tórax (MIMIC-CXR, CheXpert, BRAX), técnicas de calibração de temperatura, engenharia de prompt _Reason-then-Summarize_ (CoT) e mitigação de alucinações.
- **Referencial do Sistema ($N_{f2} = 2$ estudos / $3,64\%$):** Suporte de engenharia aplicada a testes físicos de telemetria a 15W na placa NVIDIA Jetson Orin Nano de 8 GB, quantização AWQ por magnitudes de ativação e dequantização dinâmica em C++ via `llama.cpp` (LIN et al., 2024; HASSIJA et al., 2026).

---

## 3. Validação Matemática da Consistência Global

A conciliação de todas as métricas contidas nesta pasta é validada de forma determinística pela equação de controle do fluxo:

$$
\mathbf{N}_f = \mathbf{N}_i - \mathbf{D} - \mathbf{T}_1 - \mathbf{T}_2 - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4}
$$

E a aditividade conservativa da Saída Dupla:

$$
\mathbf{N}_f = \mathbf{N}_{f1} + \mathbf{N}_{f2}
\implies
\mathbf{55} = \mathbf{53} + \mathbf{2}
$$

---

## 4. Estrutura dos Arquivos de Estatísticas

```text
analysis/statistics/
├── search_distribution.csv      # Frequências e proporções por base de dados (B_i)
├── overlap_matrix.csv          # Matriz de sobreposição e taxa de duplicatas (D)
├── rejection_breakdown.csv     # Motivos e quantitativos de exclusão (T_1, T_2, A)
├── temporal_trends.csv         # Distribuição de publicações por ano (2020–2026)
└── prisma_validation.csv       # Tabela mestre de conciliação do funil PRISMA v8
```

---

## 5. Rastreabilidade e Governança

Todas as tabelas e relatórios estatísticos mantidos nesta pasta são gerados de forma automatizada a partir dos scripts localizados em `analysis/scripts/` e auditados por notebooks em `analysis/notebooks/`. Qualquer modificação nas entradas primárias deve ser refletida atualizando e re-executando as rotinas de compilação estatística do repositório.
