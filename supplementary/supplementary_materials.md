# Materiais Suplementares e Dicionários Expandidos (`supplementary/supplementary_material/`)

Este documento compila os materiais auxiliares, dicionários de dados expandidos e registros adicionais de transparência metodológica da Revisão Sistemática da Literatura.

---

## 1. Dicionário Ampliado do Formulário de Extração (26 Variáveis)

| Campo | Tipo de Dado | Valores Válidos / Formato | Descrição Detalhada |
| :--- | :--- | :--- | :--- |
| `record_id` | String | `REC001` a `REC055` | Chave primária de identificação interna do estudo no projeto. |
| `title` | String | Texto livre | Título original em inglês ou português conforme publicação. |
| `authors` | String | Lista separada por ponto e vírgula | Sobrenome N. para todos os autores listados. |
| `year` | Inteiro | 2020 a 2026 | Ano oficial da publicação ou disponibilização do preprint. |
| `doi` | String | Formato DOI ou URL | Link persistente do objeto digital. |
| `venue` | String | Nome da conferência/periódico | Ex.: IEEE TMI, MICCAI, NeurIPS, arXiv, RSNA. |
| `study_type` | Categoria | Experimental, Benchmark, Review, Case Study | Classificação da abordagem metodológica primária. |
| `clinical_domain` | String | Radiologia Torácica, Imagem Médica Geral | Domínio de especialidade médica abordado. |
| `imaging_modality` | String | CXR, CT, MRI, Musculoskeletal X-Ray | Modalidade de aquisição de imagem radiológica. |
| `dataset` | String | BRAX, MIMIC-CXR, CheXpert, PadChest, MURA | Base(s) de dados utilizada(s) para treino ou teste. |
| `dataset_size` | String | Número exato de imagens/laudos | Volume do corpus de dados de entrada do modelo. |
| `model` | String | MedGemma, CheXagent, RadVLM, LLaVA-Med | Nome do modelo principal avaliado. |
| `model_family` | String | Gemma, Llama, ViT, SigLIP | Família de arquitetura de pesos. |
| `vision_language` | String | MedSigLIP, CLIP, EVA-02 | Encoder visual utilizado para projeção multimodal. |
| `task` | String | Triagem de Pneumonia, Report Gen, VQA | Tarefa de IA clínica executada. |
| `training_strategy` | String | SFT, Zero-Shot, In-Context Learning | Estratégia de aprendizado e treino. |
| `fine_tuning` | String | QLoRA, LoRA, Full Fine-Tuning | Método de ajuste fino de parâmetros. |
| `quantization` | String | AWQ, PTQ 4-bit, GGUF Q4_K_M, INT8 | Técnica de compressão de precisão numérica. |
| `edge_computing` | Booleano | Sim, Não, Híbrido | Presença de testes em hardware de borda. |
| `hardware` | String | Jetson Orin Nano 15W, RTX 4090, A100 | Equipamento físico de execução. |
| `inference_framework` | String | `llama.cpp`, vLLM, Ollama, TensorRT-LLM | Runtime/engine de execução do modelo. |
| `evaluation_metrics` | String | F1-score, RadGraph F1, Latência, VRAM | Métricas quantitativas de desempenho. |
| `main_results` | String | Resumo dos achados numéricos | Resultados quantitativos alcançados. |
| `limitations` | String | Viés de dataset, gargalos de hardware | Fragilidades apontadas pelos autores ou revisores. |
| `relevance_to_review` | Categoria | Referencial Dissertação / Sistema | Destinação sob o protocolo PRISMA Saída Dupla. |
| `notes` | String | Observações técnicas | Notas de auditoria e contexto de engenharia. |

---

## 2. Matriz de Auditoria e Decisões de Arbitragem

Durante o processo de revisão por pares independente, 4 estudos apresentaram divergências iniciais de enquadramento, sendo arbitrados e documentados na tabela abaixo:

| Estudo (ID) | Divergência Inicial | Posição Revisor A | Posição Revisor B | Decisão Final do Consenso |
| :---: | :--- | :--- | :--- | :--- |
| **`REC023` (Hassija et al.)** | Categoria de Saída | Dissertação | Sistema | **Referencial do Sistema ($N_{f2}$):** Ensaio de física e deploy no Jetson Orin Nano a 15W. |
| **`REC038` (Lin et al.)** | Escopo da Quantização | Algoritmo Geral | Sistema Edge | **Referencial do Sistema ($N_{f2}$):** AWQ com otimização direta em hardware restrito. |
| **`REC001` (Sellergren et al.)** | Suporte a Borda | Dissertação | Sistema | **Referencial da Dissertação ($N_{f1}$):** Modelo de fundação MedGemma sem testes no Jetson. |
| **`REC008` (Silva et al.)** | Dataset Local | Dissertação | Exclusão | **Referencial da Dissertação ($N_{f1}$):** Fundamental para transferência no dataset brasileiro BRAX. |

---

## 3. Validação da Consistência Global de Saída Dupla

$$\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies \mathbf{55} = \mathbf{53}_{	ext{(Dissertação)}} + \mathbf{2}_{	ext{(Sistema)}} \quad lacksquare$$
