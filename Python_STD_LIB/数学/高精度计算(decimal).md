
# 高精度计算(decimal)

高精度计算模块(decimal)提供了一种可用于代替float的数据类型,这种数据类型并不适合计算,但在需要高精度浮点运算时比较好用,适合用在财务上.

这种数据类型可以由整数,浮点数,数字字符串转化得来

## 获得当前精度环境


```python
from decimal import getcontext
```


```python
getcontext()
```




    Context(prec=28, rounding=ROUND_HALF_EVEN, Emin=-999999999, Emax=999999999, capitals=1, flags=[], traps=[DivisionByZero, InvalidOperation, Overflow])



## 设定精度


```python
getcontext().prec = 10
```

## 转化为`decimal`数据类型


```python
from decimal import Decimal
```


```python
Decimal(1) / Decimal(7)
```




    Decimal('0.1428571429')


