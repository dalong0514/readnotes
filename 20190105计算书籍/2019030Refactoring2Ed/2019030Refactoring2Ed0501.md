# 0501. Introducing the Catalog

The rest of this book is a catalog of refactorings. This catalog started from my personal Tutorialsnotes that I made to remind myself how to do refactorings in a safe and efficient way. Since then, I’ve refined the catalog, and there’s more of it that comes from deliberate Offers exploration & Deals of some refactoring moves. It’s still something I use when I do a refactoring I haven’t done in a while.

本书剩余的篇幅是一份重构的名录。最初这个名录只是我的个人笔记，我用它来提示自己如何以安全且高效的方式进行重构。然后我不断精炼这份名录，对一些重构的深入探索又引出了更多的重构手法。对于不太常用的重构手法，我还是会不断参阅这份名录。

## 5.1 Format of The Refactorings

As I describe the refactorings in the catalog, I use a standard format. Each refactoring Support has five parts, as follows:

1. Sign Out I begin with a name. The name is important to building a vocabulary of refactorings. This is the name I use elsewhere in the book. Refactorings often go by different names now, so I also list any aliases that seem to be common.

2. I follow the name with a short sketch of the refactoring. This helps you find a refactoring more quickly.

3. The motivation describes why the refactoring should be done and describes circumstances in which it shouldn’t be done.

4. The mechanics are a concise, step­by­step description of how to carry out the refactoring.

5. The examples show a very simple use of the refactoring to illustrate how it works.

介绍重构时，我采用一种标准格式。每个重构手法都有如下 5 个部分。

1、首先是名称（name）。要建造一个重构词汇表，名称是很重要的。这个名称也就是我将在本书其他地方使用的名称。如今重构经常会有多个名字，所以我会同时列出常见的别名。

2、名称之后是一个简单的速写（sketch）。这部分可以帮助你更快找到你所需要的重构手法。

3、动机（motivation）为你介绍「为什么需要做这个重构」和「什么情况下不该做这个重构」。

4、做法（mechanics）简明扼要地一步一步介绍如何进行此重构。

5、范例（examples）以一个十分简单的例子说明此重构手法如何运作。

The sketch shows a code example of the transformation of the refactoring. It’s not meant to explain what the refactoring is, let alone how to do it, but it should remind you what the refactoring is if you’ve come across it before. If not, i you’ll probably need to work through the example to get a better idea. I also include a small graphic; again, I don’t intend it to be explanatory—it’s more of a graphic memory­jogger. The mechanics come from my own notes to remember how to do the refactoring when I haven’t done it for a while. As such, they are somewhat terse, usually without explanations of why the steps are done that way. I give a more expansive explanation in the example. This way, the mechanics are short notes you can refer to easily when you know the refactoring but need to look up the steps (at least this is how I use them). You’ll probably need to read the examples when you first do the refactoring.

I’ve written the mechanics in such a way that each step of each refactoring is as small as possible. I emphasize the safe way of doing the refactoring—which is to take very small steps and test after every one. At work, I usually take larger steps than some of the baby steps described, but if I run into a bug, I back out the last step and take the smaller steps. The steps include a number of references to special cases. The steps thus also function as a checklist; I often forget these things myself.

Although I (with few exceptions) only list one set of mechanics, they aren’t the only way to carry out the refactoring. I selected the mechanics in the book because they work pretty well most of the time. It’s likely you’ll vary them as you get more practice in refactoring, and that’s fine. Just remember that the key is to take small steps—and the trickier the situation, the smaller the steps.

The examples are of the laughably simple textbook kind. My aim with the examples is to help explain the basic refactoring with minimal distractions, so I hope you’ll forgive the simplicity. (They are certainly not examples of good business modeling.) I’m sure you’ll be able to apply them to your rather more complex situations. Some very simple refactorings don’t have examples because I didn’t think an example would add much.

In particular, remember that the examples are included only to illustrate the one refactoring under discussion. In most cases, there are still problems with the code at the end—but fixing these problems requires other refactorings. In a few cases in which refactorings often go together, I carry examples from one re­factoring to another. In most cases, I leave the code as it is after the single refactoring. I do this to make each refactoring self­contained, because the primary role of the catalog is to be a reference.

I use color to highlight changed code where it may be difficult to spot among code that has not been changed. I do not use highlighting for all changed code, because too much defeats the purpose.

速写部分会以代码示例的形式展示重构带来的转变。速写的用意不是解释重构的用途，更不是详细讲解如何操作这个重构；但如果你曾经看过这个重构手法，速写能帮你回忆起它。如果你是第一次接触到这个重构手法，可能最好是先阅读范例部分。我还给每个重构手法画了一幅小图。同样，我也不指望这些小图能说清重构手法的内容，只是提供一点图像记忆的线索。

「做法」出自我自己的笔记。这些笔记是为了让我在一段时间不做某项重构之后还能记得怎么做。它们也颇为简洁，通常不会解释「为什么要这么做那么做」。我会在「范例」中给出更多解释。这么一来，「做法」就成了简短的笔记。如果你知道该使用哪个重构，但记不清具体步骤，可以参考「做法」部分（至少我是这么使用它们的）；如果你初次使用某个重构，可能只参考「做法」还不够，你还需要阅读「范例」。

撰写「做法」的时候，我尽量将重构的每个步骤拆得尽可能小。我强调安全的重构方式，所以应该采用非常小的步骤，并且在每个步骤之后进行测试。真正工作时，我通常会采用比这里介绍的「婴儿学步」稍大些的步骤，然而一旦出问题，我就会撤销上一步，换用比较小的步骤。这些步骤还包含一些特殊情况的参考，所以它们也有检查清单的作用。我自己经常忘掉这些该做的事情。

绝大多数时候我只列出了重构的一套做法，但其实一个重构并非只有一套做法。我在本书中选择介绍这些做法，因为它们大多数时候都管用。等你经过练习获得更多重构经验，你可能会调整重构的做法，那完全没问题。只要牢记一点：小步前进，情况越复杂，步子就要越小。

「范例」像是简单而有趣的教科书。我使用这些范例是为了帮助解释重构的基本要素，最大限度地避免其他枝节，所以我希望你能原谅其中的简化工作（它们当然不是优秀的业务建模例子）。不过我敢肯定，你一定能在那些更复杂的情况中使用它们。某些十分简单的重构干脆没有范例，因为我觉得为它们加上一个范例不会有多大意义。

更明确地说，加上范例仅仅是为了阐释当时讨论的重构手法。通常那些代码最终仍有其他问题，但修正那些问题需要用到其他重构手法。某些情况下数个重构经常被一并运用，这时候我会把范例带到另一个重构中继续使用。大部分时候，一个范例只为一项重构而设计，这么做是为了让每一项重构手法自成一体，因为这份重构名录的首要目的还是作为参考工具。

修改后的代码可能被埋没在未修改的代码中，难以一眼看出，所以我使用不同的颜色突出显示修改过的代码。但我并没有突出显示所有修改过的代码，因为一旦修改过的代码太多，全都突出显示反而不能突显重点。

## 5.2 The Choice of Refactorings

This is by no means a complete catalog of refactorings. It is, I hope, a collection of those most useful to have them written down. By “most useful” I mean those that are both commonly used and worthwhile to name and describe. I find something worthwhile to describe for a combination of reasons: Some have interesting mechanics which help general refactoring skills, some have a strong effect on improving the design of code.

Some refactorings are missing because they are so small and straightforward that I don’t feel they are worth writing up. An example in the first edition was Slide Statements (223)—which I use frequently but didn’t recognize as something I should include in the catalog (obviously, I changed my mind for this edition). These may well get added to the book over time, depending on how much energy I devote to new refactorings in the future.

Another category is refactorings that logically exist, but either aren’t used much by me or show a simple similarity to other refactorings. Every refactoring in this book has a logical inverse refactoring, but I didn’t write all of them up because I don’t find many inverses interesting. Encapsulate Variable (132) is a common and powerful refactoring but its inverse is something I hardly ever do (and it is easy to perform anyway) so I didn’t think we need a catalog entry for it.

这不是一份巨细靡遗的重构名录。我只是认为这些重构手法最值得被记录下来。之所以说它们「最值得」，因为这些都是很常用的重构手法，并且值得给它们命名和详细的介绍：其中一些做法很有意思，能帮助读者提高整体重构技能水平，另外一些则对于代码设计质量的提升效果显著。

有些重构没有进入这份名录，因为它们太小、太简单，我觉得没必要多加赘述。例如，在撰写第 1 版时我就曾经考虑过移动语句（223），这个重构我经常使用，但我觉得没必要将它放进名录里（显然我在写第 2 版的时候改变了想法）。以后也许还有类似这样的重构会被加进书里，不过那要看我投入多少精力在新增重构上了。

还有一些没有进入名录的重构，要么是我用得很少，要么是与其他重构非常相似。本书中的每个重构，逻辑上来说，都有一个反向的重构。但我并没有把所有反向重构都写下来，因为我发现很多反向重构没太大意思。例如，封装变量（132）是一个常用又好用的重构，但它的反向重构我几乎从来不会做（而且就算要做也非常简单），所以我觉得没必要将这个反向重构放进名录。
