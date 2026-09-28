# Resultados Finais e Síntese da Revisão (`results/`)

Este diretório representa a **camada final de resultados reprodutíveis** da Revisão Sistemática da Literatura (RSL) sobre a otimização e execução do **MedGemma 1.5 4B** em ambientes de computação de borda (*edge computing*).

Seguindo o princípio de rigor científico e desacoplamento de responsabilidades, o diretório `results/` funciona como o contrato central que organiza e separa os **produtos finais do artigo** (`figures/`, `tables/`, `appendix/`) dos **registros operacionais de auditoria** (`logs/`).

---

## 1. Arquitetura Lógica e Encadeamento

O diretório `results/` consolida os dados e análises que fluem ao longo de todas as etapas anteriores do repositório:

```text
protocol/
    ↓
search_strategies/
    ↓
search_results/
    ↓
screening/
    ↓
studies/
    ↓
analysis/ / extraction/
    ↓
results/
├── README.md            # Contrato central e índice da camada de resultados
├── appendix/            # Apêndices formais e materiais suplementares
├── figures/             # Figuras, gráficos e diagramas finais
├── tables/              # Tabelas consolidadas finais (CSV, Markdown, LaTeX)
└── logs/                # Rastreabilidade operacional (decision, screening, search)
    ↓
docs/ (Artigo Final / Dissertação)
```

---

## 2. Estrutura de Subdiretórios e Papel de Cada Componente

| Diretório / Arquivo | Função Metodológica | Natureza do Conteúdo |
| :--- | :--- | :---: |
| **`results/README.md`** | Documento central e contrato de interface da camada de resultados. | Índice / Contrato |
| **`results/appendix/`** | Armazena apêndices e relatórios suplementares derivados da revisão. | Produto do Artigo |
| **`results/figures/`** | Armazena figuras, gráficos e diagramas renderizados em alta resolução. | Produto do Artigo |
| **`results/tables/`** | Armazena as tabelas finais do artigo formatadas em CSV, Markdown e LaTeX. | Produto do Artigo |
| **`results/logs/`** | Mantém a rastreabilidade integral, auditoria e histórico de decisões. | Registro Operacional |

---

## 3. Síntese das Respostas às Perguntas de Pesquisa (RQs)

Os artefatos mantidos em `results/` fornecem a sustentação empírica para responder às três Perguntas de Pesquisa do projeto:

* **RQ1 — Acurácia Clínica no Dataset BRAX ($N_{f1} = 53$ estudos de suporte teórico):** Avaliação do MedGemma 1.5 4B adaptado para laudos radiológicos no dataset brasileiro do Hospital Albert Einstein, medindo métricas anatômicas baseadas em grafos (RadGraph F1, CheXbert F1 e GREEN Metric).
* **RQ2 — Engenharia de Borda e Telemetria ($N_{f2} = 2$ estudos de suporte técnico):** Desempenho físico do modelo quantizado (AWQ 4-bit e GGUF `Q4_K_M`) embarcado na placa NVIDIA Jetson Orin Nano (8 GB VRAM) sob perfil energéticamente restrito de **15W** via `llama.cpp` (pegada de VRAM de 5,6 GB, vazão de 12–15 tokens/s e latência TTFT < 1,2s).
* **RQ3 — Engenharia de Prompt e Mitigação de Alucinações:** Avaliação de prompts estruturados *Reason-then-Summarize* sob Cadeia de Pensamento (CoT) com delimitadores `<think> ... </think>` e `<answer> ... </answer>`.

---

## 4. Validação Matemática do Fluxo PRISMA (v8 - Saída Dupla)

A integridade quantitativa das tabelas, figuras e relatórios deste diretório é assegurada pela equação de controle do funil PRISMA:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad lacksquare
$$

E a aditividade conservativa da Saída Dupla:

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies \mathbf{55} = \mathbf{53}_{	ext{(Dissertação)}} + \mathbf{2}_{	ext{(Sistema)}} \quad lacksquare
$$
