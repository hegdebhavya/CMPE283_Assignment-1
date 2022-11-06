# CMPE283_Assignment1
## Virtualization Technologies Assignment 
Name: Bhavya Hegde <br>
SJSU ID: 016656029 <br>
Email: bhavya.hegde@sjsu.edu <br>
Team members: No other team members. Individual submission.


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

![image](https://user-images.githubusercontent.com/85700971/200154083-12d16cca-b474-4ea5-94d0-fffdf1df0ee9.png) <br>

![image](https://user-images.githubusercontent.com/85700971/200154111-1b2f6b80-f217-429c-9fae-cd481a74308f.png)  <br>

![image](https://user-images.githubusercontent.com/85700971/200154118-9ece257b-d9c1-4244-806a-4c6ead3074af.png)

### Kernel module source code cmpe283-1.c:
* The different MSRs to be queried are seen in the image below <br> 

![image](https://user-images.githubusercontent.com/85700971/200154481-f5c48178-6a08-48ab-b662-391fa49bed8c.png)

* One of the control structures that I added for querying the MSR capabilities in this case Primary Processor-Based VM-execution Control is seen below <br>

![image](https://user-images.githubusercontent.com/85700971/200154502-8bd588f1-08c6-498e-88ef-be82b3caef8b.png) <br>

## The source tables of the control structure and the MSR values are provided in the comments of the source code. <br>
### IA-32 Architectural MSRs
[Intel SDM volume 4](https://www.intel.com/content/dam/develop/external/us/en/documents/335592-sdm-vol-4.pdf) <br>
Table 2-2. IA-32 Architectural MSRs <br>

###  VM-Execution Control Fields 
[Intel SDM volume 3](https://www.intel.com/content/dam/develop/public/us/en/documents/325384-sdm-vol-3abcd.pdf) <br>

#### 24.6 VM-Execution Control Fields <br>

*	24.6.1 Pin-Based VM-Execution Controls <br>
*	24.6.2 Processor-Based VM-Execution Controls <br>
Table 24-6. Definitions of Primary Processor-Based VM-Execution Controls  <br>
Table 24-7. Definitions of Secondary Processor-Based VM-Execution Controls  <br>
Table 24-8. Definitions of Tertiary Processor-Based VM-Execution Controls  <br>
*	24.7 VM-EXIT CONTROL FIELDS <br>
*	24.7.1 VM-Exit Controls Definitions of VM-Exit Controls  <br>
* Table 24-13. Definitions of VM-Exit Controls <br>
* 24.8 VM-ENTRY CONTROL FIELDS <br>
* 24.8.1 VM-Entry Controls Table 24-15. Definitions of VM-Entry Controls <br>

A bit check function was added to check the status of a bit inside a 32-bit value. We use this to query the 17th bit to check availability of Tertiary Processor-Based VM-Execution Control and 31st bit to check availability of Secondary Processor-Based VM-Execution Control in the most significant 32 bits returned by the MSR query for Primary Processor-Based VM-Execution Control.  <br>

![image](https://user-images.githubusercontent.com/85700971/200154895-e20f6ca2-a2c0-436d-b16e-890dc257ec53.png)

The availability check can be seen below <br>

![image](https://user-images.githubusercontent.com/85700971/200154948-33f2e6ee-f5ed-49f1-84a3-0f37e79d43d4.png) <br>


One of the MSR query and display code can be seen below <br>


![image](https://user-images.githubusercontent.com/85700971/200154956-2f52b395-1f1e-4036-a654-178550d34c9c.png)





























