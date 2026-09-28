# Diretório de Figuras e Artefatos Visuais (`figures/`)

Este diretório armazena todas as figuras, diagramas de fluxo, gráficos de tendência e representações visuais produzidas a partir dos dados consolidados da Revisão Sistemática da Literatura (RSL) sobre a execução de **Vision-Language Models (VLMs)** em radiologia e computação de borda (*edge computing*).

As figuras aqui mantidas constituem os artefatos gráficos finais prontos para inclusão direta no artigo científico, dissertação e materiais de apresentação do projeto.

---

## 1. Arquitetura Lógica e Fluxo de Produção

A produção das figuras segue uma separação estrita de responsabilidades no repositório:

```text
       analysis/
 (Cálculo de métricas, mineração de dados e scripts de geração em Python)
           │
           ▼
        figures/
 (Artefatos visuais finais renderizados em alta resolução)
           │
           ▼
Manuscrito / Dissertação / Artigo Científico
```

> ⚠️ **Regra de Governança Importante:**
> O diretório `figures/` **NÃO é o local onde os dados são calculados ou processados**. 
> - Todo o cálculo estatístico, consolidação de frequências e execução dos scripts gráficos (`matplotlib`, `seaborn`, `Graphviz`) pertence exclusivamente ao diretório **`analysis/`**.
> - O diretório **`figures/`** recebe e armazena **apenas as imagens finais renderizadas** em formatos vetoriais (`.svg`, `.pdf`) ou bitmap de alta resolução ($\ge 300\text{ DPI}$ em `.png`).

---

## 2. Estrutura Organizacional Esperada

```text
figures/
├── README.md                   # Guia de governança e inventário do diretório
├── prisma/                     # Fluxograma PRISMA 2020 de Saída Dupla
├── screening/                  # Gráficos de retenção, sobreposição e duplicatas
├── study_characteristics/      # Distribuição temporal, por base, por modelo e por dataset
└── analysis/                   # Gráficos de acurácia clínica, calibração e telemetria edge
```

### Detalhamento das Subpastas:

* **`figures/prisma/`**: Contém o fluxograma oficial **PRISMA 2020 (v8 - Saída Dupla)** detalhando todas as etapas do funil ($N_i = 64.878 \to N_f = 55$).
* **`figures/screening/`**: Contém os gráficos de sobreposição entre bases de dados ($B_i$), curva de remoção de duplicatas ($D = 9.475$) e taxa de atrito na triagem de títulos e resumos.
* **`figures/study_characteristics/`**: Gráficos de barra e pizza representando a evolução temporal das publicações (2020–2026), distribuição dos datasets (ex: **BRAX do Albert Einstein**, MIMIC-CXR), famílias de modelos (MedGemma, CheXagent) e modalidades radiológicas (CXR, CT).
* **`figures/analysis/`**: Diagramas de calibração diagnóstica (RadGraph F1, CheXbert F1), gráficos de tradeoffs entre precisão e vazão de tokens ($t/s$) e curvas de telemetria física no **NVIDIA Jetson Orin Nano** sob limite estrito de **15W**.

---

## 3. Padrões Técnicos e Formatos de Exportação

Para garantir qualidade de publicação acadêmica, todas as figuras armazenadas neste diretório devem respeitar os seguintes requisitos técnicos:

1. **Formatos Suportados:**
   * **Vetor (Preferencial):** `.svg` e `.pdf` (para inserção direta no LaTeX / Overleaf sem perda de resolução).
   * **Bitmap:** `.png` com resolução mínima de **300 DPI** e fundo transparente ou branco puro.
2. **Nomenclatura Padronizada:** Uso de caixa baixa e hífens, prefixados pela categoria (ex: `fig_prisma_flowchart_v8.png`, `fig_temporal_distribution.pdf`, `fig_jetson_latency_telemetry.svg`).
3. **Acessibilidade Visual:** Paletas de cores amigáveis a daltonismo (*colorblind-safe*, como Viridis ou Okabe-Ito) e tipografia legível (Arial / Helvetica / Computer Modern).

---

## 4. Validação e Consistência com o PRISMA v8

As figuras que contêm contagens de estudos ou dados do fluxo refletem exatamente os parâmetros auditados pelas equações formais de controle:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad \blacksquare
$$

E a composição de Saída Dupla (*Dual-Output*):

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies \mathbf{55} = \mathbf{53}_{\text{(Dissertação)}} + \mathbf{2}_{\text{(Sistema)}} \quad \blacksquare
$$
