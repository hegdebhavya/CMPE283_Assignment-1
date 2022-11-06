# CMPE283_Assignment1
## Virtualization Technologies Assignment 
Name: Bhavya Hegde <br>
SJSU ID: 016656029 <br>
Email: bhavya.hegde@sjsu.edu <br>


## Steps to create Linux kernel module that will query various MSRs to determine virtualization features available in your CPU

* Please use VMware Workstation/Player and setup an Ubuntu Virtual machine. Navigate to the settings of the virtual machine and enable Virtualize Intel VT-x/EPT setting under Virtual Machine Settings > Hardware > Device > Processor as seen below

![image](https://user-images.githubusercontent.com/85700971/200153933-de27a127-620a-4d5f-b328-b01476feaf03.png)

* Install ‘gcc’ and ‘make’ packages using command seen below

![image](https://user-images.githubusercontent.com/85700971/200153988-60a8cb3a-b642-4c06-8f89-833dc7222830.png)

* Install the Linux header files for Linux kernel 

![image](https://user-images.githubusercontent.com/85700971/200154006-c1aca47a-038a-4a30-8a93-7c60cfeaf436.png)

* The $(uname -r ) command returns the version of Linux running in the virtual machine, we now move our cmpe283-1.c and Makefile to the virtual machine and execute the ‘make’ command. Once the ‘make’ command is executed we obtain the kernel module file ‘cmpe283-1.ko’. The compile process can be seen in the screenshot below

![image](https://user-images.githubusercontent.com/85700971/200154031-b40a98fc-d896-4a2c-adb6-3d579dd52e62.png)

* Run ‘insmod cmpe283-1.ko’ to insert our kernel module and ‘rmmod cmpe283-1.ko’ to remove the module

![image](https://user-images.githubusercontent.com/85700971/200154061-342d3770-eb0d-4a6b-b041-b883a0dd2c5e.png)

* We can see the output of this module using ‘dmesg’ command and the corresponding logs can be seen in the three screenshots below
* 
![image](https://user-images.githubusercontent.com/85700971/200154083-12d16cca-b474-4ea5-94d0-fffdf1df0ee9.png) <br>

![image](https://user-images.githubusercontent.com/85700971/200154111-1b2f6b80-f217-429c-9fae-cd481a74308f.png)  <br>

![image](https://user-images.githubusercontent.com/85700971/200154118-9ece257b-d9c1-4244-806a-4c6ead3074af.png)










