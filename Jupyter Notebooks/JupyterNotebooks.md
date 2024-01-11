# Jupyter Notbook

Jupyter Notebook是一款开源代码的web应用程序，可让我们创建并共享代码和文档  
它提供了一个环境，可以在其中记录代码，运行代码，查看结果，可视化数据并查看输出结果  

用于数据清理，统计建模，构建和训练机器学习模型，可视化数据以及许多用途  

## 初始化设置  

1. 安装  

```{bash}
# conda 安装
conda install -c conda-forge jupyter

# pip 安装 
pip3 install jupyter
```

2. 启动  

默认端口号是8888， 网址输入<https://localhost:8888>  

```{bash}
jupyter notebook
```

3. 修改配置  

在 .jupyternb 文件夹下创建 jupyter_notebook_config.py 文件  

```text
# 访问ip
c.NotebookApp.ip='172.16.50.206' 

#指定端口
c.NotebookApp.port=8888

# 是否打开浏览器
c.NotebookApp.open_browser = False

# 输入密码，要使用jupyter生成密钥
c.NotebookApp.token = ''
```

## 启动使用

1. 多项功能
在打开新的jupyter notebook中，页面右侧的new，会有Python3， text file, Folder, Terminal选项  

2. 多项内核  

jupyter可以安装python内核，使用python  
jupyter可以安装R内核，使用R <https://github.com/IRkernel/IRkernel>  
jupyter可以安装Julia内核，使用Julia <https://github.com/JuliaLang/IJulia.jl>  

3. 交互式命令  

**键盘的快捷键**  

Jupyter Notebook提供了两种不同的键盘输入模式--命令和编辑。命令模式将键盘与notebook的命令绑定，并由蓝色左边距的带有灰色单元格边框来表示。编辑模式允许你将文本输入活动单元格  

按Esc和Enter键可以切换到命令模式和编辑模式  

在命令行模式下：  

- A键将在选中单元格上方插入新单元格；B在选中单元格下方插入一个单元格  
- dd是删除一个单元格  
- z是撤销  
- Shift+ 上下键选择多个单元格，Shift+M是合并选中的多个单元格  
- F是查找替换  

在编辑模式下：  

- 按Ctrl+Enter运行选中的单元格  
- 按Shift+Enter运行选中的单元格，并进入命令模式  
- 按Alt+Enter运行选中的单元格，并在下方插入一个新单元格  

## Jupyter Notebook 拓展  

Nbextensions 是最好用的拓展之一  

```{bash}
# pip 安装
pip install jupyter_contrib_nbextensions

# 安装关联的JavaScript和CSS
jupyter contrib nbextension install --user  

```

安装完成后在Jupyter Notebook顶部能看到Nbextensions选项卡  

1. Code prettify  

重新规范代码的格式，优化代码的内容  

2. Printview  

打印预览  

3. Scratchpad  

Adds a scratchpad cell to Jupyter notebook. 在不notebook下，相当于测试代码过程中使用一个草稿本来展示结果  

4. Table of Contents  

收集Notebook中所有的标题，并展示在一个浮动窗口中  

## Jupyter Lab  

下一代的Jupyter Notebook，可视化非常的强  

操作感也强，插件也能用  