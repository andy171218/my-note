### 爬虫

```zsh
# 爬虫:将手动的自动化,一个脚本完成大量操作,获得想要的数据
模拟浏览器,发送请求,获取响应
只能获取客户端展示出来的数据
特点:知识碎片化
每个网站都是由区别的,要具体问题具体分析
模拟正常用户
爬虫:模拟客户端访问,抓取数据
反爬:保护重要数据,阻止恶意攻击
反反爬:针对反爬的策略
作用:数据采集,软件测试,抢票,网络安全,web漏洞扫描
根据爬取网站的数量:通用爬虫(搜索引擎),聚焦爬虫(数量有限,目标明确)
根据获取数据的目的:功能性爬虫(投票,抢票,短信轰炸),数据增量爬虫(获取数据用于后续分析)
客户端(渲染,显示),服务端,目标:url,参数:目标中的门,门后面就是宝藏(数据)

# 爬虫流程
1.确认目标：目标url：www.baidu.com
2.发送请求：发送网络请求，获取到特定的服务端给你的响应
3.提取数据：从响应中提取特定的数据 jsonpath/xpath/re
4.保存数据：本地（html、json、txt）、数据库
获取到的响应中，有可能会提取到还需要继续发送请求的url，可以拿着解析到的ur1继续发送请求

# robots协议(并不是一个规范,而是约定俗成的,可以修改以获取更多信息)

# 抓包(f12)

# 字符串的编码和解码
# 编码-- encode()
# 字符串转换成二进制字符串str转换成bytes
name = 'jiuge'
print(name, type(name))
name2 = name.encode()
print(name2, type(name2))

# 解码--decode（)
# 二进制字符串转换成字符串bytes 转换成str
# 图片、视频、音频，需要以bytes类型的格式去保存
a = b'abc'
print(a,type(a))
a1 = a.decode()
print(a1, type(a1))
```



### requests

```python
# 作用:发送http请求,获取响应数据

'''
requests属性:
response.text:字符串类型，是 requests 模块根据 HTTP 头部自动推测编码并解码后的结果;适用于获取文本内容，如 HTML 页面、JSON 数据等
response.content: 是字节类型，返回的是原始的二进制数据;用于处理二进制文件，如保存图片、视频等
response.encoding:指定编码格式，如将其设置为 UTF-8，能解决 response.text 可能出现的乱码问题。
获取 URL：response.url
获取请求头：response.request.headers
获取响应头：response.headers
获取 cookies：response.cookies
'''

# 例子1
import requests
# 确认目标
url='https://www.baidu.com'
# 发送请求
response = requests.get(url)
# 保存响应内容
print(response.text)
print(response.content.decode())

'''
保存html
'''

import requests

# 1. 目标URL（从浏览器Network面板复制的真实请求URL）
url = "https://tieba.baidu.com/f?kw=python&fr=index"  # Python贴吧示例

# 2. 发送GET请求，获取响应对象
response = requests.get(url)

# 3. 处理响应（解决中文乱码）并保存为HTML文件
# 方式：用content.decode("utf-8")手动指定编码，避免text属性自动推测错误
page_content = response.content.decode("utf-8")  # 解码为UTF-8格式文本

# 4. 保存到本地文件（模式"w"=文本写入，encoding="utf-8"确保中文正常）
with open("python_tieba.html", "w", encoding="utf-8") as f:
    f.write(page_content)

print("HTML页面已保存为：python_tieba.html")

'''
保存二进制(图片、音频、视频)
'''

import requests

# 1. 图片的真实URL（从浏览器"右键图片→在新标签页打开→复制地址"获取）
img_url = "https://example.com/image.jpg"  # 替换为实际图片URL

# 2. 发送GET请求，获取图片二进制响应
response = requests.get(img_url)

# 3. 保存二进制数据（模式"wb"=二进制写入，无需encoding参数）
with open("saved_image.jpg", "wb") as f:
    f.write(response.content)  # 直接写入二进制内容

print("图片已保存为：saved_image.jpg")

'''
保存json
'''

import requests
import json  # 用于处理JSON格式

# 1. JSON接口URL（示例：获取某API的JSON数据）
json_url = "https://api.example.com/data"  # 替换为实际JSON接口URL

# 2. 发送请求并解析JSON
response = requests.get(json_url)
json_data = response.json()  # 直接解析为Python字典/列表

# 3. 保存为JSON文件（ensure_ascii=False保留中文，indent=2格式化显示）
with open("api_data.json", "w", encoding="utf-8") as f:
    json.dump(json_data, f, ensure_ascii=False, indent=2)

print("JSON数据已保存为：api_data.json")
```



### 用户代理

```python
# 模拟正常用户
# User-Agent 作用：向服务器传递客户端（操作系统 + 浏览器）信息，让服务器认为请求来自 “真实浏览器” 而非爬虫
# 必要性：多数网站会拦截无 User-Agent 的请求，仅返回不完整数据，添加后可获取与浏览器一致的完整响应
# 通用建议：后续爬取任何网站，均需在请求中携带 User-Agent（可构建多个 User-Agent 组成 “UA 池”，避免单一 UA 被封禁）

# 例子
import requests

# 1. 目标URL（百度首页）
url = "https://www.baidu.com"

# 2. 构建请求头：字典格式，包含User-Agent字段（值替换为自己浏览器的User-Agent）
headers = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"
}

# 3. 发送GET请求：通过headers参数携带请求头
response = requests.get(url, headers=headers)

# 4. 解码响应内容（指定utf-8避免乱码）
response_content = response.content.decode("utf-8")

# 5. 验证结果：代码长度大幅增加（301402），内容完整
print("带User-Agent的代码长度：", len(response_content))
# 打印部分内容（可见“百度一下，你就知道”等完整内容）
print("带User-Agent的部分内容：", response_content[:1000])

# 额外：打印请求头，确认User-Agent已携带
print("实际发送的请求头：", response.request.headers["User-Agent"])


# user-agent池
为了防止反爬,而模拟多个设备发送请求

# 例子
# 1. 手动构建 user-agent 列表（即 user-agent 池）
ua_list = [
    "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/128.0.0.0 Safari/537.36",
    "Mozilla/5.0 (iPhone; CPU iPhone OS 16_6 like Mac OS X) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/16.6 Mobile/15E148 Safari/604.1",
    "Mozilla/5.0 (X11; Linux x86_64; rv:129.0) Gecko/20100101 Firefox/129.0"
]
# 2. 随机选取一个 user-agent
import random
random_ua = random.choice(ua_list)
# 3. 构造请求头并发送请求
headers = {"User-Agent": random_ua}
import requests
response = requests.get("目标网站URL", headers=headers)

# fake-useragent模块
# 1. 安装并导入 fake-useragent 模块（需先执行 pip install fake-useragent）
from fake_useragent import UserAgent
# 2. 初始化对象（自动构建 user-agent 池并随机获取）
ua = UserAgent()
random_ua = ua.random  # 随机生成一个 user-agent
# 3. 构造请求头发送请求
headers = {"User-Agent": random_ua}
import requests
response = requests.get("目标网站URL", headers=headers)
```



### url传参

```python
# url?key1=value1&key2=value2

# 编码需求
中文、特殊符号（如 “?”“=”）会导致服务器解析错误，需通过 URL 编码将明文转为 “% XX” 格式密文，解码则反向转换

# Python 实现
通过urllib.parse模块的quote()（明文转密文）和unquote()（密文转明文）实现编解码

# 例子
# 导入URL编解码模块
from urllib.parse import quote, unquote

# 1. 模拟百度搜索关键词编码（明文转密文）
# 视频中搜索关键词“学习”（明文），URL传参时需编码
plain_text = "学习"  # 明文字符串（视频中百度搜索的关键词）
encoded_text = quote(plain_text)  # 调用quote()编码，模拟URL自动编码
print("编码后（URL中实际传递的参数）：", encoded_text)  
# 输出：%E5%AD%A6%E4%B9%A0（与视频中抓包看到的密文一致）

# 2. 模拟服务器接收参数后解码（密文转明文）
# 视频中服务器收到编码后的参数，需解码才能识别
decoded_text = unquote(encoded_text)  # 调用unquote()解码
print("解码后（服务器识别的关键词）：", decoded_text)  
# 输出：学习（还原为视频中的搜索关键词明文）

'''
url传参的两种方式
'''

# params
# 1. 安装并导入requests（视频强调：第三方库需先执行 pip install requests）
import requests

# 2. 视频核心：定义基础URL（不含参数，仅保留百度搜索的核心路径）
base_url = "https://www.baidu.com/s"

# 3. 视频步骤：构建参数字典（键=URL参数名，值=参数内容，清晰易改）
param_dict = {
    "wd": "Python网络爬虫",  # 百度搜索核心参数：wd=搜索关键词（视频重点标注）
    "rn": 20                 # 扩展参数：rn=每页显示20条结果（默认10条，视频示例）
}

# 4. 视频关键：发送请求时用params传递字典（requests自动拼接URL）
# 拼接后实际URL：https://www.baidu.com/s?wd=Python网络爬虫&rn=20
response = requests.get(
    url=base_url,
    params=param_dict,
    headers={"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"}  # 视频强调：加请求头模拟浏览器，避免反爬
)

# 5. 视频乱码解决：用content.decode()指定编码（避免text自动识别偏差）
response_content = response.content.decode("utf-8")

# 6. 验证结果（视频步骤：打印前600字符，确认获取到搜索页面）
print("百度搜索'Python网络爬虫'响应片段（params方式）：")
print(response_content[:600])


# 格式化拼接
import requests

# 1. 视频场景：定义参数变量（可替换为input()用户输入，视频演示交互场景）
search_keyword = "考研经验"  # 搜索关键词
page = 3                     # 分页参数：第3页（视频提及贴吧分页用page参数）

# 2. 视频步骤：格式化拼接URL（手动嵌入参数，注意?和&的位置）
# 拼接后实际URL：https://tieba.baidu.com/f?kw=考研经验&page=3
target_url = f"https://tieba.baidu.com/f?kw={search_keyword}&page={page}"

# 3. 发送请求（视频同前：加请求头模拟浏览器）
response = requests.get(
    url=target_url,
    headers={"User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36"}
)

# 4. 处理响应（视频推荐的decode方式）
response_content = response.content.decode("utf-8")

# 5. 验证结果（视频步骤：确认获取到贴吧第3页内容）
print(f"\n贴吧搜索'{search_keyword}'第{page}页响应片段（URL格式化方式）：")
print(response_content[:600])
```



### 示例

```python
import requests
from urllib.parse import urlparse
import os

def get_headers():
    """
    构造请求头：模拟浏览器访问，避免被服务器识别为爬虫
    （建议替换为自己浏览器的User-Agent，可通过F12→Network→任意请求→Headers→User-Agent获取）
    """
    return {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/124.0.0.0 Safari/537.36",
        "Referer": "https://music.163.com/",  # 网易云音乐Referer，必须携带（否则403禁止访问）
        "Accept": "text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8"
    }

def save_binary_resource(resource_url, save_dir, file_name):
    """
    通用二进制资源保存函数：图片、歌曲、MV均为二进制数据，统一用此函数保存
    :param resource_url: 资源真实URL（需通过浏览器抓包获取）
    :param save_dir: 保存目录（如"网易云资源/图片"）
    :param file_name: 保存文件名（需带后缀，如"封面.jpg"、"歌曲.mp3"、"MV.mp4"）
    :return: 保存成功返回True，失败返回False
    """
    # 创建保存目录（不存在则自动创建）
    if not os.path.exists(save_dir):
        os.makedirs(save_dir)
    
    # 拼接完整保存路径
    save_path = os.path.join(save_dir, file_name)
    
    try:
        # 发送GET请求获取二进制数据（stream=True适合大文件如MV，避免内存占用过高）
        response = requests.get(
            url=resource_url,
            headers=get_headers(),
            stream=True,
            timeout=15  # 超时时间（防止请求卡死）
        )
        
        # 验证请求是否成功（状态码200为成功）
        if response.status_code == 200:
            # 以二进制模式写入文件
            with open(save_path, "wb") as f:
                # 分块写入（针对大文件如MV，减少内存压力）
                for chunk in response.iter_content(chunk_size=1024 * 1024):  # 1MB/块
                    if chunk:
                        f.write(chunk)
            print(f"✅ {file_name} 保存成功！路径：{save_path}")
            return True
        else:
            print(f"❌ {file_name} 请求失败！状态码：{response.status_code}")
            return False
    
    except Exception as e:
        print(f"❌ {file_name} 保存失败！错误信息：{str(e)}")
        return False

def crawl_netease_music_resource():
    """
    网易云音乐资源爬取主函数：需先通过浏览器抓包获取3类资源的真实URL
    抓包步骤：
    1. 打开网易云音乐目标页面（图片/歌曲/MV）
    2. F12打开开发者工具→Network→刷新页面
    3. 图片：筛选"Img"分类，找到图片URL（后缀为.jpg/.png）
    4. 歌曲：筛选"Media"分类，找到音频URL（后缀为.mp3）
    5. MV：筛选"Media"分类，找到视频URL（后缀为.mp4）
    """
    # -------------------------- 1. 爬取单张图片（如歌曲封面） --------------------------
    # 替换为抓包获取的图片真实URL（示例为某歌曲封面，实际需自行抓包）
    img_url = "https://p1.music.126.net/xxxxxx/yyyyy.jpg"  # 需替换！
    save_binary_resource(
        resource_url=img_url,
        save_dir="网易云资源/图片",
        file_name="歌曲封面.jpg"  # 自定义文件名（需带.jpg/.png后缀）
    )

    # -------------------------- 2. 爬取单首歌曲（音频） --------------------------
    # 替换为抓包获取的歌曲真实URL（示例为某歌曲音频，实际需自行抓包）
    song_url = "https://m701.music.126.net/xxxxxx/yyyyy.mp3"  # 需替换！
    save_binary_resource(
        resource_url=song_url,
        save_dir="网易云资源/歌曲",
        file_name="这世界那么多人.mp3"  # 自定义文件名（需带.mp3后缀）
    )

    # -------------------------- 3. 爬取单个MV（视频） --------------------------
    # 替换为抓包获取的MV真实URL（示例为某MV视频，实际需自行抓包）
    mv_url = "https://v12.music.126.net/xxxxxx/yyyyy.mp4"  # 需替换！
    save_binary_resource(
        resource_url=mv_url,
        save_dir="网易云资源/MV",
        file_name="这世界那么多人-MV.mp4"  # 自定义文件名（需带.mp4后缀）
    )

# 执行爬取（需先替换上述3个URL为实际抓包结果）
if __name__ == "__main__":
    crawl_netease_music_resource()
```

