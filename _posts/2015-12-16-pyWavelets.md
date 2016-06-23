

小波滤波器系数（wavelet filters coefficients） 可以通过 dec_lo、dec_hi、rec_lo、rec_hi 来获取

```
def print_array(arr):
	print "[%s]" % ", ".join(["%.14f" % x for x in arr])
print_array(w.dec_lo)
print_array(w.dec_hi)
print_array(w.rec_lo)
print_array(w.rec_hi)

w.filter_bank == (w.dec_lo, w.dec_hi, w.rec_lo, w.rec_hi)
```

离散小波变换 Discrete Wavelet Transform  dwt


wave object
创建小波对象：Wavelet(name, filter_bank=None)

* name: 小波名称
* filter_bank: 使用用户提供的滤波器组。该滤波器组必须实现:(dec_lo, dec_hi, rec_lo,rec_hi) =get_filters_coeffs()方法.

小波滤波器系数:

* dec_lo,dec_hi: 分解滤波器值
* rec_lo,rec_hi: 重构滤波器值
* dec_len: 分解滤波器长度
* rec_len: 重构滤波器长度

其他属性:

* family_name
* short_name
* orthogonal
* biorthogonal
* symmetry
* vanishing_moments_psi
* vanishing_moments_phi

```
Wavelet db3
  Family name:    Daubechies	# 多贝尔小波
  Short name:     db
  Filters length: 6
  Orthogonal:     True			# 正交性
  Biorthogonal:   True			# 双正交性
  Symmetry:       asymmetric	# 对称性
```

尺度函数phi(vanishing_moments_phi)和小波函数psi (vanishing_moments_psi)

```
>>> w.vanishing_moments_phi
0
>>> w.vanishing_moments_psi
3
```

创建自定义的 小波对象

1. Passing the filter bank object that implements the filter_bank attribute. The attribute must return four filters coefficients.

```
class MyHaarFilterBank(object):
    @property
    def filter_bank(self):
        from math import sqrt
        return ([sqrt(2)/2, sqrt(2)/2], [-sqrt(2)/2, sqrt(2)/2],
                [sqrt(2)/2, sqrt(2)/2], [sqrt(2)/2, -sqrt(2)/2])
                
my_wavelet = pywt.Wavelet('My Haar Wavelet', filter_bank=MyHaarFilterBank())

```

2. Passing the filters coefficients directly as the filter_bank parameter. 

```
from math import sqrt
my_filter_bank = ([sqrt(2)/2, sqrt(2)/2], [-sqrt(2)/2, sqrt(2)/2],
                  [sqrt(2)/2, sqrt(2)/2], [sqrt(2)/2, -sqrt(2)/2])
my_wavelet = pywt.Wavelet('My Haar Wavelet', filter_bank=my_filter_bank)
```

此上创建的小波是不会包含之前所述的所有属性的，我们还需要手动设置

```
my_wavelet.orthogonal = True
my_wavelet.biorthogonal = True
```

pyWavelets还包含了计算小波和尺度函数近似值的工具

