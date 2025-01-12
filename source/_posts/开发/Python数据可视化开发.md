---
title: Python数据可视化开发
date: 2024-06-14 11:29:08
categories: 
- 开发
tags: 
- 开发
- python
- 数据可视化
top: 
---
[toc]

# 一、pyecharts模块
pyecharts模块可以完成数据可视化效果图
[pyecharts官网](https://pyecharts.org)
[pyecharts官网画廊](https://gallery.pyecharts.org)，官方示例
# 二、构建折线图
构建折线图以`x轴、y轴、名称`三个要素为构建基础
x轴和y轴的数据以列表的形式存放

## 2.1、创建折线图

``` python
#导入包
from pyecharts.charts import Line
#创建一个折线图对象
line = Line()
#给折线图对象添加x轴数据
line.add_xaxis(["中国","美国","德国"])
#给折线图添加y轴数据
line.add_yaxis("GDP",[30,20,10])
#通过rander方法，将代码生成图像
line.render("名称.html")	#

```


## 2.2、配置项
### 2.2.1、全局配置选项

``` python
#导入包
from pyecharts.charts import Line
#导入配置项
from pyecharts.options import TitleOpts,LegendOpts,ToolboxOpts,VisualMapOpts

#创建一个折线图对象
line = Line()
#创建全局配置项
line.set_global_opts(
    title_opts=TitleOpts(title="GDP展示",pos_left="center",pos_bottom="1%"),  #标题展示
    legend_opts=LegendOpts(is_show=True),  #图例
    toolbox_opts=ToolboxOpts(is_show=True), #工具箱
    visualmap_opts=VisualMapOpts(is_show=False) #视觉映射
)

```

### 2.2.2、系列配置选项
``` python
#导入包
from pyecharts.charts import Line
from pyecharts.options import LabelOpts
#给折线图y轴关闭数据显示
line.add_yaxis("GDP",[30,20,10],label_opts=LabelOpts(is_show=False))

```


# 三、构建地图

## 3.1、创建地图
构建地图以`名称、数据、地图类型`三要素为构建要素
地图类型默认为`"china"`(可以不写),也可以写全国各省例如：`"云南"`(同时导入的data数据也要写为省内各市)
map数据以列表嵌套元组的形式存放`[(地区1,数值),(地区2,数值)]`

``` python
#导包
from pyecharts.charts import Map
# 创建对象
map = Map()
# 创建数据
data = [
    ("云南省",1000),
    ("上海市",900),
    ("四川省",898),
    ("广西壮族自治区",720),
    ("广东省",450),
    ("山东省",700)
]
#传入数据
map.add("测试",data,"china")	#数据名称,数据,地图类型(默认为china，也可以写省份)
#生成地图
map.render("名称.html")
```

注意事项：
- 各个省的命名规则需要规范，否则数据无法显示

``` text
"新疆维吾尔自治区", "西藏自治区", "宁夏回族自治区", "广西壮族自治区", "内蒙古自治区", "澳门特别行政区","香港特别行政区", "重庆市", "北京市", "天津市", "上海市", "甘肃省", "青海省", "四川省", "云南省","贵州省", "陕西省", "湖南省", "湖北省", "河南省", "山西省", "河北省", "辽宁省", "吉林省", "黑龙江省","山东省", "江苏省", "安徽省", "浙江省", "江西省", "福建省", "台湾省", "广东省", "海南省
```

## 3.2、配置项
### 3.2.1、全局配置项
地图颜色[RGB对照表](https://tool.oschina.net/commons?type=3)
地图颜色显示
``` python
#导入options下的VisualMapOpts,TitleOpts包
from pyecharts.options import VisualMapOpts,TitleOpts
# 设置全局选项-地图颜色
map.set_global_opts(
    title_opts=TitleOpts(title="全国疫情地图"),	#大标题
    visualmap_opts=VisualMapOpts(
        is_show=True,	#是否显示
        is_piecewise=True,	#是否分段
        pieces=[
            {"min": 1, "max": 9, "label": "1-9", "color": "#CCFFFF"},
            {"min": 10, "max": 99, "label": "10-99", "color": "#FF6666"},
            {"min": 100, "max": 500, "label": "100-500", "color": "#990033"}
        ]
    )
)
```

### 3.2.2 系列配置项

# 四、构建柱状图
## 4.1、创建柱状图
``` python
#构建基本柱状图
#导包
from pyecharts.charts import Bar
#创建一个对象
bar = Bar()
#添加x轴数据
bar.add_xaxis(["中国","美国","英国"])
#添加y轴数据
bar.add_yaxis("GDP",[30,20,10])
#绘图
bar.render("柱状图.html")
```

## 4.2、配置项
### 4.2.1、全局配置项
### 4.2.2、系列配置项

图表反转
``` python
#构建基本柱状图
#导包
from pyecharts.charts import Bar
#创建一个对象
bar = Bar()
#添加x轴数据
bar.add_xaxis(["中国","美国","英国"])
#添加y轴数据
bar.add_yaxis("GDP",[30,20,10])
#反转x和y轴
bar.reversal_axis()
#绘图
bar.render("柱状图.html")
```
