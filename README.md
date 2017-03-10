- [easy-lentic 使用说明](#org935e328)
  - [安装](#org2264771)
    - [安装 easy-lentic](#orgbbad9de)
    - [安装 ox-gfm](#org5d8a0db)
  - [配置](#org5c69729)
  - [使用](#org6686e2f)
    - [编写 org 格式的 Comment](#orgf837d7b)
    - [自动生成 README 文档](#org6afa83f)


<a id="org935e328"></a>

# easy-lentic 使用说明

注意： 这个包作者已经不维护了，有兴趣的同学可以收养它 :-) !!!

easy-lentic 是基于 lentic 的一个扩展，但它不是扩展了 lentic 的功能，而是让 lentic 更加专注 于一个 **特定** 的使用场合，即：

    编写 emacs-lisp 时，使用 org 格式组织 comment。

注：[lentic](https://github.com/phillord/lentic) 是一个很有新意的包，引用作者的原话：

    Lentic allows two buffers to share the same or similar content but otherwise operate independently.
    This can be used for several different purposes.
    Different buffers can be in the same mode, with different locations of point,
    even different text sizes -- in effect, providing multiple persistent views.

    It is also possible to have the different lentic buffers in different modes,
    giving a form of multi-modal editing. Switching buffers effectively switches modes as well.

    While the content of two lentic buffers must be related, it does not need to be syntactically identical.
    This allows it to be used for a form of literate programming -- for example,
    one buffer may contain valid LaTeX source with blocks of Lisp,
    while in the other the LaTeX source is commented out, giving an entirely valid Lisp file.

    ...


<a id="org2264771"></a>

## 安装


<a id="orgbbad9de"></a>

### 安装 easy-lentic

1.  配置 melpa 源，参考：<http://melpa.org/#/getting-started>
2.  M-x package-install RET easy-lentic RET


<a id="org5d8a0db"></a>

### 安装 ox-gfm

easy-lentic 可以使用 ox-gfm (Github Flavored Markdown exporter for Org Mode) 将 org 格式转换 为 github markdown 格式，但这个功能需要用户 **手动安装 ox-gfm**, 具体安装方式：

1.  配置 melpa 源，参考：<http://melpa.org/#/getting-started>
2.  M-x package-install RET ox-gfm RET

如果用户没有安装 ox-gfm, 那么，easy-lentic 将使用 ox-md 后端生成 README.md。


<a id="org5c69729"></a>

## 配置

    (require 'easy-lentic)   ;; You need install lentic and gfm
    (easy-lentic-mode-setup) ;; Enable `easy-lentic-mode' for `emacs-lisp-mode' and `org-mode'


<a id="org6686e2f"></a>

## 使用


<a id="orgf837d7b"></a>

### 编写 org 格式的 Comment

编辑 emacs-lisp 文件时，按 'C-c ..'（\`easy-lentic-switch-window'）会弹出一个 org-mode 窗口，这个窗口显示的内容和 emacs-lisp 文件内容在逻辑上具有高度的相似性。 这样，comment 部份可以在 org buffer 中编辑，而 elisp 代码则可以到 emacs-lisp buffer中编辑， 两个 buffer 中的内容实时自动的同步。


<a id="org6afa83f"></a>

### 自动生成 README 文档

\`easy-lentic-generate-readme' 可以从当前 elisp 文件的 Commentary 部份提取相关内容， 然后生成 README.md 文件，这个功能对 Commentary 的格式有一定的要求：

1.  必须使用 org 格式编写。
2.  Head1 必须包含 README tag。

比如：

    * This is Head1   :README:
    ** This is Head2
    *** This is Head3
    [[http://www.google.com][this is a link]]

    * This head1 will not export