---
title: How to Install Tools for the Command Line
author: Johnson Laguerre
---

Originally published on Tuesday, March 21, 2023.

## Introduction

Command line tools are great, but how do you actually *get* them? They are often found built-in on IDEs like [Visual Studio](https://visualstudio.microsoft.com/vs/compare/), [Xcode](https://developer.apple.com/xcode/), or [IntelliJ](https://www.jetbrains.com/idea/),  which is convenient, but if you want to use them in the terminal, there are a few different methods for installation, including:

* Package downloads, which bundle different tools together.

* Package managers, tools that you tell what packages to download.

* Hypervisors, which let you run a different operating system on your computer.

* Build tools and runtime environments, which allow you to build and run executable files.


After explaining these methods, I will offer my personal recommendations for each operating system (OS) and end this guide with a [small list of tools you'll likely find helpful](#tools).

While reading this guide, please keep the following things in mind:

* The following information pertains only to Windows, macOS, and Linux OSes. When I use the phrase "any OS", I'm referring solely to these three operating systems.

* Some options depend on your computer having certain hardware and software specifications (e.g., processor type, operating system version), so pay attention to that information on product websites. Keywords include **"system requirements"** and **"supported platforms"**.

## Package downloads

Think of these as bundles of files. They can be bundles of source code or executables. <sup>[[1]](#package-downloads-references)</sup> If you've ever used a ZIP file, then you've dealt with a package.

If a package contains only source files, then you need to "build" the combined files into a working executable. <sup>[[2]](#package-downloads-references)</sup> If a package contains just executables, then you can use those files directly. To avoid the hassle of building, you should either download packages containing executables or let your [package manager](#package-managers) handle building things from source. **Only download packages from official websites and sources you trust.**

Example(s):

* [Command Line Tools for Xcode](https://mac.install.guide/commandlinetools/index.html) for macOS.

	* Gives access to GCC and LLDB (which is very similar to GDB).

## Package managers

These are programs that you tell what to install for you. <sup>[[3]](#package-managers-references)</sup> They are used on the command line and may have a user interface, such as Ubuntu's optional `aptitude` package manager.

Example(s):

* [`apt`](https://ubuntu.com/server/docs/package-management), which is the default on Ubuntu and other Linux distributions.

	* Gives access to many tools.

* [`aptitude`](https://wiki.debian.org/Aptitude?action=show&redirect=aptitude), which is optional on Ubuntu and other Linux distributions.

	* Gives access to many tools.

* [Homebrew](https://brew.sh) for macOS.

	* Gives access to many tools.

* [`winget`](https://learn.microsoft.com/en-us/windows/package-manager/winget/) for Windows.

	* Gives access to many tools.

## Hypervisors

These let you run "guest" OSes on your computer by creating a virtual machine (VM). <sup>[[4]](#hypervisors-references)</sup> So if you wanted access to Linux tools, you would run a Linux distribution in the VM. If you wanted access to macOS tools, you would run macOS in the VM. A downside is that [using VMs can be resource-intensive](#windows-wsl).

This is ***not*** the same as dual-booting, which only allows you to select one OS to use when your computer starts. <sup>[[5]](#hypervisors-references)</sup> Dual-booting has its advantages but also certain disadvantages like having to reboot your computer to switch to your other OS and needing to make sure you don't overwrite data saved on your other OS. <sup>[[6]](#hypervisors-references)</sup>

Example(s):

* [WSL](https://learn.microsoft.com/en-us/windows/wsl/install) for Windows.

	* Gives access to many tools.

* [VMware Workstation Player](https://www.vmware.com/products/workstation-player.html) for Windows and Linux.
	
	* Gives access to many tools.
	
	* I recommend obtaining the no-cost Personal Use License if you intend to develop software for personal or non-commerical purposes.
	
* [VMware Fusion Player](https://www.vmware.com/asean/products/fusion/fusion-evaluation.html) for macOS.

	* Gives access to many tools.

	* I recommend obtaining the no-cost Personal Use License if you intend to develop software for personal or non-commerical purposes.

* [VirtualBox](https://www.virtualbox.org/manual/UserManual.html#hostossupport) for any OS.

	* Gives access to many tools.

## Build tools and runtime environments

Build tools are what you use to compile source files <sup>[[2]](#package-downloads-references)</sup> and link the resulting object files together to form one executable file <sup>[[7]](#build-tools-and-runtime-environments-references)</sup>.

Runtime environments provide files, such as library files, for an executable to run. <sup>[[7]](#build-tools-and-runtime-environments-references)</sup> <sup>[[8]](#build-tools-and-runtime-environments-references)</sup>

I found [an article by a software developer named David Xiang](https://davidxiang.com/2021/02/26/what-is-a-runtime-environment/) that helps explain some of the terminology around runtime environments.

While they are two separate concepts, if you're developing software, you will often find that build tools and runtime environments come packaged together.

Example(s):

* [MSYS2](https://www.msys2.org/) for Windows.
	
	* Gives access to many tools.
	
	* Composed of three subsystems: `msys2`, `mingw32`, and `mingw64`. <sup>[[9]](#build-tools-and-runtime-environments-references)</sup>
	
		* The `msys2` subsystem uses its own unique version of the `pacman` package manager. <sup>[[10]](#build-tools-and-runtime-environments-references)</sup> It should only ever be used in the `msys2` shell. <sup>[[11]](#build-tools-and-runtime-environments-references)</sup>
		
			* This subsystem gives access to many tools.
		
		* The `mingw64` subsystem is for building 64-bit Windows-compatible software using the packages and tools provided by the `msys2` subsystem. <sup>[[12]](#build-tools-and-runtime-environments-references)</sup>
			
			 * This subsystem uses the MinGW-w64 runtime headers and libraries to link Windows-compatible software against. <sup>[[13]](#build-tools-and-runtime-environments-references)</sup> 
			 
			 * This subsystem gives access to GCC and GDB.

			* Note: MinGW-w64 can be used on any OS, but it is used for building Windows-compatible software. <sup>[[14]](#build-tools-and-runtime-environments-references)</sup> 
			
		* The `ming32` subsystem like like `mingw64` subsystem, except it is used for building 32-bit Windows-compatible software. <sup>[[15]](#build-tools-and-runtime-environments-references)</sup>
		
	* See what packages are available to each subsystem [on the MSYS2 Packages' "Repos" pages](https://packages.msys2.org/repos).

## Personal Recommendations

### Windows: WSL

WSL only takes a small amount of work to set up and provides direct access to a Linux environment and all its tools. 

Their FAQs say that it ["requires fewer resources (CPU, memory, and storage) than a full virtual machine"](https://learn.microsoft.com/en-us/windows/wsl/faq) <sup>[[16]](#personal-recommendations-references)</sup>, which is great if you want to keep resource usage low.

### macOS: Homebrew

Although it doesn't give you direct access to a Linux environment, you can still access many of the same tools and have your computer use fewer resources than if you were using a VM.

### Linux: Your package manager

Linux distributions come equipped with a package manager by default, so check what yours is and what package repositories you have access to.

On Ubuntu, for example, you can search the repository from the command line using `apt` or [check the list online](https://packages.ubuntu.com/).

## Tools

* [Diffutils](https://www.gnu.org/software/diffutils/) (displaying differences between files).

* [GCC](https://www.gnu.org/software/gcc/) (compiler).

* [GDB](https://www.sourceware.org/gdb/) (debugger).

* [Git](https://git-scm.com/downloads) (version control, seeing file history, sharing repositories).
	* Has built-in [diff](https://git-scm.com/docs/git-diff) and [grep](https://git-scm.com/docs/git-grep) capabilities.

* [Grep](https://www.gnu.org/software/grep/) (searching files for text).

* [LLDB](https://lldb.llvm.org/) (debugger, very similar to GDB).

* [Nano](https://www.nano-editor.org/) (command line text editor).

* [Valgrind](https://valgrind.org/) (checking for memory leaks).

* [Vim](https://www.vim.org/) (command line text editor).

## References

### "Package downloads" references

1. Package format. (2022, December 3). In *Wikipedia*. https://en.wikipedia.org/w/index.php?title=Package_format&oldid=1125350692

	* Licensed under the [Creative Commons Attribution-ShareAlike License 3.0](https://creativecommons.org/licenses/by-sa/3.0/).

2. Software build. (2023, March 13). In *Wikipedia*. https://en.wikipedia.org/w/index.php?title=Software_build&oldid=1144461115

	* Licensed under the [Creative Commons Attribution-ShareAlike License 3.0](https://creativecommons.org/licenses/by-sa/3.0/).
	
### "Package managers" references

3. Package manager. (2023, February 19). In *Wikipedia*. https://en.wikipedia.org/w/index.php?title=Package_manager&oldid=1140335838

	* Licensed under the [Creative Commons Attribution-ShareAlike License 3.0](https://creativecommons.org/licenses/by-sa/3.0/).

### "Hypervisors" references

4. Hypervisor. (2022, October 16). In *Wikipedia*. https://en.wikipedia.org/w/index.php?title=Hypervisor&oldid=1116410861

	* Licensed under the [Creative Commons Attribution-ShareAlike License 3.0](https://creativecommons.org/licenses/by-sa/3.0/).

5. Multi-booting (2023, February 22). In *Wikipedia*. https://en.wikipedia.org/w/index.php?title=Multi-booting&oldid=1140898846

	* Licensed under the [Creative Commons Attribution-ShareAlike License 3.0](https://creativecommons.org/licenses/by-sa/3.0/).
	
6. Emmanuel. (2021, November 15). *10 risks when dual booting operating systems.* FOSS Linux. Retrieved March 18, 2023, from https://www.fosslinux.com/49511/risks-dual-booting-operating-systems.htm

	* ©2016-2023 FOSS LINUX, A PART OF VIBRANT LEAF MEDIA COMPANY. ALL RIGHTS RESERVED.

### "Build tools and runtime environments" references

Note: Publication dates listed below for each MSYS2 and MinGW-w64 pages are based on the initial commits of each individual page to the respective websites' GitHub repositories.

[To see the MSYS2 website's repository history, click here](https://github.com/msys2/msys2.github.io).

[To see the MinGW-w64 website's repository history, click here](https://github.com/mingw-w64/mingw-w64.github.io).

---

7. Linker (computing). (2023, February 16). In *Wikipedia*. https://en.wikipedia.org/w/index.php?title=Linker_(computing)&oldid=1139688758

	* Licensed under the [Creative Commons Attribution-ShareAlike License 3.0](https://creativecommons.org/licenses/by-sa/3.0/).

8. Runtime system. (2023, March 9). In *Wikipedia*. https://en.wikipedia.org/w/index.php?title=Runtime_system&oldid=1143699020

	* Licensed under the [Creative Commons Attribution-ShareAlike License 3.0](https://creativecommons.org/licenses/by-sa/3.0/).

9. Reiter, C., & Macek, D. (2017, February 2). *MSYS2-Introduction*. MSYS2. Retrieved March 20, 2023, from https://www.msys2.org/wiki/MSYS2-introduction/#subsystems

	* Licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

10. Reiter, C., Sobisch, S., tocic, & Macek, D. (2020, June 27). *Package Management*. MSYS2. Retrieved March 20, 2023, from https://www.msys2.org/docs/package-management/#package-repositories

	* Licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

11. Reiter, C., & R., Macek, D. (2017, February 2). *MSYS2-Introduction*. MSYS2. Retrieved March 20, 2023, from https://www.msys2.org/wiki/MSYS2-introduction/#path

	* Licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

12. Reiter, C., Wang, G., Rehberg, S., Macek, D., & Yeaw, D. (2017, February 2). *Creating Packages*. MSYS2. Retrieved March 20, 2023, from https://www.msys2.org/wiki/Creating-Packages/#which-subsystem

	* Licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

13. Reiter, C., & Macek, D. (2021, July 9). *MSYS2 History*. MSYS2. Retrieved March 20, 2023, from https://www.msys2.org/wiki/History/#mingw-w64

	* Licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
	
14. GalaxySnail, Podsvirov, K., Chinoune, M., Storsjö, M., Sanders, B., Reiter, C.,  Nath, B., Hao L., Guyutongxue, & Clauss, C. (2017, February 2). *Downloads*. MinGW-w64. Retrieved March 20, 2023, from https://www.mingw-w64.org/downloads/

	* Licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
	
15. Reiter, C., & Macek, D. (2017, February 2). *How does MSYS2 differ from Cygwin?*. MSYS2. Retrieved March 20, 2023, from https://www.msys2.org/wiki/How-does-MSYS2-differ-from-Cygwin/

	* Licensed under the [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).

### "Personal Recommendations" references

16. Loewen, C., NotTheDr01ds, Buck, A., Wojciakowski, M., Junker, A., LeMoine, P., v-chmccl, & v-surgos. (n.d.). *Frequently Asked Questions about Windows Subsystem for Linux*. Microsoft Learn. Retrieved March 18, 2023, from  https://learn.microsoft.com/en-us/windows/wsl/faq

	* © Microsoft 2023. All rights reserved.

---

References are in APA 7 format. References are listed in order of first appearance in this document.

Followed Purdue OWL's *APA Formatting and Style Guide (7th Edition)*, found here: https://owl.purdue.edu/owl/research_and_citation/apa_style/apa_formatting_and_style_guide/index.html

---

## Copyright/Licensing

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons License" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />This work is licensed under the <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Attribution-ShareAlike 4.0 International License</a>.

