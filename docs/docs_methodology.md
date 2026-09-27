# Metodologia da Revisão Sistemática (`docs/methodology.md`)

Este documento detalha o método científico adotado na Revisão Sistemática da Literatura (RSL) sobre a execução local e otimização de **Vision-Language Models (VLMs)** em radiologia, conduzida sob o protocolo **PRISMA 2020 (v8 - Saída Dupla)**.

---

## 1. Identificação e Estratégia de Busca

A etapa de identificação englobou buscas sistemáticas em **5 bases de dados bibliográficas globais**, retornando um total inicial de **$N_i = 64.878$ registros brutos**:

| Base de Dados                  | Identificador ($B_j$) | Registros ($n$) | Foco de Cobertura da Base                              |
| :----------------------------- | :-------------------: | :-------------: | :----------------------------------------------------- |
| **Google Scholar**             |         $B_4$         |    $19.820$     | Literatura cinzenta, preprints e citações abrangentes  |
| **arXiv**                      |         $B_2$         |    $18.420$     | Repositório aberto de IA (categorias `cs.CV`, `cs.CL`) |
| **PubMed / MEDLINE**           |         $B_1$         |    $14.250$     | Literatura biomédica e clínica indexada                |
| **IEEE Xplore**                |         $B_3$         |     $9.150$     | Engenharia biomédica, hardware e sistemas embarcados   |
| **ACM Digital Library**        |         $B_5$         |     $3.238$     | Computação, arquiteturas de sistemas e otimização      |
| **Total Identificado ($N_i$)** |      $\sum B_j$       |  **$64.878$**   | **Corpus bruto inicial**                               |

---

## 2. Strings e Blocos de Consulta

As expressões de busca foram estruturadas em três blocos conceituais e adaptadas às sintaxes de cada base:

- **Bloco $Q_1$ (Multimodalidade e Radiologia):** `"Vision-Language Model" OR "VLM" OR "Multimodal LLM" OR "MedGemma" AND "Radiology" OR "Chest X-Ray" OR "CXR" OR "Pneumonia"`.
- **Bloco $Q_2$ (Execução Local e Borda):** `"Edge Computing" OR "On-Device Inference" OR "Offline" OR "llama.cpp" OR "Quantization" OR "AWQ" OR "GGUF" OR "Embedded System"`.
- **Bloco $Q_3$ (Específico MedGemma):** `"MedGemma" OR "MedSigLIP"`.

A combinação booleana de consulta seguiu a lógica:

$$
	ext{Query Final} = (Q_1 	ext{ AND } Q_2) 	ext{ OR } Q_3
$$

---

## 3. O Funil de Seleção PRISMA v8

```text
64.878 Registros Identificados Brutos (N_i)
   │
   ▼ Remoção de D = 9.475 duplicatas
55.403 Registros Únicos para Triagem Inicial (N_1)
   │
   ▼ Exclusão de T_1 = 55.258 na Triagem de Título/Resumo (Coarse Screening)
  145 Selecionados para Triagem Detalhada (N_2)
   │
   ▼ Exclusão de T_2 = 86 resumos na Triagem Detalhada (Detailed Screening)
   59 Artigos Recuperados para Leitura Completa (N_full)
   │
   ▼ Exclusão de A = 4 relatórios na Elegibilidade em Texto Completo
   55 Estudos Científicos Incluídos (N_f)
   ├── 53 Estudos ➔ Referencial da Dissertação (N_f1: Suporte Teórico)
   └──  2 Estudos ➔ Referencial do Sistema (N_f2: Suporte Técnico de Engenharia)
```

---

## 4. Classificação de Saída Dupla (_Dual-Output Flow_)

Na fase final de inclusão, os **$N_f = 55$ estudos** foram bifurcados segundo a função metodológica no repositório:

1. **Referencial da Dissertação ($N_{f1} = 53$ estudos / $96,36\%$):** Fundamentação teórica, modelos de fundação (MedGemma 1.5), baselines clínicas de radiografia de tórax (BRAX do Albert Einstein, MIMIC-CXR, CheXpert), calibração, engenharia de prompt _Reason-then-Summarize_ (CoT) e mitigação de alucinações.
2. **Referencial do Sistema ($N_{f2} = 2$ estudos / $3,64\%$):** Suporte técnico direto e testes físicos de telemetria em hardware edge restrito a **15W** na placa NVIDIA Jetson Orin Nano 8GB, utilizando quantização AWQ e dequantização dinâmica em C++ via `llama.cpp` (LIN et al., 2024; HASSIJA et al., 2026).

---

## 5. Validação Matemática de Consistência

\[
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A} \implies 55 = 64.878 - 9.475 - 55.258 - 86 - 4 \quad \blacksquare
\]

\[
\mathbf{N*f} = \mathbf{N*{f1}} + \mathbf{N\_{f2}} \implies 55 = 53 + 2 \quad \blacksquare
\]
