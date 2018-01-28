[![Join the chat at https://gitter.im/red/red](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/red/red?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Travis build](https://travis-ci.org/red/red.svg?branch=master)](https://travis-ci.org/red/red)
[![Build status](https://ci.appveyor.com/api/projects/status/mie736c6x4268boo/branch/master?svg=true)](https://ci.appveyor.com/project/red/red/branch/master)

Red 编程语言
Red Programming Language
------------------------

Red 是一个Rebol官方强力推荐的新编程语言，但是由于使用本地代码编译器，系统编程到高级脚本，她的使用更广，同时为并发性和多核cpu进行了支持。
**Red** is a new programming language strongly inspired by [Rebol](http://rebol.com), but with a broader field of usage thanks to its native-code compiler, from system programming to high-level scripting, while providing modern support for concurrency and multi-core CPUs.


Red 有她自己完整的跨平台工具链，有两个编译器，一个解释器和一个连接器，不依赖任何第三方库，除了在引导阶段需要Rebol2的编译器。一旦完成Red将自托管。(http://en.wikipedia.org/wiki/Self-hosting)
Red has its own complete cross-platform toolchain, featuring two compilers, an interpreter and a linker, not depending on any third-party library, except for a Rebol2 interpreter, required during the bootstrap phase. Once complete, Red will be [self-hosted](http://en.wikipedia.org/wiki/Self-hosting).


Red软件栈也包含另一种语言Red/System，这是一种低级的Red方言，她是一种有限的的c级语言，看起来与Red感觉很像，编译Red运行时库需要她，并且是Red编译器的目标语言。更多信息在red-lang官网(http://www.red-lang.org)。
The Red software stack also contains another language, **Red/System**, which is a low-level dialect of Red. It is a limited C-level language with a Red look'n feel, required to build Red's runtime library and be the target language of Red's compiler. More information at [red-lang.org](http://www.red-lang.org).


写一个Red的 HelloWorld。
Making a Red "Hello World"
------------------------

Red的工具链是一个一兆字节的可执行文件，可以从这里下载[这里](http://www.red-lang.org/p/download.html)，用于3大平台。
The Red toolchain comes as a single **one-megabyte** executable file that you can download from [here](http://www.red-lang.org/p/download.html) for the big-3 platforms.

1、把下载的red二进制文件放到工作目录。
1. Put the downloaded **red** binary in the working folder.

2、在代码或文本编辑器中，编写一下Hello World程序：
2. In a code or text editor, write the following Hello World program:

        Red [
            Title: "Simple hello world script"
        ]

        print "Hello World!"

3、保存文件名 hello.red
3. Save it under the name: **hello.red**

4、从命令终端 （也可以从DOS操作它），运行下面语句：
4. From a terminal (works from DOS too), run it with:

        $ red hello.red

5、你将看到 Hello world！输出。
5. You should see the _Hello World!_ output.

6、生成一个编译过的可执行文件：
6. Want to generate a compiled executable from that program?

        $ red -c hello.red
        $ ./hello

7、生成一个没有依赖项的可编译文件：
7. Want to generate a compiled executable from that program with no dependencies?

        $ red -r hello.red
        $ ./hello
8 交叉编译到另一个支持的平台：
8. Want to cross-compile to another supported platform?

        $ red -t Windows hello.red
        $ red -t Darwin hello.red
        $ red -t Linux-ARM hello.red

命令行语法：
**The command-line syntax is:**

    red [command] [options] [file]

`[file]` 任何Red或Red/System源文件。如果没有提供文件和选项参数，则将启动图形化的交互式控制台。如果提供一个没有选项的文件，那么该文件将由解释器运行(它将是一个没有Red/system代码的Red脚本)。
`[file]` any Red or Red/System source file. If no file and no option is provided, the graphical interactive console will be launched. If a file with no option is provided, the file will be simply run by the interpreter (it is expected to be a Red script with no Red/System code).


注意:在非windows平台上，REPL在CLI模式下默认运行。但是在Windows上，默认是在GUI模式下运行。要在命令行模式下运行它，请调用带有选项的Red二进制文件——cli。
Note: On Non-Windows platforms, the REPL runs by default in CLI mode. But on Windows, the default is to run in GUI mode. To run it in the command line mode, invoke the red binary with the option `--cli`.

`[options]`

    -c, --compile                  : Generate an executable in the working
                                     folder, using libRedRT. (developement mode)
                                   ：使用libRedRT在工作文件夹中生成可执行文件。(开发模式)
                                

    -d, --debug, --debug-stabs     : Compile source file in debug mode. STABS
                                     is supported for Linux targets.
                                   ：在调试模式下编译源代码文件。STABS支持Linux目标。

    -dlib, --dynamic-lib           : Generate a shared library from the source
                                     file.
                                   ：从源文件生成一个共享库。

    -h, --help                     : Output this help text.
                                ：输出帮助信息

    -o <file>, --output <file>     : Specify a non-default [path/][name] for
                                     the generated binary file.
                                ：为生成的二进制文件指定一个非默认路径/名称。
                                
    -r, --release                  : Compile in release mode, linking everything
                                     together (default: development mode).
                                ：在发布模式下编译，将所有东西连接在一起(默认:开发模式)。

    -s, --show-expanded            : Output result of Red source code expansion by
                                     the preprocessor.
                                ：由预处理程序输出Red源代码的输出结果。

    -t <ID>, --target <ID>         : Cross-compile to a different platform
                                     target than the current one (see targets
                                     table below).
                                 ：交叉编译到不同的平台目标(参见下面的目标表)。

    -u, --update-libRedRT          : Rebuild libRedRT and compile the input script
                                      (only for Red scripts with R/S code).
                                :重新构建libRedRT并编译输入脚本(只针对带有r/s代码的Red脚本)。

    -v <level>, --verbose <level>  : Set compilation verbosity level, 1-3 for
                                     Red, 4-11 for Red/System.
                                :设置编译级别，Red 为1-3，Red/System 为 4-11。

    -V, --version                  : Output Red's executable version in x.y.z
                                     format.
                                ：输出Red的执行版本。格式：x.y.z

    --config [...]                 : Provides compilation settings as a block
                                     of `name: value` pairs.
                                :提供为编译设置一个程序块，包含 `name: value` 。

    --cli                          : Run the command-line REPL instead of the
                                     graphical console.
                                ：运行命令行REPL，而不是图形控制台。

    --no-runtime                   : Do not include runtime during Red/System
                                     source compilation.
                                ：在编译Red/System源码期间不包含的运行时。

    --red-only                     : Stop just after Red-level compilation.
                                     Use higher verbose level to see compiler
                                     output. (internal debugging purpose)
                                ：在Red层编译之后停止。使用更高的详细级别来查看编译器的输出。(内部调试目的)
                                     

`[command]`

    build libRed [stdcall]         : Builds libRed library and unpacks the 
                                     libRed/ folder locally.
                                     ：编译 libRed 包 并且解包到 本地文件夹 libRed/。 

    clear [<path>]                 : Delete all temporary files from current
                                     or target <path> folder.
                                     ：从当前或目标文件夹中删除所有临时文件。

Cross-compilation targets:
交叉编译的范围：


    MSDOS        : Windows, x86, console (+ GUI) applications
    Windows      : Windows, x86, GUI applications
    WindowsXP    : Windows, x86, GUI applications, no touch API
    Linux        : GNU/Linux, x86
    Linux-ARM    : GNU/Linux, ARMv5, armel (soft-float)
    RPi          : GNU/Linux, ARMv5, armhf (hard-float)
    Darwin       : macOS Intel, console-only applications
    macOS        : macOS Intel, applications bundles
    Syllable     : Syllable OS, x86
    FreeBSD      : FreeBSD, x86
    Android      : Android, ARMv5
    Android-x86  : Android, x86


注意：在$PATH下运行Red二进制工具链 需要包装一个shell文件，（看相关的链接： [#543](https://github.com/red/red/issues/543) and [#1547](https://github.com/red/red/issues/1547)）
_Note_: Running the Red toolchain binary from a $PATH currently requires a wrapping shell script (see relevant tickets: [#543](https://github.com/red/red/issues/543) and [#1547](https://github.com/red/red/issues/1547)).



运行这个Red REPL
Running the Red REPL
-----------------------

1、只需要运行Red二进制文件 不需要任何选项就可以访问REPL
1. Just run the `red` binary with no option to access the [REPL](http://en.wikipedia.org/wiki/Read%E2%80%93eval%E2%80%93print_loop).

        ---== Red 0.6.3 ==-- 
        Type HELP for starting information. 

        >>

1、你能用她快速的测试一些Red代码
1. You can use it to test rapidly some Red code:

        >> 1 + 2
        == 3

        >> inc: func [n][n + 1]
        == func [n][n + 1]

        >> inc 123
        == 124

  
注释:

在windows系统，REPL默认的在GUI模式下运行。要在命令行模式下运行他，请调用 `red --cli`。
Wine是一些关于GUI控制台的问题(https://github.com/red/red/issues/1618)。安装`Consolas`的字体来修复问题。
- On Windows, the REPL runs by default in GUI mode. To run it in the command line, invoke the red binary as `red --cli`.
- Wine has some [issues](https://github.com/red/red/issues/1618) with the GUI-Console. Install the `Consolas` font to fix the problem.

通过源码运行Red（参与者）
Running Red from the sources (for contributors)
------------------------

这个编译器和连接器都是用Rebol语言编写的。请跟随这个指导手册安装编译器工作链，以便运行它的源码。
The compiler and linker are currently written in Rebol. Please follow the instructions for installing the compiler toolchain in order to run it from sources:

1、克隆这个git资源库或者下载压缩包。
1. Clone this git repository or download an archive (`ZIP` button above or from [tagged packages](https://github.com/red/red/tags)).


1、下载一个对应你操作系统的Rebol解释器： [Windows](http://www.rebol.com/downloads/v278/rebol-core-278-3-1.exe), [Linux](http://www.maxvessi.net/rebsite/Linux/) (or [Linux](http://www.rebol.com/downloads/v278/rebol-core-278-4-2.tar.gz)), [Mac OS X](http://www.rebol.com/downloads/v278/rebol-core-278-2-5.tar.gz), [FreeBSD](http://www.rebol.com/downloads/v278/rebol-core-278-7-2.tar.gz), [OpenBSD](http://www.rebol.com/downloads/v278/rebol-core-278-9-4.tar.gz), [Solaris](http://www.rebol.com/downloads/v276/rebol-core-276-10-1.gz).
1. Download a Rebol interpreter suitable for your OS: [Windows](http://www.rebol.com/downloads/v278/rebol-core-278-3-1.exe), [Linux](http://www.maxvessi.net/rebsite/Linux/) (or [Linux](http://www.rebol.com/downloads/v278/rebol-core-278-4-2.tar.gz)), [Mac OS X](http://www.rebol.com/downloads/v278/rebol-core-278-2-5.tar.gz), [FreeBSD](http://www.rebol.com/downloads/v278/rebol-core-278-7-2.tar.gz), [OpenBSD](http://www.rebol.com/downloads/v278/rebol-core-278-9-4.tar.gz), [Solaris](http://www.rebol.com/downloads/v276/rebol-core-276-10-1.gz).

1、提取rebol二进制包，把它放到根目录里！
1. Extract the `rebol` binary, put it in root folder, that's all!

1、让我们测试它：运行`./rebol` ，你将看到一个 `>>` 提示出现。windows用户需要双击 rebol.exe 文件运行它 。
1. Let's test it: run `./rebol`, you'll see a `>>` prompt appear. Windows users need to double-click on the `rebol.exe` file to run it.

Rebol控制台： 
1. From the REBOL console type:

        >> do/args %red.r "%tests/hello.red"

编译过程完成应该有一个信息 `...output file size`，结果文件是在工作目录下。windows用户需要打开dos控制台并运行 `hello.exe` 命令
The compilation process should finish with a `...output file size` message. The resulting binary is in the working folder. Windows users need to open a DOS console and run `hello.exe` from there.


要查看Red/System编译的代码，使用如下命令：
To see the intermediary Red/System code generated by the compiler, use:

        >> do/args %red.r "-v 2 %tests/hello.red"

你也能从源码编译Red的控制台：
You can also compile the Red console from source:

        >> do/args %red.r "-r %environment/console/console.red"

通过源码编译windowsGUI控制台：
To compile the Windows GUI console from source:

        >> do/args %red.r "-r -t Windows %environment/console/gui-console.red"


注意： 当从源码启动Red工具链的时候，这个 `-c` 参数不是必须的，因为默认是编译输入脚步（二进制工具链默认事件是去通过解释器去运行输入脚本 ）
Note: the `-c` argument is not necessary when launching the Red toolchain from sources, as the default action is to compile the input script (the toolchain in binary form default action is to run the input script through the interpreter).

在编译Red控制台需要添加到运行时可用功能，需要使用-r参数。
The `-r` argument is needed when compiling the Red console to make additional runtime functions available.

贡献
Contributing
-------------------------

如果你想贡献代码到Red工程，一定先读这个指南文档[guidelines](https://github.com/red/red/wiki/Contributor-Guidelines)。
If you want to contribute code to the Red project be sure to read the [guidelines](https://github.com/red/red/wiki/Contributor-Guidelines) first.


如果你还有一个好的主义并且没有人做过同样的事情 请给提给Red组，你可以通过邮件列表联系我们[mailing-list](https://groups.google.com/forum/?hl=en#!forum/red-lang)，或者聊天室[chat room](https://gitter.im/red/red).
It is usually a good idea to inform the Red team about what changes you are going to make in order to ensure that someone is not already working on the same thing. You can reach us through the [mailing-list](https://groups.google.com/forum/?hl=en#!forum/red-lang) or our [chat room](https://gitter.im/red/red).


你修改了一个问题，并有一个满意的解决方案想要提交到Github上？
Satisfied with the results of your change and want to issue a pull request on Github?


确保这些更改通过了所有现有的测试，在测试套件中添加相关测试，并尽可能多地测试这些测试。您可以使用(从Rebol控制台，在存储库根中)运行所有的测试:
Make sure the changes pass all the existing tests, add relevant tests to the test-suite and please test on as many platforms as you can. You can run all the tests using (from Rebol console, at repository root):

        >> do %run-all.r

关于防病毒软件误报
Anti-virus false positive
-------------------------
一些防病毒程序太过于敏感，会错误地报告警报在一些Red生成的二进制文件，如果你遇到了 请发消息到这里，我们能报告这个误报。
Some anti-virus programs are a bit too sensitive and can wrongly report an alert on some binaries generated by Red, if that happens to you, please fill a ticket [here](https://github.com/red/red/issues), so we can report the false positive.


许可证
License
-------------------------
Red 和 Red/System 两个语言是发布在BSD(http://www.opensource.org/licenses/bsd-3-clause)许可下，运行时在BSL(http://www.boost.org/users/license.html)许可下发布。BSL比BSD更宽松，更适合于运行时部分。
Both Red and Red/System are published under [BSD](http://www.opensource.org/licenses/bsd-3-clause) license, runtime is under [BSL](http://www.boost.org/users/license.html) license. BSL is a bit more permissive license than BSD, more suitable for the runtime parts.
