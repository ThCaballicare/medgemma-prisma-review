# Material Suplementar (`supplementary/`)

Este diretório armazena os **materiais suplementares e documentação complementar** da Revisão Sistemática da Literatura (RSL) sobre a otimização e execução local de **Vision-Language Models (VLMs)** em radiologia.

O objetivo desta pasta é assegurar a **transparência metodológica absoluta** e a **rastreabilidade auditável**, disponibilizando insumos detalhados que expandem o texto principal e a documentação essencial mantida em `docs/`.

---

## 1. Regra de Distinção Metodológica: `docs/` vs. `supplementary/`

Para manter a organização conceitual e a clareza do repositório, aplica-se a seguinte diretriz de separação:

* **`docs/` (Documentação Metodológica Principal):** Contém as diretrizes e explicações **essenciais para a compreensão do método** (protocolo, critérios de inclusão/exclusão $CI/CE$, ambiente computacional e guia de reprodutibilidade).
* **`supplementary/` (Material Suplementar e Transparência):** Contém **materiais complementares que aumentam a transparência** (strings de busca brutas completas, sintaxes de consulta específicas por base, tabelas sintéticas expandidas, logs brutos de parsing e guias auxiliares).

```text
┌─────────────────────────────────────────────────────────────────────────┐
│                        REPOSITÓRIO CIENTÍFICO                           │
├───────────────────────────────────┬─────────────────────────────────────┤
│             docs/                 │           supplementary/            │
│  (Método Principal e Essencial)   │  (Transparência e Suporte Expandido)│
├───────────────────────────────────┼─────────────────────────────────────┤
│ • Protocolo formal PRISMA 2020    │ • Strings brutas completas de busca │
│ • Critérios formais CI / CE       │ • Sintaxes por sintaxe de API/base  │
│ • Especificação do Ambiente       │ • Tabelas suplementares expandidas  │
│ • Guia Geral de Reprodutibilidade │ • Logs de parsing e artefatos extra │
└───────────────────────────────────┴─────────────────────────────────────┘
```

---

## 2. Estrutura Conceitual do Diretório

A estrutura de `supplementary/` é organizada conceitualmente nos seguintes eixos e subdiretórios:

```text
supplementary/
├── README.md                   # Guia de governança e índice de materiais suplementares
├── search_strategies/          # Estratégias e strings de busca brutas e exaustivas por base
├── supplementary_tables/       # Tabelas suplementares de síntese, acurácia e telemetria
└── supplementary_material/     # Documentos auxiliares, formulários de auditoria e mapas de atributos
```

---

## 3. Mapeamento dos Conteúdos Suplementares

### 3.1 Estratégias Exaustivas de Busca (`search_strategies/`)
Armazena a íntegra das strings de consulta, parâmetros de campos e blocos booleanos executados em cada um dos 5 indexadores bibliográficos consultados ($N_i = 64.878$):
* **PubMed / MEDLINE ($B_1 = 14.250$):** String Mesh/tiab completa dividida nos blocos $Q_1$ (multimodalidade/radiologia), $Q_2$ (execução edge/quantização) e $Q_3$ (MedGemma).
* **arXiv ($B_2 = 18.420$):** Consultas por API com delimitadores de categoria (`cs.CV`, `cs.CL`, `eess.IV`).
* **IEEE Xplore ($B_3 = 9.150$):** Expressão booleana parametrizada para campos de metadados.
* **Google Scholar ($B_4 = 19.820$):** Consultas de caixa de busca adaptadas para janelas temporais de 2020 a 2026.
* **ACM Digital Library ($B_5 = 3.238$):** Filtros estruturados para conferências de AI/ML e sistemas embarcados.

### 3.2 Tabelas Suplementares (`supplementary_tables/`)
* **Tabela S1 (Distribuição Temporal e Temática):** Matriz expandida cruzando ano de publicação, modelo base e dataset.
* **Tabela S2 (Métricas Detalhadas do BRAX):** Mapeamento do subset de validação em português com 148 exames e rotulagem por PLN.
* **Tabela S3 (Telemetria Física e Perfomance Edge):** Medições detalhadas de latência (tempo até primeiro token, vazão de tokens/s), pico de memória VRAM unificada no NVIDIA Jetson Orin Nano de 8 GB sob limite estrito de **15W** (comparando quantizações AWQ e `Q4_K_M` GGUF via `llama.cpp`).

### 3.3 Materiais Auxiliares (`supplementary_material/`)
* **Dicionários Expandidos:** Mapeamento conceitual do formulário de extração (26 variáveis).
* **Logs de Arbitragem:** Registro completo das reuniões de consenso entre revisores independentes para a fase de elegibilidade ($N_{full} = 59 ightarrow 4$ descartes $ightarrow N_f = 55$).

---

## 4. Validação e Consistência com o PRISMA v8 (Saída Dupla)

Todo o material suplementar mantido nesta pasta está rigorosamente alinhado ao funil de seleção e às equações de controle do protocolo:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A} \implies 55 = 64.878 - 9.475 - 55.258 - 86 - 4 \quad lacksquare
$$

Com a classificação final de Saída Dupla do corpus ($N_f = 55$):
* **Referencial da Dissertação ($N_{f1} = 53$ estudos / $96,36\%$):** Suporte teórico de baselines clínicas, engenharia de prompt *Reason-then-Summarize* (CoT) e calibração diagnóstica.
* **Referencial do Sistema ($N_{f2} = 2$ estudos / $3,64\%$):** Suporte técnico de engenharia de software e hardware para testes físicos a 15W no Jetson Orin Nano (LIN et al., 2024; HASSIJA et al., 2026).

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies 55 = 53 + 2 \quad lacksquare
$$

---

## 5. Instruções de Uso e Reprodutibilidade

Para consultar ou reutilizar os materiais suplementares:
1. **Auditoria de Buscas:** Acesse `search_strategies/` para obter a cópia exata do texto das strings prontas para execução nos portais das bases.
2. **Análise de Métricas:** Consulte `supplementary_tables/` para visualizar as matrizes de dados numéricos em formato `.csv` e `.md`.
3. **Verificação de Consistência:** Utilize os scripts em `analysis/scripts/` para validar se os quantitativos citados nos materiais suplementares permanecem 100% sincronizados com a base do repositório.
