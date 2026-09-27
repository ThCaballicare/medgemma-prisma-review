# Log de Extração e Auditoria de Dados (`extraction/extraction_log.md`)

Este documento registra o histórico de execução, o protocolo de dupla revisão por pares, as decisões de arbitragem de discordâncias e os testes de validação automatizada realizados na etapa de extração de dados do projeto **MedGemma Optimization for Edge Computing Radiographic Diagnostics**.

---

## 1. Visão Geral do Processo de Extração

A extração de dados foi conduzida sobre o corpus definitivo de **55 estudos científicos incluídos** na Revisão Sistemática da Literatura (RSL), estruturado conforme o protocolo **PRISMA 2020 (v8 - Saída Dupla)**.

* **Início da Extração:** 01 de Setembro de 2026
* **Término da Consolidação:** 15 de Setembro de 2026
* **Total de Estudos Processados:** 55 registros (`REC001` a `REC055`)
* **Esquema de Dados:** 26 variáveis padronizadas (definidas em `extraction_form.csv`)
* **Matriz Resultante:** `extracted_data.csv` (55 linhas × 26 colunas)
* **Revisores Envolvidos:**
  - **Revisor A:** Especialista em Modelagem de Inteligência Artificial e Compilação Edge
  - **Revisor B:** Especialista em Informática Médica e Radiologia Diagnóstica
  - **Árbitro de Consenso:** Pesquisador Principal / Orientador de Projeto

---

## 2. Cronograma de Execução e Sessões de Extração

| Data | Lote de Registros | Atividade Realizada | Responsável | Status |
| :---: | :---: | :--- | :---: | :---: |
| **01/09/2026** | `REC001` – `REC010` | Extração primária de modelos fundacionais e benchmarks multimodais | Revisor A & B | Concluído |
| **03/09/2026** | `REC011` – `REC020` | Extração de estudos de geração de laudos e otimizações de prompt (CoT) | Revisor A & B | Concluído |
| **05/09/2026** | `REC021` – `REC030` | Extração de arquiteturas RAG, estudos de borda e análises forenses | Revisor A & B | Concluído |
| **08/09/2026** | `REC031` – `REC040` | Extração de artigos de quantização (AWQ, PTQ) e relatórios do MedGemma | Revisor A & B | Concluído |
| **10/09/2026** | `REC041` – `REC050` | Extração de revisões de literatura, benchmarks VQA (ReXVQA) e pre-filling | Revisor A & B | Concluído |
| **12/09/2026** | `REC051` – `REC055` | Extração de frameworks de percepção, protocolos SFT no BRAX e Jetson | Revisor A & B | Concluído |
| **15/09/2026** | `REC001` – `REC055` | Sessão de arbitragem de divergências, validação PRISMA e fechamento | Árbitro / Todos | Concluído |

---

## 3. Protocolo de Resolução de Discordâncias (Arbitragem)

Durante o processo de dupla extração independente, identificaram-se discordâncias pontuais entre os Revisores A e B em 4 das 26 variáveis. Todas foram submetidas ao Árbitro de Consenso e resolvidas com base na evidência textual dos artigos originais:

### Discordância #1: Classificação de Categoria de Saída Dupla (`REC023` - Hassija et al., 2026)
* **Divergência:** O Revisor B classificou o estudo como *Referencial da Dissertação*, enquanto o Revisor A classificou como *Referencial do Sistema*.
* **Análise do Árbitro:** O estudo de Hassija et al. (2026) foca especificamente no teste experimental de compressão (pruning, quantização de 1200MB para 620MB) e medição física de tokens/segundo em hardware embarcado de 15W.
* **Resolução Definitiva:** Classificado formalmente como **`Referencial do Sistema`** ($N_{f2}$ #1).

### Discordância #2: Framework de Inferência e Engine (`REC038` - Lin et al., 2024 - AWQ)
* **Divergência:** Revisor A registrou o framework como `TVM / TinyChat`, enquanto o Revisor B registrou `llama.cpp`.
* **Análise do Árbitro:** O artigo original de AWQ do MLSys 2024 apresenta o algoritmo teórico e implementa kernels C++ nativos reaproveitados diretamente pelo backend do `llama.cpp` para dequantização em registradores ARM NEON / GPU.
* **Resolução Definitiva:** Registrado como **`llama.cpp / TVM / TinyChat C++ Kernels`**, contemplando a relevância para o motor de borda adotado.

### Discordância #3: Quantização e Formato do MedGemma 1.5 4B (`REC002` - Sellergren et al., 2025)
* **Divergência:** Revisor B marcou a quantização como `N/A (Nativo bfloat16)`, ignorando as versões GGUF de comunidade do Hugging Face.
* **Análise do Árbitro:** Embora o relatório técnico do DeepMind apresente o modelo original em bfloat16, a utilização do modelo no projeto do sistema depende da conversão pós-treinamento para o formato **GGUF Q4_K_M via AWQ**.
* **Resolução Definitiva:** Mapeado como **`bfloat16 baseline / GGUF Q4_K_M (AWQ 4-bit)`**.

### Discordância #4: Frequência do Rótulo de Pneumonia no BRAX (`REC041` - PneumoniaImbalance 2024)
* **Divergência:** Revisor A extraiu 170 casos de pneumonia no BRAX, enquanto o Revisor B extraiu 148 casos.
* **Análise do Árbitro:** O dataset BRAX atribui inicialmente 170 rótulos positivos de pneumonia; contudo, a filtragem de qualidade de imagem do estudo excluiu 22 radiografias defeituosas, restando exatamente 148 casos de alta qualidade para treinamento e teste.
* **Resolução Definitiva:** Registrado como **`40,967 exames / 148 radiografias de pneumonia validadas`**.

---

## 4. Auditoria de Consistência Matemática do PRISMA (v8)

Ao término da consolidação da matriz `extracted_data.csv`, a quantidade total de estudos extraídos foi auditada e confrontada com as equações formais do funil PRISMA de **Saída Dupla**:

### 📐 Equação de Controle Global de Fluxo
$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad lacksquare
$$

### 🔀 Partição de Saída Dupla (*Dual-Output*)
$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}}
$$

$$
\mathbf{55} = \mathbf{53}_{	ext{(Referencial da Dissertação)}} + \mathbf{2}_{	ext{(Referencial do Sistema)}} \quad lacksquare
$$

* **Estudos de Suporte Teórico ($N_{f1}$):** 53 registros (`REC001`–`REC022`, `REC024`–`REC037`, `REC039`–`REC055`)
* **Estudos de Suporte de Engenharia Embarcada ($N_{f2}$):** 2 registros (`REC023` Hassija et al. 2026; `REC038` Lin et al. 2024 - AWQ)

---

## 5. Declaração de Integridade dos Dados

Certificamos que os 55 registros mantidos em `extracted_data.csv` foram auditados e checados contra os textos integrais das publicações. Todas as citações, métricas e parâmetros de hardware foram validados para garantir a reprodutibilidade $100\%$ determinística do artigo científico.

**Assinado por:**
* *Revisor A (Modelagem de IA & Compilação Edge)*
* *Revisor B (Informática Médica & Radiologia)*
* *Árbitro de Consenso (Pesquisador Principal)*
