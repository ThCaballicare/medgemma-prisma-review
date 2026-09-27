# Ambiente Computacional e Otimização (`docs/environment.md`)

Este documento especifica o **ambiente computacional, a infraestrutura de hardware e a pilha de software** utilizados nos experimentos de fine-tuning, quantização e inferência local do modelo **MedGemma 1.5 4B**.

---

## 1. Infraestrutura de Hardware

O projeto utiliza uma arquitetura de desenvolvimento híbrida dividida em dois nós operacionais:

### 1.1 Servidor de Treinamento e Fine-Tuning (Host Server)

- **GPU:** NVIDIA RTX 4090 (24 GB VRAM GDDR6X).
- **CPU:** AMD Ryzen 9 7950X (16 cores, 32 threads).
- **Memória RAM:** 64 GB DDR5.
- **Armazenamento:** 2 TB NVMe PCIe 4.0.
- **Função no Projeto:** Fine-tuning supervisionado (SFT) do MedGemma 1.5 4B via QLoRA/LoRA em float16/bfloat16 com imagens do dataset **BRAX do Albert Einstein**.

### 1.2 Kit de Desenvolvimento de Borda (Target Edge Device)

- **Dispositivo:** NVIDIA Jetson Orin Nano Developer Kit (8 GB VRAM Unificada).
- **TDP / Limite de Energia:** **15W** (modo de energia de baixa potência).
- **Arquitetura da GPU:** NVIDIA Ampere (1024 CUDA Cores + 32 Tensor Cores).
- **CPU:** 6-core Arm Cortex-A78AE v8.2 64-bit.
- **Função no Projeto:** Execução local e offline da inferência do MedGemma 1.5 4B quantizado para triagem de pneumonia em tempo real.

---

## 2. Pilha de Software e Frameworks de Inferência

```text
       ┌─────────────────────────────────────────────────────────┐
       │   Fine-Tuning (RTX 4090): PyTorch + Unsloth + QLoRA     │
       └────────────────────────────┬────────────────────────────┘
                                    │ Exportação GGUF / AWQ
                                    ▼
       ┌─────────────────────────────────────────────────────────┐
       │     Inferência Local (Jetson Nano 15W): llama.cpp       │
       │      Kernels CUDA + Instruções SIMD ARM NEON (C++)      │
       └─────────────────────────────────────────────────────────┘
```

- **Linguagem Base:** Python 3.12 e C++20 nativo.
- **Motor de Inferência de Borda:** `llama.cpp` (compilado com suporte a CUDA e otimizações ARM NEON).
- **Formato de Modelo:** GGUF (`Q4_K_M` de 4 bits - pico de consumo de VRAM de **5,6 GB**).
- **Técnica de Quantização Pós-Treino:** AWQ (_Activation-Aware Weight Quantization_) por monitoramento de canais salientes.
- **Bibliotecas Python:** `pandas`, `numpy`, `scikit-learn`, `pypdf`, `markitdown`.

---

## 3. Soberania de Dados e Conformidade com a LGPD

A execução local no Jetson Orin Nano garante **0% de tráfego de dados para a nuvem**, garantindo total privacidade dos exames radiológicos e conformidade estrita com a **Lei Geral de Proteção de Dados (LGPD - Lei nº 13.709/2018)**.
