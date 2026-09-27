# Documentação do Projeto (`docs/`)

Este diretório concentra a documentação metodológica, técnica e científica da Revisão Sistemática da Literatura (RSL) sobre a otimização e execução local de **Vision-Language Models (VLMs)** aplicados à radiologia diagnóstica e computação de borda (*edge computing*).

---

## 🗺️ Índice da Documentação

A estrutura de documentos no diretório `docs/` organiza-se de forma modular para orientar revisores, pesquisadores e desenvolvedores:

```text
docs/
├── README.md                 # Índice e visão geral da documentação
├── methodology.md            # Metodologia completa da RSL (PRISMA v8 - Saída Dupla)
├── inclusion_criteria.md     # Critérios de inclusão (CI)
├── exclusion_criteria.md     # Critérios de exclusão (CE)
├── environment.md            # Ambiente computacional, hardware edge e software
└── reproducibility.md        # Guia passo a passo para reprodução do pipeline
```

---

## 📌 Guia de Navegação

| Documento | Função e Conteúdo Principal |
| :--- | :--- |
| **[`methodology.md`](methodology.md)** | Descreve o protocolo científico rigoroso adotado, as estratégias de busca nas 5 bases ($B_1$ a $B_5$), o funil de seleção PRISMA 2020 e o modelo de **Saída Dupla** ($N_{f1} = 53$ para Dissertação e $N_{f2} = 2$ para Sistema). |
| **[`inclusion_criteria.md`](inclusion_criteria.md)** | Detalha os 6 critérios de inclusão ($CI1$ a $CI6$) referentes a arquiteturas VLM multimodais, imagens radiográficas (CXR/BRAX/MIMIC), requisitos de texto completo e métricas relatadas. |
| **[`exclusion_criteria.md`](exclusion_criteria.md)** | Apresenta os 4 critérios de exclusão ($CE1$ a $CE4$) que eliminam modelos unimodais, domínios não médicos, trabalhos sem dados empíricos e soluções com dependência estrita de nuvem. |
| **[`environment.md`](environment.md)** | Especifica o ambiente de hardware (NVIDIA RTX 4090 24GB para treino/host e NVIDIA Jetson Orin Nano 8GB a **15W** para borda) e software (`llama.cpp`, GGUF, AWQ, Python 3.12, CUDA). |
| **[`reproducibility.md`](reproducibility.md)** | Fornece as instruções determinísticas e comandos para re-executar a coleta, deduplicação, triagem, extração de dados e verificação das equações de consistência. |

---

## 🧮 Equação de Controle do Funil PRISMA v8

Toda a documentação mantida nesta pasta é balizada e auditada pela equação de controle do fluxo:

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A}
$$

$$
\mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad lacksquare
$$

E pela partição conservativa de Saída Dupla na fase de inclusão:

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies \mathbf{55} = \mathbf{53} + \mathbf{2} \quad lacksquare
$$
