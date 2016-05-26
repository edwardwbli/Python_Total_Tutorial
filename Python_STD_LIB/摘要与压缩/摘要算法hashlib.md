
# python3基础应用--摘要算法(hashlib)

Python的hashlib提供了常见的摘要算法，如MD5，SHA1等等。

什么是摘要算法呢？摘要算法又称哈希算法、散列算法。它通过一个函数，把任意长度的数据转换为一个长度固定的数据串（通常用16进制的字符串表示）

常见的用途比如文件校验,下载下来的文件可以通过md5校验判断是否是原版文件

还有一种是用来存储用户的密码,大家都知道明文密码存储在数据库里很不安全,所以可以通过摘要算法给密码加个密存储进去.

有没有可能两个不同的数据通过某个摘要算法得到了相同的摘要？完全有可能，因为任何摘要算法都是把无限多的数据集合映射到一个有限的集合中。这种情况称为碰撞，比如Bob试图根据你的摘要反推出一篇文章'how to learn hashlib in python - by Bob'，并且这篇文章的摘要恰好和你的文章完全一致，这种情况也并非不可能出现，但是非常非常困难。


```python
import hashlib 
```

# md5


```python
psw="haolaoshixihuandadota2"
```


```python
md5 = hashlib.md5()
```


```python
md5.update(psw.encode('utf-8'))
print(md5.hexdigest())
```

    acc5d43185d33c88def863ac18704561


## SHA1


```python
sha1 = hashlib.sha1()
```


```python
sha1.update(psw.encode("utf-8"))
print(sha1.hexdigest())
```

    e53754d171a425b1dbb4a215cd86d568050055c5


##  sha224, sha256, sha384, sha512

一样的操作,只是时间花费不同而已


```python
sha224 = hashlib.sha224()
```


```python
sha224.update(psw.encode("utf-8"))
print(sha224.hexdigest())
```

    660b6249c5213d05e1df371cf7cae75fd9369a467684bc631c44d0f4


## 长字符串操作

长字符串或者一个分段的字符串要作摘要可以分段的进行update,结果是一样的


```python
x_md5 = hashlib.md5()
x_md5.update('how to use md5 in '.encode('utf-8'))
x_md5.update('python hashlib?'.encode('utf-8'))
print(x_md5.hexdigest())
```

    d26a53750bc40b38b65a520292f69306

