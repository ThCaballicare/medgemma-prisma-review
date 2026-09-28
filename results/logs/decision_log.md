# Diário de Decisões Metodológicas (`results/logs/decision_log.md`)

Este documento registra as decisões formais tomadas durante a concepção, condução e refinamento do protocolo de revisão sistemática de literatura.

---

## Registro Histórico de Decisões

### `DEC-001` — Adoção do Fluxo PRISMA de Saída Dupla (Dual-Output)
* **Data:** 10/09/2026
* **Contexto:** Necessidade de separar estudos focados em fundamentação teórica/clínica daqueles focados em engenharia de software e hardware de borda.
* **Decisão:** O corpus final de $N_f = 55$ estudos foi particionado em **Referencial da Dissertação ($N_{f1} = 53$)** e **Referencial do Sistema ($N_{f2} = 2$)**.
* **Impacto:** Permite análises direcionadas sem misturar métricas de acurácia radiológica com benchmarks de throughput físico de GPU/NPU.

### `DEC-002` — Fixação do Target de Hardware Edge e Perfil Energético
* **Data:** 12/09/2026
* **Contexto:** Diversidade de dispositivos de borda na literatura (Raspberry Pi, Jetson Nano, Smartphones).
* **Decisão:** Padronizar os testes experimentais e a análise do sistema na plataforma **NVIDIA Jetson Orin Nano (8 GB VRAM)** sob restrição estrita de energia (**15W**) e motor `llama.cpp`.
* **Impacto:** Estabelece um baseline realista e replicável para ambientes hospitalares e radiologia de campo sem conectividade com a nuvem.

### `DEC-003` — Seleção do Dataset BRAX para Validação Diagnóstica
* **Data:** 15/09/2026
* **Contexto:** Necessidade de validar modelos de linguagem visual em dados radiológicos de língua portuguesa.
* **Decisão:** Incorporar o dataset **BRAX do Hospital Albert Einstein** (com subset validado de 148 exames com diagnóstico de pneumonia).
* **Impacto:** Garante avaliação clínica contextualizada para o cenário hospitalar brasileiro.

### `DEC-004` — Reestruturação do Diretório `results/`
* **Data:** 27/09/2026
* **Contexto:** Necessidade de separar produtos visuais/anexos dos logs operacionais de auditoria.
* **Decisão:** Criar as subpastas `results/figures/`, `results/appendix/` e `results/logs/`.
* **Impacto:** Elimina a duplicação da fonte da verdade e assegura auditabilidade rigorosa.
