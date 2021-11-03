# Watch Out! And just skip the packer

Ekoparty BlueSpace Workshop 2021

## Requirements
* Máquina virtual: https://drive.google.com/file/d/1AdC0ceCzjfADOc-Gn4veEqNFYEQwzmlX/view?usp=drivesdk

## Definitions 
* Software packer: Tool used by software developers (malicious or not) to shield programs against reverse engineering.
* Anti-analysis techniques:
* Signature avoidance:
* Shellcode:
* Code substitution:
* Code injection:
* Code virtualization:
* OEP:
* EIP:
* Packer stub:
* Payload:
* Tail jump:

## Hands-On
### Is it packed?
1. Signature-based detection:

    Depending on the packer you are facing, it could be easily detected Ex: [Detect It Easy](https://github.com/horsicq/DIE-engine/releases)
    
    ![image](https://user-images.githubusercontent.com/8562692/140227209-a93b7d07-afe6-45cf-b8d4-8229c013159c.png)


2. Strings, imports and exports analysis
    dfsdfsdfsdf
    
    ![image](https://user-images.githubusercontent.com/8562692/140229300-c5748c5c-2ca2-449b-825e-6d5c3710ac7b.png)

3. PE structure analysis
    hfhgffhgfh
    
    ![image](https://user-images.githubusercontent.com/8562692/140231353-3c6b4197-d1a2-4806-9fe7-f148ee096456.png)

4. Entropy analysis 
    sdfadfasdasd
    
    ![image](https://user-images.githubusercontent.com/8562692/140231605-67130b78-fdd7-4012-b0ab-5a8437dac2f5.png)

5. Dynamic results vs static characteristics

### Code Substitution Packers 
Understanding UPX
1. Finding the "Tail jump"
2. The importance of [VirtualProtect](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualprotect)
3. Finding the OEP
4. Dumping and fixing the unpacked PE

### Hybrid Packers (Injection - Substitution) 
1. The importance of [VirtualAlloc](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualalloc), [LocalAlloc](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-localalloc) and [GlobalAlloc](https://docs.microsoft.com/en-us/windows/win32/api/winbase/nf-winbase-globalalloc)
2. Finding the "shellcode"
4. Finding the "Tail jump"
5. Finding the OEP
4. Dumping and fixing the unpacked PE
