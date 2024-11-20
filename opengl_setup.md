# How to Install OpenGL on Debian Linux in WSL2
These steps have been tested on Windows 11 with WSL2 running Debian.


## 1. Dependencies
First install the dependencies:
```bash
apt install mesa-utils libglu1-mesa-dev freeglut3-dev mesa-common-dev
```
There are more than we need, but also include GLut and Glu libraries to link aginst during compilation for application development (these can be removed if that functionality is not required).


## 2. Window Server
### Installing
Then, you will need to setup a window server. Windows 11 should have this built in and work out of the box (skip to step 3). **We don't include windows server installation steps as we assume development on Windows 11**

## 3. Running a Test
After the following configuration you should be able to run the test application below and see some multi-colored gears spinning:
```bash
glxgears
```

# APU(iGPU) / GPU Setup:
Use the following to find out what GPU it is using:
```bash
glxinfo | grep "OpenGL renderer"
```

If it isn't your preferred GPU use the following command to point to your GPU:
```bash
export MESA_D3D12_DEFAULT_ADAPTER_NAME=NVIDIA
```
The example above sets the environment variable to the first GPU titled "NVIDIA" so check with Device Manager and type the exact beginning letters so that it selects the correct option.