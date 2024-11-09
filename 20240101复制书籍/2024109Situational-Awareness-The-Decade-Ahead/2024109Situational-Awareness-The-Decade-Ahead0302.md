Leopold Aschenbrenner.(2024).2024109Situational-Awareness-The-Decade-Ahead.Dwarkesh podcast => I. From GPT-4 to AGI: Counting the OOMs

IIIb. Lock Down the Labs: Security for AGI

The nation's leading AI labs treat security as an afterthought. Currently, they're basically handing the key secrets for AGI to the CCP on a silver platter. Securing the AGI secrets and weights against the state-actor threat will be an immense effort, and we're not on track.

In this piece:

Underrate state actors at your peril

The threat model

Model weights

Algorithmic secrets

What "supersecurity" will require

We are not on track

They met in the evening in Wigner's office. "Szilard outlined the Columbia data," Wheeler reports, "and the preliminary indications from it that at least two secondary neutrons emerge from each neutron-induced fission. Did this not mean that a nuclear explosive was certainly possible?" Not necessarily, Bohr countered.

"We tried to convince him," Teller writes, "that we should go ahead with fission research but we should not publish the results. We should keep the results secret, lest the Nazis learn of them and produce nuclear explosions first."

"Bohr insisted that we would never succeed in producing nuclear energy and he also insisted that secrecy must never be introduced into physics."

Richard Rhodes, The Making of the Atomic Bomb (p. 430)

On the current course, the leading Chinese AGI labs won't be in Beijing or Shanghai—they'll be in San Francisco and London. In a few years, it will be clear that the AGI secrets are the United States' most important national defense secrets—deserving treatment on par with B-21 bomber or Columbia-class submarine blueprints, let alone the proverbial "nuclear secrets"—but today, we are treating them the way we would random SaaS software. At this rate, we're basically just handing superintelligence to the CCP.

All the trillions we will invest, the mobilization of American industrial might, the efforts of our brightest minds—none of that matters if China or others can simply steal the model weights (all a finished AI model is, all AGI will be, is a large file on a computer) or key algorithmic secrets (the key technical breakthroughs necessary to build AGI).

America's leading AI labs self-proclaim to be building AGI: they believe that the technology they are building will, before the decade is out, be the most powerful weapon America has ever built. But they do not treat it as such. They measure their security efforts against "random tech startups," not "key national defense projects." As the AGI race intensifies—as it becomes clear that superintelligence will be utterly decisive in international military competition—we will have to face the full force of foreign espionage. Currently, labs are barely able to defend against scriptkiddies, let alone have "North Korea-proof security," let alone be ready to face the Chinese Ministry of State Security bringing its full force to bear.

And this won't just matter years in the future. Sure, who cares if GPT-4 weights are stolen—what really matters in terms of weight security is that we can secure the AGI weights down the line, so we have a few years, you might say. (Though if we're building AGI in 2027, we really have to get moving!) But the AI labs are developing the algorithmic secrets—the key technical breakthroughs, the blueprints so to speak—for the AGI right now (in particular, the RL/self-play/synthetic data/etc "next paradigm" after LLMs to get past the data wall). AGI-level security for algorithmic secrets is necessary years before AGI-level security for weights. These algorithmic breakthroughs will matter more than a 10x or 100x larger cluster in a few years—this is a much bigger deal than export controls on compute, which the USG has been (presciently!) intensely pursuing. Right now, you needn't even mount a dramatic espionage operation to steal these secrets: just go to any SF party or look through the office windows.

Our failure today will be irreversible soon: in the next 12-24 months, we will leak key AGI breakthroughs to the CCP. It will be the national security establishment's single greatest regret before the decade is out.

The preservation of the free world against the authoritarian states is on the line—and a healthy lead will be the necessary buffer that gives us margin to get AI safety right, too. The United States has an advantage in the AGI race. But we will give up this lead if we don't get serious about security very soon. Getting on this, now, is maybe even the single most important thing we need to do today to ensure AGI goes well.

Underrate state actors at your peril

Too many smart people underrate espionage.

The capabilities of states and their intelligence agencies are extremely formidable. Even in normal, non-all-out-AGI-race times (and from the little we know publicly), nation-states (or less advanced actors) have been able to:

Zero-click hack any desired iPhone and Mac with just a phone number,

Infiltrate an airgapped atomic weapons program,

Modify Google source code,

Find dozens of zero-days a year that take on average of 7 years to detect,

Spearfish major tech companies,

Install keyloggers on employee devices,

Insert trapdoors in encryption schemes,

Steal information via electromagnetic emanations or vibration,

Use just the noise from your computer to determine where you are on a video game map or steal a password,

Gain direct access to sensitive systems like nuclear power plants,

Exfiltrate 22 million security clearance files from the USG,

Expose the financial information of 110 million customers by planting vulnerabilities in HVAC systems,

Compromise computer hardware supply chains at large scale,

Slip malicious code into updates to software dependencies used by top tech companies and the USG

… let alone planting spies or seducing, cajoling, or threatening employees (which happens effectively at large scales, but is less public)

… let alone special forces operations and similar (when things really get hot).

For a further taste of what we're dealing with when facing down intelligence agencies, I highly recommend Inside the Aquarium, a book by a Soviet GRU (military intelligence) defector.

Already, China engages in widespread industrial espionage; the FBI director stated the PRC has a hacking operation greater than "every major nation combined." And just a couple months ago, the Attorney General announced the arrest of a Chinese national who had stolen key AI code from Google to take back with him to the PRC (back in 2022/23, and probably just the tip of the iceberg).

But that's just the beginning. We must be prepared for our adversaries to "wake up to AGI" in the next few years. AI will become the #1 priority of every intelligence agency in the world. In that situation, they would be willing to employ extraordinary means and pay any cost to infiltrate the AI labs.

The threat model

There are two key assets we must protect: model weights (especially as we get close to AGI, but which takes years of preparation and practice to get right) and algorithmic secrets (starting yesterday).

Model weights

An AI model is just a large file of numbers on a server. This can be stolen. All it takes an adversary to match your trillions of dollars and your smartest minds and your decades of work is to steal this file. (Imagine if the Nazis had gotten an exact duplicate of every atomic bomb made in Los Alamos.)

If we can't keep model weights secure, we're just building AGI for the CCP (and, given the current trajectory of AI lab security, even North Korea).

Even besides national competition, securing model weights is critical for preventing AI catastrophes as well. All of our handwringing and protective measures are for naught if a bad actor (say, a terrorist or rogue state) can just steal the model and do whatever they want with it, circumventing any safety layers. Whatever novel WMDs superintelligence could invent would rapidly proliferate to dozens of rogue states. Moreover, security is the first line of defense against uncontrolled or misaligned AI systems, too (how stupid would we feel if we failed to contain the rogue superintelligence because we didn't build and test it in an air-gapped cluster first?).

Securing model weights doesn't matter that much right now: stealing GPT-4 without the underlying recipe doesn't do that much for the CCP. But it will really matter in a few years, once we have AGI, systems that are genuinely incredibly powerful.

Perhaps the single scenario that most keeps me up at night is if China or another adversary is able to steal the automated-AI-researcher-model-weights on the cusp of an intelligence explosion. China could immediately use these to automate AI research themselves (even if they had previously been way behind)—and launch their own intelligence explosion. That'd be all they need to automate AI research, and build superintelligence. Any lead the US had would vanish.

Moreover, this would immediately put us in an existential race; any margin for ensuring superintelligence is safe would disappear. The CCP may well try to race through an intelligence explosion as fast as possible—even months of lead on superintelligence could mean a decisive military advantage—in the process skipping all the safety precautions any responsible US AGI effort would hope to take. We would also have to race through the intelligence explosion to avoid complete CCP dominance. Even if the US still manages to barely pull out ahead in the end, the loss of margin would mean having to run enormous risks on AI safety.

We're miles away for sufficient security to protect weights today. Google DeepMind (perhaps the AI lab that has the best security of any of them, given Google infrastructure) at least straight-up admits this. Their Frontier Safety Framework outlines security levels 0, 1, 2, 3, and 4 (~1.5 being what you'd need to defend against well-resourced terrorist groups or cybercriminals, 3 being what you'd need to defend against the North Koreas of the world, and 4 being what you'd need to have even a shot of defending against priority efforts by the most capable state actors). They admit to being at level 0 (only the most banal and basic measures). If we got AGI and superintelligence soon, we'd literally deliver it to terrorist groups and every crazy dictator out there!

Critically, developing the infrastructure for weight security probably takes many years of lead times—if we think AGI in ~3-4 years is a real possibility and we need state-proof weight security then, we need to be launching the crash effort now. Securing weights will require innovations in hardware and radically different cluster design; and security at this level can't be reached overnight, but requires cycles of iteration.

If we fail to prepare in time, our situation will be dire. We will be on the cusp of superintelligence, but years away from the security necessary. Our choice will be to press ahead, but directly deliver superintelligence to the CCP—with the existential race through the intelligence explosion that implies—or wait until the security crash program is complete, risking losing our lead.

Algorithmic secrets

While people are starting to appreciate (though not necessarily implement) the need for weight security, arguably even more important right now—and vastly underrated—is securing algorithmic secrets.

One way to think about this is that stealing the algorithmic secrets will be worth having a 10x or more larger cluster to the PRC:

As discussed in Counting the OOMs, algorithmic progress is probably similarly as important as scaling up compute to AI progress. Given the baseline trend of ~0.5 OOMs of compute efficiency a year (+ additional algorithmic "unhobbling" gains on top), we should expect multiple OOMs-worth of algorithmic secrets between now and AGI. By default, I expect American labs to be years ahead; if they can defend their secrets, this could easily be worth 10x-100x compute.

(Note that we're willing to incur American investors 100s of billions of dollars of costs by export controlling Nvidia chips—perhaps a 3x increase in compute cost for Chinese labs—but we're leaking 3x algorithmic secrets all over the place!)

Maybe even more importantly, we may be developing the key paradigm breakthroughs for AGI right now. As discussed previously, simply scaling up current models will hit a wall: the data wall. Even with way more compute, it won't be possible to make a better model. The frontier AI labs are furiously at work at what comes next, from RL to synthetic data. They will probably figure out some crazy stuff—essentially, the "AlphaGo self-play"-equivalent for general intelligence. Their inventions will be as key as the invention of the LLM paradigm originally was a number of years ago, and they will be the key to building systems that go far beyond human-level. We still have an opportunity to deny China these key algorithmic breakthroughs, without which they'd be stuck at the data wall. But without better security in the next 12-24 months, we may well irreversibly supply China with these key AGI breakthroughs.

It's easy to underrate how important an edge algorithmic secrets will be—because up until ~a couple years ago, everything was published. The basic idea was out there: scale up Transformers on internet text. Many algorithmic details and efficiencies were out there: Chinchilla scaling laws, MoE, etc. Thus, open source models today are pretty good, and a bunch of companies have pretty good models (mostly depending on how much $$$ they raised and how big their clusters are). But this will likely change fairly dramatically in the next couple years. Basically all of frontier algorithmic progress happens at labs these days (academia is surprisingly irrelevant), and the leading labs have stopped publishing their advances. We should expect far more divergence ahead: between labs, between countries, and between the proprietary frontier and open source models. A few American labs will be way ahead—a moat worth 10x, 100x, or more, way more than, say, 7nm vs. 3nm chips—unless they instantly leak the algorithmic secrets.

Put simply, I think failing to protect algorithmic secrets is probably the most likely way in which China is able to stay competitive in the AGI race. (I discuss this more later.)

It's hard to overstate how bad algorithmic secrets security is right now. Between the labs, there are thousands of people with access to the most important secrets; there is basically no background-checking, silo'ing, controls, basic infosec, etc. Things are stored on easily hackable SaaS services. People gabber at parties in SF. Anyone, with all the secrets in their head, could be offered $100M and recruited to a Chinese lab at any point. You can … just look through office windows. And so on. There are many articles, and rumors flying around SF, purporting to have extensive details of various lab algorithmic advances.

AI lab security isn't much better than "random startup security." Directly selling the AGI secrets to the CCP would at least be more honest.

… Is this what we see at OpenAI or any other American AI lab? No. In fact, what we see is the opposite — the security equivalent of swiss cheese. Chinese penetration of these labs would be trivially easy using any number of industrial espionage methods, such as simply bribing the cleaning crew to stick USB dongles into laptops. My own assumption is that all such American AI labs are fully penetrated and that China is getting nightly downloads of all American AI research and code RIGHT NOW…

Marc Andreessen

While it will be tough, I think these secrets are defensible. There are probably only dozens of people who truly "need to know" the key implementation details for a given algorithmic breakthrough at a given lab (even if a larger number need to know the basic high-level idea)—you can vet, silo, and intensively monitor these people, in addition to radically upgraded infosec.

What "supersecurity" will require

There's a lot of low-hanging fruit on security at AI labs. Merely adopting best practices from, say, secretive hedge funds or Google-customer-data-level security, would put us in a much better position with respect to "regular" economic espionage from the CCP. Indeed, there are notable examples of private sector firms doing remarkably well at preserving secrets. Take quantitative trading firms (the Jane Streets of the world) for example. A number of people have told me that in an hour of conversation they could relay enough information to a competitor such that their firm's alpha would go to ~zero—similar to how many key AI algorithmic secrets could be relayed in a short conversation—and yet these firms manage to keep these secrets and retain their edge.

While most of America's leading AI labs have refused to put the national interest first—rejecting even basic security measures in this tier, if they have any cost or require any prioritization of security—picking this low-hanging fruit would be well within their abilities.

But let's look out just a bit further. Once China begins to truly understand the import of AGI, we should expect the full force of their espionage efforts to come to bear; think billions of dollars invested, thousands of employees, and extreme measures (e.g., special operations strike teams) dedicated to infiltrating American AGI efforts. What will security for AGI and superintelligence require?

In short, this will only be possible with government help. Microsoft, for example, is regularly hacked by state actors (e.g., Russian hackers recently stole Microsoft executives' emails, as well as government emails Microsoft hosts). A high-level security expert working in the field estimated that even with a complete private crash course, China would still likely be able to exfiltrate the AGI weights if it was their #1 priority—the only way to get this probability to the single digits would require, more or less, a government project.

While the government does not have a perfect track record on security themselves, they're the only ones who have the infrastructure, know-how, and competencies to protect national-defense-level secrets. Basic stuff like the authority to subject employees to intense vetting; threaten imprisonment for leaking secrets; physical security for datacenters; and the vast know-how of places like the NSA and the people behind the security clearances (private companies simply don't have the expertise on state-actor attacks).

I'm not one of the people behind the security clearances, so I can't give a proper accounting of what security for AGI will truly require. The best public resource on this is RAND's report on weight security. To give a taste of what this state-actor proof security will actually mean:

Fully airgapped datacenters, with physical security on par with most secure military bases (cleared personnel, physical fortifications, onsite response team, extensive surveillance and extreme access control).

And not just for training clusters—inference clusters need the same intense security!

Novel technical advances on confidential compute / hardware encryption and extreme scrutiny on the entire hardware supply chain.

All research personnel working from a SCIF (Sensitive Compartmented Information Facility, pronounced "skiff", see this visualization).

Extreme personnel vetting and security clearances (including regular employee integrity testing and the like), constant monitoring and substantially reduced freedoms to leave, and rigid information siloing.

Strong internal controls, e.g. multi-key signoff to run any code.

Strict limitations on any external dependencies, and satisfying general requirements of TS/SCI networks.

Ongoing intense pen-testing by the NSA or similar.

And so on…

The giant AGI clusters are being mapped out, right now; the corresponding security effort must be too. If we are building AGI in just a few years, we have very little time.

Still, this immense effort shouldn't lead to fatalism. The saving grace on security is that the CCP probably isn't fully AGI-pilled yet, and so not yet investing in the most extreme efforts. American AI lab security "only" has to stay ahead of the curve compared to the intensity of Chinese espionage efforts. That means immediately upgrading security to stay ahead of "more normal" economic espionage (which we are far from resistant to, but private companies probably could be); and that means over the next couple years, as Chinese and other foreign espionage ramps up, rapidly upgrading to much more intense measures in cooperation with the government.

Some argue that strict security measures and their associated friction aren't worth it because they would slow down American AI labs too much. But I think that's mistaken:

This is a tragedy of the commons problem. For a given lab's commercial interests, security measures that cause a 10% slowdown might be deleterious in competition with other labs. But the national interest is clearly better served if every lab were willing to accept the additional friction: American AI research is way ahead of Chinese and other foreign algorithmic progress, and America retaining 90%-speed algorithmic progress as our national edge is clearly better than retaining 0% as a national edge (with everything instantly stolen)!

Moreover, ramping security now will be the less painful path in terms of research productivity in the long run. Eventually, inevitably, if only on the cusp of superintelligence, in the extraordinary arms race to come, the USG will realize the situation is unbearable and demand a security crackdown. It will be so much more painful, and cause much more of a slowdown, to have to implement extreme, state-actor-proof security measures from a standing start, rather than iteratively.

Others argue that even if our secrets or weights leak, we will still manage to eke out just ahead by being faster in other ways (so we shouldn't worry about these security measures). That, too, is mistaken, or at least running way too much risk:

As I discuss in a later piece, I think the CCP may well be able to brutely outbuild the US (a 100GW cluster will be much easier for them). More generally, China might not have the same caution slowing it down that the US will (both reasonable and unreasonable caution!). Even if stealing the algorithms or weights "only" puts them on par with the US model-wise, that might be enough for them to win the race to superintelligence.

Moreover, even if the US squeaks out ahead in the end, the difference between a 1-2 year and 1-2 month lead will really matter for navigating the perils of superintelligence. A 1-2 year lead means at least a reasonable margin to get safety right, and to navigate the extremely volatile period around the intelligence explosion and post-superintelligence. A mere 1-2 month lead means a breakneck international arms race with extreme pressures, racing through the intelligence explosion, and no room at all to get safety right. It is that neck-and-neck, existential race in which we face the greatest risks of self-destruction.

Don't forget about Russia, Iran, North Korea, and so on. Their hacking capabilities are no slouch. On the current course, we're freely sharing superintelligence with them too! Without much better security, we're proliferating what will be our most powerful weapon to a plethora of incredibly dangerous, reckless, and unpredictable actors.

We are not on track

When it first became clear to a few that an atomic bomb was possible, secrecy, too, was perhaps the most contentious issue. In 1939 and 1940, Leo Szilard became known "throughout the American physics community as the leading apostle of secrecy in fission matters." But he was rebuffed by most; secrecy was not at all something scientists were used to, and it ran counter to many of their basic instincts of open science. But it slowly became clear what had to be done: the military potential of this research was too great for it to simply be freely shared with the Nazis. And secrecy was finally imposed, just in time.

Leo Szilard.

In the fall of 1940, Fermi had finished new carbon absorption measurements on graphite, suggesting graphite was a viable moderator for a bomb. Szilard assaulted Fermi with yet another secrecy appeal. "At this time Fermi really lost his temper; he really thought this was absurd," Szilard recounted. Luckily, further appeals were eventually successful, and Fermi reluctantly refrained from publishing his graphite results.

At the same time, the German project had narrowed down on two possible moderator materials: graphite and heavy water. In early 1941 at Heidelberg, Walther Bothe made an incorrect measurement on the absorption cross-section of graphite, and concluded that graphite would absorb too many neutrons to sustain a chain reaction. Since Fermi had kept his result secret, the Germans did not have Fermi's measurements to check against, and to correct the error. This was crucial: it led the German project to pursue heavy water instead—a decisive wrong path that ultimately doomed the German nuclear weapons effort.

If not for that last-minute secrecy appeal, the German bomb project may have been a much more formidable competitor—and history might have turned out very differently.

There's a real mental dissonance on security at the leading AI labs. They full-throatedly claim to be building AGI this decade. They emphasize that American leadership on AGI will be decisive for US national security. They are reportedly planning 7T chip buildouts that only make sense if you really believe in AGI. And indeed, when you bring up security, they nod and acknowledge "of course, we'll all be in a bunker" and smirk.

And yet the reality on security could not be more divorced from that. Whenever it comes time to make hard choices to prioritize security, startup attitudes and commercial interests prevail over the national interest. The national security advisor would have a mental breakdown if he understood the level of security at the nation's leading AI labs.

There are secrets being developed right now, that can be used for every training run in the future and will be the key unlocks to AGI, that are protected by the security of a startup and will be worth hundreds of billions of dollars to the CCP. The reality is that, a) in the next 12-24 months, we will develop the key algorithmic breakthroughs for AGI, and promptly leak them to the CCP, and b) we are not even on track for our weights to be secure against rogue actors like North Korea, let alone an all-out effort by China, by the time we build AGI. "Good security for a startup" simply is not even close to good enough, and we have very little time before the egregious damage to the national security of the United States becomes irreversible.

We're developing the most powerful weapon mankind has ever created. The algorithmic secrets we are developing, right now, are literally the nation's most important national defense secrets—the secrets that will be at the foundation of the US and her allies' economic and military predominance by the end of the decade, the secrets that will determine whether we have the requisite lead to get AI safety right, the secrets that will determine the outcome of WWIII, the secrets that will determine the future of the free world. And yet AI lab security is probably worse than a random defense contractor making bolts.

It's madness.

Basically nothing else we do—on national competition, and on AI safety—will matter if we don't fix this, soon.

Next post in series:

IIIc. Superalignment

A billboard at the Oak Ridge, Tennessee uranium enrichment facilities, 1943.

One spoiler, as a taste: on graduation from their ~spy academy, before being sent overseas, aspiring spies had to prove their skills domestically: they had to acquire secret information from a Soviet scientist. The penalty for revealing state secrets, of course, was death. That is: graduating from the ~spy academy meant picking a countryman to condemn to death. HT Ilya Sutskever for the book recommendation.↩

By the way, the indictment provides a great illustration of how easy it is to evade security at even Google, which likely has the best security of all the AI labs (given their ability to lean on Google's decades-long investment in security infrastructure). All it took to steal the code, without detection, was pasting code into Apple Notes, then exporting to pdf!

"DING exfiltrated these files by copying data from the Google source files into the Apple Notes application on his Google-issued MacBook laptop. DING then converted the Apple Notes into PDF files. and uploaded them from the Google network into DING Account 1. This method helped DING evade immediate detection." (From the indictment.)

He only got caught because he did a bunch of other stupid things, like immediately start prominent startups in China which got people suspicious (and later even came back to the US).↩

Based off of their claimed correspondence of their security levels to RAND's weight security report's L1-L5.↩

I sometimes joke that AI lab algorithmic advances are not shared with the American research community, but they are being shared with the Chinese research community!↩

Indeed, I've heard from friends that ByteDance emailed basically every person who was on the Google Gemini paper to recruit them, offering them L8 (a very senior position, with presumably similarly high pay), and pitching them by saying they'd report directly to the CTO in America of ByteDance.↩

Inference fleets will likely be much larger than training clusters, and so there will be overwhelming pressure to use these inference clusters to run automated AI researchers during the intelligence explosion (and run billions of superintelligences more broadly in the immediate aftermath). The AGI/superintelligence weights could thus be exfiltrated from these clusters as well. (I worry that this is underrated, and inference clusters will be much less protected.)↩

But you can't rely only on this! Hardware encryption regularly gets side-channeled. Defense-in-depth is key, of course.↩

For example, space to take an extra 6 months during the intelligence explosion for alignment research to make sure superintelligence doesn't go awry, time to stabilize the situation after the invention of some novel WMDs by directing these systems to focus on defensive applications, or simply time for human decision-makers to make the right decisions given an extraordinarily rapid pace of technological change with the advent of superintelligence.↩

We try really hard to prevent nuclear proliferation to rogue states, even if we'd still be "ahead" on nuclear technology compared to their more limited arsenal, given the mayhem proliferation can cause.↩

The Making of the Atomic Bomb, p. 509↩

The Making of the Atomic Bomb, p. 507↩

100x+ compute efficiencies, when clusters worth $10s or $100s of billions are being built.