# Log de Inclusão e Elegibilidade do Corpus (`studies/study_log.md`)

Este documento registra a auditoria detalhada e a rastreabilidade do processo de seleção dos **55 estudos científicos incluídos** no corpus final da Revisão Sistemática da Literatura (RSL), em estrita conformidade com o protocolo **PRISMA 2020 (v8 - Saída Dupla)**.

---

## 1. Histórico de Leitura Integral e Descarte de Elegibilidade

A fase de elegibilidade iniciou-se com **59 relatórios recuperados em texto completo** ($N_{full} = 59$) resultantes da etapa de triagem fina manual de resumos. A avaliação independente por dupla revisão identificou e descartou **4 registros não científicos**, conforme detalhado a seguir:

### Tabela de Exclusões na Leitura Completa ($A = 4$ registros)

| ID Registro | Título do Relatório Avaliado | Ano | Motivo Formal da Exclusão ($A$) | Impacto na Elegibilidade |
| :---: | :--- | :---: | :--- | :--- |
| `EXC_FULL_01` | *Interactive Web-based Image Viewer for CXR Annotation* | 2024 | Ferramenta utilitária web de anotação sem modelo VLM ou experimento de inferência. | Descartado |
| `EXC_FULL_02` | *Deployment Tutorial for Ollama on Consumer Hardware* | 2025 | Tutorial prático de blog sem metodologia acadêmica ou avaliação de métricas. | Descartado |
| `EXC_FULL_03` | *API Wrapper for Commercial Cloud Medical Vision Services* | 2025 | Dependência estrita de API em nuvem paga sem viabilidade de execução offline. | Descartado |
| `EXC_FULL_04` | *Duplicata residual de parsing do repositório arXiv* | 2025 | Versão anterior preliminar já contemplada em artigo completo incluído. | Descartado |

---

## 2. Validação da Formação do Corpus Final

Com a exclusão dos 4 registros descritos, o corpus final de estudos incluídos ($N_f$) estabilizou em **55 estudos científicos**:

$$
\mathbf{N_f} = \mathbf{N_{full}} - \mathbf{A} \implies 59 - 4 = 55 \quad \blacksquare
$$

### Alocação de Saída Dupla (*Dual-Output Allocation*)

Durante a fase de inclusão, a dupla de revisores classificou cada um dos 55 estudos conforme a sua relevância metodológica para o projeto:

1. **Referencial da Dissertação ($N_{f1} = 53$ estudos / $96,36\%$):** Artigos selecionados para fundamentação do artigo principal, diagnóstico de pneumonia, análise do dataset BRAX, prompts CoT e calibração.
2. **Referencial do Sistema ($N_{f2} = 2$ estudos / $3,64\%$):** Artigos selecionados para suporte direto de engenharia de software e hardware de borda (LIN et al., 2024; HASSIJA et al., 2026).

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies 53 + 2 = 55 \quad \blacksquare
$$

---

## 3. Rastreabilidade com os Demais Diretórios

* Cada `study_id` (`STD001` a `STD055`) mapeia diretamente 1:1 para o `record_id` (`REC001` a `REC055`) em `extraction/extracted_data.csv`.
* Todos os 55 estudos possuem registros completos e normalizados na pasta `bibliography/` (`references.bib`, `references.csv`, `references.ris`).
* A consistência dos 55 estudos é verificada pelas equações globais em `prisma/consistency_check.md` e `analysis/statistics/prisma_validation.csv`.