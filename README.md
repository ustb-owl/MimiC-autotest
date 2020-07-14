# MimiC 自动化测试工具

一键测试就完事了.

## 在本地开发环境 (`x86/amd64`) 使用

请首先确保本地的 `compiler` 仓库已经 `checkout` 到了 `dev` 分支, 并且拉取了最新的提交. 然后你需要构建得到 MimiC 编译器的可执行文件:

```
# 当前工作目录: 仓库根目录
$ mkdir build && cd build
$ cmake .. && make -j8
$ cd ..
```

之后, 在仓库根目录建立一个 `debug` 目录, 并在此处 `clone` 该仓库:

```
$ mkdir debug && cd debug
$ git clone --recursive https://gitlab.eduxiji.net/csc2020-ustb-deadbeef/autotest.git
$ cd autotest
```

该仓库包含了自动化测试脚本 `run.py` (你的系统中必须安装 `python3.6+` 才能运行该脚本). 在运行脚本之前, 请仔细阅读脚本开头的配置参数, 并且根据环境的实际情况进行修改. 如需一键测试, 请执行:

```
$ ./run.py
```

当然你如果只想运行某个测试用例也是可以的, 比如:

```
$ ./run.py -i sysyruntimelibrary/performance_test/00_bitset1.sy
```

## 在 `armdev` 环境使用

默认情况下, `armdev` 环境不包含 `git`, `g++`, `cmake` 和 `python3`, 你需要自行安装. 然后在你喜欢的位置执行以下命令:

```
$ git clone --depth 1 --single-branch --branch dev https://gitlab.eduxiji.net/csc2020-ustb-deadbeef/compiler.git
$ cd compiler && mkdir build && cd build
$ cmake .. && make -j8
$ mkdir ../debug && cd ../debug
$ git clone --recursive https://gitlab.eduxiji.net/csc2020-ustb-deadbeef/autotest.git
$ cd autotest
```

此时你就可以按照上一节所述的内容来运行自动化测试脚本了, 但记得加上 `-c` 参数, 因为要执行交叉编译 (cross-compile):

```
$ ./run.py -c
$ ./run.py -c -i sysyruntimelibrary/performance_test/00_bitset1.sy
```
