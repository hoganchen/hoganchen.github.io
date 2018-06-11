---
title: comcka单元测试框架使用记录
date: 2018-06-11 15:50:41
tags:
---

<!-- more -->

<ol>

##### build example
```
hogan@hogan:~/framework/cmocka/tests$ gcc -o test_ordering_fail test_ordering_fail.c -I ../build/ -I ../include/ -lcmocka

hogan@hogan:~/framework/cmocka/tests$ gcc -o test_skip test_skip.c -lcmocka

hogan@hogan:~/framework/cmocka/tests$ gcc -o test_ordering test_ordering.c -I ../build/ -I ../include/ -lcmocka

cd ~/share/framework/cmocka/build/example
make clean
make
```