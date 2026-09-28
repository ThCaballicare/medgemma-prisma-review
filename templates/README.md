# Modelos e Gabaritos Padronizados (`templates/`)

Este diretório contém os **modelos neutros, gabaritos e esquemas estruturados reutilizáveis** projetados para padronizar a coleta, organização, triagem, extração de dados e auditoria quantitativa da Revisão Sistemática da Literatura (RSL) sobre **Vision-Language Models (VLMs)** em radiologia e computação de borda (*edge computing*).

Os artefatos deste diretório funcionam como esquemas (*schemas*) de referência para garantir a reprodutibilidade, consistência de campos e alinhamento com o protocolo **PRISMA 2020 (v8 - Saída Dupla)**.

---

## 1. Finalidade do Diretório

A pasta `templates/` desempenha um papel central na governança de dados do repositório:

1. **Padronizar a Entrada de Dados:** Fornece cabeçalhos e tipos de dados predefinidos para evitar variações de nomenclatura durante as fases do projeto.
2. **Garantir Reprodutibilidade e Reutilização:** Permite que outros pesquisadores apliquem a mesma estrutura metodológica em revisões sistemáticas derivadas ou futuras.
3. **Separar Modelos de Dados Efetivamente Produzidos:** Garante a distinção clara entre a *estrutura abstrata* (modelo/gabarito) e os *dados empíricos preenchidos* gerados durante o estudo.

---

## 2. Descrição dos Templates e Campos

### 2.1 `extraction_template.csv`

* **Diretório Alvo:** `extraction/` (`extraction_form.csv` / `extracted_data.csv`)
* **Finalidade:** Servir como modelo estruturado para a extração detalhada de evidências dos estudos incluídos no corpus final ($N_f = 55$).
* **Campos Mapeados (26 variáveis):**
  * `record_id`: Identificador único do estudo (`STD001` a `STD055` / `REC001` a `REC055`).
  * `title`: Título completo da publicação.
  * `authors`: Lista de autores.
  * `year`: Ano de publicação (2020–2026).
  * `doi`: Digital Object Identifier ou URL de acesso.
  * `venue`: Periódico, conferência ou repositório de publicação.
  * `study_type`: Tipo de estudo (experimental, benchmark, revisão, etc.).
  * `clinical_domain`: Domínio clínico (ex.: radiologia de tórax, pneumologia).
  * `imaging_modality`: Modalidade de imagem médica (ex.: CXR, CT, MRI).
  * `dataset`: Base de dados utilizada (ex.: BRAX, MIMIC-CXR, CheXpert).
  * `dataset_size`: Tamanho da amostragem / número de exames e laudos.
  * `model`: Nome do modelo investigado (ex.: MedGemma 1.5 4B, RadVLM, CheXagent).
  * `model_family`: Família de arquitetura (ex.: Gemma, Llama, ViT).
  * `vision_language`: Encoder de visão e conector (ex.: MedSigLIP, CLIP, EVA).
  * `task`: Tarefa clínica (ex.: triagem de pneumonia, report generation, VQA).
  * `training_strategy`: Estratégia de treino (ex.: SFT, zero-shot, RLHF).
  * `fine_tuning`: Método de ajuste fino (ex.: QLoRA, LoRA, Full).
  * `quantization`: Esquema de quantização (ex.: AWQ, PTQ 4-bit NF4, GGUF Q4_K_M).
  * `edge_computing`: Indicador de execução em borda (`Sim`/`Não`/`Híbrido`).
  * `hardware`: Plataforma de hardware (ex.: NVIDIA Jetson Orin Nano 15W, RTX 4090).
  * `inference_framework`: Framework de inferência (ex.: `llama.cpp`, vLLM, Ollama).
  * `evaluation_metrics`: Métricas de avaliação (ex.: F1-score, RadGraph F1, VRAM, Latência).
  * `main_results`: Resultados quantitativos e achados principais.
  * `limitations`: Limitações reportadas pelos autores.
  * `relevance_to_review`: Categoria de Saída Dupla (`Referencial da Dissertação` / `Referencial do Sistema`).
  * `notes`: Observações adicionais e notas do revisor.

---

### 2.2 `screening_template.csv`

* **Diretório Alvo:** `screening/` (`identified.csv`, `deduplicated.csv`, `title_abstract.csv`, `full_read.csv`)
* **Finalidade:** Fornecer um modelo unificado para o acompanhamento dos registros em todas as fases de filtragem do funil PRISMA (da identificação à leitura completa).
* **Campos Mapeados:**
  * `record_id`: Identificador sequencial do registro.
  * `paper_name`: Nome do arquivo de artigo/PDF ou identificador de documento.
  * `title`: Título do registro recuperado.
  * `authors`: Lista de autores.
  * `year`: Ano de publicação.
  * `source_database`: Base de dados de origem (PubMed, arXiv, IEEE Xplore, Google Scholar, ACM).
  * `is_duplicate`: Flag booleana de duplicata (`True`/`False`).
  * `title_abstract_status`: Decisão na triagem de título e resumo (`Included`/`Excluded`).
  * `full_text_status`: Status de recuperação e leitura em texto completo (`Retrieved`/`Excluded`).
  * `exclusion_reason`: Código ou justificativa de exclusão conforme critérios formais.
  * `final_decision`: Decisão final de elegibilidade (`Included`/`Excluded`).
  * `dual_output_category`: Categoria de Saída Dupla no corpus incluído (`Referencial da Dissertação` / `Referencial do Sistema`).

---

### 2.3 `prisma_statistics_template.csv`

* **Diretório Alvo:** `prisma/` / `analysis/statistics/` (`prisma_flow.csv`, `prisma_validation.csv`, `search_distribution.csv`)
* **Finalidade:** Servir como modelo para compilação das estatísticas descritivas, taxas de retenção/rejeição e equações de auditoria do funil PRISMA v8.
* **Campos Mapeados:**
  * `stage_id`: Identificador numérico da etapa no funil (1 a 11).
  * `stage_name`: Denominação formal da etapa metodológica.
  * `symbol`: Símbolo matemático correspondente ($N_i$, $D$, $N_1$, $T_1$, $N_2$, $T_2$, $N_{full}$, $A$, $N_f$, $N_{f1}$, $N_{f2}$).
  * `count`: Quantidade de registros no estágio ($n$).
  * `retention_rate_pct`: Taxa percentual de retenção em relação ao estágio anterior.
  * `rejection_rate_pct`: Taxa percentual de rejeição/descarte em relação ao estágio anterior.
  * `description`: Descrição explicativa do processo realizado na etapa.
  * `validation_formula`: Expressão matemática de validação da etapa.

---

## 3. Relação com os Diretórios do Repositório

O diagrama abaixo ilustra como os modelos neutros de `templates/` originam os dados preenchidos e validados nos respectivos diretórios do projeto:

```text
templates/
│
├── extraction_template.csv ─────────► extraction/
│                                      ├── extraction_form.csv
│                                      └── extracted_data.csv
│
├── screening_template.csv ──────────► screening/ & studies/
│                                      ├── identified-v8.csv
│                                      ├── deduplicated-v8.csv
│                                      ├── title_abstract-v8.csv
│                                      ├── full_read-v8.csv
│                                      └── included_studies.csv
│
└── prisma_statistics_template.csv ──► prisma/ & analysis/statistics/
                                       ├── prisma_flow.csv
                                       ├── prisma_validation.csv
                                       └── search_distribution.csv
```

---

## 4. Diferença entre Template e Dado Efetivamente Produzido

| Conceito | `templates/` (Modelo / Gabarito) | Dados Produzidos (`extraction/`, `screening/`, `prisma/`) |
| :--- | :--- | :--- |
| **Natureza** | Estrutural, abstrata e neutra. | Empírica, concreta e preenchida. |
| **Conteúdo** | Apenas cabeçalhos de colunas e máscaras de preenchimento (`[STD_ID]`, `[Title]`). | Valores reais extraídos das 55 fontes científicas ($N_f = 55$). |
| **Mutabilidade** | Fixo e imutável durante a execução da RSL. | Atualizado dinamicamente conforme os testes e a síntese progridem. |
| **Função no Projeto** | Garantir a padronização e o contrato de dados (*schema contract*). | Fornecer a evidência científica para o artigo e a dissertação. |

---

## 5. Validação Matemática da Estrutura

Os templates de estatísticas (`prisma_statistics_template.csv`) incorporam a validação determinística da equação de controle global do protocolo **PRISMA v8 (Saída Dupla)**:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad lacksquare
$$

E a composição conservativa de Saída Dupla:

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies \mathbf{55} = \mathbf{53} + \mathbf{2} \quad lacksquare
$$
