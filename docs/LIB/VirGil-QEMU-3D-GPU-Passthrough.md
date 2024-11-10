# VirGL¶

Home Page:

<https://docs.mesa3d.org/drivers/virgl/>

## What is VirGL?¶

VirGL is a virtual 3D GPU for use inside QEMU virtual machines, that allows the guest operating system to use the capabilities of the host GPU to accelerate 3D rendering. The plan is to have a guest GPU that is fully independent of the host GPU.


## What exactly does it entail?¶

The project entails creating a virtual 3D capable graphics card for virtual machines running inside QEMU. The design of this card is based around the concepts of Gallium3D to make writing Mesa and (eventually) Direct3D drivers for it easy. The card natively uses the Gallium TGSI intermediate representation for its shaders. The implementation of rendering for the card is done in the host system as part of QEMU and is implemented purely on OpenGL so you can get accelerated rendering on any sufficiently capable card/driver combination.

The project also consists of a complete Linux guest stack, composed of a Linux kernel KMS driver, X.org 2D DDX driver and Mesa 3D driver.

----
<!-- Footer Begins Here -->
## Links

- [Back to Root Document](../README.md)
