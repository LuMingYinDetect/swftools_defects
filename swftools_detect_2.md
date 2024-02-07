Affected Version:
swftools 0.92 772e55a271f66818b06c6e8c9b839befa51248f4

Vulnerability Description:
The vulnerability is a memory leak bug located at line 1113 of the file /swftools/lib/modules/swfaction.c. This vulnerability could potentially be exploited maliciously to cause resource exhaustion and denial of service attacks.

swftools download address:
https://github.com/matthiaskramm/swftools.git

1.A pointer variable named 'tag' is defined at line 1104 of the file /swftools/lib/modules/swfaction.c, and is assigned a dynamically allocated memory area by the function swf_InsertTag at line 1110, as shown in the diagram below:

![image](https://github.com/LuMingYinDetect/swftools_defects/blob/main/swftools_4.png)

2.In the swf_InsertTag function, a pointer named 't' is defined at line 1129. This pointer is assigned a dynamically allocated memory area by the function rfx_calloc at line 1131, and is returned at line 1141. Due to the NULL value passed into the 'after' variable in the swf_InsertTag function from the upper layer, the condition of the if statement at line 1134 evaluates to false, as illustrated in the diagram below:

![image](https://github.com/LuMingYinDetect/swftools_defects/blob/main/swftools_5.png)

3.At line 69 of the rfx_calloc function, the calloc function is called to allocate a memory area, and it is returned at line 81, as depicted in the diagram below:

![image](https://github.com/LuMingYinDetect/swftools_defects/blob/main/swftools_6.png)

4.Ultimately, when the program returns from line 1113, the dynamically allocated memory area pointed to by the variable 'tag' is not released, resulting in a memory leak, as illustrated in the diagram below:

![image](https://github.com/LuMingYinDetect/swftools_defects/blob/main/swftools_7.png)
