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
1. Signature-based detection. Ex: [Detect It Easy](https://github.com/horsicq/DIE-engine/releases)
2. Strings, imports and exports analysis
4. PE structure analysis
5. Entropy analysis 
6. Dynamic results vs static characteristics

### Code Substitution Packers 
Understanding UPX
1. Finding the "Tail jump"
2. The importance of [VirtualProtect](https://docs.microsoft.com/en-us/windows/win32/api/memoryapi/nf-memoryapi-virtualprotect)
3. Finding the OEP
4. Dumping and fixing the unpacked PE

### 
