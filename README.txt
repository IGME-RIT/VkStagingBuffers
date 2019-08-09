With Staging Buffers, we can actually store
memory on the GPU's VRAM, rather than leaving 
then on the CPU's RAM. The "Staging buffer", is
a buffer that is made on the CPU, that is copied
to the GPU. We don't need to change the BufferCPU
class, but we do need to change the BufferCreateInfo
of the Vertex and Index Buffers to make them 
Staging Buffers. We do not need to change the
uniform buffer, because that changes every frame
(unlike vertex and index buffer), so we can leave
uniform buffer on the GPU. We will also introduce
a new command buffer "initCmd" which will be used
to copy data from CPU to GPU. We will add a new 
class called BufferGPU to manage GPU buffers.
Inside prepare_vb_ib(), you can see how we can 
use this class, with our initCmd command buffer,
to copy buffers from CPU to GPU. First we call
prepare_init_cmd(), then we give commands to copy
data, and then those commands are executed when we
call execute_init_cmd(). The end-result of the
program will look the same, it will still be a spinning
cube, but now our buffers are on VRAM instead of RAM.
This is important, because reading from RAM is slow.
An advanced 3D Animated Human tutorial might run at 
100fps while buffers are on the CPU, while it will 
run at 400-500fps with staging buffers. We will show more
usages of staging buffers and GPU-only buffers in future
tutorials.

To fully understand how we create a new command buffer,
then put commands in that buffer, and then execute.
Please read prepare() from start to bottom, and read
all of the comments that are there