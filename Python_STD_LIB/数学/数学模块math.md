
# 数学模块math

# 数学模块math
python自带的math模块提供了一些常用的数学运算和常数

## 常数

常数|说明
---|---
math.e |  自然常数e
math.pi | 圆周率pi

## 数值

函数|说明|例子
---|---|---
math.ceil(x)|返回大于x的整数上限的浮点数,x为整数则返回自己的浮点形式|math.ceil(1)->1.0,</br>math.ceil(1.1)->2.0,</br>math.ceil(-1.5)->-1.0
math.copysign(x, y)|返回绝对值为x,符号为y的符号的数|math.copysign(1.0, -0.0)->-1.0
math.fabs(x)|相当于abs(x),返回绝对值|math.fabs(-3.4)->3.4
math.factorial(x)|数学上的x!,阶乘|math.factorial(3)->6
math.floor(x)|与ceil相反,得到上限|math.floor(-0.5)->-1.0
math.fmod(x, y)|求模运算,适合用在浮点数,注意和`%`的不同|math.fmod(3.5, -2)->1.5</br>3.5%-2->-0.5
math.frexp(x)|将x拆成分(m,e),x== m * 2**e|math.frexp(2.43)->(0.6075, 2)
math.fsum(iterable)|求序列中所有数的和的精确值|fsum([.1, .1, .1, .1, .1, .1, .1, .1, .1, .1])->1.0
math.isinf(x)|判断x是不是`float("inf")`|---
math.isnan(x)|判断x是不是`float("NaN")`|---
math.ldexp(m,e)|求m * 2**e|math.ldexp(3, 1)->6.0
math.modf(x)|拆分整数小数部分|math.modf(-3.5)->(-0.5, -3.0)
math.trunc(x)|返回整数部分|math.trunc(3.5)->3

## 平方和对数

函数|说明|例子
---|---|---
math.exp(x)|自然数的幂 e**x|math.exp(2)->7.38905609893065
math.expm1(x)|返回e的x次方减1| math.expm1(2)->6.38905609893065
math.log(x[, base])| 返回x的以base为底的对数，base默认为e|math.log(math.e)->1.0</br>math.log(10,2)->3.3219280948873626
math.log10(x)|返回x的以10为底的对数| math.log10(2)->0.30102999566398114
math.log1p(x)|返回1+x的自然对数（以e为底)| math.log1p(math.e-1)->1.0
math.pow(x, y)|返回x的y次方|math.pow(5,3)->125.0
math.sqrt(x)|返回x的平方根|math.sqrt(3)->1.7320508075688772

## 三角函数

### 弧度

函数|说明
---|---
math.acos(x)|acos(x)
math.asin(x)|asin(x)
math.atan(x)|atan(x)
math.atan2(y, x)|atan(y / x)
math.cos(x)|cos(x)
math.hypot(x, y)|sqrt(x*x + y*y)
math.sin(x)|sin(x)
math.tan(x)|tan(x)

### 角度,弧度转换

函数|说明
---|---
math.degrees(x)|弧度转度
math.radians(x)|度转弧度

## 双曲函数

函数|说明
---|---
math.sinh(x)|双曲正弦
math.cosh(x)|双曲余弦
math.tanh(x)|双曲正切
math.acosh(x)|反双曲余弦
math.asinh(x)|反双曲正弦
math.atanh(x)|反双曲正切


## 特殊函数:


函数|说明
---|---
math.erf(x)|误差函数: `$\operatorname{erf}(x) = \frac{2}{\sqrt{\pi}}\int_0^x e^{-t^2}\,\mathrm dt.$`
math.erfc(x)|互补误差函数:`$\mbox{erfc}(x) = 1-\mbox{erf}(x) = \frac{2}{\sqrt{\pi}} \int_x^{\infty} e^{-t^2}\,\mathrm dt\,.$`
math.gamma(x)|伽玛函数 `$\Gamma(z) = \int_{0}^{\infty} \frac{t^{z-1}}{\mathrm{e}^t} \,{\rm{d}}t$`
math.lgamma(x)|伽马函数绝对值的自然对数


**在标准库中还有一个cmath,他是针对复数的数学库,差不太多就不做详细介绍了. 而3.4后新增的统计模块因为数据科学一般用2.7版本,所以也不多介绍**
