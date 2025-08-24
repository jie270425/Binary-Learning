# two cups of tea
1. 首先打开该exe文件,发现要求输入flag
   ![01](./picture/01.png)
2. 使用DIE检查是否套壳,发现无壳
3. 使用IDA对其进行逆向分析,从而找到`main()`函数
   ![02](./picture/02.png)
   对代码进行分析,v15为加密过后的flag
4. 利用python写出解密代码