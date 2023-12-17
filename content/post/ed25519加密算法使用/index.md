---
title: ed25519加密算法使用
description: 一种高速高安全的签名方法
slug: ed25519
date: 2023-07-22
image:
categories:
- Nodejs
tags:
- nodejs
- 加密算法
---

## 介绍
> Ed25519是一个公钥签名系统。
   快速单签名验证，该软件只需要273364个周期来验证英特尔广泛部署的Nehalem/Westmere系列cpu上的签名。(此性能测量是针对短消息的;对于非常长的消息，验证时间主要由哈希时间决定。)Nehalem和Westmere包括2008年至2010年间发布的所有酷睿i7、i5和i3 cpu，以及同一时期发布的大部分至强cpu。
  甚至更快的批量验证，该软件执行一批64个单独的签名验证(在64个公钥下验证64个消息的64个签名)，仅855万次循环，即每个签名在134000次循环以下。该软件很容易适应L1缓存，因此内核之间的争用可以忽略:四核2.4GHz的Westmere每秒验证71000个签名，同时将最大验证延迟保持在4毫秒以下。
  非常快的签名，该软件只需要87548个周期来签署消息。四核2.4GHz韦斯特米尔每秒可签署109000条消息。
  快速生成密钥，密钥生成几乎和签名一样快。为了从操作系统获得安全的随机数，生成密钥会有轻微的代价;Linux下的/dev/urandom大约需要6000个循环。
  安全级别高，该系统的安全目标为2^128;破解它的难度与破解NIST P-256、拥有3000位密钥的RSA、强128位分组密码等类似。已知的最佳攻击实际上平均花费超过2^140位操作，并且随着位操作数量的下降，成功概率呈二次下降。
  万无一失的会话密钥。确定地生成签名;密钥生成需要新的随机性，但新签名不需要。这不仅是一个速度特性，也是一个安全特性，与最近索尼PlayStation 3安全系统崩溃直接相关。

> ED25519是一个非对称加密的签名方法，非常快、非常安全、产生的数据也非常小。

### ED25519的签名长度，公钥长度是多少？
> 签名长度为64字节，公钥长度为32字节

### 什么是数字签名？
> 数字签名（又称公钥数字签名）是只有信息的发送者才能产生的别人无法伪造的一段数字串，这段数字串同时也是对信息的发送者发送信息真实性的一个有效证明。
   是用于鉴别数字信息的方法，有签名并有验证。数字签名是非对称密钥加密技术（如ED25519）与数字摘要技术的应用。
   数字签名就是附加在数据单元上的一些数据，或者是针对数据所做出的一种密码变换。这种数据或变换允许数据单元的接收者用以确认数据单元的来源和数据单元的完整性并保护数据，即数字签名与验证同在。

### 数字签名的级别？
> 数字签名的级别是很高的，是具备不可否定性的。

### 数字签名大致有哪些算法？
> RSA、ElGamal、Fiat-Shamir、Guillou- Quisquarter、Schnorr、Ong-Schnorr-Shamir数字签名算法、Des/DSA，椭圆曲线数字签名算法和有限自动机数字签名算法等。特殊数字签名有盲签名、代理签名、群签名、不可否认签名、公平盲签名、门限签名、具有消息恢复功能的签名等。
   目前用到的是“椭圆曲线数字签名（ECDSA）”。

### 什么是“椭圆曲线数字签名(ECDSA)”？
> 简称ECC算法，是基于数学理论的椭圆曲线来实现的一种“非对称加密”算法。

### ECC的特点？
> 密钥的长度很短，高安全。

### 在数学理论中什么是“椭圆曲线”？
> 椭圆曲线指，在特定条件下的特定点的集合所形成的规律（即椭圆曲线公式）。

### 数字签名特点？
> 每条信息都有一对密钥，其中一个是信息自身的密钥，另一个是公开的公钥。
   在信息或者数据开始签名时用的是密钥，在进入验证时用的是公钥。
   在验证时公钥是公用的，那如何进行准确识别每条信息或数据？
   所有信息都可以被定义，所以公钥需要先向接收端进行注册（身份认证机构），这时就产生了“注册机”，在注册后身份认证机构会写入一串数字证书，然后在对信息签名时，会将数字证书和签名绑定到信息上一起发送到接收端，接收端会向身份认证机构确认密钥的正确性，从而判断密钥和信息是否匹配。

### 签名过程是什么？
> 发送报文时，发送方用一个哈希函数从报文文本中生成报文摘要，然后用发送方的私钥对这个摘要进行加密，这个加密后的摘要将作为报文的数字签名和报文一起发送给接收方，接收方首先用与发送方一样的哈希函数从接收到的原始报文中计算出报文摘要，接着再公钥来对报文附加的数字签名进行解密，如果这两个摘要相同、那么接收方就能确认该报文是发送方的。

### 什么是哈希函数？
> 哈希函数（Hash Function），也称为散列函数，给定一个输入x，它会算出相应的输出H(x)。

### 哈希函数的算法特点是什么？
>   1.输入x可以是任意长度的字符串。
  2.输出结果即H(x)的长度是固定的。
  3.计算 H(x) 的过程是高效的（对于长度为 n 的字符串 x ，计算出 H(x) 的时间复杂度应为 O(n) ）。

### 哈希函数在运用时有什么要求？
>   1、免碰撞：即不会出现输入 x≠y ，但是H(x)=H(y) 的情况，其实这个特点在理论上并不成立，比如目前比特币使用的 SHA256 算法，会有 2^256 种输出，如果我们进行 2^256 + 1 次输入，那么必然会产生一次碰撞，事实上，通过 理论证明 ，通过 2^130 次输入就会有99%的可能性发生一次碰撞。
  2、隐匿性：对于一个给定的输出结果 H(x) ，想要逆推出输入 x ，在计算上是不可能的。如果想要得到 H(x) 的可能的原输入，不存在比穷举更好的方法。

### 哈希算法的原理是什么？
>  是试图将一个空间的数据集映射到另外一个空间（通常比原空间要小），并利用质数将数据集能够均匀的映射。

### 目前有哪些哈希算法？
>  md4、md5、sha系列等。

## 使用
```javascript
import nacl from "tweetnacl"

//string和uint8Array互转
//https://cloud.tencent.com/developer/ask/sof/302640

//base64和uint8Array互转
//https://blog.csdn.net/qq_35606400/article/details/125629074

// uint8array转为base64字符串
const uint8arrayToBase64 = function(u8Arr) {
    try{
         let CHUNK_SIZE = 0x8000; //arbitrary number
         let index = 0;
         let length = u8Arr.length;
         let result = '';
         let slice;
         while (index < length) {
             slice = u8Arr.subarray(index, Math.min(index + CHUNK_SIZE, length));
             result += String.fromCharCode.apply(null, slice);
             index += CHUNK_SIZE;
         }
         // web image base64图片格式: "data:image/png;base64," + b64encoded;
         // return  "data:image/png;base64," + btoa(result);
         return btoa(result);
     }
     catch(e) {
         throw e;
     }
 }
// base64字符串转为uint8array数组
const base64ToUint8Array = function(base64String) {
    try{
        let padding = '='.repeat((4 - base64String.length % 4) % 4);
        let base64 = (base64String + padding)
            .replace(/\-/g, '+')
            .replace(/_/g, '/');
        let rawData = atob(base64);
        let outputArray = new Uint8Array(rawData.length);
        for (let i = 0; i < rawData.length; ++i) {
            outputArray[i] = rawData.charCodeAt(i);
        }
        return outputArray;
    }
    catch(e) {
        throw e;
    }
}

// string转uint8array
function toUint8Arr(str) {
    const buffer = []
    for (let i of str) {
        const _code = i.charCodeAt(0)
        if (_code < 0x80) {
            buffer.push(_code)
        } else if (_code < 0x800) {
            buffer.push(0xc0 + (_code >> 6))
            buffer.push(0x80 + (_code & 0x3f))
        } else if (_code < 0x10000) {
            buffer.push(0xe0 + (_code >> 12))
            buffer.push(0x80 + (_code >> 6 & 0x3f))
            buffer.push(0x80 + (_code & 0x3f))
        }
    }
    return Uint8Array.from(buffer)
}

/**
 * 使用tweetnacl进行签名
 * signContent 签名内容
 */
function tweetnaclSign(signContent) {
    // 生成 公钥、私钥
    // let keyMap = nacl.sign.keyPair()
    // let publicKey = keyMap.publicKey
    // let secretKey = keyMap.secretKey

    console.log("待签名内容: ", signContent)

    console.log("用户服务端的公钥和私钥")
    let publicKey = base64ToUint8Array("BXJXQSSIuVCdHU7FUj/e4McA6MHVP0t7AR9tQg4GyF0=")
    let secretKey = base64ToUint8Array("ZBsmNTR/pwQDSKX261V5g+7zgpfXY9ejRvLDPiK4GXwFcldBJIi5UJ0dTsVSP97gxwDowdU/S3sBH21CDgbIXQ==")

    // 字符串转为Uint8Array格式，以供签名
    let signArray = toUint8Arr(signContent)
    // 进行签名
    let signature = nacl.sign.detached(signArray, secretKey)

    // 进行验签
    let verify = nacl.sign.detached.verify(signArray, signature, publicKey)

    console.log({
        '公钥': uint8arrayToBase64(publicKey),
        '私钥': uint8arrayToBase64(secretKey),
        '签名': uint8arrayToBase64(signature),
        '验签成功': verify
    })
}

let msgData = '哈哈哈哈'
tweetnaclSign(msgData)
```