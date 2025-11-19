#fengchuirixio.github.io
**RSA加密**  
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
>>>n = p × q
>>>ψ(n) = (p-1) × (q-1)&emsp;&emsp;m^e ≡ C (mod n)&emsp;&emsp;c^d ≡ m (mod n)
>>>m^(e×d) ≡ m (mod n)
>><br>;3.2 其是依靠欧拉公式：
>>><br>&emsp;&emsp;m^φ(n) ≡ 1 (mod n)
>><br>3.3 其后续可以变为：
>>><br>&emsp;&emsp;m^(k × φ(n) + 1) ≡ m (mod n)
>>><br>&emsp;&emsp;e×d = k×ψ(n)+1 ⇒ e×d ≡ 1 (mod ψ(n))
>>><br>&emsp;&emsp;d = e^(-1) mod ψ(n)&emsp;&emsp;**or**&emsp;&emsp;d = pow(e, -1, ψ(n))
