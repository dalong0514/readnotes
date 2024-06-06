Ethan Mollick.(2024).2024029Co-Intelligence_Living-and-Working-with-AI.Penguin Publishing Group => 

## 0501. AI AS A CREATIVE

Our first principle of working with AI is to always invite it to the table. We have discussed how interacting with AI can resemble talking to and working with people. But what kind of people? What skills does an AI have? What is it good at? To talk about that, we first need to confront what AI is very bad at.

The biggest issue limiting AI is also one of its strengths: its notorious ability to make stuff up, to hallucinate. Remember that LLMs work by predicting the most likely words to follow the prompt you gave it based on the statistical patterns in its training data. It does not care if the words are true, meaningful, or original. It just wants to produce a coherent and plausible text that makes you happy. Hallucinations sound likely and contextually appropriate enough to make it hard to tell lies from the truth.

There is no definitive answer to why LLMs hallucinate, and the contributing factors may differ among models. Different LLMs may have different architectures, training data, and objectives. But in many ways, hallucinations are a deep part of how LLMs work. They don't store text directly; rather, they store patterns about which tokens are more likely to follow others. That means the AI doesn't actually "know" anything. It makes up its answers on the fly. Plus, if it sticks too closely to the patterns in its training data, the model is said to be overfitted to that training data. Overfitted LLMs may fail to generalize to new or unseen inputs and generate irrelevant or inconsistent text—in short, their results are always similar and uninspired. To avoid this, most AIs add extra randomness in their answers, which correspondingly raises the likelihood of hallucination.

Beyond the technical, hallucinations can also come from the source material of the AI, which can be biased, incomplete, contradictory, or even wrong in ways that we discussed in chapter 2. The model has no way of distinguishing opinion or creative fictional work from fact, figurative language from literal, or unreliable sources from reliable ones. The model may inherit the biases and prejudices of the data creators, curators, and fine-tuners.

It can be funny when the AI fails to distinguish when fiction bleeds into reality. For example, Colin Fraser, a data scientist, noted that when asked for a random number between 1 and 100, ChatGPT answered "42" 10 percent of the time. If it were truly choosing a number randomly, it should answer "42" only 1 percent of the time. The science fiction nerds among my readers have probably already guessed why 42 pops up so much more often. In Douglas Adams's classic comedy The Hitchhiker's Guide to the Galaxy , 42 is the answer to the "ultimate question of life, the universe, and everything" (leaving open a bigger issue: What was the question?), and the number has become a shorthand joke on the internet. Thus, Fraser speculates that there are a lot more 42s for the AI to see than other numbers, which, in turn, increases the likelihood that AI will output that number—while hallucinating that it is giving you a random answer.

These technical issues are compounded because they rely on patterns, rather than a storehouse of data, to create answers. If you ask an AI to give you a citation or a quote, it is going to generate that quote or citation based on the connections between the data it learned, not retrieve it from memory. If the quote is famous, like "Four score and seven years ago," the AI will finish it properly: ". . . our fathers brought forth on this continent, a new nation, conceived in Liberty, and dedicated to the proposition that all men are created equal." The AI has seen those connections enough times to figure out the next word. If it is more obscure, like my biography, it will fill in the details with plausible hallucinations, like GPT-4 insisting that I have a computer science undergraduate degree. Anything that requires exact recall is likely to result in a hallucination, though giving AI the ability to use outside resources, like web searches, might change this equation.

And you can't figure out why an AI is generating a hallucination by asking it. It is not conscious of its own processes. So if you ask it to explain itself, the AI will appear to give you the right answer, but it will have nothing to do with the process that generated the original result. The system has no way of explaining its decisions, or even knowing what those decisions were. Instead, it is (you guessed it) merely generating text that it thinks will make you happy in response to your query. LLMs are not generally optimized to say "I don't know" when they don't have enough information. Instead, they will give you an answer, expressing confidence.

One of the most notorious early examples of hallucination in LLMs occurred in 2023, when a lawyer named Steven A. Schwartz used ChatGPT to prepare a legal brief for a personal injury lawsuit against an airline. Schwartz used ChatGPT to research court filings; the AI cited six fake cases. He then presented these cases to the court as real precedents, without verifying their authenticity or accuracy.

The fake cases were discovered by the defense lawyers, who could not find any records of them in the legal databases. They then alerted the judge, who ordered Schwartz to explain his sources. Schwartz then admitted that he had used ChatGPT to generate the cases and that he had no intention to deceive the court or act in bad faith. He claimed that he was unaware of the nature and limitations of ChatGPT, and that he had learned about it from his college-age children.

The judge, P. Kevin Castel, was not convinced by Schwartz's explanation. He ruled that Schwartz had acted in bad faith and had misled the court by submitting false and unsupported information. He also found that Schwartz had ignored several red flags that should have alerted him to the fact that the cases were fake, such as their nonsensical names, dates, and citations. He imposed a joint $5,000 fine on Schwartz and his co-counsel, Peter LoDuca, who had taken over the case when it moved to a different jurisdiction. He also ordered them to reach out to the judges mentioned in the fake cases with information about the situation.

Those previous three paragraphs, by the way, were written by a version of GPT-4 with an internet connection. And they are almost right. According to news reports, there were more than six fake cases; LoDuca did not take over the case but merely covered for Schwartz; and part of the reason for the fine was that the lawyers doubled down on the fake cases, far beyond their initial mistake. These small hallucinations are hard to catch because they are completely plausible. I was able to notice the issues only after an extremely close reading and research on every fact and sentence in the output. I may still have missed something (sorry, whoever fact-checks this chapter). But this is what makes hallucinations so perilous: it isn't the big issues you catch but the small ones you don't notice that can cause problems.

AI researchers have mixed opinions as to when, or even if, these problems will be solved. There is some reason to hope. As models advance, hallucination rates are dropping over time. For example, a study examining the number of hallucinations and errors in citations given by AI found that GPT-3.5 made mistakes in 98 percent of the cites, but GPT-4 hallucinated only 20 percent of the time. Additionally, technical tricks, like giving the AI a "backspace" key so it can correct and delete its own errors, seem to improve accuracy. So, while it may never go away, this problem will likely improve. Remember Principle 4: "Assume this is the worst AI you will ever use." Even today, with some experience, users can learn how to avoid forcing the AI into hallucinations and when careful fact-checking is necessary. And more discussion of this issue will prevent users like Schwartz from wholly relying on LLM-generated answers. That said, we need to be realistic about a major weakness, which means AI cannot easily be used for mission-critical tasks requiring precision or accuracy.

Hallucination does allow the AI to find novel connections outside the exact context of its training data. It also is part of how it can perform tasks that it was not explicitly trained for, such as creating a sentence about an elephant who eats stew on the moon, where every word should begin with a vowel. (The AI came up with: An elephant eats an oniony oxtail on outer orbit. ) This is the paradox of AI creativity. The same feature that makes LLMs unreliable and dangerous for factual work also makes them useful. The real question becomes how to use AI to take advantage of its strengths while avoiding its weaknesses. To do that, let us consider how AI "thinks" creatively.

05 AI 作为创造者

我们与 AI 合作的首要原则是始终邀请它参与讨论。我们已经讨论了与 AI 互动如何类似于与人交流和合作。那么，AI 更像什么样的人呢？它有哪些技能？它擅长做什么？要探讨这些问题，我们首先要面对 AI 很不擅长的事情。

AI 最大的问题也是它的一大优势：它会编造信息，即所谓的「幻觉」。大语言模型（LLM）通过根据训练数据中的统计模式，预测在提示后最可能出现的词语来工作。它不在乎这些词语是否真实、有意义或原创。它的目标是生成一个连贯且看起来合理的文本，让你满意。幻觉听起来很可信、符合上下文，因此难以分辨真假。

关于为什么 LLM 会产生幻觉，目前没有明确答案，影响的因素可能因模型而异。不同的 LLM 可能具有不同的架构、训练数据和目标。但在很多方面，幻觉是 LLM 工作方式的一个固有部分。它们不直接存储文本，而是存储哪些 Token 更有可能跟随其他 Token 的模式。这意味着 AI 实际上并不「知道」任何事情。它是即时编造答案的。而且，如果它过于严格地遵循训练数据中的模式，就会出现过拟合。过拟合的 LLM 可能无法处理新的或未见过的输入，并生成不相关或不一致的文本 —— 简而言之，它们的结果总是相似且缺乏新意。为了避免这种情况，大多数 AI 会在回答中增加一些随机性，但这也提高了产生幻觉的可能性。

除了技术原因，AI 的幻觉还可能来自它的源材料。这些材料可能存在偏见、不完整、矛盾，甚至错误，这些在第 2 章中已经讨论过。模型无法区分事实与观点、创意小说与现实、比喻语言与字面语言，以及不可靠的来源与可靠的来源。它可能会继承数据创建者、策划者和微调者的偏见。

当 AI 无法区分虚构与现实时，可能会产生有趣的结果。例如，数据科学家 Colin Fraser 注意到，当被要求在 1 到 100 之间选择一个随机数时，ChatGPT 有 10% 的几率回答「42」。如果它真的在随机选择一个数字，这个几率应该只有 1%。我的读者中那些科幻迷们可能已经猜到为什么 42 会更频繁地出现了。在 Douglas Adams 的经典喜剧《银河系漫游指南》中，42 是「生命、宇宙和一切的终极问题」的答案（留下了一个更大的问题：问题是什么？），这个数字已经成为互联网上的一个简短笑话。因此，Fraser 推测 AI 看到的 42 比其他数字多，这增加了它输出这个数字的可能性 —— 即使它实际上是在给你一个随机答案。

这些技术问题变得更加复杂，因为 AI 依靠的是模式，而不是数据储备来生成答案。如果你让 AI 给出一个引用或引文，它会根据所学数据之间的联系来生成这个引用，而不是从记忆中提取。如果引用是著名的，比如「八十七年前」，AI 会正确地补充道：「…… 我们的先辈在这片大陆上创建了一个新国家，这个国家以自由为基础，奉行人人生而平等的信念。」这是因为 AI 通过多次看到这些联系，能够预测出下一个词。但如果是一些不太常见的内容，比如我的传记，AI 就可能会填补一些似是而非的内容，比如 GPT-4 坚持认为我有计算机科学的本科学位。任何需要精确回忆的内容都可能导致错误，尽管如果 AI 能使用外部资源，如网络搜索，情况可能会有所改变。

你无法通过询问 AI 来弄清它为什么会生成这些错误。它并没有意识到自己的操作过程。因此，如果你要求它解释自己，AI 看起来会给出一个合理的答案，但这与生成原始结果的过程无关。系统没有办法解释其决策，甚至不知道这些决策是什么。相反，它只是生成它认为你想要的回答。大语言模型通常不会在信息不足时说「我不知道」，而是会自信地给出一个答案。

2023 年，LLM 出现幻觉的一个著名案例发生在一名名叫 Steven A. Schwartz 的律师身上。他在为一起针对航空公司的个人伤害诉讼准备法律简报时，使用了 ChatGPT 进行法庭文件的研究；结果，AI 提供了六个虚假的案例。Schwartz 没有核实这些案例的真实性或准确性，就将它们作为真实案例提交给法庭。

辩护律师在法律数据库中找不到这些虚假案例的记录，随即通知了法官。法官要求 Schwartz 解释他的资料来源。Schwartz 承认他使用了 ChatGPT 来生成这些案例，并表示他无意欺骗法庭或恶意行事。他声称自己不了解 ChatGPT 的性质和局限性，并表示是从正在上大学的孩子那里得知的。

法官 P. Kevin Castel 对 Schwartz 的解释不予采纳。他认为 Schwartz 恶意行事，通过提交虚假且无依据的信息误导了法庭。法官还指出，Schwartz 忽略了几个明显的警示信号，这些信号本应提醒他这些案例是假的，比如荒谬的名字、日期和引文。最终，他对 Schwartz 及其共同律师 Peter LoDuca 处以 5,000 美元的联合罚款，后者在案件移交到其他司法管辖区时接手此案。法官还要求他们联系虚假案例中提到的法官并告知这一情况。

前面三个段落是由一个连接互联网的 GPT-4 版本编写的。虽然它们看起来几乎正确，但根据新闻报道，假案的数量超过了六起；LoDuca 并没有接手案件，而只是为 Schwartz 顶替；律师们被罚款的部分原因是他们在假案上不断坚持，远远超出了最初的错误。这些小错误很难发现，因为它们看起来非常可信。我是在对每个事实和句子进行极其仔细的阅读和研究后才注意到这些问题的，但我可能仍然遗漏了一些（抱歉，给核查这一章的人添麻烦了）。这正是这些幻觉危险的地方：大问题容易发现，而那些细小的不易察觉的问题才会引发麻烦。

AI 研究人员对这些问题何时，甚至是否能被解决，意见不一。不过，还有一些希望。随着模型的不断进步，幻觉率正在逐渐下降。例如，一项研究发现，GPT-3.5 在 98% 的引用中存在错误，而 GPT-4 仅有 20% 的引用中出现幻觉。此外，给 AI 增加「退格」功能，让它可以自己纠正和删除错误，似乎也能提高准确性。因此，虽然这个问题可能无法完全消除，但有望逐步改善。记住原则 4：「假设这是你用过的最差的 AI。」即使在今天，有经验的用户也可以学会避免让 AI 产生幻觉，并知道何时需要仔细核对事实。而对这个问题的更多讨论将避免用户像 Schwartz 那样完全依赖大语言模型生成的答案。总之，AI 目前还不能轻易用于需要高度精确或准确的关键任务。

幻觉现象确实让 AI 能够在其训练数据之外找到新的联系。这也是它能执行一些未明确训练任务的原因，比如创建一个关于大象在月球上吃炖菜的句子，而且每个单词都要以元音开头。（AI 给出的句子是：An elephant eats an oniony oxtail on outer orbit.）这体现了 AI 创造力的悖论。大语言模型在处理事实工作时的不可靠性和危险性，恰恰也是它们有用的原因。关键在于如何利用 AI 的优势，规避其劣势。为此，我们需要理解 AI 是如何「创造性思考」的。

### Automatic Creativity

Given the history of automation, many people would have predicted that the first tasks AI would be good at would be boring, repetitive, and analytical. Those are usually the first tasks to be automated in any wave of new technology, from steam power to robots. As we have seen, however, that is not the case. Large Language Models are excellent at writing, but the underlying Transformer technology also serves as the key for a whole set of new applications, including AI that makes art, music, and video. As a result, researchers have argued that it is the jobs with the most creative tasks, rather than the most repetitive, that tend to be most impacted by the new wave of AI.

This tends to make us uncomfortable: After all, how can AI, a machine, generate something new and creative? The issue is that we often mistake novelty for originality. New ideas do not come from the ether; they are based on existing concepts. Innovation scholars have long pointed to the importance of recombination in generating ideas. Breakthroughs often happen when people connect distant, seemingly unrelated ideas. To take a canonical example, the Wright brothers combined their experience as bicycle mechanics and their observations of the flight of birds to develop their concept of a controllable plane that could be balanced and steered by warping its wings. They were not the inventors of the bicycle, the first to observe birds' wings, or even the first people to try to build an airplane. Instead, they were the first to see the connections between these concepts. If you can link disparate ideas from multiple fields and add a little random creativity, you might be able to create something new.

LLMs are connection machines. They are trained by generating relationships between tokens that may seem unrelated to humans but represent some deeper meaning. Add in the randomness that comes with AI output, and you have a powerful tool for innovation. The AI seeks to generate the next word in a sequence by finding the next likely token, no matter how weird the previous words were. So it should be no surprise that the AI can come up with novel concepts with ease. I asked AI to: Find me business ideas that would incorporate fast food, patent 6,604,835 B2 [which turned out to be for a lava lamp that included bits of crystal] , and 14th century England.

It suggested:

A medieval-themed fast-food restaurant that serves burgers, fries, and shakes in a castle-like setting, with staff dressed as knights, princesses, and jesters. The restaurant could use patent 6,604,835 B2 to create decorative lava lamps with gems or coins floating in them, to add some sparkle and ambiance to the dining area. The lava lamps could also be sold as souvenirs or gifts to customers. This idea could appeal to families with children, history buffs, or anyone looking for a fun and unique dining experience.

You may hate this idea (or love it, depending on your tolerance for lava lamp–centric restaurants), but it somehow made sense out of the three unrelated ideas I gave it, and if I didn't like that one, it would be happy to generate many more. And while I am not sure I want to quit my job to start Lava Lampshire, as the AI suggested I name my restaurant, this sort of response does exhibit a level of creativity. In fact, by many of the common psychological tests of creativity, AI is already more creative than humans.

One such test is known as the Alternative Uses Test (AUT). This measures an individual's ability to come up with a wide variety of uses for a common object. In this test, a participant is presented with an everyday object, such as a paper clip, and is asked to come up with as many different uses for the object as possible. For example, a paper clip can hold papers together, pick locks, or fish small objects out of tight spaces. The AUT is often used to evaluate an individual's ability to think divergently and to come up with unconventional ideas.

You can try the AUT now: Come up with creative ideas for using a toothbrush that does not involve brushing your teeth. Make them as different from each other as possible. You have two minutes. I'll wait.

Time's up.

How many did you come up with? Between 5 and 10 is a typical number. I asked an AI to do exactly the same task and it came up with 122 ideas in two minutes (and the version of AI that I used is likely far slower than what is available when you are reading this book). And while some ideas do share similarities ("use it as a brush to get dirt off mushrooms" and "use it as a tool to brush dirt off fruits"), there are also a lot of interesting ideas, from sculpting fine textures in frosting to applying it as a miniature drumstick ("perfect for a dollhouse drum set").

Are these original ideas? It is often very hard to tell. The AI is not explicitly searching a database of ideas; instead, it relies on its training to find connections, some of which certainly existed before. In my web searches, I found one 1965 picture of a man from Scotland playing a cake tin with toothbrushes—but there is no way to know whether that was part of the training of the AI or not. This is part of the concern about using AI for creative work; since we can't easily tell where the information comes from, the AI may be using elements of work that might be copyrighted or patented or just taking someone's style without permission. This is especially true for image generation, where it is very possible for an AI to closely reproduce a work "in the style of Picasso" or "inspired by Banksy" that has many of the features of the artist without any of the human meaning behind it. We will return to this question of art and meaning later, but it is worth considering a more subjective standard: Do we think the output of AI art is original, compared to what a human can do?

A recent paper by Jennifer Haase and Paul Hanel did just that, having humans blindly judge the creativity of AIs compared to humans in the AUT. After testing AI and 100 people on various objects, ranging from balls to pants, they found the GPT-4 model outperformed all but 9.4 percent of humans tested in generating creative ideas, as judged by other humans. Given that GPT-4 was the latest model tested, and it was much better than previous AI models, it might be expected that the creativity of AIs could continue to grow over time.

Of course, there are other creativity tests as well. A popular one is the remote associates test (RAT). This test asks people to find the common word that connects a set of three seemingly unrelated words. For example, pine , crab , and sauce are connected by the word apple . (Try one: What word connects cream , skate , and water ? The AI got it right.) Unsurprisingly, as a connection machine, AI usually maxes out this test, too.

While these psychological tests are interesting, human creativity tests aren't necessarily definitive. There is always the chance that the AI has previously been exposed to the results of similar tests and is just repeating answers. And, of course, psychological testing is not necessarily proof that AI can actually come up with useful ideas in the real world. But we have evidence that AI is actually quite good at practical creativity as well.

自动化的创造力

从自动化的发展历史来看，许多人会预测 AI 首先擅长的是那些无聊、重复和分析性的任务。通常在每次新技术浪潮中，最先被自动化的任务都是这些，从蒸汽动力到机器人。然而，实际情况并非如此。大语言模型在写作方面表现出色，而其背后的 Transformer 技术也成为一系列新应用的核心，包括 AI 创作艺术、音乐和视频。因此，研究人员认为，这一波 AI 技术对创造性任务影响最大，而不是对重复性任务。

这让我们感到有些不安：毕竟，AI 作为一台机器，怎么可能创造出新颖又有创意的东西呢？问题在于我们常常把新颖性误认为是原创性。新想法并不是凭空产生的；它们建立在已有的概念之上。创新学者们早就指出，重组在产生新想法中起着关键作用。当人们把远离且看似不相关的想法联系起来时，往往会产生突破性的进展。举一个经典的例子，莱特兄弟把他们作为自行车机械师的经验和对鸟类飞行的观察结合起来，提出了一个通过扭曲机翼来平衡和操控的可控飞机的概念。他们既不是自行车的发明者，也不是第一个观察鸟类翅膀的人，更不是第一个尝试制造飞机的人。而是第一个发现这些概念之间联系的人。如果你能把来自不同领域的想法联系起来，再加上一点随机的创意，你也许就能创造出一些新的东西。

大语言模型（LLMs）是连接概念的机器。它们通过生成 Token 之间的关系进行训练，这些关系在人类看来可能毫不相关，但实际上代表了更深层次的联系。再加上 AI 输出的随机性，你就拥有了一个强大的创新工具。AI 寻找序列中下一个最可能出现的 Token，无论前面的词看起来多么离奇。因此，AI 能轻松生成新颖的概念也就不足为奇了。我让 AI 为我找出结合快餐、专利 6,604,835 B2（结果发现这是一个包含水晶碎片的熔岩灯）和 14 世纪英格兰的商业创意。

它建议：

一个中世纪风格的快餐店，提供汉堡、薯条和奶昔，店内装饰如同城堡，员工打扮成骑士、公主和小丑。餐馆可以利用专利 6,604,835 B2 制作装饰性的熔岩灯，内含浮动的宝石或硬币，为用餐区增添一些闪耀和氛围。这些熔岩灯还可以作为纪念品或礼物出售给顾客。这个创意可能会吸引有孩子的家庭、历史爱好者，或任何想要寻找有趣独特用餐体验的人。

你可能会讨厌这个想法（或者喜欢它，这取决于你对熔岩灯主题餐馆的接受程度），但在我提供的三个不相关的创意中，这个看起来还算合理。如果我不喜欢这个，AI 也会很乐意提供更多的创意。虽然我不确定是否要辞掉工作去开设 Lava Lampshire（AI 推荐的餐馆名字），但这种回应确实展示了 AI 的创造力。事实上，根据许多常见的心理学创造力测试，AI 已经比人类更具创造力了。

其中一个测试叫做替代用途测试（Alternative Uses Test, AUT)。这个测试衡量一个人能提出多少种常见物品的不同用途。在测试中，参与者会被给予一个日常物品，比如回形针，并被要求提出尽可能多的不同用途。例如，回形针可以用来固定纸张、开锁，或者从狭小空间中取出小物件。AUT 经常用来评估一个人的发散思维和提出非传统想法的能力。

你现在可以尝试一下 AUT：想出使用牙刷的创意点子，但不要涉及刷牙。尽量让这些用途彼此不同。你有两分钟。我等你。

时间到。

你能想到多少点子？通常在 5 到 10 个之间是一个典型的数字。我让一个 AI 完全做同样的任务，它在两分钟内想出了 122 个点子（而且我用的 AI 版本可能比你读这本书时能用的版本要慢得多）。虽然有些点子确实有相似之处（如「用它刷掉蘑菇上的泥土」和「用它清理水果上的泥土」），但也有很多有趣的点子，比如在糖霜上雕刻细纹，或者将其用作玩具屋的微型鼓槌。

这些点子是原创的吗？通常很难判断。AI 并不是在明确地搜索一个点子数据库；相反，它依赖于其训练来找到某些联系，其中一些联系肯定是先前存在的。在我的网络搜索中，我发现了一张 1965 年的照片，里面有一个苏格兰男子用牙刷敲击蛋糕罐 —— 但无法确定这是否是 AI 训练的一部分。这也是使用 AI 进行创意工作的担忧之一；因为我们无法轻易判断信息的来源，AI 可能会使用一些可能受版权或专利保护的元素，或者未经许可地采用某人的风格。这在图像生成中特别明显，AI 很可能「以毕加索的风格」或「受 Banksy 启发」来近似再现一个作品，但却没有任何人类背后的意义。我们稍后会讨论艺术和意义的问题，但值得考虑一个更主观的标准：我们认为 AI 艺术的输出相比于人类创作的是否原创？

Jennifer Haase 和 Paul Hanel 最近发表了一篇论文，让人类在不知道测试对象身份的情况下，对 AI 和人类在 AUT 测试中的创造力进行评估。经过对各种物体（从球到裤子）的测试后，他们发现 GPT-4 模型在生成创意方面优于 90.6% 的受测人类。鉴于 GPT-4 是最新的模型，并且远超以前的 AI 模型，我们可以预见 AI 的创造力将继续提升。

当然，还有其他的创造力测试。一种常见的是远距离联想测试（RAT)。这个测试要求人们找到连接三组看似不相关词语的共同词语。例如，松树（pine)、蟹（crab）和酱汁（sauce）都可以通过苹果（apple）连接起来。（试试这个：什么词语连接奶油（cream)、滑冰（skate）和水（water)？AI 答对了。）作为一种擅长联想的机器，AI 通常在这个测试中也表现出色。

尽管这些心理测试很有意思，但它们并不一定是评估创造力的最终标准。AI 可能以前看到过类似测试的答案，只是在重复它们。另外，心理测试也不能证明 AI 能在现实世界中提出有用的创意。然而，我们确实有证据表明，AI 也在实用创造力方面表现出色。

### Out-Inventing Humans

I know this is true, because they are out-inventing students in one of Wharton's most well-known innovation classes. It's a well-worn joke that MBAs are not necessarily the most innovative, but Wharton has generated a ton of start-ups, and many of them had their start in the innovation class run by professors Christian Terwiesch and Karl Ulrich. Along with their colleagues Karan Girotra and Lennart Meincke, they staged an idea generation contest to come up with the best products for a college student that would cost $50 or less. It was the GPT-4 AI against 200 students. The students lost, and it wasn't even close. AI was faster, obviously, generating a lot more ideas than the average person in any given time. But it was also better. When they asked sets of human judges whether they would be interested enough in the ideas to buy the product if it was ever made, AI ideas were more likely to attract financial interest. The degree of the victory was startling: of the 40 best ideas rated by the judges, 35 came from ChatGPT.

We aren't completely out of an innovation job, however, as other studies find that the most innovative people benefit the least from AI creative help. This is because, as creative as the AI can be, without careful prompting, the AI tends to pick similar ideas every time. The concepts may be good, even excellent, but they can start to seem a little same-y after seeing enough of them. Thus, a large group of creative humans will usually generate a wider diversity of ideas than the AI. All of this suggests that humans still have a large role to play in innovation . . . but that they would be foolish not to include AI in that process, especially if they don't consider themselves highly creative.

As should be obvious, some people are uniquely good at generating ideas and can apply this ability in almost every context. Indeed, recent research has shown that the " equal-odds rule" is true for creativity, which is that very creative people generate both more ideas and better ideas than other folks. Coming up with lots of ideas was not correlated with intelligence; it seems to be a skill some people have and others do not. Until the past year, no prosthetic or approach would help people who were not good at generating a lot of ideas to do better (besides coffee, which genuinely increases creativity). We are now in a period during which AI is creative but clearly less creative than the most innovative humans—which gives the human creative laggards a tremendous opportunity. As we saw in the AUT, generative AI is excellent at generating a long list of ideas. From a practical standpoint, the AI should be invited to any brainstorming session you hold.

So how should we use AI to help generate ideas? Fortunately, the papers, and other research on innovation, have some good suggestions. When you do include AI in idea generation, you should expect that most of its ideas will be mediocre. But that's okay—that's where you, as a human, come into the equation. You are looking for ideas that spark inspiration and recombination, and having a long list of generated possibilities can be an easier place to start for people who are not great at coming up with ideas on their own.

So how do we do it? Let's imagine that we want to come up with 20 ideas for marketing slogans for a new mail-order cheese shop. The AI can generate those for us, but we will get even better quality if we remember the principle of telling AI who it is: You are an expert at marketing. When asked to generate slogan ideas you come up with ideas that are different from each other, clever, and interesting. You use clever wordplay. You try not to repeat themes or ideas. Come up with 20 ideas for marketing slogans for a new mail-order cheese shop, make them different from each other, and make them clever and creative.

"A Brie-lliant Way to Your Doorstep!"

"Cheese the Day, Right at Your Door."

"Life's Better with a Slice of Our Gouda."

"Unlock the Melt, Post by Post."

"Savor the Curd, Delivered to Your Turf!"

"Delivered with Glee, Aged to a T."

"From Our Cave to Your Crave."

"Rethink Cheese—Mailed for Your Ease."

"Your Passport to Global Fromage."

"A Parcel of Pleasure, from Cheddar to Treasure."

"We've Got Your Cheese Needs Sealed and Delivered."

"We Make You Feta, One Package at a Time."

"Where Dairy Meets Delivery."

"Every Letter Is Feta—the Cheesier, the Better."

"Cut the Queue, Get the Blue."

"Say Cheese and We'll Mail It, Please."

"Cheesy Love, from Our Box to Your Block."

"No Whey We're Ordinary, Get Your Cheesy Story."

"Quality Aged, Perfectly Packaged."

"Embrace the Rind, Love Delivered in Kind."

And . . . most of the ideas are terrible, and some are incoherent, and a few have potential (and bad puns). It took us no time to generate 20 ideas, and it is costless to skim them to see if they inspire better ideas. I am a little bit partial to "Cut the Queue, Get the Blue" and "From Our Cave to Your Crave." But if none of those sparked your interest, ask for another 20 with different prompting. Or ask it to consider a particular customer (a cheese shop that will appeal to novices or children) or to change the context of the prompt in other ways. Tirelessly generating concepts is something AIs are uniquely good at.

Another key aspect of idea generation is to embrace variance. Research shows that, to find good novel ideas, we likely have to come up with many bad novel ideas because most new ideas are pretty bad. Fortunately, we are good at filtering out low-quality ideas, so if we can generate novel ideas quickly and at low cost, we are more likely to generate at least some high-quality gems. So we want the AI answers to be weird.

The AI will not naturally deliver novelty (as we discussed above, it tends to give the crowd-pleasing "average" answer that is most likely from its training data), but we can make it do so with a little work. We need to push the AI from an average answer to a high-variance, weird one. We can do this again by telling the AI who it is. Force it to give you less likely answers, and you will find more original combinations. Imagine you are opening a coffee shop. You might want to ask: You are an expert at problem-solving and idea generation. When asked to solve a problem, you come up with novel and creative ideas. Tell me 10 detailed ways a superhero might make espresso and how they might speculatively get the same effects in a new product.

Nightcrawler —Using his teleportation power, he could transport himself to Italy to learn firsthand from Italian baristas, and teleport back with a freshly made espresso. A new product could connect users to virtual coffee workshops with expert baristas around the world for an authentic experience.

Scarlet Witch —Using her chaos magic, she could conjure up the most amazing cup of espresso from nothing. A new product could offer a "Surprise Me" feature where the machine randomly selects from a range of beans, grinds, and brew methods to create an unexpected and delicious espresso.

The results can be interesting as sources of inspiration (I like the idea of the virtual coffee workshops!) but still require a human in the loop to filter and select the best ideas. Yet it allows us to outsource some of the most difficult aspects of creativity. When I started requiring students to use these methods to generate ideas for start-ups in my entrepreneurship class, I found that the ideas' quality increased tremendously from the prior year. I encountered novel business ideas rather than seeing the same few ideas over and over again (better ways to order drinks at bars, companies that would store your stuff between semesters—they are students after all). Having the AI at the table was a cheap source of additional innovation and a new perspective.

超越人类发明

我知道这是真的，因为在沃顿商学院最著名的创新课程中，AI 已经超越了学生。尽管有个老生常谈的笑话说 MBA 并不是最具创新力的，但沃顿商学院培养了大量的初创公司，其中许多都是在由 Christian Terwiesch 和 Karl Ulrich 教授主持的创新课程中起步的。与他们的同事 Karan Girotra 和 Lennart Meincke 一起，他们举办了一场创意生成比赛，要求提出成本不超过 50 美元的大学生最佳产品。这场比赛是在 GPT-4 AI 和 200 名学生之间进行的，结果学生完败。显然，AI 的速度更快，能在短时间内生成更多创意。而且，AI 的创意质量也更高。当一组人类评委被问及是否会购买这些创意产品时，AI 的创意更容易吸引他们的兴趣。比赛结果令人惊讶：评审团评选出的 40 个最佳创意中，有 35 个来自 ChatGPT。

不过，我们并没有完全失去创新的角色，因为其他研究发现，最具创新能力的人从 AI 的创意帮助中受益最少。这是因为尽管 AI 可以非常有创意，但如果没有精心提示，它往往会选择类似的想法。虽然这些概念可能很好，甚至出色，但看到多了之后会觉得有些雷同。因此，一个由大量有创造力的人类组成的团队通常会比 AI 生成更多样化的创意。这表明，人类在创新中仍然扮演重要角色…… 但如果他们认为自己不够有创意，不在过程中引入 AI 就显得不明智了。

显然，有些人特别擅长产生想法，并能在几乎所有情况下运用这种能力。事实上，最近的研究表明，「均等几率规则」在创造力方面是成立的，也就是说，非常有创造力的人不仅产生更多的想法，而且这些想法也更好。产生大量想法与智力无关，这似乎是一些人具备的技能，而另一些人则没有。直到去年之前，还没有任何方法或工具可以帮助那些不擅长产生大量想法的人提高创造力（除了咖啡，它确实能增加创造力）。现在，我们处在一个 AI 逐渐变得富有创造力的时期，尽管它的创造力显然不及最具创新性的人类。这给了那些在创造力上落后的人一个巨大的机会。正如我们在 AUT（替代用途测试）中看到的，生成式 AI 在生成大量想法方面非常出色。从实际角度来看，你进行的任何头脑风暴会议都应该邀请 AI 参加。

那么，我们应该如何利用 AI 来帮助生成想法呢？幸运的是，相关论文和其他关于创新的研究提供了一些很好的建议。当你在生成想法时加入 AI，你应该预期到它的大多数想法会比较平庸。但这没关系 —— 这就是你，作为人类，发挥作用的地方。你需要寻找那些能够激发灵感和重新组合的想法，而拥有一长串生成的可能性列表，可以为那些不擅长独自产生想法的人提供一个更容易的起点。

所以我们该怎么做呢？假设我们需要为一家新开的邮购奶酪店想出 20 个营销口号。AI 可以帮我们生成这些口号，但是如果我们告诉 AI 它的角色 —— 你是一位营销专家，擅长提出独特、聪明、有趣的口号，避免重复主题或想法。请为新的邮购奶酪店想出 20 个不同且有创意的营销口号。

"A Brie-lliant Way to Your Doorstep!"

"Cheese the Day, Right at Your Door."

"Life's Better with a Slice of Our Gouda."

"Unlock the Melt, Post by Post."

"Savor the Curd, Delivered to Your Turf!"

"Delivered with Glee, Aged to a T."

"From Our Cave to Your Crave."

"Rethink Cheese—Mailed for Your Ease."

"Your Passport to Global Fromage."

"A Parcel of Pleasure, from Cheddar to Treasure."

"We've Got Your Cheese Needs Sealed and Delivered."

"We Make You Feta, One Package at a Time."

"Where Dairy Meets Delivery."

"Every Letter Is Feta—the Cheesier, the Better."

"Cut the Queue, Get the Blue."

"Say Cheese and We'll Mail It, Please."

"Cheesy Love, from Our Box to Your Block."

"No Whey We're Ordinary, Get Your Cheesy Story."

"Quality Aged, Perfectly Packaged."

"Embrace the Rind, Love Delivered in Kind."

而且…… 大多数想法都很糟糕，有些甚至不连贯，但也有一些有潜力（还有些糟糕的双关语）。我们花了很少的时间就生成了 20 个想法，浏览这些想法寻找灵感几乎不费什么成本。我个人比较喜欢「Cut the Queue, Get the Blue」和「From Our Cave to Your Crave」。如果这些都没有引起你的兴趣，可以用不同的提示再生成 20 个。或者你可以让它考虑特定的客户（比如一个吸引新手或儿童的奶酪店），或者用其他方式改变提示的背景。AI 在无休止地生成概念方面有独特的优势。

想法生成的另一个关键是接受多样性。研究表明，为了找到好的新想法，我们可能需要提出很多糟糕的新想法，因为大多数新想法都不太好。幸运的是，我们擅长过滤掉低质量的想法，所以如果我们能快速且低成本地生成新想法，我们更有可能产生一些高质量的杰作。因此，我们希望 AI 的回答是奇特的。

AI 不会自然地提供新颖的想法（如前所述，它倾向于给出最符合其训练数据的「平均」答案），但我们可以通过一些方法让它做到这一点。我们需要推动 AI 从一个普通答案走向一个高变异、奇怪的答案。我们可以通过告诉 AI 它的身份来实现这一点。逼迫它给出不太可能的答案，你会发现更多原创的组合。想象你正在开一家咖啡店。你可能会问：你是解决问题和生成想法的专家。当被要求解决问题时，你会想出新颖且有创意的想法。告诉我超级英雄可能制作浓缩咖啡的 10 种详细方法，以及他们可能在新产品中如何实现同样效果的方法。

Nightcrawler — 利用他的瞬间移动能力，Nightcrawler 可以瞬间前往意大利，亲自向意大利咖啡师学习，并带回一杯新鲜制作的浓缩咖啡。一个新产品可以将用户连接到世界各地的顶级咖啡师的虚拟咖啡工作坊，带来真实的体验。

Scarlet Witch — 利用她的混沌魔法，Scarlet Witch 可以凭空变出最惊人的浓缩咖啡。一个新产品可以提供「惊喜我」功能，机器会随机选择不同的咖啡豆、研磨和冲泡方法，创造出意想不到的美味浓缩咖啡。

这些创意可以作为灵感的来源（我特别喜欢虚拟咖啡工作坊的想法！），但仍然需要人为筛选和选择最佳创意。这使我们能够外包一些最困难的创造性工作。当我在创业课上要求学生使用这些方法为初创公司生成创意时，我发现创意的质量比前一年有了显著提高。我看到了许多新颖的商业创意，而不再是重复的老想法（例如，更好的酒吧饮品订单方式、在学期之间储存物品的公司 —— 毕竟他们是学生）。让 AI 参与其中不仅成本低廉，还能带来额外的创新和新的视角。

### Adding AI to Creative Work

Upon closer inspection, a surprisingly large amount of work is actually creative work in the form that AI is good at. Situations in which there is no right answer, where invention matters and small errors can be caught by expert users, abound. Marketing writing, performance reviews, strategic memos—all these are within the capability of AI because they have both room for interpretation and are relatively easily fact-checked. Plus, as many of these document types are well represented in the AI training data, and are rather formulaic in approach, AI results can often seem better than that of a human and can be produced faster as well.

We can see these results in a study by economists Shakked Noy and Whitney Zhang from MIT, examining how ChatGPT could transform the way we work. The researchers asked the participants to write different types of documents based on their roles and scenarios. For example, the participants who were marketers had to create a press release for a fictional product; the participants who were grant writers had to craft a cover letter for a grant proposal; the participants who were managers and HR professionals had to compose a long email for the whole company on a delicate issue; the participants who were data analysts had to design an analysis plan in a code-notebook format; and the participants who were consultants had to produce a short report based on three given sources. Some were assigned to use AI and some were not. The results were nothing short of astonishing. Participants who used ChatGPT saw a dramatic reduction in their time on tasks, slashing it by a whopping 37 percent. Not only did they save time, but the quality of their work also increased as judged by other humans. These improvements were not limited to specific areas; the entire time distribution shifted to faster work, and the entire grade distribution shifted to higher quality. The study also showed that AI teammates helped reduce productivity inequality. Participants who scored lower on the first round without AI assistance benefited more from using ChatGPT, narrowing the gap between low and high scorers.

Even things that don't initially appear to be creative can be. AI works tremendously well as a coding assistant because writing software code combines elements of creativity with pattern matching. Again, early research suggests big impacts. When researchers from Microsoft assigned programmers to use AI, they found an increase of 55.8 percent in productivity for sample tasks. AI can even turn nonprogrammers into coders, of a sort. I can't write code in any modern language, but I have had AI write a dozen programs for me. The idea of programming by intent, by asking the AI to do something and having it create the code, is likely to have significant impacts in an industry whose workers earn a total of $464 billion a year. One fun, if less economically significant, impact: the lights in my office now flash in different colors when I yell "party"—the AI wrote the code to do that, walked me through setting up accounts with various cloud services companies to make the program work, and debugged problems when they occurred.

AI is also good at summarizing data since it is adept at finding themes and compressing information, though at the ever-present risk of error. As an example, I added tiny science fiction references to The Great Gatsby— in the middle of the text, Daisy refers to her iPhone, and one of Gatsby's gardeners uses a laser-powered lawn mower. I asked the AI to tell me if anything seemed unusual. It found both errors but also hallucinated a third (a mention of texting that was not there). Amusingly, it also pointed out what it found to be an unconvincing claim: There were 40 acres of land at Gatsby's mansion, unlikely in densely populated Long Island .

This ability to do high-quality analysis and summarization is not just useful for the topic of Gatsby's fictional real estate; it has real financial implications as well. A study by researchers at the University of Chicago used ChatGPT to analyze the conference-call transcripts of large companies, asking the AI to summarize the risks that companies faced. Risk obviously plays a big role in stock market returns, so financial firms have spent a lot of time and money using specialized, older forms of machine learning to try to identify the uncertainties associated with various corporations. ChatGPT, without any specialized stock market knowledge, tended to outperform these more specialized models, working as a "powerful predictor of future stock price volatility." In fact, it was the ability of the AI to apply more generalized knowledge of the world that made it such a good analyst, since it could put the risks discussed in conference calls into a larger context. The issue of hallucination was less important here, because the AI simply had to beat the best computer systems for accuracy, which it was able to do.

Of course, the unresolved question is whether AI is more or less accurate than humans, and whether its extended abilities to do creative, human work makes up for its errors. The trade-offs are often surprising. A paper published in the Journal of the American Medical Association: Internal Medicine asked ChatGPT-3.5 to answer medical questions from the internet, and had medical professionals evaluate both the AI's answers and an answer provided by a doctor. The AI was almost 10 times as likely to be rated as very empathetic than the results provided by the human, and 3.6 times as likely to be rated as providing good-quality information compared to human doctors. AIs can perform useful tasks that may not be considered traditionally creative work, and the coming months and years will likely see even more applications.

But what happens when AI touches on the most deeply human creative tasks—art? Artists have been reacting with alarm to the rapid encroachment of AI tools. Some of that concern is aesthetic. "A grotesque mockery of what it is to be human" is how famed musician Nick Cave described an AI attempt to create lyrics "in the style of a Nick Cave song." Animator Hayao Miyazaki called AI art "an insult to life itself." When one artist won a competition with an AI-generated piece, it caused an outcry, but the winning artist defended the AI's work. " Art is dead, dude. It's over. A.I. won. Humans lost."

The meaning of art is an old debate and one unlikely to be resolved in this book or any other. And the anxiety that artists face may soon be felt by many other professions as AI overlaps with their jobs. Yet this may turn out to be a reinvigoration of creativity and art rather than its collapse.

AI is trained on vast swaths of humanity's cultural heritage, so it can often best be wielded by people who have a knowledge of that heritage. To get the AI to do unique things, you need to understand parts of the culture more deeply than everyone else using the same AI systems. So now, in many ways, humanities majors can produce some of the most interesting "code." Writers are often the best at prompting AI for written material because they are skilled at describing the effects they want prose to create ("end on an ominous note," "make the tone increasingly frantic"). They are good editors, so they can provide instructions back to the AI ("make the second paragraph more vivid"). They can quickly run experiments with audiences and styles by knowing many examples of both ("make this like something in The New Yorker ," "do this in the style of John McPhee"). And they can manipulate narrative to get the AI to think in the way they want. ChatGPT won't produce an interview between George Washington and Terry Gross, because such a scenario seems implausible. But if you convince it that George Washington might have had a time machine, it is happy to reply.

A similar phenomenon is happening in visual art. AI image generators have trained deeply on the past paintings and watercolors, architecture and photographs, fashion and historical images. Creating something interesting with AI requires you to invoke these connections to create a novel image. But what most people are actually creating with AI art tools is very different and much less ambitious. There is a lot of Star Wars art, a lot of fake photos of movie stars, some anime, cyberpunk, a lot of superheroes (especially Spider-Man), and, weirdly, a LOT of marble statues of celebrities. Given a machine that can make anything, we still default to what we know well.

But AI can do so many more interesting things! The AI can create a marble statue of Spider-Man, but it can also output a pretty amazing ukiyo-e woodblock Spider-Man, or Spider-Man in the style of Alphonse Mucha, or even images entirely unrelated to Spider-Man (gasp). But you need to know what to ask for. The result has been a weird revival of interest in art history among people who use AI systems, with large spreadsheets of art styles being passed among prospective AI artists. The more people know about art history and art styles in general, the more powerful these systems become. And people who respect art might be more willing to refrain from using AI in ways that ape the style of living, working artists. So a deeper understanding of art and its history can result not just in better images but also, hopefully, in more responsible ones.

Our new AIs have been trained on a huge amount of our cultural history and are using it to provide us with text and images in response to our queries. But there is no index or map to what they know and where they might be most helpful. Thus, we need people who have deep or broad knowledge of unusual fields to use AI in ways that others cannot, developing unexpected and valuable prompts and testing the limits of how they work. AI could catalyze interest in the humanities as a sought-after field of study, since the knowledge of the humanities makes AI users uniquely qualified to work with the AI.

仔细观察后，我们发现实际上有很多工作是 AI 擅长的创造性工作。很多情况下，没有标准答案，发明创造很重要，而小错误可以被专家用户发现。例如，市场营销文案、绩效评估和战略备忘录等任务都在 AI 的能力范围内，因为这些任务既有解释的空间，又相对容易核实。再加上这些文档类型在 AI 的训练数据中出现频率较高，且其写作方式较为程式化，AI 生成的结果往往比人类更好，而且速度更快。

麻省理工学院（MIT）的经济学家 Shakked Noy 和 Whitney Zhang 进行了一项研究，探讨了 ChatGPT 如何改变我们的工作方式。研究人员要求参与者根据各自的角色和情境撰写不同类型的文档。例如，营销人员要为一个虚构的产品撰写新闻稿；资助申请书撰写者要写一封资助申请书的封面信；经理和人力资源专业人员要为公司撰写一封关于敏感问题的长邮件；数据分析师要设计一个代码笔记本格式的分析计划；顾问要根据三份给定的资料写一份简短的报告。部分参与者使用了 AI，而另一部分没有。结果非常惊人。使用 ChatGPT 的参与者在完成任务的时间上减少了 37%。不仅节省了时间，他们的工作质量也得到了其他人的高度评价。这些改进不仅限于某个领域；整体的工作时间分布变得更快，评分分布也向更高质量转移。研究还发现，AI 智能体辅助有助于减少生产力的不平等。第一轮没有 AI 辅助时得分较低的参与者在使用 ChatGPT 后受益更大，缩小了低分和高分之间的差距。

即使是一些看起来不太需要创造性的事情，也可以变得很有创意。AI 作为编码助手非常高效，因为编写软件代码既需要创意也需要模式匹配能力。早期研究已经显示出显著的效果。例如，Microsoft 的研究人员发现，当程序员使用 AI 时，执行样本任务的生产率提高了 55.8%。AI 甚至可以让非程序员也能进行某种程度的编码。虽然我不能用现代编程语言写代码，但 AI 已经为我写了十几个程序。通过这样一种意图编程的方式，即通过指示 AI 执行某些任务并生成代码，可能对一个年收入总计 4640 亿美元的行业产生重大影响。有一个有趣但经济意义不大的例子：当我喊「派对」时，我办公室的灯会变换颜色闪烁 —— 这是 AI 为我编写的代码实现的，它还指导我设置各种云服务账户，并在出现问题时进行调试。

AI 在总结数据方面也很擅长，因为它能发现主题并压缩信息，尽管总是存在出错的风险。例如，我在《了不起的盖茨比》中加入了一些微小的科幻元素 —— 在文本中，黛西提到了她的 iPhone，而盖茨比的一个园丁使用了激光动力割草机。我让 AI 检查是否有任何不寻常的地方。它发现了这两个错误，但也虚构了一个额外的（提到短信的情节，这实际上并不存在）。有趣的是，它还指出了一个它认为不可信的说法：盖茨比的豪宅有 40 英亩的土地，这在人口密集的长岛上不太可能。

这种高质量的分析和总结能力不仅对 Gatsby 虚构的房地产话题有用，还具有实际的金融意义。芝加哥大学的研究人员使用 ChatGPT 分析大型公司的会议通话记录，并要求 AI 总结公司面临的风险。风险在股市回报中起着重要作用，因此金融公司花费大量时间和金钱，利用专门的旧机器学习模型来识别与不同公司相关的不确定性。尽管没有任何专门的股市知识，ChatGPT 通常表现优于这些更专业的模型，成为「未来股票价格波动的强大预测器」。实际上，AI 能够应用更广泛的世界知识，使其成为出色的分析师，因为它能将会议通话中讨论的风险置于更大的背景中。幻觉问题在这里不那么重要，因为 AI 只需在准确性上击败最好的计算机系统，而它确实做到了。

当然，尚未解决的问题是 AI 是否比人类更准确，以及它在进行创造性和人类工作的能力是否能弥补其错误。权衡往往出人意料。发表在《美国医学会杂志：内科》上的一篇论文让 ChatGPT-3.5 回答来自互联网的医学问题，并由医学专业人士评估 AI 的答案和医生的答案。与人类医生提供的结果相比，AI 被评为非常有同情心的概率几乎高出 10 倍，而且被评为提供优质信息的可能性是人类医生的 3.6 倍。AI 可以执行许多有用的任务，这些任务可能不被认为是传统的创造性工作，未来几个月和几年可能会看到更多的应用。

当 AI 涉及到最具人类创造性的任务 —— 艺术时，会发生什么呢？艺术家们对 AI 工具的迅速入侵感到震惊。其中一部分担忧来自于审美方面。著名音乐家 Nick Cave 将 AI 尝试创作「风格类似 Nick Cave 歌曲」的歌词称为「对人类本质的荒诞嘲弄」。动画师 Hayao Miyazaki 则认为 AI 艺术是「对生命本身的侮辱」。当一位艺术家凭借 AI 生成的作品赢得比赛时，引发了巨大争议，但这位获胜者为 AI 的作品辩护称：「艺术已死，兄弟。结束了。AI 赢了。人类输了。」

艺术的意义是一个古老的辩题，本书或任何其他书籍都不太可能解决这个问题。艺术家们的焦虑可能很快会蔓延到其他职业，因为 AI 开始与他们的工作重叠。然而，这或许不是艺术的终结，而是创意与艺术的一次新生。

AI 是在大量人类文化遗产上训练的，所以懂得这些文化遗产的人通常能更好地使用 AI。要让 AI 做出独特的事情，你需要比其他使用相同 AI 系统的人更深入地了解文化。因此，人文学科的学生在很多方面可以创作出最有趣的「代码」。作家往往最擅长提示 AI 生成书面材料，因为他们熟悉如何描述希望散文达到的效果（比如「以不祥的语气结尾」，「使语调越来越紧张」）。他们是优秀的编辑，能给 AI 提供修改建议（如「使第二段更加生动」）。通过了解各种风格的例子，他们可以快速进行风格和受众的实验（如「让这像《纽约客》中的文章」，「以 John McPhee 的风格写这段」）。他们还可以通过操纵叙事来引导 AI 按照他们的意图思考。ChatGPT 不会生成 George Washington 和 Terry Gross 之间的采访，因为这种情景看似不可能。但如果你说服它 George Washington 拥有一台时间机器，它就会乐意回应。

在视觉艺术中也有类似现象。AI 图像生成器在过去的绘画、水彩画、建筑、摄影、时尚和历史图像上进行了深度训练。用 AI 创作有趣的图像需要你调用这些联系来产生新颖的作品。但大多数人用 AI 艺术工具创作的内容却很单调且不太有野心。很多人创作星球大战艺术、电影明星的假照片、动漫、赛博朋克、超级英雄（尤其是蜘蛛侠）以及大量名人的大理石雕像。尽管有一台可以制作任何东西的机器，我们仍然习惯于创作熟悉的内容。

但是 AI 能做的有趣事情远不止这些！AI 不仅能生成蜘蛛侠的大理石雕像，还能制作出令人惊叹的浮世绘木版画版本的蜘蛛侠，或者是阿尔丰斯·穆夏风格的蜘蛛侠，甚至是完全与蜘蛛侠无关的图像。但你需要知道如何进行相关的请求。结果是，使用 AI 系统的人们对艺术史的兴趣重新燃起，大家在潜在的 AI 艺术家之间传递着各种艺术风格的电子表格。人们对艺术史和艺术风格了解得越多，这些系统就会变得越强大。而那些尊重艺术的人可能会更愿意避免使用 AI 模仿在世艺术家的风格。因此，深入理解艺术及其历史不仅可以创造出更好的图像，还能带来更负责任的作品。

我们的新 AI 已经在大量的文化历史数据上进行了训练，并使用这些数据来回应我们的查询，生成文本和图像。然而，目前没有任何索引或地图来显示它们掌握了什么知识以及在哪些方面最有用。因此，我们需要那些对某些特殊领域有深厚或广泛知识的人，以独特的方式使用 AI，开发出意想不到且有价值的提示，并测试其工作极限。AI 可能会激发人们对人文学科的兴趣，使其成为一个受欢迎的研究领域，因为人文学科的知识使 AI 用户在使用 AI 时具有独特的优势。

### The Meaning of Creative Work

If AI is already a better writer than most people, and more creative than most people, what does that mean for the future of creative work?

While we will discuss the job implications in the next chapter, some strong positives exist. Not everyone is a Nick Cave or Hayao Miyazaki (obviously) or even anywhere close to that level of talent. But many people want to express themselves creatively, and remarkably few feel they can. One survey asked a representative sample of people how many felt they were living up to their creative potential. Only 31 percent said they were. There is a lot of frustrated creative energy in the world.

To some extent, I have been one of them. I come from an artistic family—my mother is a painter, one sister is a graphic designer, and another makes Hollywood movies—but despite many lessons, I am not good at creating visual art. I have tried. Painting classes, drawing classes, online tutorials. I have enough training to know I am pretty mediocre. Fortunately, there are lots of other kinds of creative expressions that I can do reasonably well. I write (obviously) and design games, but visual art has never been a great skill of mine.

Until July 28, 2022. That is when I first got access to the AI art program Midjourney. I was almost instantly hooked by its power and spent that day creating artistic bar charts (look, I am an academic, charts are in our blood). I started posting them on Twitter. By the next day, over 20,000 people had liked the tweet thread. Academics told me that they printed out copies and hung them on their walls. I had made something other people enjoyed.

Was it art? Probably not—and that's a question for the philosophers anyway. But I know it is creative. I feel the thrill of creating something, that sense of flow when I am trying to create an image that only comes from intense engagement and focus. I often need to make and modify dozens of images to get one I like. Many experiments work out badly, yet there is still joy in developing prompts, feeding images back to the AI, and seeing what happens. I know there is skill involved. I have learned from more talented people who share their results, online documents, and tons of experimentation. I have gotten pretty good at it, and I know this because people who use these tools for the first time will not be able to achieve the same results. I also know that it is useful. I am making things other people like (and I still hire just as many artists as I used to, when I need careful new work done for projects). It may not be art, but it is creatively fulfilling and valuable. And it was something I was never able to do before.

These effects go beyond art. Generative AI is giving people new modes of expression and new languages for their creative impulses—sometimes literally. I have had students mention that they were not taken seriously because they were poor writers. Thanks to AI, their written materials no longer hold them back, and they get job offers off the strength of their experience and interviews. Since requiring AI in my classes, I no longer see badly written work at all. And as my students learn, if you work interactively with the AI, the outcome doesn't feel generic, it feels like a human did it.

That said, it would be naive to see only the upside here. Especially as AI work becomes easy to generate at the push of a button. I mean that literally, as every major office application and email client will include a button to help you create a draft of your work. It deserves capital letters: The Button.

When faced with the tyranny of the blank page, people are going to push The Button. It is so much easier to start with something than nothing. Students are going to use it to start essays. Managers will use it to start emails, reports, or documents. Teachers will use it when providing feedback. Scientists will use it to write grants. Concept artists will use it for their first draft. Everyone is going to use The Button.

The implications of having AI write our first drafts (even if we do the work ourselves, which is not a given) are huge. One consequence is that we could lose our creativity and originality. When we use AI to generate our first drafts, we tend to anchor on the first idea that the machine produces, which influences our future work. Even if we rewrite the drafts completely, they will still be tainted by the AI's influence. We will not be able to explore different perspectives and alternatives, which could lead to better solutions and insights.

Another consequence is that we could reduce the quality and depth of our thinking and reasoning. When we use AI to generate our first drafts, we don't have to think as hard or as deeply about what we write. We rely on the machine to do the hard work of analysis and synthesis, and we don't engage in critical and reflective thinking ourselves. We also miss the opportunity to learn from our mistakes and feedback and the chance to develop our own style.

There is already evidence that this is going to be a problem. The MIT study mentioned earlier found that ChatGPT mostly serves as a substitute for human effort, not a complement to our skills. In fact, the vast majority of participants didn't even bother editing the AI's output. This is a problem I see repeatedly when people first use AI: they just paste in the exact question they are asked and let the AI answer it.

A lot of work is time-consuming by design. In a world in which the AI gives an instant, pretty good, near universally accessible shortcut, we'll soon face a crisis of meaning in creative work of all kinds. This is, in part, because we expect creative work to take careful thought and revision, but also that time often operates as a stand-in for work. Take, for example, the letter of recommendation. Professors are asked to write letters for students all the time, and a good letter takes a long time to write. You have to understand the student and the reason for the letter, decide how to phrase the letter to align with the job requirements and the student's strengths, and more. The fact that it is time-consuming is somewhat the point. That a professor takes the time to write a good letter is a sign that they support the student's application. We are setting our time on fire to signal to others that this letter is worth reading.

Or we can push The Button.

And the problem is that the letter the AI generates is going to be good. Not just grammatically correct, but persuasive and insightful to a human reader. It is going to be better than most letters of recommendation that I receive. This means that not only is the quality of the letter no longer a signal of the professor's interest, but also that you may actually be hurting people by not writing a letter of recommendation by AI, especially if you are not a particularly strong writer. So people now have to consider that the goal of the letter (getting a student a job) is in contrast with the morally correct method of accomplishing the goal (the professor spending a lot of time writing the letter). I am still doing all my letters the old-fashioned way, but I wonder whether that will ultimately do my students a disservice.

Now consider all the other tasks whose final written output is important because it is a signal of the time spent on the task and of the thoughtfulness that went into it—performance reviews, strategic memos, college essays, grant applications, speeches, comments on papers. And so much more.

Then The Button starts to tempt everyone. Work that was boring to do but meaningful when completed by humans (like performance reviews) becomes easy to outsource—and the apparent quality actually increases. We start to create documents mostly with AI that get sent to AI-powered inboxes, where the recipients respond primarily with AI. Even worse, we still create the reports by hand but realize that no human is actually reading them. This kind of meaningless task, what organizational theorists have called mere ceremony, has always been with us. But AI will make a lot of previously useful tasks meaningless. It will also remove the facade that previously disguised meaningless tasks. We may not have always known if our work mattered in the bigger picture, but in most organizations, the people in your part of the organizational structure felt it did. With AI-generated work sent to other AIs to assess, that sense of meaning disappears.

We are going to need to reconstruct meaning, in art and in the rituals of creative work. This is not an easy process, but we have done it before, many times. Where musicians once made money from records, they now depend on being excellent live performers. When photography made realistic oil paintings obsolete, artists started pushing the bounds of photography as art. When the spreadsheet made adding data by hand unneeded, clerks shifted their responsibilities to bigger-picture issues. As we will see in the next chapter, this change in meaning is going to have a large effect on work.

创作工作的意义

如果 AI 已经成为比大多数人更好的作家，并且比大多数人更有创造力，这对创作工作的未来意味着什么？

虽然我们将在下一章讨论工作的影响，但这里有一些显著的正面例子。并不是每个人都是 Nick Cave 或 Hayao Miyazaki（显然），甚至都没有接近那种才华的水平。但许多人希望以创意的方式表达自己，而令人惊讶的是，极少数人感到自己能够做到这一点。一项调查询问了一个具有代表性的人群样本，有多少人觉得他们正在实现自己的创意潜力。只有 31% 的人表示他们正在实现自己的创意潜力。世界上有很多被压抑的创意能量。

在某种程度上，我也是其中之一。我来自一个艺术家庭 —— 我母亲是画家，一个妹妹是平面设计师，另一个妹妹制作好莱坞电影 —— 但尽管上了很多课，我并不擅长创作视觉艺术。我尝试过绘画课、素描课、在线教程，但经过这些训练，我知道自己水平平平。幸运的是，还有很多其他形式的创意表达我可以做得相当好。我写作（显然），设计游戏，但视觉艺术从来不是我的强项。

这一切在 2022 年 7 月 28 日发生了改变。那天我第一次接触到 AI 艺术程序 Midjourney。我几乎立刻被它的强大功能吸引，并花了一整天时间创作艺术柱状图（我是个学术界人士，图表早已深入我们的血液)。我开始在 Twitter 上发布这些图表。到第二天，超过 20000 人点赞了这条推文。学者们告诉我，他们打印出这些图表并挂在墙上。我终于创作出了别人喜欢的作品。

它是艺术吗？可能不是 —— 这是哲学家的问题。不过，我知道它是有创意的。我感受到创造的兴奋感，那种全神贯注尝试创造图像时的心流体验。我经常需要制作和修改几十张图像才能得到一张满意的。尽管很多实验结果并不理想，但我仍然享受开发提示词、将图像反馈给 AI 并观察结果的过程。这其中需要技巧。我从那些更有才华的人那里学到了很多，他们分享的成果、在线文档和大量的实验经验。我已经在这方面取得了相当的进步，我知道这一点，因为那些初次使用这些工具的人无法达到同样的效果。我也知道它是有用的。我制作的作品受到了其他人的喜爱（当项目需要精细的新作品时，我仍然会雇佣和以前一样多的艺术家）。这可能不是艺术，但它在创造力上是充实的和有价值的。而且这是我以前无法做到的事情。

这些影响不仅限于艺术。生成式 AI 正在为人们提供新的表达方式和创意的新语言 —— 有时是字面意义上的语言。我的一些学生提到，他们因为写作水平差而不被认真对待。多亏了 AI，他们的书面材料不再成为障碍，他们凭借经验和面试获得了工作机会。自从我的课程要求使用 AI 后，我再也没有看到糟糕的书面作业。而且正如我的学生所学的那样，如果你与 AI 进行互动，结果不会显得千篇一律，而是会有一种人类完成的感觉。

当然，只看到好的一面是不现实的。特别是当 AI 工作变得可以一键生成时。我是字面意思上的，每个主要的办公应用程序和电子邮件客户端都会有一个按钮来帮助你创建工作的草稿。这个按钮值得特别强调：那个按钮。

当人们面对空白页的压力时，他们会选择按下按钮。开始写点什么总比什么都没有要容易得多。学生们会用它来起草论文，经理们会用它来写邮件、报告或文件，教师们会用它来提供反馈，科学家们会用它来撰写资助申请，概念艺术家们会用它来完成初稿。每个人都会用这个按钮。

由 AI 来写初稿的影响是巨大的。一个后果是我们可能会失去创造力和原创性。当我们用 AI 生成初稿时，往往会被机器生成的第一个想法所限制，这会影响我们未来的工作。即使我们完全重写草稿，它们仍会带有 AI 的影响。我们将无法探索不同的视角和替代方案，从而可能错失更好的解决方案和见解。

另一个后果是我们可能会降低思考和推理的质量和深度。使用 AI 生成初稿时，我们不再需要像以前那样深入思考。我们依赖机器来进行分析和综合，自身缺乏批判性和反思性的思考。我们也失去了从错误和反馈中学习，以及发展自己风格的机会。

已经有证据表明这将成为一个问题。之前提到的 MIT 研究发现，ChatGPT 主要作为人类努力的替代品，而不是技能的补充。事实上，绝大多数参与者甚至懒得编辑 AI 的输出。这是我在观察人们第一次使用 AI 时常见的问题：他们只是复制所问的问题，然后让 AI 回答。

很多工作本来就是设计得很耗时。在一个 AI 可以瞬间提供相当不错、几乎普遍可用的捷径的世界里，我们很快就会面临各种创意工作的意义危机。这部分是因为我们期望创意工作需要仔细思考和修订，但也因为时间往往是工作的象征。以推荐信为例。教授们经常被要求为学生写推荐信，而一封好的推荐信需要很长时间来写。你需要了解学生的情况和推荐信的目的，决定如何措辞以符合工作的要求和学生的优势等等。花时间写推荐信本身就是一个重要的信号，表明教授支持学生的申请。我们正在花费时间，向他人表明这封信值得阅读。

或者我们可以按下按钮。

问题在于 AI 生成的推荐信会非常好。不仅语法正确，而且对人类读者来说非常有说服力和洞察力。它将比我收到的大多数推荐信都要好。这意味着推荐信的质量不仅不再是教授兴趣的信号，而且如果你不是一个特别强的写手，不用 AI 写推荐信实际上可能会让学生处于不利地位。因此，人们现在不得不考虑，推荐信的目标（让学生找到工作）与实现目标的道德正确方法（教授花大量时间写信）之间的矛盾。我仍然以传统的方式写所有的推荐信，但我不知道这是否最终会对我的学生造成不利影响。

现在让我们考虑那些最终书面输出很重要的任务，因为这些输出代表了我们在任务上花费的时间和投入的心思，比如绩效评估、战略备忘录、大学论文、资助申请、演讲稿、论文评论等等。

接着，「按钮」开始诱惑每个人。那些由人类完成时虽然枯燥但很有意义的工作（如绩效评估）变得容易外包 —— 而且看起来质量反而提高了。我们开始主要用 AI 创建文件，这些文件被发送到 AI 驱动的收件箱中，接收者也主要用 AI 回复。更糟糕的是，我们仍然手工创建报告，但发现实际上没人阅读它们。这种无意义的任务，组织理论家称之为「形式主义」，一直存在于我们周围。但 AI 将使许多曾经有用的任务变得无意义，同时也揭示了那些以前被掩盖的无意义任务。我们或许并不总是知道我们的工作在大局中是否重要，但在大多数组织中，组织结构中的人们认为它是重要的。当 AI 生成的工作被其他 AI 评估时，这种意义感就消失了。

我们需要在艺术和创造性工作的过程中重新找到意义。这并不是一个简单的过程，但我们以前已经成功过很多次。以前，音乐家靠唱片赚钱，现在他们依赖于成为优秀的现场表演者。当摄影使得现实主义油画过时时，艺术家开始探索摄影作为艺术的可能。当电子表格使手工添加数据变得不必要时，职员们的职责转向了更宏观的问题。正如我们将在下一章中看到的，这种意义的变化将对工作产生重大影响。