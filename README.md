# Análise Local de Radiografias de Tórax via Vision-Language Models: Uma Arquitetura baseada em MedGemma e llama.cpp para Triagem de Pneumonia

[![GitHub Repository](https://img.shields.io/badge/GitHub-medgemma--prisma--review-blue?style=for-the-badge&logo=github)](https://github.com/Thiago-R23/medgemma-prisma-review)
[![PRISMA 2020](https://img.shields.io/badge/PRISMA-2020%20Compliant-green?style=for-the-badge)](https://github.com/Thiago-R23/medgemma-prisma-review)
[![License](https://img.shields.io/badge/License-MIT-orange?style=for-the-badge)](LICENSE)
[![Python](https://img.shields.io/badge/Python-3.12-blue?style=for-the-badge&logo=python)](https://www.python.org/)
[![C++](https://img.shields.io/badge/C++-llama.cpp-red?style=for-the-badge&logo=cplusplus)](https://github.com/ggerganov/llama.cpp)

> **Documento Mestre do Repositório (`README.md`)**  
> Apresentação pública, arquitetura geral, governança de dados e mapa de navegação metodológica do projeto **`medgemma-prisma-review`**.  
> **Link do Repositório Oficial no GitHub:** [https://github.com/Thiago-R23/medgemma-prisma-review](https://github.com/Thiago-R23/medgemma-prisma-review)

---

## 📌 1. Visão Geral e Propósito Científico

Este repositório organiza de forma modular, transparente e auditável todos os artefatos, códigos, dados brutos, logs de execução e produtos científicos relacionados à Revisão Sistemática da Literatura (RSL) e à validação técnica do projeto:

**"ANÁLISE LOCAL DE RADIOGRAFIAS DE TÓRAX VIA VISION-LANGUAGE MODELS: UMA ARQUITETURA BASEADA EM MEDGEMMA E LLAMA.CPP PARA TRIAGEM DE PNEUMONIA"**

A pesquisa investiga o estado da arte na aplicação de **Vision-Language Models (VLMs)** de parâmetros compactos para análise de radiografias de tórax (CXR), focando na adaptação do modelo **MedGemma 1.5 (4B)**, na otimização pós-treinamento por quantização ativa (**AWQ / GGUF `Q4_K_M`**) e na viabilidade física de sua execução _offline_ em computação de borda (_edge computing_) em hardwares embarcados com estrita restrição energética (**NVIDIA Jetson Orin Nano 8GB a 15W**) utilizando o motor em C++ nativo **`llama.cpp`**.

A arquitetura do repositório foi desenhada para garantir a **separação estrita de responsabilidades**, isolando o planejamento, os dados operacionais de triagem, os scripts de cálculo estatístico e os produtos finais destinados ao manuscrito e à dissertação.

```text
                                  ┌───────────────────────────┐
                                  │   Planejamento Protocolo  │
                                  │        (protocol/)        │
                                  └─────────────┬─────────────┘
                                                │
                                                ▼
                                  ┌───────────────────────────┐
                                  │   Estratégia & Buscas     │
                                  │  (search_strategies/      │
                                  │    + search_results/)     │
                                  └─────────────┬─────────────┘
                                                │
                                                ▼
                                  ┌───────────────────────────┐
                                  │   Triagem & Seleção       │
                                  │    (screening/ ➔ studies/)│
                                  └─────────────┬─────────────┘
                                                │
                                                ▼
                                  ┌───────────────────────────┐
                                  │   Extração de Dados       │
                                  │       (extraction/)       │
                                  └─────────────┬─────────────┘
                                                │
                                                ▼
                                  ┌───────────────────────────┐
                                  │  Processamento Estatístico│
                                  │     (analysis/ ➔ prisma/) │
                                  └─────────────┬─────────────┘
                                                │
                                                ▼
                                  ┌───────────────────────────┐
                                  │   Produtos do Artigo      │
                                  │    (results/ ➔ figures/   │
                                  │     + supplementary/)     │
                                  └─────────────┬─────────────┘
                                                │
                                                ▼
                                  ┌───────────────────────────┐
                                  │ Documentação & Bibliografia│
                                  │  (docs/ + templates/      │
                                  │    + bibliography/)       │
                                  └───────────────────────────┘
```

---

## 🛠️ 2. Contexto Técnico e Arquitetural do Projeto

A revisão de literatura mapeada neste repositório atua como a espinha dorsal de fundamentação e validação científica para a arquitetura do sistema proposto. O projeto abrange quatro pilares tecnológicos centrais:

1. **Modelo de Fundação Multimodal:** Utilização do **MedGemma 1.5 (4B)**, que integra o decodificador autorregressivo de linguagem **Gemma 3 (4B)** (com janela de contexto de 128k tokens) acoplado ao codificador visual **MedSigLIP (400M)** treinado sob perda sigmoide estável para alinhamento imagem-texto radiológico.
2. **Adaptação de Domínio Regional (SFT):** Ajuste fino supervisionado (_Supervised Fine-Tuning_) conduzido no _host_ (NVIDIA RTX 4090 24GB) via **Unsloth**, aplicando matrizes adaptadoras de baixo posto **QLoRA** ($r=32, lpha=64$) nas projeções lineares de atenção (`q_proj`, `k_proj`, `v_proj`, `o_proj`) e no bloco MLP (`gate_proj`, `up_proj`, `down_proj`) sob precisão de 4 bits (**NF4**), mantendo o encoder de visão congelado para evitar esquecimento catastrófico no dataset brasileiro **BRAX do Hospital Albert Einstein** (40.967 exames).
3. **Engenharia de Raciocínio Clínico (_Reason-then-Summarize_):** Formatação instrucional em Cadeia de Pensamento (_Chain-of-Thought - CoT_), forçando o modelo a registrar suas observações anatômicas dentro do bloco `<think> ... </think>` antes de emitir a decisão estruturada em JSON na tag `<answer> ... </answer>`, reduzindo alucinações fáticas a níveis próximos de zero.
4. **Deploy Offline em Computação de Borda (Edge Computing):** Implantação local do modelo comprimido em formato **GGUF** rodando no motor **`llama.cpp`** em C++ nativo com instruções SIMD ARM NEON na placa **NVIDIA Jetson Orin Nano (8GB VRAM Unificada)** configurada sob limite térmico/energético de **15W**. A solução atinge uma pegada de memória de **5,6 GB VRAM**, vazão de **12–15 tokens/s** e latência TTFT < **1,2s**, garantindo conformidade com a **LGPD** sem dependência de nuvem comercial.

---

## 📐 3. Balanço Quantitativo do Funil PRISMA 2020 (v8 - Saída Dupla)

O processo de seleção sistemática seguiu estritamente o protocolo **PRISMA 2020** com abordagem de **Saída Dupla (_Dual-Output Flow_)**, garantindo rastreabilidade determinística do volume inicial de buscas até o corpus final.

### 📊 Equação de Controle do Funil Global

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad lacksquare
$$

### 🔀 Equação de Aditividade da Saída Dupla (_Dual-Output_)

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies \mathbf{55} = \mathbf{53}_{	ext{(Dissertação)}} + \mathbf{2}_{	ext{(Sistema)}} \quad lacksquare
$$

---

### 📋 Tabela Resumo do Funil de Seleção PRISMA

| Estágio do Funil                 |       Símbolo       | Quantidade ($n$)  | Descrição Metodológica                                                                                                                        |
| :------------------------------- | :-----------------: | :---------------: | :-------------------------------------------------------------------------------------------------------------------------------------------- |
| **Identificação Bruta**          |   $\mathbf{N_i}$    | $\mathbf{64.878}$ | Buscas consolidadas em PubMed ($14.250$), arXiv ($18.420$), IEEE Xplore ($9.150$), Google Scholar ($19.820$) e ACM Digital Library ($3.238$). |
| **Deduplicação**                 |    $\mathbf{D}$     | $\mathbf{9.475}$  | Remoção automatizada de registros repetidos entre bases.                                                                                      |
| **Registros Únicos Triados**     |   $\mathbf{N_1}$    | $\mathbf{55.403}$ | Massa de registros únicos submetidos à triagem de título/resumo.                                                                              |
| **Exclusão Rápida (_Coarse_)**   |   $\mathbf{T_1}$    | $\mathbf{55.258}$ | Descarte preliminar por irrelevância ou fuga de escopo.                                                                                       |
| **Selecionados p/ Detalhamento** |   $\mathbf{N_2}$    |  $\mathbf{145}$   | Artigos pré-selecionados para triagem fina de resumos.                                                                                        |
| **Exclusão Fina (_Detailed_)**   |   $\mathbf{T_2}$    |   $\mathbf{86}$   | Descarte por falta de critérios específicos de VLM ou radiologia.                                                                             |
| **Leitura na Íntegra**           | $\mathbf{N_{full}}$ |   $\mathbf{59}$   | Relatórios científicos recuperados e lidos integralmente.                                                                                     |
| **Excluídos no Texto Completo**  |    $\mathbf{A}$     |   $\mathbf{4}$    | Registros descartados por ausência de dados empíricos de modelos.                                                                             |
| **Estudos Incluídos Final**      |   $\mathbf{N_f}$    |   $\mathbf{55}$   | Corpus final auditado e validado.                                                                                                             |
| └─ _Referencial Dissertação_     |  $\mathbf{N_{f1}}$  |   $\mathbf{53}$   | Suporte teórico geral, baselines de CXR, BRAX, calibração e CoT.                                                                              |
| └─ _Referencial Sistema_         |  $\mathbf{N_{f2}}$  |   $\mathbf{2}$    | Suporte técnico de engenharia de borda a 15W no Jetson e AWQ/`llama.cpp` (LIN et al., 2024; HASSIJA et al., 2026).                            |

---

## 🗂️ 4. Arquitetura Global e Mapa de Navegação do Repositório

O repositório está organizado em **14 diretórios especializados**, cada um respondendo a uma pergunta metodológica fundamental:

```text
medgemma-prisma-review/
│
├── protocol/                 # O que planejamos fazer? (Protocolo PRISMA-P e RQs)
├── search_strategies/        # Como procuramos? (Strings e APIs das 5 bases)
├── search_results/           # O que encontramos? (Massa bruta N_i = 64.878)
├── screening/                # O que foi selecionado/excluído? (Deduplicação e triagem)
├── studies/                  # Quais 55 estudos entraram? (Corpus N_f = 55 e catálogo)
├── extraction/               # O que extraímos deles? (Matriz de 26 variáveis)
├── analysis/                 # Como analisamos os dados? (Scripts Python e estatísticas)
├── prisma/                   # Qual é o controle do funil? (Tabelas de validação)
├── figures/                  # Como representamos os resultados? (Figuras >= 300 DPI)
├── results/                  # Quais resultados foram obtidos? (Produtos finais e logs)
│   ├── appendix/             # Apêndices formais e anexos do artigo
│   ├── figures/              # Documentação das figuras do manuscrito
│   ├── tables/               # Tabelas finais formatadas (CSV, MD, LaTeX)
│   └── logs/                 # Logs de auditoria (decision_log, screening_log, search_log)
├── supplementary/            # Que materiais complementares sustentam a revisão?
├── templates/                # Quais modelos padronizam o processo? (Schemas neutros)
├── docs/                     # Como o projeto foi conduzido? (Guia metodológico e CI/CE)
└── bibliography/             # Quais referências compõem o trabalho? (.bib, .csv, .ris)
```

---

### 🗺️ Detalhamento Funcional por Diretório

| Diretório                | Pergunta Metodológica              | Função e Conteúdo Principal                                                                                                     | Arquivos Chave                                                                                |
| :----------------------- | :--------------------------------- | :------------------------------------------------------------------------------------------------------------------------------ | :-------------------------------------------------------------------------------------------- |
| **`protocol/`**          | _O que planejamos fazer?_          | Armazena o protocolo formal da RSL alinhado ao **PRISMA-P 2015**, contendo as 7 RQs, objetivos e critérios preliminares.        | `protocol.md`, `protocolo_atualizado_v2.txt`                                                  |
| **`search_strategies/`** | _Como procuramos?_                 | Registra as equações booleanas exaustivas, termos Mesh/Emtree e sintaxes de API para as 5 bases.                                | `search_strategies-README.md`                                                                 |
| **`search_results/`**    | _O que encontramos?_               | Guarda a massa bruta e imutável de **$N_i = 64.878$** registros recuperados para fins de auditoria.                             | `search_results_README.md`, `combined_search_results.csv`                                     |
| **`screening/`**         | _O que foi selecionado?_           | Rastreia a filtragem por etapas: deduplicação ($D=9.475$), triagem $T_1=55.258$, $T_2=86$ e elegibilidade $A=4$.                | `identified.csv`, `deduplicated.csv`, `title_abstract.csv`, `full_read.csv`                   |
| **`studies/`**           | _Quais estudos entraram?_          | Catalogação oficial dos **$N_f = 55$ estudos incluídos**, com IDs permanentes (`STD001`–`STD055`) e partição de Saída Dupla.    | `studies_README.md`, `included_studies.csv`, `study_catalog.md`, `study_log.md`               |
| **`extraction/`**        | _O que extraímos deles?_           | Matriz mestre de extração com 26 variáveis estruturadas, formulário padronizado e log de arbitragem de pares.                   | `extraction_README.md`, `extraction_form.csv`, `extracted_data.csv`, `extraction_log.md`      |
| **`analysis/`**          | _Como analisamos os dados?_        | Scripts Python e notebooks para cálculo de frequências, sobreposição, gráficos e auditoria determinística do funil.             | `analysis_README-v2.md`, `statistics_README.md`, `consistency_check.md`                       |
| **`prisma/`**            | _Qual é o controle do funil?_      | Tabelas e relatórios de auditoria matemática do funil PRISMA 2020.                                                              | `prisma-readme.md`, `prisma_flow.csv`, `prisma_validation.csv`                                |
| **`figures/`**           | _Como representamos graficamente?_ | Repositório exclusivo para diagramas e gráficos visuais finais renderizados em alta resolução ($\ge 300	ext{ DPI}$).             | `figures_README.md`                                                                           |
| **`results/`**           | _Quais resultados foram obtidos?_  | Camada isolada de produtos do artigo, dividida em subpastas `tables/`, `figures/`, `appendix/` e `logs/`.                       | `results_README.md`, `results_synthesis.md`, `synthesis_results.csv`                          |
| └─ `results/tables/`     | _Tabelas Finais_                   | Versões finais formatadas das tabelas do manuscrito em `.csv`, `.md` e `.tex` (LaTeX).                                          | `results_tables_README.md`                                                                    |
| └─ `results/logs/`       | _Logs de Auditoria_                | Registros operacionais e diários de bordo (`decision_log.md`, `screening_log.md`, `search_log.md`).                             | `results_logs_README.md`, `decision_log.md`, `screening_log.md`, `search_log.md`              |
| **`supplementary/`**     | _Quais suplementos sustentam?_     | Tabelas estendidas (Tabela S1 - Tendências, Tabela S2 - BRAX 148, Tabela S3 - Telemetria Edge 15W) e estratégias brutas.        | `supplementary_README.md`, `supplementary_materials.md`, `table_s3_jetson_edge_telemetry.csv` |
| **`templates/`**         | _Quais modelos padronizam?_        | Schemas e gabaritos neutros reutilizáveis que atuam como contratos de dados para extração e triagem.                            | `templates_README.md`, `extraction_template.csv`, `screening_template.csv`                    |
| **`docs/`**              | _Como o projeto foi conduzido?_    | Central de documentação metodológica, contendo critérios $CI1	ext{--}CI6 / CE1	ext{--}CE4$, ambiente e guia de reprodutibilidade. | `docs_README.md`, `docs_methodology.md`, `docs_environment.md`, `docs_reproducibility.md`     |
| **`bibliography/`**      | _Quais referências compõem?_       | Padronização bibliográfica sincronizada em três formatos acadêmicos universais.                                                 | `bibliography_README.md`, `references.bib`, `references.csv`, `references.ris`                |

---

## 🏆 5. Governança, Reprodutibilidade e Regras de Qualidade

1. **Imutabilidade de Dados Primários:** Registros em `search_results/` e versões de triagem em `screening/` são _read-only_ e preservados para fins de auditoria científica.
2. **Separação de Código e Apresentação:** Códigos de cálculo residem em `analysis/`, enquanto artefatos visuais e tabelas do artigo residem em `figures/`, `results/tables/` e `results/figures/`.
3. **Padrão de Formatação KaTeX/GitHub:** Toda a documentação Markdown utiliza delimitadores `$$ ... $$` para blocos matemáticos e `$ ... $` para símbolos inline, assegurando renderização impecável na interface do GitHub.
4. **Reprodutibilidade Determinística:** O ambiente computacional pode ser reconstruído integralmente seguindo o guia em `docs/reproducibility.md` e os scripts armazenados em `analysis/scripts/`.

---

## 🔗 6. Links e Referências Rápidas

- **Repositório Oficial no GitHub:** [https://github.com/Thiago-R23/medgemma-prisma-review](https://github.com/Thiago-R23/medgemma-prisma-review)
- **Guia Metodológico Completo:** [`docs/methodology.md`](docs/methodology.md)
- **Guia de Reprodutibilidade:** [`docs/reproducibility.md`](docs/reproducibility.md)
- **Referências BibTeX:** [`bibliography/references.bib`](bibliography/references.bib)
- **Diário de Decisões Metodológicas:** [`results/logs/decision_log.md`](results/logs/decision_log.md)

---

_Repositório mantido sob licença MIT. Para dúvidas metodológicas ou sugestões de reprodutibilidade, consulte a documentação em `docs/`._
