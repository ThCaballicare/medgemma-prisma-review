# Fluxo PRISMA — Revisão Sistemática (Saída Dupla)

## Visão Geral

O processo de seleção de literatura desta pesquisa foi estruturado segundo as diretrizes do protocolo **PRISMA 2020** [45], incorporando uma abordagem inovadora de **Saída Dupla (Dual-Output Flow)** na etapa final de inclusão [12, 111].

O funil metodológico é composto por cinco etapas sequenciais e interdependentes: identificação, remoção de duplicatas, triagem inicial (coarse screening), triagem detalhada (detailed screening) e avaliação de elegibilidade por leitura completa do texto integral, culminando na separação estratégica do corpus científico final [12, 649].

---

## 1. Identificação

Foram identificados **64.878 registros** brutos através de buscas sistemáticas realizadas em cinco bases de dados bibliográficas eletrônicas consultadas na mesma janela temporal [649]:

| Base de Dados           | Registros ($B_i$) | Tipo de Indexação / Escopo de Cobertura                                             |
| :---------------------- | :---------------: | :---------------------------------------------------------------------------------- |
| **Google Scholar**      |      19.820       | Busca abrangente de preprints e anais multidisciplinares [649, 651].                |
| **arXiv**               |      18.420       | Repositório de preprints de rápida disseminação em aprendizado profundo [649, 651]. |
| **PubMed / MEDLINE**    |      14.250       | Base de dados de referência para ciências biomédicas e da saúde [649, 651].         |
| **IEEE Xplore**         |       9.150       | Periódicos e conferências de engenharia e ciência da computação [649, 651].         |
| **ACM Digital Library** |       3.238       | Repositório especializado em sistemas de computação e hardware [649].               |
| **Total ($N_i$)**       |    **64.878**     | **Volume total de registros brutos identificados.**                                 |

---

## 2. Remoção de Duplicatas

Os registros repetidos entre as bases de dados foram mapeados de forma automatizada por meio de scripts de correspondência textual estruturada (baseados em correspondência de strings de título e ano) [112].

- **Duplicatas Removidas ($D$):** $9.475$ registros.

A conciliação matemática pós-deduplicação para a definição dos registros únicos ($N_1$) é dada por:

$$N_1 = N_i - D$$
$$N_1 = 64.878 - 9.475 = 55.403$$

Desse modo, **55.403 registros únicos** foram encaminhados para a fase de triagem inicial de título e resumo.

---

## 3. Triagem

O processo de triagem de títulos e resumos foi estruturado em duas etapas consecutivas (filtragem rápida e filtragem detalhada) para garantir a máxima fidelidade metodológica e mitigar viés de seleção [113]:

### Etapa 3.1: Triagem Inicial (Coarse Screening)

Nesta fase, realizou-se uma varredura inicial rápida baseada em palavras-chave. Foram excluídos registros que não abordavam _Vision-Language Models_ (VLMs), radiologia ou computação de borda ($T$):

- **Registros Excluídos ($T$):** $55.258$ estudos.

$$N_2 = N_1 - T$$
$$N_2 = 55.403 - 55.258 = 145$$

Exatamente **145 artigos elegíveis** avançaram para a próxima fase.

### Etapa 3.2: Triagem Detalhada (Detailed Screening)

Os 145 artigos pré-selecionados foram submetidos a uma leitura manual e atenta de seus resumos por revisores independentes. Nesta etapa de refinamento qualitativo, foram excluídos **86 estudos** ($T_2$) por não apresentarem aderência clínica direta (exames não-radiográficos) ou por proporem arquiteturas não generalizáveis para o diagnóstico de imagens médicas [113]:

- **Registros Excluídos ($T_2$):** $86$ estudos.

O volume de artigos científicos recuperados e destinados à avaliação de elegibilidade por leitura completa ($N_{full}$) totalizou exatamente:

$$N_{full} = N_2 - T_2$$
$$N_{full} = 145 - 86 = 59$$

---

## 4. Elegibilidade (Leitura Completa)

Os **59 artigos recuperados** em texto completo foram lidos de forma integral e independente por dupla revisão [114]. Nesta etapa final de elegibilidade, foram excluídos **4 relatórios** ($A$) pelas seguintes razões metodológicas estritas [114]:

1.  Documentos não-científicos de repositórios de código de terceiros (tutoriais de ferramentas sem validação experimental).
2.  Duplicatas residuais não identificadas nas etapas de processamento automático de texto.
3.  Manuais práticos de utilização de pacotes de software online.

- **Artigos Excluídos na Leitura Completa ($A$):** $4$ relatórios.

$$N_f = N_{full} - A$$
$$N_f = 59 - 4 = 55$$

O corpus final de literatura científica selecionada totaliza **55 estudos incluídos**.

---

## 5. Inclusão e Saída Dupla

Para maximizar o aproveitamento da literatura selecionada e alinhar o rascunho com o rigor técnico do projeto, os 55 estudos científicos incluídos ($N_f$) foram distribuídos em duas vertentes funcionais através do modelo de **Saída Dupla** [111, 114, 115]:

### 5.1. Referencial da Dissertação (Suporte Teórico — $N_{f1}$)

- **Quantidade de Estudos ($N_{f1}$):** **53 estudos** [115].
- **Escopo de Aplicação:** Compreende os trabalhos que dão suporte teórico geral, fornecendo as baselines clínicas de acurácia, especificações de engenharia de prompt estruturado (_Reason-then-Summarize_), controle de temperatura, características do dataset brasileiro **BRAX do Albert Einstein** (como o desequilíbrio de classes) e alinhamento de representações multimodais [115, 698].

### 5.2. Referencial do Sistema (Suporte Técnico — $N_{f2}$)

- **Quantidade de Estudos ($N_{f2}$):** **2 estudos** (LIN et al., 2024; HASSIJA et al., 2026) [37, 115].
- **Escopo de Aplicação:** Compreende os estudos experimentais primários e aplicados de engenharia de computação de borda. Fundamentam os testes de telemetria física em hardware edge, técnicas de compressão pós-treinamento via quantização por magnitude de ativação (**AWQ**) sob restrição de energia de **15W** na GPU **NVIDIA Jetson Orin Nano (8 GB)** e motores locais offline (`llama.cpp` compilado em C++) [22, 37, 117, 119].

A relação de inclusão final é perfeitamente balanceada:

$$N_f = N_{f1} + N_{f2}$$
$$55 = 53 + 2$$

---

## 6. Controle de Consistência Matemática Global

O funil metodológico do fluxo PRISMA é matematizado e validado pela equação de conciliação global:

$$N_f = N_i - D - T - T_2 - A$$
$$55 = 64.878 - 9.475 - 55.258 - 86 - 4$$

E a distribuição pós-elegibilidade fecha com exatidão perfeita:

$$55 = 53 + 2$$
