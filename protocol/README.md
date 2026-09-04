# PROTOCOLO DE REVISÃO SISTEMÁTICA DA LITERATURA

## Consistência Mútua

**Projeto:** _MedGemma Optimization for Edge Computing Radiographic Diagnostics_  
**Alvo:** Triagem de Pneumonia Local via Modelos de Visão e Linguagem na Computação de Borda (NVIDIA Jetson, 15W)

---

Este protocolo estabelece o arcabouço metodológico e computacional rígido para a Revisão Sistemática da Literatura (RSL) que fundamenta as decisões de engenharia de software e validações clínicas da dissertação de mestrado.

A revisão segue rigorosamente a diretriz **PRISMA 2020**, com o objetivo de garantir transparência, reprodutibilidade e integridade dos dados.

---

# 1. Objetivo da Revisão Sistemática

Identificar, mapear e avaliar quantitativamente as evidências e desenvolvimentos na fronteira científica de **Modelos de Visão-Linguagem Médica (Medical VLMs)** executados offline de forma local em ambientes de recursos restritos (_edge computing_).

O protocolo foca especificamente no mapeamento de:

- Técnicas de quantização de pesos, como **AWQ (Activation-Aware Weight Quantization)** pós-treinamento em 4 bits;
- Formatos de compactação unificados, como **GGUF**;
- Motores de inferência local de alta performance em C++ nativo, como **llama.cpp**;
- Telemetria física real, incluindo:
    - latência;
    - pico de uso de memória/VRAM;
    - consumo energético em Watts;
    - taxa de processamento de tokens;
- Plataformas de computação de borda, com ênfase na linha **NVIDIA Jetson**;
- Limitações estritas de hardware;
- Conformidade ética e proteção de dados, especialmente no contexto da **LGPD**.

---

# 2. Metodologia de Seleção

A revisão sistemática adota uma estratégia de **Saída Dupla (_Dual-Output PRISMA Flow_)** na fase final de inclusão, com o objetivo de maximizar o valor científico da literatura triada.

Os estudos incluídos são divididos de acordo com seu papel metodológico na dissertação:

1. **Referencial da Dissertação (Nf1)** — suporte teórico, clínico e metodológico geral;
2. **Referencial do Sistema (Nf2)** — suporte técnico direto à arquitetura, otimização e implantação do sistema de borda.

A seleção segue os princípios da diretriz **PRISMA 2020**.

## 2.1 Critérios de Elegibilidade

### 2.1.1 Critérios de Inclusão (CI)

Para serem incluídos, os estudos devem atender cumulativamente a todos os seguintes critérios:

- **CI1 — Aderência de Domínio:** propor, adaptar ou avaliar arquiteturas de _Vision-Language Models_ (VLMs) ou _Multimodal Large Language Models_ (MLLMs) aplicadas explicitamente ao processamento ou diagnóstico de imagens médicas, com ênfase em radiografias digitais de tórax.

- **CI2 — Métricas Quantitativas:** reportar dados empíricos quantitativos de desempenho clínico, como:
    - acurácia diagnóstica;
    - sensibilidade;
    - F1-Score;
    - BLEU;
    - ROUGE;
    - BERTScore;
    - RadGraph F1;

    ou métricas de telemetria computacional, como:
    - latência em segundos;
    - pico de uso de memória DRAM;
    - taxa de processamento em tokens/s.

- **CI3 — Tipo de Estudo:** consistir em artigo científico original publicado em periódicos revisados por pares, anais de conferências consolidadas ou pré-publicações técnicas indexadas de alta relevância no domínio.

- **CI4 — Suporte Linguístico e Temporal:** estar redigido em Português ou Inglês e ter publicação compreendida na janela temporal de **janeiro de 2020 a dezembro de 2026**.

---

### 2.1.2 Critérios de Exclusão (CE)

Estudos que apresentem qualquer uma das seguintes características serão formalmente excluídos:

- **CE1 — Falta de Integração Multimodal:** utilizar abordagens estritamente unimodais, como modelos puramente visuais, classificadores CNN de prateleira sem integração de linguagem ou modelos puramente textuais de processamento clínico de linguagem.

- **CE2 — Falta de Alinhamento Médico:** tratar de modelos de visão-linguagem de domínio geral, como LLaVA de prateleira, Qwen-VL bruto ou GPT-4, sem qualquer processo de alinhamento semântico, ajuste-fino supervisionado (SFT) ou teste experimental específico sobre tarefas e dados médicos legítimos.

- **CE3 — Falta de Rigor Metodológico:** não apresentar descrição metodológica suficiente, ausência de métricas quantitativas formais de acurácia ou consistir em resumos de conferências, editoriais ou estudos preliminares de andamento sem resultados validados.

- **CE4 — Exclusão da Fase de Borda no Referencial Técnico:** para a inclusão estrita no **Referencial do Sistema (Nf2)**, são excluídos estudos que:
    - não conduzam testes de telemetria física real sobre placas de hardware de borda de recursos restritos, como a linha NVIDIA Jetson;
    - não avaliem técnicas de compressão pós-treinamento aplicadas;
    - dependam de chamadas de APIs externas na nuvem;
    - violem os princípios de soberania e conformidade associados à LGPD.

---

# 3. Equação de Controle Matemático e Funil PRISMA V8

Para assegurar a consistência múltipla das planilhas de dados:

- `identified-v8.csv`;
- `deduplicated-v8.csv`;
- `title_abstract-v8.csv`;
- `full_read-v8.csv`;

e do manuscrito final, os registros do funil PRISMA são governados pela seguinte álgebra linear exata de fluxo.

## 3.1 Fluxo Quantitativo

### Deduplicação

$$
N_1\;(\text{Deduplicados})
=
N_i\;(64.878) - D\;(9.475)
=
55.403
$$

### Seleção

$$
N_2\;(\text{Selecionados})
=
N_1\;(55.403) - T\;(\text{Coarse Screening: }55.258)
=
145
$$

### Leitura na Íntegra

$$
N_{full}
=
N_2\;(145) - 86\;(\text{Excluídos na Triagem Detalhada de T/R})
=
59
$$

### Inclusão Final

$$
N_f
=
N_{full}\;(59) - A\;(\text{Excluídos na Leitura Completa: }4)
=
55
$$

---

## 3.2 Parâmetros Quantitativos e Destinação

### 1. Identificação — $N_i = 64.878$

Total de registros identificados por meio de buscas sistemáticas combinadas executadas em exatamente **5 bases de dados bibliográficas** ($k=5$):

| Base de Dados       | Identificador |  Registros |
| ------------------- | ------------: | ---------: |
| PubMed              |         $B_1$ |     14.250 |
| arXiv               |         $B_2$ |     18.420 |
| IEEE Xplore         |         $B_3$ |      9.150 |
| Google Scholar      |         $B_4$ |     19.820 |
| ACM Digital Library |         $B_5$ |      3.238 |
| **Total**           |             — | **64.878** |

A quantidade total de registros brutos é definida por:

$$
N_i = \sum_{i=1}^{5} B_i
$$

$$
N_i =
14.250 + 18.420 + 9.150 + 19.820 + 3.238
=
64.878
$$

---

### 2. Deduplicação — $D = 9.475$

Remoção de registros duplicados idênticos de forma automatizada por meio de correspondência estrita de títulos e identificadores.

O processo resultou em:

$$
N_1 = 55.403
$$

registros únicos para a triagem inicial de título e resumo.

---

### 3. Triagem Inicial Automatizada — $T = 55.258$

Foi realizada uma filtragem rápida para separação de ruídos conceituais, eliminando registros que não abordavam inteligência artificial multimodal ou aplicações relacionadas à saúde.

O processo resultou em:

$$
55.403 - 55.258 = 145
$$

registros encaminhados para a etapa seguinte.

---

### 4. Triagem Detalhada de Título e Resumo — 86 Exclusões

Os **145 registros** restantes foram submetidos à avaliação manual e minuciosa de título e resumo por dupla revisão independente.

Foram formalmente descartados:

$$
86\;\text{artigos}
$$

por discrepâncias de escopo e arquiteturas sem adequação ao domínio.

Consequentemente:

$$
145 - 86 = 59
$$

resultando em exatamente **59 artigos científicos recuperados em texto integral** para leitura completa.

---

### 5. Elegibilidade por Leitura Completa — $A = 4$

Dos **59 textos** avaliados integralmente, exatamente **4 registros** foram excluídos por apresentarem uma ou mais das seguintes características:

- guias práticos de repositórios de código de terceiros;
- duplicatas residuais de arquivo;
- manuais técnicos de ferramentas sem conteúdo de redação científica.

Assim:

$$
59 - 4 = 55
$$

---

### 6. Corpus de Estudos Incluídos — $N_f = 55$

O corpus final é composto por **55 estudos de literatura científica**, distribuídos conforme a arquitetura de Saída Dupla.

#### Referencial da Dissertação — $N_{f1} = 53$

Compreende estudos que oferecem suporte teórico, clínico e metodológico geral à pesquisa.

Entre os temas contemplados estão:

- caracterização do dataset brasileiro **BRAX**, do Hospital Israelita Albert Einstein;
- benchmarks de acurácia de VLMs em radiologia;
- benchmarks como **ReXVQA** e **RadM-Bench**;
- configurações clínicas do modelo **MedGemma 1.5**;
- engenharia de prompt estruturada;
- estratégias para mitigação de alucinações na geração de laudos.

#### Referencial do Sistema — $N_{f2} = 2$

Compreende estudos experimentais primários de computação de borda que oferecem suporte técnico direto à arquitetura de software e ao _deploy_ local propostos.

Os estudos de referência são:

- **LIN et al. (2024)** — AWQ;
- **HASSIJA et al. (2026)** — _Edge Lightweight LLM_.

A relação entre os dois subconjuntos é:

$$
N_f = N_{f1} + N_{f2}
$$

$$
55 = 53 + 2
$$

---

# 4. Mapeamento de Parâmetros Extraídos

Para cada estudo incluído, o processo de auditoria extrai sistematicamente as dimensões técnicas e clínicas correspondentes às **7 Questões de Pesquisa (RQs)** do protocolo.

## RQ1 — Arquiteturas de VLMs Médicos

Quais arquiteturas de VLMs médicos são empregadas na literatura para tarefas relacionadas à radiologia?

São monitorados os seguintes componentes:

### Encoders Visuais

- MedSigLIP;
- CLIP ViT-L/14;
- BiomedCLIP-CXR;
- Swin Transformer.

### Decodificadores de Linguagem

- Gemma 3;
- Gemma 4B;
- LLaMA 2;
- Phi-3.5.

O objetivo é mapear a relação entre arquiteturas multimodais e a capacidade de modelagem e geração de laudos radiográficos.

---

## RQ2 — Frequência de Datasets

Quais datasets são utilizados com maior frequência para treinamento adaptativo, avaliação e _fine-tuning_?

São monitoradas bases nacionais e internacionais, incluindo:

- **BRAX**;
- **MIMIC-CXR**;
- **CheXpert**;
- **PadChest-GR**;
- **VinDr-CXR**.

---

## RQ3 — Infraestruturas de Hardware

Quais infraestruturas computacionais são utilizadas para executar os modelos?

O mapeamento considera:

- servidores convencionais de _data center_;
- infraestrutura em nuvem;
- GPUs dedicadas;
- hardware embarcado;
- dispositivos de _edge computing_;
- NVIDIA Jetson;
- Raspberry Pi.

A análise busca identificar a diferença entre ambientes computacionais convencionais e plataformas locais com recursos restritos.

---

## RQ4 — Métricas Reportadas

Quais métricas são utilizadas para avaliar o desempenho clínico, linguístico e computacional dos modelos?

### Métricas Clínicas e Linguísticas

- BLEU;
- ROUGE-L;
- METEOR;
- BERTScore;
- RadGraph-F1;
- RaTEScore;
- acurácia clínica.

### Métricas de Eficiência Computacional

- latência de inferência;
- vazão de tokens/s;
- pico de utilização de VRAM/DRAM;
- consumo energético em Watts.

---

## RQ5 — Suporte à Inferência Local/Offline

Quais estudos discutem a execução local e offline de modelos multimodais médicos?

A análise considera:

- privacidade de dados sensíveis de pacientes;
- conformidade com a **LGPD**;
- conformidade com a **HIPAA**;
- soberania nacional da infraestrutura hospitalar;
- redução da dependência de serviços externos;
- redução de custos operacionais associados a APIs comerciais;
- possibilidade de execução sem conectividade externa.

---

## RQ6 — Uso do Motor `llama.cpp`

Qual é a utilização do motor **llama.cpp** em cenários de inferência local?

A análise avalia a exploração do motor de execução em C++ nativo, incluindo:

- execução local;
- aceleração por hardware;
- dequantização dinâmica;
- uso de memória;
- vazão de tokens;
- latência;
- viabilidade de inferência em dispositivos de borda.

O objetivo é verificar sua adequação para cenários de inferência clínica local e offline.

---

## RQ7 — Uso do Modelo MedGemma

Quais estudos utilizam ou avaliam o **MedGemma** como modelo de fundação?

O mapeamento contempla especificamente:

- MedGemma 4B;
- MedGemma 27B;
- tarefas radiológicas;
- radiografias de tórax;
- geração de laudos;
- classificação diagnóstica;
- avaliação multimodal.

---

# 5. Requisitos de Design e Configuração do Experimento do Sistema

O protocolo estabelece que as evidências coletadas na literatura devem respaldar metodologicamente o desenho experimental físico desenvolvido na pesquisa aplicada.

A configuração experimental é dividida em duas etapas principais:

1. **Otimização e ajuste-fino no host**;
2. **Deploy local no dispositivo de borda**.

---

## 5.1 Otimização QLoRA no Host

### 5.1.1 Modelo de Partida

O modelo utilizado como ponto de partida é o:

**MedGemma 1.5 4B**

Composto por:

- decodificador **Gemma 3 4B**;
- encoder visual **MedSigLIP 400M**;
- encoder visual mantido congelado durante o processo de ajuste-fino.

---

### 5.1.2 Parâmetros de Baixo Posto

São utilizadas matrizes **LoRA** treináveis com:

| Parâmetro        | Valor |
| ---------------- | ----: |
| Rank ($r$)       |    32 |
| Alpha ($\alpha$) |    64 |
| Fator $\alpha/r$ |     2 |

As matrizes LoRA são injetadas nas seguintes projeções de atenção:

- `q_proj`;
- `k_proj`;
- `v_proj`;
- `o_proj`.

Também são aplicadas às projeções lineares do MLP:

- `gate_proj`;
- `up_proj`;
- `down_proj`.

---

### 5.1.3 Matriz Linguística

Os pesos de base são mantidos congelados em precisão de **4 bits**, utilizando o formato numérico **NormalFloat 4 (NF4)**.

O processo é realizado utilizando:

- PyTorch;
- Unsloth;
- NVIDIA RTX 4090;
- 24 GB de VRAM.

---

### 5.1.4 Engenharia de Prompt Estruturado

É empregada uma heurística **Reason-then-Summarize**, na qual o modelo é treinado para estruturar o raciocínio clínico antes da emissão da resposta diagnóstica.

Os alvos de treinamento são estruturados utilizando os delimitadores:

```text
<think>
...
</think>

<answer>
...
</answer>
```
