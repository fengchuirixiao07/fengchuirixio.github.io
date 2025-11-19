# fengchuirixio.github.io
>**RSA加密**  
>>1.同余：
>><br> &emsp;&emsp; $a \equiv b \pmod{m}$
>>1.1 逆元：
>><br> &emsp;&emsp; $a \times x \equiv 1 \pmod{m}$
>>&emsp;&emsp;	$x \equiv a^{-1} \pmod{m}$&emsp;&emsp;则称x为a模m的逆元
>**2.RSA加密原理：**
>><br> n为模数&emsp;&emsp;e为公钥指数&emsp;&emsp;c为密文&emsp;&emsp;m为明文
>><br>​$c \equiv m^e \pmod{n}$
>**3.RSA解密原理**
>><br>其是依靠欧拉公式：
>>>$$ m^{\varphi(n)} \equiv 1 \quad (\bmod n) $$
