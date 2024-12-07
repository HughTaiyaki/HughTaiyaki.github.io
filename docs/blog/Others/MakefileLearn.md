# Makefile

## 参考资料
- [x] [跟我一起学makefile](https://seisman.github.io/how-to-write-makefile/overview.html)
- [x] [什么是Makefile](https://opensource.com/article/18/8/what-how-makefile)

## 简介与要点
为什么要用make，一个词来说就是:自动化

写一个makefile，就可以通过一句话命令来自动化编译，测试，打包，部署等一系列操作

- make 后面可以跟多个 target
- 可以在 make 后面直接通过 VAR=value 来设置变量
```shell
make a.o CFLAGS="-std=c11 -Wall"
```

- 常用makefile命令
    - `make` : 执行makefile中的第一个目标
    - `make target` : 执行makefile中的target目标
    - `make -n` : 显示执行makefile中的命令，但不执行
    - `make -f filename` : 执行filename中的makefile
    - `make -j n` : 并行执行n个任务
