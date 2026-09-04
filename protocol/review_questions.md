# Questões de Revisão Sistemática (RQs)

## RQ1: Quais Vision-Language Models são utilizados em radiologia?

Esta questão é fundamentada pelos relatórios de desenvolvimento de modelos e revisões sistemáticas do seu repositório, mapeando a evolução técnica de arquiteturas de ponta:

- **MedGemma (4B e 27B):** Modelo de fundação desenvolvido pelo Google DeepMind, baseado nos decodificadores Gemma e no codificador de imagens MedSigLIP. É exaustivamente avaliado em diagnósticos musculoesqueléticos e classificação de pneumoconiose.

- **META-CXR:** Um modelo de visão e linguagem baseado em "Tokens Especialistas", desenvolvido por Edirisinghe (2025) para geração de laudos guiados por anomalias.

- **ChestGPT:** Modelo multimodal baseado no codificador visual de larga escala EVA e decodificador Llama 2 para detecção e localização de condições clínicas.

- **MediVLM e RadVLM:** Arquiteturas conversacionais multitarefa projetadas para geração de laudos radiológicos e marcação anatômica baseada em frases (_phrase grounding_).

- **Lingshu-7B e CheXagent-3B:** Modelos de fundação projetados para interpretação clínica estruturada de exames de tórax e consolidação de contexto clínico de prontuários eletrônicos.

- **Visão Geral e Taxonomia:** As revisões detalhadas de Yi, Xiao e Albert (2025), Dasgupta et al. (2026) e revisões clássicas de MLLMs radiológicos documentam a árvore evolutiva de modelos como o LLaVA-Med, Med-Flamingo, XrayGPT e MiniGPT-Med.

---

## RQ2: Quais datasets aparecem com maior frequência?

Esta questão mapeia os repositórios de dados médicos utilizados para treinar, validar e calibrar os modelos multimodais de radiologia:

- **MIMIC-CXR / MIMIC-CXR-JPG:** O maior banco de dados público de radiografias de tórax pareadas com laudos de texto livre (mais de 377.000 imagens), considerado o padrão ouro de treinamento e avaliação na literatura.

- **CheXpert / CheXpert Plus:** Dataset essencial para a rotulação automática de 14 achados patológicos, muito empregado em tarefas de classificação sob incerteza.

- **BRAX (Albert Einstein — Brasil):** Base nacional de radiografias em português utilizada para o alinhamento regional e ajuste-fino supervisionado (SFT) de pneumonia.

- **PadChest e PadChest-GR:** Dataset bilíngue (espanhol e inglês) com anotações de localização espacial de achados de tórax.

- **VinDr-CXR:** Banco de dados com anotações manuais de caixas delimitadoras (_bounding boxes_) desenhadas por radiologistas especialistas.

- **SLAKE e VQA-RAD:** Datasets clássicos de perguntas e respostas médicas (_Visual Question Answering — VQA_) usados para avaliar capacidades conversacionais clínicas.

---

## RQ3: Quais hardwares são utilizados?

O mapeamento de hardware documenta a transição de ambientes de servidores de alta performance para kits embarcados com restrição de energia:

### Estações de Treinamento (Host Server)

A literatura destaca o uso de aceleradores de alto desempenho, como a GPU **NVIDIA RTX 4090 de 24 GB** e servidores **H100**, essenciais para acomodar os gradientes de ajuste-fino supervisionado (SFT) via QLoRA.

### Hardware de Borda e Aceleradores Locais (Edge Devices)

O kit de desenvolvimento **NVIDIA Jetson Orin Nano**, sob limites estritos de energia de **15 W**, e o **Jetson AGX Orin** são documentados como plataformas de referência para implantação física _offline_ e real de inteligência artificial clínica em unidades remotas.

---

## RQ4: Quais métricas são reportadas?

A consolidação de métricas é dividida de forma metodológica pelas fontes em três eixos principais de avaliação:

### Eficácia Diagnóstica Clínica

- **F1-Score (Micro e Macro):** Avaliação de acerto de rótulos binários de patologias.

- **RadGraph F1:** Mapeia a extração de entidades clínicas e relações de dependência semântica entre achados e localizações anatômicas.

- **CheXbert F1:** Avalia a concordância de conceitos biomédicos gerados nos laudos livres.

### Geração de Linguagem Natural (NLG) Tradicional

- **BLEU (1 a 4):** Utilizado para medir a similaridade de _n-grams_ entre o laudo gerado pelo modelo e o laudo de referência do radiologista humano.

- **ROUGE-L:** Métrica baseada na maior subsequência comum entre o texto gerado e o texto de referência.

- **METEOR:** Métrica de avaliação de similaridade textual considerando correspondências lexicais e semânticas.

- **CIDEr:** Métrica voltada à avaliação de descrições geradas, considerando a relevância dos termos em relação às referências.

### Métricas de Telemetria e Alinhamento Técnico

- **Latência de Inferência:** Tempo físico decorrido, em segundos, para geração da saída.

- **Pico de Memória VRAM:** Consumo dinâmico em Gigabytes da memória unificada do hardware _edge_.

- **GREEN Metric:** Penaliza ativamente as alucinações baseando-se na gravidade e no risco clínico dos erros inseridos no laudo.

---

## RQ5: Há estudos utilizando inferência local?

As fontes fornecem a sustentação de privacidade e soberania de dados para inferência 100% _offline_ em ambiente hospitalar:

### Soberania e LGPD Hospitalar (SUS)

O estudo de Dosso et al. (2025), da UNICAMP, comprova que a dependência de APIs em nuvem é inviável em hospitais públicos do Brasil devido a custos em dólar e barreiras legais de privacidade de dados sensíveis de pacientes sob a **Lei Geral de Proteção de Dados (LGPD — Lei nº 13.709/2018)**, elegendo o _deploy_ local de VLMs quantizados (como o MedGemma 1.5 4B) como a alternativa segura.

### Inundação de Trabalho e Burnout

A implantação local de modelos auxiliares visa atenuar diretamente o estresse e a taxa de erros induzidos pelo cansaço físico de radiologistas em plantões clínicos contínuos.

---

## RQ6: Quais estudos utilizam llama.cpp?

Esta questão aborda a infraestrutura de software de baixo nível para execução de modelos comprimidos em CPU e GPU Tegra:

### llama.cpp e Formato GGUF

O motor de inferência em **C++ nativo** e o formato unificado **GGUF** são apontados pela literatura como ferramentas centrais para contornar gargalos de barramento DRAM.

### Superação do Gargalo do BitsAndBytes

O estudo de quantização da UNICAMP reporta que a quantização convencional dinâmica de 4 bits em Python (Hugging Face/BitsAndBytes) introduz um gargalo computacional que torna a inferência do MedGemma até **6 vezes mais lenta**, validando cientificamente por que seu projeto adota a compilação local no **llama.cpp** para realizar dequantização acelerada _on-the-fly_ via registradores de hardware, _kernels_ CUDA e instruções SIMD ARM NEON.

---

## RQ7: Quais utilizam MedGemma?

O corpus de artigos consagra o **MedGemma** como o estado da arte de modelos biomédicos abertos de tamanho compacto:

### Marco do Benchmark ReXVQA (2026)

Este estudo clínico de larga escala comprova que o **MedGemma 4B** supera médicos residentes seniores de radiologia humana em acurácia de diagnóstico visual de tórax (**83,84% vs. 77,27%**), o que convalida o modelo como o núcleo de inferência da arquitetura embarcada.

### Superioridade em Relação a Modelos Proprietários

Benchmarks controlados indicam que o **MedGemma de 4B parâmetros**, por possuir um encoder visual especializado em imagens clínicas (**MedSigLIP**), apresenta uma acurácia em tarefas médicas de diagnóstico visual muito superior a modelos multimodais proprietários de propósito geral, como o GPT-4V.

### Eficiência de Memória de Borda

Ensaios de quantização elegem o **MedGemma 4B** como o modelo mais estável e econômico para hardware de borda, demandando um pico de apenas **5,6 GB de VRAM** sob quantização de 4 bits (**Q4_K_M GGUF**), permitindo que o sistema opere com folga física dentro do limite de **8 GB** do Jetson Orin Nano.
