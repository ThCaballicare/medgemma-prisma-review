# Critérios de Elegibilidade

Este documento estabelece os limites e critérios de inclusão e exclusão de estudos para a Revisão Sistemática da Literatura (RSL) que fundamenta a arquitetura de triagem local de pneumonia por meio de _Vision-Language Models_ (VLMs) em dispositivos de borda (_edge computing_), garantindo rigor metodológico de acordo com as diretrizes do PRISMA 2020 e em perfeita consonância com o desenvolvimento do sistema local.

---

## 1. Critérios de Inclusão (Inclusion Criteria)

Para serem incluídos no corpus final da revisão sistemática, os estudos avaliados devem atender cumulativamente a todos os seguintes critérios de inclusão:

- **CI1 — Arquitetura Multimodal Nativa (VLM):** O estudo deve propor, adaptar ou avaliar modelos multimodais de linguagem e visão que integrem nativamente o processamento conjunto de imagens e linguagem natural em um único pipeline _end-to-end_ (ex.: MedGemma, LLaVA-Rad, CheXagent), superando abordagens unimodais.

- **CI2 — Aplicação Clínica de Radiologia:** O foco principal do modelo e dos experimentos deve ser o diagnóstico clínico, triagem médica, rotulagem automática ou geração de relatórios a partir de exames radiográficos, preferencialmente radiografias digitais de tórax (CXR).

- **CI3 — Otimização e Execução na Borda (Edge):** Estudos que abordem explicitamente técnicas de compressão pós-treinamento (quantização pós-treinamento — PTQ de 4 bits em formato GGUF ou AWQ), _deploy_ local, execução _offline_ ou telemetria física em hardware embarcado restrito (ex.: famílias NVIDIA Jetson, como o Jetson Orin Nano).

- **CI4 — Avaliação Científica com Métricas Quantitativas:** O estudo deve reportar de forma estruturada resultados numéricos e métricas de desempenho clínico e técnico:
    - **Métricas Clínicas:** Acurácia de classificação diagnóstica (F1-Score, AUC), qualidade linguística (BLEU, ROUGE, METEOR) ou de consistência de laudos (RadGraph, CheXbert).
    - **Métricas de Engenharia:** Latência de inferência local na borda (segundos por laudo), pico de consumo de memória unificada (VRAM em GB) ou consumo de energia em Watts.

- **CI5 — Validação de Dados em Datasets Reconhecidos:** Uso de bancos de dados consolidados de radiografias de tórax para treinamento, ajuste-fino ou teste, tais como BRAX (Hospital Albert Einstein), MIMIC-CXR, CheXpert, PadChest ou OpenI.

- **CI6 — Rigor de Qualidade e Canal Científico:** Artigos científicos avaliados por pares em periódicos de impacto, anais de conferências de IA e saúde (ex.: MICCAI, CVPR, IEEE Access) ou _preprints_ em repositórios de alta relevância (arXiv).

- **CI7 — Texto Completo Disponível:** O estudo deve estar disponível para leitura integral, permitindo a verificação detalhada das equações de otimização, hiperparâmetros de SFT e dados físicos de telemetria.

---

## 2. Critérios de Exclusão (Exclusion Criteria)

Estudos que apresentem qualquer uma das seguintes características serão descartados na fase de elegibilidade:

- **CE1 — Modelos Unimodais Isolados:** Trabalhos focados apenas na classificação de imagens médicas (ex.: CNNs puras como DenseNet ou ResNet tradicionais) ou modelos exclusivos de NLP sobre relatórios médicos textuais, sem acoplamento multimodal de visão e linguagem.

- **CE2 — Domínio Geral Não Médico:** VLMs de propósito geral (ex.: CLIP original, LLaVA básico) avaliados unicamente sobre conjuntos de dados de imagens cotidianas comuns, sem adaptação, instrução ou ajuste-fino supervisionado médico.

- **CE3 — Dependência Estrita de Infraestrutura em Nuvem:** Estudos cujo pipeline dependa obrigatoriamente de conexões e processamento remoto via APIs de nuvem comercial (ex.: chamadas remotas de modelos proprietários como GPT-4V ou Gemini sem alternativa de execução local), negligenciando as restrições físicas hospitalares locais, os custos recorrentes em dólar ou os preceitos de privacidade e confidencialidade de dados de pacientes sob a LGPD (Lei nº 13.709/2018).

- **CE4 — Ausência de Dados e Validação Empírica:** Revisões de literatura que não tragam novas análises computacionais, cartas ao editor, resumos de conferências curtos (_abstract-only_), editoriais ou tutoriais técnicos de ferramentas sem _benchmarks_ formais.

- **CE5 — Indisponibilidade de Reprodutibilidade:** Estudos que omitam detalhes fundamentais da infraestrutura computacional ou que não descrevam o método de inferência, impedindo o cálculo preciso do _trade-off_ de desempenho.

---

## 3. Idioma e Período

### 3.1 Idioma

Serão incluídos estudos redigidos em **Português e Inglês**, de modo a abarcar o desenvolvimento técnico das maiores instituições globais de IA de saúde ao mesmo tempo que se preserva o alinhamento idiomático e demográfico da saúde pública brasileira (como os dados laudados do BRAX).

### 3.2 Período

Serão consideradas publicações compreendidas entre os anos de **2020 e 2026 (inclusive)**, cobrindo o advento histórico e a evolução dos modelos de linguagem e visão até as técnicas contemporâneas de decodificação otimizada, SFT com adaptadores LoRA/QLoRA via Unsloth e compilações de inferência via C++ do llama.cpp.
