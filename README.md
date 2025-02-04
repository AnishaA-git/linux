#   ASSIGNMENT-4

*	Individual Contributions
Anisha Agarwal:
•  Analyzed the behaviour of exits after disabling the nested paging.
•  Analyzed the changes between the two runs that is ept vs no ept.

Jeena Thampi:
•   Implemented the commands as given for assignment-4, so that kvm uses shadow paging instead of nested paging.
•   Analyzed the test results, and as per the expectations the number of exits increased when switched from nested to shadow paging.

*  Include a sample of your print of exit count output from dmesg from “with ept” and “without ept”.
- **Shadow Paging1**
![Shadow Paging1](https://user-images.githubusercontent.com/70603792/101979271-944ab780-3c10-11eb-88b8-b7b8c0a956d6.png)
- **Shadow Paging2**
![Shadow Paging2](https://user-images.githubusercontent.com/70603792/101979275-990f6b80-3c10-11eb-8b43-f5768d0f18c3.png)
- **Nested Paging1**
![Nested Paging1](https://user-images.githubusercontent.com/70603792/101979280-9b71c580-3c10-11eb-8eaa-733b1aac42f1.png)
- **Nested Paging2**
![Nested Paging2](https://user-images.githubusercontent.com/70603792/101979282-9d3b8900-3c10-11eb-96be-a93b0a163bec.png)

*  What did you learn from the count of exits? Was the count what you expected? If not, why not?
    •   The count of exits increased when the EPT was set to 0 which means when we forced the kvm to use shadow paging instead of nested paging.
    •   As per the class understanding of nested and shadow paging, the expectations was that there should be an increase in exit counts as shadow 
        paging involves more number of exits then nested paging. And the count was increased as expected.

*  What changed between the two runs (ept vs no-ept)?
    •   There are 2 exits, INVLPG, exit reason = 14 and INVPCID, exit reason = 58, which happens in shadow paging and is 0 in nested paging.
    •   As a result: With EPT the kvm works as per nested paging and thus the exits are lesser. Without EPT the kvm is forced to work as per shadow paging and gives an 
        increase in exits



#   ASSIGNMENT-3

*	Individual Contributions
Anisha Agarwal:
•	Used the setup of assignment-2, after creating a new leafnode of 0x4FFFFFFE analyzed the frequency of exits. 
•   Analyzed if the exits were increased while performing VM operation.
•   Analyzed the different exit types and which were least and most frequent among them.

Jeena Thampi:
•   Implemented the code for assignment 3, analyzed where to add the code for creating a new leafnode of 0x4FFFFFFE.
•   Researched and analyzed where to add the coonditions to fulfill the requirement of assignment-3.
•   Compiled, test and debugged the code to get the desired output.

*	Steps adopted to complete the assignment
a)	Install virt-manager
b)	Created the inner VM by following the steps in virt manager for testing
c)	Did the following to build kernel
    a.	sudo bash
    b.	make && make modules && make install && make modules_install 
    c.	Reboot
    
d)	Get the inner VM ready to test by following the below steps
    a.	sudo apt-get install cpuid
    b.	If it says E: Unable to locate package cpuid, then do the following
    c.	Check if package is available for the ubuntu version
    d.	Run the below command to get the codename
        i.	lsb_release -a
        ii.	ubuntu@ubuntu:~$ lsb_release -a
        iii.	No LSB modules are available.
        iv.	Distributor ID:        Ubuntu
        v.	Description:        Ubuntu 20.04.1 LTS
        vi.	Release:        20.04
        vii.	Codename:        focal
    e.	Check in there if package is available and in which repository
    f.	https://packages.ubuntu.com/search?keywords=cpuid&searchon=names&suite=focal&section=all

    g.	sudo add-apt-repository “repository name”
    h.	sudo apt-get update
    i.	sudo apt-get install cupid
    
*	Questions
    a.	Does the number of exits increase at a stable rate?
        No, the number of exits does not increase at a stable rate, however they increase randomly.
    b.	Are there more exits performed during certain VM operations?
        Yes, more exits are performed during certain VM operations like opening a browser or opening a file or performing any other operations. 
    c.	Approximately how many exits does a full VM boot entail?
        Approximately ~1000000 many exits are performed during a full VM boot entail, which is calculated by taking the difference between number of exits before and after the reboot.
        
*  Of the exit types defined in the SDM, which are the most frequent? Least?
    a.  Frequent: EPT violation, exit reason 48 is the most frequent exit occured.
    b.  Least: MOV DR, exit reason 29 and Access to LDTR or TR, exit reason 47 are the most least exits occured.

#   ASSIGNMENT-2

1.	Individual Contributions
Anisha Agarwal:
•	Did the setup on mac OS using external hard disk.
•	Researched on how to calculate the clock cycles during exit.
•	Researched on where to place the code for clock cycles.
•	Researched and analyzed on the behaviour of exits for question-3.
•	Implemented the code for clock cycles. Compile, test and debug the code.

Jeena Thampi:
•	Did the setup on mac OS.
•	Researched on atomic variable and how to use them in the code.
•	Researched on where to place and implemented the code to calculate total number of exits.
•	Researched on how to extract high and low bits.
•	Compile, test and debug the code.

2.	Steps adopted to complete the assignment
a)	Install virt-manager
b)	Created the inner VM by following the steps in virt manager for testing
c)	Did the following to build kernel
    a.	sudo bash
    b.	apt-get install build-essential kernel-package fakeroot libncurses5-dev libssl-dev ccache bison flex libelf-dev
    c.	uname -a 
    d.	cp /boot/config-5.4.52-generic ./.config 
    e.	make oldconfig 
    f.	make && make modules && make install && make modules_install 
    g.	Reboot
d)	Fixed the error after reboot : “UUID does not exist” by doing the following steps
    a.	From GRUB menu selected the older version and booted the system
    b.	Sudo apt-get clean
    c.	Df -h to make sure filesystems on disk are not 100%
    d.	sudo update-initramfs -k 5.9.0+ -u
    e.	Reboot again
e)	Get the inner VM ready to test by following the below steps
    a.	sudo apt-get install cpuid
    b.	If it says E: Unable to locate package cpuid, then do the following
    c.	Check if package is available for the ubuntu version
    d.	Run the below command to get the codename
        i.	lsb_release -a
        ii.	ubuntu@ubuntu:~$ lsb_release -a
        iii.	No LSB modules are available.
        iv.	Distributor ID:        Ubuntu
        v.	Description:        Ubuntu 20.04.1 LTS
        vi.	Release:        20.04
        vii.	Codename:        focal

    e.	Check in there if package is available and in which repository
    f.	https://packages.ubuntu.com/search?keywords=cpuid&searchon=names&suite=focal&section=all

    g.	sudo add-apt-repository “repository name”
    h.	sudo apt-get update
    i.	sudo apt-get install cupid

3.	Questions
    a.	Does the number of exits increase at a stable rate?
       No, the number of exits does not increase at a stable rate, however they increase randomly.
    b.	Are there more exits performed during certain VM operations?
       Yes, more exits are performed during certain VM operations like opening a browser or opening a file or performing any other operations. 
    c.	Approximately how many exits does a full VM boot entail?
       Approximately ~1000000 many exits are performed during a full VM boot entail, which is calculated by taking the difference between number of exits before and after the reboot.


Linux kernel
============

There are several guides for kernel developers and users. These guides can
be rendered in a number of formats, like HTML and PDF. Please read
Documentation/admin-guide/README.rst first.

In order to build the documentation, use ``make htmldocs`` or
``make pdfdocs``.  The formatted documentation can also be read online at:

    https://www.kernel.org/doc/html/latest/

There are various text files in the Documentation/ subdirectory,
several of them using the Restructured Text markup notation.

Please read the Documentation/process/changes.rst file, as it contains the
requirements for building and running the kernel, and information about
the problems which may result by upgrading your kernel.
