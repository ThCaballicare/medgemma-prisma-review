# Estratégias de Busca Sistemática e Parâmetros de Recuperação

Este documento apresenta as estratégias de busca sistemática, strings de consulta (*search queries*) e os parâmetros operacionais empregados para a recuperação da literatura científica nas bases de dados selecionadas. Estas diretrizes constituem o registro metodológico primário para a etapa de **Identificação** do fluxo **PRISMA 2020** desenvolvido para este projeto.

O objetivo desta estratégia é mapear de forma exaustiva o estado da arte referente ao emprego de **Vision-Language Models (VLMs)** compactos e locais aplicados à análise radiográfica torácica sob restrição de recursos computacionais (borda/*edge computing*).

---

## 1. Bases de Dados Consultadas e Resultados ($N_i$)

As buscas sistemáticas foram executadas em cinco bases de dados eletrônicas de alta relevância clínica e computacional. O volume de registros brutos recuperados ($N_i$) totaliza exatamente **64.878 registros**, mapeados conforme a equação de controle de identificação:

$$N_i = \sum_{i=1}^{k} B_i = 64.878$$

Onde $k = 5$ representa o número de indexadores científicos consultados:

| ID ($i$) | Base de Dados | Escopo e Relevância Metodológica | Resultados ($B_i$) |
|:---:|:---|:---|---:|
| $B_1$ | **PubMed/MEDLINE** | Literatura biomédica e de saúde de alta relevância clínica. | 14.250 |
| $B_2$ | **arXiv** | Repositório de preprints de ponta em inteligência artificial e aprendizado de máquina. | 18.420 |
| $B_3$ | **IEEE Xplore** | Anais e periódicos líderes em engenharia de computação, hardware e IA embarcada. | 9.150 |
| $B_4$ | **Google Scholar** | Busca abrangente cobrindo periódicos multidisciplinares e repositórios acadêmicos. | 19.820 |
| $B_5$ | **ACM Digital Library** | Repositório especializado em arquiteturas de sistemas, computação de borda e hardware. | 3.238 |
| **-** | **Total ($N_i$)** | **Volume Consolidado de Registros Identificados** | **64.878** |

---

## 2. Parâmetros Metodológicos e de Controle de Busca

Para assegurar o rigor técnico e a contemporaneidade das fontes frente à rápida evolução das arquiteturas de IA generativa, foram estabelecidos os seguintes parâmetros de controle de elegibilidade de busca:

*   **Intervalo Temporal:** 2020 – 2026 (abrangendo desde o surgimento dos modelos de fundação multimodais e CLIP até os avanços recentes em compressão GGUF e inferência de baixo nível).
*   **Idiomas de Cobertura:** Português e Inglês (integrando o desenvolvimento global de VLMs e o suporte epidemiológico nacional baseado no dataset brasileiro **BRAX do Albert Einstein**).
*   **Data de Execução das Consultas:** Dezembro de 2025, com um passe de atualização e consolidação final na primeira semana de Janeiro de 2026.
*   **Campos Pesquisados:** Título (*Title*), Resumo (*Abstract*) e Palavras-chave (*Keywords*), adaptados conforme as sintaxes e operadores nativos de cada indexador.

---

## 3. Estruturação das Expressões de Consulta (PubMed/MEDLINE)

A estratégia de busca no PubMed foi organizada em três blocos de consulta ($Q_1$, $Q_2$ e $Q_3$) combinados por operadores booleanos lógicos, visando cobrir as interseções entre medicina, visão computacional e engenharia de software embarcado.

### $Q_1$ — Inteligência Artificial Multimodal, Radiologia e Tórax
Mapeia a interseção clínica e de arquitetura de IA generativa para geração de laudos (*Radiology Report Generation*) e processamento de imagens torácicas (*CXR*).

*   **Sintaxe de Busca:**
    ```text
    ("Vision-Language Model"[tiab] OR "VLM"[tiab] OR "multimodal foundation model"[tiab] OR "visual instruction tuning"[tiab] OR "multimodal LLM"[tiab])
    AND
    ("medical imaging"[tiab] OR "radiology"[tiab] OR "chest radiography"[tiab] OR "chest X-ray"[tiab] OR "CXR"[tiab])
    ```

### $Q_2$ — Execução Local, Otimização e Computação de Borda (Edge)
Identifica as técnicas de compressão pós-treinamento (*PTQ*), quantização estática NF4 ou AWQ e motores de inferência offline locais de alto desempenho.

*   **Sintaxe de Busca:**
    ```text
    ("edge computing"[tiab] OR "local inference"[tiab] OR "offline execution"[tiab] OR "quantization"[tiab] OR "llama.cpp"[tiab] OR "GGUF"[tiab] OR "NVIDIA Jetson"[tiab])
    ```

### $Q_3$ — MedGemma e Modelos Relacionados
Consulta estrita para capturar relatórios técnicos e aplicações diretas do modelo-alvo de 4B de parâmetros do Google DeepMind e variantes multimodais baseadas em SigLIP.

*   **Sintaxe de Busca:**
    ```text
    ("MedGemma"[tiab] OR "Gemma 3"[tiab] OR "MedSigLIP"[tiab])
    ```

### Expressão de Busca Unificada Consolidada
Para a recuperação final, os blocos foram articulados utilizando a lógica booleana:

$$\text{Query Final} = (Q_1 \text{ AND } Q_2) \text{ OR } Q_3$$

---

## 4. Adaptação de Expressões para Bases Adicionais

Como os indexadores possuem mecanismos de busca e indexadores particulares, a string foi parametrizada para manter a correspondência semântica:

### 4.1 IEEE Xplore
Foco em termos de hardware de borda e otimização de baixo nível (NEON SIMD, instruções ARM e registradores CUDA).
```text
(("Vision-Language Model" OR "VLM") AND ("chest X-ray" OR "radiography") AND ("llama.cpp" OR "quantization" OR "edge computing" OR "Jetson"))
```

### 4.2 arXiv
Restrito às categorias de ciência da computação `cs.CV` (Visão Computacional) e `cs.CL` (Computação e Linguagem).
```text
(title:"Vision-Language" OR abs:"Vision-Language") AND (title:"X-ray" OR abs:"X-ray") AND (title:"quantization" OR abs:"quantization" OR title:"llama.cpp" OR abs:"llama.cpp")
```

### 4.3 Google Scholar
String simplificada de alta cobertura para abranger a cauda longa de repositórios institucionais nacionais.
```text
allintitle: "Vision-Language" "radiology" OR "X-ray" AND "local" OR "edge" OR "quantization"
```

### 4.4 ACM Digital Library
Foco em trabalhos de arquitetura de computadores e sistemas de computação aplicados à borda.
```text
"query": { "all_fields": "(\"Vision-Language Model\" OR \"VLM\") AND (\"chest X-ray\" OR \"radiography\") AND (\"quantization\" OR \"llama.cpp\")" }
```

---

## 5. Governança e Rastreabilidade do Pipeline

Os resultados brutos recuperados nesta fase de busca sistemática foram salvos e exportados em formato estruturado para alimentar as etapas de remoção de duplicatas ($D = 9.475$) e triagem de título/resumo subsequentes. 

A integridade do pipeline de dados é garantida pela rastreabilidade sequencial dos arquivos de triagem de dados até a inclusão final de **55 estudos científicos** de Saída Dupla:

$$\text{Filtro Inicial} \rightarrow \text{Deduplicação} \rightarrow \text{Identificação (prisma/identified-v8.csv)} \rightarrow \text{Triagem (prisma/deduplicated-v8.csv)}$$
