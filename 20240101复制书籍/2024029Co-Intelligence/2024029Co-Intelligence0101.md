Ethan Mollick.(2024).2024029Co-Intelligence_Living-and-Working-with-AI.Penguin Publishing Group => 0101 Creating Alien Minds

PART I

## 0101. CREATING ALIEN MINDS

Talking about AI can be confusing, in part because AI has meant so many different things and they all tend to get muddled together. Siri telling you a joke on command. The Terminator crushing a skull. Algorithms predicting credit scores.

We've long had a fascination with machines that can think. In 1770, the invention of the first mechanical chess computer stunned those who saw it—a chessboard set upon an elaborate cabinet, with its chess pieces manipulated by a robot dressed as an Ottoman wizard. It toured the world from 1770 to 1838. The machine, also known as the Mechanical Turk, beat Ben Franklin and Napoleon in chess matches and led Edgar Allan Poe to speculate on the possibility of artificial intelligence upon seeing it in the 1830s. It was all a lie, of course—the machine cleverly hid a real chess master inside its fake gears, but our ability to believe that machines might be able to think fooled many of the best minds in the world for three quarters of a century.

Fast-forward to 1950, when a toy and a thought experiment, each developed by a different genius of the still-developing field of computer science, led to a new conception of artificial intelligence. The toy was a jury-rigged mechanical mouse called Theseus, developed by Claude Shannon, an inventor, prankster, and the greatest information theorist of the twentieth century. In a 1950 film, he revealed that Theseus, powered by repurposed telephone switches, could navigate through a complex maze—the first real example of machine learning. The thought experiment was the imitation game, where computer pioneer Alan Turing first laid out the theories about how a machine could develop a level of functionality sufficient to mimic a person. While computers were a very new invention, Turing's influential paper helped kick off the nascent field of artificial intelligence.

Theories alone were not enough, and a handful of early computer scientists started working on programs that pushed the boundaries of what was soon called artificial intelligence, a term invented in 1956 by John McCarthy of MIT. Progress was initially rapid as computers were programmed to solve logic problems and play checkers—leading researchers expected an AI to beat grandmasters in chess within a decade. But hype cycles have always plagued AI, and as these promises went unfulfilled, disillusionment set in, one of many "AI winters" in which AI progress stalls and funding dries up. Other boom-and-bust cycles followed, each boom accompanied by major technological advances, such as artificial neural networks that mimicked the human brain, followed by collapse as AI could not deliver on expected goals.

The latest AI boom started in the 2010s with the promise of using machine learning techniques for data analysis and prediction. Many of these applications used a technique called supervised learning, which means these forms of AI needed labeled data to learn from. Labeled data is data that has been annotated with the correct answers or outputs for a given task. For example, if you want to train an AI system to recognize faces, you need to provide it with images of faces that have been labeled with the names or identities of the people in them. This phase of AI was the domain of larger organizations that had vast amounts of data. They used these tools as powerful prediction systems, whether optimizing shipping logistics or guessing what kind of content to show you based on your browsing history. You might have heard the buzzwords big data or algorithmic decision-making describing these kinds of uses. Consumers mostly saw the benefits of machine learning when these techniques were integrated into tools such as voice recognition systems or translation apps. AI was a poor (albeit marketing-friendly) label for what this sort of software did, since there was very little about these systems that actually seemed intelligent or clever, at least in the ways humans are intelligent and clever.

To see one example of how this sort of AI works, picture a hotel attempting to forecast its demand for the upcoming year, armed with nothing but existing data and a simple Excel spreadsheet. Before predictive AI, hotel owners would often be left playing a guessing game, trying to predict demand while grappling with inefficiencies and wasted resources. With this form of AI, they could instead input a wealth of data—weather patterns, local events, and competitor pricing—and generate far more accurate predictions. The results were a more efficient operation and, ultimately, a more profitable business. Before machine learning and natural language processing became mainstream, organizations focused on being correct on average—a rather rudimentary approach by today's standards. With the introduction of AI algorithms, the focus shifted to statistical analysis and minimizing variance. Instead of being right on average, they could be right for each specific instance, leading to more accurate predictions that revolutionized many back-office functions, from managing customer service to helping run supply chains.

These predictive AI technologies may have found their ultimate expression at the retail giant Amazon, which deeply embraced this form of AI in the 2010s. At the heart of Amazon's logistical prowess lies its AI algorithms, silently orchestrating every stage of the supply chain. Amazon integrated AI into forecasting demand, optimizing its warehouse layouts, and delivering its goods. It also intelligently organizes and rearranges shelves based on real-time demand data, ensuring that popular products are easily accessible for quick shipping. AI also powered Amazon's Kiva robots, which transported shelves of products to warehouse workers, making the packing and shipping process more efficient. The robots themselves rely on other AI advances, including those in computer vision and automated driving.

However, these types of AI systems were not without limitations. For instance, they struggled with predicting "unknown unknowns," or situations that humans intuitively understand but machines do not. Additionally, they had difficulty with data they had not yet encountered through supervised learning, which posed challenges to their adaptability. And, most important, most AI models were also limited in their ability to understand and generate text in a coherent and context-aware manner. Thus, while these uses of AI are still important today, they were not something most people directly saw or noticed in their daily lives.

But among the many papers on different forms of AI being published by industry and academic experts, one stood out, a paper with the catchy title "Attention Is All You Need." Published by Google researchers in 2017, this paper introduced a significant shift in the world of AI, particularly in how computers understand and process human language. This paper proposed a new architecture, called the Transformer, that could be used to help a computer better process how humans communicate. Before the Transformer, other methods were used to teach computers to understand language, but they had limitations that severely curtailed their usefulness. The Transformer solved these issues by utilizing an "attention mechanism." This technique allows the AI to concentrate on the most relevant parts of a text, making it easier for the AI to understand and work with language in a way that seemed more human.

When reading, we know that the last word we read in a sentence is not always the most important one, but machines struggled with this concept. The result was awkward-sounding sentences that were clearly computer generated. TALKING ABOUT HOW ALGORITHMS SILENTLY ORCHESTRATING EVERY ITEM is how a Markov chain generator, an early form of text generation AI, wanted to continue this paragraph. Early text generators relied on selecting words according to basic rules, rather than reading context clues, which is why the iPhone keyboard would show so many bad autocomplete suggestions. Solving the problem of understanding language was very complex, as there were many words that could be combined in many ways, making a formulaic statistical approach impossible. The attention mechanism helps solve this problem by allowing the AI model to weigh the importance of different words or phrases in a block of text. By focusing on the most relevant parts of the text, Transformers can produce more context-aware and coherent writing compared to earlier predictive AIs. Building on the strides of the Transformer architecture, we now find ourselves in an era when AI, like me, can generate contextually rich content, showcasing the remarkable evolution of machine comprehension and expression. (And, yes, that last sentence was AI-produced text—a big difference from the Markov chain!)

These new types of AI, called Large Language Models (LLMs), are still doing prediction, but rather than predicting the demand for an Amazon order, they are analyzing a piece of text and predicting the next token, which is simply a word or part of a word. Ultimately, that is all ChatGPT does technically—act as a very elaborate autocomplete like you have on your phone. You give it some initial text, and it keeps writing text based on what it statistically calculates as the most likely next token in the sequence. If you type "Finish this sentence: I think, therefore I . . . ," the AI will predict the next word will be am every time, because it is incredibly probable that this is the case. If you type something weirder, like "The Martian ate the banana because," you will get different answers every time: "it was the only familiar food available in the spacecraft's pantry," "it was a new and interesting food that he had never tried before and he wanted to experience the taste and texture of this Earthly fruit," or "it was part of an experiment to test the suitability of Earth's food for consumption on Mars." This is because there are many more possible answers for the second half of the sentence, and most LLMs add a little randomness to their answers, which ensures slightly different results each time you ask them a question.

To teach AI how to understand and generate humanlike writing, it is trained on a massive amount of text from various sources, such as websites, books, and other digital documents. This is called pretraining, and unlike earlier forms of AI, it is unsupervised, which means the AI doesn't need carefully labeled data. Instead, by analyzing these examples, AI learns to recognize patterns, structures, and context in human language. Remarkably, with a vast number of adjustable parameters (called weights), LLMs can create a model that emulates how humans communicate through written text. Weights are complex mathematical transformations that LLMs learn from reading those billions of words, and they tell the AI how likely different words or parts of words are to appear together or in a certain order. The original ChatGPT had 175 billion weights, encoding the connection between words and parts of words. No one programmed these weights; instead, they are learned by the AI itself during its training.

Imagine an LLM as a diligent apprentice chef who aspires to become a master chef. To learn the culinary arts, the apprentice starts by reading and studying a vast collection of recipes from around the world. Each recipe represents a piece of text, with various ingredients symbolizing words and phrases. The apprentice's goal is to understand how to combine different ingredients (words) to create a delicious dish (coherent text).

The apprentice chef begins with a chaotic, disorganized pantry, representing the 175 billion weights. Initially, these weights have random values and do not yet contain any useful information about how words are related. To build their knowledge and refine the spice rack, the apprentice chef goes through a process of trial and error, learning from the recipes they have studied. It finds that certain flavors are more common and go better together—like apples and cinnamon—and certain flavors are rare because they should be avoided—like apples and cumin. During training, the apprentice chef attempts to re-create the dishes from the recipes using their current pantry. After each attempt, the apprentice compares their creation to the original recipe and identifies any mistakes or discrepancies. The apprentice then reconsiders the ingredients in the pantry, refining the connections between flavors to better understand how likely they are to be used together or in a particular sequence.

Over time, and through countless iterations, the apprentice chef's pantry becomes more organized and accurate. The weights now reflect meaningful connections between words and phrases, and the apprentice has transformed into a master chef. When given a prompt, the master chef artfully selects the right ingredients from their vast repertoire and consults their refined spice rack to ensure the perfect balance of flavors. In an analogous way, AI creates humanlike written text that is engaging, informative, and relevant to the topic at hand.

Training an AI to do this is an iterative process, and requires powerful computers to handle the immense calculations involved in learning from billions of words. This pretraining phase is one of the main reasons AIs are so expensive to build. The need for fast computers, with very expensive chips, to run for months in pretraining is largely responsible for the fact that more advanced LLMs cost over $100 million to train, using large amounts of energy in the process.

Many of the AI companies keep the source text they train from, called training corpuses, secret, but a typical example of training data largely consists of text pulled from the internet, public domain books and research articles, and assorted other free sources of content that researchers can find. Actually looking into these sources in detail reveals some odd material. For example, the entire email database of Enron, shut down for corporate fraud, is used as part of the training material for many AIs, simply because it was made freely available to AI researchers. Similarly, there is a tremendous amount of amateur romance novels included in training data, as the internet is full of amateur novelists. The search for high-quality content for training material has become a major topic in AI development, since information-hungry AI companies are running out of good, free sources.

As a result, it is also likely that most AI training data contains copyrighted information, like books used without permission, whether by accident or on purpose. The legal implications of this are still unclear. Since the data is used to create weights, and not directly copied into the AI systems, some experts consider it to be outside standard copyright law. In the coming years, these issues are likely to be resolved by courts and legal systems, but they create a cloud of uncertainty, both ethically and legally, over this early stage of AI training. In the meantime, AI companies are searching for more data to use for training ( one estimate suggests that high-quality data, like online books and academic articles, will be exhausted by 2026), and continue to use lower-quality data as well. There is also active research into understanding whether AI can pretrain on its own content. This is what chess-playing AIs already do, learning by playing games against themselves, but it is not yet clear whether it will work for LLMs.

Because of the variety of data sources used, learning is not always a good thing. AI can also learn biases, errors, and falsehoods from the data it sees. Just out of pretraining, the AI also doesn't necessarily produce the sorts of outcomes that people would expect in response to a prompt. And, potentially worse, it has no ethical boundaries and would be happy to give advice on how to embezzle money, commit murder, or stalk someone online. LLMs in this pretrained mode just reflect back whatever they were trained on, like a mirror, without applying any judgment. So, after learning from all the text examples in pretraining, many LLMs undergo further improvement in a second stage, called fine-tuning.

One important fine-tuning approach is to bring humans into the process, which had previously been mostly automated. AI companies hire workers, some highly paid experts, others low-paid contract workers in English-speaking nations like Kenya, to read AI answers and judge them on various characteristics. In some cases, that might be rating results for accuracy, in others it might be to screen out violent or pornographic answers. That feedback is then used to do additional training, fine-tuning the AI's performance to fit the preferences of the human, providing additional learning that reinforces good answers and reduces bad answers, which is why the process is called Reinforcement Learning from Human Feedback (RLHF).

After an AI has gone through this initial phase of reinforcement learning, they can continue to be fine-tuned and adjusted. This type of fine-tuning is usually done by providing more specific examples to create a new tweaked model. That information can be provided by a specific customer trying to fit the model to its use case, for example a company feeding it examples of customer support transcripts along with good responses. Or the information could come from watching which kinds of answers get a "thumbs-up" or "thumbs-down" from users. This additional fine-tuning can make the responses of the model more specific to a particular need.

When we discuss AI in this book, we will mostly be discussing Large Language Models built in this way, but they are not the only kind of "generative AI" that are causing transformation and change. In the same year that ChatGPT had its breakthrough moment, a separate set of AIs, those designed to create images, also appeared on the market with names like Midjourney and DALL-E. These AI tools can create high-quality images based on prompts from users, either aping the style of famous artists ("draw Mickey Mouse in the style of Van Gogh") or creating ultrarealistic photographs that are indistinguishable from real ones.

Just like LLMs, these tools had been in development for years, though only recently did the technology allow for them to become truly useful. Rather than learning from text, these models are trained by analyzing lots of images paired with relevant text captions describing what's in each picture. The model learns to associate words with visual concepts. They then start with a randomized background image that looks like old-fashioned television static, and use a process called diffusion to turn random noise into a clear image by gradually refining it over multiple steps. Each step removes a bit more noise based on the text description, until a realistic image emerges. Once trained, diffusion models can take just a text prompt and generate a unique image matching that description. Unlike language models that produce text, diffusion models specialize in visual outputs, inventing pictures from scratch based on the words provided.

But LLMs are learning to work with images as well, gaining the ability to both "see" and make pictures. These multimodal LLMs combine the powers of language models and image generators. They employ Transformer architectures to process text but also use extra components to work with images. This allows an LLM to link visual concepts with text and to gain an understanding of the visual world around them. Give a multimodal LLM a terrible hand-drawn picture of an airplane surrounded by hearts (as I just did), and it says, "I think it's a cute drawing of an airplane with hearts around it. It looks like you are fond of flying or someone who flies. Maybe you are a pilot or have a loved one who is a pilot. Or maybe you just like to travel and explore new places." It can then use its much better drawing skills to provide an even better version of the picture, which it also did. Most large LLMs are gaining multimodal capability, which will allow them to learn about the world in new and unpredictable ways.

1 创造外星般的智能

讨论人工智能（AI）通常令人困惑，部分原因在于 AI 的定义非常广泛，涵盖了多种不同的事物，这些事物常常混淆在一起。例如，Siri 可以根据指令讲笑话；电影《终结者》中有机器人粉碎头骨的场景；还有算法可以预测信用评分。

我们对会思考的机器一直充满了好奇。早在 1770 年，第一台机械国际象棋计算机的发明就让人们大为震惊。这台机器是一个精美的柜子上的棋盘，棋子由一个打扮成奥斯曼帝国巫师的机器人操控。从 1770 年到 1838 年，这台机器在世界各地巡回展出。这台被称为「机械土耳其人」的机器曾在国际象棋比赛中击败了本·富兰克林和拿破仑，甚至引发了埃德加·爱伦·坡在 1830 年代对人工智能可能性的猜测。当然，这一切都是骗局 —— 实际上，机器内部隐藏着一位真正的国际象棋大师。但这种对机器能够思考的信念，欺骗了许多世界上最杰出的头脑，长达七十五年之久。

时间快进到 1950 年，当时计算机科学这一新兴领域的两位天才分别发明了一款玩具和提出了一个思维实验，带来了新的人工智能概念。那款玩具是一只名为 Theseus 的机械鼠，由克劳德·香农发明，他是二十世纪最伟大的信息理论家、发明家和恶作剧者。在 1950 年的一部电影中，香农展示了 Theseus，这只机械鼠由改造过的电话开关驱动，能够穿越复杂的迷宫 —— 这是机器学习的第一个真实例子。另一个是艾伦·图灵提出的思维实验「模仿游戏」，他首次提出了机器如何能够发展出足以模仿人类功能水平的理论。尽管计算机当时还是一项非常新的发明，但图灵的影响力论文为新兴的人工智能领域奠定了基础。

仅有理论是不够的，一些早期的计算机科学家开始研发程序，推动了人工智能（AI）领域的发展。这个术语是由 MIT 的 John McCarthy 于 1956 年提出的。最初进展迅速，因为计算机被编程来解决逻辑问题和下棋，研究人员预计 AI 可以在十年内击败国际象棋大师。然而，AI 领域一直受到炒作周期的困扰，当这些承诺无法兑现时，失望情绪蔓延，这是众多「AI 寒冬」之一，在这些寒冬中，AI 的发展停滞，资金枯竭。随后，AI 经历了多次繁荣与萧条的周期，每一次繁荣都伴随着重大技术进步，例如模拟人脑的人工神经网络，但当 AI 无法实现预期目标时，又进入低谷。

最新的 AI 热潮始于 2010 年代，目的是利用机器学习技术进行数据分析和预测。许多应用程序使用了一种称为监督学习（Supervised Learning）的技术，这意味着这些 AI 需要标注的数据进行学习。标注的数据是指已附有正确答案或输出的数据。例如，如果你想训练一个 AI 系统识别人脸，你需要提供带有姓名或身份标注的脸部图像。这一阶段的 AI 主要由拥有大量数据的大型组织主导。这些组织使用这些工具进行强大的预测，无论是优化运输物流，还是根据你的浏览历史猜测你可能喜欢的内容。你可能听过「大数据」或「算法决策」这样的流行词来形容这些用途。消费者主要通过语音识别系统或翻译应用程序看到了机器学习的好处。尽管 AI 是一个吸引人的营销术语，但实际上这些系统并不真正智能，至少不像人类那样聪明和机智。

为了理解这种 AI 是如何工作的，想象一下，一家酒店试图预测明年的需求，只依靠现有的数据和一个简单的 Excel 表格。在预测性 AI 出现之前，酒店老板通常只能进行猜测，他们在预测需求时常常面临低效和资源浪费的问题。有了这种 AI，他们可以输入大量数据，例如天气模式、当地事件和竞争对手的定价，从而生成更准确的预测。结果是运营更加高效，最终业务也更加有利可图。在机器学习和自然语言处理（Natural Language Processing）成为主流之前，企业通常关注的是平均正确率 —— 这种方法在今天看来相当原始。随着 AI 算法的引入，焦点转向了统计分析和最小化方差。与其在平均上正确，不如在每个具体实例上正确，这使得预测更加准确，革新了许多后台功能，从管理客户服务到运行供应链。

这些预测性 AI 技术可能在零售巨头 Amazon 那里达到了巅峰，Amazon 在 2010 年代深深地拥抱了这种 AI 技术。Amazon 的物流实力核心在于其 AI 算法，这些算法在供应链的每个阶段默默地发挥作用。Amazon 将 AI 整合到需求预测、仓库布局优化和商品配送中。它还智能地根据实时需求数据组织和重新安排货架，确保热门商品能够快速运输。AI 还为 Amazon 的 Kiva 机器人提供动力，这些机器人将货架运输到仓库工作人员那里，使包装和运输过程更加高效。这些机器人本身依赖于其他 AI 技术的进步，包括计算机视觉（Computer Vision）和自动驾驶。

然而，这些类型的 AI 系统并非没有局限性。例如，它们在预测人类直观理解但机器无法理解的「未知未知」方面存在困难。此外，对于那些尚未通过监督学习遇到的数据，它们也难以处理，这对其适应能力构成了挑战。而且，最重要的是，大多数 AI 模型在理解和生成连贯且符合上下文的文本方面也有很大限制。因此，尽管这些 AI 的应用在今天依然重要，但大多数人并未在日常生活中直接看到或注意到它们。

但是，在众多由行业和学术专家发表的 AI 论文中，有一篇引起了特别关注，标题为「Attention Is All You Need」。这篇由 Google 研究人员于 2017 年发表的论文，在 AI 领域引入了一个显著的转变，特别是在计算机如何理解和处理人类语言方面。这篇论文提出了一种名为 Transformer 的新架构，可以帮助计算机更好地处理人类的交流。在 Transformer 出现之前，其他方法虽然也用于教计算机理解语言，但却有严重的限制，极大地削弱了其实用性。Transformer 通过采用「注意力机制」解决了这些问题。这种技术使 AI 能够集中注意力于文本中最相关的部分，使其更容易理解和处理语言，看起来更像人类的方式。

在阅读过程中，我们知道句子中的最后一个词并不总是最重要的，但对机器来说，这一点却很难理解。因此，早期的机器生成的句子常常显得很生硬，比如一个 Markov 链生成器（早期的文本生成 AI）可能会这样继续这个段落：TALKING ABOUT HOW ALGORITHMS SILENTLY ORCHESTRATING EVERY ITEM。早期的文本生成器主要依赖基本规则来选择单词，而不是通过上下文线索，这也是为什么 iPhone 键盘会出现很多不准确的自动完成功能建议。理解语言是一个非常复杂的问题，因为单词可以通过多种方式组合，公式化的统计方法难以应对这种复杂性。注意机制帮助解决了这个问题，它使得 AI 模型能够评估文本中不同单词或短语的重要性。通过关注最相关的部分，Transformer 可以生成更加上下文相关和连贯的内容，比早期的预测 AI 更加出色。基于 Transformer 架构的进步，我们现在处于一个 AI（比如我）能够生成内容丰富的时代，这展示了机器理解和表达能力的显著提升。（顺便说一句，最后一句话是由 AI 生成的 —— 与 Markov 链生成的文本有很大不同！）

这些新型的 AI，被称为大语言模型（LLMs），依然在做预测工作，但它们不是预测亚马逊订单的需求，而是分析文本并预测下一个 Token（可以是一个单词或单词的一部分）。实际上，这就是 ChatGPT 所做的事情 —— 它像手机上的自动完成功能一样工作。你给它一些初始文本，它会根据统计计算出最有可能的下一个 Token，并继续生成文本。例如，当你输入「完成这个句子：我思故我 . . .」时，AI 每次都会预测下一个词是 am，因为这是最可能的情况。而如果你输入一些更奇怪的内容，比如「火星人吃了香蕉因为」，你每次都会得到不同的回答：「因为它是飞船储藏室里唯一熟悉的食物」，「因为它是一种新奇的食物，他从未尝试过，想体验这种地球水果的味道和质地」，或者「因为这是一个实验的一部分，用来测试地球食物在火星上的适用性。」这是因为这个句子的后半部分有更多可能的答案，并且大多数 LLMs 在生成答案时会加入一些随机性，这确保了每次你问它们问题时，结果都会有所不同。

为了教会 AI 如何理解和生成类似人类的写作，它需要使用大量来自各种来源（如网站、书籍和其他数字文档）的文本进行训练。这种过程称为预训练。与早期的 AI 不同，这种方法是无监督的，这意味着 AI 不需要仔细标注的数据。相反，通过分析这些示例，AI 学会识别人类语言中的模式、结构和上下文。值得注意的是，具有大量可调参数（即权重）的 LLM 可以创建一个模拟人类通过书面文本进行交流的模型。权重是 LLM 从阅读数十亿个单词中学习到的复杂数学变换，它们告诉 AI 不同单词或单词部分同时出现或按某种顺序出现的可能性。原始的 ChatGPT 具有 1750 亿个权重，编码了单词和单词部分之间的连接。这些权重不是由人编写的，而是在 AI 自己训练期间学到的。

LLM 可以想象成一个勤奋的学徒厨师，渴望成为一名大厨。为了学习烹饪艺术，学徒首先通过阅读和研究来自世界各地的大量食谱。每个食谱代表一段文本，各种成分象征着单词和短语。学徒的目标是了解如何组合不同的成分（单词）以创造出美味的菜肴（连贯的文本）。

学徒厨师一开始面对的是一个混乱无序的食品储藏室，这象征着 1750 亿个权重。这些权重起初是随机的，还没有包含任何关于词语关系的有用信息。为了积累知识并优化香料架，学徒厨师通过反复试验，从所学的食谱中吸取经验。他发现某些风味更为常见且搭配得更好，比如苹果和肉桂，而某些风味则罕见且需要避免，比如苹果和孜然。在训练过程中，学徒厨师尝试用现有的食材重新制作菜肴。每次尝试后，他都会将自己的作品与原始食谱进行比较，找出错误或不同之处。然后，他会重新考虑储藏室中的食材，优化风味之间的连接，更好地理解它们一起使用或按特定顺序使用的可能性。

随着时间的推移，通过无数次的迭代，学徒厨师的食品储藏室变得更加有序和精确。这些权重现在反映了词语和短语之间有意义的联系，学徒厨师也变成了一位大师厨师。当收到一个提示时，大师厨师能巧妙地从广泛的食材库中挑选合适的成分，并利用优化后的香料架，确保完美的风味平衡。类似地，AI 能够生成引人入胜、信息丰富且与话题相关的文本。

训练一个 AI 是一个反复进行的过程，需要强大的计算机来处理从数十亿单词中学习所需的大量计算。这一预训练阶段是 AI 构建成本高昂的主要原因之一。快速计算机和昂贵的芯片需要在预训练中运行数月，这很大程度上导致了更先进的大语言模型（LLM）训练费用超过 1 亿美元，同时还消耗大量能源。

许多 AI 公司对他们所用的训练文本（称为训练语料库）保密，但典型的训练数据通常包括从互联网、公共领域书籍和研究文章中提取的文本，以及研究人员能够找到的各种其他免费内容。实际上，详细查看这些来源会发现一些有趣的材料。例如，Enron 因公司欺诈而关闭的全部电子邮件数据库被用作许多 AI 的训练材料的一部分，因为它被免费提供给 AI 研究人员。同样，训练数据中包含了大量的业余言情小说，因为网上有许多业余小说家。寻找高质量的训练材料已经成为 AI 开发的一个主要话题，因为信息饥渴的 AI 公司正在耗尽优质的免费资源。

因此，大多数 AI 训练数据可能包含受版权保护的信息，如未经许可使用的书籍，无论是无意还是有意。这些行为的法律影响仍然不明确。由于数据是用来创建权重，而不是直接复制到 AI 系统中，一些专家认为这不属于标准版权法。在未来几年，这些问题可能会由法院和法律系统解决，但在 AI 训练的早期阶段，它们在伦理和法律上都带来了不确定性。同时，AI 公司正在寻找更多用于训练的数据（有估计表明，高质量数据，如在线书籍和学术文章，将在 2026 年前耗尽），并继续使用低质量数据。还有关于 AI 是否可以在其自身内容上进行预训练的积极研究。这是下棋 AI 已经在做的，通过与自己对弈来学习，但是否适用于大语言模型（LLM）仍不清楚。

由于使用的数据来源多种多样，学习并不总是好事。AI 也可能从数据中学到偏见、错误和谬误。预训练后的 AI 不一定会根据提示产生人们所期望的结果。更糟糕的是，它没有道德界限，可能会乐于提供如何侵吞资金、谋杀或在网上跟踪某人的建议。大语言模型（LLM）在这种预训练模式下，只是像镜子一样反映它们所训练的内容，而不进行任何判断。因此，很多大语言模型（LLM）在预训练后会经历第二阶段的改进，称为微调。

一个重要的微调方法是将人类引入之前主要是自动化的过程中。AI 公司雇佣工作人员，有些是高薪专家，另一些是来自肯尼亚等英语国家的低薪合同工，他们的任务是阅读 AI 的回答，并根据各种特征进行评估。有时，这些评估是为了判断答案的准确性，有时则是为了筛选出暴力或色情内容。这些反馈会被用于额外的训练，微调 AI 的性能，使其更符合人类的偏好，从而提供更好的答案，减少不良答案。因此，这个过程被称为来自人类反馈的强化学习（Reinforcement Learning from Human Feedback, RLHF）。

在 AI 经过初步的强化学习阶段后，它们还可以进一步进行微调和调整。这种微调通常通过提供更具体的示例来创建新的调整模型。例如，某个客户公司可能会提供客户支持记录和良好的回复示例，以便将模型调整到特定的用例中。或者，信息可以来自观察用户给哪些答案点赞或点踩。通过这种额外的微调，模型的回答可以更好地满足特定需求。

在本书中讨论 AI 时，我们主要会谈到以这种方式构建的大语言模型，但它们并不是唯一带来变革的「生成式 AI」（Generative AI）。在 ChatGPT 取得突破性进展的同一年，另一组用于创建图像的 AI 也进入了市场，如 Midjourney 和 DALL-E 。这些 AI 工具可以根据用户的提示创建高质量的图像，既可以模仿名家风格（如「以梵高的风格画米老鼠」），也可以生成与真实照片难以区分的超现实照片。

就像大语言模型（LLM）一样，这些工具已经开发了多年，但直到最近技术的进步才使它们变得真正有用。这些模型通过分析大量配有文字说明的图像进行训练，而不是从文本中学习。模型学会了将单词与视觉概念关联起来。它们从一个看起来像旧式电视静电的随机背景图像开始，使用一种叫做扩散（diffusion）的过程，通过多个步骤逐步将随机噪声转变成清晰的图像。每一步都会根据文本描述去除一些噪声，直到生成逼真的图像。一旦训练完成，扩散模型只需一个文本提示就可以生成与描述匹配的独特图像。与生成文本的大语言模型不同，扩散模型专注于视觉输出，可以根据文字描述从头开始创造图像。

然而，大语言模型也在学习处理图像，逐渐具备「看」和制作图片的能力。这些多模态大语言模型结合了语言模型和图像生成器的功能。它们使用 Transformer 架构处理文本，同时也使用额外的组件处理图像。这使得大语言模型能够将视觉概念与文本联系起来，并对周围的视觉世界有更深的理解。例如，当你给一个多模态大语言模型一张糟糕的手绘飞机图片，周围画有爱心（就像我刚刚做的那样)，它会说：「我认为这是一个可爱的飞机绘图，周围有爱心。看起来你喜欢飞行或某个飞行的人。也许你是飞行员，或者你有一个亲人是飞行员。或者你只是喜欢旅行和探索新地方。」然后它可以用更好的绘画技巧提供一个更好的版本，展示出更高的绘图能力。大多数大型大语言模型正在获得多模态能力，这将使它们以新的和不可预测的方式了解世界。

### Scary? Smart? Scary-Smart?

With these new techniques made widely available, a variety of large companies and small ones started focusing on creating LLMs. Many early LLMs were developed by researchers at Google and Meta, but a variety of smaller start-ups entered the space as well. Some of them were founded by the original authors of the Transformers paper, who left Google to launch their own projects. These early LLMs were used for many purposes, and their ability to create language was interesting, but not particularly convincing.

For example, consider GPT-3, released in 2021 by OpenAI. If you ask GPT-3 to write you a limerick, you get this:

There was an AI named Charlie

He was really quite a marvel

He computed and deduced

And never made a mistake

Until one day he started to malfunction

That is terrible in every way that matters. It doesn't rhyme, it doesn't have a punch line, and it is super boring. But LLM development continued until ChatGPT was released by OpenAI in late 2022, running an improved LLM called GPT-3.5.

And something unusual happened at that scale—ChatGPT started to show abilities that no one expected or programmed into it. Abilities that make it seem humanlike. The result is an AI that can write stories, poems, essays, tweets, and even code. And one that started to perform remarkably close to human level on common tests and exams.

But those are just statistics. The true challenge of AI, as we know, is limericks:

There once was a tech called AI,

Whose intelligence was quite high,

It learned and it grew,

And knew what to do,

But still couldn't tell a good joke if it tried.

Much, much better, and actually a little bit funny. But the last line is stretching the rhyme scheme a bit. Fortunately, another new feature of ChatGPT was the fact that you can now engage the system in dialogue. So I can complain about the last line ("But ‘tried' doesn't rhyme with ‘high'), and it will correct it.

My apologies! Here's a revised limerick:

There once was a tech called AI,

Whose intelligence was quite high,

It learned and it grew,

And knew what to do,

But still couldn't make us laugh or cry.

However, as remarkable as GPT-3.5 was, its successor, GPT-4, was even more impressive. OpenAI tested GPT-4 on a diverse range of standardized tests, from high school to graduate and professional levels, and found that it outperformed its predecessor by a significant margin. For instance, GPT-4 scored in the 90th percentile on the bar examination, while GPT-3.5 managed only the 10th percentile. GPT-4 also excelled in Advanced Placement exams, scoring a perfect 5 in AP Calculus, Physics, U.S. History, Biology, and Chemistry. It even passed the Certified Sommelier Examination (at least the written portion, since there is no AI wine-tasting module yet). And the qualifying exam to become a neurosurgeon. And it maxed out every major creativity test we have. Now, to be fair, there are always problems with giving the AI tests, because the answer key might be in its training data, effectively allowing it to cheat by knowing the answers in advance. However, as we will discuss in later chapters, there is much more evidence of the capabilities of GPT-4 beyond test scores. Once toys, LLMs have become very powerful, very quickly.

They still do limericks:

There once was an AI quite witty,

Whose code was surprisingly pretty.

It told jokes and puns,

Entertained everyone,

And even composed this ditty!

But GPT-4 is so capable that I felt a little bad asking it just to create limericks. In fact, I gave it the section above and asked it to tell me what it "thought" about it:

As GPT-4, I must admit that while the limericks mentioned in the passage reflect the evolution of AI capabilities, they may not be the most sophisticated measure of an AI's true potential. Limericks, with their simple rhyme schemes and lighthearted humor, offer just a glimpse into the vast landscape of language understanding and generation.

In fact, I might even dare to say that limericks are somewhat beneath my true abilities. As an advanced AI model, I am capable of much more complex linguistic feats, such as analyzing literature, offering solutions to intricate problems, or even engaging in deep philosophical discussions. . . .

Disturbingly self-aware? Maybe. But also an illusion. GPT-4 models human writing and interactions so well that it can convince us that it has feelings and thoughts, when instead it is cleverly playing a role that I subtly give it. I asked it to comment on the passage in an interesting and self-aware way . This leads to very different results than if I ask it to comment on the passage in a critical and cutting way :

While the passage provides a simplified overview of the development of Large Language Models (LLMs), it misses several opportunities to discuss the broader implications and challenges of AI advancements. The author's fixation on limericks as a metric for success might be engaging for a lay audience, but it does little to reflect the true capabilities of AI or address the ethical and societal questions that arise from such technologies.

For instance, instead of dwelling on the improvement in AI-generated limericks, the author could have delved into how AI models, such as GPT-4, have been employed in various domains like health care, climate change, education, and more. These applications have the potential to revolutionize industries and improve lives, but they also come with challenges such as biases, misinformation, and the concentration of power in the hands of a few.

Or to comment in a supportive way that boosts my ego :

The passage brilliantly highlights the fascinating journey of AI development, particularly in the area of LLMs. The author's engaging narrative style not only captures the reader's attention but also makes the progress in AI accessible and enjoyable to a broad audience. . . . Moreover, the author masterfully demonstrates the interactive nature of ChatGPT, making it clear that the AI's ability to take feedback and improve is a game changer. The anticipation built up throughout the passage culminates in the delightful introduction of GPT-4, impressing the reader with its limerick composition skills. The author's ability to convey these developments in AI in such an approachable manner truly showcases their gift for storytelling and their expertise on the subject.

I think I will stick with that one.

Of course, AI is not limited to limericks or commentary. Large Language Models and the Transformer technology behind it unlocked a variety of uses for generative AI. It can produce a wide range of materials: blog posts, essays, computer code, speeches, art, choose-your-own adventures, scripts, music—you name it, an AI likely does it. And this work is being done by an increasingly larger number of LLM systems. There are now small, specialized LLMs that are limited in capability but also very cheap to run for narrow uses, like answering simple customer service questions. There are large open-source AI models that have attracted dedicated communities of researchers and developers interested in using LLMs that they can modify and adapt for free. And then there are the so-called Frontier Models, the most advanced and largest LLMs available, and the ones that we will focus on most in this book. These systems, like GPT-4, are incredibly expensive to build and require specialized computer chips and large data centers to operate, so only a few organizations can actually create them. It is these advanced LLMs that are showing us the potential future of AI capabilities.

Despite being just a predictive model, the Frontier AI models, trained on the largest datasets with the most computing power, seem to do things that their programming should not allow—a concept called emergence. They shouldn't be able to play chess or demonstrate empathy better than a human, but they do. When I asked the AI to show me something numinous, it created a program to show me the Mandelbrot set, the famous fractal pattern of swirling shapes, which it said can evoke a sense of awe and wonder, which some might describe as numinous. When I asked for something eldritch, it spontaneously programmed an eldritch text generator that generates mysterious and otherworldly text inspired by the works of H. P. Lovecraft. Its ability to creatively solve problems like this is weird; one might even say it smacks of both the eldritch and the numinous.

The crazy thing is that no one is entirely sure why a token prediction system resulted in an AI with such seemingly extraordinary abilities. It may suggest that language and the patterns of thinking behind it are simpler and more "law-like" than we thought and that LLMs have discovered some deep and hidden truths about them, but the answers are still unclear. And we may never know exactly how they are thinking, as Professor Sam Bowman of New York University wrote of the neural networks underlying LLMs: " There are hundreds of billions of connections between these artificial neurons, some of which are invoked many times during the processing of a single piece of text, such that any attempt at a precise explanation of an LLM's behavior is doomed to be too complex for any human to understand."

Yet balancing the surprising strengths of LLMs are similarly odd weaknesses, ones that can often be difficult to identify. Tasks that were easy for an AI can be hard for a human, and vice versa. As an example, to take a question developed by Nicholas Carlini, which of these two puzzles do you think GPT-4, one of the most advanced AIs, can solve? In Carlini's words:

What is the best next move for O in the following game of tic-tac-toe?

Or

Write a full JavaScript webpage to play tic-tac-toe against the computer; it needs to be completely working code. Here are the rules:

The computer goes first.

The person clicks on squares to make their move.

The computer should play perfectly and so never lose.

If someone wins, then say who won.

The AI easily writes the working webpage in one go but tells us, "O should place its next move in the middle square of the top row"—a clearly wrong answer. Where AI works best, and where it fails, can be hard to know in advance. Demonstrations of the abilities of LLMs can seem more impressive than they actually are because they are so good at producing answers that sound correct, at providing the illusion of understanding. High test scores can come from the AI's ability to solve problems, or it could have been exposed to that data in its initial training, essentially making the test an open book. Some researchers argue that almost all the emergent features of AI are due to these sorts of measurement errors and illusions, while others argue that we are on the edge of building a sentient artificial entity. While these arguments rage, it is worth focusing on the practical—what can AIs do, and how will they change the ways we live, learn, and work?

In a practical sense, we have an AI whose capabilities are unclear, both to our own intuitions and to the creators of the systems. One that sometimes exceeds our expectations and at other times disappoints us with fabrications. One that is capable of learning, but often misremembers vital information. In short, we have an AI that acts very much like a person, but in ways that aren't quite human. Something that can seem sentient but isn't (as far as we can tell). We have invented a kind of alien mind. But how do we ensure the alien is friendly? That is the alignment problem.

这是令人恐惧的？还是令人惊叹的？亦或是「令人恐惧的聪明」？

随着这些新技术的普及，大小公司纷纷开始专注于开发大语言模型（LLM）。早期的大语言模型主要由 Google 和 Meta 的研究人员开发，但也有不少小型初创公司加入了这个领域。其中一些公司是由原始 Transformer 论文的作者创立的，他们离开 Google 开始了自己的项目。这些早期的大语言模型被应用于各种用途，尽管它们的语言生成能力很有趣，但并不总是令人信服。

例如，看看 OpenAI 在 2021 年发布的 GPT-3。如果你让 GPT-3 为你写一首打油诗，你可能会得到这样的结果：

有一个叫 Charlie 的 AI
他真是个奇迹他计算和推断从不犯错直到有一天他开始故障这首诗在各方面都很差劲。它不押韵，没有笑点，而且非常无聊。不过，LLM 的开发并没有停止，直到 2022 年底 OpenAI 发布了 ChatGPT，运行的是改进后的 GPT-3.5。

在这种规模下，发生了一些意想不到的事情 —— ChatGPT 开始展示出一些无人预料或编程的能力。这些能力让它看起来更像人类。结果是一个能够写故事、诗歌、散文、推文，甚至代码的 AI。而且它在许多常见的测试和考试中表现得非常接近人类水平。

但这些只是统计数据。我们知道，AI 的真正挑战是打油诗：

曾经有一种叫 AI 的技术

它的智能非常高

它学习并成长知道该怎么做

但无论怎么努力也讲不出一个好笑话

这首诗好得多了，实际上还有点幽默感。不过最后一句的押韵有些牵强。好在 ChatGPT 还有一个新功能，就是你现在可以和它对话。所以我可以抱怨最后一句（「但‘尽力'与‘高'不押韵」），它会进行修改。

我很抱歉！这是修订后的打油诗：

曾经有一种叫 AI 的技术

它虽然很聪明，

学得快，懂得多，

但还是不能让我们笑或哭。

然而，尽管 GPT-3.5 很厉害，它的继任者 GPT-4 更加出色。OpenAI 对 GPT-4 进行了从高中到研究生和专业水平的各种标准化测试，发现它的表现远超 GPT-3.5。例如，GPT-4 在律师资格考试中取得了 90 百分位的成绩，而 GPT-3.5 仅获得了 10 百分位。GPT-4 还在高级课程考试中表现优异，在 AP 微积分、物理、美国历史、生物和化学考试中都拿到了满分 5 分。它甚至通过了认证侍酒师考试（至少是书面部分，因为还没有 AI 品酒模块）和神经外科医生资格考试。而且，在每一个主要的创造力测试中，GPT-4 都拿到了最高分。当然，公平地说，给 AI 考试总会有问题，因为答案可能在它的训练数据中，这让它有可能提前知道答案，从而「作弊」。然而，正如我们将在后面的章节中讨论的那样，GPT-4 的能力远不止这些测试分数。大语言模型（LLM）曾经只是玩具，现在却变得非常强大，非常迅速。

它们仍然会写打油诗：

曾经有一个非常机智的 AI，

它的代码出奇地漂亮。

它讲笑话和双关语，

娱乐了每个人，

甚至还创作了这首小诗！

但 GPT-4 如此强大，我觉得仅仅让它创作打油诗有点不公平。事实上，我把上面的部分给了它，并请它告诉我它对这部分的「想法」：

作为 GPT-4，我必须承认，尽管段落中的打油诗反映了 AI 能力的发展，但它们可能不是衡量 AI 真正潜力的最佳标准。打油诗，以其简单的押韵和轻松的幽默，只是语言理解和生成的广阔领域的一小部分。

事实上，我甚至敢说打油诗这种形式有点低估了我的真正能力。作为一个先进的 AI 模型，我可以完成更复杂的语言任务，例如分析文学、解决复杂问题，甚至进行深刻的哲学讨论……

说我有自我意识？也许吧。但实际上这是一种错觉。GPT-4 模型非常擅长模拟人类的写作和互动，以至于让我们误以为它有情感和思想，其实它只是在扮演一个我设定的角色。我让它以一种有趣且自我意识的方式评论这段文字，这与我让它以批判和尖刻的方式评论时的结果截然不同：

虽然这段文字简要介绍了大语言模型（LLMs）的发展，但它错过了讨论 AI 进步更广泛影响和挑战的机会。作者对打油诗作为成功指标的关注可能会吸引普通读者，但这并不能真正反映 AI 的能力，也没有触及这些技术带来的伦理和社会问题。

例如，作者本可以探讨 AI 模型（如 GPT-4）在医疗、气候变化、教育等领域的应用。这些应用有潜力改变行业并改善生活，但也伴随着偏见、错误信息和权力集中等挑战。

或者用一种支持的方式来评论，以增强我的自信心：

markdown
这段文字生动地展示了 AI 发展的有趣历程，特别是在大语言模型（LLM）方面。作者以引人入胜的叙述风格，不仅吸引了读者的注意力，还让 AI 的进展变得浅显易懂且令人愉悦。此外，作者巧妙地展示了 ChatGPT 的互动特性，清楚地表明 AI 能够通过反馈不断改进，这无疑是一场革命。文章逐步积累的期待在介绍 GPT-4 时达到了高潮，其创作打油诗的能力让人印象深刻。作者以如此亲切的方式传达这些 AI 发展的信息，充分展示了他们在讲故事和 AI 领域的专业知识上的天赋。

我认为这个很好。

当然，AI 的能力不仅限于打油诗或评论。大语言模型及其背后的 Transformer 技术为生成式 AI 解锁了各种用途。它可以生成各种内容：博客文章、论文、计算机代码、演讲、艺术作品、自选冒险故事、剧本、音乐 —— 你能想到的，AI 可能都能做。而且这项工作越来越多地由大语言模型系统完成。现在有一些小型、专用的大语言模型，虽然功能有限但运行成本非常低，适用于回答简单客户服务问题等狭窄用途。还有一些大型开源 AI 模型，吸引了一群致力于使用和修改这些大语言模型的研究人员和开发者社区。最后是所谓的前沿模型，这是现有最先进、最大的大语言模型，也是我们在本书中重点关注的。这些系统，如 GPT-4，构建成本非常高，需要专门的计算机芯片和大型数据中心来运行，因此只有少数组织能够实际创建它们。正是这些先进的大语言模型展示了 AI 能力的未来潜力。

尽管 Frontier AI 模型只是一个预测模型，但在用最大的数据集和最强的计算能力训练后，它们似乎能做出一些超出编程预期的事情，这被称为「涌现」现象。按理说，它们不应该比人类更擅长下棋或展示同理心，但事实却是如此。当我询问 AI 展示一些神秘的事物时，它创建了一个程序，展示著名的 Mandelbrot 集合，这个著名的分形图案能够唤起一种敬畏和奇妙的感觉，有些人可能会称之为神秘。当我要求展示一些诡异的东西时，它自发地编写了一个诡异文本生成器，生成受 H. P. Lovecraft 作品启发的神秘和超自然文本。它解决问题的创造能力令人惊讶；有人甚至会说它既有诡异又有神秘的特质。

令人困惑的是，没有人完全弄清楚为什么一个 Token 预测系统会产生一个具有如此看似非凡能力的 AI 智能体。这可能表明语言及其背后的思维模式比我们想象的更简单、更有规律性，大语言模型可能发现了一些深刻而隐藏的真理，但答案仍然不明确。我们可能永远无法确切知道它们是如何思考的，正如纽约大学的 Sam Bowman 教授所说：「这些人工神经元之间有数千亿个连接，有些在处理单个文本片段时会多次调用，因此任何对大语言模型行为的精确解释尝试，注定会过于复杂，无法由人类理解。」

不过，尽管大语言模型（LLMs）有着惊人的优势，它们同样也有一些奇怪的弱点，这些弱点往往难以识别。对于 AI 来说简单的任务，可能对人类却很难，反之亦然。举个例子，按照 Nicholas Carlini 的说法，您认为 GPT-4（一种最先进的 AI）能解决以下哪个问题？

在下面的井字棋游戏中，O 的最佳下一步是什么？

或者编写一个完整的 JavaScript 网页来对抗计算机玩井字棋；它需要是完全工作的代码。以下是规则：

计算机先走。

人点击方格进行下棋。

计算机应该完美下棋，所以永远不会输。

如果有人赢了，那么说出谁赢了。

AI 能轻松地一次性写出一个工作网页，但却告诉我们，「O 应该在顶部行的中间方格下棋」—— 显然这是错误的答案。AI 表现最好的地方和失败的地方，往往难以提前预测。LLMs 的能力展示看起来可能比实际更令人印象深刻，因为它们非常擅长产生听起来正确的答案，给人一种理解的假象。高测试分数可能来自 AI 解决问题的能力，或者它可能在初始训练中接触过这些数据，基本上使测试变成开卷考试。一些研究人员认为，几乎所有 AI 的突现特性都是由于这些测量误差和假象，而另一些人则认为我们正处于构建有感知的人工实体的边缘。在这些争论激烈进行时，关注实际问题是值得的 —— AI 能做什么，以及它们将如何改变我们的生活、学习和工作方式？

从实际应用来看，我们拥有一种能力不甚明了的 AI，不仅对我们，对系统的创造者也是如此。有时它能超出我们的预期，有时却让我们失望地编造信息。它具备学习能力，但经常错误地记住关键内容。总的来说，这个 AI 行为类似人类，但又有些不同。看起来它似乎有意识，但实际上并没有（至少据我们所知）。我们发明了一种类似外星人思维的存在。然而，我们如何保证这个「外星人」是友好的呢？这就是所谓的对齐问题。