# Watch Out! And just skip the packer

Ekoparty BlueSpace Workshop 2021

## Requirements
* Virtual machine: https://drive.google.com/file/d/1AdC0ceCzjfADOc-Gn4veEqNFYEQwzmlX/view?usp=drivesdk

## Definitions 
* Software packer: Tool used by software developers (malicious or not) to shield programs against reverse engineering.
* Shellcode: Small piece of code that is injected and executed directly into memory. It does not comply any of the standard executable formats, it is just code. To be executed, a shellcode requires another program acting as a loader. 
* Code substitution packer: A packer that replaces parts of the original executable mapped into memory by the OS loader.
* Code injection packer: A packer that allocates new memory sections in the same process or in additional process and writes shellcode or complete PE files that will be executed.
* Hybrid packer: A packer that implements both code substitution and injection in its logic.
* Code virtualization packer: A packer that contains a virtual machine and a copy of the program ported to a custom set of instructions (only known by the VM) that are interpreted in run-time.
* OEP: *Original Entry Point*. This is where the code execution starts in the unpacked PE.
* EIP: *Extended Instruction Pointer*. CPU registry which stores the address of the instruction to be executed.
* IAT: *Import Address Table*. PE structure that contains all the information required to correctly resolve the dependencies/libraries used by the software during its execution.
* Tail jump: Instruction in which the packer execution ends and the control flow is redirected to entry point of the unpacked sample.

## Hands-On
### Is it packed?
1. Signature-based detection:

    Depending on the packer you are facing, sometimes it is super easy to recognize it just by using static analysis tools such as [Detect It Easy](https://github.com/horsicq/DIE-engine/releases) and [PEiD](https://www.aldeid.com/wiki/PEiD). This kind of tools rely on a set of signatures known for several packers, so its performance its limited when you are dealing with a custom packer; however it is always good to try it.
    
    Below an example of this kind of detection for the UPX packer in the software Detect It Easy.
    
    ![image](https://user-images.githubusercontent.com/8562692/140227209-a93b7d07-afe6-45cf-b8d4-8229c013159c.png)


2. Strings, imports and exports analysis:

    One of the main goals of a packer is to hide the valuable code and data. This is clearly visible when you statically compare a packed and an unpacked version of a software (see below, strings of the packed sample in the left and strings of the unpacked sample in the right). The amount of interesting and valuable data that is available during the static analysis in a packed software is drastically reduced.
    
    ![image](https://user-images.githubusercontent.com/8562692/140229300-c5748c5c-2ca2-449b-825e-6d5c3710ac7b.png)

3. PE structure analysis:
    
    If you look at the sections of a PE file you will find two interesting values: *raw-size* and *virtual-size*. These values inform the OS the size of each section in disk and the required space in memoy to handle its corresponding data. 
    
    In an unpacked sample these values are comparable in magnitude, however if you are dealing with a packed sample; sometimes you could see a huge difference between those values, this is a great indicator that something is hidden. Below, the information of each PE section is provided for both the packed sample (left) and unpacked sample (right). 
    
    ![image](https://user-images.githubusercontent.com/8562692/140231353-3c6b4197-d1a2-4806-9fe7-f148ee096456.png)

4. Entropy analysis 
    
    Entropy in the context of information, can be defined as the average level of "uncertainty" in the outcome of a variable. In other words, the higher the entropy the more random a variable looks like. 
    
    This is important when you are dealing with packers, because they usually apply cryptographic algorithms to protect the data; increasing in this way the entropy of the final sample. Long story short, a sample with high entropy is more likely to have encrypted data or being packed. See below an entropy comparison between a packed (left) and an unpacked sample (right).
    
    ![image](https://user-images.githubusercontent.com/8562692/140231605-67130b78-fdd7-4012-b0ab-5a8437dac2f5.png)

5. Dynamic results vs static characteristics:

    This validation is quite simple, just execute the sample in your VM and compare the behavior with the static characteristics of the sample (strings, imports, exports); if there's a mismatch between both analyses, it is clear that something is hiding the true nature of the sample.

### Code Substitution Packers 
Understanding UPX
1. Finding the "Tail jump"
2. The importance of [VirtualProtect](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualprotect)
3. Finding the OEP
4. Dumping and fixing the unpacked PE

### Hybrid Packers (Injection - Substitution) 
1. The importance of [VirtualAlloc](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualalloc), [LocalAlloc](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-localalloc) and [GlobalAlloc](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-globalalloc)

![image](https://user-images.githubusercontent.com/8562692/140280380-e51f08ad-a176-4f48-aa8f-a4da32edbb56.png)
     
2. Finding first injected shellcode (LocalAlloc)

![image](https://user-images.githubusercontent.com/8562692/140274435-652cae1f-a34d-46b7-8f61-01fb774676d0.png)
![image](https://user-images.githubusercontent.com/8562692/140274562-41ce1163-6386-4334-900e-d435f0d7bd7e.png)

3. Finding second injected shellcode (VirtualAlloc)

![image](https://user-images.githubusercontent.com/8562692/140274983-5487bb9b-ba3b-42fd-aafb-826047d3b2ad.png)
![image](https://user-images.githubusercontent.com/8562692/140273981-22e08c0d-fd73-4ca2-afb4-77e0573025c2.png)

4. Payload decryption (VirtualAlloc)

![image](https://user-images.githubusercontent.com/8562692/140275736-e165e32e-8c7f-4e62-a0fc-d712fe7e00c4.png)
![image](https://user-images.githubusercontent.com/8562692/140275862-eef1e23c-5b4a-43d9-856e-2a168ea10fdb.png)

5. Code substitution (VirtualProtect)

![image](https://user-images.githubusercontent.com/8562692/140276292-8a1577ce-df14-4278-bf25-3322d3e51c89.png)

6. Finding the "Tail jump"

![image](https://user-images.githubusercontent.com/8562692/140276841-d722df0e-34bf-450f-8a49-64f02adfcdd0.png)

7. Finding the OEP

![image](https://user-images.githubusercontent.com/8562692/140277622-893bde4c-0270-4c38-befd-67b29b4f6a1c.png)

8. Dumping unpacked PE

![image](https://user-images.githubusercontent.com/8562692/140277373-c9db991d-540c-4500-bb8a-b65cb2fa6f02.png)

9. Fixing IAT

![image](https://user-images.githubusercontent.com/8562692/140277952-1ad3ce16-7b75-40af-ba3e-dfaf457f0f6b.png)
