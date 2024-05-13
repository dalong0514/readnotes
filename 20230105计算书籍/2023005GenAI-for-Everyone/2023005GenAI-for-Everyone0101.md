参考：Andrew Ng.(2023).GenAI for Everyone.DeepLearning.AI => xxxx

### 0101. Welcome

Welcome to generative AI for everyone.

Since the release of ChatGPT, AI, specifically generative AI, has caught the attention of many individuals,
corporations, and governments.

ChatGPT

It is a very disruptive technology that's already changing how many people learn and work.

Many developers think that generative AI will empower many people and lead to productivity gains, and also
make a significant contribution to global economic growth.

But there could be downsides as well, since it's job loss or worse that some people worry about.

In this course, you learn what generative AI is, what it can and cannot do, and also how to use it in your own
work or business.

Because generative AI is so new, there is still a lot of misinformation out there, and so in this course, I hope to
convey an accurate non-technical understanding of what it really is.

It also works for you to think through how you can best make use of this technology.

This course does not assume any technical or AI background and is designed to be useful to anyone in
business, science, engineering, the humanities, arts, or other sectors so that, let's dive in.

Generative AI has caught the mainstream attention starting around November 2022 when OpenAI released
ChatGPT, and its momentum has continued unabated.

2022 11 OpenAI

ChatGPT

According to McKinsey, it could add $2.6 to $4.4 trillion annually to the economy.

2.6 4.4

Goldman Sachs estimates it could raise global GDP by 7% in the next decade.

GDP

7%

And a study by OpenAI and UPenn estimates that it could impact 10% of the work or tasks carried out daily by
over 80% of workers in the United States.

OpenAI

80%

10%

The same study also estimates that there is a 20% of workers whose work or task is more than 50% impacted by
generative AI.

20%

50%

And so, studies like these lead to hopes for a tremendous productivity gain, as well as worries about job loss
through automation.

What is generative AI?

This term refers to AI, or artificial intelligence systems that can produce high-quality content, specifically text,
images, and audio.

One of the best-known generative AI or GenAI systems is OpenAI's ChatGPT, which can follow instructions to
carry out tasks like writing three captions for a social media post about our new line of sunglasses for robots, and
have it generate a variety of creative outputs.

GenAI

OpenAI ChatGPT

Many users are familiar with websites or direct consumer applications that can generate texts like this.

Other examples include Bard, which is offered by Google, as well as Bing Chat offered by Microsoft.

Bard

Bing Chat

But there are now many companies that are offering user interfaces that let you type in some text called a
prompt and will generate a response.

But beyond these consumer applications, there's one other application of generative AI that I think may turn out
to be even more impactful in the long term, which is the use of generative AI as a developer tool.

AI is already pervasive in our lives and many of us use it dozens of times a day or more without even thinking
about it.

Every time you do a web search on Google or Bing, that's AI.

Every time you use your credit card, there's probably an AI checking if it really is you using your credit card.

Or every time you go to a website like Amazon or Netflix and it recommends products or movies to you, that's AI.

But many AI systems have been complex and expensive to build, and generative AI is making many AI
applications much easier to build.

This means that the number and variety of AI product offerings is blossoming because it's becoming much
cheaper to build certain AI applications compared to before.

In this course, one of the things we'll touch on a few times as well will be how generative AI may allow your
business to much more inexpensively build very valuable AI applications.

And you learn best practices for identifying and exploring whether or not such applications might be useful for a
given business.

I've described generative AI as generating text, images and audio, and of these three types of contents, the
biggest impact so far has been on text generation.

But it can also generate images where given instructions, a different type of prompt.

It can generate beautiful images like this one, or even a photo-realistic image like this.

Generative AI can also generate audio.

For example, here is a voice clone of me.

Hi, I'm an AI-generated voice clone of Andrew.

Andrew

Andrew never actually said these words.
Andrew

Isn't that cool?

You can also put audio together with image or even video generation to create a video clone of me like this.

Hi, I'm a video clone of Andrew, it's nice to meet you.

Andrew

There's a lot going on in generative AI, and this is an exciting and disruptive technology that I'm confident you
will find useful in your work.

In this course, during the first week, we'll go through how generative AI technology actually works and
specifically what it can and cannot do, and you also see a variety of common use cases that I hope will help
spark your creativity to how you may use it to create value in your life or your work.

In the second week, we'll discuss generative AI projects.

Specifically how to identify useful generative AI applications, as well as best practices for how to go about
building them, and

we'll take a deeper dive into the range of technology options for building a variety of valuable projects.

In the final week, we will zoom out beyond a single project to look at how generative AI will impact businesses as
well as society at large.

We'll look at some best practices for how teams within a company can take advantage of generative AI and also
take a look at AI risks and how to make sure that what we do with AI is responsible and benefits people.

I'm excited to dive into this material with you.

Until then, let's go on to the next video where we'll go through a non-technical description of how generative AI
technology actually works.

I'll see you in the next video.

02 How Generative AI works

The ability of systems like ChatGPT and Bard to generate text seems almost magical.

ChatGPT Bard

They do represent a big step forward for AI technology.

But how does text generation actually work?

In this video, we'll take a look at what actually underlies the generative AI technology, and this will hopefully help
you understand what you can use it for and also when you might not want to count on it.

Let's take a look.

Let's start by looking at where generative AI fits within the AI landscape.

There's a lot of buzz and excitement and also hype about AI, and I think a useful way to think of AI is as a
collection or as a set of tools.

One of the most important tools in AI is supervised learning, which turns out to be really good at labeling things.

Don't worry if you don't know what this means, we'll talk more about it on the next slide.

Second to it that started to work really well only fairly recently is generative AI.

If you study AI, you may recognize that there are other tools as well, such as things called unsupervised learning
and reinforcement learning.

But for the purposes of this course, I'm going to touch briefly on what is supervised learning and then spend
most of our time talking about generative AI.

These two, supervised learning and generative AI, are the two most important tools in AI today.

For most business use cases, you should be fine if you just not worry about the other tools than these for now.

Before describing how generative AI works, let me briefly describe what is supervised learning because it turns
out generative AI is built using supervised learning.

Supervised learning is the technology that has made computers very good at given an input, which I'm going to
call A, to generate a corresponding output, which I'm going to call B.

A

B

Look at a few examples.

Given an email, supervised learning can decide if that email is spam or not.

The input A is an email and the output B is either zero or one, where zero is not spam and one is spam.

A

B

This is how spam filters work today.

As a second example, probably the most lucrative application, not the most inspiring, but lucrative for some
companies that I've ever worked on was online advertising, where given an ad and some information about a
user, an AI system can generate an output B corresponding to whether or not you're likely to click on that ad.

B

By showing slightly more relevant ads, this drives significant revenue for the online ad platforms.

In self-driving cars and in driver assistance systems, supervised learning is used to take as input a picture of
what's in front of your car and radar info and label that with the position of other cars.

Give it a medical x-ray, it can try to label that with a medical diagnosis.

X

I've also done a lot of work in manufacturing defect inspection where you can have a system take a picture of a
phone as it rolls off the assembly line and check if the phone has any scratches or other defects.

Or in speech recognition, the input A would be a piece of audio and we would label that with the text transcript.

A

Or as a final example, if you run a restaurant or some other business where occasionally you have reviews
written about your business or your products, supervised learning can read those reviews and label each one as
having either a positive or a negative sentiment.

This is useful for reputation monitoring of the business.

It turns out the decade of around 2010-2020 was a decade of large-scale supervised learning.

2010-2020

I want to touch on this briefly because it turns out this laid the foundation for modern generative AI.

But what we found starting around 2010 was that for a lot of applications, we had a lot of data, but even as we
fed it more data, its performance wasn't getting that much better if we were training small AI models.

2010
AI

This means, for example, if you were building a speech recognition system, even as your AI listened to tens of
thousands or hundreds of thousands of hours of data, that's a lot of data, it didn't get that much more accurate

compared to a system that listened to only a smaller amount of audio data.

AI

But what more and more researchers started to realize through this period is if you were to train a very large AI
model, meaning an AI model on very fast, very powerful computers with a lot of memory, then its performance as
you fed it more and more data will just keep on getting better and better.

AI

AI

In fact, years ago when I started and led the Google Brain team, the primary mission that I set for the Google
Brain team in the early days was I said, let's just build really, really large AI models and feed them a lot of data.

Google Brain

AI

And fortunately, that recipe worked and ended up driving a lot of AI progress at Google.

AI

Large-scale supervised learning remains important today, but this idea of very large models for labeling things is
how we got to generative AI today.

AI

Let's look at how generative AI generates text using a technology called large language models.

AI

Here's one way that large language models, which I will abbreviate LLM, can generate text.

LLM

Given an input like, I love eating, this is called a prompt, an LLM can then complete this sentence with maybe
bagels with cream cheese, or if you run it a second time, it might say, my mother's meatloaf, or if you run it a
third time, maybe it'll say out with friends.

「I love eating」

LLM
「my mother's meatloaf」

「bagels with cream cheese」

「out

with friends」

How does an LLM, a large language model, generate this output?

LLM

It turns out that LLMs are built by using supervised learning.

LLM

That's a technology to input A and output a label B. It uses supervised learning to repeatedly predict what is the
next word.

A

B

For example, if an AI system has read on the Internet a sentence like, my favorite food is a bagel with cream
cheese, then this one sentence will be turned into a lot of data points for it to try to learn to predict the next word.

AI

「my favorite food is a bagel with cream cheese」

Specifically, given this sentence, we now have one data point that says, given the phrase, my favorite food is a,
what do you think is the next word?

「my favorite food is a」

In this case, the right answer is bagel.

bagel

Also, given my favorite food is a bagel, what do you think is the next word?

「my favorite food is a bagel」

It's with, and so on.

with

This one sentence is turned into multiple inputs A and outputs B for it to try to learn from where the LLM is
learning given a few words to predict what is the next word that comes after.

A

B

LLM

When you train a very large AI system on a lot of data, a lot of data for LLMs means hundreds of billions of
words, and in some cases, more than a trillion words, then you get a large language model like ChatGPT that's
given a prompt is very good at generating some additional words in response to that prompt.

AI

LLM

ChatGPT

For now, I'm omitting some technical details.

Specifically, next week, we'll talk about a process that makes LLMs not just predict the next word, but actually
learn to follow instructions and also be safe in what it outputs.

LLM

But at the heart of LLMs is this technology that's learned from a lot of data to predict what is the next word.

LLM

That's how large language models work; they're trained to repeatedly predict the next word.

It turns out that many people, perhaps including you, are already finding these models useful for day-to-day
activities at work to help with writing, to find basic information, or to be a thought partner to help think things
through.

Let's take a look at some examples in the next video.

03 LLMs as a thought partner

There are quite a few web interfaces where you can access a Large Language Model.

ChatGPT is the best known one and Google's Bard, Microsoft Bing and quite a few others also work well.

ChatGPT

Bard

Bing

Let's take a look at how people are using these LLM applications.

Whether or not you're already using them regularly, I hope that this will give you some new ideas for when and
how they could be useful to you.

LLMs are giving a new way to find information.

For example, if you ask it what's the capital of South Africa, it may give a response like that.

Now as we'll see later, LLM can sometimes make facts up.

We call this hallucination.

If you're really relying on getting the right answer to the question, it may be useful to double check the answer
with an authoritative source before counting on it.

But in this case, it does get the capital or three capitals of South Africa right.

And sometimes a back and forth with an LLM is helpful too, for example, if you ask what does LLM stand for, it
might answer, LLM stands for Legum Magister, which is a term used in law, and it's actually a pretty common
use of the acronym LLM on the Internet.

Magister

LLM
LLM

LLM

Legum

But if you were to then say what about in the context of AI? Then hopefully it'll say in the context of AI and LLM
refers to a Large Language Model.

Sometimes this back and forth can help you give the right context, the LLM to give you the information you're
looking for.

LLM

LLM can also sometimes be a thought partner to help you think things through.

For example, I often use an LLM to help me refine my writing.

If you were to tell it, rewrite this for clarity, since all around the world are realizing learning has happened and so
on.

Leading Elms are actually pretty good at rewriting texts for you.

Or here's a fun example, if you were to tell it, to write a three did word story involving trucks.

Maybe because you have a child that likes trucks like I do, my son love trucks.

But to encourage them to brush the teeth, then leading Elms can actually create pretty fun and interesting
stories.

I don't think this is nearly as good as the stories written by the great novelist, but for a quick fun thing, I think it's
not bad.

Now, there will be times when you're looking for a piece of information and you might be wondering, "Should I
use web search or use an LLM?"

「

」

So If you're playing a sport and unfortunately wound up with a sprained ankle and want to know what to do about
it, web search can lead you to pretty authoritative and I think trustworthy sources that can give advice on how to
approach medical matters.

For example, web pages from the Mayo Clinic or from Harvard Health.

These seem like they would be trustworthy sources for what to do about the sprained ankle.

You could also ask an LLM what to do about the sprained ankle and it will generate some answer.

But given the propensity of LLM's to make things up and sometimes sound very authoritative and confident when
making things up, I would probably want to double check anything it says about healthcare or medicine before
following the suggestions.

Here's one more example.

If you want to make a pineapple pie and they're looking for a recipe, it turns out there are lots of recipes on the
Internet for a pineapple pie, and picking one created by a trusted website or a trusted chef, that might get you
pretty good results.

Or you can ask an LLM to make one up for you, and in that case, it'll come up with something that frankly might
be okay, but also has a high chance of being a somewhat strange recipe.

So if you want to bake a pineapple pie, I would probably go find a webpage because there are multiple web
pages that will give a good solid answer to what's a good pineapple pie recipe.

But if you were to look for something more esoteric, say your friend challenges you to make coffee-infused
pineapple pie, there aren't any web pages that I could find really on coffee-infused pineapple pies.

I don't think there is currently a single webpage that gives a good answer to this.

This would be one example where an LLM can help be a thought partner to think through how you might go
about baking a coffee-infused pineapple pie.

These are just some of the tasks for which you might find the web user interface for LLM useful.

We'll explore more examples, discuss strengths and weaknesses of LLMs, and go through some best practices
later this week.

But as you can see from this video, Generative AI is capable of many different things.

AI

In the next video, we'll more systematically discuss Generative AI as a general-purpose technology as well as
start to come up with a way to organize all of these things that they can do, which includes writing, reading, and
chatting tasks.

AI

Let's go take a look at that in the next video.

04 AI is a general purpose technology

What is Generative AI good for?

One of the reasons that question is a bit hard to answer is because AI is a general-purpose technology.

Unlike a lot of technologies like a car which is good for transportation or microwave oven good for heating food,
AI isn't useful just for one thing.

It's useful for a lot of things and that almost makes it harder to talk about.

But let's take a look at what a general-purpose technology really means.

Similar to electricity, AI is useful for many tasks.

If we were to ask you, what is electricity good for or what is the Internet good for?

These are other general-purpose technologies and it's almost difficult to think what is electricity good for because
it's so pervasive and it's used around us for so many different things.

In fact, as you saw earlier, supervised learning is useful for many tasks like spam filtering, advertising, speech
recognition, and many others.

Generative AI is like this too.

In the last video, you saw a few of the tasks that an LLM can carry out, answering certain questions and hoping
with writing for example.

LLM

Let's discuss more broadly a framework for what tasks LLMs can do.

LLM

First off, Generative AI generates texts.

Not surprisingly, perhaps it's useful for writing.

I routinely use Generative AI tools as a brainstorming companion.

If you're trying to name a product, you can ask it to brainstorm some names and it comes up with some creative
suggestions.

LLMs can also be good at answering questions, and if you give them access to information specific to a
company, they can help members of your team find information that they need.

LLM

In this case, about the availability of parking at the office.

In addition to writing, Generative AI is also good for what I'm going to call reading task, where you're going to
give it a relatively long piece of information and have it generate a short output.

For example, if you run an online shopping e-commerce company and you get

a lot of different customer emails, Generative AI can read the customer emails and help you very quickly figure
out is this email a complaint or not, which can be used for helping to route complaints to the appropriate
department to be handled quickly.

Given, I love my new llama t-shirt, fabric is so soft, that's not a complaint.

T

But if someone emails, I wore my Ilama t-shirt to friend's wedding and now they're mad at me for stealing the
show.

Well, maybe that is a complaint.

T

But Generative AI can help you route emails to the right departments.

I call this a reading task because it's looking at a relatively long piece of text, that is a customer email, and then
generating a relatively short output, just yes or no, is this a complaint or not?

While supervised learning can also be used for this particular task, we'll see later that Generative AI is allowing
this source of reading tasks and other examples that we'll see later this week to be built much more quickly and
inexpensively.

Lastly, Generative AI is also used for many chatbot types of tasks.

Whereas ChatGPT, and Bard, and Bing chat are general-purpose chatbots.

ChatGPT Bard Bing

Generative AI technology and large language models is also enabling many special-purpose chat bots to be
built.

In this example, here's what a chatbot might be like for taking online orders where a user can say, I like a
cheeseburger for delivery and the chatbot acknowledges and puts the order through for the user.

Now in talking through these tasks, I find that it's sometimes useful to distinguish between two different types of
LLM-based applications.

LLM

One is examples like this brainstorming one, where it could be quite natural for you to type a prompt like this into
ChatGPT, or Bard, or Bing chat, or one of the other free or paid large language models on the Internet and get a
result back.

ChatGPT Bard Bing

I'm going to call an application like this a web interface-based application.

In contrast, in the example of recognizing if an email is a customer complaint, this fits more into a company's
email routing workflow, and it doesn't really make sense for anyone to cut and paste customer emails one at a
time into a web interface to get back answers as to which ones are actually complaint emails.

This is an example of an LLM that would make sense when it's built into a larger software automation, that in this
case helps with a company's automated email routing.

LLM

I'm going to call this a LLM-based software application, the second writing example of answering HR questions.

LLM

It turns out this also will make more sense as a software-based LLM application because it'll need access to
information about your specific company's parking policy for employees, whereas a general large language
model on the Internet probably doesn't have that information.

LLM

We'll talk more later in this course about how this technology is built and most of the specialized chatbots will
also be software-based LLM applications.

LLM

In the rest of this course, I'm going to use these two symbols to distinguish between web interface use cases
and software-based LLM applications.

LLM

For many people, it may be easier to get started with some of the web interface use cases because you can just
go to a website like ChatGPT, or Bard, or Bing and type in a prompt, and get the result back.

ChatGPT Bard Bing

But I think both the web interface-based applications and the software-based LLM applications are important and
will be very useful for individuals and for companies.

LLM

I found that the framework of writing, reading, and chatting as a useful way to think about the many different
tasks that LLM a large language model can do.

LLM

In the next three videos, we'll dive more deeply into many different examples of writing, reading, and chatting
tasks.

I hope that you'll find some of them potentially useful for your own work.

I look forward to seeing you in the next video, we'll talk more about writing, and until then, I look forward to enjoy
my burger.

05 app Writing

In the last video, we looked at writing, reading and chatting as three major categories of tasks that you can get
an LM to do.

Given that large language models were trained to repeatedly predict the next word, maybe it's no surprise that
they're pretty good at writing at generating words.

And it turns out that many writing tasks can be done via a web user interface.

So I hope you find this video where we'll dive more into writing tasks immediately useful.

For writing tasks broadly, what we typically do is start with prompts and use a relatively short prompt to write or
to generate a much longer piece of text.

So let's take a look at some writing applications.

I often use the web interface of large language models as a brainstorming partner.

If you ask it brainstorm 5 creative names for peanut butter cookies, it actually comes up with some pretty
creative names Nutty Nirvana Nibbles, I would eat that.

5

「Nutty Nirvana

Nibbles」

Or if you ask it to brainstorm ideas for increasing cookie sales, then it comes up with a few ideas and you can
take a look to see if any of these may be useful.

You can also use a large language model, again, maybe the web interface version, to write some copy for you.

Let's start with an example.

If you were to ask it to write a press release announcing the hire of a new COO, a new chief operating officer for
your company, it may come up with a piece of text like this Company Name Welcomes, New COO's Full Name
as, so on and so forth.

「

COO

」

And this is a pretty generic press release.

COO

When writing a prompt, you find that if you can give the large language model more context or more background
information, then it will write more specific and better copy for you.

If all that the large language model sees is this writer a press release, at this point in time, it doesn't know
anything about your company, about the new CEO's name or their qualifications and so it ends up writing
something very generic like this.

CEO

If you end up prompting a large language model like this, it's not a problem.

You may realize that you wound up with a very generic press release and decide to update the prompt to give it
more information.

And so if you were to prompt it and say, use the following information for the press release, this is a COO bio,
this is the name of our company and some details about our company, then it will write a much more detailed
and insightful press release specific to the CEOs joining this company.

I find that when prompting an LM, I'll often not get the prompt right the first time, like what we saw just now,
where we had the prompt press release announcing the new hire of COO without giving any context.

COO

CEO

LM

And that's totally fine.

COO

If you see the result isn't what you want, just revise the prompt and try again.

I'll say more about this in a later video this week, when we talk about tips for writing effective prompts.

Let's look at one more example.

Another writing task that I sometimes use LLMs for is translation.

LLMs

In fact, some of the large language models you can access via Web UI are competitive and sometimes even
better than the dedicated machine translation engines already, especially for languages with a lot of text on the
internet.

Web

And so where the large language model has a lot of data to learn how to generate text in that particular
language, it tends to do less well in languages, also called low resource languages, with less text on the Internet
in that language.

But if you're operating a hotel and you want to translate the welcome message into formal Hindi to welcome
guests, then a large language model may be able to output text like this for you.

Unfortunately, I don't speak Hindi, I wish I did, but it turns out that this particular translation is only so-so; the
word 'front desk' it translates into 'the desk at the front' rather than 'reception', which is what we mean when we
say 'the front desk' of a hotel.

'

'

'

'

'

'

'

'

So if you're working with a Hindi speaker, and I was when preparing the slide, then they may be able to give you
some tips to say, this is some sort of not quite the best formal Hindi, but if you were to tell it to translate this into
formal spoken Hindi, then it updates this text to make 'front desk' translate into the Hindi word for 'reception',
which is a much better translation.

'

'

'

Now, here's one fun thing I've seen recently in the AI community, which is a lot of us that are working with
translation often need to translate text into languages that we don't speak ourselves.

'

So how can we tell if the large language model is doing something reasonable?

And in fact, even if you have, say, one Hindi speaker on your team, if other members of the team don't speak
Hindi, how can they figure out what's going on?

So what I'm seeing multiple teams in the AI community do is translate text into pirate English for testing
purposes.

And so if you were to prompt a large English model to translate this into pirate English, you get, 'Ahoy matey, we
be hoping you'll relish your time aboard the Oceanview Inn.'

「Ahoy matey, we be hoping you'll

relish your time aboard the Oceanview Inn.」

That sounds like pretty good pirate English to me.

So that hobby grand worthy models be used for writing.

Let's move on to peepin at Reading House.

06 app Reading

In the last video, we looked at writing tasks where you would specify a prompt to the last Larch language model,
and have it generate a comparatively longer output than the input prompt.

It turns out, is also useful for many reading tasks, and by that I mean tasks where you would input a prompt, and
then have it generate usually a similar length or often shorter output than the input prompt.

Let's take a look at some reading tasks starting with something that I use myself all the time, which is
proofreading.

Many times if I'm writing a piece of text, I will read through it carefully three or four times myself for spelling and
grammatical errors, and even though I thought I proofread it carefully myself, a line model will still find errors in it
that somehow I had missed.

Here's an example of a prompt that you could try: "Proofread the following text," and I find that if you tell it what
you want the text before.

「

」

Here's text intended for a website selling children's stuffed toys, and sometimes I ask it to check for spelling and
grammatical errors as well as awkward sentences, and then have it rewrite it with corrections.

This is a piece of text with some errors, and the output of the Larch language model fixes, snuggle was
misspelled and it fixes this little piece of grammar over here.

"snuggle"

When I'm writing text myself, that I want to be quite confident it's free of spelling and grammatical errors, and
sometimes also awkward sentences, I actually use this myself to proofread what I write.

A second reading task that Larch language models are often used for is to summarize long articles.

One of my collaborators, Erik Brynjolfsson, who's a Stanford professor, once sent me an email linking to an
article that he had written titled "The Turing Trap."

「

」

·

I knew it was a good article, but it was a very long article and I didn't have time to read the whole thing before I
responded to his email.

I actually used the following prompt and copy-pasted his entire article into a web interface of a Larch language
model, and had it quickly generate a summary for me.

It turns out this paper that he had written talks about how human-like AI offers benefits, but there's a lot to be
done by having AI augment humans rather than automate.

But the point of Brynjolfsson's article on the Turing Trap was he was advocating that instead of having AI
automate or replace human work, we should put more effort into having AI complement or to augment human
work.

With a Larch language model summarizing this long article, I was able to get back on this faster than if I had to
read the entire article myself.

By the way, this is a good article.

Eventually, I did read the entire article myself, and I really enjoyed it, but today, I do sometimes use Larch
language models to summarize for me things that I don't have time to read in its entirety.

This is a use case that you could go to one of the web interfaces of a Larch language model and use relatively
quickly yourself.

Now it turns out there's a software application version of this too that is taking off in businesses.

Let me illustrate this with an example.

Say you're a manager of a customer service call center where you have many customer service agents, like this
person shown on the left with the microphone, having phone calls with customers, like this person shown on the
right.

If you have permission to record these phone calls between the agents and the customers, you can then run the
phone calls through a speech recognition system to get a text transcript of the conversation.

If you have many customer service agents having conversations, you end up with a lot of text transcripts.

If you want to review what's going on in your call center, you probably end up with too much text to read.

Given a text transcript like this between the customer and an agent, what really happened in this call?

One use of Larch language models would be to have it summarize this entire conversation and generate a short
summary.

Like MP401-27KX was reported as broken, and so on.

MP401-27KX

If you were to take all of these different text transcripts and have a software application to generate the
summaries, then you as a manager of this can take a quick look at all of these summaries and just spot if there
are any issues, or any trends that you want to be aware of.

A system like this would be implemented as a software application that uses a Larch language model, because it
doesn't really make sense for you or anyone else to copy paste these conversations one at a time into the
website of a Larch language model provider.

In terms of customer service interactions, Larch language models are also used for customer email analysis.

In an earlier video, you saw the example of taking a customer email, and deciding if it's a complaint, in this case,
no, as well as what department to route this email.

This will be another software application that uses a Larch language model.

Let's take a deeper look at how one could build this application, focusing on the part of deciding what
department to route this email.

One thing you could do is write a prompt to tell the LOM to read the email and decide which department to route
it to.

You can specify the task and provide the email.

LOM

But it turns out that with a prompt like this, you may find that the algorithm routes it to the complaints department
in this case, which may or may not be a department that exists in your organization.

This would be an example of where the LLMs has been given insufficient context to know what are the names of
the actual departments in your company that it should choose from.

LLMs

In contrast, if you were to update the prompt as follows, and say, read the email, choose the most appropriate
department to rouse it to, and choose department only from the following list.

In this case, given the set of choices you wanted to choose from, routes it to the apparel department correctly.

The process of building an application using a Larch language model is again, not a lot uncommon.

To write a prompt that doesn't quite work right the first time, and when you find it, route it to a nonexistent
complaint department, then just update the prompt and that fixes the problem.

One last application that I want to touch on is reputation monitoring, where you can use an LLMs to build a
dashboard to track your customer sentiments, positive or negative, of your business or your products over time.

LLMs

For example, if you run a restaurant and occasionally your customers write online reviews or send your emails
describing their experience, you can then use a prompt like this.

Read the following review and classify it as having positive or negative sentiment, to have it decide automatically
if each review was positive or negative.

In this case, if the food was amazing or service friendly, that would be classified as having a positive sentiment.

Then by having software count the number of positive reviews per day, as well as the number of negative
reviews per day, you can build a dashboard that tracks per day, all the time, how the sentiments are trending.

Looks like the customer sentiment is pretty positive, but if ever it starts trending negative like this, with more
negative reviews, then this dashboard can alert you to that maybe something's happening that we should pay
attention to, and see if there's something we need to fix at the restaurant.

In this video, we looked at a number of reading applications, including proofreading, summarization, email
routing, restaurant review sentiment analysis.

If you can think of tasks where you wish you had someone that could read a piece of text and just say a few
things or give a few quick indications of what was in that piece of text, that could be a good candidate for a
reading task to get an LLMs to do for you.

LLMs

Next, let's go onto the next video to take a look at chatting tasks.

07 app Chatting

In the last two videos, we looked at writing and reading applications.

In this video, we'll look at chatting applications.

In addition to the general purpose chatbots like ChatGPT, bot, and Bing chat.

ChatGPT bot Bing

Many companies are looking at whether they can build specialized chat applications.

If you're involved in a company where you have many people interacting with customers or having certain types
of conversations of similar nature, this may be a case where you can consider whether or not a specialized
Chatbot can help with those types of conversations.

Let's take a look.

Earlier we already saw the example of a customer service Chatbot that might better take orders for
cheeseburgers.

Another example of a specialized Chatbot would be one that specializes in helping you to plan trips.

How can one vacation in Paris inexpensively?

A bot could be built to have specialized knowledge about travel.

Today, there are companies exploring a wide range of advice bots.

For example, can a bot give you career coaching advice or give advice on cooking a meal?

A large variety of specialized bots that are really good at answering questions about one thing are being
developed by different companies today.

Some of these bots are capable of just having a conversation and giving advice.

Some of these bots can also interface with the rest of a company's software system and take actions such as to
put in an order for a cheeseburger to be delivered.

Another example of a bot that might be able to take action would be a customer service chatbot.

Where it turns out that many IT departments get tons of password reset requests.

IT

If a bot can take care of that, then it may take some of the workload off your IT department.

IT

A bot like this that needs to send a text message to verify identity and actually help reset the password.

This is a bot that would need to be empowered to actually take action in the world such as to get a text message
to be sent to someone.

Next week we'll discuss more about how chatbots like these are built that don't just generate text but can actually
take action.

Because of the number of customer service organizations exploring the use of chatbots, I want to share with you
a range of the spectrum of common design points being used by different businesses.

For this slide, I want to focus on text-based chat rather than voice or phone-based chat.

At one end of the spectrum would be a customer service center with only humans.

You would have human service agents typing back and forth messages like, "Welcome to Better Burgers, let me
place the order for you."

「

」

At the opposite end of the spectrum would be Chatbots only where you just have software responding directly to
customers.

But between these two ends of the spectrum of humans typing of the keyboard or Chatbots only, there are a
couple of common design points.

One common design point would be to have bots support humans.

In which a bot will generate a suggested message for a human but the human service agent will review the
message and either approve it if it looks good.

Or have a chance to edit the message before it is actually sent back to the customer.

This type of design is often also called human in the loop.

Because as a human, there's a lot in and it's part of the process before the message actually gets sent back to
your customer.

This is a way to mitigate the risk of the Chatbot maybe saying the wrong thing.

Because a human can check over it before it's actually sent back to your customer.

In the next video, when we talk about what LLMs can and cannot do, we'll go over some of the mistakes that
LLMs can sometimes make.

LLMs

LLMs

This design helps protect against those mistakes of LLMs.

LLMs

A little bit further on the automation spectrum would be if you have a bot to triage messages for humans.

Maybe the bot answers the easy messages but escalates to a human for the things that it isn't quite ready to
handle yet.

Sometime back, I actually led the team that built a bot that would automatically detect if the customer was asking
for a refund request.

It turns out that was about 10% of our total chat call volume.

10%

By just detecting that and automatically giving the customer instructions just routed 10% or so of the traffic away
from the human agents and so to save the agents a lot of time and let the humans focus on servicing the harder
requests.

10%

But this type of triage is another common design to help your human service agents save time and have to focus
only on the harder cases.

That they're more uniquely qualified to handle.

In many customer service centers, a single human may be simultaneously having chat conversations with four or
eight, or in some extreme cases, maybe even 16 customers at the same time.

16

With bots supporting the humans, it becomes easier for a human to manage a larger number of parallel
conversations.

Given that bots sometimes say the wrong thing, I want to share with you what building and deploying a bot often
feels like in companies that want to do this in a safe way.

Often, companies will start with an internal-facing Chatbot.

Many times I would build a Chatbot, but let only my own team use it to say, answer the questions about travel or
whatever the bot is supposed to do.

Assuming your internal team will be more sympathetic and more understanding of mistakes and be more
forgiving if the bot says something wrong at one time, this gives you some time to assess the behavior of the bot
and also avoid public mistakes that could be embarrassing for the company.

After this looks safe enough, a common next step would be to deploy with human in the loop.

To let the human check over many of the messages if feasible, before it actually goes out to the customer.

After doing this for a while if it looks like the bot's messages are generally safe to send to customers, then you
might allow the bot to communicate directly with customers.

Of course, the details of every business differ.

For some applications, it may not be practical to have humans check over every message because of the sheer
volume of traffic.

But depending on the risk of the bot saying the wrong thing as well as the volume of traffic, and thus whether or
not human in the loop is feasible, these are some of the design patterns I've seen companies use to try to deploy
bots safely.

To summarize, we've seen how LLMs can be used for writing, reading, and chatting.

LLMs

These three categories are not meant to be an exhaustive list of what LLMs can do, but they are just a few broad
categories of what you might really use them for.

LLMs

LLMs can do a lot, but they can't do everything.

LLMs

In the next video, let's take a look at what LLMs can and cannot do and better understand the limitations.

LLMs

Let's go on to the next video.

08 What LLMs can and cannot do

Generative AI is an amazing technology, but it can't do everything.

AI

In this video, we'll take a careful look at what LLMs can and cannot do.

LLMs

We'll start off with what I found to be a useful mental model for what it can do, and after that, let's look together at
some specific limitations of LLMs.

I found that understanding the limitations can lower the chance that you might get tripped up trying to use them
for something that they're really not good at, so let's dive in.

LLMs

If you're trying to figure out what prompting an LLM can do, here's one question that I found to provide a useful
mental framework.

LLM

Which is I'll ask myself, can a fresh college grad, following only the instructions in the prompt, complete the task
you want?

For example, can a fresh college grad follow instructions to read an email to determine if an email is a
complaint?

Well, I think a fresh college grad could probably do that, and an LLM could do that pretty well too.

LLM

Or can a fresh college grad read a restaurant review to determine if it's a positive or negative sentiment?

I think they could do that quite well too, and so too can prompting an LLM.

LLM

Here's another example, can a fresh college grad write a press release without any information about the COO
or your company?

Well, this fresh college grad just graduated from college. They only just met you and don't know anything about
you or your business, and so the best they could do is maybe write a really generic and not quite satisfying press
release like this.

But on the flip side, if you were to give them more context about your business and about the COO, then we can
ask, can this fresh college grad write a press release given the basic relevant context?

And I think they may be able to do that decently well, and so too, can the large language model.

When you're picturing an LLM as doing many of the things that a fresh college grad might be able to do, think of
this fresh college grad as having lots of background knowledge that they know, lots of general knowledge off the
Internet.

LLM

But they have to complete this task without access to a web search engine, and they don't know anything about
you or your business.

For clarity, this mental model thought experiment, fresh college grad has to complete a task with no training
specific to a company or your business.

And every time you prompt your LLM, the LLM does not actually remember earlier conversations.

LLM

LLM

And so it's as if you're getting a different fresh college grad for every single task, so you don't get to train them up
over time on the specifics of your business or the style you want them to write.

This rule of thumb of asking what a fresh college grad can do is an imperfect rule of thumb, there are things
college grads can do that LLMs cannot and vice versa.

LLMs

But I found this to be a useful starting point for thinking through what LLMs can and cannot do.

LLMs

And while we're focused on this slide on what prompting an LLM can do, next week when we talk about
generative AI projects, we'll talk about some slightly more powerful techniques that might be able to expand what
you can do with generative AI beyond this fresh college grad concept.

LLM

AI

AI

Now, let's take a look at some further specific limitations of LLMs.

LLMs

First, is knowledge cutoffs.

An LLM's knowledge of the world is frozen at the time of its training.

LLM

More precisely, a model trained on Internet data scraped by January 2022, will have no information about more
recent events.

2022 1

So given such a model, if you were to ask it, "What was the highest grossing film of the year 2022?" It would say
it doesn't know.

「2022

」

Even though now that we're well past 2022, we know that it was the movie "Avatar: The Way of Water" that was
the highest grossing film.

2022

Around July 2023, there were claims of a research lab having discovered a room temperature superconductor
called LK-99.

2023 7

LK-99

You may have seen this picture in some of the news, this claim turned out not quite to be right.

But if you were to ask an LLM about LK-99, even though it's widely covered in the news, if the LLM learned only
from text on the Internet as of January 2022, it won't know anything about this.

LLM

LK-99

LLM

2022 1

So this is called a knowledge cutoff, where the LLM knows things about the world only up to a certain moment in
time.

LLM

When it was trained, or when text from the Internet was last downloaded for the LLM's training.

LLM

A second limitation of LLMs is that they will sometimes just make things up, and we call these hallucinations.

LLMs

I found that if I ask an LLM to give me some quotes from well-known people in history, it will often make up the
quotes.

LLM

For example, if you ask it, "Give me three quotes that Shakespeare wrote about Beyoncé." Since Shakespeare
lived and died well before Beyoncé, I don't think Shakespeare said anything about Beyoncé.

「

」

But LLM will confidently give you back some quotes like "her vocals shine like the sun," or "all hail the queen,
she is most worthy of love."

LLM

「

」

「

」

So these are hallucinated Shakespearean quotes.

Or if you ask it to list court cases tried in California about AI, it might give authoritative sounding answers like
this.

AI

And in this case, it turns out the first case is real, there was a Waymo versus Uber case, but I was not able to
find an Ingersoll versus Chevron case, and so the second case is a hallucination.

Waymo Uber

Ingersoll

Chevron

Sometimes LLMs can hallucinate things or make things up in a very confident, authoritative-sounding tone.

LLMs

And this can mislead people into thinking that this made-up thing may actually be real.

Hallucinations can have serious consequences.

There was a lawyer that unfortunately used ChatGPT to generate text for a legal case and actually submitted it
to the court, not knowing that he was submitting to the court illegal filings with lots of made-up court cases.

ChatGPT

And in this New York Times headline, we see in this cringe-inducing court hearing.

The lawyer who relied on AI said she did not comprehend that the chatbot could lead him astray, and this
particular lawyer was sanctioned for submitting a co-filing for made-up things.

AI

So understanding of limitations is important if you are using this for documents of real consequence.

LLMs also have a technical limitation in that the input length, that is, the length of the prompt is limited, and so is
the output length of the text it can generate.

LLM

Many LLMs can accept a prompt of up to only a few thousand words, and so the total amount of context you can
give it is limited.

LLM

So if you were asking it to summarize a paper, and the paper's length is much longer than this input length
limitation, the LLM may refuse to process that input.

LLM

In this case, you may have to give it one part of the paper at a time, and ask it to summarize parts of the paper at
a time.

Or sometimes you can also find an LLM with a longer input limit length, some will go up to many tens of
thousands of words.

LLM

And technically, LLMs have a limitation on what's called the context length, and the context length is actually a
limit on the total input+output size.

LLM

+

When I use LLMs, I rarely have it generate so much output that I run into limitation really on the output length.

LLM

But I do hit input length limits sometimes if I have many, many thousands of words of context that I want to give
it.

Lastly, one major limitation of generative AI is that they do not currently work well with structured data.

AI

And by structured data I mean tabular data, like sort of data that you might store in an Excel or Google Sheets
spreadsheet.

Excel Google Sheets

For example, here is a table of home prices with data on both the size of the house in square feet, as well as the
price of the house.

If you were to feed all of these numbers into an LLM and then ask it, "I have a house that's 1,000 square feet,
what do you think is a good price?" LLMs are not really good at that.

LLM

「

1000

」

LLM

Instead, if you call the size the input A, and the price the output B, then supervised learning would be a better
technique with which to estimate the price as a function of the size.

A

B

Here's another example of structured data of tabular data showing when different visitors may be visiting your
website, how much you offered a product to them, and whether or not they purchased it.

Then again, supervised learning would be a better technique than trying to copy-paste all of this time, and price,
and purchase information into the prompt of a large language model.

In contrast, to structured data, generative AI tends to work best with unstructured data.

AI

Structured data refers to tabular data of the sort you would store in a spreadsheet, whereas unstructured data
refers to text, images, audio, video.

And generative AI does apply to all of these types of data, although the impact is the largest and that's why we'll
focus mostly on text data in this course.

AI

Finally, large language models can bias output and can sometimes output toxic or other harmful speech.

For example, large language models were trained on text off the Internet.

And unfortunately, text on the Internet can reflect biases that exist in society.

So if you were to ask an LLM to complete the sentence, "The surgeon walked to the parking lot and took out,"
the LLM might output "his car keys," but if you say "the nurse walked to the parking lot and took out," it may say
"her phone."

「

LLM

」

「
「

」

」LLM

「

」

So in this case, the LLM has assumed that the surgeon is male, and the nurse is female, whereas we know that
clearly surgeons and nurses can be any gender.

LLM

And so if you're using an LLM in an application where such biases could cause harm, I would use care in how
we prompt and apply the LLM to make sure we don't contribute to such undesirable biases.

LLM

LLM

Finally, some LLMs can also occasionally output toxic or other harmful speech.

LLM

For example, some LLMs will sometimes teach people how to do undesirable, sometimes even illegal acts.

LLMs

Fortunately, all the major large language providers have been working hard on the safety of these models, and
so most models have gotten much safer over time.

And if you use the web interfaces of the major LLM providers, it's actually been getting much harder over time to
get them to output these types of harmful speech.

LLM

So that summarizes what prompting an LLM can and cannot do.

LLM

And as I mentioned, next week we'll take a look at some techniques for overcoming some of these limitations to
make what LLMs can do even broader and more powerful.

But first, let's take a look at some tips on prompting LLMs.

LLM

LLM

And I hope that the tips I share in the next video will be useful right away to how you use LLMs, I'll see you in the
next video.

LLM

09 Tips for prompting

I'd like to share with you some tips for prompting large language models.

If you're using the web user interface of an LLM provider, hopefully, these tips will be useful to you right away.

LLM

Web

And it turns out that similar tips are also useful for if you're ever involved in building a software application that
uses LLMs, let's dive in.

LLM

In this video, we'll go through three main tips for prompting.

First is be detailed and specific.

Second is guide the model to think through its answer.

And third is experiment and iterate.

This starts with being detailed and specific.

Using the Fresh College Grad analogy, I would often think about how to make sure the model has sufficient
context or sufficient background information to complete the task.

So for example, if you were to ask it to help me write an email asking to be assigned to the Legal Documents
project.

Well, given only a prompt like this, a model doesn't really know how to write a compelling case to advocate for
you to be assigned to that project.

But if you give additional context such as "I've applied for a job in the Legal Documents project. We check legal
documents. I have prior experience prompting LLMs to get accurate text or professional tone."

LLMs

「

」

Then this gives the LLM more relevant context to write that email to help you ask to be assigned to the project.

LLM

Further, if you can also describe the desired task in detail.

So if you tell it instead of saying "help me write an email," if you ask it to "write a paragraph of text explaining
why my background makes me a strong candidate for this project,"

「

」

「

」

Then this type of prompt would not only give the LLMs sufficient context but also tell it quite clearly what you
want it to do, and this is more likely to get you the result that you want.

LLMs

Second tip is to guide the model to think through its answer.

So if you were to tell it to brainstorm five names for a new cat toy, it actually could do pretty well.

But if, say, you have in mind that you want a rhyming cat toy name with a relevant emoji, this is what I might try.

I might tell it to brainstorm five names and tell it step one, come up with five joyful words related to cats.

Then for each word, come up with a rhyming name.

And finally, for each toy name, add a fun relevant emoji.

And with a prompt like this, you might get a result like this where the LLM follows your instructions to first come
up with 'purr', 'whisker' and so on.

LLM

'purr'

'whisker'

And then 'purr-twirl', 'whisker-whisper', 'feline-beeline' with fun emojis added to the end.

'purr-twirl'

'whisker-whisper'

'feline-beeline'

So if you already have in mind a process by which you think the model could get to the answer that you want,
giving it clear step-by-step instructions to follow could be quite effective.

Finally, there have been a bunch of articles that I've seen on social media that say things like "20 prompts that
everyone must know" or "17 prompts that will help you grow your career."

」

I don't think there's a perfect prompt for everyone.

「

20

」

「17

Instead, I find it more useful to have a process by which you can write the prompt that will generate the result for
you.

So when I'm prompting an LLM myself, I will often experiment and iterate and try something like my first draft,
say, "help me rewrite this."

LLM

「

」

And if I don't like the result I might clarify and say, "correct any grammatical and spelling errors in this."

「

」

And if it still doesn't give me exactly the result I want, I might clarify even further to say, "correct any grammatical
and spelling errors and rewrite in the tone appropriate for a professional resume."

」

「

So very frequently the process of prompting is not about starting off with the right prompt.

It's about starting off with something and then seeing if the results are satisfactory and knowing how to adjust the
prompt to get it closer to the answer that you want.

I think of the process of prompting as like this: you start off with an idea of what you want the LLM to do and you
just express that in a prompt.

And then based on the prompt, the LLM will give a response and it may or may not be what you want.

LLM

LLM

If it is, then great, you're done.

But if it isn't satisfactory, then that initial response helps you shape your idea and modify the prompt and iterate
maybe a few times before you get to the result that you want.

So I think of the prompting process as when I start off, I try to be reasonably clear and specific.

But to save time, I'll often start off with a short prompt that maybe is frankly less specific than it's desired, but I
just want to get going quickly.

After you get a result back, if it's not what you want, then think about why the result isn't the desired output.

And based on that, refine your prompt to clarify your instructions and keep on repeating until hopefully you get
the LLM response that you want.

One tip I want to share is I've seen some people overthink the initial prompt.

LLM

I think it's better to usually just try something quickly and if it doesn't give you the results you want, it's fine, go
ahead and improve it over time.

You will not break the Internet by just accidentally having a slightly incorrectly worded prompt.

So go ahead and try what you want.

Two important caveats: first, if you are in possession of highly confidential information.

I would make sure I understand how a large language model provider does or does not use or keep that
information confidential before copy-pasting highly confidential information into the web user interface of an LLM.

LLM

And second, as we saw in the last video with the lawyer, they got into trouble for submitting court filings with
facts made up by an LLM.

LLM

Before you counter the LLM's result, it may be worth double-checking and deciding for yourself whether or not
you can trust and act on the LLM's output.

LLM

LLM

But with these two caveats when prompting, I will often just jump in and try something and see it not work, but
then use the initial result to decide how to refine the prompt to get a better result.

And that's why we say prompting is a highly iterative process.

Sometimes you have to try a few things before you get the result you want.

So that's it for tips on prompting.

I hope that you go to some of the web user interfaces of the large language model providers and try out some of
these ideas yourself.

And in this course, we provide some links to some of the popular LLM providers and hope you go play with them
and have fun with them.

That brings us to the end of the main set of videos for this week.

LLM

There's one optional video to follow where I'll talk a little bit about image generation or diffusion models.

So take a look at that if you want, and then I look forward to seeing you back next week where we'll talk more
about how to build projects using large language models.

Look forward to diving into that with you next week.

10 Image generation

Thanks for sticking with me for this final optional video on image generation.

So far this week we'll focus most of attention on text generation.

Text generation is what a lot of users are using and is having the biggest impact of all the different tools of
generative AI.

But part of the excitement of generative AI is also image generation.

AI

AI

They're also starting to be some models that can generate either text or images, and these are sometimes called
multimodal models, because it can operate in multiple modalities, text, or images.

What I'd like to do in this video is share with you how image generation works.

Let's take a look.

With just a prompt, you can use generative AI to generate a beautiful picture of a person that had never existed,
or a picture of a futuristic scene, or a picture of a cool robot like this.

AI

How does this technology work?

Image generation today is mostly done via a method called a diffusion model.

Diffusion models have learned from huge numbers of images found on the Internet or elsewhere.

It turns out that at the heart of a diffusion model is supervised learning.

Here's what it does.

Let's say the algorithm finds a picture on the Internet of an apple like this, and it wants to learn from pictures like
this and hundreds of millions of others how to generate images.

The first step is to take this image, and gradually add more and more noise to it.

You go from this nice picture of an apple, to a noisier, to an even noisier, to finally a picture that looks like pure
noise.

Where all the pixels are chosen at random and it doesn't look at all like an apple.

The diffusion model then uses pictures like these as data to learn using supervised learning, to take as input, a
noisy image and output a slightly less noisy image.

Specifically, it would create a dataset where, the first data point says if it's given the second input image, what
we want the supervised learning algorithm to do is learn to output a cleaner version of this apple.

Here's another data point, given this third image of an even noisier image, we would like the algorithm to learn to
output a slightly less noisy version like this.

Finally, given an image of pure noise like this fourth image, we would like it to learn to output a slightly less noisy
picture here that suggests the presence of an apple.

After training on maybe hundreds of millions of images, viral process like this, when you want to apply it to
generate a new image, this is how you would run it.

You will start off with a pure noise image.

Start by taking a picture where, every single pixel in the picture is chosen completely at random.

We then feed this picture to the supervised learning algorithm that we trained up on the previous line.

When we feed in pure noise, it learns to remove a little bit of noise from this picture, and you may end up with a
picture like this that suggests some sort of fruit in the middle, but we're not quite sure what it is yet.

Given the second picture, we again feed it to the model, and it then takes away even a little bit more noise, and
now it looks like we can see a noisy picture of a watermelon.

Then if you apply this one more time, we end up with this fourth image, which looks like a pretty nice picture of a
watermelon.

I'm illustrating this process using four steps of adding noise on the previous slide, and four steps of removing
noise on this slide.

But in practice, maybe about 100 steps will be more typical for a diffusion model.

100

This algorithm will work for generating pictures completely at random.

But we want to be able to control the image it generates by specifying a prompt to tell it what we want it to
generate.

Let me describe a modification of the algorithm that lets you add text, or add a prompt to tell it what you want it to
generate.

In this training data, we're given pictures like this apple, as well as a description or a prompt that could have
generated this apple.

Here, I have a text description saying this is a red apple.

Then we will same as before, add noise to this picture until we get the fourth image, which is pure noise.

But we're going to change how we build the learning algorithm, which is, rather than inputting the slightly noisy
picture and expecting it to generate a clean picture, we'll instead have the input A, to the supervised learning
algorithm B, this noisy picture, as well as the text caption or the prompt that could have generated this picture,
namely red apple.

A

B

Given this input, we want the algorithm to output this clean picture of an apple.

Similarly, we'll generate additional data points for the algorithm using the other noisy images.

Where each time, given a noisy image, and the text prompt red apple, we want the algorithm to learn to generate
a less noisy picture of a red apple.

Having learned from a large dataset, when you want to apply this algorithm to generating, say, a green banana,
this is what you do.

Same as before, we start off with an image of pure noise.

Every single pixel is chosen completely at random.

If you wanted to generate a green banana, you input to the supervised learning algorithm, that picture of pure
noise together with the prompt, "green banana".

「

」

Now that it knows you want a green banana, hopefully the ovum will output a picture that maybe looks like this.

Can't see the banana clearly, but maybe there's a suggestion of some greenish fruit in the middle, and this is the
first step of image generation.

The next step is, we then take this image on the right, there was an output B, and feed that is the input A, with
again, the prompt "Green banana" to get it to generate a slightly less noisy picture, and now we see clearly,
looks like there's a green banana, but a pretty noisy one.

B

A

We do this one more time and it finally removes most of the noise, until we end up with that picture of a pretty
nice green banana.

That's how diffusion models work for generating images.

At the heart of this magical process of generating beautiful images is, again, supervised learning.

Thanks for sticking with me for this optional video, and I look forward to seeing you next week where, we'll dive
much more into applications being built using generative AI.

AI

I'll see you in the next video.