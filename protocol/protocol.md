# Protocolo de Revisão Sistemática da Literatura

## 1. Identificação

**Título:** _Vision-Language Models (VLMs) para Análise de Radiografias de Tórax em Ambiente Local via llama.cpp: Uma Revisão Sistemática._

**Objetivo:** Identificar o estado da arte, desafios técnicos e métricas de desempenho para a execução de VLMs especializados em radiologia executados localmente em hardware de borda (_edge computing_).

---

## 2. Metodologia (Diretriz PRISMA 2020)

Esta revisão segue as recomendações da diretriz PRISMA 2020 para garantir a transparência, rigor metodológico e reprodutibilidade no processo de seleção e análise dos estudos.

### 2.1 Critérios de Elegibilidade

#### Critérios de Inclusão (CI)

- **CI1:** Estudos que propõem, adaptam ou avaliam Vision-Language Models (VLMs) aplicados a dados médicos (preferencialmente radiografias de tórax).
- **CI2:** Estudos que abordam técnicas de quantização pós-treino (ex.: 4-bit, formato Q4_K_M) e formatos de compressão como GGUF e AWQ para viabilizar inferência local.
- **CI3:** Estudos que relatam métricas quantitativas de desempenho diagnóstico (F1-score, precisão, recall) associadas a métricas de eficiência computacional física (latência de inferência em segundos, pico de uso de VRAM unificada em gigabytes e consumo de energia em Watts).
- **CI4:** Artigos originais publicados em periódicos indexados, anais de conferências avaliadas por pares ou repositórios de preprints de ampla circulação acadêmica (ex.: arXiv).

#### Critérios de Exclusão (CE)

- **CE1:** Estudos focados exclusivamente em modelos unimodais (classificadores puramente visuais como CNNs clássicas ou processadores apenas textuais) sem integração multimodal.
- **CE2:** Trabalhos que dependem estritamente de processamento remoto em nuvem (ex.: chamadas de APIs proprietárias comerciais) sem viabilidade comprovada de execução offline local.
- **CE3:** Artigos sem resultados empíricos quantitativos, cartas ao editor ou relatórios que consistam apenas em manuais práticos de ferramentas e tutoriais de repositórios de código de terceiros.

### 2.2 Estratégia de Busca

- **Período de busca:** 2020–2026 (abrangendo desde a introdução das arquiteturas fundacionais até as otimizações recentes de dequantização dinâmica por hardware).
- **Idiomas:** Português e Inglês (essenciais para englobar as bases epidemiológicas e linguísticas nacionais e a literatura global de inteligência artificial de borda).
- **Bases de dados ($k = 5$):** Google Scholar, PubMed/MEDLINE, IEEE Xplore, ACM Digital Library e arXiv.

**String de Busca (Exemplo de Sintaxe):**

```text
("Vision-Language Model" OR "VLM" OR "Multimodal Large Language Model") AND ("Chest X-ray" OR "Radiography" OR "BRAX" OR "MIMIC-CXR") AND ("llama.cpp" OR "quantization" OR "GGUF" OR "AWQ" OR "edge computing" OR "NVIDIA Jetson")
```

### 2.3 Processo de Seleção (Fluxo PRISMA de Saída Dupla)

Para garantir o aproveitamento de 100% da literatura qualificada sem prejuízo ao foco experimental estrito de hardware, a fase final de inclusão do fluxo PRISMA adota o modelo de **Saída Dupla (Teórica e Técnica)**.

O funil sistemático obedece à seguinte formulação matemática de controle de consistência:

$$
N_1 = N_i - D = 64.878 - 9.475 = 55.403
$$

$$
N_2 = N_1 - T = 55.403 - 55.258 = 145
$$

$$
N_{full} = N_2 - 86 = 59
$$

$$
N_f = N_{full} - A = 59 - 4 = 55
$$

Onde:

- **$N_i$ (Registros Identificados):** 64.878 registros totais capturados nas buscas ($B_1 + B_2 + B_3 + B_4 + B_5$).
- **$D$ (Duplicatas Removidas):** 9.475 registros repetidos identificados e eliminados.
- **$N_1$ (Registros Únicos):** 55.403 estudos encaminhados para triagem inicial.
- **$T$ (Excluídos por Título/Resumo Inicial):** 55.258 exclusões preliminares por falta de aderência técnica fundamental.
- **$N_2$ (Elegíveis para Triagem Detalhada):** 145 registros pré-selecionados para análise manual de resumos.
- **Excluídos na Triagem Detalhada de T/R:** 86 estudos rejeitados na revisão fina de resumos por inadequação clínica de escopo.
- **$N_{full}$ (Leitura Completa):** 59 textos completos recuperados e analisados na íntegra de forma independente.
- **$A$ (Excluídos no Texto Completo):** 4 registros descontinuados por consistirem em duplicatas, manuais práticos de ferramentas online ou tutoriais de código de repositórios.
- **$N_f$ (Estudos Incluídos Final):** 55 estudos científicos de suporte divididos de forma simétrica:
    - **Referencial da Dissertação (Suporte Teórico — $N_{f1} = 53$):** Estudos incluídos como base teórica (datasets como o BRAX do Albert Einstein, baselines clássicos de redes neurais, comportamento clínico do MedGemma 1.5 de fábrica e estratégias de prompts estruturados contra alucinações).
    - **Referencial do Sistema (Suporte Técnico — $N_{f2} = 2$):** Estudos experimentais primários e aplicados de computação de borda física (telemetria em NVIDIA Jetson Orin Nano de 8 GB sob limite estrito de energia de 15 W, quantização AWQ pós-treinamento baseada na magnitude das ativações de canal e motores compilados em C++ via llama.cpp).

---

## 3. Extração de Dados e Avaliação de Qualidade

Para cada estudo selecionado na leitura integral, os seguintes parâmetros são rigorosamente tabelados e auditados:

| Categoria                 | Parâmetros Extraídos                                                                                 | Aplicação no Sistema de Pneumonia                              |
| ------------------------- | ---------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| **Arquitetura do Modelo** | Encoders (ex.: MedSigLIP 400M) e decodificadores (ex.: Gemma 3 4B).                                  | Definição do esqueleto VLM para o deploy.                      |
| **Otimização**            | Método de quantização (AWQ vs. bitsandbytes) e motor local (llama.cpp).                              | Justificativa de velocidade da inferência local em C++.        |
| **Dataset**               | Rótulos, divisão de paciente e achados (ex.: BRAX do Albert Einstein).                               | Calibração de classes frente ao desbalanceamento de pneumonia. |
| **Hardware**              | Especificações de GPU, VRAM dedicada e VRAM unificada (ex.: NVIDIA Jetson Orin Nano 8 GB, RTX 4090). | Definição de limites térmicos e operacionais (15 W).           |
| **Métricas**              | F1-Score (Micro e Macro), latência (segundos), pico de VRAM (GB), consumo (W).                       | Validação do _trade-off_ de eficiência clínica e técnica.      |

---

## 4. Cronograma

| Etapa                                                   | Data Prevista  |
| ------------------------------------------------------- | -------------- |
| **Execução das Buscas Bibliográficas**                  | Julho de 2026  |
| **Triagem e Seleção Sistemática (PRISMA v8)**           | Julho de 2026  |
| **Análise, Extração de Dados e Síntese de Evidências**  | Agosto de 2026 |
| **Redação Final do Artigo e Integração de Metodologia** | Agosto de 2026 |
