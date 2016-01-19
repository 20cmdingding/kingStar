/**
 *@文件  ：Readme_ksmarketdata.txt  测试行情API的源代码说明文件
 *@作者  : xdhu
 *@系统名：API测试程序
 *@公司名：胜科金仕达
 *@修改历史：
    20121203  创建
 */
一、文件说明：
KSMarketDataAPI_Sample文件夹包含如下文件：
源文件   MdUserApi_Sample.cpp
linux环境makefile文件   makefile
windows环境vc项目文件   MdUserApi_Sample.cpp.sln，MdUserApi_Sample.cpp.vcproj
帮助文件		Readme_ksmarketdata.txt, Readme_ksmarketdata_en.txt

二、文件功能：
MdUserApi_Sample.cpp  			                        主要实现测试libksmarketdataapi.so动态库的基本功能
makefile 			    				主要实现在linux平台下，测试可执行程序的编译。
MdUserApi_Sample.cpp.sln，MdUserApi_Sample.cpp.vcproj	        主要实现在windows平台下，测试可执行程序的编译。

三、linux平台编译、运行说明

1，编译说明
   makefile提供32位测试程序和64位测试程序的编译。

   1）  编译检查
	首先确保本机器安装了gcc 4.1.2及其以上版本
	在linux的shell命令行下 运行 gcc -v 可以查看gcc的版本信息
	低版本的gcc可能导致编译错误。
   
   2）  如何编译
	在linux的 shell命令行下运行make命令。
	make   		生成64位测试程序（默认）
	make  vtype=32r 生成32位测试程序。
        make  vtype=64r 生成64位测试程序。

   3）  生成目标
	make 或 make vtype=64r 将在 KSMarketDataAPI_Sample 目录下，生成 MdUserApi_Sample可执行文件，用于64位测试程序。
        make vtype=32r         将在 KSMarketDataAPI_Sample 目录下，生成 MdUserApi_Sample可执行文件，用于32位测试程序。
	
   4）  注意事项
	在当前环境，编译32位和64位程序时，执行一次make命令后，需要执行 make clean ,删除上次编译的中间目标文件，
	以防止编译64位程序引用32位的中间目标文件或编译32位程序引用了64位的中间目标文件，导致编译出错。

2，运行说明
   
   1）运行检查
      测试代码的运行，需要确保动态库libksmarketdataapi.so,libkslkc64r.so(32位则是libkslkc32r.so)文件的存在。（发布物包括32位和64位的libksmarketdataapi.so，文件名相同，分别在sdk/linux/linux32/和   sdk/linux/linux64目录下。而libkslkc32r.so在sdk/linux/linux32/目录下，libkslkc64r.so在sdk/linux/linux64/目录下）
      检查是否已经成功编译出测试程序的可执行文件（ 编译阶段将在run目录下生成相应的可执行程序）。

   2) 动态库文件可执行属性设置
      
      确保动态库 libksmarketdataapi.so具有可执行属性。可以通过ls -l libksmarketdataapi.so查看文件的属性。
      确保动态库 libkslkc64r.so（或libkslc32r.so）具有可执行属性。可以通过ls -l libkslkc64r.so （libkslkc32r.so）来查看文件属性。
      若动态库不具备可执行属性，可以在linux shell命令行下，通过 chmod +x libksmarketdataapi.so来实现。 具体命令参考 man 1 chmod

   3）设置动态库加载路径
      假设libksmarketdataapi.so的绝对路径为/xxx/yyy/zzz/libksmarketdataapi.so。有如下方式设置动态库加在路径，可以参考man 3 dlopen

      	 可以将libksmarketdataapi.so,libkslkc64r.so(或libkslkc32r.so）的所在目录路径，添加到LD_LIBRARY_PATH环境变量中。
	 LD_LIBRARY_PATH=/xxx/yyy/zzz/：${LD_LIBRARY_PATH};  export LD_LIBRARY_PATH

   4) 检查环境配置的正确性
      a)检查可执行程序对动态库的设置加载是否正确
	ldd  MdUserApi_Sample   检查测试程序对动态库的加载
      b)查看当前的动态库的版本信息
	strings libksmarketdataapi.so|grep KSFT_API_Version
   5）注意事项
      程序的正确运行，还需要获得金仕达的授权文件KSInterB2C.lkc, 确保在可执行文件所在目录存在KSInterB2C.lkc文件，具体可联系热线获取授权文件。


三、Windows平台编译、运行说明

1，编译说明
   主要通过Visual Studio 2005 IDE环境来配置编译。

   1) 编译检查
   首先确保本机器安装了Visual Studio 2005及以上版本。
   
   2）如何编译
   通过vs打开MdUserApi_Sample.cpp.sln文件，编译即可。
   
   3）生成目标
   在KSMarketDataAPI_Sample目录下生成MdUserApi_Sample.exe可执行文件。

2，运行说明
   确保KSMarketDataAPI_Sample目录下有KSMarketDataAPI.dll,cpack.dll,lkcdll.dll
   在KSMarketDataAPI_Sample目录下执行MdUserApi_Sample.exe即可。
   同样正确运行需要获取授权文件KSInterB2C.lkc，确保在可执行文件所在目录存在KSInterB2C.lkc
      