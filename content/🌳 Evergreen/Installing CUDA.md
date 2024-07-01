---
tags:
  - 🖥️Computing
  - 🖍️Learning
---
# Installation

Following instructions found [here](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#). After [cleaning up](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#removing-cuda-toolkit-and-driver) the mess caused in the previous attempt.

```
❯ lspci | grep -i nvidia
01:00.0 VGA compatible controller: NVIDIA Corporation GM206 [GeForce GTX 960] (rev a1)
01:00.1 Audio device: NVIDIA Corporation GM206 High Definition Audio Controller (rev a1)
```

My GeForce is listed as supported here: https://developer.nvidia.com/cuda-gpus#compute
```
❯ uname -m && cat /etc/*release
x86_64
PRETTY_NAME="Debian GNU/Linux 12 (bookworm)"
NAME="Debian GNU/Linux"
VERSION_ID="12"
VERSION="12 (bookworm)"
```

Distro is listed as supported:

| Distribution       | Kernel1  | Default GCC | GLIBC |
| ------------------ | -------- | ----------- | ----- |
| Debian 12.x (x<=5) | 6.1.76-1 | 12.2.0      | 2.36  |
Kernel version:
```
jrekier in 🌐 WATSON-PC in ~
❯ uname -r
6.1.0-21-amd64
```

>[!warning]
>This differs from the Kernel listed in the table above. Might be an issue?

Downloaded the `.deb` package and executed instructions found [here](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=Debian&target_version=12&target_type=deb_local).

# Testing

Not much info is given to test the installation. 

First thing first, I check that cuda is in my path:

```
❯ echo $PATH
/home/jrekier/.cargo/bin:/usr/local/cuda/bin:/home/jrekier/bin:/usr/local/bin:/usr/bin:/bin:/usr/local/games:/usr/games:/snap/bin
```
I found [this](https://www.baeldung.com/linux/ubuntu-gpu-cuda#testing), which is made for Ubuntu, but should work. First try:

```
❯ ./deviceQuery
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

cudaGetDeviceCount returned 999
-> unknown error
Result = FAIL
```

Googling the error, I find [this](https://forums.developer.nvidia.com/t/cuda-10-2-on-linux-listing-devices-gives-error-999/113151/5). Second try as root:
```
❯ sudo ./deviceQuery
./deviceQuery Starting...

 CUDA Device Query (Runtime API) version (CUDART static linking)

Detected 1 CUDA Capable device(s)

Device 0: "NVIDIA GeForce GTX 960"
  CUDA Driver Version / Runtime Version          12.5 / 12.5
  CUDA Capability Major/Minor version number:    5.2
  Total amount of global memory:                 4031 MBytes (4226613248 bytes)
  (008) Multiprocessors, (128) CUDA Cores/MP:    1024 CUDA Cores
  GPU Max Clock rate:                            1278 MHz (1.28 GHz)
  Memory Clock rate:                             3505 Mhz
  Memory Bus Width:                              128-bit
  L2 Cache Size:                                 1048576 bytes
  Maximum Texture Dimension Size (x,y,z)         1D=(65536), 2D=(65536, 65536), 3D=(4096, 4096, 4096)
  Maximum Layered 1D Texture Size, (num) layers  1D=(16384), 2048 layers
  Maximum Layered 2D Texture Size, (num) layers  2D=(16384, 16384), 2048 layers
  Total amount of constant memory:               65536 bytes
  Total amount of shared memory per block:       49152 bytes
  Total shared memory per multiprocessor:        98304 bytes
  Total number of registers available per block: 65536
  Warp size:                                     32
  Maximum number of threads per multiprocessor:  2048
  Maximum number of threads per block:           1024
  Max dimension size of a thread block (x,y,z): (1024, 1024, 64)
  Max dimension size of a grid size    (x,y,z): (2147483647, 65535, 65535)
  Maximum memory pitch:                          2147483647 bytes
  Texture alignment:                             512 bytes
  Concurrent copy and kernel execution:          Yes with 2 copy engine(s)
  Run time limit on kernels:                     Yes
  Integrated GPU sharing Host Memory:            No
  Support host page-locked memory mapping:       Yes
  Alignment requirement for Surfaces:            Yes
  Device has ECC support:                        Disabled
  Device supports Unified Addressing (UVA):      Yes
  Device supports Managed Memory:                Yes
  Device supports Compute Preemption:            No
  Supports Cooperative Kernel Launch:            No
  Supports MultiDevice Co-op Kernel Launch:      No
  Device PCI Domain ID / Bus ID / location ID:   0 / 1 / 0
  Compute Mode:
     < Default (multiple host threads can use ::cudaSetDevice() with device simultaneously) >

deviceQuery, CUDA Driver = CUDART, CUDA Driver Version = 12.5, CUDA Runtime Version = 12.5, NumDevs = 1
Result = PASS
```
Looks like we're in business 🎉. After running as root once, `$./deviceQuery` returns no error. 


>[!Warning]
>The weirdest thing: after reboot CUDA stops working until I reevaluate `sudo ./deviceQuery`. Probably related to [this](https://groups.google.com/g/caffe-users/c/bCe2cbRmV8E). ~~-> need to figure out [this install step](https://docs.nvidia.com/cuda/cuda-quick-start-guide/index.html#debian)~~.

>[!success]
>I found the commands needed to enable CUDA after reboot in [this comment](https://askubuntu.com/questions/607118/cuda-not-working-after-returning-laptop-from-sleep). 
>
>The solution suggested is antiquated, instead I created the following [`systemd` service](https://linuxhandbook.com/create-systemd-services/):
>```
>[Unit]
Description=NVIDIA settings on startup
After=multi-user.target
>
>[Service]
Type=oneshot
ExecStart=/usr/local/bin/nvidia-setup.sh
RemainAfterExit=yes
>
>[Install]
WantedBy=multi-user.target
>```
>
> which execute the following bashscript:
> ```
> #!/bin/bash
/usr/bin/nvidia-smi -pm ENABLED
/usr/bin/nvidia-smi -c EXCLUSIVE_PROCESS
>```

