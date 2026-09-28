# Estratégias de Busca Exaustivas por Base de Dados (`supplementary/search_strategies/`)

Este documento apresenta o detalhamento exaustivo das expressões de busca, sintaxes por API, operadores booleanos e delimitadores aplicados nas 5 bases bibliográficas consultadas na Revisão Sistemática da Literatura.

---

## 1. PubMed / MEDLINE

* **Data de Execução:** 10/01/2026
* **Registros Recuperados ($B_1$):** $14.250$
* **Filtros Aplicados:** Período 2020–2026; Idiomas: Inglês e Português.

### String Exaustiva de Consulta (MeSH e Termos Livres)
```text
(("Multimodal Large Language Models"[Mesh] OR "Vision-Language Models"[Title/Abstract] OR "VLM"[Title/Abstract] OR "Generative AI"[Title/Abstract] OR "MedGemma"[Title/Abstract]) AND ("Radiology"[Mesh] OR "Radiography, Thoracic"[Mesh] OR "Chest X-Ray"[Title/Abstract] OR "CXR"[Title/Abstract] OR "Pneumonia"[Title/Abstract])) OR ("Edge Computing"[Mesh] OR "On-Device Inference"[Title/Abstract] OR "Model Quantization"[Title/Abstract] OR "llama.cpp"[Title/Abstract])
```

---

## 2. arXiv (cs.CV, cs.CL, eess.IV)

* **Data de Execução:** 11/01/2026
* **Registros Recuperados ($B_2$):** $18.420$
* **Mecanismo:** API do arXiv via e-fetch e query de categorias.

### Query de API
```text
(cat:cs.CV OR cat:cs.CL OR cat:eess.IV) AND (all:"vision language model" OR all:"MedGemma" OR all:"chest x-ray" OR all:"pneumonia diagnosis" OR all:"edge quantization")
```

---

## 3. IEEE Xplore

* **Data de Execução:** 12/01/2026
* **Registros Recuperados ($B_3$):** $9.150$
* **Filtros:** Conferences e Journals (2020–2026).

### Query IEEE Advanced Search
```text
(("Full Text & Metadata":"Vision-Language Model" OR "Full Text & Metadata":"MedGemma") AND ("Full Text & Metadata":"Chest Radiograph" OR "Full Text & Metadata":"Pneumonia")) AND ("Full Text & Metadata":"Edge Computing" OR "Full Text & Metadata":"Quantization" OR "Full Text & Metadata":"Embedded AI")
```

---

## 4. Google Scholar

* **Data de Execução:** 13/01/2026
* **Registros Recuperados ($B_4$):** $19.820$
* **Estratégia:** Sub-queries combinadas para contorno de limitação de cauda longa (1.000 resultados/query).

### Sub-queries Principais
1. `"MedGemma" "chest x-ray" OR "pneumonia"`
2. `"vision-language model" "radiology" "edge" OR "quantization"`
3. `"chest radiograph" "deep learning" "on-device"`

---

## 5. ACM Digital Library

* **Data de Execução:** 14/01/2026
* **Registros Recuperados ($B_5$):** $3.238$
* **Campos:** Abstract, Title e Keywords.

### Query ACM Syntax
```text
+Abstract:("vision language model" OR "MedGemma") +Abstract:("radiology" OR "chest x-ray") +Abstract:("edge" OR "quantization")
```

---

## 6. Validação do Volume Total ($N_i$)

$$N_i = B_1 + B_2 + B_3 + B_4 + B_5 = 14.250 + 18.420 + 9.150 + 19.820 + 3.238 = 64.878 \quad lacksquare$$
