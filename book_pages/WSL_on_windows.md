# Using the Unix command line on Windows
In this course we will become familiar with the Unix command line. macOS includes a Terminal app and many Unix utilities by default, but Windows does not. By installing Windows Subsystem for Linux 2 (WSL2) you can run a full Linux environment on your Windows machine without dual-booting or using another computer. WSL2 is tightly integrated with Windows and lets you install popular distributions such as Ubuntu.

This is thanks to the introduction of [Windows Subsystem for Linux 2 (WSL2) by Microsoft](https://learn.microsoft.com/en-us/windows/wsl/about). It allows you to install various Linux distributions, such as Ubuntu. It is tightly integrated into Windows. For example, it can access files in your Windows file system.

## Starting on WSL2
There is no place better than the official channel for the installation instructions. [Here is the full Microsoft documentation on how to create a WSL2 development environment in Windows](https://learn.microsoft.com/en-us/windows/wsl/setup/environment). We will stick with the [default](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#get-started), that is, typing in PowerShell:
```powershell
wsl --install
```

We will keep following [the above guide](https://learn.microsoft.com/en-us/windows/wsl/setup/environment). We will
- [Set up your Linux username and password](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#set-up-your-linux-username-and-password)
- [Update and upgrade packages](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#update-and-upgrade-packages)

It is recommended that you use Windows Terminal, a useful terminal that hosts the WSL2 command-line shells. You can customize how your terminal looks! We will use the section on 
- [Set up Windows Terminal](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#set-up-windows-terminal)

WSL2 can access your Windows files, and you can access your WSL2 files from Windows File Explorer. This is described in the section on
- [File storage](https://learn.microsoft.com/en-us/windows/wsl/setup/environment#file-storage)

We will end here. We will go further into the documentation about code editors and Git when we learn those.