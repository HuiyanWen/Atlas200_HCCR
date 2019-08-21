# Atlas200_HCCR
<br>华为智能硬件生态项目，基于Atlas200开发，实现手写汉字、文本行识别等功能，如图作为示例项目供后续开发者学习，2019年年底结题。项目进行中，持续更新。</br>

![Example image2](https://github.com/HuiyanWen/Atlas200_HCCR/blob/master/1.png)  

<h3>MicroSoft Caffe环境配置</h3>
<br>1.	升级操作系统到server 2019，内核实际为win10</br>
<br>2.	安装vs 2019，vs2013，最后使用的是vs2013</br>
<br>3.	安装cuda10.1，最后使用的是cuda8</br>
4.	下载caffe包。从Microsoft官方Github上下载Caffe的源码压缩包https://github.com/Microsoft/caffe
5.	修改CommonSettings.props，把cuda、cudnn路径补充上，matlab和python都不支持
6.	在caffe-master|windows下打开Caffe.sln，设置libcaffe为启动项目
7.	设置工程为release类型，否则后面会提示无python的debug库，e.g. python35_d.dll
8.	OpenCV找不到动态库：\\private\coapp.NuGetNativeMSBuildTasks.dll未能加载任务“NuGetPackageOverlay”。在在路径NugetPackages/OpenCV.2.4.1x/build/native/中找到OpenCV.props第五行，去掉反斜杠
9.	在项目属性设置的c/c++页面，关闭视警告为错误(即设置为No)如果不设置的话,在编译boost库的时候会由于文字编码的警告而报错
10.	glog依赖glag动态库出错：glog.targets error MSB4062: 未能从程序集 …\gflags.2.1.2.1\...\coapp.NuGetNativeMSBuildTasks.dll 加载任务“NuGetPackageOverlay”。可以在管理NuGet程序包中删除glog，在重装解决
11.	缺少python35.lib库错误，可以通过安装python35并把路径加到工程解决
12.	缺少python27.lib库错误，可以通过安装python27并把路径加到工程解决
13.	一开始尝试使用了vs2019和vs2017和cuda10.1，当时没成功，所以后来的尝试全部转到vs2013+cuda8.0，其实也是一样出错，后来逐一解决后能够正常编译了，但没有重新再vs2019+cuda10.1等配置上尝
14. 无法打开libcaffe.lib是因为编译未成功，可忽略此问题，解决其他error
15. 若error提示缺失依赖包，且与glog或gflags相关，可注释掉错误所在代码解决
16.	下载mnist数据集：http://yann.lecun.com/exdb/mnist/得到四个文件
17.	在caffe-windows安装的根目录下，新建一个mnist_data_convert.bat文件，用来将原始的mnist数据转换成caffe能读入的lmdb格式，并在文件中添加以下命令:
caffe-master\Build\x64\Release\convert_mnist_data --backend=lmdb minist_data/train-images.idx3-ubyte minist_data/train-labels.idx1-ubyte minist_data/mnist_train_lmdb
caffe-master\Build\x64\Release\convert_mnist_data --backend=lmdb minist_data/t10k-images.idx3-ubyte minist_data/t10k-labels.idx1-ubyte minist_data/mnist_test_lmdb
Pause
18.	在caffe-windows根目录下新建一个mnist_test_run.bat.bat文件，在文件中添加：
caffe-master\Build\x64\Release\caffe.exe  train --solver=caffe-master\examples\mnist\lenet_solver_adam.prototxt
pause  
19.	保存并双击运行，caffe开始用mnist数据集训练lenet网络。表明Caffe框架安装成功！！！
I0814 15:48:54.821549 16076 sgd_solver.cpp:273] Snapshotting solver state to binary proto file caffe-master/examples/mnist/lenet_iter_10000.solverstate
I0814 15:48:54.852798 16076 solver.cpp:317] Iteration 10000, loss = 0.00243393
I0814 15:48:54.852798 16076 solver.cpp:337] Iteration 10000, Testing net (#0)
I0814 15:48:55.087173 16076 solver.cpp:404]     Test net output #0: accuracy = 0.9882
I0814 15:48:55.087173 16076 solver.cpp:404]     Test net output #1: loss = 0.0641316 (* 1 = 0.0641316 loss)
I0814 15:48:55.087173 16076 solver.cpp:322] Optimization Done.
I0814 15:48:55.087173 16076 caffe.cpp:255] Optimization Done.
