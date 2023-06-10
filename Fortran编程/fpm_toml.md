fpm.toml
fpm.toml 是一个用 TOML 格式编写的文件，它包含了你的 fpm 项目的元数据和配置信息。  fpm.toml 文件必须放在你的项目根目录下，它由以下几个部分组成：

●*ame*: 项目的名称，必须指定
●*ersion*: 项目的版本号，可以是字符串或者一个包含版本号的文件名
●*icense*: 项目的许可证，可以使用 SPDX 标识符
●*aintainer*: 项目的维护者，可以是邮箱或者其他联系方式
●*uthor*: 项目的作者
●*opyright*: 项目的版权声明
●*escription*: 项目的简介，应该是纯文本，不含格式标记
●*ategories*: 项目的类别，可以是多个
●*eywords*: 项目的关键词，可以是多个
●*omepage*: 项目的主页

●*build]*: 构建配置，可以指定以下选项：
    - auto-tests : 是否自动发现测试可执行文件，默认为 true
    - auto-examples : 是否自动发现示例程序，默认为 true
    - auto-executables : 是否自动发现可执行文件，默认为 true
    - link : 链接外部依赖，默认为空
    - external-modules : 指定使用的外部模块，默认为空
    - profile : 指定编译器配置文件，默认为空

●*[profiles]*: 编译器配置文件，可以指定以下选项：
    - compiler : 编译器名称，默认为 gfortran
    - flags : 编译器标志，默认为空

●*[library]*: 库目标配置，可以指定以下选项：
    - source-dir : 库源文件所在目录，默认为 src
    - source-files : 库源文件列表，默认为空

●*[executable]]*: 可执行目标配置，可以指定以下选项：
    - name : 可执行文件名称，默认为项目名称
    - source-dir : 可执行文件源文件所在目录，默认为 app
    - source-file: 可执行文件源文件名称，默认为 main.f90

●*[test]]*: 测试目标配置，可以指定以下选项：
    - name : 测试名称，默认为 test_1, test_2, ...
    - source-dir : 测试源文件所在目录，默认为 test
    - source-file: 测试源文件名称，默认为空

●*[dependencies]*: 项目库依赖，可以指定以下选项：
    - name : 依赖库名称，必须指定
    - version: 依赖库版本号，默认为 *
    - git: 依赖库的 git 地址，默认为空

●*[dev-dependencies]*: 仅用于测试的依赖，选项同上

●*[install]*: 安装配置，可以指定以下选项：
    - [library: 是否安装库目标，默认为 false

●*[preprocess]*: 预处理配置，可以指定以下选项：
    - include-dir: 预处理器包含目录列表，默认为空
    - file-extension: 需要预处理的文件后缀列表，默认为空
    - definitions: 预处理器宏定义列表，默认为空

更多关于 fpm.toml 的用法和示例，请参考 fpm 的文档 。

: https://fpm.fortran-lang.org/en/index.html
: https://fpm.fortran-lang.org/en/spec/manifest.html

