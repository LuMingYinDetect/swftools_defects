Affected Version
swftools 772e55a271f66818b06c6e8c9b839befa51248f4(The latest commit of the software)

Vulnerability Description
The vulnerability is a memory leak bug located at line 1072 of the file /project/swftools/lib/modules/swftext.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

swftools download address
https://github.com/matthiaskramm/swftools.git

1. A memory leak vulnerability was discovered on line 1072 of the file /project/swftools/lib/modules/swftext.c. A pointer named 'ofs' was dynamically allocated memory by the function 'rfx_alloc' on line 1068, as shown in the diagram below:
![image](https://github.com/LuMingYinDetect/swftools_defects/blob/main/swftools_1.png)
2.At line 23 of the rfx_alloc function, a pointer variable named 'ptr' is defined. This pointer variable is dynamically allocated memory by the malloc function at line 30 and is returned at line 36, as illustrated in the diagram below:
![image](https://github.com/LuMingYinDetect/swftools_defects/blob/main/swftools_2.png)
3.Following that, the program returns -1 at line 1072 without releasing the memory area pointed to by the variable 'ofs' before the return, as illustrated in the diagram below:
![image](https://github.com/LuMingYinDetect/swftools_defects/blob/main/swftools_3.png)
