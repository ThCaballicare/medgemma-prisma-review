# Análise e Auditoria de Dados (`analysis/`)

Esta pasta contém os artefatos utilizados para análise, validação, estatística e auditoria dos dados produzidos durante a Revisão Sistemática da Literatura (RSL) sobre a execução local de **Vision-Language Models (VLMs)** especializados em radiologia.

A análise está integrada ao fluxo metodológico PRISMA 2020 de **Saída Dupla (Dual-Output Flow)** adotado no projeto e utiliza os resultados consolidados das buscas realizadas nas bases PubMed, arXiv, IEEE Xplore, Google Scholar e ACM Digital Library.

---

## 1. Estrutura do Diretório

```text
analysis/
├── combined_search_results.csv
├── README.md
├── statistics/
├── notebooks/
└── scripts/
```

---

## 2. Componentes e Descrição dos Artefatos

### Arquivo Consolidado

- **`combined_search_results.csv`**: Arquivo contendo a consolidação de todos os $N_i = 64.878$ resultados brutos recuperados nas 5 bases de dados bibliográficas utilizadas na revisão. O arquivo permite a inspeção conjunta e cruzada dos registros provenientes de diferentes fontes bibliográficas, constituindo o artefato primário de apoio à análise, rastreabilidade e auditoria do processo de busca.

> **Nota de Governança:** Os arquivos oficiais e imutáveis utilizados nas etapas posteriores de identificação, deduplicação, triagem (_screening_) e elegibilidade são mantidos em seus respectivos diretórios do repositório (`search_results/`, `screening/` e `prisma/`).

### Diretórios Internos

- **`statistics/`**: Contém os resultados, métricas e artefatos relacionados à análise quantitativa dos dados da revisão sistemática. Armazena:
    - Estatísticas descritivas das buscas sistemáticas;
    - Distribuição de registros por base de dados ($B_i$);
    - Distribuição temporal das publicações (2020–2026);
    - Estatísticas de duplicação e taxa de sobreposição entre bases ($D = 9.475$);
    - Resultados quantitativos e taxas de rejeição das etapas de triagem (_coarse_ e _detailed screening_);
    - Tabelas analíticas de validação do fluxo PRISMA;
    - Demais métricas de síntese qualitativa e quantitativa da revisão.

- **`notebooks/`**: Contém notebooks Jupyter exploratórios para análise, mineração e visualização dos dados. Os notebooks priorizam a reprodutibilidade integral das análises e indicam de forma explícita:
    - Os arquivos de entrada utilizados;
    - As transformações e limpezas de dados realizadas;
    - As métricas calculadas e testes estatísticos aplicados;
    - Os gráficos e tabelas produzidos.

- **`scripts/`**: Contém scripts Python automatizados para o processamento, unificação de metadados e validação programática dos dados. Os scripts garantem a execução repetível de tarefas de parsing, contagem de frequências e verificação de consistência, contribuindo para a rastreabilidade absoluta do processo.

---

## 3. Relação com o Fluxo PRISMA (v8 - Saída Dupla)

Os artefatos desta pasta dão suporte à validação quantitativa e auditoria do fluxo PRISMA de **Saída Dupla** adotado na revisão sistemática.

O funil consolidado verificado pelas rotinas de análise apresenta a seguinte distribuição em cada etapa:

| Etapa do PRISMA                                    | Registros ($n$) | Descrição e Ação de Filtragem                                                                  |
| :------------------------------------------------- | :-------------: | :--------------------------------------------------------------------------------------------- |
| **Registros Identificados ($N_i$)**                |   **64.878**    | Registros brutos recuperados nas 5 bases de dados bibliográficas consultadas.                  |
| **Duplicatas Removidas ($D$)**                     |    **9.475**    | Registros idênticos identificados e removidos por scripts automatizados.                       |
| **Registros para Triagem ($N_1$)**                 |   **55.403**    | Conjunto de estudos únicos submetidos à primeira etapa de triagem de título/resumo.            |
| **Excluídos na Triagem Inicial ($T_1$)**           |   **55.258**    | Estudos fora do escopo técnico ou sem relevância preliminar (_coarse screening_).              |
| **Selecionados para Triagem Detalhada ($N_2$)**    |     **145**     | Registros pré-selecionados e submetidos à análise fina de resumos.                             |
| **Excluídos na Triagem Detalhada ($T_2$)**         |     **86**      | Resumos descartados por falta de aderência clínica estrita ou arquiteturas não generalizáveis. |
| **Recuperados para Leitura Completa ($N_{full}$)** |     **59**      | Artigos recuperados em texto integral e submetidos à avaliação de elegibilidade.               |
| **Excluídos na Leitura Completa ($A$)**            |      **4**      | Relatórios não científicos descartados (manuais de ferramentas online, duplicatas de parsing). |
| **Estudos Científicos Incluídos ($N_f$)**          |     **55**      | Corpus final de estudos científicos de suporte incluídos na revisão.                           |

### Classificação de Saída Dupla (Inclusão Final)

Os $N_f = 55$ estudos científicos incluídos são posteriormente classificados em duas vertentes metodológicas complementares:

1. **Referencial da Dissertação ($N_{f1} = 53$ estudos):** Suporte teórico geral, abrangendo modelos de fundação (MedGemma 1.5), baselines clínicas, calibração, engenharia de prompt _Reason-then-Summarize_ (CoT) e caracterização epidemiológica do dataset brasileiro **BRAX do Albert Einstein**.
2. **Referencial do Sistema ($N_{f2} = 2$ estudos):** Suporte técnico de engenharia de software e hardware embarcado, cobrindo testes experimentais de telemetria a 15W na placa NVIDIA Jetson Orin Nano, quantização AWQ por magnitudes de ativação e dequantização dinâmica em C++ via `llama.cpp` (LIN et al., 2024; HASSIJA et al., 2026).

---

## 4. Equação de Controle e Validação de Consistência

A conciliação matemática integral do fluxo **PRISMA 2020 (v8 - Saída Dupla)** é verificada programaticamente pelos scripts de auditoria em `scripts/`. Para garantir visibilidade e clareza absoluta, a relação entre as variáveis de entrada, taxas de rejeição por etapa e o corpus final incluído é modelada formalmente sob a seguinte equação de controle global:

### Equação de Controle Global de Fluxo

$$\large \mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}$$

Substituindo os parâmetros numéricos e símbolos matemáticos correspondentes:

$$\large \mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad lacksquare$$

---

### Decomposição Simbólica e Mapeamento de Variáveis

| Símbolo Matemático | Denominação Metodológica           |    Valor ($n$)    | Operação e Função Lógica no Funil                                |
| :----------------: | :--------------------------------- | :---------------: | :--------------------------------------------------------------- |
|   $\mathbf{N_i}$   | **Registros Identificados Brutos** | $\mathbf{64.878}$ | Somatório inicial de buscas nas 5 bases ($\sum_{j=1}^{5} B_j$)   |
|    $\mathbf{D}$    | **Duplicatas Removidas**           | $\mathbf{9.475}$  | Subtração de registros idênticos repetidos entre bases           |
|   $\mathbf{T_1}$   | **Excluídos na Triagem Inicial**   | $\mathbf{55.258}$ | Descarte automático por irrelevância (_Coarse Screening_)        |
|   $\mathbf{T_2}$   | **Excluídos na Triagem Detalhada** |   $\mathbf{86}$   | Descarte manual de resumos fora de escopo (_Detailed Screening_) |
|    $\mathbf{A}$    | **Excluídos no Texto Completo**    |   $\mathbf{4}$    | Descarte na elegibilidade integral (_Full-Text Eligibility_)     |
|   $\mathbf{N_f}$   | **Estudos Científicos Incluídos**  |   $\mathbf{55}$   | Corpus final retido e validado para a síntese do artigo          |

---

### Validação da Classificação de Saída Dupla (Dual-Output)

A partição do corpus final ($\mathbf{N_f}$) nas duas vertentes de suporte metodológico é formalizada pela equação de aditividade conservativa:

$$\large \mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}}$$

$$\large \mathbf{55} = \mathbf{53}_{	ext{(Suporte Teórico - Dissertação)}} + \mathbf{2}_{	ext{(Suporte Técnico - Sistema Edge)}} \quad lacksquare$$

---

### Equações do Funil Etapa por Etapa

$$
N_1 = N_i - D = 64.878 - 9.475 = 55.403
$$

$$
N_2 = N_1 - T_1 = 55.403 - 55.258 = 145
$$

$$
N_{full} = N_2 - T_2 = 145 - 86 = 59
$$

$$
N_f = N_{full} - A = 59 - 4 = 55
$$

---

## 5. Reprodutibilidade, Escopo e Governança

- **Reprodutibilidade:** Os arquivos de análise preservam a rastreabilidade determinística entre os dados de entrada (`combined_search_results.csv`), os procedimentos executados nos scripts/notebooks e os resultados gerados. Alterações relevantes nos scripts, notebooks ou métodos de análise são obrigatoriamente registradas no histórico do repositório.
- **Escopo:** Esta pasta é destinada exclusivamente às atividades de análise, validação quantitativa, estatística e auditoria dos dados da revisão sistemática. Os registros bibliográficos brutos, critérios metodológicos formais, resultados individuais de _screening_, arquivos dos estudos incluídos e materiais suplementares são mantidos em suas respectivas estruturas organizacionais no repositório (`search_results/`, `screening/`, `prisma/`, etc.).
