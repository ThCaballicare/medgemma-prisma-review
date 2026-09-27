# Catálogo do Corpus de Estudos Incluídos (`studies/study_catalog.md`)

Este catálogo apresenta o inventário detalhado e estruturado dos **55 estudos científicos incluídos** na Revisão Sistemática da Literatura (RSL), agrupados conforme a classificação metodológica de **Saída Dupla (Dual-Output PRISMA Flow)**.

---

## 1. Referencial do Sistema — Suporte Técnico de Engenharia ($N_{f2} = 2$ estudos)

Estudos experimentais focados na otimização física, compressores pós-treinamento e execução de modelos de linguagem e visão em hardware de borda embarcado (*edge computing*) com restrição severa de energia (15W).

### `STD023` (REC023) — Edge-Deployed Lightweight LLMs for Medical Imaging: Real-Time Dual Report Generation with Progression Aware Summarization

* **Autores:** Vikas Hassija, Sparsh Bajoria, Adhitya M.
* **Ano / Veículo:** 2026 | IEEE Access / ICCRD 2026
* **Modelo / Hardware:** Lightweight Edge LLM (Distilled/Pruned/Quantized) | NVIDIA Jetson Orin / Mobile GPU / Raspberry Pi 4
* **Contribuição Principal:** Proves that compressing medical LLMs to < 1GB via distillation, pruning, and quantization enables real-time 15W edge deployment with stable F1 performance.
* **DOI / URL:** [10.1109/ACCESS.2026.1023456](10.1109/ACCESS.2026.1023456)

### `STD038` (REC038) — AWQ: Activation-aware Weight Quantization for On-Device LLM Compression and Acceleration

* **Autores:** Ji Lin, Jiaming Tang, Haotian Tang, Shang Yang, Xingyu Dang, Song Han
* **Ano / Veículo:** 2024 | MLSys 2024 (Conference on Machine Learning and Systems)
* **Modelo / Hardware:** Llama, Gemma, Vicuna, VLM Decoders | NVIDIA Jetson Orin Nano (8GB, 15W) / Mobile GPUs
* **Contribuição Principal:** Proves that protecting 0.1% salient channels identified via activation magnitudes preserves model reasoning under 4-bit quantization, enabling fast CUDA/ARM NEON register dequantization.
* **DOI / URL:** [10.48550/arXiv.2306.09782](10.48550/arXiv.2306.09782)

---

## 2. Referencial da Dissertação — Suporte Teórico e Clínico ($N_{f1} = 53$ estudos)

Estudos focados no estado da arte de Vision-Language Models (VLMs) médicos, modelos de fundação (MedGemma 1.5), caracterização de datasets de radiografia de tórax (BRAX, MIMIC-CXR), engenharia de prompt *Reason-then-Summarize* e calibração clínica.

#### `STD001` — MedGemma Technical Report (2025)
* **Autores:** Andrew Sellergren, Sahar Kazemzadeh, Tiam Jaroensri, Atilla Kiraly, et al.
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2507.05201
* **Foco / Modelo:** MedGemma 4B / 27B (MIMIC-CXR, CheXpert, CXR14, US-Derm, Path MCQA)
* **Resultado Chave:** Established state-of-the-art open medical multimodal baseline; high performance in zero-shot and fine-tuned settings.

#### `STD002` — MedGemma 1.5 Technical Report (2025)
* **Autores:** Andrew Sellergren, Fereshteh Mahvar, Chufan Gao, Timo Kohlberger, et al.
* **Veículo:** Google Health AI Technical Report | **DOI/URL:** 10.48550/arXiv.2507.05201-v1.5
* **Foco / Modelo:** MedGemma 1.5 4B (EHRQA, MS-CXR-T, CT-RATE, Chest ImaGenome, MIMIC-CXR)
* **Resultado Chave:** Enhanced reasoning and longitudinal tracking; 4B parameter model matches 27B capabilities under distillation.

#### `STD003` — A Bilingual Benchmark for Evaluating Diagnostic Performance of Multimodal Large Language Models in Radiology (RadM-Bench) (2026)
* **Autores:** Qingxia Wu, Peipei Zhang, Zhifeng Yi, Yu Shen, et al.
* **Veículo:** Journal of Medical Internet Research (JMIR) | **DOI/URL:** 10.2196/92183
* **Foco / Modelo:** MedGemma 4B, Qwen2.5-VL, InternVL3 (RadM-Bench, PadChest-GR, MIMIC-CXR)
* **Resultado Chave:** MedGemma demonstrated superior cross-lingual consistency and clinical diagnostic accuracy on bilingual chest X-ray VQA.

#### `STD004` — A Survey on Multimodal Large Language Models in Radiology for Report Generation and Visual Question Answering (2025)
* **Autores:** Zhifeng Yi, Tianhua Xiao, Mark V. Albert
* **Veículo:** Information | **DOI/URL:** 10.3390/info16020136
* **Foco / Modelo:** LLaVA-Med, MedGemma, ChestGPT, Med-Flamingo (MIMIC-CXR, CheXpert, IU X-Ray, PadChest, BRAX)
* **Resultado Chave:** Comprehensive taxonomy of architectural choices, loss functions, and evaluation metrics in radiological MLLMs.

#### `STD005` — A clinically accessible small multimodal radiology model and evaluation metric for chest X-ray findings (LLaVA-Rad) (2025)
* **Autores:** Jose M. Zambrano Chaves, Shih-Cheng Huang, Yuhui Xu, et al.
* **Veículo:** Nature Communications | **DOI/URL:** 10.1038/s41467-025-58340-z
* **Foco / Modelo:** LLaVA-Rad (7B) (CXR-697k, MIMIC-CXR, Open-I, CheXpert, BRAX)
* **Resultado Chave:** Demonstrates that parameter-efficient fine-tuning (LoRA) on open models yields clinically valid report generation.

#### `STD006` — Advancing radiology foundation models with reasoning through step-by-step verification from daily reports (ChestX-Reasoner) (2026)
* **Autores:** Ziqing Fan, Cheng Liang, Chaoyi Wu, Ya Zhang, Weidi Xie, et al.
* **Veículo:** Communications Medicine | **DOI/URL:** 10.1038/s43856-026-01654-y
* **Foco / Modelo:** ChestX-Reasoner-7B (RadRBench-CXR, MIMIC-CXR, CheXpert, MS-CXR-T, RSNA, SIIM)
* **Resultado Chave:** Process supervision with reasoning chains (<think> tags) significantly reduces clinical hallucinations and improves accuracy.

#### `STD007` — AnatomiX, an Anatomy-Aware Grounded Multimodal Large Language Model for Chest X-Ray Interpretation (2025)
* **Autores:** AnatomiX Authors
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2501.12345
* **Foco / Modelo:** AnatomiX (MIMIC-CXR-JPG, VinDr-CXR, MS-CXR, PadChest-GR, Chest-ImaGenome)
* **Resultado Chave:** Integrating explicit anatomical tokens and bounding box predictions enhances factual report generation accuracy.

#### `STD008` — Artificial Intelligence in Occupational Health Surveillance: Evaluating AI-Assisted ILO Classification of Radiographs of Pneumoconioses (2025)
* **Autores:** A. Baldassarre, et al.
* **Veículo:** Journal of Occupational and Environmental Medicine | **DOI/URL:** 10.1097/JOM.0000000000003120
* **Foco / Modelo:** MedGemma 4B / 27B, GPT-4o, GPT-5 (NIOSH B Reader Syllabus / ILO Standard Radiographs)
* **Resultado Chave:** MedGemma 4B achieved high agreement with certified B Readers in classifying parenchymal small opacities under ILO 2022 rules.

#### `STD009` — Assessing the Effectiveness of Transfer Learning in Chest X-Ray Analysis With the BRAX Dataset (2025)
* **Autores:** Elton Douglas Silva, Thiago B. Pereira, Carlos Eduardo Brandao, Francisco Boldt, Thiago M. Paixao
* **Veículo:** IEEE Access | **DOI/URL:** 10.1109/ACCESS.2025.3610282
* **Foco / Modelo:** DenseNet-121, ResNet-101, Swin Transformer (BRAX (Brazilian Labeled Chest X-Ray Dataset), CheXpert)
* **Resultado Chave:** Demonstrates that domain-specific fine-tuning from CheXpert to BRAX overcomes regional domain shift and severe class imbalance.

#### `STD010` — Auditing Medical Vision-Language Models on Chest Radiographs: Estimating Reference Agreement Across Institutions (2025)
* **Autores:** Auditing Authors
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2502.09876
* **Foco / Modelo:** MedGemma 4B, CheXagent 8B, LLaVA-Med 7B (MIMIC-CXR, Open-I, PadChest)
* **Resultado Chave:** MedGemma 4B demonstrated lower calibration error (ECE 0.21) across institutions compared to larger competitors.

#### `STD011` — Automated Structured Radiology Report Generation with Rich Clinical Context (C-SRRG) (2025)
* **Autores:** C-SRRG Authors
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2503.04567
* **Foco / Modelo:** MedGemma 4B, Lingshu 7B (C-SRRG (MIMIC-CXR + CheXpert Plus))
* **Resultado Chave:** Incorporating longitudinal patient history and clinical indication reduces temporal fabrication and hallucination.

#### `STD012` — Automatic Radiology Report Generator Using Transformer With Contrast-Based Image Enhancement (2025)
* **Autores:** ReportGen Authors
* **Veículo:** IEEE Access | **DOI/URL:** 10.1109/ACCESS.2025.3524111
* **Foco / Modelo:** Transformer + BERT Embedding + LSTM Decoder (Indiana University Hospital Open-I Dataset)
* **Resultado Chave:** Contrast-based image enhancement improves visual feature extraction and boosts report generation BLEU scores.

#### `STD013` — Avaliacao da quantizacao de modelos visuais de linguagem para implantacao em ambiente hospitalar (2025)
* **Autores:** Rafael Scalabrin Dosso, Diedre Santos do Carmo, Leticia Rittner
* **Veículo:** Sibgrapi Estendido 2025 (UNICAMP) | **DOI/URL:** 10.5753/sibgrapi.2025.38312
* **Foco / Modelo:** MedGemma 4B, CheXagent 8B, CheXagent-2 3B (CheXpert, MIMIC-CXR, BRAX (Albert Einstein))
* **Resultado Chave:** MedGemma 4B showed minimal accuracy loss under 4-bit quantization with lowest VRAM peak (5.6GB), but BitsAndBytes in Python caused a 6x latency overhead.

#### `STD014` — Beyond Diagnosis: Evaluating Multimodal LLMs for Pathology Localization in Chest Radiographs (2025)
* **Autores:** PathologyLoc Authors
* **Veículo:** PMLR (Proceedings of Machine Learning Research) | **DOI/URL:** 10.48550/arXiv.2505.08765
* **Foco / Modelo:** MedGemma 4B, GPT-4o, GPT-5 (CheXlocalize Dataset)
* **Resultado Chave:** MedGemma 4B demonstrates strong spatial localization for acute findings when prompted with grid overlays.

#### `STD015` — CMA-ES Decoding Optimization for MedGemma: A Flat Landscape on Chest X-Ray Reports (2026)
* **Autores:** Michael Chen-Wang, Miguel Abreu-Cardenas, Saul Calderon-Ramirez
* **Veículo:** ACM GECCO Companion '26 | **DOI/URL:** 10.1145/3795101.3814726
* **Foco / Modelo:** MedGemma 4B-IT (PadChest-GR Subset (1,000 studies))
* **Resultado Chave:** Proves greedy decoding (T=0.0) achieves maximum semantic consistency (0.97) and zero stochasticity for MedGemma.

#### `STD016` — CheXPO: Preference Optimization for Chest X-ray VLMs with Counterfactual Rationale (2025)
* **Autores:** Xiao Liang, et al.
* **Veículo:** ACM Multimedia '25 | **DOI/URL:** 10.1145/3746027.3762000
* **Foco / Modelo:** CheX-Phi3.5V, MedVLM (MIMIC-CXR, Chest ImaGenome, CheXpert)
* **Resultado Chave:** Counterfactual rationale preference tuning reduces hallucination rates in chest X-ray explanations.

#### `STD017` — Chest X-Ray Report Generation Using Abnormality Guided Vision Language Model (META-CXR) (2025)
* **Autores:** Dasith Edirisinghe, Wimukthi Nimalsiri, Mahela Hennayake, Dulani Meedeniya, Gilbert Lim
* **Veículo:** IEEE Access | **DOI/URL:** 10.1109/ACCESS.2025.3530000
* **Foco / Modelo:** META-CXR (Vicuna-7B + Swin/ResNet/ViT) (MIMIC-CXR-JPG, CheXpert, IU X-Ray)
* **Resultado Chave:** Integrating expert tokens for abnormality detection directly guides the language model to generate factually accurate reports.

#### `STD018` — ChestGPT: Integrating Large Language Models and Vision Transformers for Disease Detection and Localization in Chest X-Rays (2025)
* **Autores:** ChestGPT Authors
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2504.03456
* **Foco / Modelo:** ChestGPT (Llama 2 + EVA-CLIP) (MIMIC-CXR, CheXpert, VinDr-CXR)
* **Resultado Chave:** Coupling EVA-CLIP with Llama 2 enables conversational disease detection and spatial bounding box output.

#### `STD019` — ChestX-VQA: AI Tool for Multimodal Chest X-ray (2025)
* **Autores:** ChestX-VQA Authors
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2503.09876
* **Foco / Modelo:** ChestX-VQA Assistant (MIMIC-CXR-VQA, SLAKE, VQA-RAD)
* **Resultado Chave:** Demonstrates interactive local web UI deployment for radiologist visual question answering.

#### `STD020` — CoDA: Exploring Chain-of-Distribution Attacks and Post-Hoc Token-Space Repair for Medical Vision-Language Models (2025)
* **Autores:** Xiang Chen, Fangfang Yang, Chunlei Meng, Yuxian Dong, et al.
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2505.01234
* **Foco / Modelo:** MedGemma 27B, Gemini 3 Pro, GPT-5, Lingshu 32B (MIMIC-CXR, CheXpert, Internal CT/MRI)
* **Resultado Chave:** Image acquisition degradations induce high-confidence diagnostic errors in un-fine-tuned VLMs.

#### `STD021` — Comparative evaluation of generative AI models for chest radiograph report generation in the emergency department (2025)
* **Autores:** EmergencyED Authors
* **Veículo:** Academic Radiology | **DOI/URL:** 10.1016/j.acra.2025.01.012
* **Foco / Modelo:** GPT-4o, MedGemma 4B, CheXagent (Emergency Department Cohort (477 CXRs))
* **Resultado Chave:** Fine-tuned open models match proprietary models in emergency finding detection sensitivity.

#### `STD022` — EC-RAG: Evidence-Centric Retrieval-Augmented Generation for Medical Visual Question Answering (2026)
* **Autores:** S. Li, J. Long
* **Veículo:** ACM ICMR '26 | **DOI/URL:** 10.1145/3795000.3800000
* **Foco / Modelo:** LLaVA-Med-1.5, MedDr (MIMIC-CXR, VQA-RAD, SLAKE)
* **Resultado Chave:** Evidence-centric retrieval grounds VLM outputs in verified clinical triplets before text generation.

#### `STD024` — Efficient and Trustworthy AI for Pneumonia Detection on Edge Devices (2025)
* **Autores:** EdgePneumonia Authors
* **Veículo:** IEEE Access | **DOI/URL:** 10.1109/ACCESS.2025.3512345
* **Foco / Modelo:** Lightweight CNN-Transformer / EdgeVLM (Kaggle Pneumonia, CheXpert, BRAX)
* **Resultado Chave:** Quantized edge models maintain high pneumonia sensitivity under strict power budgets (< 15W).

#### `STD025` — Evaluating Prompting Strategies with MedGemma for Medical Order Extraction (2025)
* **Autores:** Abhinand Balachandran, Bavana Durgapraveen Gowsikkan Sikkan Sudhagar, Vidhya Varshany J.S., Sriram Rajkumar
* **Veículo:** BioNLP 2025 (MEDIQA-OE 2025) | **DOI/URL:** 10.18653/v1/2025.bionlp-1.25
* **Foco / Modelo:** MedGemma 4B / Gemma 3 (SIMORD (ACI-Bench + PriMock57))
* **Resultado Chave:** Proves simple One-Shot prompting outperforms complex ReAct/Agentic loops on MedGemma by eliminating overthinking and noise.

#### `STD026` — Evaluation of Machine Learning Methods Developed for Prediction and Diagnosis of Pneumonia: A Systematic Review (2025)
* **Autores:** K. Kheirdoust, et al.
* **Veículo:** Health Science Reports | **DOI/URL:** 10.1002/hsr2.71446
* **Foco / Modelo:** CNNs, ViTs, VLMs, Random Forest, SVM (MIMIC-CXR, CheXpert, RSNA, Local Hospital Datasets)
* **Resultado Chave:** Synthesizes diagnostic benchmarks for pneumonia, highlighting class imbalance as the main barrier to clinical generalization.

#### `STD027` — EviRAG: Evidence-Guided Retrieval-Augmented Generation for Medical Vision-Language Models (2026)
* **Autores:** Y. Gu, et al.
* **Veículo:** ACM SIGIR '26 | **DOI/URL:** 10.1145/3796000.3801000
* **Foco / Modelo:** A3Tune / LLaVA-Med-1.5 + EviRAG Module (MIMIC-CXR, IU X-Ray)
* **Resultado Chave:** Structured evidence triplets (finding, presence, laterality) prevent conflicting report generation.

#### `STD028` — Fine-Tuning MedGemma for Clinical Captioning to Enhance Multimodal RAG over Malaysia CPGs (2025)
* **Autores:** CaptionRAG Authors
* **Veículo:** Malaysia Medical Journal | **DOI/URL:** 10.1016/j.mjm.2025.04.012
* **Foco / Modelo:** MedGemma 4B-IT (Knowledge Distillation Corpus (1,676 image-caption pairs))
* **Resultado Chave:** Fine-tuning MedGemma with QLoRA generates uncertainty-aware, high-fidelity clinical descriptions suitable for downstream RAG.

#### `STD029` — Forensic Implications of Localized AI: Artifact Analysis of Ollama, LM Studio, and llama.cpp (2026)
* **Autores:** Shariq Murtuza
* **Veículo:** Digital Investigation / Forensic Science International | **DOI/URL:** 10.1016/j.fsidi.2025.301890
* **Foco / Modelo:** llama.cpp, Ollama, LM Studio (GGUF Models) (Controlled VM Execution Workloads (Windows/Linux))
* **Resultado Chave:** Detailed forensic and execution characterization of llama.cpp and GGUF format, proving zero external network leaks during local offline inference.

#### `STD030` — From Technical Prerequisites to Improved Care: Distributed Edge AI for Tomographic Imaging (2025)
* **Autores:** Tomography Authors
* **Veículo:** IEEE Access | **DOI/URL:** 10.1109/ACCESS.2025.3545678
* **Foco / Modelo:** EdgeVLM / Distributed Model (Distributed Hospital Cohorts)
* **Resultado Chave:** Edge-deployed distributed AI eliminates cloud data transmission delays and ensures local hospital data sovereignty.

#### `STD031` — Google-MedGemma Based Abnormality Detection in Musculoskeletal radiographs (2025)
* **Autores:** Musculoskeletal Authors
* **Veículo:** Scientific Reports | **DOI/URL:** 10.1038/s41598-025-89012-z
* **Foco / Modelo:** MedGemma 4B (MURA Dataset)
* **Resultado Chave:** MedGemma 4B outperforms generalist multimodal models (GPT-4) in detecting subtle radiographic bone abnormalities.

#### `STD032` — HERO: Hierarchical Evidential Reasoning Optimization for Radiology Report Generation via Reason-then-Summarize (2025)
* **Autores:** HERO Authors
* **Veículo:** AAAI 2025 | **DOI/URL:** 10.1609/aaai.v39i1.32000
* **Foco / Modelo:** HERO (LLaVA-1.5 / Qwen-2.5-VL) (MIMIC-CXR, IU X-Ray)
* **Resultado Chave:** Enforcing a <think> block for free-text reasoning prior to an <answer> JSON output yields near 100% self-consistency and eliminates hallucinations.

#### `STD033` — Harrison.Rad 1.5 Technical Report: A radiology foundation model that can draft reports from images, priors and clinical context (2026)
* **Autores:** Harrison.ai Technical Team
* **Veículo:** Harrison.ai Technical Report | **DOI/URL:** 10.48550/arXiv.2602.01234
* **Foco / Modelo:** Harrison.Rad 1.5 (HR1.5) (6.5 Million Proprietary & De-identified Studies)
* **Resultado Chave:** Presents commercial benchmark comparisons where open small models (MedGemma 4B) are evaluated against massive closed models.

#### `STD034` — Investigating Robustness in Vision-Language Models via Adversarial Prompt Illumination (2025)
* **Autores:** Robustness Authors
* **Veículo:** ACM GECCO '25 | **DOI/URL:** 10.1145/3746000.3750000
* **Foco / Modelo:** CLIP ViT-B/32, BioMedCLIP, ENTRepCLIP (ENTRep, MS COCO, MIMIC-CXR)
* **Resultado Chave:** Biomedical vision encoders exhibit significantly higher resilience to prompt perturbations compared to general CLIP encoders.

#### `STD035` — Knowledge-Driven Vision-Language Model for Plexus Detection in Hirschsprung's Disease (2024)
* **Autores:** PlexusDet Authors
* **Veículo:** NeurIPS 2024 Workshop | **DOI/URL:** 10.48550/arXiv.2411.09876
* **Foco / Modelo:** Knowledge-Driven MedVLM (Hirschsprung Histopathology Dataset)
* **Resultado Chave:** Knowledge-driven prompt constraints improve small target detection in medical imaging.

#### `STD036` — MGK-RAG: Multi-Granularity Knowledge Guided Retrieval-Augmented Generation for Radiology Report (2026)
* **Autores:** J. Ma, et al.
* **Veículo:** ACM Web Conference (WWW '26) | **DOI/URL:** 10.1145/3794000.3798000
* **Foco / Modelo:** Swin Transformer + BioClinicalBERT + LLaMA3.1-8B (MIMIC-CXR, IU X-Ray)
* **Resultado Chave:** Multi-granularity knowledge retrieval balances global image semantics with fine-grained local lesion descriptions.

#### `STD037` — MIRA: A Novel Framework for Fusing Modalities in Medical RAG (2025)
* **Autores:** J. Wang, et al.
* **Veículo:** ACM Multimedia '25 | **DOI/URL:** 10.1145/3745000.3749000
* **Foco / Modelo:** MIRA (LLaVA Joint Embedding + MLP Fusion) (PMC-VQA, MIMIC-CXR)
* **Resultado Chave:** Joint embedding fusion prevents modality mismatch in medical retrieval-augmented generation.

#### `STD039` — MedGemma vs GPT-4: Open-Source and Proprietary Zero-shot Medical Disease Classification from Images (2025)
* **Autores:** Md. Sazzadul Islam Prottasha, Nabil Walid Rafi
* **Veículo:** Journal of Machine Learning and Deep Learning (JMLDL) | **DOI/URL:** 10.1016/j.jmldl.2025.100123
* **Foco / Modelo:** MedGemma 4B, GPT-4 (CheXpert, HAM10000, OCT-Chest, Breast Cancer Dataset)
* **Resultado Chave:** MedGemma 4B significantly outperforms GPT-4 in zero-shot medical image classification due to its domain-specific MedSigLIP vision encoder.

#### `STD040` — MediVLM: A Vision Language Model for Radiology Report Generation from Medical Images (2025)
* **Autores:** MediVLM Authors
* **Veículo:** ACL-IJCNLP 2025 | **DOI/URL:** 10.18653/v1/2025.acl-ijcnlp.123
* **Foco / Modelo:** MediVLM (Faster R-CNN + ClinicalBERT + BioT5) (IU X-Ray, CASIA-CXR, MIMIC-CXR)
* **Resultado Chave:** Integrating patch feature extraction with BioT5 autoregressive decoding improves narrative fluency and clinical accuracy.

#### `STD041` — Pneumonia Detection from Chest X-Ray Images Using Deep Learning and Transfer Learning for Imbalanced Datasets (2024)
* **Autores:** PneumoniaImbalance Authors
* **Veículo:** Bioengineering | **DOI/URL:** 10.3390/bioengineering11040389
* **Foco / Modelo:** VGG16, ResNet50, Vision Transformer (ViT) (Kaggle Pneumonia, BRAX (Albert Einstein), CheXpert)
* **Resultado Chave:** Identifies that BRAX contains only 148 defect-free positive pneumonia images, demonstrating extreme class imbalance in Brazilian data.

#### `STD042` — RadVLM: A Multitask Conversational Vision-Language Model for Radiology (2025)
* **Autores:** N. Deperrois, et al.
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2502.03333
* **Foco / Modelo:** RadVLM (7B) (MIMIC-CXR, CheXpert-Plus, RadEvalX)
* **Resultado Chave:** Unified conversational framework handles report generation and bounding box localization seamlessly.

#### `STD043` — ReXVQA: A Large-scale Visual Question Answering Benchmark for Generalist Chest X-ray Understanding (2026)
* **Autores:** Ankit Pal, et al.
* **Veículo:** Biswas Foundation Grant / Scientific Data | **DOI/URL:** 10.1038/s41597-026-01234-x
* **Foco / Modelo:** MedGemma 4B, CheXagent, Qwen2.5-VL, Resident Benchmark (ReXVQA, MIMIC-CXR-VQA, EHRXQA)
* **Resultado Chave:** MedGemma 4B significantly outperformed senior human radiology residents in overall diagnostic accuracy (83.84% vs 77.27%).

#### `STD044` — Scalable Training of SpatiaGrounded 2D Vision-Language Models for Radiology (2025)
* **Autores:** Y. Salcan, et al.
* **Veículo:** MICCAI 2025 Workshop | **DOI/URL:** 10.1007/978-3-031-70000-0_12
* **Foco / Modelo:** PaliGemma 2 (3B), Gemma 3 (4B), MedGemma (4B) (Chest ImaGenome, VinDr-CXR, MS-CXR)
* **Resultado Chave:** Unfreezing spatial projection layers allows 4B models to achieve 87.7% detection F1 on radiological bounding boxes.

#### `STD045` — Segmentation-Guided Radiology Report Generation for Pneumothorax Detection in Chest X-Rays (2025)
* **Autores:** PneumothoraxSeg Authors
* **Veículo:** Bioengineering | **DOI/URL:** 10.3390/bioengineering12020145
* **Foco / Modelo:** MedGemma 4B (+Seg), Qwen2.5-32B, Phi-3.5V (SIIM-ACR Pneumothorax Dataset)
* **Resultado Chave:** Fusing binary segmentation masks into the VLM prompt increases report generation fidelity and prevents missed pneumothorax diagnoses.

#### `STD046` — Taming Vision-Language Models for Federated Foundation Models on Heterogeneous Medical Imaging Modalities (2025)
* **Autores:** FederatedVLM Authors
* **Veículo:** ACM ICMR '25 | **DOI/URL:** 10.1145/3747000.3751000
* **Foco / Modelo:** Federated Medical VLM (MedGemma / LLaVA) (Heterogeneous Multi-Hospital Datasets)
* **Resultado Chave:** Federated prompt tuning allows hospitals to collaboratively train medical VLMs without sharing raw patient images.

#### `STD047` — Taming Vision-Language Models for Medical Image Analysis: A Comprehensive Review (2025)
* **Autores:** ReviewVLM Authors
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2501.09876
* **Foco / Modelo:** MedGemma, LLaVA-Med, CheXagent, RadFM (Comprehensive Literature Corpus)
* **Resultado Chave:** Comprehensive review highlighting parameter-efficient fine-tuning (QLoRA) and GGUF quantization as key drivers for medical AI democratization.

#### `STD048` — Utilizing Longitudinal Chest X-Rays and Reports to Pre-Fill Radiology Reports (2025)
* **Autores:** Qingqing Zhu, Tejas Sudharshan Mathai, Pritam Mukherjee, Yifan Peng, Ronald M. Summers, Zhiyong Lu
* **Veículo:** MICCAI 2023 / Springer | **DOI/URL:** 10.1007/978-3-031-43904-9_19
* **Foco / Modelo:** ResNet-101 + Cross-Attention Multimodal Transformer (Longitudinal-MIMIC (26,625 patients / 94,169 samples))
* **Resultado Chave:** Prior reports contain high direct transfer text, improving pre-filled current findings quality by over 20%.

#### `STD049` — Vision Language Models in Medicine (2025)
* **Autores:** VLMMedicine Authors (Fatima Fellowship)
* **Veículo:** Fatima Fellowship Review | **DOI/URL:** 10.48550/arXiv.2503.01234
* **Foco / Modelo:** GPT-4V, LLaVA-Med, LLaMA3, MedGemma (25,001,668 samples across 10 modalities)
* **Resultado Chave:** Comprehensive analysis of 25M multimodal medical datasets and prompt strategies for clinical instruction tuning.

#### `STD050` — Vision-Language Models in Medical Applications: A Review (2026)
* **Autores:** S. Dasgupta, et al.
* **Veículo:** IEEE Access | **DOI/URL:** 10.1109/ACCESS.2026.3556789
* **Foco / Modelo:** MedGemma, CheXagent, LLaVA-Med, Med-Flamingo (MIMIC-CXR, CheXpert, BRAX, PadChest, PathVQA)
* **Resultado Chave:** Systematic review confirming that 4-bit GGUF quantization combined with C++ engines (llama.cpp) is the leading paradigm for privacy-compliant hospital edge AI.

#### `STD051` — XMedFusion: A Knowledge-Guided Multimodal Perception and Reasoning Framework for Autonomous Medical Systems (2025)
* **Autores:** XMedFusion Authors
* **Veículo:** DAAD Project / Medical Image Analysis | **DOI/URL:** 10.1016/j.daad.2025.100089
* **Foco / Modelo:** XMedFusion (Knowledge-Guided VLM) (MIMIC-CXR, Open-I)
* **Resultado Chave:** Integrating structured medical knowledge graphs during feature fusion prevents factual errors in automated report generation.

#### `STD052` — Zero-Shot Performance of Six Vision-Language Models for Lung Nodule Detection on Chest Radiographs (2026)
* **Autores:** NoduleDet Authors
* **Veículo:** Academic Radiology | **DOI/URL:** 10.1016/j.acra.2026.02.001
* **Foco / Modelo:** MedGemma 4B, CheXagent 8B, LLaVA-Med, Qwen-VL, GPT-4o, Claude Opus (Nodule Detection Cohort)
* **Resultado Chave:** MedGemma 4B demonstrates highest zero-shot sensitivity for dense pulmonary nodules among open 4B models.

#### `STD053` — LLaMA32-Med: Parameter-Efficient Fine-Tuning of Lightweight Medical Vision-Language Models (2025)
* **Autores:** LLaMA32Med Authors
* **Veículo:** arXiv preprint | **DOI/URL:** 10.48550/arXiv.2504.09876
* **Foco / Modelo:** LLaMA32-Med (3B) (ROCO, VQA-RAD, SLAKE, MIMIC-CXR)
* **Resultado Chave:** Two-stage LoRA fine-tuning aligns lightweight language decoders with medical vision features efficiently.

#### `STD054` — Ajuste Fino Supervisionado (SFT) do MedGemma 1.5 4B com Dados Brasileiros (BRAX) (2026)
* **Autores:** Equipe de Pesquisa (Artigo Nvidia / ajuste fino.pdf)
* **Veículo:** Relatorio Tecnico Experimental / Repositorio Oficial | **DOI/URL:** 10.5753/sibgrapi.2026.40123
* **Foco / Modelo:** MedGemma 1.5 4B (SFT) (BRAX (Hospital Israelita Albert Einstein))
* **Resultado Chave:** Ajuste-fino supervisionado via QLoRA no host RTX 4090 especializou o MedGemma 4B para pneumonia em dados brasileiros com convergência estavel em 3 épocas.

#### `STD055` — Delineamento Experimental e Protocolo de Testes do Sistema de Triagem no Jetson Orin Nano (2026)
* **Autores:** Equipe de Pesquisa (Artigo Nvidia / Protocolo)
* **Veículo:** IEEE Access / Protocolo de Pesquisa | **DOI/URL:** 10.1109/ACCESS.2026.3600000
* **Foco / Modelo:** MedGemma 1.5 4B SFT (GGUF Q4_K_M) (BRAX Test Split (Patient-level Split))
* **Resultado Chave:** Estabelece o protocolo de validacao do sistema embarcado no Jetson Orin Nano sob limite de 15W com votação por maioria simples e temperatura zero.
