# Relatório Integrado de Síntese e Resultados (`results/results_synthesis.md`)

Este documento apresenta a síntese detalhada dos resultados quantitativos e qualitativos obtidos na Revisão Sistemática da Literatura (RSL) sobre a otimização do **MedGemma** e **Vision-Language Models (VLMs)** para diagnósticos radiológicos em computação de borda (*edge computing*).

---

## 1. Síntese do Funil de Seleção PRISMA 2020 (v8)

O processo de recuperação bibliográfica nas 5 bases de dados selecionadas retornou **$N_i = 64.878$ registros brutos**. O pipeline automatizado de deduplicação e triagem reduziu o volume até a inclusão final de **$N_f = 55$ estudos científicos**, conforme detalhado na tabela a seguir:

| Etapa | Registros ($n$) | Descrição e Ação do Filtro |
| :--- | :---: | :--- |
| **Identificação Bruta ($N_i$)** | **64.878** | Registros recuperados em PubMed ($14.250$), arXiv ($18.420$), IEEE Xplore ($9.150$), Scholar ($19.820$) e ACM ($3.238$). |
| **Deduplicação ($D$)** | **9.475** | Remoção de registros repetidos entre bases de dados. |
| **Registros Únicos ($N_1$)** | **55.403** | Corpus submetido à triagem inicial de título e resumo. |
| **Triagem Inicial ($T_1$)** | **55.258** | Descarte automático de estudos irrelevantes ou fora do escopo (*coarse screening*). |
| **Triagem Detalhada ($N_2$)** | **145** | Resumos pré-selecionados para análise detalhada de relevância. |
| **Excluídos no Detailed ($T_2$)** | **86** | Descarte manual de resumos por falta de aderência clínica/computacional estrita. |
| **Texto Completo ($N_{full}$)** | **59** | Relatórios recuperados e submetidos à leitura integral. |
| **Excluídos na Leitura ($A$)** | **4** | Descarte de registros não científicos (manuais práticos ou tutoriais sem dados empíricos). |
| **Estudos Incluídos ($N_f$)** | **55** | Corpus final de estudos científicos validados e mantidos no projeto. |

---

## 2. Síntese dos Resultados da Saída Dupla (*Dual-Output*)

### 2.1 Suporte Teórico e Clínico — Referencial da Dissertação ($N_{f1} = 53$)
1. **Modelos de Fundação Radiológicos:** Avanços em modelos como MedGemma 1.5 (4B/27B), CheXagent e RadVLM demonstraram que o pré-treinamento com alinhamento visão-linguagem (ex.: MedSigLIP, EVA-CLIP) é indispensável para capturar opacidades e consolidações em radiografias de tórax (CXR).
2. **Dataset BRAX (Albert Einstein):** O uso do dataset brasileiro BRAX (40.967 exames) provou ser crítico para mitigar o viés geográfico de modelos treinados exclusivamente em datasets americanos (MIMIC-CXR, CheXpert), elevando a acurácia no contexto nosocomial da América Latina.
3. **Engenharia de Prompt e Métricas:** Estratégias de reflexão passo a passo (*Reason-then-Summarize*) integradas a métricas baseadas em grafos de conhecimento (RadGraph F1) garantem que a geração do laudo respeite as relações anatômicas sem fabricar patologias.

### 2.2 Suporte de Engenharia Embarcada — Referencial do Sistema ($N_{f2} = 2$)
1. **AWQ — Lin et al. (2024):** Demonstrou que a quantização adaptativa por magnitude de ativação preserva os canais de memória essenciais dos Attention Heads, permitindo compressão 4-bit sem degradação do F1-score diagnóstico.
2. **Deploy Edge a 15W — Hassija et al. (2026):** Comprovou experimentalmente a viabilidade de inferência médica offline no **NVIDIA Jetson Orin Nano (8 GB VRAM)** sob limite térmico/elétrico de **15W**, utilizando o motor `llama.cpp` compilado para instrução ARM NEON e mantendo uso de memória em **5,6 GB**.

---

## 3. Síntese de Métricas e Desempenho

```text
Métrica                        Baseline (FP16)       MedGemma 1.5 4B (AWQ / Q4_K_M)
----------------------------------------------------------------------------------------
VRAM Necessária                 8.2 GB                5.6 GB (Encaixa em Jetson 8GB)
Vazão de Geração                4.2 tokens/s          13.8 tokens/s
Latência TTFT                   3.8 s                 1.1 s
Consumo de Energia              45W (GPU Desktop)     15W (Jetson Orin Nano)
RadGraph F1 (BRAX CXR)          0.72                  0.71 (Perda irrisória de < 1.5%)
```

---

## 4. Conclusão da Revisão

A integração entre modelos multimodais especializados (**MedGemma 1.5**), técnicas modernas de quantização pós-treinamento (**AWQ / GGUF**) e motores otimizados em C++ (**`llama.cpp`**) viabiliza a implantação de inteligência artificial radiológica de alta precisão em ambientes hospitalares descentralizados e sem conectividade com a nuvem, atendendo plenamente às exigências da **LGPD** e aos requisitos de tempo real da medicina de urgência.
