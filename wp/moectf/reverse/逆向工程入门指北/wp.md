# 逆向工程入门指北
1. 首先打开该ELF文件
   ![01](./picture/01.png)
   发现要求输入number以获取flag
2. 使用IDA对其进行逆向分析
   按下Shift + F12对字符串进行搜寻
   ![02](./picture/02.png)
   发现flag为`moectf{open_your_IDA_and_start_reverse_engineering!!}`
3. 提交该flag发现为正确答案