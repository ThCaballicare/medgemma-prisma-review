# Controle de Consistência Matemática do Fluxo PRISMA

Este documento estabelece a validação matemática detalhada do funil de seleção de literatura do projeto, estruturado sob o modelo de **Fluxo PRISMA de Saída Dupla (Dual-Output PRISMA Flow)**. As fórmulas e conciliações numéricas garantem a consistência integral entre as etapas de identificação, deduplicação, triagem, elegibilidade e inclusão final.

---

## 1. Identificação e Deduplicação

O volume inicial de registros brutos identificados ($N_i$) é governado pelo somatório dos resultados retornados pelas buscas sistemáticas nas $k = 5$ bases de dados consultadas:

$$N_i = \sum_{i=1}^{k} B_i = 64.878$$

Onde as frequências de recuperação individuais por base ($B_i$) correspondem a:
*   **arXiv** ($B_1$): $18.420$ registros
*   **Google Scholar** ($B_2$): $19.820$ registros
*   **PubMed** ($B_3$): $14.250$ registros
*   **IEEE Xplore** ($B_4$): $9.150$ registros
*   **ACM Digital Library** ($B_5$): $3.238$ registros

Após a identificação, o processo de deduplicação remove as referências repetidas ($D$), resultando no corpus de registros únicos ($N_1$):

$$D = 9.475 \text{ duplicatas}$$

$$N_1 = N_i - D$$

$$N_1 = 64.878 - 9.475 = 55.403$$

---

## 2. Primeira Etapa de Triagem (Coarse Screening)

Os $55.403$ registros únicos foram submetidos à primeira fase de triagem rápida de título e resumo. Foram excluídos os estudos que não abordaram Vision-Language Models (VLMs), aplicações médicas ou computação de borda ($T$):

$$T = 55.258 \text{ registros excluídos}$$

O total de estudos selecionados para a próxima fase de análise refinada ($N_2$) é dado por:

$$N_2 = N_1 - T$$

$$N_2 = 55.403 - 55.258 = 145$$

---

## 3. Segunda Etapa de Triagem (Detailed Screening)

Dos $145$ artigos elegíveis resultantes da triagem inicial, realizou-se uma avaliação manual aprofundada de títulos e resumos para mitigar ruídos conceituais ou metodológicos. Nesta fase, foram excluídos:

$$T_2 = 86 \text{ registros excluídos}$$

O conjunto de artigos científicos recuperados e destinados à leitura completa do texto integral ($N_{full}$) totaliza:

$$N_{full} = N_2 - T_2$$

$$N_{full} = 145 - 86 = 59$$

---

## 4. Avaliação de Elegibilidade (Leitura Completa)

Os $59$ artigos foram analisados de forma independente por dupla revisão em texto completo. Foram excluídos aqueles que correspondiam a manuais práticos de ferramentas online, tutoriais de código de terceiros ou duplicatas residuais de parsing ($A$):

$$A = 4 \text{ relatórios excluídos}$$

Dessa forma, o número de estudos científicos incluídos de forma definitiva ($N_f$) corresponde a:

$$N_f = N_{full} - A$$

$$N_f = 59 - 4 = 55$$

---

## 5. Destinação de Saída Dupla (Inclusão)

Para atender de forma rigorosa às demandas de fundamentação teórica e engenharia aplicada do projeto, os $55$ estudos incluídos foram divididos em duas categorias estratégicas na fase final de inclusão:

1.  **Referencial da Dissertação (Suporte Teórico - $N_{f1}$):** Estudos focados no estado da arte clínico, datasets de raios-X (como o BRAX brasileiro e MIMIC-CXR), calibração de modelos e heurísticas para mitigar alucinações.
    $$N_{f1} = 53$$
2.  **Referencial do Sistema (Suporte Técnico - $N_{f2}$):** Estudos aplicados diretamente a testes práticos experimentais em hardware edge limitado a 15W, quantização de precisão (como o AWQ) e motores locais de inferência offline.
    $$N_{f2} = 2$$

A conciliação da inclusão final é expressa por:

$$N_f = N_{f1} + N_{f2}$$

$$55 = 53 + 2$$

---

## 6. Controle e Conciliação Global

O equilíbrio matemático e a consistência integral do fluxo PRISMA são validados pela equação de conciliação global:

$$N_f = N_i - D - T - T_2 - A$$

Substituindo os valores empíricos correspondentes:

$$55 = 64.878 - 9.475 - 55.258 - 86 - 4$$

A validação fecha com exatidão perfeita e reprodutibilidade de $100\%$ entre todas as etapas do funil metodológico.
