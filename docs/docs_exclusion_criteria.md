# Critérios de Exclusão (`docs/exclusion_criteria.md`)

Este documento estabelece os **Critérios de Exclusão ($CE$)** formais aplicados para o descarte de registros incompatíveis durante as etapas de triagem e elegibilidade do fluxo **PRISMA v8**.

---

## Lista de Critérios de Exclusão ($CE1$ a $CE4$)

Qualquer estudo que apresente **pelo menos uma** das características a seguir é imediatamente descartado do corpus:

### $CE1$ — Modelos Unimodais

- **Descrição:** Trabalhos focados exclusivamente em classificação de imagens via redes convolucionais/ViTs puras sem componente de linguagem (ex.: ResNet/DenseNet isoladas), ou processamento de texto puro sem entrada visual.
- **Impacto no Funil:** Principal causa de exclusão na etapa de triagem inicial ($T_1 = 55.258$).

### $CE2$ — Domínio Geral Não Adaptado

- **Descrição:** Arquiteturas VLMs genéricas (ex.: CLIP original, GPT-4v padrão) avaliadas apenas em objetos do cotidiano, sem qualquer adaptação, alinhamento ou benchmark no contexto radiológico.
- **Impacto no Funil:** Excluídos por falta de relevância clínica e ausência de vocabulário biomédico.

### $CE3$ — Ausência de Dados Empíricos

- **Descrição:** Editoriais, cartas ao editor, resumos curtos (_abstract-only_), opiniões, tutoriais de código comerciais ou manuais de ferramentas online sem experimentação técnica formal.
- **Impacto no Funil:** Justifica a exclusão de 86 resumos no _Detailed Screening_ ($T_2 = 86$) e de 4 relatórios na leitura completa ($A = 4$).

### $CE4$ — Dependência Estrita de Nuvem Comercial (Cloud-Only)

- **Descrição:** Soluções que dependem exclusivamente de chamadas de API em nuvem pagas e não permitem ou não discutem a viabilidade de execução offline em hardware de borda (_edge computing_) via `llama.cpp` ou quantização (GGUF/AWQ).
- **Impacto no Funil:** Justifica a restrição dos estudos de engenharia do sistema ($N_{f2} = 2$) àqueles que comprovam a viabilidade offline sob a **LGPD (Lei nº 13.709/2018)** e limites de **15W**.

---

## Motivos de Exclusão Registrados no Funil

| Etapa de Exclusão                    | Símbolo | Quantidade ($n$) | Principal Critério Aplicado                              |
| :----------------------------------- | :-----: | :--------------: | :------------------------------------------------------- |
| **Deduplicação**                     |   $D$   |     $9.475$      | Registros idênticos entre bases                          |
| **Triagem Inicial (Coarse)**         |  $T_1$  |     $55.258$     | $CE1$ (Unimodal) e $CE2$ (Domínio Geral)                 |
| **Triagem Detalhada (Detailed)**     |  $T_2$  |       $86$       | $CE3$ (Falta de dados empíricos/resumos)                 |
| **Leitura Integral (Elegibilidade)** |   $A$   |       $4$        | $CE3$ (Manuais/tutoriais) e $CE4$ (Sem viabilidade edge) |
