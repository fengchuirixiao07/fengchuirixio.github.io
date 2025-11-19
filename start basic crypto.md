**1.RSA加密**  
><br>**1.同余：**
>><br> &emsp;&emsp; $a \equiv b \pmod{m}$
>>><br>1.1 逆元：
>>><br> &emsp;&emsp; $a \times x \equiv 1 \pmod{m}$
>>>&emsp;&emsp;	$x \equiv a^{-1} \pmod{m}$&emsp;&emsp;则称x为a模m的逆元

><br>**2.RSA加密原理：**
>><br> n为模数&emsp;&emsp;e为公钥指数&emsp;&emsp;c为密文&emsp;&emsp;m为明文
>><br>​c ≡ m^e (mod n)

><br>**3.RSA解密原理:**
>><br>3.1 选择两个大质数 p和 q，并计算模数 n和欧拉函数 φ(n):
>><br>n = p × q
>><br>ψ(n) = (p-1) × (q-1)&emsp;&emsp;m^e ≡ C (mod n)&emsp;&emsp;c^d ≡ m (mod n)
>><br>m^(e×d) ≡ m (mod n)
>><br>3.2 其是依靠欧拉公式：
>><br>&emsp;&emsp;m^φ(n) ≡ 1 (mod n)
>><br>3.3 其后续可以变为：
>><br>&emsp;&emsp;m^(k × φ(n) + 1) ≡ m (mod n)
>><br>&emsp;&emsp;e×d = k×ψ(n)+1 ⇒ e×d ≡ 1 (mod ψ(n))
>><br>&emsp;&emsp;d = e^(-1) mod ψ(n)&emsp;&emsp;**or**&emsp;&emsp;d = pow(e, -1, ψ(n))
>><br>&emsp;&emsp;m = c^d mod(n)
<br>
<br>

**2.共享素数攻击**
><br>通过gcd（n1,n2) = 共享素数p
>><br>q1 = n1 // p&emsp;&rArr;φ (n1) = (p-1)(q1-1)&emsp;&rArr;d1=e^(-1)mod/φ(n1)
>><br>q2 = n2 // p&emsp;&rArr;φ (n2) = (p-1)(q2-1)&emsp;&rArr;d2=e^(-1)mod/φ(n2)
>><br>m1 = c^(d1)mod n1
<br>
<br>

**3.中国剩余定理**
><br>$$
\begin{cases}
x \equiv a_{1} \pmod{m_{1}} \\
x \equiv a_{2} \pmod{m_{2}} \\
\vdots \\
x \equiv a_{k} \pmod{m_{k}}
\end{cases}
$$
>>模M = m<sub>1</sub> * m<sub>2</sub> * m<sub>3</sub> * …… * m<sub>k</sub>
>><br>Mi = M /mi&emsp;&emsp;&emsp;逆元x = pow（M<sub>i</sub>,-1,m<sub>i</sub>)
>>><br>x ≡ (a<sub>1</sub> * M<sub>1</sub> * x<sub>1</sub> + a<sub>2</sub> * M<sub>2</sub> * x<sub>2</sub>+……+a<sub>k</sub> * M<sub>k</sub> * x<sub>k</sub>)mod(M)
```python
import Crypto.Util.number from *
import gmpy2
me = gmpy2.iroot(x,k)[0]
```
**4.小明文攻击**
><br>只是适用于c 与 n的数量级差距很大时及m^e mod n = c，m^e =c
直接开方运算
>><br>$m^e$ < n
>><br> c =>m^emod(n)
>><br> c = >m^e
```python
import Crypto.Util.number from *
import gmpy2
m = gmpy2.iroot(c,e)[0]
```
**5.费马小定理**
><br>形式一：如果 p是一个质数，且整数 a不是 p的倍数（即 a与 p互质，gcd(a,p)=1)，那么有：
><br>&emsp;&emsp;a^(p - 1)  ≡ 1 mod(p)
><br>形式二：如果 p是一个质数，对于任意整数 a，有：
><br>&emsp;&emsp;a^p ≡  p mod(p)
>><br>临近素数问题
>>><br>*1.平方差遍历法*
>>><br>如果素数 p和 q临近，那么它们的算术平均值 a与它们之间的差值 b都会很小。我们可以将模数 N=p×q表示为一个平方差公式：
>>>设 p=a−b，q=a+b。 其中 a 和 b 的定义为：a =(p + q)//2&emsp;&emsp; b = (q - p）//2
>>><br>&emsp;&emsp;N=p×q=(a−b)(a+b)=a^2 - b^2
>>><br>b^2 = a^2 -N
```python
from Crypto.Util.number import *
from sympy import *
import gmpy2
n = 122719648746679660211272134136414102389555796575857405114496972248651220892565781331814993584484991300852578490929023084395318478514528533234617759712503439058334479192297581245539902950267201362675602085964421659147977335779128546965068649265419736053467523009673037723382969371523663674759921589944204926693
e = 65537
c = 109215817118156917306151535199288935588358410885541150319309172366532983941498151858496142368333375769194040807735053625645757204569614999883828047720427480384683375435683833780686557341909400842874816853528007258975117265789241663068590445878241153205106444357554372566670436865722966668420239234530554168928
a = gmpy2.iroot(n,2)[0]
while 1:
    b_2 = a*a - n
    if gmpy2.is_square(b_2):
        b = gmpy2.iroot(b_2,2)[0]
        p = a - b
        q = a + b
        if p * q == n:  
            break
    a += 1
'''assert pow(666666, x, p) == 1'''
x = p - 1
phi = (p - 1) * (q - 1)
d = pow(e,-1,phi)
m_ = pow(c,d,n)
m = m_ ^ x
 
print(long_to_bytes(m))


```
>>><br>*2.相邻素数法*
```python
from Crypto.Util.number import *
import gmpy2
e = 65537
n = 169522900072954416356051647146585827691225327527086797334523482640452305793443986277933900273961829438217255938808371865341750200444086653241610669340348513884285892043530862971785487294831341653909852543469963032532560079879299447677636753647721541724969084825510405349373420839032990681851700075554428485967
c = 105943762023156641770119141175498496686312095002592803768522760959533958364969985856505466722378959991757667341747887520146437729810252085791886309974903778546814812093444837674447485802109225767800488527376777153844313243366001288246744190001997192598159277512188417272938455513900277907186067996704043274199
t=gmpy2.iroot(n,2) 
p=gmpy2.next_prime(t[0]) 
x=(p-1)*1024
q=n // p 
phi = (p - 1) * (q - 1) 
d=inverse(e,phi) 
m_ = pow (c,d,n) 
m = m_ ^ x 
print(long_to_bytes(m)) 

```
>><br>**适用范围差异**
>>><br>1.平方差遍历法 适用条件 p和q相近&emsp;&emsp;&emsp;&emsp;适用条件 p和q相近&emsp;&emsp;&emsp;&emsp;搜索范围 从√n开始线性搜索 &emsp;&emsp;&emsp;&emsp;成功率 较高（只要p,q相近）
>>><br>2.直接找相邻素数法 &emsp;&emsp;&emsp;&emsp;适用条件 p和q相近&emsp;&emsp;&emsp;&emsp;搜索范围 只检查一个特定的素数&emsp;&emsp;&emsp;&emsp;较低（依赖特定假设）

**6.dp泄露**
>其形式：dp = d mod (p-1)
>><br>&emsp;&emsp;e×d = k×ψ(n)+1 ⇒ e×d ≡ 1 (mod ψ(n))
>><br>&emsp;&emsp;e×dp ≡ 1 (mod (p-1))
>><br>&emsp;&emsp;e×dp ≡ 1 + k * (p-1)
>><br>&emsp;&emsp;(e×dp-1)//k = p-1
```python
from Crypto.Util.number import *
import gmpy2
n = 110231451148882079381796143358970452100202953702391108796134950841737642949460527878714265898036116331356438846901198470479054762675790266666921561175879745335346704648242558094026330525194100460497557690574823790674495407503937159099381516207615786485815588440939371996099127648410831094531405905724333332751
dp = 3086447084488829312768217706085402222803155373133262724515307236287352098952292947424429554074367555883852997440538764377662477589192987750154075762783925
c = 59325046548488308883386075244531371583402390744927996480498220618691766045737849650329706821216622090853171635701444247741920578127703036446381752396125610456124290112692914728856924559989383692987222821742728733347723840032917282464481629726528696226995176072605314263644914703785378425284460609365608120126
e = 65537
for i in range(1,e):
    if (dp*e-1)%i == 0:
        if (n%((dp*e-1)//i+1)) == 0:
            p = (dp*e-1)//i+1
            q = n // p
            phi_n = (p-1)*(q-1)
            d = pow(e,-1,phi_n)
            m = pow(c,d,n)
print(long_to_bytes(m))
```
*补充定理*
><br>定理：比如m = c ^d mod n 
><br>n = p*q(p,q 都是素数)那么 m = c^d mod p &emsp;&emsp;*or*&emsp;&emsp; m = c^d mod q 
><br>phi =（p -1）*(q -1),也可以以此类推，找其与e互质的部分满足逆元使用条件



**7.线性同余生成器（lcg）**
><br>递推公式：X <sub>n+1</sub>=(a×X <sub>n</sub>+b)modm
><br>参数说明：X <sub>n</sub>：当前状态（种子） &emsp;&emsp;a：乘数 &emsp;&emsp;b：增量 &emsp;&emsp;m：模数

>><br>求初始Seed：
<br> x<sub>n</sub>≡(x<sub>n+1</sub> - b) * a^(-1) mod(m)
>><br>求a：
><br>x<sub>n+1</sub>=(a * x<sub>n</sub> +  b)mod(m)
><br>x<sub>n</sub>=(a * x<sub>n-1</sub> +  b)mod(m)
><br>>x<sub>n+1</sub> - x<sub>n</sub> = (a * (x<sub>n</sub> - x<sub>n-1</sub> ))mod(m)
><br>a ≡ (x<sub>n+1</sub> - x<sub>n</sub>) * (x<sub>n</sub> - x<sub>n-1</sub> )^(-1) mod (m)
>><br>求b：
><br>b ≡ (x<sub>n+1</sub> - a * x<sub>n</sub>) mod(m)
>><br>求m：
><br>t<sub>n</sub> = x<sub>n+1</sub> - x<sub>n</sub>
><br>=[(a*x<sub>n</sub>+b)-(a*x<sub>n-1</sub>+b)+b)]mod(m)
><br>=a*t<sub>n-1</sub>+b)+b)mod(m)
><br>t<sub>n+1</sub>*t<sub>n-1</sub>=a*t<sub>n</sub>*t<sub>n-1</sub>=(t<sub>n</sub>)^(2)

