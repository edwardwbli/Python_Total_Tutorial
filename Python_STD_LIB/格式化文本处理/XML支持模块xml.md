
# XML支持模块(xml)

**什么是xml？**

xml即可扩展标记语言，它可以用来标记数据、定义数据类型，是一种允许用户对自己的标记语言进行定义的源语言,简单说它是html的爹。大约长这个样子:

    <?xml version="1.0" encoding="utf-8"?>
    <catalog>
        <maxid>4</maxid>
        <login username="pytest" passwd='123456'>
            <caption>Python</caption>
            <item id="4">
                <caption>测试</caption>
            </item>
        </login>
        <item id="2">
            <caption>Zope</caption>
        </item>
    </catalog>


它有如下特征：

+ 它是有标签对组成，
        
        <aa></aa>
 
+ 标签可以有属性：
        
        <aa id=’123’></aa>

+ 标签对可以嵌入数据：
        
        <aa>abc</aa>

+ 标签可以嵌入子标签（具有层级关系）：

        <aa>

             <bb></bb>

        </aa>

和html特点上是差不多的.
 


对于xml的支持,python提供4种解析方式:DOM,SAX和ElementTree,具体特点归纳如下:


方法|对应模块|实现方式|特点
---|---|---|---
DOM|xml.dom|`W3C DOM API`的实现.将XML数据在内存中解析成一个树，通过对树的操作来操作XML。|高内存占用,但解析成树便于分析
SAX|xml.sax|`SAX API`的实现.用事件驱动模型，通过在解析XML的过程中触发一个个的事件并调用用户定义的回调函数来处理XML文件。|低内存占用,局部加载,API不友好
ElementTree|xml.etree.ElementTree|一个轻量级的DOM，具有方便友好的API。代码可用性好，速度快，消耗内存少|比DOM快,API友好,性能和SAX差不多,也支持文档局部加载


顺道一提,因为html是xml的子集所以理论上也可以当xml一样解析

我们拿来做样板的是w3school上的一个例子[下载](http://www.w3school.com.cn/example/xmle/plant_catalog.xml)


```python
from __future__ import print_function
```


```python
with open("source/plant_catalog.xml") as f:
    f_str=f.read()
    print(f_str)
```

    <?xml version="1.0" encoding="ISO-8859-1"?>
    <!-- Edited with XML Spy v2007 (http://www.altova.com) -->
    <CATALOG>
    	<PLANT>
    		<COMMON>Bloodroot</COMMON>
    		<BOTANICAL>Sanguinaria canadensis</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$2.44</PRICE>
    		<AVAILABILITY>031599</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Columbine</COMMON>
    		<BOTANICAL>Aquilegia canadensis</BOTANICAL>
    		<ZONE>3</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$9.37</PRICE>
    		<AVAILABILITY>030699</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Marsh Marigold</COMMON>
    		<BOTANICAL>Caltha palustris</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Mostly Sunny</LIGHT>
    		<PRICE>$6.81</PRICE>
    		<AVAILABILITY>051799</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Cowslip</COMMON>
    		<BOTANICAL>Caltha palustris</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$9.90</PRICE>
    		<AVAILABILITY>030699</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Dutchman's-Breeches</COMMON>
    		<BOTANICAL>Dicentra cucullaria</BOTANICAL>
    		<ZONE>3</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$6.44</PRICE>
    		<AVAILABILITY>012099</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Ginger, Wild</COMMON>
    		<BOTANICAL>Asarum canadense</BOTANICAL>
    		<ZONE>3</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$9.03</PRICE>
    		<AVAILABILITY>041899</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Hepatica</COMMON>
    		<BOTANICAL>Hepatica americana</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$4.45</PRICE>
    		<AVAILABILITY>012699</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Liverleaf</COMMON>
    		<BOTANICAL>Hepatica americana</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$3.99</PRICE>
    		<AVAILABILITY>010299</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Jack-In-The-Pulpit</COMMON>
    		<BOTANICAL>Arisaema triphyllum</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$3.23</PRICE>
    		<AVAILABILITY>020199</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Mayapple</COMMON>
    		<BOTANICAL>Podophyllum peltatum</BOTANICAL>
    		<ZONE>3</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$2.98</PRICE>
    		<AVAILABILITY>060599</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Phlox, Woodland</COMMON>
    		<BOTANICAL>Phlox divaricata</BOTANICAL>
    		<ZONE>3</ZONE>
    		<LIGHT>Sun or Shade</LIGHT>
    		<PRICE>$2.80</PRICE>
    		<AVAILABILITY>012299</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Phlox, Blue</COMMON>
    		<BOTANICAL>Phlox divaricata</BOTANICAL>
    		<ZONE>3</ZONE>
    		<LIGHT>Sun or Shade</LIGHT>
    		<PRICE>$5.59</PRICE>
    		<AVAILABILITY>021699</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Spring-Beauty</COMMON>
    		<BOTANICAL>Claytonia Virginica</BOTANICAL>
    		<ZONE>7</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$6.59</PRICE>
    		<AVAILABILITY>020199</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Trillium</COMMON>
    		<BOTANICAL>Trillium grandiflorum</BOTANICAL>
    		<ZONE>5</ZONE>
    		<LIGHT>Sun or Shade</LIGHT>
    		<PRICE>$3.90</PRICE>
    		<AVAILABILITY>042999</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Wake Robin</COMMON>
    		<BOTANICAL>Trillium grandiflorum</BOTANICAL>
    		<ZONE>5</ZONE>
    		<LIGHT>Sun or Shade</LIGHT>
    		<PRICE>$3.20</PRICE>
    		<AVAILABILITY>022199</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Violet, Dog-Tooth</COMMON>
    		<BOTANICAL>Erythronium americanum</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$9.04</PRICE>
    		<AVAILABILITY>020199</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Trout Lily</COMMON>
    		<BOTANICAL>Erythronium americanum</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$6.94</PRICE>
    		<AVAILABILITY>032499</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Adder's-Tongue</COMMON>
    		<BOTANICAL>Erythronium americanum</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$9.58</PRICE>
    		<AVAILABILITY>041399</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Anemone</COMMON>
    		<BOTANICAL>Anemone blanda</BOTANICAL>
    		<ZONE>6</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$8.86</PRICE>
    		<AVAILABILITY>122698</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Grecian Windflower</COMMON>
    		<BOTANICAL>Anemone blanda</BOTANICAL>
    		<ZONE>6</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$9.16</PRICE>
    		<AVAILABILITY>071099</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Bee Balm</COMMON>
    		<BOTANICAL>Monarda didyma</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$4.59</PRICE>
    		<AVAILABILITY>050399</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Bergamot</COMMON>
    		<BOTANICAL>Monarda didyma</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$7.16</PRICE>
    		<AVAILABILITY>042799</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Black-Eyed Susan</COMMON>
    		<BOTANICAL>Rudbeckia hirta</BOTANICAL>
    		<ZONE>Annual</ZONE>
    		<LIGHT>Sunny</LIGHT>
    		<PRICE>$9.80</PRICE>
    		<AVAILABILITY>061899</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Buttercup</COMMON>
    		<BOTANICAL>Ranunculus</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$2.57</PRICE>
    		<AVAILABILITY>061099</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Crowfoot</COMMON>
    		<BOTANICAL>Ranunculus</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$9.34</PRICE>
    		<AVAILABILITY>040399</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Butterfly Weed</COMMON>
    		<BOTANICAL>Asclepias tuberosa</BOTANICAL>
    		<ZONE>Annual</ZONE>
    		<LIGHT>Sunny</LIGHT>
    		<PRICE>$2.78</PRICE>
    		<AVAILABILITY>063099</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Cinquefoil</COMMON>
    		<BOTANICAL>Potentilla</BOTANICAL>
    		<ZONE>Annual</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$7.06</PRICE>
    		<AVAILABILITY>052599</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Primrose</COMMON>
    		<BOTANICAL>Oenothera</BOTANICAL>
    		<ZONE>3 - 5</ZONE>
    		<LIGHT>Sunny</LIGHT>
    		<PRICE>$6.56</PRICE>
    		<AVAILABILITY>013099</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Gentian</COMMON>
    		<BOTANICAL>Gentiana</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Sun or Shade</LIGHT>
    		<PRICE>$7.81</PRICE>
    		<AVAILABILITY>051899</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Blue Gentian</COMMON>
    		<BOTANICAL>Gentiana</BOTANICAL>
    		<ZONE>4</ZONE>
    		<LIGHT>Sun or Shade</LIGHT>
    		<PRICE>$8.56</PRICE>
    		<AVAILABILITY>050299</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Jacob's Ladder</COMMON>
    		<BOTANICAL>Polemonium caeruleum</BOTANICAL>
    		<ZONE>Annual</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$9.26</PRICE>
    		<AVAILABILITY>022199</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Greek Valerian</COMMON>
    		<BOTANICAL>Polemonium caeruleum</BOTANICAL>
    		<ZONE>Annual</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$4.36</PRICE>
    		<AVAILABILITY>071499</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>California Poppy</COMMON>
    		<BOTANICAL>Eschscholzia californica</BOTANICAL>
    		<ZONE>Annual</ZONE>
    		<LIGHT>Sun</LIGHT>
    		<PRICE>$7.89</PRICE>
    		<AVAILABILITY>032799</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Shooting Star</COMMON>
    		<BOTANICAL>Dodecatheon</BOTANICAL>
    		<ZONE>Annual</ZONE>
    		<LIGHT>Mostly Shady</LIGHT>
    		<PRICE>$8.60</PRICE>
    		<AVAILABILITY>051399</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Snakeroot</COMMON>
    		<BOTANICAL>Cimicifuga</BOTANICAL>
    		<ZONE>Annual</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$5.63</PRICE>
    		<AVAILABILITY>071199</AVAILABILITY>
    	</PLANT>
    	<PLANT>
    		<COMMON>Cardinal Flower</COMMON>
    		<BOTANICAL>Lobelia cardinalis</BOTANICAL>
    		<ZONE>2</ZONE>
    		<LIGHT>Shade</LIGHT>
    		<PRICE>$3.02</PRICE>
    		<AVAILABILITY>022299</AVAILABILITY>
    	</PLANT>
    </CATALOG>
    


## DOM方法:

在`xml.dom`模块中我们一般用`xml.dom.minidom`子模块来解析xml


```python
import xml.dom.minidom
```


```python
dom = xml.dom.minidom.parse("source/plant_catalog.xml")#解析xml文件,返回一个dom对象
```


```python
root=dom.documentElement#返回xml生成树的根
```


```python
root.nodeName#节点名
```




    'CATALOG'




```python
root.nodeValue#节点值
```


```python
root.nodeType#节点类型
```




    1




```python
root.hasAttributes()   # 判断标签是否有属性
```




    False



NodeTypes - 有名常数:

NodeType|	Named Constant
---|---
1|	ELEMENT_NODE
2|	ATTRIBUTE_NODE
3|	TEXT_NODE
4|	CDATA_SECTION_NODE
5|	ENTITY_REFERENCE_NODE
6	|ENTITY_NODE
7|	PROCESSING_INSTRUCTION_NODE
8|	COMMENT_NODE
9|	DOCUMENT_NODE
10|	DOCUMENT_TYPE_NODE
11|	DOCUMENT_FRAGMENT_NODE
12|	NOTATION_NODE



```python
commoneles=root.getElementsByTagName('COMMON')#获取已知标签名的元素(按顺序返回元素)
```


```python
#item = commoneles[0].getAttribute("id") #获得标签属性值
```


```python
commonele0 = commoneles[0]
```


```python
commonele0.firstChild.data#获取到第一个子节点的值
```




    'Bloodroot'



>我们来打印出所有植物和他的对应价格


```python
dom = xml.dom.minidom.parse("source/plant_catalog.xml")#解析xml文件,返回一个dom对象
root=dom.documentElement#返回xml生成树的根
plantes = root.getElementsByTagName('PLANT')
result = map(lambda x:(x.getElementsByTagName('COMMON')[0].firstChild.data,
              x.getElementsByTagName('PRICE')[0].firstChild.data),plantes)
for i in result:
    print(i[0],":",i[1])
```

    Bloodroot : $2.44
    Columbine : $9.37
    Marsh Marigold : $6.81
    Cowslip : $9.90
    Dutchman's-Breeches : $6.44
    Ginger, Wild : $9.03
    Hepatica : $4.45
    Liverleaf : $3.99
    Jack-In-The-Pulpit : $3.23
    Mayapple : $2.98
    Phlox, Woodland : $2.80
    Phlox, Blue : $5.59
    Spring-Beauty : $6.59
    Trillium : $3.90
    Wake Robin : $3.20
    Violet, Dog-Tooth : $9.04
    Trout Lily : $6.94
    Adder's-Tongue : $9.58
    Anemone : $8.86
    Grecian Windflower : $9.16
    Bee Balm : $4.59
    Bergamot : $7.16
    Black-Eyed Susan : $9.80
    Buttercup : $2.57
    Crowfoot : $9.34
    Butterfly Weed : $2.78
    Cinquefoil : $7.06
    Primrose : $6.56
    Gentian : $7.81
    Blue Gentian : $8.56
    Jacob's Ladder : $9.26
    Greek Valerian : $4.36
    California Poppy : $7.89
    Shooting Star : $8.60
    Snakeroot : $5.63
    Cardinal Flower : $3.02


## SAX方法

SAX方法是事件驱动的,所以第一个就是继承回调类并重载回调函数,这和`html.parser`类似

ContentHandler类常用方法介绍:

+ characters(content)方法

    调用时机：
    从行开始，遇到标签之前，存在字符，content的值为这些字符串。
    从一个标签，遇到下一个标签之前， 存在字符，content的值为这些字符串。
    从一个标签，遇到行结束符之前，存在字符，content的值为这些字符串。
    标签可以是开始标签，也可以是结束标签。
  
  
+ startDocument()方法

    文档启动的时候调用。
    
    
+ endDocument()方法

    解析器到达文档结尾时调用。
    
    
+ startElement(name, attrs)方法

    遇到XML开始标签时调用，name是标签的名字，attrs是标签的属性值字典。
    
    
+ endElement(name)方法

    遇到XML结束标签时调用。

+ startElementNS(name, qname, attrs)方法

    遇到XML命名空间开始时调用
    
+ endElementNS(name, qname)方法
    
    遇到XML命名空间结束时调用
    
    
之后只要创建解析器对象就可以像解析html一样解析xml了

>我们来打印出所有植物和他的对应价格


```python
import xml.sax.handler

class PlanteHandler(xml.sax.handler.ContentHandler):
    def __init__(self):
        self.CurrentData = ""
        self.type = ""
        self.format = ""
        self.year = ""
        self.rating = ""
        self.stars = ""
        self.description = ""
        
    # 元素开始事件处理
    def startElement(self, tag, attributes):
        self.CurrentData = tag
        chidren = {
            "PlANTE":lambda :print("*****PlANTE*****"),
            "COMMON":lambda :print("name:",end=''),
            "PRICE":lambda :print("price:",end='')
        }
        chidren.get(self.CurrentData,lambda : None)()
    
    # 元素结束事件处理
    def endElement(self, tag):
        self.CurrentData = ""

    # 内容事件处理
    def characters(self, content):
        chidren = {
            "COMMON":lambda:print(content),
            "PRICE":lambda:print(content)
        }
        chidren.get(self.CurrentData,lambda :None)()
        
    
```


```python
parser = xml.sax.make_parser()#创建解析器对象
Handler = PlanteHandler()#创建回调对象
parser.setContentHandler(Handler)#设置回调对象到解析器对象
parser.parse("source/plant_catalog.xml")
```

    name:Bloodroot
    price:$2.44
    name:Columbine
    price:$9.37
    name:Marsh Marigold
    price:$6.81
    name:Cowslip
    price:$9.90
    name:Dutchman's-Breeches
    price:$6.44
    name:Ginger, Wild
    price:$9.03
    name:Hepatica
    price:$4.45
    name:Liverleaf
    price:$3.99
    name:Jack-In-The-Pulpit
    price:$3.23
    name:Mayapple
    price:$2.98
    name:Phlox, Woodland
    price:$2.80
    name:Phlox, Blue
    price:$5.59
    name:Spring-Beauty
    price:$6.59
    name:Trillium
    price:$3.90
    name:Wake Robin
    price:$3.20
    name:Violet, Dog-Tooth
    price:$9.04
    name:Trout Lily
    price:$6.94
    name:Adder's-Tongue
    price:$9.58
    name:Anemone
    price:$8.86
    name:Grecian Windflower
    price:$9.16
    name:Bee Balm
    price:$4.59
    name:Bergamot
    price:$7.16
    name:Black-Eyed Susan
    price:$9.80
    name:Buttercup
    price:$2.57
    name:Crowfoot
    price:$9.34
    name:Butterfly Weed
    price:$2.78
    name:Cinquefoil
    price:$7.06
    name:Primrose
    price:$6.56
    name:Gentian
    price:$7.81
    name:Blue Gentian
    price:$8.56
    name:Jacob's Ladder
    price:$9.26
    name:Greek Valerian
    price:$4.36
    name:California Poppy
    price:$7.89
    name:Shooting Star
    price:$8.60
    name:Snakeroot
    price:$5.63
    name:Cardinal Flower
    price:$3.02


## ElementTree方法

从总结上来看可以说ElementTree方法是最好的方法,Dom处理大文本的时候会相当吃内存,而SAX无法全面解析文档结构.ElementTree怎两者兼而有之,加上友好的api.这也是我最推荐的方法.


```python
import xml.etree.ElementTree as ET
```

### 将 XML 解析为树的形式

XML 是一种分级的数据形式，所以最自然的表示方法是将它表示为一棵树。ET 有两个对象来实现这个目的

+ ElementTree 

    将整个 XML 解析为一棵树
    
    
+ Element 将单个结点解析为树。


如果是整个文档级别的操作(比如说读，写，找到一些有趣的元素)通常用 ElementTree 。单个 XML 元素和它的子元素通常用 Element 。

> 解析整个文档


```python
tree = ET.ElementTree(file='source/plant_catalog.xml')#将文档解析为树
"""
ET.parse('source/plant_catalog.xml')也是一样

也可以先读成str然后用

ET.fromstring(country_data_as_string)

来读取
"""
```




    "\nET.parse('source/plant_catalog.xml')也是一样\n\n也可以先读成str然后用\n\nET.fromstring(country_data_as_string)\n\n来读取\n"




```python
root = tree.getroot()#获取根节点
```


```python
root.tag, root.attrib#标签和属性
```




    ('CATALOG', {})




```python
#查看子节点
for child in root:
    print(child.tag, child.attrib)
```

    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}
    PLANT {}



```python
root[0].tag, root[0].attrib#进入一个子节点查看
```




    ('PLANT', {})



>找元素


```python
#以一个节点为根深度优先遍历
for elem in tree.iter():
    print(elem.tag, elem.attrib,elem.text)
```

    CATALOG {} 
    	
    PLANT {} 
    		
    COMMON {} Bloodroot
    BOTANICAL {} Sanguinaria canadensis
    ZONE {} 4
    LIGHT {} Mostly Shady
    PRICE {} $2.44
    AVAILABILITY {} 031599
    PLANT {} 
    		
    COMMON {} Columbine
    BOTANICAL {} Aquilegia canadensis
    ZONE {} 3
    LIGHT {} Mostly Shady
    PRICE {} $9.37
    AVAILABILITY {} 030699
    PLANT {} 
    		
    COMMON {} Marsh Marigold
    BOTANICAL {} Caltha palustris
    ZONE {} 4
    LIGHT {} Mostly Sunny
    PRICE {} $6.81
    AVAILABILITY {} 051799
    PLANT {} 
    		
    COMMON {} Cowslip
    BOTANICAL {} Caltha palustris
    ZONE {} 4
    LIGHT {} Mostly Shady
    PRICE {} $9.90
    AVAILABILITY {} 030699
    PLANT {} 
    		
    COMMON {} Dutchman's-Breeches
    BOTANICAL {} Dicentra cucullaria
    ZONE {} 3
    LIGHT {} Mostly Shady
    PRICE {} $6.44
    AVAILABILITY {} 012099
    PLANT {} 
    		
    COMMON {} Ginger, Wild
    BOTANICAL {} Asarum canadense
    ZONE {} 3
    LIGHT {} Mostly Shady
    PRICE {} $9.03
    AVAILABILITY {} 041899
    PLANT {} 
    		
    COMMON {} Hepatica
    BOTANICAL {} Hepatica americana
    ZONE {} 4
    LIGHT {} Mostly Shady
    PRICE {} $4.45
    AVAILABILITY {} 012699
    PLANT {} 
    		
    COMMON {} Liverleaf
    BOTANICAL {} Hepatica americana
    ZONE {} 4
    LIGHT {} Mostly Shady
    PRICE {} $3.99
    AVAILABILITY {} 010299
    PLANT {} 
    		
    COMMON {} Jack-In-The-Pulpit
    BOTANICAL {} Arisaema triphyllum
    ZONE {} 4
    LIGHT {} Mostly Shady
    PRICE {} $3.23
    AVAILABILITY {} 020199
    PLANT {} 
    		
    COMMON {} Mayapple
    BOTANICAL {} Podophyllum peltatum
    ZONE {} 3
    LIGHT {} Mostly Shady
    PRICE {} $2.98
    AVAILABILITY {} 060599
    PLANT {} 
    		
    COMMON {} Phlox, Woodland
    BOTANICAL {} Phlox divaricata
    ZONE {} 3
    LIGHT {} Sun or Shade
    PRICE {} $2.80
    AVAILABILITY {} 012299
    PLANT {} 
    		
    COMMON {} Phlox, Blue
    BOTANICAL {} Phlox divaricata
    ZONE {} 3
    LIGHT {} Sun or Shade
    PRICE {} $5.59
    AVAILABILITY {} 021699
    PLANT {} 
    		
    COMMON {} Spring-Beauty
    BOTANICAL {} Claytonia Virginica
    ZONE {} 7
    LIGHT {} Mostly Shady
    PRICE {} $6.59
    AVAILABILITY {} 020199
    PLANT {} 
    		
    COMMON {} Trillium
    BOTANICAL {} Trillium grandiflorum
    ZONE {} 5
    LIGHT {} Sun or Shade
    PRICE {} $3.90
    AVAILABILITY {} 042999
    PLANT {} 
    		
    COMMON {} Wake Robin
    BOTANICAL {} Trillium grandiflorum
    ZONE {} 5
    LIGHT {} Sun or Shade
    PRICE {} $3.20
    AVAILABILITY {} 022199
    PLANT {} 
    		
    COMMON {} Violet, Dog-Tooth
    BOTANICAL {} Erythronium americanum
    ZONE {} 4
    LIGHT {} Shade
    PRICE {} $9.04
    AVAILABILITY {} 020199
    PLANT {} 
    		
    COMMON {} Trout Lily
    BOTANICAL {} Erythronium americanum
    ZONE {} 4
    LIGHT {} Shade
    PRICE {} $6.94
    AVAILABILITY {} 032499
    PLANT {} 
    		
    COMMON {} Adder's-Tongue
    BOTANICAL {} Erythronium americanum
    ZONE {} 4
    LIGHT {} Shade
    PRICE {} $9.58
    AVAILABILITY {} 041399
    PLANT {} 
    		
    COMMON {} Anemone
    BOTANICAL {} Anemone blanda
    ZONE {} 6
    LIGHT {} Mostly Shady
    PRICE {} $8.86
    AVAILABILITY {} 122698
    PLANT {} 
    		
    COMMON {} Grecian Windflower
    BOTANICAL {} Anemone blanda
    ZONE {} 6
    LIGHT {} Mostly Shady
    PRICE {} $9.16
    AVAILABILITY {} 071099
    PLANT {} 
    		
    COMMON {} Bee Balm
    BOTANICAL {} Monarda didyma
    ZONE {} 4
    LIGHT {} Shade
    PRICE {} $4.59
    AVAILABILITY {} 050399
    PLANT {} 
    		
    COMMON {} Bergamot
    BOTANICAL {} Monarda didyma
    ZONE {} 4
    LIGHT {} Shade
    PRICE {} $7.16
    AVAILABILITY {} 042799
    PLANT {} 
    		
    COMMON {} Black-Eyed Susan
    BOTANICAL {} Rudbeckia hirta
    ZONE {} Annual
    LIGHT {} Sunny
    PRICE {} $9.80
    AVAILABILITY {} 061899
    PLANT {} 
    		
    COMMON {} Buttercup
    BOTANICAL {} Ranunculus
    ZONE {} 4
    LIGHT {} Shade
    PRICE {} $2.57
    AVAILABILITY {} 061099
    PLANT {} 
    		
    COMMON {} Crowfoot
    BOTANICAL {} Ranunculus
    ZONE {} 4
    LIGHT {} Shade
    PRICE {} $9.34
    AVAILABILITY {} 040399
    PLANT {} 
    		
    COMMON {} Butterfly Weed
    BOTANICAL {} Asclepias tuberosa
    ZONE {} Annual
    LIGHT {} Sunny
    PRICE {} $2.78
    AVAILABILITY {} 063099
    PLANT {} 
    		
    COMMON {} Cinquefoil
    BOTANICAL {} Potentilla
    ZONE {} Annual
    LIGHT {} Shade
    PRICE {} $7.06
    AVAILABILITY {} 052599
    PLANT {} 
    		
    COMMON {} Primrose
    BOTANICAL {} Oenothera
    ZONE {} 3 - 5
    LIGHT {} Sunny
    PRICE {} $6.56
    AVAILABILITY {} 013099
    PLANT {} 
    		
    COMMON {} Gentian
    BOTANICAL {} Gentiana
    ZONE {} 4
    LIGHT {} Sun or Shade
    PRICE {} $7.81
    AVAILABILITY {} 051899
    PLANT {} 
    		
    COMMON {} Blue Gentian
    BOTANICAL {} Gentiana
    ZONE {} 4
    LIGHT {} Sun or Shade
    PRICE {} $8.56
    AVAILABILITY {} 050299
    PLANT {} 
    		
    COMMON {} Jacob's Ladder
    BOTANICAL {} Polemonium caeruleum
    ZONE {} Annual
    LIGHT {} Shade
    PRICE {} $9.26
    AVAILABILITY {} 022199
    PLANT {} 
    		
    COMMON {} Greek Valerian
    BOTANICAL {} Polemonium caeruleum
    ZONE {} Annual
    LIGHT {} Shade
    PRICE {} $4.36
    AVAILABILITY {} 071499
    PLANT {} 
    		
    COMMON {} California Poppy
    BOTANICAL {} Eschscholzia californica
    ZONE {} Annual
    LIGHT {} Sun
    PRICE {} $7.89
    AVAILABILITY {} 032799
    PLANT {} 
    		
    COMMON {} Shooting Star
    BOTANICAL {} Dodecatheon
    ZONE {} Annual
    LIGHT {} Mostly Shady
    PRICE {} $8.60
    AVAILABILITY {} 051399
    PLANT {} 
    		
    COMMON {} Snakeroot
    BOTANICAL {} Cimicifuga
    ZONE {} Annual
    LIGHT {} Shade
    PRICE {} $5.63
    AVAILABILITY {} 071199
    PLANT {} 
    		
    COMMON {} Cardinal Flower
    BOTANICAL {} Lobelia cardinalis
    ZONE {} 2
    LIGHT {} Shade
    PRICE {} $3.02
    AVAILABILITY {} 022299



```python
#以一个节点为根深度优先遍历,查找有没有符合要求的元素
for elem in tree.iter(tag="COMMON"):
    print(elem.tag, elem.attrib,elem.text)
```

    COMMON {} Bloodroot
    COMMON {} Columbine
    COMMON {} Marsh Marigold
    COMMON {} Cowslip
    COMMON {} Dutchman's-Breeches
    COMMON {} Ginger, Wild
    COMMON {} Hepatica
    COMMON {} Liverleaf
    COMMON {} Jack-In-The-Pulpit
    COMMON {} Mayapple
    COMMON {} Phlox, Woodland
    COMMON {} Phlox, Blue
    COMMON {} Spring-Beauty
    COMMON {} Trillium
    COMMON {} Wake Robin
    COMMON {} Violet, Dog-Tooth
    COMMON {} Trout Lily
    COMMON {} Adder's-Tongue
    COMMON {} Anemone
    COMMON {} Grecian Windflower
    COMMON {} Bee Balm
    COMMON {} Bergamot
    COMMON {} Black-Eyed Susan
    COMMON {} Buttercup
    COMMON {} Crowfoot
    COMMON {} Butterfly Weed
    COMMON {} Cinquefoil
    COMMON {} Primrose
    COMMON {} Gentian
    COMMON {} Blue Gentian
    COMMON {} Jacob's Ladder
    COMMON {} Greek Valerian
    COMMON {} California Poppy
    COMMON {} Shooting Star
    COMMON {} Snakeroot
    COMMON {} Cardinal Flower


> 用XPath查找元素

`XPath`是一门在 XML 文档中查找信息的语言。XPath 可用来在 XML 文档中对元素和属性进行遍历。
XPath 是 W3C XSLT 标准的主要元素，对XPath 的理解是很多高级 XML 应用的基础.ElementTree支持XPath语法查找元素.

什么是 XPath?

XPath可以说是使用路径表达式在 XML 文档中进行导航的一个标准

支持的路径表达式有:

表达式|	描述
---|---
tag|选取此节点的所有子节点。
/	|从根节点选取。(绝对路径)
//	|从匹配选择的当前节点选择文档中的节点，而不考虑它们的位置。(相对路径)
.	|选取当前节点。
..	|选取当前节点的父节点。
@	|选取属性。
@ xxx=aaa|选取属性值为aaa的属性
\*|匹配任意元素节点
@\*|匹配任意元素
node()|匹配任意类型节点
[]|筛选
竖条|和


`iterfind()`方法可以使用XPath来查找需要的元素

>我们来打印出所有植物和他的对应价格并为大于5美元的计数


```python
countmony = 0 
for elem in zip(tree.iterfind("*/COMMON"),tree.iterfind("*/PRICE")):
    print(elem[0].tag, elem[0].text)
    print(elem[1].tag, elem[1].text)
    if float(elem[1].text[1:]) > 5:
        countmony += 1
print(countmony)
```

    COMMON Bloodroot
    PRICE $2.44
    COMMON Columbine
    PRICE $9.37
    COMMON Marsh Marigold
    PRICE $6.81
    COMMON Cowslip
    PRICE $9.90
    COMMON Dutchman's-Breeches
    PRICE $6.44
    COMMON Ginger, Wild
    PRICE $9.03
    COMMON Hepatica
    PRICE $4.45
    COMMON Liverleaf
    PRICE $3.99
    COMMON Jack-In-The-Pulpit
    PRICE $3.23
    COMMON Mayapple
    PRICE $2.98
    COMMON Phlox, Woodland
    PRICE $2.80
    COMMON Phlox, Blue
    PRICE $5.59
    COMMON Spring-Beauty
    PRICE $6.59
    COMMON Trillium
    PRICE $3.90
    COMMON Wake Robin
    PRICE $3.20
    COMMON Violet, Dog-Tooth
    PRICE $9.04
    COMMON Trout Lily
    PRICE $6.94
    COMMON Adder's-Tongue
    PRICE $9.58
    COMMON Anemone
    PRICE $8.86
    COMMON Grecian Windflower
    PRICE $9.16
    COMMON Bee Balm
    PRICE $4.59
    COMMON Bergamot
    PRICE $7.16
    COMMON Black-Eyed Susan
    PRICE $9.80
    COMMON Buttercup
    PRICE $2.57
    COMMON Crowfoot
    PRICE $9.34
    COMMON Butterfly Weed
    PRICE $2.78
    COMMON Cinquefoil
    PRICE $7.06
    COMMON Primrose
    PRICE $6.56
    COMMON Gentian
    PRICE $7.81
    COMMON Blue Gentian
    PRICE $8.56
    COMMON Jacob's Ladder
    PRICE $9.26
    COMMON Greek Valerian
    PRICE $4.36
    COMMON California Poppy
    PRICE $7.89
    COMMON Shooting Star
    PRICE $8.60
    COMMON Snakeroot
    PRICE $5.63
    COMMON Cardinal Flower
    PRICE $3.02
    23


###  iterparse(source, events=None, parser=None)处理XML流

我们刚讲过如何使用 ET 来将 XML 读入内存并且处理。但它就不会碰到和 DOM 一样的内存问题么？当然会。这也是为什么这个包提供一个特殊的工具，用来处理大型文档，并且解决了内存问题，这个工具叫 iterparse 。

他有4个关键字:

+ start---元素开始
+ end---元素结束
+ start-ns---命名空间开始
+ end-ns---命名空间结束

iterparse每次返回一个 (event, elem)对,可以用这些返回和关键字做匹配,调用回调函数达到解析的目的


> 我们来统计价钱大于5美元的植物有多少


```python
countf = 0
def counter():
    def count():
        global countf
        if float(elem.text[1:]) >5:
            countf += 1
        return countf
    return count
mycounter = counter()

for event,elem in ET.iterparse('source/plant_catalog.xml'):        
    keywords={
        "PRICE":mycounter
    }
    events={
        "start":lambda :False,
        "end":lambda :(keywords.get(elem.tag,lambda :False)()),
        "start-ns":lambda :False,
        "end-ns":lambda :False
    }
    events.get(event,lambda :False)()
    
print(countf)
```

    23


## 建立XML文档

ElementTree 对象提供了 write 方法可以用来建立xml文档,另外俩虽然也可以,但没这个方便.

我们要建立一个xml,需要从元素入手


```python
a = ET.Element("elema")# 创建一个元素
```


```python
b = ET.Element("elemb")
```


```python
sub1 = ET.Element("sub1")
```


```python
sub2 = ET.Element("sub2")
```


```python
root = ET.Element('root')
```


```python
a.text = "text"#为元素创建数据
```


```python
a.attrib = {"class":"a"}#创建属性
```


```python
sub1sub1 = ET.SubElement(sub1,"sub1sub1")#创建一个节点的子节点
```


```python
root.extend((a,b))#扩展节点
```


```python
b.extend((sub1,sub2))
```


```python
tree = ET.ElementTree(root)
```


```python
tree.write("output.xml")
```


```python
!cat output.xml
```

    <root><elema class="a">text</elema><elemb><sub1><sub1sub1 /></sub1><sub2 /></elemb></root>
