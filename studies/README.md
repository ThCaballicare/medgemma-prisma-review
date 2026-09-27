# Corpus de Estudos Incluídos (`studies/`)

Este diretório destina-se à organização, consolidação e documentação do **corpus final de 55 estudos científicos incluídos** na Revisão Sistemática da Literatura (RSL) sobre a execução local de **Vision-Language Models (VLMs)** para diagnóstico radiológico e computação de borda (_edge computing_).

Este diretório representa a etapa imediata seguinte às fases de identificação, deduplicação, triagem preliminar e avaliação de elegibilidade em texto completo do protocolo **PRISMA 2020 (v8 - Saída Dupla)**, reunindo os trabalhos que efetivamente fundamentam o projeto.

---

## 1. Objetivos do Diretório

A estrutura e os artefatos mantidos em `studies/` têm como finalidades primárias:

- **Consolidar o Corpus Final:** Manter o inventário estável dos 55 estudos científicos selecionados.
- **Identificação Única e Rastreável:** Atribuir identificadores padronizados (`STD001` a `STD055` / `REC001` a `REC055`) mantendo a correspondência direta com as fases de _screening_ e extração.
- **Organização de Metadados:** Armazenar informações bibliográficas primárias (autores, título, ano, periódico/conferência e DOI).
- **Classificação de Saída Dupla (_Dual-Output_):** Registrar a destinação funcional de cada estudo entre o suporte teórico da Dissertação e o suporte técnico do Sistema.
- **Rastreabilidade Fato-Extração:** Servir como ponte imutável entre a planilha de elegibilidade (`full_read-v8.csv`) e a matriz de extração detalhada (`extraction/extracted_data.csv`).

---

## 2. Estrutura do Diretório

```text
studies/
├── README.md               # Guia de governança e documentação do corpus final
├── included_studies.csv    # Tabela estruturada com o inventário dos 55 estudos incluídos
├── study_catalog.md        # Catálogo descritivo e organizado por categoria de Saída Dupla
└── study_log.md            # Log de auditoria da transição de elegibilidade (59 -> 4 descartes -> 55)
```

### Descrição dos Arquivos

| Arquivo / Artefato         | Conteúdo e Função Metodológica                                                             |
| :------------------------- | :----------------------------------------------------------------------------------------- |
| **`README.md`**            | Manual de governança, regras de nomenclatura e especificação do diretório.                 |
| **`included_studies.csv`** | Matriz tabular padronizada com os 55 estudos incluídos, contendo metadados e categorias.   |
| **`study_catalog.md`**     | Catálogo textual formatado contendo as fichas sintéticas e agrupadas dos estudos.          |
| **`study_log.md`**         | Registro de auditoria detalhando o descarte dos 4 relatórios e validação dos 55 incluídos. |

---

## 3. Funil de Seleção e Mapeamento de Saída Dupla

Em conformidade com o protocolo da revisão sistemática, a transição para a formação deste corpus final é regida pelo funil de leitura integral:

```text
Estudos Selecionados para Leitura Completa (N_full) = 59
                       │
                       ▼ Exclusão de A = 4 relatórios não científicos
Estudos Científicos Incluídos Definitivos (N_f) = 55
```

### Distribuição no Modelo de Saída Dupla (_Dual-Output PRISMA Flow_)

Os 55 estudos incluídos são categorizados formalmente em duas frentes de aplicação:

```text
                     Corpus Final Incluído (N_f = 55)
                                   │
         ┌─────────────────────────┴─────────────────────────┐
         ▼                                                   ▼
Referencial da Dissertação (N_f1 = 53)              Referencial do Sistema (N_f2 = 2)
- Suporte Teórico Clínico                           - Suporte de Engenharia Aplicada
- Datasets (BRAX, MIMIC-CXR, CheXpert)             - Telemetria a 15W no Jetson Orin Nano
- Engenharia de Prompt Reason-Summarize             - Otimização AWQ por Magnitude (Lin2024)
- Calibração & Mitigação de Alucinações             - Dequantização llama.cpp (Hassija2026)
```

---

## 4. Validação Matemática da Consistência Global

A conciliação dos estudos mantidos neste diretório é verificada programaticamente em tempo de compilação através das equações de controle:

$$
\mathbf{N_f} = \mathbf{N_{full}} - \mathbf{A} \implies \mathbf{55} = \mathbf{59} - \mathbf{4} \quad \blacksquare
$$

$$
\mathbf{N_f} = \mathbf{N_i} - \mathbf{D} - \mathbf{T_1} - \mathbf{T_2} - \mathbf{A} \implies \mathbf{55} = \mathbf{64.878} - \mathbf{9.475} - \mathbf{55.258} - \mathbf{86} - \mathbf{4} \quad \blacksquare
$$

$$
\mathbf{N_f} = \mathbf{N_{f1}} + \mathbf{N_{f2}} \implies \mathbf{55} = \mathbf{53} + \mathbf{2} \quad \blacksquare
$$

---

## 5. Diretrizes de Atualização e Rastreabilidade

- Os registros contidos em `included_studies.csv` são imutáveis e representam a seleção aprovada pela revisão por pares.
- Qualquer acréscimo de metadados deve manter total sincronia com os arquivos bibliográficos da pasta `bibliography/` (`references.bib`, `references.csv`, `references.ris`) e da matriz `extraction/extracted_data.csv`.
