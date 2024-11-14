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
