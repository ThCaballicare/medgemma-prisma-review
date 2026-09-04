## 5. REQUISITOS DE DESIGN E CONFIGURAÇÃO DO EXPERIMENTO DO SISTEMA

O protocolo estabelece que as evidências colhidas na literatura respaldam metodologicamente o desenho experimental físico construído na pesquisa aplicada, conforme os parâmetros definidos a seguir.

### 5.1 Otimização QLoRA no Host (Ajuste-Fino Supervisionado)

- **Modelo de Partida:** MedGemma 1.5 4B (decodificador Gemma 3 4B + encoder visual MedSigLIP 400M congelado de fábrica).

- **Parâmetros de Baixo Posto:** Injeção de matrizes LoRA treináveis de Rank $r=32$ e Alpha $\alpha=64$, correspondendo a um fator de escala constante de $\alpha/r=2$, nas projeções de atenção (`q_proj`, `k_proj`, `v_proj`, `o_proj`) e nas projeções lineares MLP (`gate_proj`, `up_proj`, `down_proj`) do decodificador Gemma 3.

- **Matriz Linguística:** Pesos de base congelados em precisão de 4 bits, utilizando o formato NormalFloat 4 (NF4), por meio do framework PyTorch/Unsloth em estação local equipada com GPU NVIDIA RTX 4090 de 24 GB de VRAM.

- **Engenharia de Prompt Estruturado (CoT):** Utilização da heurística _Reason-then-Summarize_, com alvos de treinamento estruturados para descrever obrigatoriamente as observações clínicas dentro do bloco delimitador `<think> ... </think>` antes de emitir a triagem diagnóstica estruturada em JSON na tag `<answer> ... </answer>`.

### 5.2 Deploy Local no Dispositivo de Borda (NVIDIA Jetson)

- **Plataforma Física:** Kit de desenvolvimento NVIDIA Jetson Orin Nano Developer Kit, com 8 GB de memória unificada, operando sob limite estrito de potência de **15 W**.

- **Compilação e Aceleração:** Motor de inferência de baixo nível `llama.cpp`, compilado localmente em C++, utilizando a pilha de aceleração CUDA disponibilizada pelo ambiente JetPack instalado no dispositivo.

- **Formato de Execução:** O modelo resultante do processo de ajuste-fino é convertido offline para um formato binário compatível com o `llama.cpp`, utilizando o padrão **GGUF** e uma configuração de quantização de 4 bits, com destaque para a variante **Q4_K_M**, visando reduzir o consumo de memória e o custo computacional da inferência.

- **Otimização por Quantização:** Quando aplicável, técnicas de quantização pós-treinamento baseadas em consciência de ativações, como **AWQ (Activation-aware Weight Quantization)**, serão avaliadas como estratégia de redução da precisão dos pesos. A comparação deverá distinguir explicitamente o método de quantização utilizado do formato final de armazenamento e execução, evitando tratar AWQ e Q4_K_M como conceitos equivalentes.

- **Aceleração de Baixo Nível:** A execução utiliza kernels CUDA para exploração da GPU integrada do SoC Tegra, enquanto operações executadas no processador ARM podem utilizar instruções SIMD **ARM NEON**. Essa separação permite avaliar individualmente o impacto da aceleração por GPU e das otimizações vetoriais da CPU sobre a latência e a eficiência energética da inferência.

- **Telemetria Física:** Durante a execução, serão monitorados a latência de geração, a taxa de processamento em tokens por segundo, o pico de utilização da memória unificada, a potência consumida e, quando disponível, as temperaturas dos componentes computacionais.

- **Restrição Operacional:** Todos os testes de inferência deverão ser realizados localmente, sem dependência de APIs externas ou processamento remoto em nuvem, mantendo o dispositivo dentro do limite energético estabelecido de **15 W**.

- **Objetivo do Deploy:** Avaliar a viabilidade de execução offline de um VLM médico quantizado para triagem de pneumonia em ambiente de computação de borda, estabelecendo uma relação quantitativa entre desempenho diagnóstico, latência, consumo de memória e eficiência energética.
