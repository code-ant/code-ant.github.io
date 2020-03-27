---
title: 【每日一题】int32 to IPv4
date: 2020-01-27 11:45:33
tags: [算法,CodeWars,BINARY]
categories: [每日一题,CodeWars]
---

### 【CodeWars】int32 to IPv4

Take the following IPv4 address: `128.32.10.1`

This address has 4 octets where each octet is a single byte (or 8 bits).

- 1st octet `128` has the binary representation: `10000000`
- 2nd octet `32` has the binary representation: `00100000`
- 3rd octet `10` has the binary representation: `00001010`
- 4th octet `1` has the binary representation: `00000001`

So `128.32.10.1` == `10000000.00100000.00001010.00000001`

Because the above IP address has 32 bits, we can represent it as the unsigned 32 bit number: `2149583361`

Complete the function that takes an unsigned 32 bit number and returns a string representation of its IPv4 address.

<!-- more-->

### Examples

```shell
2149583361 ==> "128.32.10.1"
32         ==> "0.0.0.32"
0          ==> "0.0.0.0"
```



### 解题思路

按照题目描述，点分十进制的IP地址转换成点分二进制之后，去掉分隔符后转化成unsigned 32位整数。例如：

```
128.32.10.1 ---> 10000000.00100000.00001010.00000001 ---> 10000000001000000000101000000001 ---> 2149583361
```

此题最终思路只需将上述转化过程逆序实现即可。



利用与运算取最后8位二进制：2149583361 & 0xff

利用无符号右移、与运算取倒数第二个8位二进制：2149583361>>>8 & 0xff

同理：

```java
public class Kata {
    public static String longToIP(long ip) {
        return String.format("%d.%d.%d.%d",ip >>> 24 & 0xff,ip >>> 16 & 0xff,ip >>> 8 & 0xff,ip & 0xff);
    }
}
```





