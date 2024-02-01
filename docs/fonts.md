---
title: Fonts 字体
tags: #fonts #字体
---


# 字体格式

## TTF
TTF (TrueType Font) 字体格式是由苹果和微软为 PostScript 而开发的字体格式。在 Mac 和 Windows 操作系统上，TTF 一直是最常见的格式，所有主流浏览器都支持它。然而，IE8 不支持 TTF；且 IE9 上只有被设置成 "installable" 才能支持（译注：别想了，转别的格式吧）。

TTF 允许嵌入最基本的数字版权管理标志————内置标志可以告诉我们字体作者是否允许改字体在 PDF 或者网站等处使用，所以可能会有版权问题。另一个缺点是，TTF 和 OTF 字体是没压缩的，因此他们文件更大。

## TTC
TTC字体是TrueType字体集成文件(. TTC文件)，是在一单独文件结构中包含多种字体,以便更有效地共享轮廓数据,当多种字体共享同一笔画时,TTC技术可有效地减小字体文件的大小。

TTC是几个TTF合成的字库，安装后字体列表中会看到两个以上的字体。两个字体中大部分字都一样时，可以将两种字体做成一个TTC文件，常见的TTC字体，因为共享笔划数据，所以大多这个集合中的字体区别只是字符宽度不一样，以便适应不同的版面排版要求。

## OTF
OTF (OpenType Font) 由 TTF 演化而来，是 Adobe 和微软共同努力的结果。OTF 字体包含一部分屏幕和打印机字体数据。OTF 有几个独家功能，包括支持多平台和扩展字符集。OTF 字体可以在 Macintosh 和 Windows 系统上使用。

OTF 也允许多达 65000 个字符的存储。这个额外的空间让设计师可以自由地添加附加元素，比如小帽子、老式数字体、代替的字符和其他一些以前必须作为独立字体分发的附加材料。
（译注：苹果当年为了对抗 Adobe 在 PostScript 的 Type 1 字体拉上了微软一起撸了 TTF，结果后来微软又反水跟 Adobe 搞一套 OTF，还让 IE 后面的版本取消 TTF 支持，IT圈子还真是乱。。）

## OTC
OTC是OTF的合集

## EOF
EOT (Embedded Open Type) 字体是微软设计用来在 Web 上使用的字体。是一个在网页上试图绕过 TTF 和 OTF 版权的方案。你可以使用微软的工具从现有的 TTF/OTF 字体转成 EOT 字体使用，其中对字体进行压缩和裁剪使得文件体积更小。同时为了避免一些收版权保护的字体被随意复制，EOT 还集成了一些特性来阻止复制行为，以及对字体文件进行加密保护。听起来很有前途？嗯哼，可惜 EOT 格式只有 IE 支持。

（译注：微软曾经弄死网景的恶意竞争引起了公愤，在 IE 上推行孤立主义的微软遭到整个行业的唾弃）

## WOFF
WOFF (Web Open Font Format) 本质上是 metadata + 基于 SFNT 的字体（如 TTF、OTF 或其他开放字体格式）。该格式完全是为了 Web 而创建，由 Mozilla 基金会、微软和 Opera 软件公司合作推出。 WOFF 字体均经过 WOFF 的编码工具压缩，文件大小一般比 TTF 小 40%，加载速度更快，可以更好的嵌入网页中。metadata 允许在字体文件中包含许可数据，以解决版权问题。这是万维网联盟提（qing）倡（ding）的，所以毫无疑问的是字体格式的未来。目前主流的浏览器的新版本几乎都支持 WOFF。

WOFF2 是 WOFF 的下一代。 WOFF2 格式在原有的基础上提升了 30% 的压缩率。由于它还没有 WOFF 的广泛支持，所以还只是一个可展望的升级。

## SVG
SVG (Scalable Vector Graphics font) 字体格式使用 SVG 的字体元素定义。这些字体包含作为标准 SVG 元素和属性的字形轮廓，就像它们是 SVG 映像中的单个矢量对象一样。SVG 字体最大的缺点是缺少字体提示（font-hinting）。字体提示是渲染小字体时为了质量和清晰度额外嵌入的信息。同时，SVG 对文本（body text）支持并不是特别好。因为 SVG 的文本选择（text selection）目前在 Safari、Safari Mobile 和 Chrome 的一些版本上完全崩坏，所以你不能选择单个字符、单词或任何自定义选项，你只能选择整行或段落文本。

然而，如果你的目标是 iPhone 和 iPad 用户，需要说 SVG 字体是 iOS 上 Safari 4.1 以下唯一允许的字体格式。

## PostScript 与 Type 1 字体
PostScript 是 Adobe 公司在 1984 年开发的页面描述语言。我们现在熟知的 PDF、XPS、SVG 都是同类型的东西。同时它也是个完备的编程语言

在 PostScript 出现之前，打印机多以点阵形式实现，也就是一种位图格式。有点类似于现在我们经常见到的各种购物小票或者电影票，喵喵机打印的也是这种点阵字符。这种打印方式打印的字符很不清晰

而 PostScript 作为一种矢量图形描述语言，具有高质量的曲线处理能力，同时它又兼容位图格式的输出。在 1985 年 3 月，支持 PostScript 的激光打印机 Apple LaserWriter 面世，随后 PostScript 便迅速流行

而 Type 1 是作为PostScript的一部分出现的一个配套字体文件。Type 1 字体一般由 *.pfm，*.pfb，*.afm，*.inf 四个文件组成


不过当时这种字体只在打印机中使用，屏幕上依旧用位图字体。因为 Adobe 没有公开渲染提示方案的细节,并将 Type 1 轮廓数据和渲染提示加密保护了起来。Adobe 要求 Type 1 字体技术的使用者购买高额的许可证授权。正因如此，苹果公司于 1991 年决定开发自己的 TrueType 格式……

## TrueType 字体
正如上文所述，苹果公司为了对抗 Adobe 开发的 PostScript Type 1 字体，开发了 TrueType 字体。后来，微软也加入了 TrueType 的开发。TrueType 随后成为了应用最广泛的屏幕显示字体格式。时至今日，还有相当数量的字体使用 TrueType 格式开发制作

TrueType 字体虽然最早由苹果牵头开发，但最终却并没有成功让 MacOS 换上 TrueType 字体。因为当时已经有很多用户花了大笔资金购买了 Type 1 字体，而且 TrueType 格式的字体数量稀少，也不值得更新。于是 MacOS 中呈现出了 PostScript 和 TrueType 对立的局面

反观微软这边，TrueType 却取得了大成功。1991 年，微软把 TrueType 加入Windows 3.1 系统。在与 Monotype 公司合作下，微软花了大力气制作了一批高质量 TrueType 字体，并使其可以与当时 PostScript 设备捆绑的核心字体兼容。其中包括了目前Windows系统的一些著名字体：Times New Roman 、 Arial 和 Courier New 等


不仅如此，微软还开发“提示技术”（hinting technology）来解决字体在低分辨率的显示模糊问题。后来逐步发展为使用至今的“次像素补偿”技术——ClearType。如上图所示，1、2 分别是使用、不使用 ClearType 技术渲染的斜直线，而3、4是 1、2 两条直线的放大图，5是 LED 显示器中的实际像素点亮情况。可以看到 ClearType 利用次像素补偿了斜直线的锯齿感，增加了字体清晰度


微软在发布 Windows Vista 时，同时发布了两个 ClearType 中文字体：微软雅黑和微软正黑体。微软雅黑体也从那时起作为 Windows 系统默认显示字体沿用至今。今天，如果你使用 Windows 系统，如果你放大屏幕文字截图，依然可以看到如上图所示的 ClearType 技术的应用

另外，微软还在1994年开发了一个叫“智能字体”（TrueType Open）的技术，两年后与 Adobe 的 Type 1 技术合并，共同开发了新一代字体格式 OpenType


TrueType 字体文件在 Windows 中的格式为 .ttf（TrueType Fonts）或 .ttc（TrueType Collection），在 MacOS 中为 .dfont

## OpenType 字体
如上文所述，微软在开发 TrueType Open 后与 Adobe 的 Type 1 合并，联合开发出了新一代字体 OpenType 用来代替 TrueType 的地位。再之后，苹果和谷歌也陆续加入了 OpenType 的开发

由于微软和 Adobe 的联合开发，OpenType 向下兼容 TrueType 以及 PostScript 字体，扩展名可能为 .otf、.otc、.ttf、.ttc 等。使用 PostScript 曲线的 OpenType 字体格式为 .otf、.otc，使用 TrueType 曲线的格式为 .ttf、.ttc

OpenType 字体有很多特性：

字体编码基于万国码（Unicode），可以支持任何文本，或者同时支持多种文本。一个OpenType字体可以带有最多65,536个字形，基本满足绝大多数地区的使用需求

OpenType 拥有良好的跨平台兼容性，能够在Mac OS，Windows和一些Unix系统中进行设置

字体有高级字形功能，可以进行对复杂文本进行充分的字形处理，并能通过更简单的文字施加更复杂的字形效果

而在2016年9月14日，由苹果、微软、谷歌和Adobe联合开发，OpenType 1.8版规范发布了 OpenType 可变字体（OpenType variable fonts）技术，更是将 OpenType 拉到了更高的台阶

OpenType 可变字体 能够储存轮廓变化数据，在初始字形轮廓的基础上自动生成丰富的变化造型，无极字重成为现实。上图为小米兰亭 Pro 字体的无极字重效果演示

至此，几家公司之间长达 40 年对电脑字体的探索终于凝缩到了 OpenType 这个标准中。目前，OpenType 所拥有的诸多新特性还未完全被各种软件全部支持，OpenType 作为一个前沿的字体规范引领着字体设计行业的发展


# 免费商用

- 思源字体

完整 Source Han 字体系列远远超出了普通 “超系列” 字体的范畴，它是 Adobe 与 Google 之间的大量合作以及合作伙伴公司（中国的常州华文、韩国的 Sandoll Communications、日本的 Iwata Corporation）参与的成果。这些字体以开源许可证形式在 GitHub 上发布。

思源黑体和思源宋体项目的成功离不开我们与 Google 的合作关系，Google 帮助我们启动此项目，并且提供了指导、测试资源和财务支持。思源黑体和思源宋体字体集成到 Google 的泛 Unicode 字体系列（称为 Noto）中。

- 阿里
1. 阿里巴巴普惠体
2. 阿里妈妈妈智造字
https://fonts.alibabagroup.com/ 

- Oppo Sans

- 台北黑体

