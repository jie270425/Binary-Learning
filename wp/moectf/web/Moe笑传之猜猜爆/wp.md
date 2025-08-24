# Moe笑传之猜猜爆
1. 打开该网址按下`F12`，对网页源代码进行分析发现` <script src="/static/main.js"></script>`，即网页交互逻辑在`/static/main.js`中
2. 打开该页面，发现随机数randomNumber是在浏览器端用 JavaScript 生成的（范围 1-10000），这意味着我们可以直接获取这个随机数的值，无需猜测
3. 在开发者工具的`控制台`标签页中输入`randomNumber`获取当前的随机数，即可提交正确答案获得flag
4. 最终获取的flag为`moectf{0dd59fdb-20a2-e495-6bbf-67b8edca045d}`