# Critérios de Inclusão (`docs/inclusion_criteria.md`)

Este documento estabelece os **Critérios de Inclusão ($CI$)** formais aplicados para a seleção de estudos na revisão sistemática de literatura sobre a execução local de **Vision-Language Models (VLMs)** em radiologia.

---

## Lista de Critérios de Inclusão ($CI1$ a $CI6$)

Para que um estudo seja incluído no corpus final da revisão ($N_f = 55$), ele deve atender obrigatoriamente a **todos** os seguintes critérios:

### $CI1$ — Arquitetura Vision-Language Model (VLM)

- **Descrição:** O estudo deve propor, adaptar, quantizar ou avaliar modelos multimodais que integrem nativamente o processamento de imagens radiológicas e linguagem natural em uma arquitetura unificada.
- **Justificativa:** Modelos multimodais oferecem capacidade de raciocínio contextual e geração de laudos estruturados superior a classificadores visuais isolados.

### $CI2$ — Aplicação em Radiologia e Saúde

- **Descrição:** O foco primário do trabalho deve ser o domínio biomédico, visando o suporte à decisão clínica, diagnóstico de patologias ou triagem radiológica.
- **Justificativa:** Assegura alinhamento com as necessidades do setor de saúde e do Sistema Único de Saúde (SUS).

### $CI3$ — Imagens de Radiografia (Preferencialmente Tórax)

- **Descrição:** O modelo deve ser treinado, ajustado (fine-tuned) ou avaliado com imagens radiográficas (CXR), utilizando datasets públicos ou institucionais reconhecidos (ex.: BRAX, MIMIC-CXR, CheXpert, PadChest).
- **Justificativa:** A radiografia de tórax é o exame de imagem médica mais realizado no mundo e a principal ferramenta de triagem para pneumonia.

### $CI4$ — Disponibilidade do Texto Completo

- **Descrição:** Apenas publicações com acesso integral ao texto do artigo foram consideradas para permitir a extração detalhada de metodologias, hiperparâmetros e telemetria.
- **Justificativa:** Viabiliza a auditoria e extração precisa de dados quantitativos.

### $CI5$ — Qualidade e Revisão por Pares

- **Descrição:** Serão aceitos artigos publicados em periódicos científicos, anais de conferências revisadas por pares (ex.: MICCAI, CVPR, IEEE, ACM) ou preprints de repositórios reconhecidos (ex.: arXiv).
- **Justificativa:** Garante a contemporaneidade dos modelos de fundação médicos lançados recentemente (2020–2026).

### $CI6$ — Métricas Quantitativas Relatadas

- **Descrição:** O estudo deve reportar resultados numéricos de desempenho clínico (F1-score, AUC, RadGraph F1) ou métricas de engenharia (latência de inferência, consumo de VRAM, watts).
- **Justificativa:** Permite a síntese quantitativa e comparação de eficiência entre baselines.

---

## Aplicação dos Critérios no Funil PRISMA v8

A aplicação estrita dos critérios $CI1$–$CI6$ resultou na seleção dos **$N_f = 55$ estudos incluídos**, devidamente validados pela equação de controle:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A} \implies 55 = 64.878 - 9.475 - 55.258 - 86 - 4 \quad \blacksquare
$$
