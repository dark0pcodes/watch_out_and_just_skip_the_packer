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
* IAT:
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
