# Extração e Consolidação de Dados (`extraction/`)

Este diretório concentra os artefatos, formulários padronizados, logs de auditoria e bases consolidadas de extração de dados referentes aos estudos incluídos no corpus final da Revisão Sistemática da Literatura (RSL) sobre **Vision-Language Models (VLMs)** para análise radiológica e computação de borda (*edge computing*).

A etapa de extração representa a fase pós-seleção integral do protocolo **PRISMA 2020 (v8 - Saída Dupla)**, estruturando as evidências qualitativas e quantitativas necessárias para a comparação entre arquiteturas, síntese estatística e fundamentação metodológica do artigo.

---

## 1. Estrutura do Diretório

```text
extraction/
├── README.md               # Guia de governança, diretrizes e protocolo de extração
├── extraction_form.csv     # Esquema padronizado do formulário de extração (dicionário de dados)
├── extracted_data.csv      # Matriz consolidada de dados extraídos dos 55 estudos incluídos
├── extraction_log.md       # Log de execução, controle de revisão por pares e discordâncias
└── scripts/                # Scripts de validação de esquema, parsing e exportação
```

---

## 2. Escopo e Categoria das Informações Extraídas

Para cada estudo do corpus final ($N_f = 55$), o formulário de extração mapeia exaustivamente 26 variáveis divididas em 10 dimensões analíticas principais:

| Dimensão Analítica | Descrição das Variáveis Mapeadas |
| :--- | :--- |
| **Identificação Bibliográfica** | `record_id`, `title`, `authors`, `year`, `doi`, `venue` |
| **Metodologia de Pesquisa** | `study_type` (experimental, comparativo, revisão, benchmark) |
| **Domínio Clínico e Imagem** | `clinical_domain` (radiologia de tórax, pneumologia), `imaging_modality` (CXR, CT, MRI) |
| **Bases de Dados (Datasets)** | `dataset` (BRAX, MIMIC-CXR, CheXpert, PadChest), `dataset_size` (número de exames/laudos) |
| **Arquitetura do Modelo** | `model` (MedGemma, CheXagent, RadVLM), `model_family` (Gemma, Llama, ViT), `vision_language` (MedSigLIP, CLIP, EVA) |
| **Tarefa Clínica e Treino** | `task` (triagem de pneumonia, report generation, VQA), `training_strategy` (SFT, zero-shot, RLHF), `fine_tuning` (QLoRA, LoRA, Full) |
| **Otimização e Compressão** | `quantization` (AWQ, PTQ 4-bit NF4, GGUF Q4_K_M) |
| **Ambiente de Borda (Edge)** | `edge_computing` (sim, não, híbrido), `hardware` (NVIDIA Jetson Orin Nano 15W, RTX 4090, A100), `inference_framework` (`llama.cpp`, vLLM, Ollama) |
| **Métricas e Desempenho** | `evaluation_metrics` (F1-score, RadGraph F1, ROUGE-L, Latência, VRAM), `main_results` (desempenho quantitativo) |
| **Avaliação Crítica e Síntese**| `limitations` (viés de dataset, gargalo de memória), `relevance_to_review` (dissertação vs. sistema), `notes` |

---

## 3. Alinhamento com o PRISMA v8 (Saída Dupla)

A extração de dados contempla a classificação estrita dos $N_f = 55$ estudos incluídos segundo a abordagem de **Saída Dupla (*Dual-Output Flow*)**:

### 3.1 Referencial da Dissertação ($N_{f1} = 53$ estudos / $96,36\%$)
Estudos extraídos para fundamentação teórica geral, cobrindo:
* Caracterização do dataset brasileiro **BRAX do Albert Einstein** (40.967 exames de tórax, desequilíbrio de classes e rotulagem por PLN em português).
* Baselines de diagnóstico de pneumonia e lesões pleuropulmonares (MIMIC-CXR, CheXpert, PadChest).
* Engenharia de prompt estruturada *Reason-then-Summarize* sob Cadeia de Pensamento (CoT) com delimitadores `<think> ... </think>` e `<answer> ... </answer>` para mitigação de alucinações clínicas.
* Métricas de calibração diagnóstica (RadGraph F1, CheXbert F1, GREEN Metric).

### 3.2 Referencial do Sistema ($N_{f2} = 2$ estudos / $3,64\%$)
Estudos extraídos para suporte de engenharia aplicada e implantação física:
* **LIN et al. (2024)** (*MLSys*): Otimização de compressores pós-treinamento AWQ (*Activation-Aware Weight Quantization*) por monitoramento ativo das magnitudes de ativação de canais salientes.
* **HASSIJA et al. (2026)** (*IEEE Access*): Telemetria e deploy de LLMs/VLMs leve em hardware de borda com restrição estrita de energia (**15W** na placa **NVIDIA Jetson Orin Nano 8GB**), utilizando kernels C++ via `llama.cpp` e dequantização *on-the-fly* sob registradores ARM NEON.

---

## 4. Validação Matemática da Consistência dos Dados

O quantitativo de registros processados na etapa de extração é rigidamente auditado pela equação de controle do funil PRISMA:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad lacksquare
$$

E pela partição conservativa de Saída Dupla:

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies \mathbf{55} = \mathbf{53} + \mathbf{2} \quad lacksquare
$$

---

## 5. Rastreabilidade, Qualidade e Governança

1. **Dupla Extração Independente:** Os dados são extraídos por dois revisores independentes. Conflitos de interpretação sobre métricas ou parâmetros de hardware são registrados em `extraction_log.md` e resolvidos por consenso.
2. **Reprodutibilidade do Dicionário de Dados:** O arquivo `extraction_form.csv` define o tipo de dado, obrigatoriedade e valores válidos para cada campo, impedindo inconsistências de preenchimento.
3. **Sincronização Automatizada:** Scripts armazenados em `extraction/scripts/` validam a integridade estrutural da matriz `extracted_data.csv` e garantem que as citações permaneçam 100% alinhadas com os arquivos da pasta `bibliography/` (`references.bib`, `references.csv`, `references.ris`).
