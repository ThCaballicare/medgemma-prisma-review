# Resultados das Buscas (`search_results/`)

Esta pasta contém os arquivos de dados primários obtidos a partir das buscas sistemáticas realizadas nas bases de dados selecionadas para fundamentar a Revisão Sistemática da Literatura (RSL) deste projeto.

Os registros brutos aqui armazenados constituem a camada de dados de entrada que alimenta todo o pipeline de triagem, deduplicação e inclusão final de estudos de acordo com o protocolo **PRISMA 2020** adaptado para **Saída Dupla (Dual-Output PRISMA Flow)**.

---

## 1. Bases de Dados Consultadas e Resultados Brutos ($N_i$)

As buscas foram executadas simultaneamente seguindo a string de busca definida no protocolo, retornando um total de **64.878 registros** distribuídos da seguinte forma:

*   **PubMed/MEDLINE:** 14.250 registros
*   **arXiv:** 18.420 registros
*   **IEEE Xplore:** 9.150 registros
*   **Google Scholar:** 19.820 registros
*   **ACM Digital Library:** 3.238 registros
*   **Total de Registros Identificados ($N_i$):** **64.878**

---

## 2. Pipeline de Processamento de Dados (Fluxo PRISMA v8)

Para garantir a rastreabilidade e a reprodutibilidade da revisão sistemática, o processamento dos arquivos nesta pasta segue o fluxo metodológico e de arquivos estruturado a seguir:

```text
Bases de Dados Consultadas (PubMed, arXiv, IEEE, Scholar, ACM)
                           │
                           ▼ [N_i = 64.878]
           Resultados Brutos (search_results/)
                           │
                           ▼
    Consolidação de Registros ➔ prisma/identified-v8.csv [N_i = 64.878]
                           │
                           ▼ Deduplicação (Remoção de D = 9.475 duplicatas)
      Registros Únicos Triados ➔ prisma/deduplicated-v8.csv [N_1 = 55.403]
                           │
                           ▼ Triagem Inicial de T/R (Exclusão de T = 55.258)
     Selecionados para Análise ➔ prisma/title_abstract-v8.csv [N_2 = 145]
                           │
                           ▼ Triagem Detalhada de T/R (Exclusão de 86 resumos)
      Elegibilidade (Texto Completo) [N_full = 59]
                           │
                           ▼ Leitura Integral (Exclusão de A = 4 relatórios)
      Estudos Científicos Incluídos ➔ prisma/full_read-v8.csv [N_f = 55]
                           │
     ┌─────────────────────┴─────────────────────┐
     ▼                                           ▼
Referencial da Dissertação (Suporte Teórico)   Referencial do Sistema (Suporte Técnico)
[N_f1 = 53 artigos]                          [N_f2 = 2 artigos]
- Baselines Clínicas (BRAX, MIMIC, etc.)     - Otimização AWQ & GGUF
- Engenharia de Prompt (CoT/Reason-Summarize)- Telemetria física no Jetson Nano a 15W
- Calibração & Ausência de Alucinações        - Dequantização via llama.cpp (C++ nativo)
```

---

## 3. Descrição das Etapas do Fluxo

### 2.1 Identificação e Consolidação
Os resultados individuais exportados de cada base em formato bruto são consolidados em um único arquivo estruturado denominado `prisma/identified-v8.csv` ($N_i = 64.878$).

### 2.2 Deduplicação
Scripts automatizados realizam a correspondência e limpeza das referências idênticas entre as bases ($D = 9.475$), gerando o arquivo `prisma/deduplicated-v8.csv` ($N_1 = 55.403$ registros exclusivos).

### 2.3 Triagem Inicial (Coarse Screening)
Triagem rápida baseada em títulos e resumos para exclusão automática de registros sem qualquer correlação clínica ou computacional ($T = 55.258$ excluídos), gerando os $145$ artigos elegíveis preliminares ($N_2 = 145$).

### 2.4 Triagem Detalhada (Detailed Screening)
Análise manual e criteriosa dos resumos dos $145$ candidatos. Excluem-se $86$ artigos por inadequação temática estrita, restando exatamente **59 artigos** para busca do texto completo e leitura integral ($N_{full} = 59$), documentados em `prisma/title_abstract-v8.csv`.

### 2.5 Elegibilidade por Leitura Completa
Revisão independente por pares do texto completo das $59$ publicações. São excluídos $4$ registros não científicos (manuais práticos ou duplicatas de parsing), documentados em `prisma/full_read-v8.csv`.

### 2.6 Inclusão com Saída Dupla
O corpus final de **55 estudos científicos incluídos** ($N_f = 55$) é segmentado de forma estratégica:
*   **Referencial da Dissertação ($N_{f1} = 53$):** Suporte teórico de dados, baselines e calibração clínica.
*   **Referencial do Sistema ($N_{f2} = 2$):** Suporte de engenharia embarcada física e telemetria local no Jetson Orin Nano (LIN et al., 2024; HASSIJA et al., 2026).

---

## 4. Governança e Consistência

As frequências e os mapeamentos descritos neste documento são governados pela relação de consistência global:

$$N_f = N_i - D - T - 86 - A$$
$$55 = 64.878 - 9.475 - 55.258 - 86 - 4$$

A manutenção da integridade matemática de toda a estrutura de diretórios (`search_results/`, `screening/` e `prisma/`) é auditada em tempo de build de forma a inviabilizar inconsistências metodológicas no repositório.
