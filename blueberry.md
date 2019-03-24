
# mac 下使用排坑:

### 使用configure & make

可能会出错说是 bison 版本过低的情况，使用 `brew install bison`解决，但是还是会说版本过低，以为mac自带的有bison，并且无权限更改；
解决：在bash_profile 中将自己安装的bison设置到path之前：  export PATH="/usr/local/opt/bison/bin:$PATH"
 设置LDFLAGS 环境变量 使用-L添加bisonlib的目录 


后续可能还会出错说是找不到 openssl 中的头文件；
同理：设置CPPFLAGS 环境变量，使用-I添加头文件目录


### cmake 构建

需要安装 boost; `brew install boost`
boost 依赖icu4c,同样，由于系统已经有了，需要在bash_profile设置 
export PATH="/usr/local/opt/icu4c/bin:$PATH"
export PATH="/usr/local/opt/icu4c/sbin:$PATH"

 需要安装 openssl 、 libevent 、zlib等

在根目录CMakeLists.txt 中添加宏，设置这些库的root目录

后续cmake . & make 过程中发现有些地方(test project)报找不到 openssl 或 boost 头文件等。手动使用 include_directories(SYSTEM,"目录"）解决；

具体参考这个分支的代码提交
