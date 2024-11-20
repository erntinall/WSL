# Table of Contents
1. [How to use WSL with VS Code to Utilize Linux Natively in Development](#How-to-use-WSL-with-VS-Code-to-Utilize-Linux-Natively-in-Development)
    1. [Setup WSL Using the Terminal](#1-setup-wsl-using-the-terminal)
    2. [Setup WSL to Interact with VS Code](#2-setup-wsl-to-interact-with-vs-code)
2. [Using WSL to Interact with Linux and VS Code](#using-wsl-to-interact-with-linux-and-vs-code)
3. [Debugging Errors with WSL and VS Code](#debugging-errors-with-wsl-and-vs-code)

# How to use WSL with VS Code to Utilize Linux Natively in Development
To contextualize my reasoning for finding this out stems from how I studied C, Web, and ASM development which was largely based on using Red Hat/CentOS linux. Moving from that to Windows has led to multiple roadblocks which included ***how slow Visual Studio ran on my PC*** as well as ***my preference towards VS Code as an IDE due to how extensible it was*** and ***how easy it was to pick up for developers of any experience to work just like a text editor.*** 

Given that, this is one setup of many to develop in C/C++/Java/Python/etc. and I aspire any person who almost loves this setup to create their own setup and document it for other developers! ❤️

## 1. Setup WSL Using the Terminal
AFAIK WSL2 is supported on Windows Home and Pro editions[[1]](https://learn.microsoft.com/en-us/windows/wsl/faq).

Head over to your favorite terminal and type in the following to show all available linux versions through WSL:
```
wsl --list --online
```
To keep things simple, we will use Debian as it provides huge community support.
```
wsl --install debian
```
It will go through a typical cli debian installation and ask for a root password, keep this noted as it will be used to use sudo.

## 2. Setup WSL to Interact with VS Code
After Debian (or other nix distro) is setup go to your VS Code and head over to the extensions tab and install ["WSL"](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl).

After installing it may prompt with setup and from here you have two options:
1. Connect to your WSL instance through VS Code
2. Input ```code .``` into your WSL instance to open the current directory as the working space in VS Code.

From here you can create new files in VS Code and it will show in your WSL directory.

# Using WSL to Interact with Linux and VS Code
Now that you have WSL with VS Code setup you are either 1 of 2 people.
1. Used to developing with linux and can interact with linux as a method of compilation and separating development workspace to efficiently manage libraries and compiler versions. **This means you can install all your compilation tools on WSL (Java/Python/GCC/CMake/etc.) and use your Windows workspace to write code exclusively.**
2. New to development and want to understand the benefits of using Linux to develop applications over other methods. **This means you are, possibly, new to Linux or new to developing low level applications in C/C++.** I advise you seek out resources on learning Linux and practice separating your workspace to efficiently work on projects.

# Debugging Errors with WSL and VS Code
**Nothing is ever perfect and you can make the best of your situation by solving those imperfections.** 

I will show all the problems I faced when setting this up and how you can possibly fix them if you come across them.

## execvpe(/bin/sh) failed: No such file or directory
A couple of errors showed with this including "Failed to mount C:\" and "getpwuid(0) failed 2" after seeing that sh failed to start it signifies that WSL had a problem starting the shell which most likely attributed to a corrupted installation.

Run the following to get your list of linux versions:
```
wsl --list --verbose
```
If you see your linux version and it is asterisked (For example "* Debian Running") then try to reinstall it by inputting the following replacing "distro-name" with the version you want to install:
```
wsl --terminate <distro-name>
wsl --unregister <distro-name>
wsl --install <distro-name>
```
This will stop your instance, uninstall, and install the distro again.

## VS Code cannot connect to WSL
This occured when I shutdown the instance of WSL I had running and VS Code wouldn't connect despite retrying. It ended up connecting again after I quit VS Code and used WSL from the terminal to start VS Code using the following command:
```
code .
```