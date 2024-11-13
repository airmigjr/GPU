
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

## Diagrama em blocos

<!-- ![Overview](https://drive.google.com/file/d/1yJn49e8HynzYiTckGkOXIzlm_g_dsWa_/view?usp=sharing) -->
![Descrição da Imagem](https://github.com/airmigjr/GPU/blob/main/X15299-mali-gpu-block.jpg)

## Detalhamento
<font size="4">

1. **Geometry Processor:** é responsável pelo processamento de vértices e pela execução de operações de transformação geométrica, como a projeção e a modelagem de objetos 3D. Ele processa informações sobre a posição, cor e textura dos vértices antes de passá-los para o estágio de rasterização. O Mali-400 MP2 possui um único Geometry Processor que executa shaders de vértice, permitindo que ele manipule a geometria das cenas renderizadas.

2. **Pixel Processors:** Os Pixel Processors (ou Fragment Processors) são responsáveis por calcular a cor e outros atributos dos pixels que compõem a imagem final. Eles realizam operações como texturização, blending e anti-aliasing. O Mali-400 MP2 possui dois Pixel Processors, que operam em paralelo para aumentar a eficiência e a taxa de preenchimento da GPU. Isso permite que a GPU renderize mais pixels por segundo, melhorando o desempenho gráfico.

3. **MMU (Memory Management Unit):** A MMU gerencia o acesso à memória da GPU, controlando como os dados são lidos e escritos. Ela traduz endereços virtuais em endereços físicos, permitindo que a GPU acesse a memória **(externa ao mpsoc)** de forma eficiente. A MMU do Mali-400 MP2 é dedicada e ajuda a otimizar o uso da memória, garantindo que os dados necessários para o processamento gráfico sejam acessados rapidamente.

4. **L2 Cache:** O L2 Cache é uma memória cache de nível 2 que armazena dados frequentemente acessados para reduzir o tempo de acesso à memória principal. Ele melhora o desempenho geral da GPU ao minimizar latências durante o processamento gráfico. O Mali-400 MP2 possui um cache L2 compartilhado de 64 KB, que ajuda a melhorar a eficiência no acesso aos dados necessários para os Pixel Processors e Geometry Processor, reduzindo assim o consumo de largura de banda da memória.

</font>

## Aplicações Típicas

### Com relação à renderização 2D/3D e processamento de imagens
<font size="4">

A Mali-400 MP2 é utilizada em uma variedade de dispositivos, **sendo mais adequada para aplicações que exigem gráficos 2D e 3D**.
Essas características tornam a Mali-400 MP2 uma opção popular em dispositivos móveis e aplicações onde a eficiência energética e o desempenho gráfico são cruciais. 
É uma GPU projetada principalmente para renderização de gráficos 2D e 3D, **mas não possui funcionalidades nativas de pré-processamento de imagens**. Essas funções são geralmente realizadas por um **Processador de Sinal de Imagem ([ISP](https://www.sinoseen.com/pt/what-is-isp-image-signal-processorits-meaningfunctionsimportance))**, que é um componente separado responsável por processar imagens capturadas por sensores de câmera.

**PORÉM**

[Essa GPU possui capacidades de Pós-Processamento](https://community.arm.com/support-forums/f/graphics-gaming-and-vr-forum/4438/what-are-the-image-processing-techniques-supported-by-mali-400)

**Processamento de Imagem:** A Mali-400 MP2 pode executar técnicas de processamento de imagem através de shaders programáveis. Isso inclui operações como:
- **Correção de Distorções:** Ajustes para corrigir distorções causadas por lentes.
- **Filtragem de Imagem:** Aplicação de filtros para melhorar a qualidade da imagem.
- **Sombreamento de Pixels:** Processamento que envolve a aplicação de efeitos visuais nos pixels renderizados.
- A implementação dessas técnicas é feita utilizando OpenGL ES 1.1 e 2.0, escrevendo shaders em ESSL (Embedded Systems Shading Language) para realizar o processamento desejado 14.
- **Renderização em Tempo Real:** A Mali-400 MP2 é capaz de processar vídeo ao vivo, onde cada quadro pode ser processado individualmente antes da renderização na tela. Isso significa que, desde que o processamento seja rápido o suficiente para completar antes do próximo quadro, é viável realizar operações em tempo real em feeds de vídeo 1.
- **Uso de Shaders:** O uso de shaders permite uma ampla gama de manipulações gráficas e processamento de imagens. Existem muitos exemplos e bibliotecas disponíveis que demonstram como usar OpenGL ES para realizar essas operações 1.

**Limitações**
Embora a Mali-400 MP2 tenha capacidades para pós-processamento, ela não é um substituto completo para um Processador de Sinal de Imagem (ISP). Para tarefas mais complexas ou específicas, como correção avançada de imagem ou redução significativa de ruído, um ISP dedicado seria mais eficaz.

</font>

### Com relação à redes neurais (detecção de objetos, reconhecimento de imagens)

<font size="4">

A Mali-400 é uma GPU de baixo consumo projetada para tarefas gráficas básicas. Sua arquitetura não possui os recursos avançados encontrados em GPUs mais modernas que são otimizadas para aprendizado profundo, como unidades de processamento tensorial (TPUs) ou suporte robusto para operações de ponto flutuante necessárias para o treinamento e inferência de redes neurais. [Estudo sobre deep learning em GPUs de baixa potência](https://github.com/airmigjr/GPU/blob/main/ug4_proj.pdf)

</font>

## Conclusão

<font size="4">

### **A Mali 400 seria então para aplicações de baixo consumo, como interfaces de usuário e visualizações básicas.**

### **Diferenças entre processamento de imagens com um ISP vs GPU Mali integrada:**

#### Eficiência em Tempo Real e Latência:
- O ISP proporciona processamento em tempo real, essencial para aplicações de visão computacional. A GPU Mali-400, devido ao seu design genérico, pode introduzir latência adicional em operações gráficas.

  **Fonte:** [Mali-400 MP: A Scalable GPU for Mobile Devices](https://github.com/airmigjr/GPU/blob/main/HPG2010_Hot3D_ARM.pdf)
  
#### Consumo de Energia e Eficiência:
- O ISP é mais eficiente em termos de energia para tarefas específicas de imagem, enquanto a GPU Mali-400 consome mais energia para realizar operações que não são otimizadas para seu design.

  **Fonte:** [Introduction to the UltraScale Architecture](https://docs.amd.com/r/en-US/ug571-ultrascale-selectio/Introduction-to-the-UltraScale-Architecture)
  
#### Desempenho da GPU para Pós-Processamento e Tarefas de Visualização:
- A Mali-400 pode ser utilizada efetivamente no pós-processamento, aplicando efeitos visuais leves após o pré-processamento feito pelo ISP.

  **Fonte:** [ARM Mali Graphics Architecture](https://community.arm.com/arm-community-blogs/b/graphics-gaming-and-vr-blog/posts/arm-mali-400-overview)
  
#### **Realizei um estudo sobre utilização de CPU para eventualmente transferir algumas das atividades hoje realizadas pelo processador principal, como as atividades do HMI e CMS, esperando que renderização de ícones, linhas fossem realizadas pela GPU, porém, verifiquei que mesmo desabilitando as renderizações nos códigos do HMI para verificar o quanto de diminuição de uso de CPUs (que está em torno de 290%) ocorreria, foi praticamente insignificante.**

</font>

## Observações

<font size="4">

- Busquei qualquer chamada ou referência à Mali na ECU VT Base e não encontrei nenhuma.

```bash
DVS:/home/sredev# lsmod
    Not tainted
uio_dmem_genirq 16384 0 - Live 0xffffff800072b000
xt_conntrack 16384 1 - Live 0xffffff8000723000
nf_conntrack 94208 1 xt_conntrack, Live 0xffffff8000700000
libcrc32c 16384 1 nf_conntrack, Live 0xffffff80006f8000
nf_defrag_ipv4 16384 1 nf_conntrack, Live 0xffffff80006f0000
uio_pdrv_genirq 16384 6 - Live 0xffffff80006ba000
```

- Já na VT Base Plus, a qual não tenho acesso nesse momento, consegui com o Alex um ```lsmod``` que mostra a seguinte saída:

```bash
    Tainted: G  
uio_dmem_genirq 16384 0 - Live 0xffffff80007a1000
xt_conntrack 16384 1 - Live 0xffffff8000799000
nf_conntrack 94208 1 xt_conntrack, Live 0xffffff8000776000
libcrc32c 16384 1 nf_conntrack, Live 0xffffff800076e000
nf_defrag_ipv4 16384 1 nf_conntrack, Live 0xffffff8000766000
al5e 16384 2 - Live 0xffffff800075d000 (O)
al5d 16384 0 - Live 0xffffff8000754000 (O)
allegro 32768 7 al5e,al5d, Live 0xffffff8000734000 (O)
xlnx_vcu 16384 1 allegro, Live 0xffffff800072c000
xlnx_vcu_clk 16384 0 - Live 0xffffff8000724000
mali 229376 0 - Live 0xffffff80006d8000 (O) # carregamento de driver mali
xlnx_vcu_core 16384 4 - Live 0xffffff80006d0000
uio_pdrv_genirq 16384 7 - Live 0xffffff80006a0000
```
- Devido a falta de acesso à VT Base Plus, não consegui verificar se há alguma chamada ou referência à Mali na ECU VT Base Plus.

## Teste utilizando ECU Peregrino com SW PBUS2

- **Abrindo Menu e navegando, máximo de utilização de CPU 22%**
```bash
       inet 172.18.0.1  netmask 255.255.0.0  broadcast 172.18.255.255
Mem: 185068K used, 1536308K free, 400K shrd, 9292K buff, 33456K cached
CPU: 23.3% usr  2.8% sys  0.0% nic 73.7% idle  0.0% io  0.0% irq  0.0% sirq
Load average: 0.87 0.61 0.35 3/104 1648
  PID  PPID USER     STAT   VSZ %VSZ CPU %CPU COMMAND
 1605     1 root     S     474m 28.1   2 21.9 /bin/hmi -c /etc/hmi/config.json
 1537     1 root     S     181m 10.7   2  2.8 /bin/sysmgr -p /etc/sysmgr/config -f /etc/sysmgr/filepol
 1601     1 root     S     422m 25.0   3  0.7 /bin/cms -f /var/volatile/rpu/cvp/cvp_0_metadata.json -g
 1591     1 root     S     182m 10.8   2  0.1 /bin/sdm
 1578     1 root     S    78524  4.5   2  0.1 /bin/doipd
 1580     1 root     S    96352  5.5   2  0.1 /bin/shmlogd
```

***

# Mali-400 GPU Description in Zynq UltraScale+ MPSoC

## Official AMD Documentation

<font size="4">[GPU Documentation Link](https://docs.amd.com/r/en-US/ug1085-zynq-ultrascale-trm/Graphics-Processing-Unit)</font>

<font size="4">It supports APIs like OpenGL ES 1.1 and 2.0, enabling efficient 2D and 3D graphics rendering. It can perform graphic overlays, facilitating the integration of additional visual elements over real-time images or videos. The Mali-400 MP2 provides adequate performance for applications requiring 2D and 3D graphics, such as user interfaces and basic visualizations. Its architecture allows for the creation of graphic overlays, enabling the insertion of icons or additional information over images or videos.</font>

## Technical Specifications
<font size="4">

**Architecture:** Mali-400 MP2 is based on the Utgard architecture.

**Frequency:** Up to 667 MHz in the fastest configuration.

**Processors:** It has one geometry processor and two pixel processors.

**Cache:** 64 KB of dedicated L2 cache.

**Performance:**

**Fill rate:** 1334 Mpixels/s.

**Triangle performance:** Up to 72.6 Mtriangles/s.

**Floating-point performance:** 21.34 GFLOPS.

**Supported APIs:** OpenGL ES 1.1, OpenGL ES 2.0, and OpenVG 1.1.

**Energy Efficiency:** Designed for low power consumption, ideal for mobile devices.
</font >

### Additional Features
<font size="4">

**Rendering:** Supports tile-based rendering, reducing off-chip memory bandwidth requirements.
**Anti-aliasing:** Includes support for anti-aliasing, enhancing image quality without performance penalty.

</font>

## Block Diagram

<!-- ![Overview](https://drive.google.com/file/d/1yJn49e8HynzYiTckGkOXIzlm_g_dsWa_/view?usp=sharing) -->
![Image Description](https://github.com/airmigjr/GPU/blob/main/X15299-mali-gpu-block.jpg)

## Details
<font size="4">

1. **Geometry Processor:** Responsible for vertex processing and performing geometric transformations, such as projection and modeling of 3D objects. It processes information about the vertices' position, color, and texture before passing them to the rasterization stage. The Mali-400 MP2 has a single Geometry Processor that executes vertex shaders, allowing it to manipulate the geometry of rendered scenes.

2. **Pixel Processors:** Pixel Processors (or Fragment Processors) are responsible for calculating the color and other attributes of the pixels composing the final image. They perform operations like texturing, blending, and anti-aliasing. The Mali-400 MP2 has two Pixel Processors, which operate in parallel to increase efficiency and the GPU's fill rate, enabling it to render more pixels per second and improving graphics performance.

3. **MMU (Memory Management Unit):** The MMU manages the GPU's memory access, controlling how data is read and written. It translates virtual addresses to physical addresses, allowing the GPU to efficiently access memory **(external to the MPSoC)**. The Mali-400 MP2’s dedicated MMU helps optimize memory use, ensuring quick access to data needed for graphic processing.

4. **L2 Cache:** The L2 Cache is a level 2 cache memory that stores frequently accessed data to reduce main memory access time. It enhances the GPU’s overall performance by minimizing latency during graphic processing. The Mali-400 MP2 has a shared 64 KB L2 cache, which helps improve efficiency in accessing data required for the Pixel and Geometry Processors, thus reducing memory bandwidth consumption.

</font>

## Typical Applications

### Regarding 2D/3D Rendering and Image Processing
<font size="4">

The Mali-400 MP2 is used in a variety of devices, **best suited for applications requiring 2D and 3D graphics**. These features make the Mali-400 MP2 a popular choice in mobile devices and applications where energy efficiency and graphics performance are crucial. It is a GPU primarily designed for 2D and 3D graphics rendering, **but it lacks native image pre-processing functionalities**. These tasks are usually performed by an **Image Signal Processor ([ISP](https://www.sinoseen.com/pt/what-is-isp-image-signal-processorits-meaningfunctionsimportance))**, a separate component responsible for processing images captured by camera sensors.

**HOWEVER**

[This GPU has Post-Processing Capabilities](https://community.arm.com/support-forums/f/graphics-gaming-and-vr-forum/4438/what-are-the-image-processing-techniques-supported-by-mali-400)

**Image Processing:** The Mali-400 MP2 can perform image processing techniques through programmable shaders, including operations such as:
- **Distortion Correction:** Adjustments to correct lens-induced distortions.
- **Image Filtering:** Application of filters to enhance image quality.
- **Pixel Shading:** Processing that involves applying visual effects on rendered pixels.
- Implementing these techniques is done using OpenGL ES 1.1 and 2.0 by writing shaders in ESSL (Embedded Systems Shading Language) for desired processing.
- **Real-Time Rendering:** The Mali-400 MP2 can process live video, where each frame can be processed individually before rendering on-screen. This means that, as long as processing completes before the next frame, real-time operations on video feeds are feasible.
- **Shader Use:** Using shaders allows a wide range of graphic manipulations and image processing. Many examples and libraries are available demonstrating how to use OpenGL ES for these operations.

**Limitations**
While the Mali-400 MP2 has post-processing capabilities, it is not a complete substitute for an Image Signal Processor (ISP). For more complex or specific tasks, like advanced image correction or significant noise reduction, a dedicated ISP would be more effective.

</font>

### Regarding Neural Networks (Object Detection, Image Recognition)

<font size="4">

The Mali-400 is a low-power GPU designed for basic graphics tasks. Its architecture lacks advanced features found in more modern GPUs optimized for deep learning, such as tensor processing units (TPUs) or robust support for floating-point operations required for neural network training and inference. [Study on Deep Learning on Low-Power GPUs](https://github.com/airmigjr/GPU/blob/main/ug4_proj.pdf)

</font>

## Conclusion

<font size="4">

### **The Mali 400 is then suitable for low-power applications, such as user interfaces and basic visualizations.**

### **Differences between Image Processing with an ISP vs Integrated Mali GPU:**

#### Real-Time Efficiency and Latency:
- The ISP provides real-time processing essential for computer vision applications. The Mali-400 GPU, due to its generic design, may introduce additional latency in graphics operations.

  **Source:** [Mali-400 MP: A Scalable GPU for Mobile Devices](https://github.com/airmigjr/GPU/blob/main/HPG2010_Hot3D_ARM.pdf)
  
#### Energy Consumption and Efficiency:
- The ISP is more energy-efficient for specific image tasks, while the Mali-400 GPU consumes more power to perform operations not optimized for its design.

  **Source:** [Introduction to the UltraScale Architecture](https://docs.amd.com/r/en-US/ug571-ultrascale-selectio/Introduction-to-the-UltraScale-Architecture)
  
#### GPU Performance for Post-Processing and Visualization Tasks:
- The Mali-400 can be effectively used in post-processing, applying light visual effects after pre-processing done by the ISP.

  **Source:** [ARM Mali Graphics Architecture](https://community.arm.com/arm-community-blogs/b/graphics-gaming-and-vr-blog/posts/arm-mali-400-overview)
  
#### **I conducted a study on CPU usage for possibly offloading some activities currently handled by the main processor, such as HMI and CMS activities, expecting icon rendering, and line rendering to be handled by the GPU. However, I found that even disabling renderings in HMI code to assess how much CPU usage (around 290%) would decrease was practically negligible.**

</font>

## Observations

<font size="4">

- I searched for any reference to Mali in the VT Base ECU and found none.

```bash
DVS:/home/sredev# lsmod
    Not tainted
uio_dmem_genirq 16384 0 - Live 0xffffff800072b000
xt_conntrack 16384 1 - Live 0xffffff8000723000
nf_conntrack 94208 1 xt_conntrack, Live 0xffffff8000700000
libcrc32c 16384 1 nf_conntrack, Live 0xffffff80006f8000
nf_defrag_ipv4 16384 1 nf_conntrack, Live 0xffffff80006f0000
uio_pdrv_genirq 16384 6 - Live 0xffffff80006ba000
``` 

- On the VT Base Plus, to which I currently do not have access, Alex provided an lsmod output showing the following:

```    Tainted: G  
uio_dmem_genirq 16384 0 - Live 0xffffff80007a1000
xt_conntrack 16384 1 - Live 0xffffff8000799000
nf_conntrack 94208 1 xt_conntrack, Live 0xffffff8000776000
libcrc32c 16384 1 nf_conntrack, Live 0xffffff800076e000
nf_defrag_ipv4 16384 1 nf_conntrack, Live 0xffffff8000766000
al5e 16384 2 - Live 0xffffff800075d000 (O)
al5d 16384 0 - Live 0xffffff8000754000 (O)
allegro 32768 7 al5e,al5d, Live 0xffffff8000734000 (O)
xlnx_vcu 16384 1 allegro, Live 0xffffff800072c000
xlnx_vcu_clk 16384 0 - Live 0xffffff8000724000
mali 229376 0 - Live 0xffffff80006d8000 (O) # mali driver loaded
xlnx_vcu_core 16384 4 - Live 0xffffff80006d0000
uio_pdrv_genirq 16384 7 - Live 0xffffff80006a0000
```

- Due to lack of access to the VT Base Plus, I was unable to verify if there is any call or reference to Mali in the VT Base Plus ECU.

## Test using Peregrine ECU, running SW PBUS2

- Opening Menu and navigating, max CPU usage 22%

```bash
       inet 172.18.0.1  netmask 255.255.0.0  broadcast 172.18.255.255
Mem: 185068K used, 1536308K free, 400K shrd, 9292K buff, 33456K cached
CPU: 23.3% usr  2.8% sys  0.0% nic 73.7% idle  0.0% io  0.0% irq  0.0% sirq
Load average: 0.87 0.61 0.35 3/104 1648
  PID  PPID USER     STAT   VSZ %VSZ CPU %CPU COMMAND
 1605     1 root     S     474m 28.1   2 21.9 /bin/hmi -c /etc/hmi/config.json
 1537     1 root     S     181m 10.7   2  2.8 /bin/sysmgr -p /etc/sysmgr/config -f /etc/sysmgr/filepol
 1601     1 root     S     422m 25.0   3  0.7 /bin/cms -f /var/volatile/rpu/cvp/cvp_0_metadata.json -g
 1591     1 root     S     182m 10.8   2  0.1 /bin/sdm
 1578     1 root     S    78524  4.5   2  0.1 /bin/doipd
 1580     1 root     S    96352  5.5   2  0.1 /bin/shmlogd
``` 
