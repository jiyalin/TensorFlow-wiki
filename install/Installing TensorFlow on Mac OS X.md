# 在 Mac OS X 上安装 TensorFlow

这个文档说明了如何在 Mac OS X 上安装 TensorFlow。

```
注意：从 1.2 版本开始，在 Mac OS X 上 TensorFlow 不再支持 GPU。
```



## 确定如何安装 TensorFlow

你可以选择一种方式安装 TensorFlow，支持下面的几种选择：

- virtualenv
- "本地" pip
- Docker
- 从源代码安装，更专业有单独的文档记录

我们建议使用 virtualenv 安装。[virtualenv](https://virtualenv.pypa.io/en/stable/) 是一个和其它 Python 项目开发隔离的虚拟 Python 环境，在同一台机器上不会干扰也不会被其它程序影响。virtualenv 安装过程中，你不仅仅安装了 TensorFlow 还有它的所有依赖包。（事实上这很简单）要开始使用 TensorFlow，你需要“启动” virtualenv 环境。总而言之，virtualenv 提供了一个安全可靠的 TensorFlow 安装和运行机制。

本地 pip 安装 TensorFlow 不经过任何容器或者虚拟环境系统直接装到了系统上，由于本地 pip 安装没被关闭，pip 安装会干扰或者影响系统上其它有 Python 依赖的安装。而且，如果要通过本地 pip 安装，你需要禁用系统完整性保护（SIP）。然而，如果你了解 SIP，pip 和 你的 Python 环境，本地 pip 安装相对容易执行。

[Docker](http://docker.com/) 可使 TensorFlow 的安装完全脱离于机器上的其它已存在的包，Docker 容器包括 TensorFlow 和它的所有依赖。注意 Docker 镜像可能很大（几百 M）。如果你已将 TensorFlow 集成到使用了 Docker 的大型应用架构中可以选择 Docker 安装。

选择 Anaconda，你可以使用 conda 创建一个虚拟环境，我们建议使用 `pip install` 命令而不是 `coda install` 命令安装 TensorFlow。

```tex
注意：coda 包是社区而不是官方支持，也就是说，TensorFlow 团队既不测试也不维护 conda 包，如果使用风险自己承担。
```



## 使用 virtualenv 安装

按照以下步骤安装 TensorFlow：

1. 打开终端（一个 shell），你将在这个终端中执行随后的步骤

2. 通过以下命令安装 pip 和 virtualenv：

   ```shell
   $ sudo easy_install pip
   $ sudo pip install --upgrade virtualenv
   ```

3. 执行以下任一命令创建虚拟环境：

   ```shell
    $ virtualenv --system-site-packages targetDirectory # for Python 2.7
    $ virtualenv --system-site-packages -p python3 targetDirectory # for Python 3.n
   ```

   targetDirectory 因虚拟环境根路径而异，我们的命令假使 targetDirectory 是 `~/tensorflow`，但你可以选择任一目录。

4. 执行任一命令激活虚拟环境：

   ```shell
   $ source ~/tensorflow/bin/activate      # If using bash, sh, ksh, or zsh
   $ source ~/tensorflow/bin/activate.csh  # If using csh or tcsh 
   ```

   上面的 *source* 命令应该将提示符改成了下面这样：

   ```shell
   (tensorflow)$ 
   ```

5. 如果已经安装了 pip 8.1 或者更新的版本，执行以下任一命令在激活的虚拟环境中安装 TensorFlow 及其所有依赖：

   ```shell
    $ pip install --upgrade tensorflow      # for Python 2.7
    $ pip3 install --upgrade tensorflow     # for Python 3.n
   ```

   如果前面的命令执行成功了，跳过步骤 6；如果失败了，再执行步骤 6。

6. 可选，如果步骤 5 失败了（一般是因为你使用了低于 8.1 版本的 pip），执行以下任一命令在激活的虚拟环境中安装 TensorFlow：

   ```shell
    $ pip install --upgrade tfBinaryURL   # Python 2.7
    $ pip3 install --upgrade tfBinaryURL  # Python 3.n 
   ```

   *tfBinaryURL* 是 Tensorflow 包的 URL，准确的 tfBinaryURL 值因操作系统和 Python 版本而异，在[这里](#TensorFlow Python 包 URL)找到和你系统相关的 *tfBinaryURL* 值。例如，你要在 Mac OS X 上安装 Python 2.7 对应的 Tensorflow 版本，在虚拟环境中安装 Tensorflow 就执行下面的命令：

   ```shell
   $ pip3 install --upgrade \
    https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.2.1-py2-none-any.whl
   ```


如果安装过程中遇到麻烦，参考[常见安装问题]()。

### 下一步

安装完成后，验证你的安装是否工作正常。

注意，每打开一个新的 shell 使用 TensorFlow 都必须激活虚拟环境。如果当前虚拟环境没有被激活（也就是提示符不是 *tensorflow*），执行以下任一命令：

```shell
$ source ~/tensorflow/bin/activate      # bash, sh, ksh, or zsh
$ source ~/tensorflow/bin/activate.csh  # csh or tcsh 
```

你的提示符变成下面这样说明 tensorflow 环境已经激活：

```shell
(tensorflow)$ 
```

当虚拟环境激活后，你可以在这个 shell 中运行 TensorFlow 程序。如果你不再使用 TensorFlow，可以通过下面命令退出环境：

```shell
(tensorflow)$ deactivate 
```

提示符将会恢复到默认的（在 PS1 中定义的）。

### 卸载 TensorFlow

如果你想卸载 TensorFlow，简单地移除你创建的目录。例如：

```shell
 $ rm -r ~/tensorflow 
```



## 使用本地 pip 安装

我们已经将 TensorFlow 二进制文件上传到了 PyPI，因此你可以通过 pip 安装， [REQUIRED_PACKAGES section of setup.py](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/pip_package/setup.py) 文件列出了 pip 将要安装或升级的包。

### 必备: Python

要安装 TensorFlow，你的系统必须依据安装了以下任一 Python 版本：

- Python 2.7
- Python 3.3+

如果你的系统还没有安装符合以上版本的 Python，现在[安装]((https://wiki.python.org/moin/BeginnersGuide/Download))。

安装 Python，你可能需要禁用系统完整性保护（SIP）来获得从 Mac App Store 外安装软件的许可。

### 必备: pip

[Pip](https://en.wikipedia.org/wiki/Pip_(package_manager)) 安装和管理 Python写的软件包，如果你要使用本地 pip 安装，系统上必须安装下面的任一 pip 版本：

- `pip`, for Python 2.7
- `pip3`, for Python 3.n.

pip 或者 pip3 可能在你安装 Python 的时候已经安装了，执行以下任一命令确认系统上是否安装了 pip 或 pip3：

```shell
$ pip -V  # for Python 2.7
$ pip3 -V # for Python 3.n 
```

我们强烈建议使用 pip 或者 pip3 为 8.1 或者更新的版本安装 TensorFlow，如果没有安装，执行以下任一命令安装或更新：

```shell
$ sudo easy_install --upgrade pip
$ sudo easy_install --upgrade six 
```

### 安装 TensorFlow

假设你的 Mac 上已经装好了必备的程序，按照以下步骤执行：

1. 执行以下任一命令安装 TensorFlow：

   ```shell
    $ pip install tensorflow      # Python 2.7; CPU support
    $ pip3 install tensorflow     # Python 3.n; CPU support
   ```

   如果上面的命令执行完成，现在可以验证你的安装了。

2. (可选的) 如果步骤 1 失败了，执行下面的命令安装最新版本 TensorFlow：

   ```shell
    $ sudo pip  install --upgrade tfBinaryURL   # Python 2.7
    $ sudo pip3 install --upgrade tfBinaryURL   # Python 3.n 
   ```

   *tfBinaryURL* 是 Tensorflow 包的 URL，准确的 tfBinaryURL 值因操作系统和 Python 版本而异，在这里找到和你系统相关的 *tfBinaryURL* 值。例如，你要在 Mac OS X 上安装 Python 2.7 对应的 Tensorflow 版本，在虚拟环境中安装 Tensorflow 就执行下面的命令：

   ```shell
    $ sudo pip3 install --upgrade \
    https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.2.1-py2-none-any.whl 
   ```

   如果以上命令运行失败，参考 [安装问题]()：

### 下一步

安装完成后，验证你的安装是否工作正常。

### 卸载 TensorFlow

如果要卸载 TensorFlow，执行下面的命令：

```shell
$ pip uninstall tensorflow
$ pip3 uninstall tensorflow 
```



## 使用 Docker 安装

按照以下步骤使用 Docker 安装 TensorFlow：

1. 按照 [文档](https://docs.docker.com/engine/installation/#/on-macos-and-windows) 在你的机器上安装 Docker
2. 启动任一个包含 TensorFlow 镜像的 Docker 容器

本节剩下部分解释如何启动 Docker 容器。

要启动包含 TensorFlow 镜像的 Docker 容器，执行以下命令：

```shell
 $ docker run -it -p hostPort:containerPort TensorFlowImage 
```

where:

- *-p hostPort:containerPort* 是可选的，如果你想从 shell 运行 TensorFlow 程序忽略这个选项。如果你想从 Jupyter notebook 运行 TensorFlow 程序，*hostPort* 和 *containerPort* 都设置为 `8888`。如果你想在镜像中运行 TensorBoard，再添加一个`-p` 参数，*hostPort* 和 *containerPort* 都设置为 6006。
- *TensorFlowImage* 是需要的，它用于指定 Docker 容器，你必须指定接下来的任一一个：`gcr.io/tensorflow/tensorflow`: TensorFlow 二进制镜像，`gcr.io/tensorflow/tensorflow:latest-devel`: TensorFlow 二进制镜像加源码。

`gcr.io` 是 Goole 的容器注册表(?)，注意部分 TensorFlow 也可以从 [dockerhub](https://hub.docker.com/r/tensorflow/tensorflow/) 获取。

例如，下面的命令可以在 Docker 容器中启动一个 TensorFlow CPU 镜像，然后你可以在镜像的 shell 中运行 TensorFlow 程序：

```shell
$ docker run -it gcr.io/tensorflow/tensorflow bash
```

以下命令也可以在 Docker 容器中启动一个 TensorFlow CPU 镜像，然而，在这个 Docker 镜像中，你可以在 Jupyter notebook 中运行 TensorFlow 程序：

```shell
$ docker run -it -p 8888:8888 gcr.io/tensorflow/tensorflow
```

Docker 将会先下载 TensorFlow 镜像然后启动它。

### 下一步

现在可以验证你的[安装](https://www.tensorflow.org/install/install_mac#ValidateYourInstallation)了。



## 使用 Anaconda 安装

**Anaconda 安装只是社区而非官方支持**

按照以下步骤在 Anaconda 环境中安装 TensorFlow：

1. 按照 [Anaconda 下载站点](https://www.continuum.io/downloads) 说明下载安装 Anaconda

2. 执行以下命令创建名为 `tensorflow` 的 conda 环境：

   ```shell
   $ conda create -n tensorflow
   ```

3. 执行以下命令激活 conda 环境：

   ```shell
   $ source activate tensorflow
    (tensorflow)$  # Your prompt should change
   ```

4. 执行以下命令在你的 conda 环境中安装 TensorFlow：

   ```shell
   (tensorflow)$ pip install --ignore-installed --upgrade TF_PYTHON_URL
   ```

   *TF_PYTHON_URL* 是 [TensorFlow Python 包](https://www.tensorflow.org/install/install_mac#the_url_of_the_tensorflow_python_package) 的 URL，例如，以下命令是安装 Python 2.7 CPU-only 版本的 TensorFlow：

   ```shell
    (tensorflow)$ pip install --ignore-installed --upgrade \
    https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.2.1-py2-none-any.whl
   ```

   ​

## 验证你的安装

要验证你的 TensorFlow 安装，操作以下步骤：

1. 保证你的环境可以运行 TensorFlow 程序
2. 运行一个小的 TensorFlow 程序

### 准备你的环境

如果你使用本地 pip, virtualenv 或者 Anaconda 安装，操作以下步骤：

1. 打开一个终端
2. 如果你使用 virtualenv 或 Anaconda 安装，激活你的容器
3. 如果你安装了 TensorFlow 源码，进到任何一个处了包含 TensorFlow 源码的目录

如果通过 Docker 安装，启动一个运行 bash 的 Docker 容器，例如：

```shell
$ docker run -it gcr.io/tensorflow/tensorflow bash
```

### 运行一个小的 TensorFlow 程序

在一个 shell 中执行 Python：

```shell
$ python
```

在 python 交互式 shell 中输入以下小程序：

```python
# Python

import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))
```

如果系统输出以下内容，你可以开始写 TensorFlow 程序了：

```
Hello, TensorFlow!
```

如果你不熟悉 TensorFlow，参考 [Getting Started with TensorFlow](https://www.tensorflow.org/get_started/get_started)。

如果系统输出错误信息而不是欢迎语，参考 [常见安装问题]()。



## 常见安装问题

我们依据 Stack Overflow 记录 TensorFlow 安装问题和相应的解决方法。下面的表格包括 Stack Overflow 常见的安装问题回复链接，如果你遇到的错误信息或者其它安装问题不在表格中，请在 Stack Overflow 上搜索。如果 Stack Overflow 上没有你搜索的错误信息，提一个新问题并且打上 `tensorflow` 标签。

| Stack Overflow Link                      | Error Message                            |
| ---------------------------------------- | ---------------------------------------- |
| [42006320](http://stackoverflow.com/q/42006320) | `ImportError: Traceback (most recent call last):File ".../tensorflow/core/framework/graph_pb2.py", line 6, in from google.protobuf import descriptor as _descriptorImportError: cannot import name 'descriptor'` |
| [33623453](https://stackoverflow.com/q/33623453) | `IOError: [Errno 2] No such file or directory:  '/tmp/pip-o6Tpui-build/setup.py'` |
| [35190574](https://stackoverflow.com/questions/35190574) | `SSLError: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify  failed` |
| [42009190](http://stackoverflow.com/q/42009190) | `  Installing collected packages: setuptools, protobuf, wheel, numpy, tensorflow  Found existing installation: setuptools 1.1.6  Uninstalling setuptools-1.1.6:  Exception:  ...  [Errno 1] Operation not permitted:  '/tmp/pip-a1DXRT-uninstall/.../lib/python/_markerlib' ` |
| [33622019](https://stackoverflow.com/q/33622019) | `ImportError: No module named copyreg`   |
| [37810228](http://stackoverflow.com/q/37810228) | During a `pip install` operation, the system returns:`OSError: [Errno 1] Operation not permitted` |
| [33622842](http://stackoverflow.com/q/33622842) | An `import tensorflow` statement triggers an error such as the following:`Traceback (most recent call last):  File "", line 1, in   File "/usr/local/lib/python2.7/site-packages/tensorflow/__init__.py",    line 4, in     from tensorflow.python import *    ...  File "/usr/local/lib/python2.7/site-packages/tensorflow/core/framework/tensor_shape_pb2.py",    line 22, in     serialized_pb=_b('\n,tensorflow/core/framework/tensor_shape.proto\x12\ntensorflow\"d\n\x10TensorShapeProto\x12-\n\x03\x64im\x18\x02      \x03(\x0b\x32      .tensorflow.TensorShapeProto.Dim\x1a!\n\x03\x44im\x12\x0c\n\x04size\x18\x01      \x01(\x03\x12\x0c\n\x04name\x18\x02 \x01(\tb\x06proto3')  TypeError: __init__() got an unexpected keyword argument 'syntax'` |
| [42075397](http://stackoverflow.com/q/42075397) | A `pip install` command triggers the following error:`...You have not agreed to the Xcode license agreements, please run'xcodebuild -license' (for user-level acceptance) or'sudo xcodebuild -license' (for system-wide acceptance) from within aTerminal window to review and agree to the Xcode license agreements....  File "numpy/core/setup.py", line 653, in get_mathlib_info    raise RuntimeError("Broken toolchain: cannot link a simple C program")RuntimeError: Broken toolchain: cannot link a simple C program` |



## TensorFlow Python 包 URL

一些安装方法需要 TensorFlow Python 包的 URL，值与三个方面有关(?)：

- 操作系统
- Python 版本

本节记录了 Mac OS 安装相关的值

### Python 2.7

```
https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.2.1-py2-none-any.whl
```

### Python 3.4, 3.5, or 3.6

```
https://storage.googleapis.com/tensorflow/mac/cpu/tensorflow-1.2.1-py3-none-any.whl

```



## Protobuf pip package 3.1

如果你没有遇到 protobuf pip 包相关的问题可以跳过本节。

**注意：**如果你的 TensorFlow 运行很慢，可能是和 protobuf pip 包有关的问题。

TensorFlow pip 包依赖 protobuf pip 3.1 版本的包，从 PyPI 下载的 protobuf pip 包（在调用 `pip install protobuf` 时）是一个仅包含 Python 的库，其中包含执行速度比 C++ 实现慢10 ～ 50 倍的原始序列化/反序列化的Python 实现。 Protobuf 还支持包含基于快速 C++ 的原语解析的 Python 包的二进制扩展，此扩展在标准的仅Python 专用 pip 包中不可用，我们为 protobuf 创建了一个包含二进制扩展名的自定义二进制 pip 包。要安装自定义二进制 protobuf pip 包，请调用以下命令之一：

- for Python 2.7:

  ```shell
  $ pip install --upgrade \
  https://storage.googleapis.com/tensorflow/mac/cpu/protobuf-3.1.0-cp27-none-macosx_10_11_x86_64.whl
  ```

- for Python 3.n:

  ```shell
  $ pip3 install --upgrade \
  https://storage.googleapis.com/tensorflow/mac/cpu/protobuf-3.1.0-cp35-none-macosx_10_11_x86_64.whl
  ```

安装这些 protobuf 包将会覆盖已安装的包，注意二进制 pip 包已经支持大于 64M 的 protobufs，修复了如下报错：

```shell
[libprotobuf ERROR google/protobuf/src/google/protobuf/io/coded_stream.cc:207]
A protocol message was rejected because it was too big (more than 67108864 bytes).
To increase the limit (or to disable these warnings), see
CodedInputStream::SetTotalBytesLimit() in google/protobuf/io/coded_stream.h.
```



> 原文：https://www.tensorflow.org/install/install_mac
>
> 上次更新日期：六月 30, 2017