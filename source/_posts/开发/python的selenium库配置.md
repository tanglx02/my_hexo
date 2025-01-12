---
title: python的selenium库配置
date: 2024-11-18 14:25:40
categories: 
- 开发
tags: 
- python
- seleium
- 开发
top: 
---
[toc]
# 一、selenium版本环境
seleium版本：`3.141.0`
pip安装命令：`pip install selenium==3.141.0`

# 二、浏览器驱动下载
Chrome驱动：
Chrome130以后：[链接](https://googlechromelabs.github.io/chrome-for-testing/#stable)
Chrome113-129以后：[链接](https://googlechromelabs.github.io/chrome-for-testing/known-good-versions-with-downloads.json)
Chrome114之前：[链接](https://chromedriver.storage.googleapis.com/index.html)
Edge:
[链接](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)

Firefox:
[链接](https://github.com/mozilla/geckodriver/releases)

Safari:
[链接](https://webkit.org/blog/6900/webdriver-support-in-safari-10/)
# 三、配置浏览器驱动
## 3.1Chrome浏览器

``` python
#导入库
import time

from selenium import webdriver
from selenium.webdriver.common.by import By
from selenium.webdriver.chrome.service import Service
from selenium.webdriver.chrome.options import Options

options = Options()

# 设置 Chrome 驱动路径
driver_path="../call/chromedriver.exe"  # 替换为 chromedriver 的实际路径
driver = webdriver.Chrome(executable_path=driver_path, options=options)
#配置driver参数(可选)
driver.maximize_window()    #窗口最大化
driver.delete_all_cookies()  # 清空cookie
# 加载 HTML
driver.get(f"http://www.baidu.com")


```