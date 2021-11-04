## 记忆时间

## 卡片

### 0101. 主题卡——

这本书的主题核心，就是最大的反常识卡，并且注意时间脉络。

### 0201. 术语卡——

根据反常识，再补充三个证据——就产生三张术语卡。

例子。

### 0202. 术语卡——

### 0203. 术语卡——

### 0301. 人名卡——

根据这些证据和案例，找出源头和提出术语的人是谁——产生一张人名卡，并且分析他为什么牛，有哪些作品，生平经历是什么。

维基百科链接：有的话。

#### 01. 基本信息

用一句话描述你对这个大牛的印象。

#### 02. 贡献及著作

### 0401. 金句卡——

最后根据他写的非常震撼的话语——产生一张金句卡。

### 0501. 行动卡——

行动卡是能够指导自己的行动的卡。

### 0601. 任意卡——

最后还有一张任意卡，记录个人阅读感想。

## Foreword to the First Edition

Conventional wisdom dictates that Vim has a steep learning curve. I think most Vim users would disagree. Sure, there’s an initial hump, but once you run through vimtutor and learn the basics of what to put in your vimrc, you reach a point where you can actually get work done—a sort of hobbled productivity.

What comes next? The Internet’s answer to this is the「tip」—a recipe for solving a specific problem. You might search for specific tips when your current solution to a problem feels suboptimal, or you might proactively read some of the more popular tips. This strategy works—it’s how I learned, after all—but it’s slow. Learning that `*` searches for the word under the cursor is helpful, but it hardly helps you think like a Vim master.

You can understand my skepticism, then, when I found out Practical Vim was using a tips format. How could a couple of hundred tips accomplish what took me thousands? A few pages in I realized my definition of「tip」was narrow-minded. In contrast to the problem/solution pattern I had expected, Practical Vim tips teach lessons in thinking like a proficient Vim user. In a sense, they are more like parables than recipes. The first few tips are lessons about the wide applicability of the `.` command. This is a staple of any proficient Vim user’s repertoire, yet without guidance it was years before I came to realize this on my own.

## Read Me

Practical Vim is for programmers who want to raise their game. You’ve heard it said that in the hands of an expert, Vim shreds text at the speed of thought. Reading this book is your next step toward that end.

Practical Vim is a fast track to Vim mastery. It won’t hold you by the hand, but beginners can find the prerequisite knowledge by running through the Vim tutor, an interactive lesson distributed with Vim.[1] Practical Vim builds on this foundation by highlighting core concepts and demonstrating idiomatic usage.

Vim is highly configurable. However, customization is a personal thing, so I’ve tried to avoid recommending what should or should not go into your vimrc file. Instead, Practical Vim focuses on the core functionality of the editor—the stuff that’s always there, whether you’re working over SSH on a remote server or using a local instance of GVim, with plugins installed to add extra functionality. Master Vim’s core, and you’ll gain portable access to a text editing power tool.

### 01. How This Book Is Structured

Practical Vim is a recipe book. It’s not designed to be read from start to finish. (I mean it! At the start of the next chapter, I’ll advise you to skip it and jump straight to the action.) Each chapter is a collection of tips that are related by a theme, and each tip demonstrates a particular feature in action. Some tips are self-contained. Others depend upon material elsewhere in the book. Those tips are cross-referenced so you can find everything easily.

Practical Vim doesn’t progress from novice to advanced level, but each individual chapter does. A less-experienced Vim user might prefer to make a first pass through the book, reading just the early tips in each chapter. A more advanced user might choose to focus on the later tips or move around the book as needed.

### 02. A Note on the Examples

In Vim, there’s always more than one way to complete any given task. For example, in Chapter 1, ​The Vim Way​, all of the problems are designed to illustrate an application of the dot command, but every one of them could also be solved using the `:substitute` command.

On seeing my solution, you might think to yourself,「Wouldn’t it be quicker to do it this way?」And you may well be right! My solutions illustrate a particular technique. Look beyond their simplicity, and try to find a resemblance to the problems that you face daily. That’s where these techniques will save you time.

### 03. Learn to Touch Type, Then Learn Vim

If you have to look down to find the keys on the keyboard, the benefits of learning Vim won’t come fast. Learning to touch type is imperative. Vim traces its ancestry back to the classic Unix editors, vi and ed (see ​On the Etymology of Vim (and Family)​). These predate the mouse and all of the point-and-click interfaces that came with it. In Vim, everything can be done with the keyboard. For the touch typist, that means Vim does everything faster.

如果你要低头看着键盘打字，那学习 Vim 的好处不会立竿见影地显现出来。要高效地使用 Vim，必须学会盲打。Vim 的祖先要追溯到经典的 Unix 编辑器 vi 和 ed，参见技巧 27 中的「Vim（及其家族）的词源」部分，它们比鼠标及所有点击界面出现得都早，因此根本没有这类接口，所有操作都通过键盘完成。Vim 也是一样，Vim 中的所有操作也都可以通过键盘完成。对盲打人员来说，这意味着用 Vim 做任何事都能更快些。

## Read the Forgotten Manual

In Practical Vim, I demonstrate by showing examples rather than by describing them. That’s not easy to do with the written word. To show the steps taken during an interactive editing session, I’ve adopted a simple notation that illustrates the keystrokes and the contents of a Vim buffer side by side.

If you’re keen to jump to the action, you can safely skip this chapter for now. It describes each of the conventions used throughout Practical Vim, many of which you’ll find to be self-explanatory. At some point, you’ll probably come across a symbol and wonder what it stands for. When that happens, turn back and consult this chapter for the answer.

在本书中，我会通过图例进行演示，而不是描述它们，因为用书面语不太容易做到这一点。为了显示在交互式编辑会话中所采取的步骤，我采用了一种简单的标记方法，把按键操作及 Vim 缓冲区的内容排在一起进行说明。如果你急于动手操作的话，现在可以直接跳过这一部分。这一部分主要描述本书沿用的体例，你会发现其中很多都不需要解释。或许在某个地方你会偶然发现一个符号，想搞清楚它究竟代表什么意思。当这种情况发生时，你可以回到这一部分来寻求答案。

### 01. Get to Know Vim’s Built-in Documentation

The best way to get to know Vim’s documentation is by spending time in it. To help out, I’ve included「hyperlinks」for entries in Vim’s documentation. For example, here’s the「hyperlink」for the Vim tutor: `:h vimtutor`.

The icon has a dual function. First, it serves as a signpost, drawing the eye to these helpful references. Second, if you’re reading this on an electronic device that’s connected to the Internet, you can click the icon and it will take you to the relevant entry in Vim’s online documentation. In this sense, it truly is a hyperlink. But what if you’re reading the paper edition of the book? Not to worry. If you have an installation of Vim within reach, simply enter the command as it appears in front of the icon.

For example, type :h vimtutor (:h is an abbreviation for the :help command). Consider this a unique address for the documentation on vimtutor: a URL of sorts. In this sense, the help reference is a kind of hyperlink to Vim’s built-in documentation.

这个图标具有两个作用。第一，它起到指示牌的作用，把目光吸引到这些有用的参考信息上；第二，如果你在联网的电子设备上阅读本书的话，那么你可以单击这些图标，它会把你带到 Vim 在线文档的相应入口。从这个意义上讲，它的确是超链接。但是，如果你正在阅读纸版书，那该怎么做？别担心，如果在你手边有可访问的 Vim 程序，简单地输入图标前的命令即可。

### 02. Notation for Simulating Vim on the Page

Vim’s modal interface sets it apart from most other text editors. To make a musical analogy, let’s compare the Qwerty and piano keyboards. A pianist can pick out a melody by playing one note at a time or he or she can hold down several keys at once to sound a chord. In most text editors, keyboard shortcuts are triggered by pressing a key while holding down one or more modifier buttons, such as the control and command keys. This is the Qwerty equivalent of playing a chord on the piano keyboard.

Some of Vim’s commands are also triggered by playing chords, but Normal mode commands are designed to be typed as a sequence of keystrokes. It’s the Qwerty equivalent of playing a melody on the piano keyboard.

Ctrl-s is a common convention for representing chordal key commands. It means「Press the Control key and the s key at the same time.」But this convention isn’t well suited to describing Vim’s modal command set. In this section, we’ll meet the notation used throughout Practical Vim to illustrate Vim usage.

Vim 区分模式的界面把它同其他文本编辑器区别开来。以音乐作个比喻，让我们拿 Qwerty 键盘与钢琴键盘进行比较。一个钢琴家可以每次只弹一个琴键来演奏主旋律，他也可以一次弹多个键来演奏和弦。对于多数文本编辑器，要触发一个键盘快捷键，需要先按住一个或多个修饰键，如控制键或命令键，然后再按另外一个键，在 Qwerty 键盘上的这种操作方式，等同于在钢琴键盘上演奏和弦。某些 Vim 命令也由演奏和弦的方式触发。不过普通模式命令则被设计成输入一串按键。在 Qwerty 键盘上的这种操作方式，则等同于在钢琴键盘上演奏主旋律。

`Ctrl-s` 是用来表示组合键命令的惯用约定，意为「同时按控制键及 s 键」，但这种约定方式并不适合用来描述 Vim 区分模式的命令集。在本节，我们将结识贯穿于全书的标记，在讲解 Vim 的用法时会用到它们。

### 03. Playing Melodies

In Normal mode, we compose commands by typing one or more keystrokes in sequence. These commands appear as follows:

| Notation | Meaning |
| --- | --- |
| x | Press x once |
| dw | In sequence, press d, then w |
| dap | In sequence, press d, a, then p |

Most of these sequences involve two or three keystrokes, but some are longer. Deciphering the meaning of Vim’s Normal mode command sequences can be challenging, but you’ll get better at it with practice.

在普通模式中，我们按次序输入一个或多个键组成一条命令。这些命令看起来像下面这样：这些序列大多数包含两个或 3 个按键，但有的命令会更长。解读 Vim 普通模式命令序列的含义可能颇具挑战性，不过经过练习后你会做得更好。

### 04. Playing Chords

When you see a keystroke such as `<C-p>`, it doesn’t mean「Press <, then C, then -, and so on.」The `<C-p>` notation is equivalent to `Ctrl-p`, which means「Press the `<Ctrl>` and p keys at the same time.」

I didn’t choose this notation without good reason. Vim’s documentation uses it (`:h key-notation`), and we can also use it in defining custom key mappings. Some of Vim’s commands are formed by combining chords and keystrokes in sequence, and this notation handles them well. Consider these examples:

我不会无缘无故地选择这种标记方式的。首先，在 Vim 的文档中使用了这种标记（`:h key-notation`），我们也用它定义自定义按键映射项。另外，某些 Vim 命令由组合键及其他键以一定的次序组合在一起，这种标记也可以很好地表达这些命令。请看下面这些例子。

| Notation | Meaning |
| --- | --- |
| `<C-n>` | Press `<Ctrl> `and n at the same time |
| `g<C-]>` | Press g, followed by `<Ctrl>` and ] at the same time |
| `<C-r>0` | Press `<Ctrl>` and r at the same time, then 0 |
| `<C-w><C-=>` | Press `<Ctrl> `and w at the same time, then `<Ctrl>` and = at the same time |

### 05. Placeholders

Many of Vim’s commands require two or more keystrokes to be entered in sequence. Some commands must be followed by a particular kind of keystroke, while other commands can be followed by any key on the keyboard. I use curly braces to denote the set of valid keystrokes that can follow a command. Here are some examples:

很多 Vim 命令需要以一定的次序按两个或多个按键。有些命令后面必须跟某种特定类型的按键，而其他命令后面则可以跟键盘上的任意键。我使用花括号表示一条命令后可以跟有效按键集合。下面是一些例子。

| Notation | Meaning |
| --- | --- |
| `f{char}` | Press f, followed by any other character |
| ``{a-z}` | Press \`, followed by any lowercase letter |
| `m{a-zA-Z}` | Press m, followed by any lowercase or uppercase letter |
| `d{motion}` | Press d, followed by any motion command |
| `<C-r>{register}` | Press `<Ctrl>` and r at the same time, followed by the address of a register |

### 06. Showing Special Keys

Some keys are called by name. This table shows a selection of them:

| Notation | Meaning |
| --- | --- |
| `<Esc>` | Press the Escape key |
| `<CR>` | Press the carriage return key (also known as `<Enter>`) |
| `<Ctrl>` | Press the Control key |
| `<Tab>` | Press the Tab key |
| `<Shift>` | Press the Shift key |
| `<S-Tab>` | Press the `<Shift>` and `<Tab>` keys at the same time |
| `<Up>` | Press the up arrow key |
| `<Down>` | Press the down arrow key |
| `␣` | Press the space bar |

Note that the space bar is represented as `␣`. This could be combined with the `f{char}` command to form `f␣`.

### 07. Switching Modes Midcommand

When operating Vim, it’s common to switch from Normal to Insert mode and back again. Each keystroke could mean something different, depending on which mode is active. I’ve used an alternative style to represent keystrokes entered in Insert mode, which makes it easy to differentiate them from Normal mode keystrokes.

Consider this example: cwreplacement<Esc>. The Normal mode cw command deletes to the end of the current word and switches to Insert mode. Then we type the word「replacement」in Insert mode and press <Esc> to switch back to Normal mode again.

The Normal mode styling is also used for Visual mode keystrokes, while the Insert mode styling can indicate keystrokes entered in Command-Line mode and Replace mode. Which mode is active should be clear from context.

在操作 Vim 时，经常会从普通模式切换到插入模式，然后再切换回普通模式。Vim 中的每个键都可能具有不同的含义，这取决于当前哪个模式生效。我用了另一种样式表示在插入模式中输入的键，这可以让人很容易地把它们与普通模式下的按键区分开来。

看看这个例子 `cw`replacement`<Esc>`。普通模式命令 cw 会删除从光标位置到当前词结尾处的文本，并切换到插入模式。然后我们在插入模式中输入单词「replacement」，并按 `<Esc>` 键再切换回普通模式。普通模式所用的样式也用于可视模式，而插入模式的样式也用来表示命令行模式及替换模式下输入的按键。你可以通过上下文清楚地知道当前处于哪个模式。

### 08. Interacting with the Command Line

In some tips we’ll execute a command line, either in the shell or from inside Vim. This is what it looks like when we execute the grep command in the shell:

```
​=> ​$ grep -n Waldo *​
```

And this is how it looks when we execute Vim’s built-in `:grep` command:

```
​=> ​:grep Waldo *​
```

In Practical Vim, the `$` symbol indicates that a command line is to be executed in an external shell, whereas the `:` prompt indicates that the command line is to be executed internally from Command-Line mode. Occasionally we’ll see other prompts, including these:

| Prompt | Meaning |
| --- | --- |
| `$` | Enter the command line in an external shell |
| `:` | Use Command-Line mode to execute an Ex command |
| `/` | Use Command-Line mode to perform a forward search |
| `?` | Use Command-Line mode to perform a backward search |
| `=` | Use Command-Line mode to evaluate a Vim script expression |

Any time you see an Ex command listed inline, such as :write, you can assume that the `<CR>` key is pressed to execute the command. Nothing happens otherwise, so you can consider `<CR>` to be implicit.

By contrast, Vim’s search command allows us to preview the first match before pressing `<CR>` (see Tip 82). When you see a search command listed inline, such as /pattern`<CR>`, the` <CR>` keystroke is listed explicitly. If the `<CR>` is omitted, that’s intentional, and it means you shouldn’t press the Enter key just yet.

无论你何时在文中见到一条 Ex 命令，比如 `:write`，都可以假设我们按了 `<CR>` 键来执行该命令，否则该命令什么也不会做，因此可以认为 `<CR>` 在 Ex 命令中是隐含的。与之相反，Vim 的查找命令允许在按 `<CR>` 前预览第一个匹配项（参见技巧 82）。当你在文中见到一条查找命令时，比如 /pattern`<CR>`，你会看到 `<CR>` 键被显式地标出来了；如果 `<CR>` 被省略了，那是有意为之，也就是说你现在还不要按回车。

### 09. Showing the Cursor Position in a Buffer

When showing the contents of a buffer, it’s useful to be able to indicate where the cursor is positioned. In this example, you should see that the cursor is placed on the first letter of the word「One」:

When we make a change that involves several steps, the contents of the buffer pass through intermediate states. To illustrate the process, I use a table showing the commands executed in the left column and the contents of the buffer in the right column. Here’s a simple example:

显示缓冲区内光标的位置。在显示缓冲区内容时，如果能指示当前光标位于何处，那会很有用。在下面的例子里，你可以看到光标位于单词「One」的第一个字母上。当我们执行一项包含若干步的修改时，缓冲区的内容会经历一些中间状态。为了讲解这一过程，我使用了一个表格，在其左栏中显示所执行的命令，在右栏中显示缓冲区的内容。下面是个简单的例子。

| Keystrokes | Buffer Contents |
| --- | --- |
| `{start}` | One two three |
| dw | ​ two three |

In row 2 we run the dw command to delete the word under the cursor. We can see how the buffer looks immediately after running this command by looking at the contents of the buffer in the same row.

在第 2 行，我们运行 dw 命令删除了光标下的单词。通过查看位于同一行的缓冲区内容，我们可以立刻看到这条命令执行完后缓冲区的状态。

### 10. Highlighting Search Matches

When demonstrating Vim’s search command, it’s helpful to be able to highlight any matches that occur in the buffer. In this example, searching for the string「the」causes four occurrences of the pattern to be highlighted:

| Keystrokes | Buffer Contents |
| --- | --- |
| `{start}` | ​the problem with these new recruits is that they don't keep their boots clean. |
| `/the<CR>` | ​ ​the problem with these new recruits is that they don't keep their boots clean. |

Skip ahead to Tip 81, to find out how to enable search highlighting in Vim.

在讲解 Vim 的查找命令时，如果能把缓冲区内出现的每个匹配项都高亮显示出来，那会很有帮助。在下例中，查找字符串「the」会让出现该模式的 4 处地方被高亮显示出来。你可以跳到技巧 81，了解如何激活 Vim 的查找高亮功能。

### 11. Selecting Text in Visual Mode

Visual mode lets us select text in the buffer and then operate on the selection. Here, we use the `it` text object to select the contents of the `<a>` tag:

| Keystrokes | Buffer Contents |
| --- | --- |
| `{start}` | `​<a href="http://pragprog.com/dnvim/">Practical Vim</a>` |
| `vit` | ​`<a href="http://pragprog.com/dnvim/">Practical Vim</a>` |

Note that the styling for a Visual selection is the same for highlighted search matches. When you see this style, it should be clear from context whether it represents a search match or a Visual selection.

可视模式允许在缓冲区内选择文本，然后在其上操作。在下例中，用 it 文本对象选中 `<a>` 标签内的文本。注意，高亮显示可视选区的样式与高亮显示查找匹配项的样式相同。当你看到这种样式时，根据上下文就可以知道它究竟是代表一处查找匹配项，还是一个高亮选区。

### 12. Downloading the Examples

The examples in Practical Vim usually begin by showing the contents of a file before we change it. These code listings include the file path:

```
macros/incremental.txt
​ partridge in a pear tree
​ turtle doves
​ French hens
​ calling birds
​ golden rings
```

Each time you see a file listed with its file path in this manner, it means that you can download the example. I recommend that you open the file in Vim and try out the exercises for yourself. It’s the best way to learn!

To follow along, download all the examples and source code from the Pragmatic Bookshelf.[2] If you’re reading on an electronic device that’s connected to the Internet, you can also fetch each file one by one by clicking on the filename. Try it with the example above.

本书中的例子通常都先显示修改前的文件内容，并在示例文本中给出该文件所在的路径，如下所示。每当你看到以这种方式列出的文件路径时，都表示该例可被下载。我建议你在 Vim 中打开此文件，然后亲自试试这个例子。这是学习 Vim 的最好方式。要照着书中的例子操作，你可以从 Pragmatic Bookshelf 的网站上下载本书所有的示例和源代码。如果你在联网电子设备上阅读本书，也可以单击文件名来逐一获取每个文件。你可以用上面的例子试验一下。

### 13. Use Vim’s Factory Settings

Vim is highly configurable. If you don’t like the defaults, then you can change them. That’s a good thing, but it could cause confusion if you follow the examples in this book using a customized version of Vim. You may find that some things don’t work for you the way that they are described in the text. If you suspect that your customizations are causing interference, here’s a quick test. Try quitting Vim and then launching it with these options:

Vim 是高度可配置的，如果你不喜欢其默认的行为，可以改变它们。这本是好事，但是，如果你用自定义的 Vim 跟着做本书中的例子，可能会感到迷惑，你也许会发现有些东西并不像书中描述的那样工作。如果你怀疑是自定义配置造成了干扰，那么你可以做一个快速的测试。试着先退出 Vim，然后再用下列选项启动它。

```
​=> ​$ vim -u NONE -N​
```

The -u NONE flag tells Vim not to source your vimrc on startup. That way, your customizations won’t be applied and plugins will be disabled. When Vim starts up without loading a vimrc file, it reverts to vi compatible mode, which causes many useful features to be disabled. The -N flag prevents this by setting the ‘nocompatible’ option.

For most examples in Practical Vim, the vim -u NONE -N trick should guarantee that you get the same experience as described, but there are a couple of exceptions. Some of Vim’s built-in features are implemented with Vim script, which means that they will only work when plugins are enabled. This file contains the absolute minimum configuration that is required to activate Vim’s built-in plugins:

`-u NONE` 标志让 Vim 在启动时不加载你的 vimrc，这样，你的定制项就不会生效，插件也会被禁用。当用不加载 vimrc 文件的方式启动时，Vim 会切换到 vi 兼容模式，这将导致很多有用的功能被禁用，-N 标志则会使能 `‘nocompatible’` 选项，防止进入 vi 兼容模式。

对于本书中的大多数例子来说，用 `vim -u NONE –N` 启动 Vim 应该可以确保你获得与书中的描述相符的体验，不过也有几处例外。有些 Vim 的内置功能是由 Vim 脚本实现的，也就是说，只有在激活插件时，它们才会工作。下面的文件中包含了激活 Vim 内置插件的最小配置。

```
essential.vim
​ ​set​ nocompatible
​ ​filetype​ plugin ​on​
```

When launching Vim, you can use this file instead of your vimrc by running the following:

```
​=> ​$ vim -u code/essential.vim​
```

You’ll have to adjust the code/essential.vim path accordingly. With Vim’s built-in plugins enabled, you’ll be able to use features such as netrw (Tip 44) and omni-completion (Tip 119), as well as many others. I consider Vim’s factory settings to mean built-in plugins enabled and vi compatibility disabled.

Look out for subsections titled「Preparation」at the top of a tip. To follow along with the material in these tips, you’ll need to configure Vim accordingly. If you start up with Vim’s factory settings and then apply the customizations on the fly, you should be able to reproduce the steps from these tips without any problems.

If you’re still having problems, see ​On Vim Versions​.

在启动 Vim 时，可以执行如下命令，用该文件取代你的 vimrc。在执行时，需要相应地调整 `code/essential.vim` 文件所在的路径。激活 Vim 内置的插件功能后，可以使用诸如 netrw（参见技巧 44）、omni-completion（参见技巧 119），以及很多其他的功能。我在本书中所说的 Vim 的出厂配置，指的就是激活了内置的插件功能，并且禁用了 vi 兼容模式时的配置。

需要留意技巧开头的名为「准备工作」的小节，要想跟着技巧中的步骤做，需要对 Vim 进行相应的配置。如果你由 Vim 的出厂配置开始，然后再动态应用这些定制项，就应该能重现技巧中的结果，不会遇到任何问题。如果你仍遇到问题，请看后面的「关于 Vim 的版本」部分。

### 14. On the Role of Vim Script

Vim script enables us to add new functionality to Vim or to change existing functionality. It’s a complete scripting language in itself and a subject worthy of a book of its own. Practical Vim is not that book.

But we won’t steer clear of the subject entirely. Vim script is always just below the surface, ready to do our bidding. We’ll see a few examples of how it can be used for everyday tasks in Tip 16; Tip 71; Tip 95; and Tip 96.

Practical Vim shows you how to get by with Vim’s core functionality. In other words, no third-party plugins assumed. I’ve made an exception for Tip 87. The visual-star.vim plugin adds a feature that I find indispensable, and it requires very little code—less than ten lines of Vim script. It demonstrates how easily Vim’s functionality can be extended. The implementation of visual-star.vim is presented inline without explanation. This should give you an idea of what Vim script looks like and what you can accomplish with it. If it piques your interest, then so much the better.

Vim 脚本让我们可以给 Vim 添加新的功能，或是改变其已有的功能。它是一种完整的脚本语言，并且这个主题本身就可以写一整本书。不过本书并不是这样一本书。但我们不会完全避开此话题，Vim 脚本一直隐身在幕后，时刻准备响应我们的召唤。在技巧 16、技巧 71、技巧 95 及技巧 96 中，我们将看到一些如何使用它们完成日常工作的例子。

本书展示了如何使用 Vim 的核心功能。换句话说，它假设我们不使用任何第三方插件。不过技巧 87 是个例外，visual-star.vim 插件添加的功能我认为是不可或缺的，并且它只需很少的代码 —— 不超过 10 行。同时它也展示了扩充 Vim 的功能是多么容易。文中给出了 visual-star.vim 的实现，但没有讲解。这应该能给你一些印象，了解 Vim 脚本是什么样的，以及你能用它干什么。如果它激起了你的兴趣，那就更好了。

### 15. On Vim Versions

All examples in Practical Vim were tested on the latest version of Vim, which was 7.4 at the time of writing. That said, most examples should work fine on any 7.x release, and many of the features discussed are also available in 6.x.

Some of Vim’s functionality can be disabled during compilation. For example, when configuring the build, we could provide the --with-features=tiny option, which would disable all but the most fundamental features (there are also feature sets labeled small, normal, big, and huge). You can browse the feature list by looking up +feature-list.

If you find that you’re missing a feature discussed in this book, you might be using a minimal Vim build. Check whether or not the feature is available to you with the :version command:

```
​=> ​:version​
​<= VIM - Vi IMproved 7.4 (2013 Aug 10, compiled Oct 14 2015 18:41:08)
​ Huge version without GUI. Features included (+) or not (-):
​ +arabic +autocmd +balloon_eval +browse +builtin_terms +byte_offset
​ +cindent +clientserver +clipboard +cmdline_compl +cmdline_hist
​ +cmdline_info +comments
 ...
```

On a modern computer, there’s no reason to use anything less than Vim’s huge feature set!

本书中的所有例子都在最新的 Vim 版本中测试过，在写本书时是版本 7.4。就是说，大多数例子在任意 7.x 版本中都能够很好地工作，并且所讨论的很多功能在 6.x 中也同样适用。有些 Vim 功能可以在编译期间被禁用。例如，在配置编译选项时，可以传入 `--with-features=tiny` 参数，这会禁用除最基本的功能外的其他所有功能（Vim 的功能集还包括 small、normal、big 和 huge）。可以查阅 `:h+feature-list`，浏览完整的功能列表。如果你发现自己的 Vim 缺少本书所讨论的某个功能，那么你也许正在使用一个最小功能集的 Vim 发行版。可以用 `:version` 命令检查此功能是否可用。在现代计算机上，没理由不用 Vim 的 huge 功能集！

### 16. Vim in the Terminal or Vim with a GUI? You Choose!

Traditionally, Vim runs inside of the terminal, with no graphical user interface (GUI). We could say instead that Vim has a TUI: a textual user interface. If you spend most of your day at the command line, this will feel natural.

If you’re accustomed to using a GUI-based text editor, then GVim (or MacVim on OS X) will provide a helpful bridge into the world of Vim (see guiⓘ). GVim supports more fonts and more colors for syntax highlighting. Also, you can use the mouse. And some of the conventions of the operating system are honored. For example, in MacVim you can interact with the system clipboard using Cmd-X and Cmd-V, save a document with Cmd-S, or close a window with Cmd-W. Use these while you find your bearings, but be aware that there’s always a better way.

For the purposes of this book, it doesn’t matter whether you run Vim in the terminal or as GVim. We’ll focus on core commands that work just as well in either. We’ll learn how to do things the Vim way.

传统上，Vim 在终端内运行，没有图形用户界面（GUI）。我们也可以说 Vim 具有 TUI，即文本用户界面。如果你每天有大量时间花在命令行上，你会感觉这很自然。如果你通常使用基于图形用户界面的文本编辑器，那么 GVim（或 OSX 上的 MacVim）可以给你提供一个通往 Vim 世界的有用桥梁（参见 `:h gui`）。GVim 支持更多的字体以及更多的语法高亮颜色，也可以使用鼠标。它也遵从某些操作系统的约定，例如，在 MacVim 中，可以用 `Cmd-X` 和 `Cmd-V` 与系统剪切板交互，也可以用 `Cmd-S` 保存文件，用 `Cmd-W` 关闭一个窗口。如果你能接受的话，可以用这些命令，不过你应该已意识到，还有更好的方法完成这些。对本书的目的而言，运行终端 Vim 还是 GVim 关系不大。我们将着重于介绍 Vim 的核心命令，这些功能在两者中都能很好地运行。我们要学习的重点是如何用 Vim 的方式来工作。