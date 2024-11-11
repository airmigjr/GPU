
# Descrição da GPU Mali-400 no Zynq UltraScale+ MPSoC

## Documentação oficial AMD
<font size="4">[Link Documentação GPU](https://docs.amd.com/r/en-US/ug1085-zynq-ultrascale-trm/Graphics-Processing-Unit)</font>

<font size="4">Ela suporta APIs como OpenGL ES 1.1 e 2.0, permitindo a renderização eficiente de gráficos 2D e 3D. É capaz de realizar sobreposições gráficas (overlays), facilitando a integração de elementos visuais adicionais sobre imagens ou vídeos em tempo real. 
A Mali-400 MP2 oferece desempenho adequado para aplicações que requerem gráficos 2D e 3D, como interfaces de usuário e visualizações básicas. Sua arquitetura permite a criação de sobreposições gráficas, possibilitando a inserção de ícones ou informações adicionais sobre imagens ou vídeos.</font>

## Características Técnicas
<font size="4">

**Arquitetura:** Mali-400 MP2 é baseado na arquitetura Utgard.

**Frequência:** Até 667 MHz na configuração mais rápida.

**Processadores:** Possui um processador de geometria e dois processadores de pixel.

**Cache:** 64 KB de cache L2 dedicado.

**Desempenho:**

**Taxa de preenchimento:** 1334 Mpixels/s.

**Desempenho em triângulos:** Até 72.6 Mtriângulos/s.

**Desempenho em ponto flutuante:** 21.34 GFLOPS.

**APIs Suportadas:** OpenGL ES 1.1, OpenGL ES 2.0 e OpenVG 1.1.

**Eficiência Energética:** Projetada para baixo consumo de energia, ideal para dispositivos móveis.
</font >

### Recursos Adicionais
<font size="4">

**Renderização:** Suporta renderização baseada em tiles, o que reduz a largura de banda necessária para a memória off-chip.
**Anti-aliasing:** Inclui suporte para anti-aliasing, melhorando a qualidade da imagem sem penalizar o desempenho.

</font>

### Aplicações Típicas

<font size="4">

A Mali-400 MP2 é utilizada em uma variedade de dispositivos, sendo mais adequada para aplicações que exigem gráficos 2D e 3D.
Essas características tornam a Mali-400 MP2 uma opção popular em dispositivos móveis e aplicações onde a eficiência energética e o desempenho gráfico são cruciais.

</font>

## Abaixo, comparativo com outra GPU embarcada com o objetivo de se compreender qual seria uma GPU específica para o aprendizado profundo, no caso do objetivo de não se fazer uso da FPGA para este fim.

### (comparação entre GPU Mali vs AMD Ryzen Embbedded V1000) --> Neste caso, faria-se o uso de um chip dedicado para o aprendizado profundo.

<font size="4">

| **Característica**                      | **Mali-400 MP2**                                   | **AMD Radeon Embedded** V1000                       |
|-------------------------------------|------------------------------------------------|-------------------------------------------------|
| Arquitetura                         | ARM Mali                                      | GCN (Graphics Core Next)                        |
| Frequência Máxima                   | Até 667 MHz                                   | Até 1.5 GHz                                     |
| Processadores de Pixel              | 2                                             | 4                                               |
| Cache L2                            | 64 KB                                         | 512 KB                                          |
| Taxa de Preenchimento               | 1334 Mpixels/sec                              | 10.4 Gpixels/sec                                |
| Desempenho de Flops                 | 21.34 Gflops                                  | Até 6.4 TFLOPS                                  |
| Suporte a APIs Gráficas             | OpenGL ES 2.0, OpenVG 1.1                     | OpenCL, Vulkan, DirectX 12                      |
| Eficiência Energética               | Baixo consumo, ideal para dispositivos móveis | Maior consumo, mas otimizado para desempenho    |
| Capacidades de Aprendizado Profundo | Limitadas, não otimizadas para ML             | Otimizado para aprendizado profundo com suporte a frameworks como TensorFlow e PyTorch |
| Conectividade                       | Interfaces de memória DDR4/LPDDR4             | PCIe Gen3, USB 3.0, HDMI                        |

</font>

## Vantagens de cada GPU

### Vantagens da Mali-400 MP2
<font size="4">

- Eficiência Energética: Ideal para dispositivos que precisam operar com baixo consumo de energia.
- Custo-Benefício: Geralmente mais acessível em termos de custo, adequado para aplicações menos exigentes.

</font>

### [Vantagens da AMD Radeon Embedded V1000](https://www.amd.com/en/products/embedded/ryzen/ryzen-v1000-series.html)

<font size="4">

- Desempenho Superior: Com uma frequência mais alta e maior taxa de preenchimento, a Radeon V1000 é mais adequada para tarefas intensivas como detecção de objetos em tempo real.
- Suporte Avançado a Aprendizado Profundo: A arquitetura GCN é otimizada para operações paralelas e aprendizado profundo, tornando-a mais eficaz em tarefas de visão computacional.
- Maior Capacidade de Cache: O cache L2 maior permite um melhor gerenciamento de dados durante o processamento gráfico.
- Essas características tornam a AMD Radeon Embedded V1000 uma escolha superior para aplicações que exigem detecção de objetos em tempo real, enquanto a Mali-400 MP2 pode ser mais adequada para aplicações menos exigentes que priorizam eficiência energética e custo.

</font>

## Comparativo MPSoCs com GPU superior (AMD vs Texas)

<font size="4">

| **Característica**                  | **Xilinx UltraScale+ MPSoC (UG1085)**            | **[Texas Instruments Jacinto™ 7 TDA4VM](https://www.ti.com/lit/ml/spruis8a/spruis8a.pdf?ts=1723104609355)**         |
|---------------------------------|----------------------------------------------|---------------------------------------------|
| Arquitetura                     | ARM Cortex-A53, ARM Cortex-R5, Mali-400 MP2  | Dual ARM Cortex-A72, múltiplos Cortex-R5F   |
| Frequência do Processador       | Até 1.5 GHz (Cortex-A53), até 600 MHz (Cortex-R5) | Até 2.0 GHz (Cortex-A72)                 |
| Unidades de Processamento Gráfico | Mali-400 MP2                                | PowerVR GE8430                              |
| Memória                         | Suporte a DDR4, LPDDR4, DDR3 com ECC         | Suporte a DDR4                              |
| I/O                             | PCIe Gen2/Gen3, USB 3.0, SATA 3.1, Gigabit Ethernet | PCIe Gen3, USB 3.0, CAN, Ethernet     |
| FPGA/Hardware Acelerador        | FPGA Kintex UltraScale+                      | Aceleradores integrados para visão e aprendizado profundo |
| Consumo de Energia              | Variável dependendo da configuração          | TDP típico de 15W                           |
| Aplicações Típicas              | Automotivo, IoT, processamento de sinais e vídeo | ADAS, veículos autônomos               |
| Segurança                       | Múltiplas camadas de segurança integradas    | Recursos robustos de segurança funcional    |

</font>

## Comparativo entre as duas GPUs acima mencionadas entre os dois MPSoCs

<font size="4">


| **Característica**                   | **Mali-400 MP2**                          | **PowerVR GE8430**                                 |
|---------------------------------|---------------------------------------------|------------------------------------------------|
| Desenvolvedor                   | ARM                                         | Imagination Technologies                       |
| Arquitetura                     | Mali                                        | PowerVR Series8                                |
| Frequência Máxima               | Até 667 MHz                                 | Até 600 MHz                                    |
| Núcleos de Processamento        | 4 núcleos (Quad-core)                       | 4 núcleos (Quad-core)                          |
| Cache L2                        | 64 KB                                       | 128 KB                                         |
| Desempenho de GFLOPS (FP32)     | 21.34 GFLOPS                                | Até 40 GFLOPS                                  |
| Taxa de Preenchimento (Mpixels/s)| 1334 Mpixels/s                             | 5.2 Gpixels/s                                  |
| Taxa de Triângulos (Mtriângulos/s)| 72.6 Mtriângulos/s                        | Não especificado                               |
| Suporte a APIs Gráficas         | OpenGL ES 1.1, OpenGL ES 2.0, OpenVG 1.1    | OpenGL ES 3.0, Vulkan                          |
| Eficiência Energética           | Alta eficiência energética                  | Alta eficiência energética                     |
| Recursos de Renderização        | Renderização baseada em tiles, anti-aliasing| Renderização avançada com suporte a múltiplos formatos de textura |
| Aplicações Típicas              | Dispositivos móveis, jogos casuais, interfaces gráficas | Dispositivos móveis, consoles de jogos, aplicações de vídeo |
| Consumo de Energia              | Baixo consumo em comparação com GPUs dedicadas | Consumo otimizado para dispositivos móveis  |

</font>

## Conclusão sobre a GPU Mali-400 MP2

<font size="4">

**A GPU Mali-400 integrada nos dispositivos Zynq UltraScale+ MPSoC é projetada para acelerar gráficos 2D e 3D, oferecendo suporte a APIs como OpenGL ES 1.1 e 2.0. Essa GPU é adequada para aplicações que exigem sobreposições gráficas em tempo real, como a fusão de imagens de câmeras com elementos gráficos.**

**Fusão de Imagens de Câmeras e Overlays Gráficos: A combinação de múltiplas fontes de vídeo com sobreposições gráficas é uma aplicação típica da GPU Mali-400. É possível adicionar informações contextuais ou alertas em tempo real. A arquitetura programável do Zynq UltraScale+ permite que a GPU manipule gráficos, enquanto a lógica programável (FPGA) processa dados de sensores ou câmeras, facilitando a fusão de imagens.**

**Aprendizado Profundo e Reconhecimento de Objetos: Para tarefas de aprendizado profundo, como reconhecimento de objetos, a GPU Mali-400 não é a mais indicada devido às suas limitações de desempenho. Nesses casos, a lógica programável (FPGA) do Zynq UltraScale+ oferece vantagens significativas. As FPGAs podem ser configuradas para executar inferências de redes neurais com alta eficiência e baixa latência, tornando-as mais adequadas para aplicações de aprendizado profundo.**

</font>