# speed
1. 首先打开该exe文件,发现弹窗跳出来的一瞬间就没了
2. 使用DIE查看有没有壳,发现没有壳
3. 使用IDA对其进行逆向分析,发现该文件会创建一个窗口  
   对创建窗口的部分函数进行分析得,该窗口会在生成1ms后直接销毁,所求的flag则在`WndProc`中,且在程序运行时会将flag显示
4. 使用动态调试在`Sleep(1u);`处设置断点,并调试程序,获得flag`moectf{Just_dyn@mic_d3bugg1ng}`
   ![01](./picture/01.png)