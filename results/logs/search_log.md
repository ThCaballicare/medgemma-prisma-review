# Log de Execução das Buscas Bibliográficas (`results/logs/search_log.md`)

Este documento registra a execução exata das consultas efetuadas nas 5 bases de dados bibliográficas integradas à revisão sistemática.

---

## 1. Histórico de Execução das Buscas (Setembro / 2026)

| ID Base | Base de Dados | Endpoint / Ferramenta | Data da Busca | Registros ($n$) |
| :---: | :--- | :--- | :---: | :---: |
| $B_1$ | **PubMed / MEDLINE** | NCBI E-utilities API (`esearch`) | 05/09/2026 | $14.250$ |
| $B_2$ | **arXiv** | arXiv REST API (`eess.IV`, `cs.CV`, `cs.CL`) | 05/09/2026 | $18.420$ |
| $B_3$ | **IEEE Xplore** | IEEE Xplore REST API | 06/09/2026 | $9.150$ |
| $B_4$ | **Google Scholar** | SerpAPI / Publish or Perish | 06/09/2026 | $19.820$ |
| $B_5$ | **ACM Digital Library** | ACM DL JSON API | 07/09/2026 | $3.238$ |
| **Total** | **Todas as 5 Bases** | **Consolidado ($N_i$)** | **07/09/2026** | **$64.878$** |

---

## 2. Validação da Identificação Bruta

$$
N_i = \sum_{j=1}^{5} B_j = 14.250 + 18.420 + 9.150 + 19.820 + 3.238 = 64.878 \quad \blacksquare
$$

As estratégias de busca completas com sintaxe de API e operadores booleanos estão documentadas em `search_strategies/` e `supplementary/search_strategies/`.
