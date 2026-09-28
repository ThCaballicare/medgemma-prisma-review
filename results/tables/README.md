# Tabelas Finais do Artigo (`results/tables/`)

Este diretório armazena e documenta as **tabelas consolidadas finais** produzidas a partir dos dados da revisão sistemática, prontas para inclusão no artigo científico, dissertação e materiais de divulgação.

Da mesma forma que o diretório `results/figures/`, este espaço funciona exclusivamente como a **camada de apresentação tabular final**, separada do processamento de dados efetuado em `analysis/` e `extraction/`.

---

## 1. Regra de Governança e Separação de Responsabilidades

```text
       analysis/ / extraction/
 (Extração de variáveis, agregação estatística e cálculo de métricas)
                   │
                   ▼
            results/tables/
 (Tabelas finais formatadas em Markdown, CSV e LaTeX com booktabs)
                   │
                   ▼
       Manuscrito / Dissertação / Artigo
```

* **Cálculos e Agregações (`analysis/`):** Os scripts de computação, filtros de dados e tabelas brutas intermediárias pertencem estritamente às pastas `analysis/` e `extraction/`.
* **Apresentação Final (`results/tables/`):** Abriga apenas as tabelas formatadas em sua versão final, nos formatos `.csv` (dados estruturados), `.md` (visualização rápida no GitHub) e `.tex` (código LaTeX para compilação do artigo).

---

## 2. Catálogo das Tabelas do Artigo

As tabelas finais catalogadas nesta pasta atendem diretamente às Perguntas de Pesquisa (RQs) do projeto:

| Arquivo da Tabela | Título / Descrição Metodológica | Formatos | Pergunta Atendida |
| :--- | :--- | :---: | :---: |
| **`table1_study_characteristics`** | **Caracterização Geral do Corpus ($N_f = 55$):** Síntese dos estudos por modalidade de imagem (CXR), tarefas clínicas, família de modelos e estratégia de treino. | `.csv`, `.md`, `.tex` | Visão Geral |
| **`table2_clinical_accuracy_brax`** | **Acurácia Clínica no Dataset BRAX:** Desempenho do MedGemma 1.5 4B no dataset do Hospital Albert Einstein vs. baselines (RadGraph F1, CheXbert F1, GREEN Metric). | `.csv`, `.md`, `.tex` | **RQ1** |
| **`table3_edge_telemetry_jetson`** | **Telemetria Física a 15W no Jetson Orin Nano:** Métricas de vazão de tokens/s, latência TTFT e consumo de VRAM (FP16 vs. AWQ 4-bit vs. GGUF `Q4_K_M`). | `.csv`, `.md`, `.tex` | **RQ2** |
| **`table4_dual_output_breakdown`** | **Mapeamento de Saída Dupla (*Dual-Output*):** Distribuição do corpus entre o Referencial da Dissertação ($N_{f1} = 53$) e o Referencial do Sistema ($N_{f2} = 2$). | `.csv`, `.md`, `.tex` | Método / PRISMA |

---

## 3. Padrões de Exportação LaTeX (`.tex`)

Todas as tabelas destinadas ao artigo em LaTeX utilizam o pacote `booktabs` para garantir tipografia acadêmica de alta qualidade:

* Sem linhas verticais (`|`);
* Linhas horizontais estritas: `\toprule`, `\midrule` e `\bottomrule`;
* Alinhamento numérico explícito e notas de rodapé de tabela centralizadas.

---

## 4. Validação e Consistência Numérica

Todas as contagens agregadas apresentadas nas tabelas finais obedecem rigorosamente à equação de controle do **PRISMA v8**:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A} \implies 55 = 64.878 - 9.475 - 55.258 - 86 - 4 \quad lacksquare
$$

E a composição de Saída Dupla:

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies 55 = 53_{	ext{(Dissertação)}} + 2_{	ext{(Sistema)}} \quad lacksquare
$$
