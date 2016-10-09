---
title: DOL 
tags: dol框架简述，dol的安装，实验感想
grammar_cjkRuby: true
---
## 实验一 ——DOL环境配置
***
### DOL 框架描述
	Distributed operation layer (DOL) is a software development framework to program parallel applications. The DOL allows to specify applications based on the Kahn process network model of computation and features a simulation engine based on SystemC. Moreover, the DOL provides an XML-based specification format to describe the implementation of a parallel application on a multi-processor systems, including binding and mapping.



### DOL的安装
这里我是在之前已经安装了Ubuntu的基础上对dol的安装
#### 首先先安装一些必要的环境(执行下面的命令)：
		$	sudo apt-get update
		$	sudo apt-get install ant
		$ 	sudo apt-get install openjdk-7-jdk
		$	sudo apt-get install unzip
#### 解压文件：
		将相关的压缩包上传到虚拟机上
		1.新建dol的文件夹 
			$	mkdir dol
		2.将dolethz.zip解压到 dol文件夹中
			$	unzip dol_ethz.zip -d dol
		3.解压systemc
			$	tar -zxvf systemc-2.3.1.tgz
#### 编译systemc
		1.解压后进入systemc-2.3.1的目录下
			$	cd systemc-2.3.1
		2.新建一个临时文件夹objdir
			$	mkdir objdir
		3.进入该文件夹objdir
			$	cd objdir
		4.运行configure(能根据系统的环境设置一下参数，用于编译)
			$	../configure CXX=g++ --disable-async-updates
		5.编译
			$	sudo make install
		6.编译完后文件目录如下($ cd ..        $ ls)命令，能看到include, lib-linux64(对于32位系统，这里是lib-linux)
		记录当前的工作路径(会输出当前所在路径，记下来，待会有用)
			$	pwd
#### 编译dol
		1.进入刚刚dol的文件夹
			$	cd ../dol
		2.修改build_zip.xml文件
			找到下面这段话，就是说上面编译的systemc位置在哪里，
			<property name="systemc.inc" value="YYY/include"/>
			<property name="systemc.lib" value="YYY/lib-linux/libsystemc.a"/>
			把YYY改成上页pwd的结果（注意，对于  64位 系统的机器，lib-linux要改成lib-linux64）
		3.然后是编译
			$	ant -f build_zip.xml all
			若成功会显示build successful
#### 运行例子（检测是否安装成功）
		1.接着可以试试运行第一个例子（检测是否安装成功）
		进入build/bin/mian路径下
			$	cd build/bin/main
		2.然后运行第一个例子
			$	ant -f runexample.xml -Dnumber=1

### 实验感想
	上次的实验Dol的安装按照TA大大给出的PPT来装还是比较简单的，主要是在修改build_zip文件时，要注意是否有写错，因为在这里浪费了很久时间。还有就是前面配置环境的时候要把需要的环境配置好（如javac等等）。
