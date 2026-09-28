# Log Operacional de Triagem e Elegibilidade (`results/logs/screening_log.md`)

Este documento registra os quantitativos, critérios aplicados e deliberações de arbitragem durante o funil de seleção de literatura.

---

## 1. Funil Operacional de Seleção

```text
Identificados Brutos (N_i = 64.878)
   │
   ▼ Deduplicação (-9.475)
Únicos para Triagem (N_1 = 55.403)
   │
   ▼ Triagem Inicial / Coarse (-55.258)
Selecionados Título/Resumo (N_2 = 145)
   │
   ▼ Triagem Detalhada / Detailed (-86)
Recuperados Leitura Completa (N_full = 59)
   │
   ▼ Elegibilidade / Texto Completo (-4)
Estudos Incluídos Final (N_f = 55)
```

---

## 2. Registro de Exclusões na Leitura Completa ($A = 4$)

| ID Exclusão | Título / Estudo | Motivo da Exclusão | Critério |
| :---: | :--- | :--- | :---: |
| `EXC_FULL_01` | *Interactive Web-based Image Viewer for CXR Annotation* | Ferramenta utilitária de anotação sem modelo VLM ou inferência local | $CE3$ |
| `EXC_FULL_02` | *Cloud-native Multi-hospital Diagnostic Pipeline* | Arquitetura com dependência estrita de nuvem sem suporte a edge | $CE4$ |
| `EXC_FULL_03` | *Educational Tutorial on Radiology Image Parsing* | Relatório tutorial sem dados de validação empírica ou clínica | $CE3$ |
| `EXC_FULL_04` | *Duplicate Abstract from Regional Conference* | Registro duplicado residual identificado na leitura do texto integral | $CE1$ |

---

## 3. Log de Arbitragem entre Revisores

* **Sessão 1 (18/09/2026):** Avaliação de concordância entre Revisor A e Revisor B.
* **Consenso:** 53 estudos acordados imediatamente; 2 estudos (`REC023` Hassija et al., 2026 e `REC038` Lin et al., 2024 - AWQ) reclassificados por unanimidade para a vertente **Referencial do Sistema ($N_{f2} = 2$)**.
