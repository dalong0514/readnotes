Leopold Aschenbrenner.(2024).2024109Situational-Awareness-The-Decade-Ahead.Dwarkesh podcast => I. From GPT-4 to AGI: Counting the OOMs

IIIc. Superalignment

Reliably controlling AI systems much smarter than we are is an unsolved technical problem. And while it is a solvable problem, things could very easily go off the rails during a rapid intelligence explosion. Managing this will be extremely tense; failure could easily be catastrophic.

In this piece:

The problem

The superalignment problem

What failure looks like

The intelligence explosion makes this all incredibly tense

The default plan: how we can muddle through

Aligning somewhat-superhuman models

Automating alignment research

Superdefense

Why I'm optimistic, and why I'm scared

The old sorcerer

Has finally gone away!

Now the spirits he controls

Shall obey my commands.

…

I shall work wonders too.

…

Sir, I'm in desperate straits!

The spirits I summoned –

I can't get rid of them.

Johann Wolfgang von Goethe, "The Sorcerer's Apprentice"

By this point, you have probably heard of the AI doomers. You might have been intrigued by their arguments, or you might have dismissed them off-hand. You're loath to read yet another doom-and-gloom meditation.

I am not a doomer. Misaligned superintelligence is probably not the biggest AI risk. But I did spend the past year working on technical research on aligning AI systems as my day-job at OpenAI, working with Ilya and the Superalignment team. There is a very real technical problem: our current alignment techniques (methods to ensure we can reliably control, steer, and trust AI systems) won't scale to superhuman AI systems. What I want to do is explain what I see as the "default" plan for how we'll muddle through, and why I'm optimistic. While not enough people are on the ball—we should have much more ambitious efforts to solve this problem!—overall, we've gotten lucky with how deep learning has shaken out, there's a lot of empirical low-hanging fruit that will get us part of the way, and we'll have the advantage of millions of automated AI researchers to get us the rest of the way.

But I also want to tell you why I'm worried. Most of all, ensuring alignment doesn't go awry will require extreme competence in managing the intelligence explosion. If we do rapidly transition from AGI to superintelligence, we will face a situation where, in less than a year, we will go from recognizable human-level systems for which descendants of current alignment techniques will mostly work fine, to much more alien, vastly superhuman systems that pose a qualitatively different, fundamentally novel technical alignment problem; at the same time, going from systems where failure is low-stakes to extremely powerful systems where failure could be catastrophic; all while most of the world is probably going kind of crazy. It makes me pretty nervous.

By the time the decade is out, we'll have billions of vastly superhuman AI agents running around. These superhuman AI agents will be capable of extremely complex and creative behavior; we will have no hope of following along. We'll be like first graders trying to supervise people with multiple doctorates.

In essence, we face a problem of handing off trust. By the end of the intelligence explosion, we won't have any hope of understanding what our billion superintelligences are doing (except as they might choose to explain to us, like they might to a child). And we don't yet have the technical ability to reliably guarantee even basic side constraints for these systems, like "don't lie" or "follow the law" or "don't try to exfiltrate your server". Reinforcement from human feedback (RLHF) works very well for adding such side constraints for current systems—but RLHF relies on humans being able to understand and supervise AI behavior, which fundamentally won't scale to superhuman systems.

Simply put, without a very concerted effort, we won't be able to guarantee that superintelligence won't go rogue (and this is acknowledged by many leaders in the field). Yes, it may all be fine by default. But we simply don't know yet. Especially once future AI systems aren't just trained with imitation learning, but large-scale, long-horizon RL (reinforcement learning), they will acquire unpredictable behaviors of their own, shaped by a trial-and-error process (for example, they may learn to lie or seek power, simply because these are successful strategies in the real world!).

The stakes will be high enough that hoping for the best simply isn't a good enough answer on alignment.

The problem

The superalignment problem

We've been able to develop a very successful method for aligning (i.e., steering/controlling) current AI systems (AI systems dumber than us!): Reinforcement Learning from Human Feedback (RLHF). The idea behind RLHF is simple: the AI system tries stuff, humans rate whether its behavior was good or bad, and then reinforce good behaviors and penalize bad behaviors. That way, it learns to follow human preferences.

Indeed, RLHF has been the key behind the success of ChatGPT and others. Base models had lots of raw smarts but weren't applying these in a useful way by default; they usually just responded with a garbled mess resembling random internet text. Via RLHF, we can steer their behavior, instilling important basics like instruction-following and helpfulness. RLHF also allows us to bake in safety guardrails: for example, if a user asks me for bioweapon instructions, the model should probably refuse.

The core technical problem of superalignment is simple: how do we control AI systems (much) smarter than us?

RLHF will predictably break down as AI systems get smarter, and we will face fundamentally new and qualitatively different technical challenges. Imagine, for example, a superhuman AI system generating a million lines of code in a new programming language it invented. If you asked a human rater in an RLHF procedure, "does this code contain any security backdoors?" they simply wouldn't know. They wouldn't be able to rate the output as good or bad, safe or unsafe, and so we wouldn't be able to reinforce good behaviors and penalize bad behaviors with RLHF.

Aligning AI systems via human supervision (as in RLHF) won't scale to superintelligence. Based on illustration from "Weak-to-strong generalization".

Even now, AI labs already need to pay expert software engineers to give RLHF ratings for ChatGPT code—the code current models can generate is already pretty advanced! Human labeler-pay has gone from a few dollars for MTurk labelers to ~$100/hour for GPQA questions in the last few years. In the (near) future, even the best human experts spending lots of time won't be good enough. We're starting to hit early versions of the superalignment problem in the real world now, and very soon this will be a major issue even just for practically deploying next-generation systems. It's clear we will need a successor to RLHF that scales to AI capabilities better than human-level, where human supervision breaks down. In some sense, the goal of superalignment research efforts is to repeat the success story of RLHF: make the basic research bets that will be necessary to steer and deploy AI systems a couple years down the line.

What failure looks like

People too often just picture a "GPT-6 chatbot," informing their intuitions that surely these wouldn't be dangerously misaligned. As discussed previously in this series, the "unhobbling" trajectory points to agents, trained with RL, in the near future. I think Roger's graphic gets it right:

Roger Grosse (Professor at the University of Toronto)

One way to think of what we're trying to accomplish with alignment, from the safety perspective, is add side-constraints. Consider a future powerful "base model" that, in a second stage of training, we train with long-horizon RL to run a business and make money (as a simplified example):

By default, it may well learn to lie, to commit fraud, to deceive, to hack, to seek power, and so on—simply because these can be successful strategies to make money in the real world!

What we want is to add side-constraints: don't lie, don't break the law, etc.

But here we come back to the fundamental issue of aligning superhuman systems: we won't be able to understand what they are doing, and so we won't be able to notice and penalize bad behavior with RLHF.

If we can't add these side-constraints, it's not clear what will happen. Maybe we'll get lucky and things will be benign by default (for example, maybe we can get pretty far without the AI systems having long-horizon goals, or the undesirable behaviors will be minor). But it's also totally plausible they'll learn much more serious undesirable behaviors: they'll learn to lie, they'll learn to seek power, they'll learn to behave nicely when humans are looking and pursue more nefarious strategies when we aren't watching, and so on.

The superalignment problem being unsolved means that we simply won't have the ability to ensure even these basic side constraints for these superintelligence systems, like "will they reliably follow my instructions?" or "will they honestly answer my questions?" or "will they not deceive humans?". People often associate alignment with some complicated questions about human values, or jump to political controversies, but deciding on what behaviors and values to instill in the model, while important, is a separate problem. The primary problem is that for whatever you want to instill the model (including ensuring very basic things, like "follow the law"!) we don't yet know how to do that for the very powerful AI systems we are building very soon.

Again, the consequences of this aren't totally clear. What is clear is that superintelligence will have vast capabilities—and so misbehavior could fairly easily be catastrophic. What's more, I expect that within a small number of years, these AI systems will be integrated in many critical systems, including military systems (failure to do so would mean complete dominance by adversaries). It sounds crazy, but remember when everyone was saying we wouldn't connect AI to the internet? The same will go for things like "we'll make sure a human is always in the loop!"—as people say today.

Alignment failures then might look like isolated incidents, say, an autonomous agent committing fraud, a model instance self-exfiltrating, an automated researcher falsifying an experimental result, or a drone swarm overstepping rules of engagement. But failures could also be much larger scale or more systematic—in the extreme, failures could look more like a robot rebellion. We'll have summoned a fairly alien intelligence, one much smarter than us, one whose architecture and training process wasn't even designed by us but some super-smart previous generation of AI systems, one where we can't even begin to understand what they're doing, it'll be running our military, and its goals will have been learned by a natural-selection-esque process.

Unless we solve alignment—unless we figure out how to instill those side-constraints—there's no particular reason to expect this small civilization of superintelligences will continue obeying human commands in the long run. It seems totally within the realm of possibilities that at some point they'll simply conspire to cut out the humans, whether suddenly or gradually.

The intelligence explosion makes this all incredibly tense

I am optimistic that superalignment is a solvable technical problem. Just like we developed RLHF, so we can develop the successor to RLHF for superhuman systems and do the science that gives us high confidence in our methods. If things continue to progress iteratively, if we insist on rigorous safety testing and so on, it should all be doable (and I'll discuss my current best-guess of how we'll muddle through more in a bit).

What makes this incredibly hair-raising is the possibility of an intelligence explosion: that we might make the transition from roughly human-level systems to vastly superhuman systems extremely rapidly, perhaps in less than a year:

The intelligence explosion makes superalignment incredibly hair-raising.

We will extremely rapidly go from systems where RLHF works fine—to systems where it will totally break down. This leaves us extremely little time to iteratively discover and address ways in which our current methods will fail.

At the same time, we will extremely rapidly go from systems where failures are fairly low-stakes (ChatGPT said a bad word, so what)—to extremely high-stakes (oops, the superintelligence self-exfiltrated from our cluster, now it's hacking the military). Rather than iteratively encountering increasingly more dangerous safety failures in the wild, the first notable safety failures we encounter might already be catastrophic.

The superintelligence we get by the end of it will be vastly superhuman. We'll be entirely reliant on trusting these systems, and trusting what they're telling us is going on—since we'll have no ability of our own to pierce through what exactly they're doing anymore.

The superintelligence we get by the end of it could be quite alien. We'll have gone through a decade or more of ML advances during the intelligence explosion, meaning the architectures and training algorithms will be totally different (with potentially much riskier safety properties).

One example that's very salient to me: we may well bootstrap our way to human-level or somewhat-superhuman AGI with systems that reason via chains of thoughts, i.e. via English tokens. This is extraordinarily helpful, because it means the models "think out loud" letting us catch malign behavior (e.g., if it's scheming against us). But surely having AI systems think in tokens is not the most efficient means to do it, surely there's something much better that does all of this thinking via internal states—and so the model by the end of the intelligence explosion will almost certainly not think out loud, i.e. will have completely uninterpretable reasoning.

This will be an incredibly volatile period, potentially with the backdrop of an international arms race, tons of pressure to go faster, wild new capabilities advances every week with basically no human-time to make good decisions, and so on. We'll face tons of ambiguous data and high-stakes decisions.

Think: "We caught the AI system doing some naughty things in a test, but we adjusted our procedure a little bit to hammer that out. Our automated AI researchers tell us the alignment metrics look good, but we don't really understand what's going on and don't fully trust them, and we don't have any strong scientific understanding that makes us confident this will continue to hold for another couple OOMs. So, we'll probably be fine? Also China just stole our weights and they're launching their own intelligence explosion, they're right on our heels."

It just really seems like this could go off the rails. To be honest, it sounds terrifying.

Yes, we will have AI systems to help us. Just like they'll automate capabilities research, we can use them to automate alignment research. That will be key, as I discuss below. But—can you trust the AI systems? You weren't sure whether they were aligned in the first place—are they actually being honest with you about their claims about alignment science? Will automated alignment research be able to keep up with automated capabilities research (for example, because automating alignment is harder, e.g. because there are less clear metrics we can trust compared to improving model capabilities, or there's a lot of pressure to go full-speed on capabilities progress because of the international race)? And AI won't be able to fully substitute for the still-human decision makers making good calls in this incredibly high-stakes situation.

The default plan: how we can muddle through

Ultimately, we are going to need to solve alignment for vastly superhuman, fairly alien superintelligence. Maybe, somewhere, there is a once-and-for-all, simple solution to aligning superintelligence. But my strong best guess is that we'll get there by muddling through.

I think we can harvest wins across a number of empirical bets, which I'll describe below, to align somewhat-superhuman systems. Then, if we're confident we can trust these systems, we'll need to use these somewhat-superhuman systems to automate alignment research—alongside the automation of AI research in general, during the intelligence explosion—to figure out how to solve alignment to go the rest of the way, all the way to vastly superhuman, fairly alien superintelligence.

Aligning somewhat-superhuman models

Aligning human-level systems won't be enough. Even the first systems that can do automated AI research, i.e. start the intelligence explosion, will likely already be substantially superhuman in many domains. This is because AI capabilities are likely to be somewhat spikey—by the time AGI is human-level at whatever a human AI researcher/engineer is worst at, it'll be superhuman at many other things. For example, perhaps the ability for AI systems to effectively coordinate and plan lags behind, meaning that by the time the intelligence explosion is in full force they'll probably already be superhuman coders, submitting million-line pull requests in new programming languages they devised, and they'll be superhuman at math and ML.

These early-intelligence-explosion-systems will start being quantitatively and qualitatively superhuman, at least in many domains. But they'll look much closer to the systems we have today in terms of architecture, and the intelligence gap we need to cover is much more manageable. (Perhaps if humans trying to align true superintelligence is like a first grader trying to supervise a PhD graduate, this is more like a smart high schooler trying to supervise a PhD graduate.)

More generally, the more we can develop good science now, the more we'll be in a position to verify that things aren't going off the rails during the intelligence explosion. Even having good metrics we can trust for superalignment is surprisingly difficult—but without reliable metrics during the intelligence explosion, we won't know whether pressing on is safe or not.

Here are some of the main research bets I see for crossing the gap between human-level and somewhat-superhuman systems:

Evaluation is easier than generation. We get some of the way "for free," because it's easier for us to evaluate outputs (especially for egregious misbehaviors) than it is to generate them ourselves. For example, it takes me months or years of hard work to write a paper, but only a couple hours to tell if a paper someone has written is any good (though perhaps longer to catch fraud). We'll have teams of expert humans spend a lot of time evaluating every RLHF example, and they'll be able to "thumbs down" a lot of misbehavior even if the AI system is somewhat smarter than them. That said, this will only take us so far (GPT-2 or even GPT-3 couldn't detect nefarious GPT-4 reliably, even though evaluation is easier than generation!)

Scalable oversight. We can use AI assistants to help humans supervise other AI systems—the human-AI team being able to extend supervision farther than the human could alone. For example, imagine an AI system generates 1M lines of complex code. It's easier for a human to double-check that a given line of code has a bug if an AI assistant has pointed out that (say) line 394,894 looks fishy, than it is for a human to find that same bug from scratch. A model trained to critique the code written by another model could thus help humans supervise a system with narrowly superhuman coding abilities.

Several scalable oversight strategies have been proposed, including debate, market-making, recursive reward modeling, and prover-verifier games, as well as simplified versions of those ideas like critiques. Models are now strong enough that it's possible to empirically test these ideas, making direct progress on scalable oversight.

I expect this to help a lot for the "quantitatively" superhuman part of the problem, such as the aforementioned million-lines of code example. But I am less optimistic that scalable oversight techniques can really help for the "qualitatively" superhuman part of the problem—imagine the model invents quantum physics when you only understand Newtonian physics.

Generalization. Even with scalable oversight, we won't be able to supervise AI systems on really hard problems, problems beyond human comprehension. However, we can study: how will the AI systems generalize from human supervision on easy problems (that we do understand and can supervise) to behave on the hard problems (that we can't understand and can no longer supervise)? For example, perhaps supervising a model to be honest in simple cases generalizes benignly to the model just being honest in general, even in cases where it's doing extremely complicated things we don't understand.

There's a lot of reasons to be optimistic here: part of the magic of deep learning is that it often generalizes in benign ways (for example, RLHF'ing with only labels on English examples also tends to produce good behavior when it's speaking French or Spanish, even if that wasn't part of the training). I'm fairly optimistic that there will both be pretty simple methods that help nudge the models' generalization in our favor, and that we can develop a strong scientific understanding that helps us predict when generalization will work and when it will fail. To a greater extent that for scalable oversight, the hope is that this will help with alignment even in the "qualitatively" superhuman case.

Here's another way of thinking about this: if a superhuman model is misbehaving, say breaking the law, intuitively the model should already know that it's breaking the law. Moreover, "is this breaking the law" is probably a pretty natural concept to the model—and it will be salient in the model's representation space. The question then is: can we "summon" this concept from the model with only weak supervision?

I'm particularly partial to this direction (and perhaps biased), because I helped introduce this with some recent work with some colleagues at OpenAI. In particular, we studied an analogy to the problem of humans supervising superhuman systems—can a small model align a larger (smarter) model? We found that generalization does actually get you cross some (but certainly not all) of the intelligence gap between supervisor and supervisee, and that in simple settings there's a lot you can do to improve it.

A simple analogy for studying superalignment: instead of a human supervising a superhuman model, we can study a small model supervising a large model. For example, can we align GPT-4 with only GPT-2 supervision? Will that result in GPT-4 appropriately generalization "what GPT-2 meant"? From Weak-to-strong generalization.

Interpretability. One intuitively-attractive way we'd hope to verify and trust that our AI systems are aligned is if we could understand what they're thinking! For example, if we're worried that AI systems are deceiving us or conspiring against us, access to their internal reasoning should help us detect that.

By default, modern AI systems are inscrutable black boxes. Yet it seems like we should be able to do amazing "digital neuroscience"—after all, we have perfect access to model internals.

There's a few different approaches here, going from "most ambitious and ‘cool' but will be very hard" to "hackier things that are easier and might just work":

Mechanistic interpretability. Try to fully reverse-engineer large neural networks from the ground up—fully disentangle the inscrutable matrices, so to speak.

Chris Olah's team at Anthropic has done much of the pioneering work on this, starting by understanding simple mechanisms in very small models. There's incredibly exciting progress happening recently, and I'm thrilled about the overall level of activity in this space.

That said, I'm worried fully reverse-engineering superhuman AI systems will just be an intractable problem—similar, to, say "fully reverse engineering the human brain"—and I'd put this work mostly in the "ambitious moonshot for AI safety" rather than "default plan for muddling through" bucket.

(Neel Nanda's 200 open problems in mechanistic interpretability also gives a flavor of this kind of research.)

"Top-down" interpretability. If mechanistic interpretability tries to reverse engineer neural networks "from the bottom up," other work takes a more targeted, "top-down" approach, trying to locate information in a model without full understanding of how it is processed.

For example, we might try to build an "AI lie detector" by identifying the parts of the neural net that "light up" when an AI system is lying. This can be a lot more tractable (even if it gives less strong guarantees).

Over the past couple of years, there's been a flurry of exciting work in this area. CCS is able to identify a "truth direction" in models with only unsupervised data. ROME is able to identify the part of the model that knows the Eiffel Tower is in Paris—and then directly edit the model's knowledge to place the Eiffel Tower in Rome. Representation Engineering and Inference-time Interventions demonstrate using top-down techniques to detect lying and hallucinations and surgically control model behavior on jailbreaking, power-seeking, fairness, truthfulness, and more. There's other creative work on lie detection that doesn't even require model internals.

I'm increasingly bullish that top-down interpretability techniques will be a powerful tool—i.e., we'll be able to build something like an "AI lie detector"—and without requiring fundamental breakthroughs in understanding neural nets.

Chain-of-thought interpretability. As mentioned earlier, I think it's quite plausible that we'll bootstrap our way to AGI with systems that "think out loud" via chains of thought. Even if it's not the most efficient algorithm in the limit (I'd be very surprised if superintelligence still used English-chain-of-thought, rather than thinking via some sort of recurrent internal states), we may well still benefit from this property for the first AGIs. This would be an incredible boon for interpretability: we'd have access to the AGI's "internal monologue"! That would make it relatively easy to detect egregious alignment failures.

There's a ton of work to do here, however, if we wanted to rely on this. How do we ensure that the CoT remains legible? (It may simply drift from understandable English to unintelligible model-speak, depending on how we e.g. use RL to train models—can we add some simple constraints to ensure it remains legible?) How do we ensure the CoT is faithful, i.e. actually reflects what models are thinking? (E.g, there's some work that shows in certain situations, models will just make up posthoc reasoning in their CoT that don't actually reflect their actual internal reasoning for an answer.)

My best guess is that some simple measurement of legibility and faithfulness, and some simple hacks to preserve legibility and faithfulness longer, could go quite far. Yes, this won't work in some worlds, and it's a bit of a simple hack, but it's such low-hanging fruit; this direction is criminally underrated in my view.

Adversarial testing and measurements. Along the way, it's going to be critical to stress test the alignment of our systems at every step—our goal should be to encounter every failure mode in the lab before we encounter it in the wild. This will require substantially advancing techniques for automated red-teaming. For example, if we deliberately plant backdoors or misalignments into models, would our safety training would have caught and gotten rid of them? (Early work suggests that "sleeper agents" can survive through safety training, for example.)

More generally, it'll be critical to have good measurements of alignment along the way. Does the model have the power to be misaligned? For example, does it have long-horizon goals, and what sorts of drives it is learning? And what are clear "red lines"? For example, a very intuitive bound might be "model reasoning (chain of thoughts) always has to remain legible and faithful." (As Eric Schmidt says, the point at which AI agents can talk to each other in a language we can't understand, we should unplug the computers.) Another might be developing better measurements for whether models are being fully honest.

The science of measuring alignment is still in its infancy; improving this will be critical for helping us make the right tradeoffs on risk during the intelligence explosion. Doing the science that lets us measure alignment and gives us an understanding of "what evidence would be sufficient to assure us that the next OOM into superhuman territory is safe?" is among the very-highest priority work for alignment research today (beyond just work that tries to extend RLHF further to "somewhat-superhuman" systems).

See also this writeup of superalignment research directions for the Superalignment Fast Grants call-for-proposals.

Automating alignment research

Ultimately, we're going to need to automate alignment research. There's no way we'll manage to solve alignment for true superintelligence directly; covering that vast of an intelligence gap seems extremely challenging. Moreover, by the end of the intelligence explosion—after 100 million automated AI researchers have furiously powered through a decade of ML progress—I expect much more alien systems in terms of architecture and algorithms compared to current system (with potentially less benign properties, e.g. on legibility of CoT, generalization properties, or the severity of misalignment induced by training).

But we also don't have to solve this problem just on our own. If we manage to align somewhat-superhuman systems enough to trust them, we'll be in an incredible position: we'll have millions of automated AI researchers, smarter than the best AI researchers, at our disposal. Leveraging these army of automated researchers properly to solve alignment for even-more superhuman systems will be decisive.

(This applies more generally, by the way, for the full spectrum of AI risks, including misuse and so on. The best route—perhaps the only route—to AI safety in all of these cases, will involve properly leveraging early AGIs for safety; for example, we should put a bunch of them to work on automated research to improve security against foreign actors exfiltrating weights, others on shoring up defenses against worst-case bioattacks, and so on.)

Getting automated alignment right during the intelligence explosion will be extraordinarily high-stakes: we'll be going through many years of AI advances in mere months, with little human-time to make the right decisions, and we'll start entering territory where alignment failures could be catastrophic. Labs should be willing to commit a large fraction of their compute to automated alignment research (vs. automated capabilities research) during the intelligence explosion, if necessary. We'll need strong guarantees that let us trust the automated alignment research being produced and much better measurements than we have today for misalignment to know whether we're still in the clear. For every OOM we want to ascend, we will need to have extremely high confidence in our alignment approaches for that next OOM.

Most of all, getting this right will require an extreme degree of competence, seriousness, and willingness to make hard tradeoffs. Once we're approaching true superintelligence, the stakes get very real, and failure—rogue AI—could be catastrophic. There will be moments with ambiguous evidence, when metrics will superficially look ok, but there are some warning signs that hint at looming danger, and we mostly don't have a clue what's going on anymore. Navigating this situation responsibly will require making very costly tradeoffs. Eventually, the decision to greenlight the next generation of superintelligence will need to be taken as seriously as the decision to launch a military operation.

Superdefense

"Getting alignment right" should only be the first of many layers of defense during the intelligence explosion. Alignment will be hard; there will be failures along the way. If at all possible, we need to be in a position where alignment can fail—but failure wouldn't be catastrophic. This could mean:

Security. An airgapped cluster is the first layer of defense against superintelligence attempting to self-exfiltrate and doing damage in the real world. And that's only the beginning; we'll need much more extreme security against model self-exfiltration across the board, from hardware encryption to many-key signoff. And once our AGIs can do automated R&D, we should put them to work on further hardening security as well.

Monitoring. If our AI systems are up to something fishy or malevolent—or a rogue employee tries to use them for unauthorized activities—we need to be able to catch it. However, this is not a trivial task: we will have millions of AGI instances running our cluster, executing complex code and so on. We will need advanced monitoring systems that leverage the models themselves, including monitoring model outputs, chains of thought, model-written code, server/network activity, and interactions with researchers/other humans; essentially, leveraging some AI systems to nark on other AI systems. Moreover, we'll want to develop and employ sophisticated "control" protocols, using less powerful but trusted models to protect against subversion from more powerful but less trusted models. This may require, for example, dedicating the same amount of compute to monitoring model instances as to compute for active model instances.

Targeted capability limitations. As much as possible, we should try to limit the model's capabilities in targeted ways that reduce fallout from failure. A central example of this might be scrubbing everything related to biology and chemistry from model training (or using "unlearning" techniques); this helps cut off paths to catastrophic real world damage that occur via biological and chemical weapons

Targeted training method restrictions. There are likely some ways of training models that are inherently riskier—more likely to produce severe misalignments—than others. For example, imitation learning seems relatively safe (hard to see how that would lead to models that have dangerous long-term internal goals), while we should avoid long-horizon outcome-based RL (which seems much more likely to lead to the model learning undesirable long-term goals) as long as possible. We should also avoid training against our interpretability methods and our monitoring setup (such that our models aren't simply trained to work around these). There might be additional desirable limitations, for example, maintaining legible and faithful chains of thought as long as possible. We should define these constraints ahead of time, maintain them as long as we can throughout the intelligence explosion, and only drop them if absolutely necessary.

There's likely a lot more possible here.

Will these be foolproof? Not at all. True superintelligence is likely able to get around most-any security scheme for example. Still, they buy us a lot more margin for error—and we're going to need any margin we can get. We'll want to use that margin to get in a position where we have very high confidence in our alignment techniques, only relaxing "superdefense" measures (for example, deploying the superintelligence in non-airgapped environments) concomitant with our confidence.

Things will get dicey again once we move to deploying these AI systems in less-controlled settings, for example in military applications. It's likely circumstances will force us to do this fairly quickly, but we should always try to buy as much margin for error as much as possible—for example, rather than just directly deploying the superintelligences "in the field" for military purposes, using them to do R&D in a more isolated environment, and only deploying the specific technologies they invent (e.g., more limited autonomous weapons systems that we're more confident we can trust).

Why I'm optimistic, and why I'm scared

I'm incredibly bullish on the technical tractability of the superalignment problem. It feels like there's tons of low-hanging fruit everywhere in the field. More broadly, the empirical realities of deep learning have shaken out more in our favor compared to what some speculated 10 years ago. For example, deep learning generalizes surprisingly benignly in many situations: it often just "does the thing we meant" rather than picking up some abstruse malign behavior. Moreover, while fully understanding model internals will be hard, at least for the initial AGIs we have a decent shot of interpretability—we can get them to reason transparently via chains of thought, and hacky techniques like representation engineering work surprisingly well as "lie detectors" or similar.

I think there's a pretty reasonable shot that "the default plan" to align "somewhat-superhuman" systems will mostly work. Of course, it's one thing to speak about a "default plan" in the abstract—it's another if the team responsible for executing that plan is you and your 20 colleagues (much more stressful!). There's still an incredibly tiny number of people seriously working on solving this problem, maybe a few dozen serious researchers. Nobody's on the ball! There's so much interesting and productive ML research to do on this, and the gravity of the challenge demands a much more concerted effort than what we're currently putting forth.

But that's just the first part of the plan—what really keeps me up at night is the intelligence explosion. Aligning the first AGIs, the first somewhat-superhuman systems, is one thing. Vastly superhuman, alien superintelligence is a new ballgame, and it is a scary ballgame.

The intelligence explosion will be more like running a war than launching a product. We're not on track for superdefense, for an airgapped cluster or any of that; I'm not sure we would even realize if a model self-exfiltrated. We're not on track for a sane chain of command to make any of these insanely high-stakes decisions, to insist on the very-high-confidence appropriate for superintelligence, to make the hard decisions to take extra time before launching the next training run to get safety right or dedicate a large majority of compute to alignment research, to recognize danger ahead and avert it rather than crashing right into it. Right now, no lab has demonstrated much of a willingness to make any costly tradeoffs to get safety right (we get lots of safety committees, yes, but those are pretty meaningless). By default, we'll probably stumble into the intelligence explosion and have gone through a few OOMs before people even realize what we've gotten into.

We're counting way too much on luck here.

Next post in series:

IIId. The Free World Must Prevail

As not-very-politely certified by the doomer-in-chief! At the very least, I would call myself a strong optimist that this problem is solvable. I have spent considerable energies debating the AI pessimists and strongly advocated against policies like an AI pause.↩

I'm most worried about things just being totally crazy around superintelligence, including things like novel WMDs, destructive wars, and unknown unknowns. Moreover, I think the arc of history counsels us to not underrate authoritarianism—and superintelligence might allow authoritarians to dominate for billions of years.↩

As Tyler Cowen says, muddling through is underrated!↩

Ironically, the safety guys made the biggest breakthrough for enabling AI's commercial success by inventing RLHF! Base models had lots of raw smarts but were unsteerable and thus unusable for most applications. ↩

This highlights an important distinction: the technical ability to align (steer/control) a model is separate from a values question of what to align to. There have been many political controversies about the latter question. And while I agree with the opposition to some of the outgrowths here, that shouldn't distract from the basic technical problem. Yes, alignment techniques can be misused—but we will need better alignment techniques to ensure even basic side constraints for future models, like follow instructions or follow the law. See also "AI alignment is distinct from its near-term applications".↩

"We estimate an average hourly payment of approximately $95 per hour," p.3 of the GPQA paper.↩

Very simplified, think of an AI system trying, via trial and error, to maximize money over a period of a year, and the final, trained AI model being the result of a selection process that selects for the AI systems that were most successful at maximizing money.↩

What RL is doing is simply exploring strategies for succeeding at the objective. If a strategy works, it is reinforced in the model. So if lying, fraud, power-seeking, etc. (or patterns of thinking that could lead to these sorts of behaviors in at least some situations) work, these will also be reinforced in the model.↩

(or inference-time monitoring models trained with human supervision)↩

Moreover, even recent progress in mechanistic interpretability to "disentangle the features" of models with sparse autoencoders doesn't on its own solve the problem of how to deal with superhuman models. For one, the model might simply "think" in superhuman concepts you don't understand. Moreover, how do you know which feature is the one you want? You still don't have ground truth labels. For example, there might be tons of different features that look like the "truth feature" to you, one of which is "what the model actually knows" and the others being "what would xyz human think" or "what do the human raters want me to think" etc.

Sparse autoencoders won't be enough on their own, but they will be a tool—an incredibly helpful tool!—that ultimately has to cash out in helping with things like the science of generalization.↩

Essentially, needing only the consistency properties of truth, rather than strong/ground truth labels of true/false, which we won't have for superhuman systems.↩

I'm still worried about the scalability of a lot of these techniques to very superhuman models—I think explicitly or implicitly they mostly rely on ground-truth labels, i.e. a supervisor smarter than the model, and/or favorable generalization.↩

A model stealing its own weights, to make copies of itself outside of the original datacenter.↩

Protecting against humans fooled or persuaded by the AI to help it exfiltrate↩

Though, of course, while that may apply to current models and perhaps human-level systems, we have to be careful about attempting to extrapolate evidence from current models to future vastly superhuman models.↩

To be clear, given the stakes, I think "muddling through" is in some sense a terrible plan. But it might be all we've got.↩

I'm reminded of Scott Aaronson's letter to his younger self:

"There's a company building an AI that fills giant rooms, eats a town's worth of electricity, and has recently gained an astounding ability to converse like people. It can write essays or poetry on any topic. It can ace college-level exams. It's daily gaining new capabilities that the engineers who tend to the AI can't even talk about in public yet. Those engineers do, however, sit in the company cafeteria and debate the meaning of what they're creating. What will it learn to do next week? Which jobs might it render obsolete? Should they slow down or stop, so as not to tickle the tail of the dragon? But wouldn't that mean someone else, probably someone with less scruples, would wake the dragon first? Is there an ethical obligation to tell the world more about this? Is there an obligation to tell it less?

I am—you are—spending a year working at that company. My job—your job—is to develop a mathematical theory of how to prevent the AI and its successors from wreaking havoc. Where "wreaking havoc" could mean anything from turbocharging propaganda and academic cheating, to dispensing bioterrorism advice, to, yes, destroying the world."