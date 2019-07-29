---
description: golang重构php项目，碰到的一些问题
---

# go 与php

## php go aes-256-cbc

php使用aes加密时，key的长度没有限制为16, 24, 32，但是go限制了。这就会导致部分解密异常。 如果key长度超过对应方式限制的长度，php在处理的时候只截取key实际需要的长度。如果长度不够php也会使用‘x00’填充,所以使用go解密时，key需要转为byte，并在末尾填充0

