# 使用"最短运行时间先调度"逻辑的携程库
- 该库包含文件`cothread.h`和`cothread.cpp`
- 调度器使用的是借助优先级队列统计当前已经运行时间最短的携程，将其最先调度
- 使用的是`<ucontext.h>`
- 编译`g++ cothread.cpp main.cpp -o test`
- 执行时间统计结果
```shell
thread 1 has been running for 1079486461
thread 0 has been running for 1079495518

thread 1 has been running for 1080034983
thread 0 has been running for 1079986142

thread 1 has been running for 1080466323
thread 0 has been running for 1080492081
```
```shell
thread 3 has been running for 11560540
thread 2 has been running for 11543938
thread 1 has been running for 11658331
thread 0 has been running for 11509848

thread 3 has been running for 11964030
thread 2 has been running for 11938902
thread 1 has been running for 11784062
thread 0 has been running for 11879633
```
- 给thread添加了优先级设置功能，每个线程计算运行时间的时候用真实的时间/优先级
- 测试结果
```shell
thread 3 has been running for 8242206
thread 2 has been running for 6113781
thread 1 has been running for 4113923
thread 0 has been running for 2097486

thread 3 has been running for 8490418
thread 2 has been running for 6297884
thread 1 has been running for 4303349
thread 0 has been running for 2243932
```
- 四个线程优先级分别是4，3，2，1，可见效果还是明显的