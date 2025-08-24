# 第四章 金曦破禁与七绝傀儡阵
1. 打开网页挑战第一关，发现要求使用GET方法传递参数 key=xdsec，传输完成后获得玉简碎片`bW9lY3Rme0Mw`
2. 进入第二关，发现要求使用POST方法请求数据：declaration=织云阁=第一，编写python代码，并返回网页html代码
    ```py
    import requests

    url = "http://127.0.0.1:59411/cloud_weaver"

    data = {
        "declaration": "织云阁=第一"
    }

    try:
        response = requests.post(url, data=data)
        
        print("响应状态码：", response.status_code)
        print("响应内容：", response.text)
    except Exception as e:
        print("请求发生错误：", str(e))
    ```
    获得获得玉简碎片: bjZyNDd1MTQ3，并得到了第三关的url在`/shadow_stalker`处
3. 进入第三关，发现要求从本地访问这个页面