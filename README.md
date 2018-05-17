# CAIL2018

该项目为 **CAIL2018** 的代码和模型提交说明。

## 提交的文件格式及组织形式

你可以在 ``python_sample`` 中找到最简单的提交代码的格式。你需要将你所有的代码压缩为一个 ``zip`` 文件进行提交，该 ``zip`` 文件内部形式可以参看 ``python_smaple/predictor.zip``。该 ``zip`` 文件内部顶层应该只包含一个叫做 ``predictor`` 的文件夹，在该文件夹下需要有你的所有代码、模型及其他相关的东西。

在压缩包内的 ``predictor`` 文件夹内，你需要保证 ``__init__.py`` 和 ``predictor.py`` 这两个文件一定存在。这两个文件的内容我们将在下文提及。

## 代码的内容

你需要保证 ``__init__.py`` 在文件夹 ``predictor`` 内存在并且内容为：

```from .predictor import Predictor```

你需要保证 ``predictor.py`` 在文件夹 ``predictor`` 内存在，并且其中实现了 ``Predictor`` 这个类。``Predictor`` 类需要实现如下几个函数：

* ``__init__``：你需要在该函数类中完成你模型的各种初始化，并且为该类声明变量 ``batch_size``，该变量代表评测器每次需要给你多少个数据同时进行预测。``batch_size`` 需要是一个大于等于 $1$ 小于等于 $128$ 的整数，如果该参数对你来说没有意义，请直接使用 ``self.batch_size=1`` 将该变量设为 $1$。
* ``predict(content)``：在该函数内你需要实现自动判决的预测。参数 ``content`` 为一个长度**不超过** ``batch_size`` 的数组，其中每个元素为一个字符串，对应下载的数据中的事实即 ``fact`` 字段，你需要对每一个数组中的元素进行预测，并返回预测的结果 ``result``。``result``的类型应该为数组，且其元素个数应与 ``content`` 的元素个数相同，并且 ``result`` 中预测的结果顺序应与 ``content`` 中的事实顺序相同。对于每个预测结果，其类型应为 ``dict`` 类型，且包含以下字段：
    * ``accusation``：该字段的类型为一个数组，数组中包含若干个整数，代表预测相关罪名的结果。如 $[1,2,3]$ 表示和第 $1,2,3$ 条罪名都相关，罪名的编号与下发的 ``accu.txt`` 中的顺序一致，从 $1$ 开始编号。
    * ``articles``：该字段的类型为一个数组，数组中包含若干个整数，代表预测相关法条的结果。如 $[1,2,3]$ 表示和第 $1,2,3$ 条法条都相关，法条的编号与下发的 ``law.txt`` 中的顺序一致，从 $1$ 开始编号。**注意**这里的数字并不是代表你预测的结果为法条的第几条，你预测的结果为 $1$ 代表的是 ``law.txt`` 中的第一条法条。
    * ``imprisonment``：该字段类型为一个整数，代表预测的刑期，单位为月。如果预测结果为无期徒刑，请将该字段的值设为 $-1$；如果预测结果为死刑，请将该字段的值设为 $-2$。

以上为 ``predictor.py`` 中你需要实现的内容，你可以利用 ``python_example/predictor`` 下的文件进行进一步参考。

## 其他语言的支持

如上文所述，我们现阶段只支持 ``python`` 语言的提交，但是这并不代表你不能够使用其他语言进行预测。我们在 ``c++_sample/predictor`` 下提供了一种可能的 ``c++`` 的实现方法。我们现在仍然需要实现上文所述的 ``predictor.py`` 的各种接口，但是我们在预测的时候利用 ``os.system`` 调用系统命令运行你编译好的可执行文件，或者其他运行你代码的命令。如果你担心可执行文件没有权限，可以像给出的例子在初始化的过程中加上权限。

## 现有的系统环境

* python3.5.2
* tensorflow 1.7
* pytorch 0.3.1
* gensim 3.4
* sklearn 0.19.1
* scipy 1.1
* numpy 1.14.3
* java 1.8.0_171

等待补全中

如果你有需要的环境，请联系比赛管理员进行安装。
        







