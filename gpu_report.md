
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
[Ela possui capacidades de Pós-Processamento](https://community.arm.com/support-forums/f/graphics-gaming-and-vr-forum/4438/what-are-the-image-processing-techniques-supported-by-mali-400)
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

A Mali-400 é uma GPU de baixo consumo projetada para tarefas gráficas básicas. Sua arquitetura não possui os recursos avançados encontrados em GPUs mais modernas que são otimizadas para aprendizado profundo, como unidades de processamento tensorial (TPUs) ou suporte robusto para operações de ponto flutuante necessárias para o treinamento e inferência de redes neurais. [Estudo sobre deep learning em GPUs de baixa potência](https://drive.google.com/file/d/1vVFJDkzuRdngTFHkYuQoHagMs5bJQaj2/view?usp=sharing)

</font>

## Conclusão

<font size="4">

- A Mali 400 seria então para aplicaçes de baixo consumo, como interfaces de usuário e visualizações básicas.
- Realizei um estudo sobre utilização de CPU para eventualmente transferir algumas das atividades hoje realizadas pelo processador principal, como as atividades do HMI e CMS, esperando que renderização de ícones, linhas fossem realizadas pela GPU, porém, verifiquei que mesmo desabilitando as renderizações nos códigos do HMI para verificar o quanto de diminuição de uso de CPUs (que está em torno de 290%) ocorreria, foi praticamente insignificante.
- Uma outra possibilidade de uso da GPU seria a de dewarp, redução de ruídos e correções de brilho, porém, pelo fato da GPU não possuir um ISP, não seria possível realizar essas tarefas.

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
