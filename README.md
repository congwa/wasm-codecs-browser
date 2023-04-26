# wasm-codecs-browser
in browser.WebAssembly codecs for mozjpeg, oxipng, gifsicle and webp。

本包包含编译成 WebAssembly 的不同代码，因此它们可以安装在任何系统上并且不需要本地二进制文件，包括浏览器。

经过我发现市面上所有的类似工具，都是基于 [Squoosh](https://github.com/GoogleChromeLabs/squoosh) 团队所做的工作。

接下来授人之渔， 如果对你**有帮助，请给我star**

## 在服务器环境中

一共有两种方式，

### 编译可执行包，在服务器上使用

以mozjpeg为例子

在mozjpeg官方开源库编译成各个操作系统可以使用的开源包，然后使用exec进行运行[这里也有示例](https://github.com/imagemin/mozjpeg-bin/tree/main)

[mozjpeg编译可执行文件示例](https://github.com/imagemin/mozjpeg-bin/blob/main/lib/install.js),其它的库的在这个作者这里也能找的到

[mozjpeg各个参数的使用](https://github.com/imagemin/imagemin-mozjpeg/blob/main/index.js),其它的库的参数的使用在这里也能找的到

### 编译成wasm，在服务器上使用

wasm给了前端、后端无限的想象力，wasm作为胶水语言再配合wasm runtime可以任意可达。曾经读过一个项目通过使用ffpemg在浏览器进行视频帧拆解，然后浏览器剪辑，之后合成一个新视频的web项目。现在应该在github上一搜有很多的类似项目了。

编译wasm以mozjpeg为例
> 使用emscripten/emsdk进行编译成wasm

以mozjpeg为例子,本仓库中有mozjpeg的wasm包，可以直接拿来使用

也可以在node上[直接安装使用的包](https://github.com/cyrilwanner/wasm-codecs),这个作者给出了已经弄好的npm包

node上编译参数是啥？不想读文档可以看这里，有现成的

[编译成node直接可用的wasm参数配置示例](https://github.com/cyrilwanner/wasm-codecs/blob/master/packages/mozjpeg/build.sh)

#### 如果官方更新了新特性，如何**自己编译**  --不懂参数的情况下

别怕，我这里同样帮你找到了方案。

[mozjpeg使用emscripten/emsdk编译wasm参数](/mozjpeg/Makefile)，其它库同理

如果是rust，你会发现，[使用wasm-pack就可以了](/oxipng/build.sh),不得不说，rust是一个好语言，永远不会有内存泄漏问题导致它写啥用户用的都放心，唯一缺点就是开发慢，语法难。

其中enc是编码器
其中dec是解码器

这里会发现编译wasm使用了一个[cpp文件](/mozjpeg/enc/mozjpeg_enc.cpp),这里感谢谷歌大佬进行编写。

#### 如果我这门服务端语言不能直接运行wasm

没关系，现在有很多wasm的runtime运行时，这里以[wasmer](https://github.com/wasmerio/wasmer)为参考，点击即可传送过去，wasmer同时维护了一个wasm文件仓库，你也可以作为wasm的开发者进行上传的wasm，以供其他人直接可用。

## 在浏览器中使用

我相信能看到本项目的一定是有阅读代码的能力的，而且，在前端有一定开发经验和对wasm有一定了解的开发者，这里给出几个示例
- [squoosh开源项目的使用-17行encode跟着代码追即可](https://github.com/GoogleChromeLabs/squoosh/blob/dev/src/features/encoders/mozJPEG/client/index.tsx)
- [一个大佬的nextjs项目中的使用，我这里提供一个测试用例，源码包里有具体使用](https://github.com/coolweb131/next.js-template/blob/84e6c9ec5b3e7f654c7f868dfb6837e7072efbe8/packages/next/next-server/server/lib/squoosh/main.ts#L64)
    > 项目中也有具体的参数的使用，能直接通过点击看到每个参数的效果
- [基于wasm在浏览器imagestool工具](https://github.com/renzhezhilu/webp2jpg-online-demo)
    > 这是社区内某个大佬基于以上分享实现的前端压缩网页工具，代码结构非常简单，功能不多，很容易理解。

### 浏览器直接兼容

本来想着自己集成一下的，结果逛了逛发现已经有人集成好了npm包，这里我就不做了，列出来

[已经发布到npm直接可用的前端开发包](https://github.com/jamsinclair/jSquash)，源码非常简单，就是集成的谷歌团队的


## 我自己基于以上经验实现的库

### 使用编译可执行包，在服务器上使用

- [image-lossless-compressor](https://github.com/congwa/image-lossless-compressor)-node.js上使用
- [imageCompressor](https://github.com/congwa/imageCompressor)-go语言上使用

## 最后

如果您想了解更多，请来我的[博客](https://github.com/congwa/Front-end-Basics-Notes)

如果本文对你有帮助或者启发，或者给您节省了时间，**请给我star**

