



Part I

Three Introductory Talks




CHAITER 2 Measuring Information

FOREWORD

Future historians of science may find it curious that despite the zolume of activity sparked off by Wiener's and Shannon's classic publications in the United States, it was in London that the First International

Symposium on Information Theory was held in the summer of 1950. Organized by a small commitlee chaired by Professor IVillis Jackson (now Lord Jackson) of Imperial College, which included a number of enthusiasts for inter-disciplinary collaboration, it became the

forerunner of a series of 'London Symposia' which oucr the next

ten years brought together an unusually wide range of scientists, all

concerned in some way with systems that depend for their functioning on the transmitting or processing of information.

Such inter-disciplinary meetings, now commonplace, cere suficiently

novel in 1950 to excite considerable public interest. The B.B.C. Third Programme talk, the text of which is given below, was an attempt to sketch for a lay audience the ideas and hopes that brought us together on that first occasion. As such I hope that it may be found

useful (despite its antique flacour in spots) by readers who feel the need for some gentle introduction to the papers that follow. Those who do not can skip it without loss.

A few months ago there met in London, in the rooms of the Royal Society, a strangely assorted group of pcople. About a hundred and twenty strong, they includcd mathema- ticians, physicists, engineers, linguists, physiologists, gencti- cists-in fact folk from almost every branch of scicnce 10 CHAPTER 2

-and they numbered among them representatives from eight different countries.

The subject which attracted us from our various speciali- zations to take part in this unique exchange of ideas was a relatively new one. It is called 'the theory of information', and, as you will have guessed, there are few branches of science about which it has not something more or less useful to say. It is about the new ways of measuring and thinking about information, which we have recently discovered, that I want to speak in this paper.

But, first, why should we want to measure information? There are sevcral reasons. The first is a sevcrely practical one. A scientist is constantly having to choose betwcen differ- ent possible ways of tackling a problem. An agriculturalist wants to compare the yields of two kinds of wheat: how shall he plan his experimcnts so as to get the most out of them for a given expenditure of land or seed? Or, a tclegraph engincer wants to design a communication system: which of the many possible varieties will be the most economical for his purpose? What we really want in each case is to discover the method which will give us the maximum amount of information for a given outlay of time or space or other resources. Therc are other reasons for studying the notion of information which will become clearer as we go along; but pcrhaps the practical one will suffice for the moment.

SELECTIVE INFORMATION-CONTENT

Suppose we begin by asking ourselves what we mcan by information. Roughly speaking, we say that we have gaincd information when we know something now that we didn't know before; when 'what weknow' has changed. For example, if we ask a question so simple that it has only two possible answers— yes or no — then we gain information when we receive the answer, yes or no as the case may be. This is the simplest piece of information we can receive; the simplest possible answer to a question with only two possiblc answers. MEASURING INFORMATION

11

Now, if we know there are only two possible answers, we may think of the word 'yes' as an instruction, telling us to select one of the two answers. We can carry this idea a step further. We can say that any answer to a question, however complicated, can be reduced to a set of instructions telling us which of the possible answers to select as the right one. e have, in fact, arrived at one of the most important tech- nical senses of the term 'information': that which enables us to make a selection from a set of possibilities or to narrow the range of possibilities about which we are ignorant. We may use the term 'selective' to distinguish this from other possible functions of information, and it is not difficult to sce how this function can be measured. The selcctive information- content' of a message, or of the result of a scientific experiment, for example, has to do with the number of independent choices between two possibilities which it enables us to make —the number of independent yes's or no's to which it is equivalent.

Let me hasten to give you a homely illustration, for this idea is quite simple to see in practice, though difficult to describe in words. Let us suppose that we have two jars ofd jam on a shelf, numbered one and two, and in one of them the jam has gone bad, we don't know which, but a friend does.d We ask him 'Is it number one?' The answer, whether yes or no, provides us with one unit or 'bit' of information, as it is called. It has enabled us to select onc out of two possibilitics. Imagine now that we were confronted with eight jars of jam, numbered one to eight. If we entered into a kind of 'Twenty Questions' game with our friend, we might begin by asking—Is it onc? Is it two? — and so forth until we found the onc containing the bad jam. But on the avcrage this is not the quickest way. The most cconomical method is to divide the jars first into two blocks of four and ask: Is the bad jam in the first block? Then, having discovered in which block it is, we split that into two, and so on. You can casily verify that this method, on the average, leads more 12

CHIAPTER 2

quickly to the final answer than any other. So the amount of selective information wrung from our friend in this case is defined as the minimum number of choices we've had to make in order to identify the jar of bad jam. And the number of choices is at a minimum if at each stage we arrange to choose between two equally likely possibilitics. If we do not, then on the average we shall have to ask more questions—without, of course, gaining any more information.

Mathematicians will no doubt recognize at this point that we have really brought in the notion of probability in an underhand way. The assumption we are secretly making is that thc chances of the bad jam's being in the first block are equal to the chances of its being in the second, provided that we have the same number ofjars in cach. So before lcaving the technicalities (which aren't, perhaps, of great importance in what follows), let us come into the open and admit that we must define 'selective information-content' as the equivalent number of independent choices betwcen equally likely alterna- tives. If we didn't make this amendment we might find ourselves saying that the 'amount of information' in a message which we were practically sure of getting was the same as in one which was quite unexpected or improbable.

DESCRIPTIVE INFORMATION-CONTENT

We have so far been talking of situations in which informa- tion could be thought of as the answer to a question. It is as if we possesscd an enormous filing cabinet containing all possible messages, or results of an expcriment, and we re- garded our information as instructing us to select the right one. The commonest messages we would arrange, of course, to be the easiest to select — to be picked out in the smallest number of stages.

But I want now to discuss a new kind of situation, in which our problem is not to select but to build a picture. Suppose, for example, that we are biologists or physicists looking down MEASURING INFORMATION

13

a microscope or taking readings on a measuring instrument. Our first problem here is to transform our experience into a symbolic picture or description of what we believe to bed the case. Our picture, be it a graph or a drawing, or a scientific statement, depends for its every feature on our actual observations. Each element in the picture therefore formally represents and has its origin in one corresponding elementary feature of the experience pictured. Nothingt can legitimately appear in the picture, in other words, unless we have evidence for it by way of expcrienced obscrvations.

This is an essentially different situation from the earlier one in which we were interested in choosing from a set of ready-made alternatives. Here our picture is not selected, but built up brick by brick, the bricks being provided byu our scientific observations. The result is again an addition to what we know to be the case, so we can still say that we are gaining information. But our use of the term here has changed. a radio signal, whose power we can measure with an accuracy of one percent, gives us more information than one which we can measure only to ten percent, since we can justify the use of more scale-divisions in the first case than in the sccond to represent our result. Again, we would say that a The apparatus which gives us most descriptive information, in this new sense of the term, will be that which yields the largest number of bricks (metaphorically speaking) for our symbolic picture, or which enables us to show the maximum amount of fine structure in it. For example, we may say that microscope which can distinguish points one ten-thousandth of a centimetre apart gives more information than one which can only discriminate to one one-thousandth. As a matter of fact, there is an important difference between these two examples. In the first it was the precision or reliability of our result which we took as a measure of the amount of information it gave us. In the second, it was the number of distinguishable features which provided our criterion. 14

CHAPTER 2

To avoid confusion we have to introduce two more technical terms. When an observation mercly incrcascs our reliance on a result, we say it has gained in metrical information- content; whereas when we are enabled to add new features to our picture, we say it has gained in structural information- content. The two are complementary measurcs of scientific information, which typically includes both aspects.

But here again the technicalities do not really matter. The point is that we have found a sccond way of quantifying information, by thinking of it as providing the bricks out of which to build scientific statements. Without information we could not formulate our statements. On the other hand, once a statement has been formulated, we can still regard it as a sclection from a range of possible alternatives and so estimate the selective information-content it represents, if we so wish. The threc measures of sclective, structural and metrical information-content are, in fact, complementary. A very rough analogy of their relationship would be the connection between volume, area and height, as measures of size. We must use whichever is appropriate to our purpose in given circumstances.

APPLICATIONS OF INFORMATION THEORY

How then do these new ways of thinking quantitatively about information find applications in the various branches of science? Our survey of the theory has been very hasty and rather rough; but if, for the moment, we stick to selective information-content, we can see, I think, the connecting thread. To measure the sclective information-content of any body of data, you remember, we ask one standard question. Out of how many equally likely possibilities has this come? If it excludes a large family of other possibilities, so to speak, it 'conveys more selective information' than if it represents onc out of only two or thrce possibilities. And a simple arith- metical rule enables us to calculate the actual amount of MEASURING INFORMATION

15

selective information in any given case from the number of possible alternatives.

Much of the work on selective information measures has been carried out by telegraph and telephone engineers. The engineer nowadays considers a communication system as a device which can exist in any one of a certain number of possible states. He thinks of a message as something chosen out of a set of possible messages. By thinking in this way, he can calculate precisely how much information his channel could carry in one minute and how much is represented by the message it is actually carrying. In this way it becomes meaningful to talk about the informational efficiency of a telephone channel and to compare, for example, the efficien- cies of rival coding systems.

A very similar approach is possible in any situation where information is communicated. Linguists are interested in measuring amounts of information contained in different speech sounds. Physiologists want to know how much in- formation could be carried by a nerve-fibre in a second,how much per second is received by the eye or the ear, and a host of other questions like that. It becomes quite precisely mean- ingful to ask, for example, whether a particular hypothetical model of the brain could contain as much information as we believe to be held by the real article. In fact, I believe that the ideas of information theory may make a number of real contributions to the study of the brain, which, if nothing else, is a remarkably efficient transformer of information.

In physics, of course, the notion of descriptive information- content is often more useful than that of selective in- formation-content. A physicist may want to know how much theoretically available information is being wasted in a given microscope. He may wish to compare the informational merits of two ways of tackling some problem of measurement. In each case he now has a precise measure of performance, which is sufficiently general to apply to all his possible techniques. 16 CHAPTER 2

But in physics the concept of selective information-content also becomes interesting, and even exciting, for its own sake. You have probably realized that our method of calculating the number of bits of information, by counting the number of successive sub-divisions rcquired to identify a given choice, amounts to taking the logarithm of the total number of equally likely possibilities. You remember that four jam jars needed two steps and eight jam jars needed three. One out of sixteen jam jars could be selected in four steps, and so on. The number of steps is just the logarithm of the number of possibilities, to the base 2.

Now in thermodynamics this strikes a familiar note. To cut a long story short, our definition of selective information- content turns out to be identical in its mathematical form with the statistical measure of thermodynamic entropy. The units of course are different; but otherwise the only distinction is a difference in sign: where information is given out, entropy increases.

It is possible to make too much of this resemblance; but I think there is no doubt that the famous second law of thermo- dynamics, which states that the entropy of an isolated system tends always to increase, is equivalent in our new language to the assertion that an isolated system can only lose or give out information. And since if a system did not give out information we could never know of it-is the second law really a tautology? I do not know. It is a controversial point. But perhaps now you begin to see why the study of information theory may have an importance quite apart from its immedi- ately practical value.

Of its other more philosophical implications there is not time to say much now. I think a strong case can be made for the suggestion that our concept of time, in at least one of its aspects, is directly linked with the objective notion of the flux of information. If this were so, the concept of time would become meaningless-in fact, could not be defined-for any total system in which the total information remained MEASURING INFORMATION

17

constant. The presence of an observer, of course, defines an

information sink, so that the concept of time must enter directly a system is divided into 'the observed' plus 'the observer'. The concepts of scientific information are still at a fairly primitive stage of development. There are interesting re- semblances, nevertheless, between the types of argument which are applicable in scientific information theory and certain of Eddington's theoretical discussions of the constants of nature. The emphasis in each case is the same-on the nature of the abstract symbolic picture, which we make to represent that which is the case. It remains to be seen how far the two approaches may beinter-related.

I am afraid that in this brief sketch I have given you only some very inadequate glimpses into this new subject and its implications; but we have, I think, seen how it has spun a connecting thread through many disciplines which are otherwise widely separated. At the same time we must beware of the tenptation to over-estimate its significance. The theory of information is first and foremost a linguistic tool. It enables us to speak precisely and quantitatively where previously we have had to speak vaguely and qualitatively. It providcs objective substitutes for intuitive criteria and subjective prejudices.

But its conclusions are seldom surprising; and it would, I think, be a mistake to place it in the same category as physical theories such as quantum or relativity theory. This is not of course to decry its value, but only to safeguard the theory from mistaken appraisal. If its contributions to science had been only linguistic, their practical results would have already

justified the effort which has been expended. But the subject is young, and I think we can confidently look for further develop- ments which, in the end, may even succeed in surprising us. POSTSCRIPT

Such were the hopes of 1950. It soon became clear that the biggest

problem in applying Shannon's selective information measure to 18 CHAPTER 2

human information-processing was to establish meaningful probabilities to be attached to the different possible signals or brain-states concerned. After a flourish of'applications of information theoryin psychology and biology which underrated the difficulty of this requirement, it has now come to be recognized that information theory has more to offer to the biologist in terms of its qualitative concepts than of its quantitative measures, though these can sometimes be useful in setting upper or lower limits to information-processing performance.

It also became clear that to avoid conceptual confusion it was not sufficient to preface the word'information' with distinguishing adjectives such as 'selective', structural' and 'metrical'. Our chief terminological need was for a way of keeping the notion of information per se distinct from all measures of'amount-of-information'. Rather than invent still more neologisms, I took to using 'information-content' (qualified as selective, structural or metrical) to denote the latter, leaving 'information' free to be used in its original ereryday sense (see Chapter 6). CHAPTER 3

Meaning and Mechanism

FOREWORD

Claude Shannon's measure of selectice information-content was framed explicitly to require no reference to the meaning of the infor- mation selected in response to a communication signal. The communica- tion process was viewed as a transaction betwcen terminals whose task was confined to the generation and reproduction of symbols. The understanding of these symbols was declared to be outwith the concern of the communication engineers, and the saying went abroad that Information Theory had no place for the concept of meaning.

The second part of this collection (see for example Chapters 5, G and 7) contains a number of papers aiming to narrow the gap between semantic and other aspects of the concept of Information as these were gradually hammered out. The text of the talk that follows* outlines a way of thinking about the function of an utterance which these papers use as a conceptual bridge between the mechanistic and semantic lecels. By picturing an item of information as a kind of tool that operates upon the recipient's internal'state of conditional readiness', we can conceniently define its meaning on the one hand, and its information-content (in various senses) on the other. This approach also ofJers a criterion of meaningfulness and meaninglessness which seems more realistic and less Procrustean than the'verifiability' or'falsifiability' criteria canvassed by some linguistic philosophers.

First broadcast in January 1960 on the B.B.C. Third Programme. Reprinted (revised) in Common Factor, No. 5，1968，pp. 57-65. 20 CHAPTER 3

A human conversation depends on many processes which a scientist would call 'mechanical', in the sense that only physical categories of cause and effect are needed to describe and explain them. Puffs of air, produced by vibration of the speaker's larynx, echo around the cavities of his mouth and result in a characteristic sequencc of sound waves. These travel through space and vibrate the sensitive membrane of the listener's ear, giving rise to nerve impulscs, and so on. Now, until the chain of explanation reaches the nervous system, nobody minds its mechanistic flavour. True, it has made no reference to the meaning of what is being said; but this, we might say, would obviously be premature. Questions of meaning need not arise until we bring in thc human links in the chain.

As far as it goes, I think this answer is fair enough; but as a clue to the relation between the meaning of a message and its mechanical embodiment it is far from satisfactory, on two main counts.

In the first place, it seems to imply a rather worrying and muddling sort of discontinuity. The original speaker, we suppose, means somcthing by what he says. His utterance has meaning-at least for him. Yet in the next stages of the chain of explanation (the generation of sound waves and all the rest of it) all signs of his meaning seem to have disappeared. Discussion at this level proceeds in exactly the same terms whether the air is handling the outpourings of a genius or the jabber of a monkey. Yet finally, when the message reaches the ear of a human listener, its 'meaning' seems to pop up again from nowhere, and concerns him far more than the physical properties of the sound wave which the speaker actually produces. There are in fact two awkward discontinuities in this way of telling the story: a jump from meaningful utterance to meaningless air vibrations; and then back again to meaning- ful utterance. The question that seems to be raised by this way of looking at the process is how the message recovers its meaning. Whether or not this is a sensible question remains to be seen. AEANING AND MECHANISA

21

The second objcction to an easy division of human communi- cation into mechanical stages and meaningful stages is a more serious one. The process by which the sound pressure-waves titillate the eardrums is mechanical. So far, so good. But what happens next? Isn't the process by which the nerves convey these titillations to the brain a mechanical one? And what then? Isn't the next, neurophysiological stage, though still puzzling in detail, plainly a mcchanical one too? WWhere are we to draw the line?

The position is complicated by our enormous ignorance of what goes on in the central nervous system. Some people would take advantage of this to suggest that somewhere in the brain the laws of mechanical causation, on which we have been relying, may give place to 'something else'-associated with the action of mind-and this could be the stage at which (as they would say)'meaning is given' to the buzz of physical brain activity.

For reasons that I won't go into now, I must say I find this suggestion unattractive. To begin with, it seems entircly arbitrary and without scientific foundation, and relics only on our ignorance of brain organization. But my chief objection is that it is an unnecessary way of seeking to safeguard the meaningfulness of human communication-a way that commends itself only if we insist on regarding meaningful and mechanical processcs as mutually exclusive, so that to describe something as 'mechanical' implies automatically that it is 'meaningless'. If, as I hope to show, this opposition of 'meaningful' and 'mechanical' is false, the momentum of the whole debate between 'mechanists' and 'anti-mechan- ists'disappears.

A FUNCTIONAL APPROACH

Suppose we now make a fresh start on the problem of meaning by asking what difference it makes to you when you receive and understand the meaning of a message. For our 22 CHAPTER 3

purpose it will be sufficicnt if we confine oursclvcs to in- dicative sentences;* suppose, for example, someone tells you 'it's raining'. What happens? You may be immersed in a book, and may not feel inclined even to grunt an acknow- ledgement. But this does not mean that your understanding of the message has had no effect on you. If a sudden call comes for you to go out of doors, for example, you may now be ready to reach for umbrella or mac. If someone comes in, you are likely to ask whcther he got wet; and so on. What has been affected by your understanding of the messagc is not necessarily what you do— as some behaviourists have suggested-but rather what you would be ready to do if given (relevant)circumstanccs arose. It is quite possible that relevant circumstances may never arise, so that a naively behaviouristic approach would reveal no sign that you had understood the message. It is not your behaviour, but rather your state of conditional readiness for bchaviour, which betokens the meaning (to you) of the message you heard.

At this stage you may wonder whether we are not merely replacing one problem by another-this idea of'states of conditional readiness' may sound every bit as vague and elusive as the notion of meaning itself. The all-important point, however, is that we can talk about 'states of readiness' in relation either to human beings or to mechanical systems- or indeed to human beings as mechanical systems. The notion offers us a conceptual bridge between the two ways of talking whose relationship has puzzled us.

Let me try to make it more definite by way of an example. Think of a railway signal-box controlling a large shunting- yard. At any given moment, the configuration of levers in the box defines what the yard is ready to do to any waggon that happens to come along. There may in fact be no waggons moving; there may be some tracks on which no waggons will *For a discussion of non-indicative meaning in these terms sce Chaptcrs 4 to 8 and Chapter 11. MEANING AND MECHANISA

23

move for years; but this is no obstacle to a definition of the total state of conditional readiness of the yard, as betokened by the total configuration of lever-settings, which determines what would happen if any given circumstance arose. A change of a lever that controls a disused siding may cause no visible change in the activity of the yard; but it makes a perfectly definite change in its state of conditional readiness.

Now we do not know at present how the 'signal-box' in our heads controls our own conditional rcadiness to act and react in all possible circumstances; but it seems reasonable in our present state of knowledge to suppose that there is a brain mechanism that does this. I don't mean of course that the brain is organized on the simple principles of railway signal- ling; there is vastly more subtlety in its blend of spontancous and controlled activity, which allows us to think of it as determining only the probabilitics of diffcrent actions in given circumstances, rather than anything as rigid as the motions of railway waggons. What is more, the brain differs from a shunting-yard in being a self-guiding system; and what we are chiefly concerned with is its state of readiness for goal-directed, adaptive activity: activity with a purpose. It is your conditional readiness for this kind of activity that is modified and moulded according to your understanding of the information you receive.

ENERGY VERSUS FORM

But with these cautions in mind, I do suggest that we can think metaphorically of the receipt of a message as causing a change in the 'lever-settings' of the brain, and so in the human receiver's state of readiness, in much the same sense as in the case of our shunting-yard. This will allow us to relate the concepts of meaning and mechanism in a very natural way.

On the one hand, we could say that all that is required to make the brain-levers change is the purely mechanical 24 CHAPTER 3

energy of the message, without reference to its meaning. In one sense this is true. On the other hand, changing the physical energy, say by doubling the loudness, of the message you hear, would not normally make much difference to its cffect on your brain-levers; whercas a change in its meaning, even if it left the total energy unaltercd, could makc all the diffcr- ence in the world.

The mechanical energy of a message must be sufficient to do the mechanical job that eventually rescts the brain-levers; but the selective job, of determining which levers shall move, depends on the form of the mcssage, and on the state of your brain before you hear it. This is where the meaning of the message comes in. As long as we think only of what actually happens, we may be able to make do with explanations solely in terms of physical energy. It isn't until we consider the range of other states of rcadiness, that might have been selected but weren't, that the notion of meaning comes into its own. A change in meaning implies a different selcction from the range of states of readiness. A meaningless message is one that makes no selection from the range. An ambiguous message is one that could make more than one selection.

A WORKING DEFINITION OF MEANING

And so we could go on; but these examples are pcrhaps sufficient to Icad us to a working dcfinition of meaning, in this context. It looks as if the meaning of a message can be defined very simply as its selcctive function on the range of the recipient's states of conditional readiness for goal-dircctcd activity; so that the meaning of a message to you is its selective function on the range of your states of conditional readiness. Defined in this way, meaning is clearly a relationship between message and recipient rather than a unique property of the message alonc. Thus the conundrum with which we began-the puzzle of the missing meaning- appears to be a spurious one. For the original speaker, the meaning of MEANING AND MECHANISM

25

what he says is the selective function he wants it to perform on the listener's range of states of readiness. This is distinct- and may, as we shall sec, be quite different-from the effective meaning to the listcner, which is of coursc the selcctive function actually performed; and both of these may differ from the conventional meaning, which is the selective function calculated for a 'standard recipient'. In between the speaking and the hearing-at the stages of mechanical transmission- no comparable selective opcrations occur, so that questions of meaning do not normally arise; but at any stage we can still define the intended meaning of the message as its in- tended selective function, and so on. No queer discontinuity occurs along the way.

The jabber of monkeys is thus distinguishablc cven at the mechanical level from the outpouring of the genius, if we ask the right mechanical question-about its ultimate selective function. Traced far enough along the chain,the effects of the signals emitted by the genius should-or at least could in principlc-modify your bodily state of readi- ness in a imanner intended by him; whereas nothing com- parable could be said for the sound of monkeys-unless indeed you had some exceptional acquaintance with their vocal habits!

MESSAGES AS KEYS'

Let me now digress a moment to introduce one further feature into our analogy of the signal-box. On the older one-track railway lines, the engine-driver carrics a key,which must be inserted and turned in a special signalling lock at the station before his train can be clearcd into the next section of the lines. His signal, we may say, is key-operatcd. Imagine now a complcte signal-box, working on the same principle. Insert a key of a given shape into the box, and you make a certain selection from the range of possiblc configurations of the signal-levers. Insert another, and the selection you make is different. 26 CHAPTER 3

What I am leading up to is the idea that the brain, con- sidered as a signal-box, is also 'key-operated'. The physical embodiment of a message, which eventually acts on the brain, may be likened to the key that sets up a certain configuration of levers in the signal-box we have been talking about. Its selective function, like that of a key, depends both on its shape and on the arrangement of levers it meets.

It will now be cvident that we have sidestepped our sccond conundrum (about the point in the nervous system at which incoming physical stimuli acquirc meaning). From our present point of view, it makes no more sense than to ask about the point inside the key-operated signal-box at which a key 'acquires selective power'. Therc is, no doubt, a point inside the box at which the 'selcctive powcr' of the key is exercised; but of course it had this power all along. Similarly, there is, no doubt, a stage in the central nervous process at which the selective function of a message is exercised, and your brain is set up in conditional readincss to match the state of affairs that the message betokens. But we should, I think, rightly decline to regard this as the acquisition of meaning by a hitherto meaningless incoming pattern; for anyone who knew enough of the state and mechanism of your brain (ex hypothesi) would have been ablc in principle to tell that the pattern possessed that mcaning for you, even if in fact you never received it. If you know enough about a signal-box, you can dctermine the 'selcctive power' that a particular key has for it without ever inserting the key.

STRUCTURAL VERSUS FUNCTIONAL CRITERIA

The analogy of a signal-box and key is of course desperately incomplete; for the brain responds to mcssages in a far more lively way than signal-levers to a key, and its reactions may even include a change in 'code' such that the same key can have different functions on two successive occasions. But the illustration will serve to introduce a topic of recent AEANING AND MECHANISA

27

debate among philosophical linguists and logicians, who arc professionally concerned to find an objcctive basis for talk about meaning. Proponents of one school of thought,whom for short we may call the 'structuralists', concentrate on the structure of what is said, and try to analyse mcaning by breaking sentences and words down into their logical com- ponents. An extreme form of this approach, advocatcd at one time by Bertrand Russell, 30 went by the name of logical atomism': the idea that the mcaning of a complex uttcrance could be broken down into a conjunction of clcmentary or atomic'sentences, cach so simple that it could not be further analyscd. Though applicable in some scicntific contexts, this notion runs into many difficultics with ordinary language. Advocatcs of the other school, whom we may term the op- crationalists', look for meaning rathcr in the pattern of the use that is made of words. This approach is gencrally associated with the name of Wittgenstein o whose later years were spent in vigorous repudiation of the atomistic view of language earlier expounded in his famous Tractatus Logico-Philosophicus.

Each party claims an insight into the nature of meaning that the other lacks; and although an outsidcr here must nceds tread delicately, I believe that the mechanistic analogics we have been considcring may help us to see not only the justice of these rival contentions, but also the possibility of a unified approach that finds room for both. For a similar argument could be imagined between people on the one hand who wanted to define the 'selective power' of a key by looking at its shape, and those on the other who prcferred to watch and see how it was used.

The first, the structuralists, could be quite successful if only all signal-boxcs were of a fixed pattern; but ifit turncd out that some boxes changed their internal arrangement with time, for example, so that the same key had a different sclcctive power at diffcrent times, their structural approach would naturally lose prestige. The second, the operationalists, would be in their element if keys behaved in a way that could not be 28 CHAPTER 3

predicted from their structure; but if in fact most kcys of a certain shape were found consistently to make a sclcction predictable from that shape, their operational mcthod would seem very roundabout and incfficient and lacking in insight.

As a parable of the situation in semantics this is a little unfair, but it will serve our present purpose. In cach case, I think, trouble arises through taking an experimental critcrion as an objective definition. Both the structure of a kcy and the pattern of its usc are necessary expcrimental pointers to its 'selective power'; but neither is suitable as an overall defini- tion of the notion. Similarly, both the structure of a message and its pattern of use would seem to be neccssary experimental pointers to its 'meaning'; but we only breed confusion if we try to turn cither of them into a definition of what they betoken.

Docs our mechanistic analysis offer any clucs, then, to a synthesis between these rival lines of thought? Let us recapitu- late briefly. Ve have been thinking of human communication in terms of the mcchanical pattern of causc-and-effcct that we have assumed to embody it from start to finisli. We have considered the human recipicnt's brain as a physical systcin, with at any time a ccrtain (statistical) 'state of conditional readiness', roughly analogous to what we called the 'state of conditional readincss' of a railway shunting-yard. The object of communication is to sclect some particular conditional readiness in the recipient from the range of statcs that are possible. The intcndcd meaning of the communication is then definable as the sclcctive function that it is intended to exercise on the range of possible states. Its effective meaning is the selcctive function that it actually performs.

SEMANTIC UNITS AND CRITERIA OF TRUTHFULNESS

Now the big difference between the brain and a signal-box, of course, comes in here; for, as we noted, the effect of an MEANING AND MECHANISAI

29

input to the brain is liable to depend in a complicated way on what has gone before it; and it is only in spccial cases, usually after long training, that onc could rely on gctting exactly the samc effcct from the same input at different times. The moral-and it is an important onc-is that what we may call the 'semantic units' of communication-corres- ponding to the keys we have been talking about-are often made up of a whole group of words or even of sentences acting together, rather than singlc words acting in isolation. The sclective job is done in easy stages, as it were, and the final sharpening-up of the state of readiness may sometimes have to wait a long time for some of the words necessary to complete it. (This is particularly true, of course, in poctic and religious forms of spccch--but that's another story.)

It might be argued on these lines that the concept of semantic unit must be extended to include the whole linguistic experience of the listener; but this in most cascs would be unrealistic. Our point is simply that in many quite ordinary cases the unit of communication can and does cxtend far beyond the boundaries of a grammatically complete and apparently unambiguous statement, so that it becomes unrcalistic to attach labels such as 'true' or 'false' to the particular statement in isolation. For truthful communication, what matters is whether the present mcssage, coupled with what has gone before it, is calculated to select a state of readiness to match the actual state of affairs. If it is not, then the communication is untruthful, regardless of whether we would be inclincd to accept its component sentences as truc if we took them in isolation. It is easy to see from a mechanistic angle how cven a physical change in tone of voice might alter the state of readiness selected from an appropriate one to an inappropriate one. I can deceive you by telling you the truth, if I do so in such a way that I know you will not believe me. More insidiously, of course, I can do so by simply selccting 'true information' which I know will give you a false im- prcssion in the absencc of other data. In short, by insisting 30 CHAPTER 3

that criteria of truthfulness should be applied to semantic units rather than to statements, we demand an even higher

standard of honesty in human discourse than is achicved by simple propositional logic.

In the end, then, we find ourselves agreeing with both the 'structuralists' and the 'operationalists'. Meaning is indecd inseparable from use, for it is a relation between imcssage and recipient which may differ from one recipicnt to another. Thus far our sympathies must be with the opcrationalists. On the other hand, provided that we considcr semantic units instead of words, we can agree with the 'structuralists' in believing that the structurc is a major determinant of selcctive function. Different though they are in dctailed contents, our brains embody basic principlcs of organization that have to be

reckoned with- and in that sense reflccted —in any linguistic system. Indecd I would go so far as to hope that

when-if ever-the outlincs of the 'shunting-yard' of

our brains become a little clearer, one of the tools that will

help us further to unravel its structure may well be the analysis of human language.

POSTSCRIPT

A standard source of the line of thought we have called "operational-

ist'is Wittgenstein's Philosophical Invcstigations.40 A more

'structuralist' approach is taken by Ullman in The Principles of

Scmantics. 38 Contemporary trends may be followed in: The Structure

of Language, edited by J. A. Fodor and J. J. Katz.6

A recent general review entitled 'Opinions about Language'is

given in: What is Language?-A New Approach to Linguistic

Description by R. M1. IV. Dixon.³ CHAPTER 4

What Makes a Question?

In our search for a conceptual bridge between mechanism and meaning, we have so far considered only indicatice sentences. The third of these introductory talks* tackles the problem of defining the meaning of interrogatice utterances in a mechanistic context. The notion of 'conditional readiness' is here illustrated in terms of a swilchboard (of a rather indeterministic sort) instead of a signal-box; but the approach is essentially the same as in Chapter 3.

Asking questions, like walking, is something we lcarn to do from infancy-as every parent knows all too well. It comes so naturally, in fact, that to ask how we do it may seem more than a little queer. And yet, when you think about it, there is something rather remarkable about this ability of ours to coax or wring information out of one another just by uttering a few words of our own; and when you come to study communication between human beings from a scientific point of view, as the new science of 'information theory'tries to do, it is not at all obvious what distinguishes a question from all the other noises a man can make, or how to describe the process by which questions produce the effects they do. This is the problem I want to discuss-the problem of describing scientifically how questions work.

Broadcast on B.B.C. Third Programme and first published in The Listener, May 5th, 1960. 32 CIIAPTER 4

FORM AND INTONATION

I suppose our first gucss might be that the peculiar nature of a qucstion lay in its grammatical construction. It is a fact that ncarly all our questions are cxprcsscd in a special form: for cxample, we turn the indicative: 'You are going home'into the interrogative: 'Are you going home?'Thc order of subject and verb is reversed. In many cases this kind of clue is indced sufficicnt to mark the uttcrance as a question. But what if someone simply says, 'Going home?' I do not think you would doubt that he was asking you a qucstion; yet the very same words, withh a different intonation, could also be the answer to a question: 'Where are you off to?'-Going home'. Evidently grammatical form, though a useful clue in most cases, is not the essential distinguishing featurc of a qucstion. In idiomatic specch particularly, the intonation may sometimes be the thing that matters most. IVe can think of the questioning intonation, in fact, as a kind of vocal equivalent of the qucstion-mark. Incidcntally, have you ever thought how much richer and less ambiguous our printed language would be if otuly we had an easy way of reprcsenting intonation-say by making lettcrs larger and smallcr, or tilting the lines up or down? IVe lose much of the information-content of spcech by printing it.

Our examples so far have all had some peculiarity, either of grammatical form or of intonation, that marked the utterance as a question. But now what about the man who says: "I take it that you are going home'. Is he asking a question? Here the grammatical form is plainly indicative and not interrogative; and his utterance of it can be as flat as you like. A computing machine programmed only to distinguish questions by their form would be foxed here. Yet it would make perfectly good sense for you to treat it as a question and reply: "Yes, I'm just on my way', or 'No, I'll be around for a few minutes yet': just as if he had asked the direct qucstion, Are you going home?' In fact, this response of yours not only makes sense but IWHIAT MAKES A QUESTION?

33

it is what would normally be expected of you. I mean, if he were to say: "I take it that you're going home', and you were to reply 'All right; so you take it that I'm going home'-he would not think you were playing the game at all.

AN INCOMPLETE PICTURE

What has he done to you (as distinct from the computer), by making this purely indicative statement, that gives him any right to expect an informative reply? WWhat does his statement have in common with the interrogative form of question to which he is really wanting an answer? Here I think we come to the root of our problem. What he has donc, by making his indicative statement, is to expose to you a certain in- completeness in his picture of the world-an inadequacy in what we might call his 'state of readiness' to interact purposefully with the world around him and specifically with yourself. He is only assuming that you are going home. If he knew that you were going to be about for some time,he would perhaps be ready to call on you if he needed help, ready to leave the lights on in the hall if he were going out, and so forth. If, on the othher hand, he knew you were going home, he would be ready to act quite differently in these various circumstances. It is rather as if he had a whole series of switches in his brain, needing to be set one way if you are going home, and the other way if you are not. His state of readiness is incomplete until these have been set.

It is perhaps hardly necessary to say that the human brain is not as simple as a switchboard, even of the complicated automatic sort you would find in an electronic computer. What goes on in it is far less cut-and-dried, far more spon- taneous and undisciplined, than an engineer could tolerate in a switchboard. In place of the virtual certainty with which a switch operates, the brain cells offer only a certain probability that they will send signals one way rather than another. So if we were going to be accurate we would have to describe a 34 CHAPTER 4

man's state of readiness in terms of a large number of what the theorist calls conditional probabilities-- the probabilities that if he wanted to do such and such, in given circumstances, he would set about it thus and so.

With this qualification, I think the idea of switch-settings in the brain is not a bad way of picturing the mechanisms that embody our 'states of readiness'. It provides us with a useful metaphorical way of looking at a question, as an opportunity presented to someone else to set some of the switches for the questioner. It is as if the questioner uncovered and held out the incomplete part of his switchboard to the listener, in the hope of having the switches set for him.

AN ESSENTIAL PRESUPPOSITION

This brings out an essential presuppostion behind the whole business: namely, that the exposure of an incomplete or incorrectly set switchboard is normally a stimulus to action on the part of the receiver: that human beings are motivated to set one another's switches; or, in more psychological terms, to adjust one another's states of rcadiness, just as they are motivated to help one another in other ways. Call it, if you like, filling up one another's world map. I do not want now to discuss the reasons for this. We may be moved by the purest wish to be helpful, or by its tiresome twin, the longing to put other people right. Part of what makes us people is our readincss to interact with one another in this way. No doubt one could argue that if we did not have a mechanism of this sort built into us the race would hardly have survived. But that is by the way. The point to note is that we cannot define an utterance to be a question simply on the ground that it has moved someone to adjust the speaker's state of readiness, because people are liable to do this spon- taneously, and may sometimes get no thanks for their pains. Where then does this take us? WWhat we have established is that a question is a combination of an indication and an WHAT MAKES A QUESTION?

35

invitation, which we have likened to the uncovering of a switchboard, whereby the questioner seeks to have some of his switches set for him by the receiver. Instead of passively regarding it, as he might the back of a bus, the recciver reacts to the uncovered switchboard as a target for his ac- tivity. He sets to work to try to alter or to complete the switch- settings that have been displayed to him. He may judge that he has been invited to do this either from the manner of the uncovering or from the circumstances.

The usefulness of this rather long-winded way of expressing common-sense facts is that it has brought us clean away from any necessary reference to grammar or even to language. There are all sorts of wordless methods of displaying an inadcquacy, and plenty of wordless conventions to indicate readiness to have it remcdied, from the extravagances of comcdians in the old days of the silent film, to the discrcetly inquiring lift of an eyebrow. As we have alrcady scen, the mere fact that the speaker has chosen to display the in- adequacy to the receiver may be a sufficient indication that help is being asked. At the mechanical level, I dare say the process has some analogy with the way a mother bird's reactions are stimulated by a gaping beak in the nest-the big difference being that our responses have to be learned.

LOOKING FOR A DEFINITION

Suppose we try in this context to define the mcaning of a question. I have suggested in the previous talk that the meaning of an indicative sentence to a receiver might be defined in terms of the state of readiness it sets up; or, more precisely, as its selective function on the range of the receiver's possible states of readiness for goal-directed activity. For short, I suggest we call this its organizing function. Thus the sentence 'It is raining' selects in you a whole complex state of readiness to take umbrella or mackintosh if you go out, to shut a window if you see it wide open, and so forth. 36 CHAPTER 4

We can picture this effect as the setting of a whole series of the brain-switches we have been talking about, which govern what you are likely to do in all relevant circumstances. You may notice that we are not defining the meaning as the change produced in you, but as a relation between the utterance and yourself, which we have called its organizing function. Meaning is always meaning to someone.

The main purpose of a question is to bring about, by remote control as it were, a change in the questioner's own state of readiness. He is trying to get some of his switches set for him. The primary meaning of a question, then, which we might call its interrogative meaning, can be defined as its selective function on the range of the questioner's states of readiness for purposeful activity, or, for short, its organizing function for the questioner. Its job is to identify the switches that need setting. The meaning of the answer will be a selective function on the same range but a more detailed one. Its job is to set the switches.

On the other hand, as we have seen, a question also plays an indicative role, by simply showing the recciver the state of the questioner's switchboard. We might thercfore define the indicative mcaning of a question as its organizing function on the receiver's readiness for the statc of the questioner's switchboard. One further distinction we must obviously make is between the organizing function actually exercised in cach case — the effective meaning- and that which was intended by the questioner.

CRITERIA OF MEANINGLESSNESS

All this leads up to a topic of fierce debate among philoso- phers nowadays: When is a question meaningless? Some people would argue that a question is meaningless unless one has some physical way of verifying the answer to it. For them, the whole of metaphysics and theology are worthless on this score, and questions of the kind 'Does God exist?' WHAT MAKES A QUESTION?

37

can simply be ignored. At the other extreme are those who would admit any qucstion to be meaningful if people in fact ask it.

Our own first answer has to be that a qucstion is mcaninglcss when it has no organizing function. But we must go on to distinguish again between interrogative and indicative meaning. Interrogatively, a question is meaningless when it calls for no organizing operation. Indicatively, it is meaning- less when it has none. We can also distinguish in obvious ways between meaninglessness to the receiver and to the questioner. As a basic criterion of meaninglessncss, this absence of organizing function' is I think a good dcal more realistic than either of the cxtremes I have mentioncd. On the one hand, it rulcs out questions whose components have either no selective function or mutually incompatible selective functions, whether or not people have been accus- tomed to asking them. On the other hand, it gives no excuse to stifle any metaphysical or theological questions that have a bcaring, however remote, on experience or action.

Thus to ask: 'IWhere does the flame go when the gas is turned off?' is interrogatively meaningless as it stands, because if we assume that 'flame' means 'gas being burncd', the two halves of the qucstion contradict one another: they call for mutually incompatible selective functions. When there is no gas, there is no flame to go anywhere. But it is not indicatively meaningless, because its uttcrance docs convey a picture of the questioner's muddled switchboard.

On the other hand, questions of the kind: 'Does God exist?' may well seem indicatively meaningless to a non-religious person who has no mcans of knowing what kind of inadequacy, if any, they betoken. Yet, inasmuch as the qucstioner's whole apparatus of motives and conduct-not to mention his experience-can depend radically on the answer, such qucstions can scarccly be termed interrogatively mcaningless. Their answers, whether true or false, are going to affect switchboard-settings for the whole of his life. 38 CHAPTER 4

There is, however, one kind of nonsense-question that might seem to slip through our net. I mean the sort of question that is asked and answered only in terms of an artificial language with no relation to reality-a kind of game without meaning. Here one might argue that the questions ought still to be called meaningful, because they do have a bearing on activity of a kind-namely the activity of talking the artificial language. To avoid a wrangle, I would be prepared to concede this, but on condition that where the only readinesses affected by talking a language are readinesses to talk more of the same language, it should be termed only artificially meaningful. I think it was a horror of this kind of artificial, empty meaning that led some people to try to define sen- tences as meaningless unless they admitted of physical verification. But I hope I have shown that such Procrustean measures are not necessary in order to have a working idea of what makes a meaningful question. Part II

Information, Communication and Meaning CHAPTER 5

In Search of Basic Symbols"

FOREWORD

"Information is as information does"- such is the watchword of the operational theory of information. Where it selects or constructs tangible representations, information is easy to measure, at least in principle. But what happens when information is absorbed by a human recipient? Can we think of analogous selectice or constructice processes going on inside his brain? If so, what might we suppose to be the elements-the basic symbolic alphabet, so to speak-upon which such operations could take place?

These were the main questions intended to be raised by an informal talk under the above title, portions of which are here reproduced more or less cerbatim from the proceedings of the 1951 Josiah Macy Jr. Foundation conference on Cybernetics. These enjoyable occasions were noted for their rumbustiousness, and as it turned out a good deal of time had to be devoted to explaining and arguing the need

for different but complementary measures of information-content; so the semantic aspects had to be crowded into an inadequate few minutes at the end. Although the extracts that follow give only a sketchy indication of what was in mind, they may help to show how a formalism originally deceloped to represent the information derived from a scientific measurement led to exploratory questions in a more general context.

*Proc. 8th Conf. on Cybernetics (H. von Focrster, ed.) Josiah Macy Jr. Foundation, Ncw York, 1951，181-221. 42

CHAPTER 5

General information theory is concerned with the problem of measuring changes in knowledge. Its key is the fact that we can represent what we know by means of pictures, logical statements, symbolic models, or what you will. IWhen we receive information, it causes a change in the symbolic picture, or represenlation, that we could usc to depict what we know.

We shall want to keep in mind this notion of a represcnta- tion, which is a crucial one. Indeed, the subjcct matter of general information theory could be said to be the making of representations-the different ways in which representations can be produced, and the numerics both of the production processcs and of the represcntations themselves.

By throwing our spotlight on this representational activity, we find ourselvcs able to formulate definitions of the ccntral notions of information thcory which are opcrational, with more resultant advantages than just current respcctability. In any question or debate about "amount of information", we have simply to ask, "What representational activity are we talking about, and what numerical parametcr is in question?" and we eliminate most of the ground for alterca- tions, or we ought to do so if we arc careful cnough!

Our first concern must be to make enough distinctions and provide ourselves with an adequate enough vocabulary to avoid major trouble.*

Representations commonly originate in two distinct ways. The diffcrence betwecn these is the essence of one of the most important distinctions in information theory-between the theory of communication on the one hand and what for want of a better terin we may call the theory of scientific information on the other. Both a communication-process and a scientific observation-process result in the appcarance of a representation in the "reprcsentation-space" of the recciver or obscrver. But what distinguishes communication, I suggest, is the fact that the representation produced is (or purports to be) a replica of a representation already present to (with, in-the-mind-of) the sender. Communication is the activity of replicaling representations.

An explanatory survey of some key terms of information theory (as of 1950)is reprinted as an Appendix. IN SEARCHI OF BASIC SY.MBOLS

43

This is to be contrasted with the typical activity of physical scientific observation of which the goal is the making of a new reprcsention, repre- senting some additional knowledge of that-which-is-physically-the-case concerning some uniquc spacc-time tract not heretofore represented anywhere.

We might put it crudcly as the distinction between the replication and the formulation of knowledge. The problems raised in the two cascs are in some respects quite different and give risc (as we saw in Chapter 2)to different"measures ofinformation".

Now it is evident that in any situation in which what is observed is thought of as specifying one out of an ensemble of preconceived possibilities, the amount of selective in- formation so specified can in principle be computed (see Appendix). Shannon's concept has, therefore, a much wider domain of usefulness than that of communication theory. The point is that it is always a relevant parameter of a commu- nication-process, because successful communication depends on symbols having significance for the receiver, and hence on their being already in some sense prefabricated for him. The practical difficulty, of course, is to estimate the pro- portions of the appropriate cnsemble, when these are de- termined by subjectively and even unconsciously assessed probabilities.

SCIENTIFIC INFORMATION

But now let us turn to this other problem which faces the physicist: namely, making a represention of that-which-is- physically-the-case concerning some tract of spacc-time. This I have discussed at length elsewhere (sce Chapter 1 and Appendix), and I want here only to outline the kind of formalism which is useful to rcprescnt the processes conccrned.

In this case, we are not usually in a position to selcct from a filing-cabinet of preformed representations; we have to produce our representations ab initio. Our scientific representa- tion is in general compounded of elements portraying certain relations, say between the magnitudc of a voltage and a particular point on a time axis, or between the intensity of transmitted light and a particular coordinate-intersection in 44 CHAPTER 5

the field of view of a microscope. We say "the voltage was 10 volts at time t1, 10.5 at L2"and so forth.

Our ability to name operationally a ccrtain number of distinct coordinate values, such as t and l2, cnables us to prepare in advance the samc number of distinguishable, independent "blank statements" of the form: "The magni- tude had the value such-and-such at coordinate-point gn"or, rather, "The magnitude had the average value such-and-such over the coordinate-interval Ag around g", and so on. The blanks in these statements or "propositional functions" we then fill in as a result of our obscrvations.

We are thus clearly faced wıth a two-fold problem: First, we must be able to define distinguishably in operational terims the blank statements which we want to prepare. In other words, something in the design of the experimental apparatus or procedure must enable us to identify and distinguish between observations if we want to call these observations "independent"or even "distinct".

Second, we must collect evidence for our statements by ob- servation of events. We"plug in" obscrved data, so to speak, into the blank spaces which we have for them in our pre- viously prepared propositional structure. If we boil a typical statement down to the over-simple form "value X relates to interval y", then our two problems are the operational definition of Y and the collection of ecidence for X.

Now a set of independent propositions can be represented or symbolized by a set of perpendicular axes in a multi- dimensional hyperspace. So we can represent the additive process by which information accumulates with the help of a convenient geometrical vector-model, in which for each new independent proposition we add one dimension to our hyperspace-our "information-space". We then can take distance in each of those dimensions to represent some function of the amount of metrical information (see Chapter 1 and Appendix) associated with the corresponding proposition. IN SEARCIH OF BASIC SYMBOLS

45

If each structural proposition is represented by a vector whose length is the square root of its metrical information- content, then the total information-content, structural and metrical, is represented by the vector sun of the individual components.

For example, if we had just two propositions, we could define their total information-content by drawing a singlc vector whose two perpendicular components are the square roots of the amount of metrical information in each. In the particular case of voltage measurcment, the two propositions concern two successive independent readings, and these vector-components are actually proportional to the signal- noise voltage ratio. In that case, of course, the squarc of the length of the resultant is the sum of the squares of the lengths of its individual components, and is proportional to the total energy, so we get a representation in which additivity is preserved.*

COMMUNICATION

If now we had to communicate a representation like this to somebody elsc, we could think of our activity asinstructing him to selcct, out of a certain number of possible positions for the information vector, one representing the result that we have obtaincd. The tip of the vector can be reprcsented as occupy- ing one of a number of cells into which the space is divided or quantized. In that case (on the assumption that each position is equally probable for the sake of argument), we can take the logarithm (base 2)of the number of possible positions out of which our result has selected one, as a measure, first, of the number of binary dccisions to which this selcction is equivalent and, hence, as a measurc of the amount of information in Shannon's sense, which you remcmber we distinguished by calling it the selective information-content.

This assumes a constant " noise" level per degree of frecdom. The case where the noise level is different for different degrecs of frecdon requires an cxtension to the formalism which was never undertaken. 46

CHAPTER 5

In communication betwccn human bcings, and possibly betwecn animals, the problem is ultimatcly the production in one reasoning-mechanism of a representation-a pattern -already present in another reasoning-mechanism. In the human case the communication enginecr is intcrestcd cs- pecially in the most economical way in which we could transmit the selective operation that cvokes the appropriate pattern; and, since we can do this by coding, we are always prepared in principle to take the logarithm of the total number of cquiprobable possibilities as our mcasure of the "amount of information" given, irrespcctive of the properties of the pattern signified.

In the other process, the proccss of scicntific observation in which we arc confronted by a situation about which wc are initially wordlcss, our expcrimcntal method-our mode of approaching the situation-has to provide us with both(a) the conceptual possibility of formulating -giving distinguish- able significancc to-a certain number of propositions, and (b), as a result of observing events, the ability to adduce evidence for these propositions.

MEANING

Now, what about the concept of mcaning? Supposc we forget for the moment about signals, which are very oftcn symbols for something else, and just take the casc of two propositions. In ordinary mathematical logic, one could say that, if you assert two indcpendent propositions A and B, you have said something which is equivalent to the logical combination of these two, which could be symbolized, there- fore, as a point in a diagram with four possible positions (Fig. 1). In position 1, you have said both. In position 2, you say "A" but not"B"; and so on. So the statement you make could be defined by a vector, the vector linking these points to the origin, which has four possible quantal positions. Now it is common experience that we do not fully define IN SEARCH OF BASIC SYMBOLS

47

2

1

A

4

Fig. 1. A vectorial representation of the four possible conjunctions of two

independent all-or-nothing propositions A and B

many of our concepts in terms of a set of discrcte, yes-or-no propositions. The concept of a chair is not definable simply by enumerating a certain number of characteristics, because we all know that if a chair doesn't have a lcg, we may still judge that it is a chair which has lost its leg, or something like that. I bclieve that according to some linguistic philoso- phers the most you can do is to cnumerate a sct of possible charactcristics of chairs, of which any adcquate sub-selcction constitutes a chair where found. What we need, it seems, is some way of symbolizing the partial participation of onc or more characteristics in a definition. The black-and-white of atomic, yes-or-no components is too coarse for our everyday terms.

PARTIAL PARTICIPATION

Can we then sharpen-up this notion of "partial participa- tion"? What could we mean by saying that a certain term means "a little of A and a lot of B", instcad of acccpting the four-way choice offcred to us by conventional logic in Fig. 1? Suppose we try to say that the mcaning of a term represents, not a discrete selection from a set of "yes-or-no"characteris- tics, but a selection of each in a certain proportion; what reason- able meaning could we give to that?

What we could mean, I suggest, is that our definitions are to some extent ostensive-that their meaning is acquired 48 CHAPTER 5

from expericnce. In the past over which a given term has acquired certain associations to which we point implicitly or cxplicitly when we usc it, we imay have found that 1 was associated only 10 times, say, and B 100 times, so that the term means in this scnsc "a littlc of A and a lot of B". If you likc to picture the clementary characteristics as spread out along a scalc, the meaning of a term bccomes a kind of spectrum— a spectral distribution — over the scale, the relative frequencics of occurrencc of the diffcrent elements being symbolized by the height or intensity of the spcctrum over the corresponding points on the scale.

I wonder if I am making that clear? The idca is that if you make a list of featurcs of chairs: having Icgs, having backs, and what not; then some chairs arc backless, some chairs have no legs, and so on. So if we acccpt thesc(for the sake of argument) as simple"yes-or-no"characters, then over a long expcricnce of the word "chair" we should build up a concept of "chairfulncss", which could be defincd by the proportions of diffcrent characters in the ensemble of all chairs experienced.

The interesting thing is that this possibility would corres- pond in our vector-modcl(Fig. 1) to attributing significance to all orientations of the vector. Instead of having merely the possibility that the vector is vertical, horizontal, or inclined at 45 degrecs, we now have the possibility of conceptually infinitcsimal gradations of orientation. Quite preciscly, what corresponds to the meaning of a given term which is dcfinable in terms of this space of basic vectors (clementary componcnt characters)is the orientation of its represcntative vector-thhc direction which defines the relative weights with which those clementary components enter into our experience-based undcrstanding of the term.

It is possible, of course, to use different metrics herc. Wc could arrangc that as the probability of inclusion gocs from 0 to 1，so length only goes from 0 to 1，as in quantum theory. But if we are dcaling in tcrms of metrical information we IN SEARCH OF BASIC SYMBOLS

49

make no restriction, and the length could go to infinity(which would be cquivalent to an infinite weight of evidence).

The choice of metric for our purpose is not particularly important. The point is that with a given metric we can have a precise representation of the meaning of a statement for a giren individual, remembering that each individual receiver will have his basic vectors defined by his own internal apparatus. Different shades of meaning are represented by diffcrent orientations within the same subspace. The relevance of evidence to a dependent statement is represented quite precisely by the square of the cosine of the angle between the two corresponding directions in information-space, in that the weight of evidencc afforded to a dependent statement by a given body of information is found by squaring the projcction of the information-vector on thhe ray which dcfines the statcment. THIE RECEIVER'S INTERNAL REPRESENTATION OF

INFORMATION

Pcrhaps I can best introduce the question of the receiver's internal representation of information by prescnting to you the bare bones of a possilblc general-purpose reasoning mechanism,11.14 which we want to be capable not only of dealing in black-and-white logic, but also capable of receiving and representing and rcacting appropriately to the kind of information we have been talking about-information in the general sense. Essentially, this is a probabilistic mcchanism, in which "trains of thought"(metaphorically spcaking) correspond to transformations of information-vcctors which may be continuous or discrete.

The main things we are going to nced are, first, some means of symbolizing probalility, of representing probability appropriately in our mcchanism; and, second, some way of representing the basic vectors or dimensions of information- space: the clcmentary components, the basic symbols, out of which such a mechanism could build its representation of a universe of discourse. 50

CILAPTER 5

It will be easiest I think to Icave the probabilistic question to the last, and consider first how the computing machinery of an organism reacting with its cnvironment might derive its internal "dcscriptive alphabet" of elementary symbols. As I sce it, we have a basic choice betwecn (a) the use of the incoming stimuli or filtratcs thereof, and (b) the usc of the elementary acts of internal response to reccived stimuli, as symbolic components for the internal reprcsentation of what is "perccived". So this is our first question: Docs one's internal represcntational mechanism describe an ostcnsively defined concept as cffectively "so much of this received stimulus and so much of that received stimulus"? Or are the clementary symbols going to be derived from the repcrtoire of internal responses evoked by the ostensive process?

For the sake of brcvity, I will jump straight on to suggest a mechanism on the sccond principle, without discussing now the reasons that have led me to favour it in prefercnce to the other.14 Suppose we have a device which rcacts to incoming stimuli by an act of replication. At the very simplest level, let us consider one which has an irritable surface and is designed so' that, if it is excited at a certain point, its rcaction is a hunting motion over the surface with a finger, which eventually elicits a success signal. Call this, if you like, a scratch-response mechanism. It is easy to sce that if this stimulus recurs often enough we can devise a self-adjusting statistical mechanism (sce Chapter 12), which will increase the probability that on the next arrival of such a stimulus the scratch mcchanism will tend to hunt in its ncighbourhood. You can sce that if any particular irritation is a sufficiently consistcnt feature of the flux of incoming stimuli, it can come to clicit the success- ful scratch response by a scries of elcmcntary opcrations between which the transition probabilitics are higher than they would have been originally. It has now evolved somc- thing that can serve as an internal symbol of any movements of the incoming stimulus, namely, the scquence by which these movements are successfully replicated. IN SEARCH OF BASIC SYMBOLS

51

Suppose now that we have several stimuli-say three forming a triangular pattern-and imagine a mechanism whose constant activity is to "doodle" in speculative move- ment from one to the other-in other words, it is built to respond with self-guided attempts to organize a programme of movement from one to the othcr. IVc will equip it with means of determining that it has successfully finished all its scratch- ing. It gocs from one stimulus to another until it gets the indication that it has no more scratching to do. If triangular patterns recur with sufficient frequency in its incoming stimuli, then a process of natural sclection, which I think one can easily envisage, is all we necd invoke in order to make a device that automatically discovers for itself-and internally names-an abstraction. Stimulated by any triangular pattern, the device will find that the same sequence of elcmentary commands to its scratching machinery (go ahead, turn, go ahead, turn, go ahead) is required to produce a satisfactory internal "match"; so that we could think of this sequence as becoming one of the internal representative symbols of the "experience" of this devicc-its name for "triangularity". Out of the welter of all possible combinations, this one has acquired the dignity of a symbol for a "universal", through recurring with sufficient frcquency among the or- ganizers of succcssful responses to the flux of incoming stimuli.

One can go on from this to think of any incoming pattern which is sulficiently recurrent, or which persists for long enough at a given time to evoke internal matching activity, as gaining for itself the status of a "universal" in the world of discourse of such a device. What we have been doing is to go behind the problem of devising a mechanism for deductice reasoning, which we can takc for granted well enough, to the problem of transforming the information carried by incoming scnsory stimuli into a symbolic linguistic form suitable for such a mechanism, which takes us to the problem of inductice reasoning. Our typical problem is this: how can we ensure that a mechanism presented with, say, a triangle in the 52 CHAPTER 5

field of its optical receptors can always make calculations appropriate to the presence of (i.e. act as if recognizing) triangularity, irrespective of size, shape, or oricntation? What I have bcen describing is one possiblc way of solving the problem which in detail is hardly realistic as a model of human brain mechanisms; but it illustrates a principle which I think we should not neglect: the representation of a particu- lar universal by a compresence and/or a sequence of the elementary internal acts involved in responding adaptively to it.

PROBABILISTIC ASPECTS

Now we come to the probabilistic aspect. These elementary components will not always recur in association in cqual proportions. A complex universal therefore becomes defined not by simply enumerating the internal acts which participate in its symbolization, but by cnumerating those plus the relative frequencies with which they have been involved. And here, of course, our information-space comes into its own; because what we have done, in effect, is to define our universal by a vector in a space which is not quantal (at this macro- scopic Ievel at any rate), but has the possibility of representing practically continuous gradations or shadcs of meaning. The mcaning of this universal is defined by the orienlation of the information vector-by the statistical spectrum, if you like-over the elementary acts of rcsponsc which cxemplars of this universal have evoked in the organism in the past.

Questions now arise thick and fast. Clcarly, this just takes us past the first step. We havc discussed an artificial organism which can recognize pattern in the flux of incoming stimuli-which can abstract from among its received data those relationships whosc rccurrence or invariance gives them the status of universals. The next step is to consider the possibility of recognizing pattern in the flux of perceived universals-of abstracting from among the evoked acts of IN SEARCII OF BASIC SYAIBOLS

53

symbolic response those higher-ordcr relationships whose rccur- rence or invariance gives them also the status of universals.

This, I think, is the essence of the making of hypotheses-to predicate pattern of a group of abstractions. Can an artificial organism spontancously formulate useful hypotheses? I think it can, certainly in the sense that we can devise a second-order probabilistic mechanism, analogous to our first, but one in which each individual basic symbol now represents a pattern of first-order symbols. It is evident that we have here the possibility of a hierarchy of abstraction; and indeed this hierarchy itsclf could in turn become the subject of internal discourse; but perhaps I have said enough to indicate the possibilities. To summarize: our device, working probabilistically, makes its abstractions by a process of natural selection of matching rcsponses. It chooses a means of (internal) response which is invariant with respect to the transformations that leave the abstraction invariant, by a self-guiding proccss in which the statistical configuration for each attempt is dependent upon the succcss of the last. Expcrience elevates the statistical status of certain response sequcnces, which can then appcar as elements in the internal logical vocabulary. Performing sccond-ordcr abstractions (as in the formation of hypothescs), or even nth order abstractions, is in principle just a repetition of this process at the next level or at a highcr level.

This kind of approach to the mechanics of reasoning might, I think, find a place for most of the concepts thhat we arrive at from the other direction. Consciousness, for example-if I darc stick my neck out-might be introduced in this way: IWe might say that the point or area "of conscious attcntion" in a field of data is the point or arca under active internal symbolic replication, or evocative of internal matching re- sponse. When a man speaks to another man, the meaning of what he says is defined by a spectrum over the elementary acts of internal responsc which can be cvoked in the hearer. If the hcarer is such that when the speaker raiscs his eyebrows, something inside the hearer happens which corresponds to 54

CHAPTER 5

imitation-the internal initiation of part of the scquence that would normally lead to the raising of eyebrows, and so on-then, clearly, the meaning of what the speaker says can be fully representcd only in terms of the full basic-symbol complex defined by all the elementary responses evoked. These may include visceral responses and hormonal secretions and what have you. So, along these lines, I think one would say that an organism probably includcs in its clementary conceptual alphabet (its catalogue of basic symbols) all the elementary internal acts of rcsponse to the environment which have acquired a sufficiently high probabilistic status, and not merely those for which verbal projections have been found. Without here going into further detail, I should pcrhaps point out that many human charactcristics such as bias, prejudice, preference and the like would have obvious analogues in such a mechanism, in the shape of altcrations of the thresholds of excitation or, if you like, distortion of the probability amplitudes, associated with the basic vector components affected by the "bias".

Indeed, along these lines, I think one could go a long way towards simulating what appears to be the ordinary conscious behaviour of human beings. On the other hand, if one were to ask whether such a mechanism could ever be built, I would take refuge for the moment in the blesscd phrase "in principle", and say that in principle I sce no rcason why it shouldn't. But I would not myself be surprised, were one to attempt to devise a probabilistic mcchanism with the same mobility and other capacitics as homo sapiens, if one would have to go in for mechanisms in protoplasm instead of mechanisms in copper. That secms to me to be one implication of some of the very neat tricks that we find in the central nervous system. POSTSCRIP

The emphasis above on spontaneous activity may need some com- ment. In the formalism of wave mechanics the notion of probability IN SEARCH OF BASIC SYMBOLS

55

(of a single erent) shades ocer into that of frequency (of spontancous occurrence of events) at ligh wave amplitudes. Thus spontaneous activity can be thought of as the limiting case of increasing probability of activity- as, for example, in a neurone whose threshold is steadily lowered. The suggestion was not that the mechanism should operate on a purely random basis (like proverbial monkeys on a typewriter), but rather that the statistical pallern of its explorations should reflect the"metrical" aspect of the available information. An important feature of such a mechanism would be its ability, unlike Buridan's ass, to act in the absence of adequate information; but any acailable information of high metron-content would of course be fully used in shaping its exploratory activity.

What I wanted to stress was the readiness with which a spon- taneously active mechanism on these lines could evolve categories of description beyond those built into its design, in response to redundancy in the pattern of demand from the encironment.

The passing reference to"conscious awareness"I would now want to extend and qualify in several respects (see, for example, Ref. 25)； but the essential suggestion stands, that the correlate of awareness should be sought in an internal adaptive matching response, rather than in the mere arrival of sensory stimulation at a particular internal point. CHAPTER 6

Operational Aspects of Some Fundamental

Concepts of Human Communication"

In cveryday language we arc accustomed to spcak of the mcaning and the relecance of information. In the statistical thcory of communication,t31 on the other hand, no such concepts appcar. Indccd its founders have very propcrly insisted that the "amount of information" (or, bettcr, the sclective information-content) of a signal, as thcy definc it, bears no direct relation to the scmantic function of thhc signal.

From its inception, naturally, the theory has been plagued by qucstions of the rclationship of its concepts to those normally associated with the term information. Where do concepts like mcaning fit into the picture? Or is it that the concept of information which the comrnunication engincer has in mind is a quite different one from the concept of the scnanticists?

The trouble here appears to be duc largcly to a confusion of the concept of information with that of information-content- the confusion of a ting with a measure of a thing. Communication cngincers have not dcveloped a concept of information at all. A papcr given at the 9th Intcrnational Conference on Significs, Amersfoort (Netherlands), 1953. First published in Synthese, 9，1954，pp. 182-98.

t Referred to by some as Iuformation Theory, but never so by Shannon, its chief originator. Information Theory logically cmbraces a much wider ficld. ASPECTS OF HUMAN COMMUNICATION

57

They have developed a theory dealing explicitly with only one particular featurc or aspect of messages ""carrying"informa- tion-thcir uncxpectedncss or surprisc valuc. Unexpccted- ncss is a feature not only of messages but of othcr things, such as the states of a physical system, as well. Physicists had already devcloped a quantitative method of measuring unexpectedncss by Boltzmann's statistical concept of entropy. IWhat Shannon and others did was to adapt and cxtend this method to the measurcment of the unexpectedness of messages. Their measure of unexpectedncss, the average logarithm of the improbability of the mcssage, -Σp, logPi, is not thercfore information but simply a particular mcasure of what they termed amount-of-information: (i.c.)the minuteness of the selection which the message makes from the sct or "ensemble" of all possible messages.*

Semanticists on the other hand are concerned with different features of information, such as its logical complexity and its meaning. But both engineers and semanticists have in mind the same concept of information, in the sense that we can find one definition of the term which will cover all its uses. Both mean by information that which promotes or validates representational activity (activity from which it is possible to infer something about some other state of affairs). Both are entitled to regard the function of information as to be selective: to prescribe choice or decision. The cngincer sceks to define a suitable measure of the uncxpcctcdncss or in- frequency of the choicc, and calls his measure the selective information-content. The semanticist may seek to define suitable measurcs of the logical complexity of the represen- tational activity evoked, and is also cntitled to call these "measures of information-content", in various complementary In this ensenble the different possiblc messages are pictured as occupying space proportional to their relative probabilities, so that the least-probable message occupies the smallest space and requires the most minute selective operation. But the technicalities do not here concern us. 58 CHAPTER 6

senses. It is a mere solecism, howwever, to regard the concept of information itself as identical to any of these measures; to do so, besides being grammatically absurd, leads inevitably to debate over spurious paradoxes, which it is part of our present aim to resolve.

So much then for clearing the ground. The view I have offered is that while the connection between statistical and semantic features of information cannot but be indirect, thesc are features of one and the same central concept, which admits of a single universally applicable operational definition. Our aim must now be to elucidate the conncction by exploring the basis of this operational definition.

On what does information operate? Ultimatcly, we say, "on the receiver's mind". At once we are ncrvous of losing ourselves-and our respcctability! -in a morass of sub- jective terminology. Cannot we put it differently? Cannot we find an objective description in "observer-language" of what goes on when a man receives information? If we could, then it might be possible to form a coherent picture of the whole process of communication, in which concepts like selective information-content and concepts like meaning would both find a place, and be seen in their proper relationship.

Here I can attcmpt only an outline of the possibilities, amounting to little more than a programme. It may however suffice to indicate morc clearly the scope-and the degree of overlap-of the concepts used in the tivo fields.

THE SUBJECTIVE ASPECT

Our first precaution must be to distinguish clearly between the two complementary languages in which we may describe an activity like gaining information. There is first (a)the private actor-language in which I as actor describe what I mean by my knowing something; secondly(6) there is the public observer-language in which we might hope that a super-mcchanic of the brain could describe what goes on in the human organism as the correlate of my actor-account. ASPECTS OF HUMAN COMMUNICATION

59

There scems to be no good rcason to miss any clucs we can gain from the use of words from both languages, provided we avoid the common pitfall of careless mixing of the two. As far as possible we shall carry on our discussion in discrctc stagcs, cach consistently using one language or thc othcr. It will be fruitful to devclop the two dcscriptions in parallcl, since each can be suggestive of qucstions to be explorcd in the other. On the other hand, we shall be wise not to prcsume the existence of any simple one-to-one correspondencc, but to treat what correspondence we find as permissive rather than confirmatory.

Lct us then begin in subjcctive actor-language, whcre our fecling for the notion of information is clearcst and our thinking pcrhaps woollicst. I normally say I have gained information when I know something now that I didn't know beforc: when what I know has changed.

How much morc inforimation do I gain from onc statemcnt, or expcriment, than from another? I might be ablc to answer this qucstion quantitatively if I could measure the corresponding changes in what I know. I get more information from that which makcs a biggcr change in what I know.

How could we hope to measurc-or even to define quantitativcly- changes in what I know? Could we perhaps count the minimum nunber of indcpendent simple sentences in which I could describe the change? If our sentences wcre all indepcndent, ideal, "atomic" scntences in the logician's sense, this might do for onc kind of mcasurc. But the difficult problem is not so much t definc appropriate incasurcs when we are given the idcal language, but to discipline real language into a forin sufficicntly 'atomic" for our purposc.

Scicntific language is one of the few that lend of themsclves readily to such disciplinc, and in an carly paper12 the author suggestcd definitions of two complementary mcasurcs of the "scmantic information content" of scicntific statcincnts, based on their appcal to the inherently quantal processcs of mcasurement and verification. In the vector-represcntation suggested in that papcr, the meaning and relerance of scicntific information had espccially siniplc gcomctrical corrclates. But scicntific language is too casily quantified to be typical; and although the work was catalytic in the development of the present linc of approach, no familiarity with it is ncccssary in what follows.*

It may also be mentioned that the author's work on semantic measures of scientific information, first described in a lecture in January 1948,was initiated some ycars before the publication of Shannon's papers and is concerned to answer quite different qucstions from a diffcrent starting-point. Misunderstanding has somctimes arisen from attempts to sce it as an application or extension of communication thcory. The rclation of the two has been discussed in an earlier paper. (Sce Appendix). 60

CHAPTER 6

For we are here concerned witli information in gencral; and normal human language is notoriously different from the ideal of the scientist or the logician. Am I sure, morcover, that I can always fully describe all changes in my state of knowledge in sentcnces, or indeed in any objcctive symbolisation? Is what I know limited to what I can describe? For a starting-point that begs no such questions we must move a stage farther back. THIE OPERATIONAL EFFECT OF INFORMATION

Let us do so by asking in more gencral, opcrational terms what differencc it makes when I gain information. Iunda- mentally it implies that in some circurnstance or other my expectations will be different. I am now conditionally ready to react differently. The reactions potentially affected may be internal or cxternal. They may themselvcs take the form of choiccs from among a number of possiblc latcr statcs of readi- ness to react, choices which will now be diffcrent as a result of my gaining information. It is the hicrarchy of such readincsses -my total state of readincss for adaptivc or goal-directed activity-which changes when I gain information. Informa- tion in fact could be dcfined in actor-language as that which alters my total state of adaptive readincss in this scusc.

If I were a simplc sort of being with only a clcar-cut set of independent states of rcadincss (analogous to the states of readiness represented by the possible settings of independent levcrs in a railway signal-box), then it would be possible in principlc to measurc the amount of inforination I receive in terms of the number of clcmentary decisions (analogous to the number of changes in lever-scttings)cvoked in responsc to it. As we shall scc later, some sort of cquivalent measurc can be defincd for the much more complex type of organism that we appear to be.

In parenthescs at this point it may be wise to guard against a possible pitfall. Our language might suggest that we picturc my gaining information in actor-language as a two-stage activity: first my conscious receipt of information, then my ASPECTS OF HUMAN COMMUNICATION

61

response to it. This however would be a misinterpretation. Our suggestion is that the act of perception is constituted by the act of succcssful internal adaptive responsc, not that it evokes it as a sequel.

It is not denicd that in observer-language we can distinguish two stages. Of all the objccts in the field of vision, for example, only a few are normally perceived at any onc time-those that have "caught the attention" as we say. Stimuli corrc- sponding to the prescnce of the others arc receited; but they evoke no"matching-response"1+.15 in the organism-at least nonc structured to correspond to the individual objccts. These objccts are not perccived.

Our suggestion is simply that of the two stages that can be described in observcr-language, only the second finds a corrclate in actor-language: in effect, that the activity of knowing is an activity of (internal) adaptive response.

It is sometimes suggested that the activity of knowing amounts to the gradual construction of a mental model of the external world. Information might then be defincd as that which adds something to our model, either introducing new features or incrcasing our confidencc in the old.

There is a sense in which this description is defensible. Our suggestion however will be that what is internally imitated is not a static structure of relations betwcen things, so much as the dynamic structurc of relations betwecn events. Events of perception are what we know primarily, and what is organised as we rcccive information is our conditional rcadincss to match the pattern of evcnts of perception by the pattern of our own internal or cxternal reaction. The basic symbols in which our "model" of the world could most cconomically be described would stand, not for objects in the world, but for characteristic patterns in the events of perception. These events themselves, be it remembered, we have taken to be acts of internal adaptive response.

In the concept of the total state of readiness we have a possible bridge betveen actor- and observer-language. We 62

CHAPTER 6

must first remark that our state of readiness differs from that of a signal-box primarily in that it docs not prescribe all our reactions uniquely. In many cascs in which our information is incomplete there may be several possible adaptive rcactions equally reasonable on the evidence we have.*

In any event, it would sccm that the closcst correlate of my state of readincss in observer-language is a specification of a stochastic rather than a dcterministic proccss (sce Chapter 5). Of course, a cataloguc of probabilitics and conditional probabilities is not what I nean by my state of readincss. But the latter in theory would presumably reveal itsclf (if only it were sufficiently stationary, which in practicc it is not) through the statistical structurc of my total adaptive rcaction- pattern; and I should not be able to defend a purported description of my total state of readincss which was inconsis- tent with the observed structurc.t

Remembering then that the total rcaction-pattcrn includcs intcrnal as well as external activity, we shall take as the objective correlate of my total statc of rcadiness the matrix of transition-probabiliticsortransition-probability-matrix(t.p.m.) describing statistically the total adaptive rcaction-pattern to all possible configurations of stimuli, intcrnal and cxternal. Our aim is not of coursc to dcfinc this as obsercable. Likc any non-stationary probability, the probabilitics in the t.p.m. can be interpreted only as frcqucncics in an cnscmblc of identical organisms, and not as frequcncies in the timc-scries of a given organism.

We shall sce below that the t.p.n. may have a physical determinant that is in principle perfectly obscrvable; but observability docs not nced to worry us. Our aim is simply to Rctrospectively, it is conventional to find a "cause" for our ultinate choice in such cases, but in many it is doubtful whethrr such phrases as "the whim of the moment"describe a cause or its absence.

t Comparisons of this sort are of course what we use to detcct hypocrisy, the non-stationary character of the state of readiness and the absence of data on internal activity being ignored to the detriment of justice as well as charity! ASPECTS OF HUMAN COMMUNICATION

63

dcfine conceptually an objective correlate of the subjcctive notion of my state of readiness in tcrms of which we have so far defined the concept of information. Our suggestion is that by discussing the cffect of information on the t.p.m., we can find a place for all the concepts clustering round the notion of information in both communication thcory and scmantics- at least for thcir corrclates in obscrver-language, which is perhaps as much as an objective thcory can hope to do.

It will be helpful to begin by summarising the evidence for the statistical picture of the ultimatc receiver of information, in terms of which we shall frame our definitions.

THE CENTRAL NERVOUS SYSTEM

The central nervous systcm is a coinnunity of sonc 1010 clectrically sensitive cells and their fibrous"processes", linked on the one hand with effcctor organs (limbs, glands, ctc.)which have fields of activity both external and intcrnal, and on the other with receptor organs (eyes, muscle-spindles, ctc.)both external and internal.

A typical cell can be"cxcitcd" to send an clectrical impulse down onc of its efferent fibres as a result of electrical and/or chemical changes in its neighbourhood. The sizc of the impulse is substantially independent of the naturc of the change that evoked it. The readiness with which cells can be excited may be increascd or decreased by:

(a)general factors governing the metabolism of most or all the population;

(b)specific agents rendering some group of cells more and others less active or sensitive;

(c)electrical and chemical activity in thhe ncighbourhood insufficient in itself to excite impulses;

(d) changes in geometry of the system such as growth in the length or diamctcr of fibres, constriction of blood vessels, and the like.

It cannot be too strongly stressed that a description of the system is not complcted by saying which cclls arc "wired"to 64 CHAPTER 6

which, and which cclls arc active at a given instant; nor is the number of degrecs of firccdom of the systcm detcrmined by counting the number of cclls. It is true that cach ccll must be in onc of two states: excited or unexcited; but many cclls have dozens or hundreds of fibrous proccsscs raniifying over an cffective volumc much greatcr than that of the cell body, and each making perhaps hundreds of approachcs within critical distance of other fibres and cell bodics. The readiness with which the cell can be excited is a continuously-variable parametcr-or a number of paramcters-depending among othcr things on thc geometry of the wholc rainification and its chemical state. The delay in rcsponsc (of the ordcr of 1 inilli- sccond) is yet another variable of importance (sce below). The total number of degrecs of frecdom inay thercfore avcrage out at many more than one per cell.*

As sotne small consolation for the would-be modcl-nakcr, large groups of cclls often appcar to be so interlocked as to func- tion as co-opcrativc units. Thc effcctive number of funclional degrecs of frecdorn is therefore probably many orders of magni- tude smaller than the dimensionality of the total description.

Sonc cclls arc spontancously active. Others are highly resistant to stimulation, requiring many impulscs to con- verge on them simultancously before they will "firc". IVe express this by saying that the "height of the threshold to stimulation" varics from onc cell to another. The higher the threshold, the lower the probability that a given inipulse will cxcite the cell. "Effective hcight of threshold"(depcnding on the factors outlined above among others) thus can be thought of as the physical determinant of improbability of excitation. An "effective height of threshold" can be dcfincd separatcly for each fibre converging on a given cell.

The strength of a stimulus is often represented by the repetition frequcncy of a continuous train of impulscs in a * Calculations of the limit to memory capacity on the basis of I unit of information per cell are thus unrcalistic, cven if cells were assuned to be invariable units, which they are not. ASPECTS OF HUMAN COMMUNICATION

65

single fibre. This together with the foregoing evidence gives strong cncouragemcnt to considcr a model of the nervous system in which the significant variablcs arc the threslholds of the various clements, in the general scnse which we have given the term. We should then have the following correlation:

Strong stimulus:

high frequency of impulses

WWeaker stimulus:

lower frequency of impulses

Still weaker stimulus:

corresponding probability of a

single impulse in a given time-

interval

As intensity diminishes, we pass from speaking in terins of frequency of impulses to speaking in terms of the probability of a single impulse, in the same way as we do in the photon- description of the intensity of light. The parallel is suggestive, but need not detain us now.

There are any number of potential models in electronic "relaxation oscillators"which (given the presence of a finite random noise level) show the same smooth transition as their applied bias is reduced.

Four phenomena should be mentioned which may have relevancc to the problems of short-term and/or long-term memory: the first is that of adaptation, whereby the threshold in many cases rises with time (the frequency drops) if the stimulus is maintaincd. It normally recovers aftcr a short time. The second is that of facilitation, whereby the transfer of a signal at a given point from one cell to another may increase the sensitivity (lowcr the threshold) to excitation there at a later timc.

The third which might conccivably be rclevant is that of "potentiation". A fibre which has been saturated by excessive stimulation is found to deliver abnormally large impulses for a short time after recovery. These are correspondingly more effective than usual in stimulating other cells.

The fourth is the differential change in diameter of some fibres with usc. It is not known how general this may be, but 66

CHAPTER 6

if it occurs centrally it may have great importancc. The reason is that the specd of transmission in a fibre depends on its diameter. Now the probability of cxcitation of a cell is often critically sensitive to the rclative timing of two or more im- pulses convergent on it. A change of as little as milli- second10 may alter the probability from almost zero to almost unity. The change in temporal relationships with use might well provide us with just the threshold-control mechan- ism required to account for learning and memory.

But we can afford for our present purpose to wait and see. The point is that when we think of the whole system, a popula- tion in continuous electrical and micro-chemical activity, we have abundant evidence for a model in which the proba- bility of transition from one state of excitation to each of the other possible following states can be modified by any num- ber of continuously variable factors in combination, of which perhaps the most flexible and subtle is the pattern of temporal relationships between impulses. Minute changes of delay in transmission (not necessarily through variation in diameter of fibres-see above) can drastically modify the whole structure of the activity of the population. In addition, whole areas can be depressed or activated by general chemical or electrical agents.

THE PHYSICAL REPRESENTATION OF TIIE PERCEIVED

WORLD

Unfortunately we are still probably many years away from undcrstanding properly in these terms what goes on when a man receives information. IWe can follow some signals a little way into his head, but they soon lose themselves in a scurry of activity that we are at a loss to interpret.

But our survey has been some guide as to the kind of model of the process mediating perception that may not be un- rcalistic, and will serve as a peg to which to anchor our later discussion. For our limited purpose we can ignore much of the detail that is obscure. ASPECTS OF HUMAN COMMUNICATION

67

The essential notion around which we shall build our concept of perceptual activity is that of adaptive or matching- response. Any mechanism such as we have described, sub- jected to a flow of signals through its rcceptors, is likcly to be stimulated to all kinds of internal or external activity. What then particularly characteriscs activity that we shall call adaptive? How do we distinguish adaptive response from evokcd activity in general? Here we can give only a summary answer. The question has been much discussed, and the author has dealt with it in detail in Refs. 14 and 15. The basic requirements are two:

(a)In the organism there should be one or more evaluatory mechanisms cmbodying criteria of success or failure: mechan- isms, that is, emitting signals indicating the diffcrence be- tween the present state of the organism and some acccptable condition or goal-statc.

(b)Then(the crucial feature)thesc signals must be allowed to altcr the controls that govern activity (including the choice of subsidiary goals if necessary)in such a way as to reduce (at lcast statistically)the difference between the present state and the goal-state. Evidently the controls can come to rest only if the goal-state is attained and the difference- signal reads "zero". Unless this is so they should always be found actively opposing any changes in the state of affairs which would tend to increase the difference-reading. An adaptive or matching-response is one which is goal-directed in this way towards minimising the degrce of mismatch as indicatcd by evaluatory mechanisms. We might define it as ""activity under the correction of cvaluatory signals".

This is of course the type of control familiar in engineering under the name of negative fcedback. The standard illustra- tion is the thermostat, in which the degrce of mismatch betwcen the present temperature and an adjustable pre- scribed temperature is evaluated by a simple device which 68 CHAPTER 6

turns heat on or off as required to reducc the degrce of mismatch. If the prescribed temperature is altercd the sys- tem will (in its own time!) follow the adjustments.

The point of special rclevance here is that insofar as an adaptive response is successful, the automatic movements of the goal-directed control-centre will in quitc a precisc scnse mirror the current state of affairs, or rather thosc fcatures of the state of affairs to which it is responding adaptively. The state of the control-centre is in effect a representation of those features of the state of affairs, just as much as a code-pattern of binary symbols could be. In each case we nced a principle of interpretation, provided in onc casc by knowledge of the evaluatory critcria, in the other by the code book. In cach casc, given thesc, we can infer certain things about the statc of aflairs represcntcd.

Let us now generalisc. It is pcrhaps obvious that when I move my finger to follow the outline of a moving spot of light, the configuration of the thrcsholds of the ncrvous system controlling my muscle-movements is an implicit reprcscntation of the position of the spot. But what about listening to some- thing, or looking at something?

Our suggestion is that here also perception is distinguished from reception by the elcment of adaptive response: that in pcrception an internal pattern of activity is cvoked (undcr evaluatory correction)which in some sense (we do not know what) matches the spatio-temporal rhythm of incoming signals from ear or eye. Once again, if this is so, the controlling threshold-configuration (or of course the activity it detcrmincs) may bc considered as a reprcsentation of current cvents perceived.

In short, our suggestion is that whencver information is reccived, there is in the human organism adaptive activity; and that the current changes in the "setting of the controls" (the threshold configuration) that lead to a satisfactory matching-response(relative to definite though not necessarily permanent criteria)form a representation of the information ASPECTS OF HUMAN COMMUNICATION

69

actually perceived-i.e. what the man is noticing in the flux ofevents.*

Such activity will be sclective and abstractive-as human perception notoriously is. Any adaptive activity, producing internal spatio-temporal rhythms that are a good enough "match" within the resolving-power of the evaluatory mechanism, will pass muster. In many cases more than one such response could meet the criteria, and the control mech- anism might fluctuate betwcen two or more adaptive statcs. This may plausibly be the basis of many ambiguities of visual perception, such as the familiar isometric drawing of a cube which appears in cither of two aspects. It would also scem to account satisfactorily for some classical optical illusions.

So far we have not discussed the way in which evaluative correction could bc applied. At one extreme we could en- visage a logical network which computed the best correction to minimise the mismatch. At the other we might envisage undisciplined trial and error by random alteration of thresh- olds until success was signalled. This would be slow to con- vergc, and indeed convergence could not be guaranteed. Let us suppose however that we have a hierarchy of mechan- isms for altering the relalive probabilities of trial of mcclhanisms for altering the relative probabilitics... to as many terms as we wish. If now we usc our logical network to prcselect the arcas of trial, and use cvaluatory signals to lower all thresholds associated with successful trials and raisc all associatcd with failurcs, it is evident that any statistical regularitics in the flux of cvents will tend to find themselves reflected sooncr or later in the relative probabilitics of trials.

The Kantian catugorics here find their physical embodiment not in the nature of a set of built-in filters, but in the characteristics of the possible modes of response, partly built-in, partly evolved. In actor-language, my world (as known) is structured for me in terms of my basic modes of match- ing myself to it. I know only thosc features of the world of events that stir me to adapt myself to match them; and the form of my knowing is deter- mined by the form of adaptation in which I find myself matched to them. 70 CHAPTER 6

Such a hierarchical mechanism could in time come to repre- sent a set of abstractions from the statistical structure of events to which the organism has made adaptive response, even with only the roughest guidance from its logical analysers. These abstractions would in fact amount to hy- potheses about the world of events, representing implicitly what past experience has shown to be its steady fcatures.

The higher-order probabilities in such a system will tend to change more slowly, the lower-order most rapidly. Changes in the lower which persist in occurring will tend to become reflected in changes at a higher level adapted to evoke the lower changes automatically. Thus gradually only those aspects of situations which are new to the organism will come to evoke adaptive activity at the level of the controlling mechanisms. (In actor-language, familiar items will come to be expected, and will yield a smaller and smaller amount of information. They may even cease to be noticed.)

But this is not the place for a full discussion of the theory of learning and memory that could be based on our conceptual model. It will suffice if we have gained a clear picturc of what is meant by the hierarchy of threshold-configurations govern- ing adaptive response. For this in quite a literal sense deter- mines the state of conditional readincss of the organism for adaptive response. Corresponding to a given threshold- configuration there will be a hierarchy of transition-probabili- ties— the t.p.m. — which we regard as the correlate in observer-language of my state of readiness. IWe can now complete our transition from the subjective discussion of information. Information can be generally defined as that which promotes or validates representational activity. In the human organism this activity is a change in the t.p.m.that specifies adaptive response and the hierarchy of conditional readinesses for adaptive response.*

It should be remembered that only the adaptive t.p.m., and not the t.p.m. for all activity, embodies the representation of the perceived world. ASPECTS OF IIUMAN COMMUNICATION

71

MEANING

IVe are now in a position to define (at least conceptually) objective correlates for the notions of the meaning and rele- vance of information. The meaning of a signal to a given receiver(in observer-language)may be defined as the selective operation which the signal defines (in a logical, not a physical sense)on the sct of possible states of readiness (i.e. of the t.p.m.). The selectice information-content for the receiver as defined in communication theory is a logarithmic measure of the unexpectedness of that selective operation. Thus we can readily see why even to the receiver the selective information- content is not directly related to the meaning. If the state of readiness happened already to match the signal, this would imply that the prior probability of adaptive response was unity and the selective information-content nil. The meaning however is unaltered.

Has the notion of imcaning any quantitative aspccts? Subjectively we sometimes speak as if it had. IVe have an intuitive notion of "richness" of meaning, as the opposite of simplicity. It would seem reasonable to identify this with the complexity of the selective operation (or of the features of thc state of readiness organised by it). If we like we may carry the mathcmatical representation a stage further. Assuming that the degrces of freedom of the mechanism controlling the t.p.m. are finite in number, we can represent a particular adaptive modification conveniently by a point in a multi- dimensional space of the same number of dimensions, or by the vector linking that point to the origin. This space, which we may term "response-space", in effect represents the universe of discourse for the organism, since all information received may be (indeed on our definition must be)repre- sented by the motion of a point within it. Its dimensionality defines the number of independent symbols that could be necessary and sufficient for the complete exchange of such 72 CHAPTER 6

information;* but since the probability of occupancy of much of the space will be ncgligible, a sufficicnt working vocabulary of basic symbols could be much smaller.

This picture offers a symbolic representation of the ineaning of a signal by the orienlation of the vector describing its selective operation. Our notion of "richness of meaning" may then find an adequate definition as the number of dimensions of the subspace "spanned" by the vector: the number of its com- ponents.

Unfortunately the picture is misleading in one important respect, for the degrees of frecdom of the control system may themselves be liable to adaptive trial and error like everything else. Thus the identification of the basic vectors is not per- manent. The dimensionality and metric of response-space itself will change with experience-cven in the process of communication. The picture can serve only as a basis for our definition of the meaning to the rcceiver at time of receipt.

A distinction should be carefully madc between the notion of meaning-to-the-receivcr, which we have here defined, and the notions of intended-meaning and generally-accepted- meaning. Analogous definitions of these other concepts are obvious. In each the cssential notion is formally the selec- tive function (intended, effected, etc.) on a set of possible responscs.

We may assumc that part of the human mcchanisin of adaptive response governs a varicty of internal activitics such as humoral secretion and the like, which are not directly coupled to our mechanisms for handling propositions and are only vagucly describable in actor-language if at all. The naturc and extent of such activity or readiness for it could be expected however to make a differcnce to the quality of awarencss. It is represented in rcsponse-space by component- This assumes that each symbol could be qualified by a continuously variable parameter. The number of two valucd symbols required would of course be greater. ASPECTS OF IIUMAN COMMUNICATION 73 vectors on the samc footing a priori as any others. If this is so it may scrve as a further caution against supposing that the meaning of a message can be exhausted by a catalogue of its cquivalent propositional content. Botlh the intended meaning and the understood meaning in our sense of the terin may have non-propositional components, without being rendered in the Icast indefinite in consequence. It seems important to free ourselves from the notion that something is indcfinite unless somcone can talk definitely about it.

So far we have been concerncd only with the meaning of a complete message: i.e. something designed to cvokc a definite sclcction from the set of possible responscs. A single word of a message does not in gencral cvoke a unique sclective opcration. It may be thought of as setting up a conditional probability- distribution over possible matching-responses, which is gradually moulded and narrowed down as the message is complcted. The mcaning of a word can thus be represented not by a point but by a distribution in responsc-spacc.

RELEVANCE

What of the concept of relevancc? We say that information has more relevance to one qucstion than to anothcr. It is necessary first therefore to consider how a guestion is represented in our formalism.

Recciving the answer to a question determines a subsct of adaptive responses, whiclh until then were undctermincd or only partly determincd (i.e. statistically). To frame a qucstion is to spccify this subset of undetermincd responses- or in our formalism, the corrcsponding subspacc of response- space. It is to invite a selective opcration on this subspace. The notion of the rclevancc of information to a qucstion is thus linked with thhe notion of the proportion of the total selective opcration that concerns the required sub- space. 74 CHAPTER 6

It is tempting to seek a metric for responsc-spacc such that (as in the formalism of scicntific information theory)a given question could be represented by a particular ray in the space, and the relevance of information defined as a number betwcen 0 and 1, represented by the cosine (or better, the square of the cosine)of the angle between the information- vector and that ray. This would ensure that a sclective opera- tion on precisely the subspace spccified by the qucstion could have a relevance of unity, while a selective opcration on an orthogonal subspace (related to nonc of the rcadinesscs specified by the question)would have a relevance of zcro. With such a metric the square of the length of the information- vector could serve as a further quantitative mcasure of information-content, being additivc for the combination of information-vectors.

But this must form part of a latcr programme. For the moment we may be content that within this same objective framework there is evidently room for a quantitative concept of rclevance, as somc conventional mcasure of ovcrlap betwcen the selective opcration performed on response-space by information, and the selective opcration invitcd by the question to which its relevance is to be estimated.

It may be noted that "irrelevant information", which operates on a subspace orthogonal to that specified by the question, is clearly distinct from "scmantic noise", which (is any feature of a message that) reduces the sharpncss of a selective operation on the required subspace.

THE COMMUNICATION PROCESS

By way of summary, we may now revicw the picture of the communication process which we have been building up.

The object of communication in actor-language is to evoke in the mind of the receiver something which the originator has in mind. We have takcn as the correlate of "having in mind" in observer-language the posscssion of a certain objective state of conditional readincss for intcrnal and ASPECTS OF HUMAN COMMUNICATION

75

external adaptive activity.* The problem of communication is thus in observer-language the problem of evoking in the receiver a state of readiness in some desired respects similar to that of the originator.

It would be tedious to give an observer-description of the whole process whereby physical symbols are conventionally associated with appropriate states of readiness. Engineering communication theory is concerned with the transmission process by which a symbol chosen by the originator is caused to appear before the receiver.

In its most economical form this uses physical signals not to depict but to select a standard representation of the symbol at the receiving end. The communication engineer measures the selective information-content of such signals, not in terms of the selective operation performed by the symbol on the ensemble of states of readincss of the human receiver, but in terms of the selective operation performed by the signal on the ensemble of symbols. The symbols are represented in this ensemble in the proportions in which they normally occur, the most frequently used occupying the largest space and being most easily selected.

The ensemble of states of readiness of the receiving human being may have quite different proportions, unless he were the only user of the communication channel and had an ideal matching-response mechanism.

It should therefore be clear why the selective information- content estimated by the engineer and the selcctive informa- tion-content estimated by the receiver are numerically different quantities, though the concepts denoted by the term are one and the same. Selective information-content in fact measures not a stu, but a relation (selective power) betwecn a signal and an enscmble. Confusion would often be avoided .This may include, e.g. the states of half-readiness corrclated with what we call imagining something, where some of our readinesses are organised "as ir" it were the case, others are suppressed. See Refs. 14 and 15. 76 CHAPTER G

and debate dissolved if the ensemble were defincd with every cstimate.

As a final illustration of this approach we inight considcr the familiar conundrum: Is information multiplicd when a newspaper is printed? Information bcing that which promotes representational activity, it seems fair to say that it is. But what is often meant by the question is rather: "Is sclective information-content multiplied when we produce fresh copies of the same newspaper?"

To this the obvious response is to ask ""relativc to what enscmble?". If the ensemble is that of all possible newspaper contents, it is clear that the production of fresh copies in no way affects the selcctive operation performcd on this ensemble, unless successive copies were liable to random errors so that fresh copies enabled the selective operation to be statistically more precise.

So there is no paradox. It was only a solecism.

CONCLUSION

Our discussion of communication has suggested that

(a)there is but one concept of information, though there are several complementary concepts of inforimation-content; there is no specifically engineering concept of informalion;

(b) the concept of the meaning of a message can be opera- tionally defined as its selective function in relation to the adaptive-response-space"of the human recciver;

(c)the prior improbability of the adaptive response evoked defines logarithmically the selective information-content for the receiver in the same way that the prior improbability of the symbol evoking the response does for the communica- tion engineer;

(d)these improbabilities being measured from different ensembles, there is no reason for the receiver's estimate of selec- tive information-content and the engincer's estimatc to have the same numerical value, though the concepts are the same; ASPECTS OF HUMAN COMMUNICATION

77

(e)sclective information-content in fact measures not a stulf but a relation, and is not defined unless both terminals of the relation are specificd;

(f) concepts such as the relevance of a message find ready correlates in terms of the function of the message on the adaptive-response-space of the receiver;

(g) to identify the dimensions of adaptive-responsc-space should enable the definition of an ideally economical language; but unfortunately the variation from onc individual to an- other and in one individual from time to time rendcr any hope of a complctcly unambiguous universal language illusory in principle.

POSTSCRIPT

Ii will be crident that this operational approach to semantics was closely comected with other ideas about the nature and orgarisation of mind-like behaviour in general, and hunan behaviour in particular. These were sketched in a series of papers (from 1949 onwards) to be published as a separate colume. Their central notion was that the organisation of intelligent agency reqired the field of action to be represented internally, in terms of the constraints imposed by its structure upon the transition-probabilities (the conditional probabilities of various possible next steps in various gicen circumstances) governing the planning of any action that must take account of that structure. A structured environment implies some degree of redundancy or pre- dictability in the sequence of actions, internal and external, demanded by it; and this in turn suggested that redundant features of the control sequence could be internally preorganised to increase efficiency. The internal hierarchic "organising system" needed to mould the con- ditional probabilities of action in this way was thought of as con- stituting ipso facto the necessary internal representation of the world, and hence the ultimate "target"" for any indicative communicalions from another organism.

It should perlhaps be emphasised that the meaning of a message is not here defined as the effect it produces in the recipicnl. The meaning it 78 CHAPTER 6

has for a gicen recipient is a logical properly, which it possesses whether or not it has a chance to exercise its function on the recipient. The definition of meaning in the original paper as the selectice operation which the signal performs on the set of possible states of readiness" was open to misinterpretation on this score, since it was easy to coufuse the logical operation on the set with the physical operation on the organism. To avoid this misunderstanding I hace made some changes in weording in the present zersion. CHAPTER 7

The Place of Meaning' in the Theory

of Information*

FOREWORD

By the time of our Third London Symposium on Information Theory in 1955，it had become something of an accepted saying that 'information theory has nothing to do with meaning'. The time seemed ripe to question this hardering dogma, and the follozeing paper to some extent orerlaps with earlier chapters in its atlempt to do so constructicely.

Some comments in discussion of Professor Yngre's paper in the same symposium have been worked into the present text for concenience, in the paragraph headed' Mechanical Translation'.

INTRODUCTION

It is nowt scven ycars since Shannon published his papers on a 'Mathe- matical Theory of Communication'31.36 In this he defined a quantity which he called 'amount-of-information', which is cssentially a logarithmic mcasure of the statistical unexpcctedness (reciprocal of probability) of the nmcssage co:icerued. Since the urexpectedness of a message need have no dircct connection with its smauntic content or ncaning, Shannon wisely insisted that the concept of 'meaning' was outside the scope of his theory.

This innocent statement by Shannon has given rise to two unfurtunate consequences.

* 'Information Theory'(E. C. Cherry, cd.), Butterworths, 215-25，1956i ↑1955 80

CHAPTER 7

In the first place the original sense of Shannon's warning has somctimes bcen forgotten and he is credited with the vicw that the whole thcory of information (which includes his own theory of the unexpertrdness of information as a vital part) has nothing to do with "neaning'.

Sccondly, and largely in consequence of this, the idea has become current that the whole subject of meaning is not satisfactory for the infarmation theorist. 'Subjectivc', 'vague', 'dangrrous', are the adjcctives with which it is aften smothered.

Now there is no doubt that the idea of 'meaning'. has subjective aspeçts, that it is vague in many people's minds, and that it still in fact provokes debate among philosophers of the subjec:t: it is at least as 'dangerous'in these respects as the idea of 'information' itself. But it is no more so; and in this paper I venture to outline a tentative account of the place of'niean- ing' in the theory of information which I hopr, though dlealing by definition with the human subject, may be objective, precise and (sufficicnily) safe. TIIE TIIEORY OF INFORMATION

It must be understood that if anyonc wishes to use the term 'throry of infurmation' cxclusively for Shannon's statistical theory of cominunication he cannot of course be prevented, but he must then realize that we are here. discussing something wider for which he must coin his own nane. By the theory of inforination we shall mcan broadly the theory of proccsses by which representations come into being, together with the theory of thos abstract features wl:ich are common to a representation and that which it represents. By a representation of I we shall mean a sct of events or objects exhibiting in at least onc respect (even if only statistically) the pattern of relationships between the components of the situation Y. By information we shall nican that whhich justifirs representational activity: that to which logical appeal is made to justify a representation.

Infurmation that thr water-level at Richinond is 10 ft., for cxample, logically justifics a representation of the water-level at Richinond as 10 ft. Whether the information is truc or false is another matter. If it is truc the representation corresponds with the actual state: of affairs at Riclmond; if not, it corresponds with a fictitious state: of aflitirs. The infornation is what was essential to justify the making of a representation at all.

So far our definitions have been qualitative. They have been framed so as to apply to a wide range, if not all, of the corauon ust's of the term informationi, including those of communication theorists. When we come to quantitative measures, it is essential, as Shannon has pointed out,3 to distinguish the qualitative concept of infomation from the various quanti- tative incasures of amoumt-of-information of which Shannon's is one.

As a basic definition of amount-of-information or infornation-coutent it is reasonable (in view of our definition of information as that which justifics representational activity) to take 'an additive measure of the cquivalent number of clementary steps or stages in the represcntational activity justified'. This has the merit of covering all three measures of information-content so far found uscful.

(a)Shannon's imeasure indicates the minimum cquivalent number of binary steps by which the representation concerned may be selected from an ensemble of possible representations. T'his has suggested the term 'sclective. information-conten:' for Shannon's measure of 'amount-of-information'. 'MEANING' IN THEORY OF INFORMATION

81

(6)The two complementary mcasures of what we may term 'descriptive- infornation-content' indicate the cquivalent number of clementary steps or stages by which the represcntation concerned may be constructed: (i)the 'structural-information-content' or "logon-content' indicatcs the minimum equivalent number of independent features which must be specificd-the nuinber of degrees of freedom or logical dimensionality of the representation; (ii) the 'metrical-information-content'or 'metron- content' indicates the cquivalent number of units of evidence which the information providcs for the construction of the represcntation (e.g.the number of mininally significant events, in the case of a scicntific reprcsenta- tion of an experimental result).

In 1952 Bar-Hillel and Carnap1 (hereafter rcferred to as B and C) suggested two possible measures of the information- content of statcments in an artificial language system. Bricfly, they considcr reprcscntations constructed from atomic statements', cach of which asserts that a particular 'individual' of a finite set has onc of a finite sct of 'propcrties'.

In order to derivc quantitative measures, however, they cousidcr not the structurc of a given representation, but its power to imply possilble statcmcnts. In particular they con- sidcr the large class of statcments forincd by taking each possiblc atomic statcment or its ncgation and combining them with the disjunction 'or': for example, 'l1 or A2 or not-Bl or... ctc.' Thesc arc the wcakcst possible statcments in the language systcnt, and are called 'content-clements'. T'hc class of content-clencnts logically implicd by a given statcment is then called its 'content', and is suggested by B and C as an cxplication of the "information' conveyed by it. A suitable measure of this class, the 'content-measure', is suggested as one possiblc cxplication of the amount of information con- veyed' in its semantic sense. This measurc cquals zero if a statement is true and unity if it is false, and inay be thought of as tlhe inductive probability of the negation of the statcment. Unfortunatcly it is not additive for indcpcndent statemcnts.

Accordingly B and C proposc a second mcasure, the negative log of the inductive probability of the statcment itsclf, which they call the 'measurc of information'. This is, of coursc, additivc, and differs from Shannon's familiar measure only in using inductive rathcr than statistical probability. 82

CIIAPTER 7

A connection can rcadily be madc betwec this lattcr approach and that of descriptive information thcory (which owing to its origins I called carlicr the 'thcory of scicntific information'). In dcscriptive information theory we are concerned with the analysis of represcntations in tcrms of thcir logical dimcnsionality and thcir wcight of cvidence. Each dimension or degrce of frcedoin of a represcntation corrcs- ponds to one of B's and C's 'individuals'. To cach may be attributed a variablc number of indistinguislhablc 'nctrons' representing the weight of cvidence' or 'numlbcr of clemcn- tary cvents' it subsunmcs. It is gencrally possible, in any givcn casc, to compute the number of different possible representa- tious. The logarithm of the number (base 2)，called 'amount of detail' in rcference 12, sccms quite closc to the 'mcasure of information'defined lby B and C. If the inductive probalbility of any one representation werc inverscly proportional to the number of possibilitics, the two incasures would in fact bc thhe same. In many cascs the total mctron-content, or the

maximum per logon, may be fixcd, and if so this will affcct the probability distribution and introducc a differencc betwecn the two mcasures. There scens however no rcason why the

label 'scmantic'should not be attached cqually to B's and C's

measures and to those of logon- and mctron-content, and to amount of dctail'. All arc conccrncd with the structure, rather than merely the rarity, of a reprcsentation.

To B's and C's 'content-mcasurc' therc corresponds no directly analogous mcasure of descriptive information-conteut hithcrto defincd. Numcrically it corresponds to the fraction of the total information-spacc* which is left umoccupicd by the description concerned. Since scientific descriptions arc seldom given, and still morc scldom accepted, in disjunc- tive forin, the class of scntenccs considcrcd in ny thcory of descriptive inforination was mucht nore restrictcd, and admits of measurement by simpler parameters.

See first paragraph of section: "Mcaning' in the Furmalism of Information Thcory, bclow. 'MEANING' IN THEORY OF INFORAMATION

83

The point at present, however, is that our gencral definition of information-content applics, additivity apart, to Bar- Hillel's and Carnap's 'content-mcasure' and, additivity included, to thcir 'measure of inforination'. There is thus no basis for any separation of 'semantic information thcory' from the general theory of information as defined in the Appendis.

MEANING

The forcgoing recapitulation of the scope and the concepts of information theory provides a framework on which to hang our discussion of the conccpt of mcaning. At the outset we must note that it is not only statements which may be said to have mcaning. IVe speak also of the 'meaning' of other cxpres- sions such as questions, coninands and even exclamations. In secking to definc an equivalcnt of the term in the language of information theory, we must be carcful not to imply too narrow a definition.

I do not mcan that wc must find an omnibus equivalent which can be substituted directly for all uscs of 'mcaning'in everyday spcech; but it docs seem reasonablc for the reader to demand, and the infornation-theorist to accept, the principle that, in the early stages particularly, the technical cquivalent of a common tcrm should couform as far as possible with common usagc. The technician's cffort to sharpen the concept should at least in principle allow the technical equivalent to be substituted for the term, without violation of basic scnsc or grammar, in as many contexts as possible.

Let us now picture a communication process in which you send a message (A1) to ine. For cxaniple, AI might be: 'Someonc is waiting for you outside:'. Now we nay assune that by sending lf to nic you intend to produce soine cffect on me. If you had sent a message in gibbcrish or in a language unknown to me, you might have intended ouly to distract and puzzle ine; but since the message Af is in English, we will take it that you intend ne to understand it and to appreciate its neaning. What kind of cifrct is this? Obviously it need not be an immediate change in my observable pattern of behaviour. What you are' concerned with is my 'total state of readiness': in objective terms, the sct or matrix of conditional probabilities of different 84 CHAPTER 7

possible pattcrus of bchaviour in relevant circumstanres. For example, when I leave the room you want me to behave as if I expected to find someone outside, and so forth. It is, then, the conditional-probability matrix or 'C.P.M.' which you want to affect in a particular way, by my 'uuder- standing the ueaning' of your message. If the C.P.MI. is already in the desired state- if for example I know already that somcone is waiting for me-then your object has already been achievrd. y'our object, ther, is not necessarily to bring about a change in the C.P.M., but to establish a certain state of (part of) the C.P.A1. for activity, internal (c.g. prrerptual)or external (c.g. motor activity).

What then of the meaning of your message? IVe must clcarly distinguish betwecn (a) the meaning intended by the sender, (b)the mcaning understood by the receiver, and (c)the conventional meaning. But if we takc (b), for cxamplc, can we define the reccived mcaning as simply the change that takes placc in B's behaviour? Attempts havc been made to define the meaning of a message simply as the bchaviour- pattern it produccs in the receiver; lout this I think will not do. To begin with, we would not say that a message has no meaning if the recciver already knows what it is saying. A message docs not lose its meaning through being repeated. And then purely on linguistic grounds one could scarcely regard the bchaviour resulting from reccipt of a message as synonymous with its reccived mcaning. Any number of sentences in which 'meaning' is normally used wouldd become grammatical nonsensc, if this 'definition' were substituted.

On the other hand, the reccived meaning is ccrtainly closcly tied up with the bchavioural conscquences, if we include internal as well as external activity under 'behaviour'. We may reasonably say that the conscqucnt intcrnal and external behaviour-pattern in principle shows or demonstrates the received mcaning.

Can we then definc the rcccived meaning as the change in the C.P.M. for intcrnal and cxtcrnal activity? Again our objection would apply, that a repeated message may produce no significant change. Can we idcntify the mcaning with the state of the C.P.M. rather than the change? Again the linguistic objections arc I think conclusive. The mcaning of a message is not identical with the statc it produces. It is 'MEANING' IN THEORY OF INFORMATION

85

identified by the statc it produces. This represents somc progress. A incssage rcad for a sccond timc produces-or should producc-substantially the samc state of the relevant C.P.AI. Its mcaning is the same. WWhat technically precisc phrasc can we substitutc then for 'mcaning'here?

I suggest that the rcceived mcaning of the message be defincd, not as the resulting statc of the C.P.M. but as the selectice function of the message on an ensemble of possible states of the C.P.11. 'Sclectivc function' here implics of coursc a rclation- ship, not a happening.

Tentativcly we take as our basic delinition of 'ncaning', then, the selective function on a spccificd sct or cnscmble, or for short 'sclcctive function'. This Icavcs room for as rnany subdivisions of the concept as there are diffcrcnt dcfinable enscmlbles; but I have not yet come across any instanccs in which one cannot consistently replace 'meaning'by sclective function' or 'sclective opcration', lcaving the sensc unaltcred, and giving oficn considcrablc illumination.

Corrcsponding to our distinctions bciwcen intended, received, and conventional meaning, we now have distinctions between (a)the sclective function intendrd by the originator; ( the selcctive function actually cxcrcised; (c) the selective function on the cnscmble of states of a conventional symbolic reprcscntational systcm.

In what follows we shall not always recapitulatc thesc, but the necessary modifications to the argument to make it apply in cases (a), (b), or (c) will be obvious.

SOME TEST CASES

Lct us take a few cxamples. T'o begin with, Iet us considder the term 'ncaningless'. "I'his mcssagc or word is ncaningless', on our definition, becomes This nessage or word lacks a selective function. . it has no selective relationship to..To what? Immediately our definition suggests that the statement I is incaningless' is incomplete. This we should expect, for a sentence may casily be meaningful to onc nan and 86 CHAPTER 7

gibbcrish to another. Mcaninglcssncss is a rclative conccpt, and a precisc definition of mcaning would be usclcss unless it automatically remindcd us of thhis.

Now it is possible for somcthing to lack a sclectivc function for two reasons: (a) one or more of its component terms may be undcfincd-may have no sclcctivc function-so that the total sclcctive opcration is undcfincd; (6) two or more of the componcnt sclective functions may be incompatible, so thhat the total sclcctive opcration cannot be complcted.

Correspondingly, we find two kinds of mcaningless sentencc. The gups arc plec' is mcaninglcss to most of us for thc first reason. "The watcr is isosccles' is mcaninglcss for the sccond. On the other hand, 'This stochastic process is station- ary' is probably mcaningless to most of our fellow-nortals for the first reason; and 'The radiation from a horn-fcd checse'(actual titlc of a papcr on Nicrowaves!) perhaps cqually mcaningless for thc sccond.

Consider next the notion of 'synonyimy'. Onc oljcction to any attempt to define meaning is that Two concepts may have the samc meaning on onc definition of the tcrm, but diffcrent mcanings on anothcr'. For cxamplc, docs an equilatcral plane figurc with four right-anglcd corncrs' have the samc mcaning as 'a square'? Our answer is quitc clcar. If we translate 'incaning' by 'selcctivc function'we see at once that identity of sclective function(synonymy)is going to depend on the particular cnscmble on which wc propose to test the selective function. The fact that various proposcd 'dcfinitions' of incaning have given different answcrs from common sensc may increly be evidence that thcy were not sufficicntly fundamcntal. If attcmpts arc inadc to definc a relation in terms of only onc of its terminals, we must cxpect apparent paradoxes to result. Thus 'an cquilatcral plane figure with four right-angled corncrs' has thc samc selcctive function as 'a squarc' on the cnsemble of plane geometric figures. It may have quite a different sclective function on the enscmblc of my statcs of imaginativc activity. 'MEANING' IN THEORY OF INFORMATION

87

What then of a message which statcs something I know alrcady or a message which is repcatcd? As long as we dcfine the mcaning as the sclcctivc function rathcr than the cffect there is no paradox in thc fact that the cffect on sccond hcaring may be ncgligiblc. The sclcctive opcrator which formally represents the mcaning of a message is usually (in mathcmatical jargon)'idempotent': the immcdliatc repetition of the sclcctive opcration should yicld an unchanged result. Admittedly the fact that it has bcen rcpcated ınay itsclf have meaning-may have a sclcctivc function of its own. This however is quite distinct fron the mcaning of the message itsclf which is unchanged.

Hcre we begin to rencw contact with information thcory. We arc accustomed to saying that a mcrc repctition of the same messagc (in the abscnce of noisc) has no sclective- information-content for the recciver, because the ensemble on which it operatcs the sccond timc has only onc memlcr with non-zcro probability. Sclcctive-information-content in fact mcasures the sizc of the change brought about by a given selcctive operation. A second hearing of our mcssage causcs no changc, and so has no selective-information-contcnt; but it has the same selcctive function and so on our dcfinition the same mcaning as before. If, on the other hand, it did not cxcrcise the appropriatc selcctive function on first hcaring, we say it was misundcrstood. Its selcctive function, and hence its reccived meaning, on sccond hearing may then be differcnt.

It is of coursc a psychological fact thhat if the sainc phrasc or sentence is repcated suflicicntly often it tcmporarily loses its meaning. Here is a furthcr test of our dcfinition, and again it not only survives, but shows the phenomenon itsclf in a fresh light. Repctition robs a scntencc of mcaning-to-the- subjcct-of 'sclective function on thc enscmble of statcs of the subject's C.P.M.', we would say. This not only makcs sensc, but suggcsts various experincntal qucstions as to the proccsscs by which constant repetition of symbolic stimuli Icads 88 CHAPTER 7

temporarily to their 'uncoupling' from the sclcctive systcm governing the subject's C.P.M.

So we might go on. The mcaning (intended, received, conventional)of a command, a qucstion, or an cxclarnation, for example, can likewise be defined as thcir sclectivc function on a spccificd ensemblc of responses. Thc detailed discussion of qucstions, commands, and other non-dcscriptive messages would have takcn us too far, but the outlines of their treatment from the prescnt standpoint will probably bc clear cnough. For the moment it is sufficient to notc that our technical definition of meaning appears to be cqually applicablc in all such cases. Diffcrenccs therc arc in plenty, but thcy are differences in the ensemble on which sclective function is cxerciscd, rather than differenccs in the basic concept of ineaning in cach case.

One remaining use of 'mcaning' is in a rather differcnt category. We sometimcs spcak of the mcaning of objccts or events which arc not messagcs. An overcast sky 'mcans' that rain is immincnt; or a mud-pic on the front doorstcp 'means' that the children have becn playing therc.

Here the objcct is a sign of what it 'means', but not a symbol. It thus docs not have an intended or a conventional sclcctive function; but the mcaning which we attribute to it can still be defined as its sclective function on the ensemblc of statcs of our C.P.M. The concept of meaning once again admits of one and the same definition.

THE RELEVANT ENSEMBLES

At this point-if not before-an objcction may well be raised. Not everything which alters the total C.P.M. for activity is a inessage; nor would it necessarily be described as meaningful. Thus our dcfinition might scem to be too broad.

In onc sense it certainly is. We have secn already that in any particular case we must fill it out by spccifying whether the selcctive function is intended, actual, or conventional, and 'MEANING' IN THEORY OF INFORMATION

89

saying for what ensemble it is defined. Our purpose has been to discovcr, if wc can, a satisfactory basic concept from which the various common senscs of 'meaning' can be derived by making thesc various distinctions. By extracting the common factor of 'selective function'(i.c. selcctivc relationship to an ensemble specified or implicd) we have, I hope, found the first term in a 'family trec'of sub-definitions which we must expect to ramify as widely as the range of rclevant cnsembles. On the other hand, a dcfinition of mcaning must not be mistaken for a sufficient criterion of meaningfulness. Our object is to provide a tcchnical equivalent for the tcrm 'mean- ing'wherc it is in fact used, not to legislate as to where it should be tised. The latter is largcly an cinpirical task-to discover, if we can, the range of relevant enscmbles pre- supposed in our basic dcfinition of meaning. Here we may note only a few pointers.

First, what distinguishes the perception of a meaningful object or event from that of a meaningless one? Essentially, the first lcads or could lead to a further inference. To say 'X means Y' is to imply that a further representation, Y, is logically justified, givcn Y. Even to say Y is meaningful' is to imply that some further reprcscntational activity is logically justified by I, whether or not the speaker is able to carry it out.

Tlius the range of cnscmbles to which a meaningful object or event has a selcctive rclationship by virtue of its meaning is restricted to those of representational states. In the human organism, for example, we may presume that there arc ccrtain internal states of the information flow system which constitute implicit representations of the subject's world of activity, both conceptual and physical.

To ask in detail what characterizcs representational states of the information flow system would take us too far, and I have discusscd the question elsewhere.15 But we may draw one more basic dividing linc. A typical pattern of activity- say walking out of the room expecting to find a friend outside 90

CHAPTER 7

the door-is directed to the achicvement of a hierarchy of 'goals': to maintain balance, to avoid the corner of the tablc, to find the door handlc, and so forth. If the table, for examplc, is moved, the corresponding 'goal-setting'alters if I bccome awarc that it has moved. The hierarchy of goal- settings represents, in a definite sense, what I know or believe concerning my world of activity. Our suggestion is, bricfly, that the internal representational activity of the human organism takes the forn of the selection of goal-settings- including the conditional probabilitics of their alteration. The cnsembles presupposed in our definition of meaning are ensembles of goal-scttings in the above scnsc.

What then of conventional mcaning', as given for cxample in dictionarics? What an cntry in a dictionary docs is to replacc an unfaimiliar sclective opcrator by an cquivalent whose selective function for the user is presumed to be estab- lishcd. The cnsemble concerncd is in the first instance that of cstablished selective opcrators; but the term established' presupposcs a 'standard uscr' whose cnscmble of reprcsenta- tional states is ultimatcly in qucstion.

This discussion applies cqually to natural and to artificial languages. The only diffcrencc is that whcreas natural sentenccs may modify the C.P.M. (statc of rcadiness)for other than symbolic responscs, sentences in an artificial language affect only the C.P.M. for perception and manipula- tion of the symbols themsclves.

MECHANICAL TRANSLATION

Our prescnt linc of thought has a bcaring on the vexcdd qucstion of mcchanical translation. When as children we learn to translatc from one language to another we may begin by trying to substitute onc word directly for another with the help of a dictionary. As we progress, we gradually pass ovcr to a quitc different kind of procedure. IVe try to discover what the original author wants to contey in the new language. In short, we pass over from thinking solely in terms MEANING' IN TIIEORY OF INFORMIATION

91

of the symbols to thinking in terms of the dispositions inlended to be evoked by the symbols. This is what distinguishcs insightful tran- slation from what some would prefcr to call mere transcription.

A corresponding distinction exists betwecn two diffcrcnt approachcs which are covered by the namc of mcchanical translation. The first, at present almost universal, produccs a translation by a corrclation of syntactic structurc in the two languages. No understanding is necded, in principle, of the dispositions intended to be cvokcd by the matcrial to be translated. For this rcason I would suggest that evcn Pro- fcssor Y'ngve's ingenious 'transition language'41 would perhaps be bcttcr tcrmed a 'transition code', since its function is not to sclcct dispositions but rathcr symbols.

T'lc sccond approach would be to make, as an inter- niediatc step, a reprcsentation of the dispositions intcndcd to be evoked by the matcrial to be translated. A translation could thcn be achicved by producing, as the output, cx- pressions in the other language which cvoked the samc dispositions. I know of no practical work being carricd out on thesc lincs, and I suspect that it nay have to wait for our undcrstanding of information-proccssing in the human organism; but the product of such a translating device would, I think, be much closcr to what wc normally desire of a human translator. The diffcrence would be shown most casily in the kinds of fault to which each translation would be liable. A translation on the first principlc should quitc faithfully reflect the syntactic structure of the original, but could casily fail seriously to convcy the meaning. A translation on thc sccond principle might allow only a loose inferencc to the syntactic structure of the original, but should on the wholc faithfully reproduce its mcaning.

MEANING' IN THIE FORMALISM OF INFORMATION

THEORY

We may now scek to connect this approach with the au- thor's carlicr representation of mcaning int the formalism of 92 CHAPTER 7

information theory. The statc of a represcntational system can be dcscribed by enumerating the states of cach of its indc- pendent dcgrces of frcedom. If therc are l of these, each may be associatcd with one dimension of an l-dimensional 'in- formation-space', so that any given state is represented by a point or rcgion of this space.

A particular messagc inay now be pictured as selecting a particular region, which may be identified by the vector (or distribution of vectors) linking it to the origin. The meaning of the message is then reprcscnted by the oricntation of this vector, rclative to thc vector basis. Wherc the mcaning is iinprecisc, the selective operation is imprccisc, and the oricn- tation of the vector correspondingly distributed statistically.

Somc further details of this reprcscntation have been dis- cussed in Chaptcr 6. For thc moment we notc only tlat the oricntation of the vector spccifics and corresponds one-to-onc with the selcctive function of the mcssage. The two approaches thus unite in an illuminating way, since the term 'selcctivc function', although the best I can suggest at the moment, is not idcally explicit; and the orientation of a sclective 'arrow' provides a uscful thought-inodel of what is intended by the term.

CONCLUSIONS

(1)It appears from our investigation that the thcory of information has a natural, precisc, and objcctively dcfinable place for the concept of mcaning.

(2)The meaning of a inessage may be defined as its sclective function on a spccificd ensemble.

(3)Tlic sclcctive-information-content of the nessage meas- ures logarithnically the size of the changc brought alout by its selective operation on the sanic cnsemblc.

(4)The relevant ensemble comprises diflerent possible states of a represcntational system. In the human organism these are states of the conditional-probability matrix (C.P.M.) 'MEANING' IN THEORY OF INFORMATION

93

governing goal-sctting activity. Where the human C.P.M. is in qucstion, the relcvant probabilitics cannot of coursc be cstimatcd oljcctively (nor, probally, subjectively). This docs not, howcver, prevent the concept from being objectively defincd; nor does it preclude the possibility that these prob- abilities are determincd by an objcctively definable physical state of the organism.

(5)The basic concept of meaning as selective function subdividcs according to the enscmbles for which the function is dcfincd. Thc distinctions betwcen intended meaning, received mcaning, and conventional meaning are automatic- ally preserved.

(6) It may be too much to expect that every idiomatic usage of 'meaning' will be adequately translated by 'sclective function', but the conccpt seems to apply equally readily in rclation to qucstions, commands, and other non-propositional utteranccs, and to non-symbolic objects possessing significance.

(7)Since meaning, as thus defincd, has as fine gradations as the gradations of human C.P.A.'s, the ideal of an unam- biguous universal language would seem to be unrealizable. The most hopeful idcal approximation would be a language the primitive individuals of wlich represented the independent degrecs of frccdom of the human C.P.M. which are common to all normal humans. It may well prove the best, if not the most practicable solution to the problems of context and the like in mcchanical translation to use an ideal languagc based on this principle as an intermediary betwecn the original and final languages. Unfortunately the completion of a truly basic language on these lines waits on our understanding of the human C.P.MI. CHIAPTER 8

The Informational Analysis of Questions

and Commands*

INTRODUCTION

It is not, I think, without significance that some recent symposia on information thcory contain relatively few papers on the thcory of information; but the significance is not, as might be supposed, that the theoretical concepts are now so far worked out that only thcir applications remain to be discussed. In fact the contrary would be nearcr the truth: that most of us who bcgan with an interest in the theoretical concept of information have becomc so increasingly and profitably absorbed in practical problems of information- proccssing, in animals or machines, that thhe gencral analysis of informational cxchange has been largcly by-passed, and for the majority of the new gencration now leaving collcge information theory still mcans little more than Shannon's measure of unexpcctedncss and its various applications. Othcrwise cxccllent leading textlbooks unashaincdly pro- claim a divorce between what they call 'information theory' and semantics, which topic is discussed, if at all, in the woolliest terms, and generally relegated to the philosopher.

As this can hardly be regarded as an ideal state of affairs in * From Proccedings of 4th London Symposium on Information Theory, 1960 (E. C. Cherry, ed.), Butterworths, pp.469-76. ANALYSIS OF QUESTIONS AND COMMANDS

95

such a young subjcct, we may well ask why so little progress has bcen madc on the scmantic side. Apart from the abscncc of workers, I suspcct the reason to lie in our failure to study the communicative proccss within a wide cnough context: to follow the flow of information far enough back, and forward, from the communication channel. We are all farniliar with diagrams showing the human sender and rcceiver as 'black box' terminals linked by a chain of noisy channcls. My suggestion is that scmantic qucstions find their natural place in information theory when (but only when)we widcn our diagrams to takc account of the naturc of these terminals as goal-dirccted sclf-adaptive systems.

Our particular object will be to suggest how qucstions and commands can be analyscd in informational tcrms similar to those outlincd in earlicr chaptcrs for the analysis of in- dicative scntcnces. In the first part we shall skctch the infor- mational rcquirements of organisms in the situation in which questions and commands arc cxchanged bctwecn them. Thus fortificd, we shall try to disccrn some lines along which at lcast scmi-quantitative analysis may fruitfully be prcsscd.

THE IMPACT OF INFORMATION ON THE ORGANISM

An organism can be regarded for our purpose as a system with a certain repertoire of basic acts (both internal aud external) that in various com- binations and scquences imake up its behaviour. In orcler that its bchaviour should be adaptive to its environment," the sclective process by which basic acts are concatenated requires to be organized according to the current state of the cnvironment in rclation to the organism. There are various ways of picturing this need. In its most basic terms, we may regard what is rcquired as cquivalent to a vast constantly changing matrix of conditional probabilities (the C.P.M.), determining the rclative probabilities of various patterns (and patterns of patterns) of bchaviour in all possiblc circumstances. More economically, we can think of it as the sctting-up of a hicrarchic structure of organizing 'sub-routines' to detcrminc these conditional probabilitics, 17.19 interlocked in such a way as to represent implicitly the structure of the environment (the world of activity) with which the organism must interact. For many purposes we may reduce it to the filling-out of a world-nap, ready to be consulted according to current nceds and goals.

*'Enviromnent' here mcans the total world of activity of the organisin, and not only its immediate physical milicu. 96

CIIAPTER 8

Whatever our thought-model, it is clcar that unless the orgauism happens to be organized exactly to match the current state of aifairs, womk must be done to bring it up to date: work not only in a physical, but in a logical scusc. This'logical work' consists in the adjusting and moulding of the conditional- probability structure of the organizing system: the formation, strengthening or dissolution of functional linkagcs between various basic acts or basic sequences of acts. The total configuration of thesc linkages cmbodics what we nay call the total 'statc of readincss' of the organism. Some of them will of course have purely vegetative functions that do not conccrn us. What dors intcrest us is the total configuration that keeps the organisn matched to its field of purposive activity, and so implicitly represents (whether correctly or not) the feature:s of that ficld. For brevity, Iet us call this the orienting system, and the corresponding total state of readincss the oricnlation of the organisn.

Informution can now be defined as that which does logical work on the organism's oricntation (whether correctly or not, and whether by adding to, replacing or confirming the functional linkages of the oricntiug systen). Thus we leave open the qucstion whcther the information is true or false, fresh, corrective or confirmatory, and so on.

The arirount of information received by an organism can then be measured (in various ways)by mcasuring if we can (in various ways)the logical (organizing) work that it docs for the orgauism. I have discusscd clscwhere some of the different measures that suggest themselves for different purposes, and we shall retura bricfly to the question later. Acanwhilc it is suflicicnt to note that they are neccssarily rclatire measurcs, siucc they ncasure the impact of information on the given recciver. Amount of inforntation' measurcs not a 'stulf' but a relation. The mcaning of an indicativc item of information to the organisn may now be defincd as its sclective function on the range of the organism's possible states of oricntation, or, for short, its organizing function for the organism. It will be noted that this too is a rclation. (It must be clcarly distinguished from the organizing work done on the organ- ism, which is the result of the exercise of this organizing function. Much con- fusion is caused by attempts to identify mcaning with the change produccd in the recciver.)

PERCEPTION AND COMMUNICATION

A solitary organism keeps its orienting system up to datc in responsc to physical signs of the state of the environment, rcceived by its scnse organs. This adaptive up-dating of thc state of orientation we call perception. We can regard communi- cation as an cxtension of this proccss whereby some of the organizing work in one organism is attempted by another

*This docs not of course make the concept any less objcctive in principle, since onc can always postulate a 'standard receiver', and this is in cffect what is done in communication theory; but it dot's prevent the magnitude associated with it from having a uniquc valuc. The same item can have quite diffcrent information-contents for dilTerent reccivers. ANALYSIS OF QUESTIONS AND COMIAIANDS

97

organism. Normally this means that the receiving organism is induccd to adapt itself in response to physical signs that arc perccived as symbols—as calling for orienting (or other) activity over and above that which constitutes their perception as physical events.*

The logical starting point for a semantic theory of communi- cation would therefore seem to be the analysis of the organizing functions that are 'extensible' in this way from one organism to another. There is a sense in which for this purpose the analysis of questions is logically prior to that of indicative sentences; for the meaning of an indicative sentence is often ambiguous until we know the question to which it is an answer, and/or the assertion which it excludes. For cxample, the sentence S: I sleep in room 10' may be an answer to the question (a) 'Where do you sleep?' or (b) 'Do you sleep in room 10 or room 12?' or (c)"Who sleeps in room 10?'or (d) "What do you use room 10 for?' and so on. Typical assertions excluded by S are then respectively (a)'I slcep elsewhere...' (b)'I sleep in room 12'(c)'Someone else sleeps in room 10' (d)'I use room 10 for other purposes'.t

Clearly, the selective function of S is quite different in these cases, either in its range (as between (a) and(b) or in its dimensions (as between (a), (c) and (d). No analysis of its scmantic information-content can claim to be adcquate unless it brings out differences of this sort, as well as doing justice to logical structure.

QUESTIONS

What then in these terms constitutcs a question? The object of a question is normally to evoke communicative activity of the sort we have becn discussing; but this by itself would be far from a definitive notion. Again the linguistic form of a * The training process by which symbols come to be accepted as such nced not here concern us.

t For a uscful discussion of this point see M. and A. Prior: 'Erotetic Logic' (ref. 28). It should be noted that in spoken, as opposed to written, speech the ambiguity is normally resolved by appropriate use of stress and intonation. 98 CHAPTER 8

question is often characteristic, but not always. Intonation may sometimes be the key discriminant, as in a phrase like going home?' which could cqually well be the answer to a question. TWhat, howcver, are we to say of the sentence 'I take it that you are going home'? It would normally make sense to treat this as a question requiring the same answer as Are you going home?'; yet it is in form (and could be in intonation)a plain indicative statement.

But indicative of what? IIere I think we come to the heart of the matter. WWhat is indicated here is the state of readiness of the originator, in rclation to the recciver; and this points to a characteristic of all questions. A question is basically a purported indication of inadequacy in its originator's state of readincss, calculated to clicit some organizing work to remedy the inadequacy. It is as if the questioncr uncovercd and held out the incompletc part of his organizing systcm to the reccivcr for his attention.

The fact that this normally works reveals an intcresting presupposition behind the whole procedure. We may well ask why the receiver should be expected to pay any responsive attention of this sort to the exposcd organizing systcm; and the answer is clcar. Qucstions work only because human beings are motivaled to adjust one another's statcs of rcadincss. Whether thanks to nature or nurture, a human being finds an organizing system exposed' in this dcliberate way by another a natural targct for adaptivc activity, muchh as a mother bird is moved to regard a gaping beak in the ncst. Doubt- Icss were it not so the human race would hardly have survived!

The moral would sccm to be that what makes an uttcrancc a qucstion cannot always be pinned down cither to a pcculi- arity of its logical form (since an inadcquacy of orientation can be indicated in many ways, some of them wordless)nor to the fact that it has clicited information (since pcoplc arc liable spontancously to try to adjust one another's orientation).

Our problem in fact has some affinity with that of deter- mining whether a given action was 'goal-directed' towards a ANALYSIS OF QUESTIONS AND COMMANDS

99

ccrtain cnd-point. Ncither the form nor the effect of the action arc infalliblc criteria alonc. Instcad, we adopt a 'variational' approach 15 and look for cvidcncc (usually structural) that if the 'goal' had been slightly displaccd, or the starting point slightly diffcrcnt, the form of action would have been correspondingly modificd in a manner calculatcd to rcach the samc cnd-point.

Similarly we can determinc somc utterances to be a qucstion only, in the cnd, by inquiring how the bchaviour of the originator would have bcen modificd in varying circumstanccs: in other words, by cxamining the total information-flow-map within which the utterancc originatcd.

For many purposes, however, this is too stringent a tcst. An cxamincr, for cxample, may framc a qucstion to which he alrcady knows the answer. His objcct is to gain, not the information represented by the answer, but information as to whether the condidate knows the answer. Y'ct the candidatc would be ill-advised to ignore the uttcrance on the ground that the cxamincr was not really asking a qucstion. HIere the form, in its context, is decisive. A propcrly framed cxamination qucstion depicts an inadequacy in the oricntation of an imagin- ary questioner, and the candidate is cxpected to show his prowess by an answer calculated to remedy the inadcquacy in a typical originator.* Wc may perhaps take as our tentative definition of a qucstion, then, a combination of an indication and an incitation: or, if we likc, a two-fold indication, (a) of inadcquacy in oricntation, and (b) of dcsire to have it remcdicd by the recciver.

TIIE MEANING OF A QUESTION

The purpose of an indicative statement is to bring up to date some aspect of the rccciver's state of rcadincss. Con- vcrsely, the main ostensible purposc of a qucstion is to bring The qucstion here is merely bcing "inentioncd' by the cxamincr, and not'used', as it would be by a typical originator. 100

CILAPTER 8

about, as it were by rcnotc coutrol, an updating of the questioner's own state of rcadiness. Hc wants the rccciver to do some organizing work on him. The primary mcaning of a question, then, which we inight call its inlerrogalice meaning, can be dcfined, like the mcaning of an indicative sentcnce, as its selcctive function; but it selects from the range of possiblc oricnting operations on the questioner himself. Its job is to identify the organizing work that needs to be done on the originator's switchboard, so to say. The meaning of the answer will in turn be its selective function-a morc detailed one-on the range of the questioncr's states of orientation. Its job is to sct the switches.

On the other hand, as we have scen, a question also plays an indicative rolc, by simply showing the recciver the in- adequacy of the qucstioncr's state of readiness, together with his desirc to have it renedied. It is therefore worth whhilc to distinguish the indicatice meaning of a qucstion as (for short)its orienting function for the rcceiver. It is obviously quite possible for a qucstion to be intcrrogatively mcaningful while indicatively meaningless, and vice versa. Interrogatively, a question is meaningless when it calls for no orienting work on the originalor; indicatively, it is meaninglcss when it performs none on the receicer.

Thus to ask 'where does the flame go when the gas is turned off?' is intcrrogatively nicaningless as it stands, becausc if we assume that 'flame' ineans 'gas being burned', the two halves of the question call for mutually iacompatible sclective functions. When there is no gas, there is no flame to go anywhere. But it is not indicatively mcaningless, for its uttcrance dors oricnt the receiver with respect to the qucstionr's inuddled organizing system.

REQUESTS AND COMMANDS

We have pictured the asking of a question as offering the receiver access to some of the originator's controls. Conversely, we inay now think of the uttering of a reqquest or cominand as seeking or claiming acccss to some of the rccciver's controls. It is perhaps hardly necessary in detail to go over all the ANALYSIS OF QUESTIONS AND COMMANDS

101

corrcsponding ground. Thc controls in question are now thosc tlhat dctcrminc goal-sctting and action, rathcr than map- making and oricntation. The rclationship is potcntially onc of much grcatcr subordination than that of a qucstioner to his respondent, since a requcst or command (if acceptcd) supplants the process of calculation-in-view-of-goals by which the action would normally be determincd, and on which the response to a qucstion would bear.

Once again, as those with memorics of nurscry (or Army) language know well, we would be unwise to try to characterize a command by its logical form, though of course the'impcrative' if used is distinctive. 'Johnny, I want you to stop banging on the floor'; or (in the United States)'Do you want to pass me the salt?' are cautionary samples of well-understood requcsts or commands to which the response required is not'Oh'or'Yes', respectively, but aclion.

A request or command then, as a communicative act, is basically an indication that action on the part of the recciver is nccessary to remove discquilibrium in the originator: in other words, that the receiver is an intermediate target within the goal-system of the originator-that one of the originator's information-flow loops for goal-dircction passes through him, so that he is potentially under fecdback. Once again, the 'variational' question— what would happcn in the originator's organizing system if the recciver did not act appropriately?-is the reliably diagnostic one, rather than analysis of form or effect in isolation.

Clcarly we must again distinguish two semantic functions for a request or command. As its primary purpose is to select a goal-sctting in the receiver, we may definc its im- peratice meaning as its selective function on the range of the receiver's goal-scttings. Inevitably, however, it also serves to indicate the goal-scttings of the originator, so that its in- dicative meaning may be distinguished for short as its oricnting function relative to the originator's goal-settings.

The usual distinctions between meaning-to-originator, mcaning-to-receiver, and conventional meaning, can be madc in obvious ways in each case. They are of coursc essential if ambiguity is to be avoided. 102

CHAPTER 8

QUANTITATIVE ASPECTS

There is now no difficulty in principle in defining a measure of selective information-content for questions and commands, as for indicative sentences. In cach case we may define it as the equivalent number of independent binary sclective opera- tions specified by the selective function in question.

For many purposcs, however, we may be interested in the form as well as the magnitude of the sclcctive operation; and here, as with indicative sentences, the structure of the or- ganizing system would scem to offer a natural basis for quantification. I have argucd elsewhere19 for a model organized hierarchically, in which 'organizing sub-routines' at a given level arc themselves organizcd by sub-routines at a deeper* level representing morc abstract concepts.

Ifa model of this sort is correct, then an important quantita- tive paramcter of a question will be the order-number of the level of organization at which it betokcns an inadequacy. To take a simple example, a question of the form 'Is 1, B?' is of a lower order than one of the form 'Are all A, B?'. 'Does the road next bend to left or right?' is of lowcr order than 'Is there any regularity in the scquence of bends?'. Similarly the command 'Turn left' is of lower order than the command Turn alternatcly lcft and right'. The sccond selects an organizer of the organizers dealt with by the first.

A second parametcr of great importance will be the logical dimensionality (logon-content) of the question or command, defined as the number of independcnt 'degrces of freedom'of the organizing operation concerned. Thus What is the tem- pcrature?' has an (intcrrogative) logon-content of 1. (Indica- tively it has of course as many as rcquired for identification of the originator's state of inadequacy.)'How has the temperature varied during the day?' has as many logons as there are independent ordinates on the graph required, and so on.

*'Deeper' and "highcr', oddly cnough, sccm to be interchangeable as indices of greater abstractness. ANALYSIS OF QUESTIONS AND COMMANDS

103

With non-numcrical qucstions the actual cstimation of logon-content waits, of course, on our knowledge of the human organizing hierarchy; but the concept may have its qualitative uses even now. For examplc, we can recognize the importance of matching the logon-contcnt of an answer to that of a question. W'e all know that feeling of impatience with an answer that swamps us with data in unnccessary detail, or of frustration with onc that leaves us short of some kcy item. What I am suggcsting is not that numerical measurcs as such would be easy or evcn uscful in such a case, but rather that a quantitative theory of what is going on might hclp to articulate our intuitions and sharpen our recommendations of a remedy in more complex cascs. This, after all, is perhaps the main ser- vice to be rendered by any scmantic theory of communication. It would be of obvious practical importance, for exanple, to ascertain whether Gcorge Miller's 23 'Magic number 7' represents a naximum logon-content for any useful unit- question (or answer, or comnand).

CONCLUSIONS

The main argument of this paper has been that the semantic informational analysis of questions and commands, as of indicative sentences, could be most naturally and least ambiguously carricd out by analysis of thcir organizing function' with respcct to the information-systcms engaged. This requircs a stronger link than exists at present between scmantics and the study of bchavioural organization; and it is not unlikely that the bencfits could be mutual, for the thcorist of organization might well gain significant clucs in rcturn; for cxaimple, from the logical structure of thesauri.

It is of coursc easier to make such suggestions than to carry them out, and I have done no morc than to indicate a few possibilities. IWe have seen how mcasures of selective informa- tion-content, and concepts of mcaning, can readily be de- fined on this basis for questions and commands; and we have 104 CHAPTER 8

singled out thc order-number (can we call it simply the 'order'?), and the logical dimcnsionality or 'logon-content', as two mcasurcs likcly to be important. Wc have also notcdl the imporlance of distinguishing bctween mcasurcs of in- dicative' function and those of interrogative and impcrative function, and betwecn intended, received and conventional meanings and inforination-contcnts.

But I am painfully aware that the bulk of what necd: to be done is little reduced by all this. If it succecds only in stirring up fruitful discussion in a neglected arca it will have served its purpose. CILAPTER 9

Communication and Meaning-a Functional

Approach

FOREWORD

The IVenner-Gren Sympusium on Cross-Cultural Understanding (1962) brought together a group that included anthropologists, biologists, linguists, and philosophers. My brief was to outline the scope of the theory of information in its most general sense, and to consider what light it might throw on the problem of cross-cultural communication. A large section dealing with information-measurement has here been omitted, but the remainder has been reproduced un- abbreciated despite some ocerlap with earlier chapters.

INTRODUCTION

My purposc in this paper is to outline an approach to hunan behaviour from the standpoint of communication science, which may serve as a link betwcen the study of individual man and that of social groups. Since both the human organism and the human group arc systens that 'run on information', it may be of some interest to ask what informational mechanisms may cmbody the processcs that anthropologists study.

Man as a ncchanism is (as we have scen in carlier papers) a telcological or goal-directed system. In a general sense, we Fron Cross-Culural Undrrstanding, edited by F. S. C. Northrop and Helen Livingston, New York, IHarper and Row, 1964，pp. 162-79. Copy- right C 19G4 by Wenuer-Gren Foundation for Anthropological Research, Incorporated. 106

CHAPTER 9

can say that information as to the current statc of his cnviron- ment(including results ofhis own activity)contributcs to the on- going selective process by which his behaviour is organized.19.29 The numerous goals of the human systcm form a partially- ordered hicrarchy, such that many goal-settings are undcr the control of 'supcrior' sub-systems. The setting of such goals, in other words, constitutes a means to a (temporarily or permanently)dominant end. Thus for a solitary man the acquisition of a tool, or the turning of a control knob, may be a sub-goal prescribed by superior goal-dirccted calcula- tions. Since the rank-ordering of sub-goals generally depends on current information as to the state of the field of action, we nced a tcrm which covcrs both the current goal-settings and the' matrix of conditional probabilities' which dctermincs what change would take place if such and such information were reccived. Let us refcr to this as the'goal-complex' of the systcm.

When the cnvironment includes other membcrs of the same (or sufficicntly similar) species, a new kind of possibility cincrges. In addition to the ordinary methods of intcraction, the individual now has the possibility of influcncing his environ- ment by way of another individual, by inducing changes in that individual's goal-complex. This laticr is the process we call communication. Clcarly, it introduces the further possi- bility of back-reaction from the sccond individual to the first, directed towards alteration in his goal-complex. Where this is the casc (as normally in dialogue) it may become logically impossiblc to dissociatc the two goal-complexcs. The individu- als have acquired a relationship in which thcir individualitics have partly merged. They constitute for ccrtain purposes a single goal-dirccted system. For these purposes, it becomes meaningful to refer to them as a social unit.

TIE CONCEPT OF INFORMATION

Human bcings modify one another's goal-complexes in a variety of ways. We make indicative statcnents, ask qucstions, issuc rcqucsts and commands. To summarisc discussions COMMUNICATION AND MEANING

107

presented elsewhere (Chapters 7 and 8), it seems possible to distinguish fairly clearly between the mechanical aspects of such processcs, by looking at their different cffccts on the goal-complexes involved.

Remembering that the goal-complex embodics implicitly a representation of what is believed to be the case', as well as the hierarchy of goals being pursued, we may distinguish between two kinds of change which can be cffected by an utterance: between two kinds of "target' which an individual's goal-complex presents to his interlocutor. The first target is the current map', or reprcscntation of the statc of affairs, implicit in his goal-complex. The sccond is the current content and rank-ordcr of the goal-hicrarchy.

An indicalive utterance is goal-directed towards the completion or altcra- tion of the 'map' implicit in the recipient's goal-complex -i.c. it is uttered as a means of alerting his systcm to the situation indicated by the uttcrance; and any sign that it did not have the required effect on the recipicnt's 'map'would normally evoke further corrective or adaptive action by the originator.

An interrogative utterance, on the other hand, is goal-directed towards tlhe up-dating' of the originator's oun map'. The recipient becomes a link in the forward path of an action-under-feedback, whose goal is the filling-up of an inadequacy in the originator's state of readiness. Of course the utter- ance cannot hclp having an indicative aspeet as well: it alerts the recipient to the inadequacy it reveals in the originator. That this is not normally its primary goal may be seen, however, by asking what would happen if the originator's inadequacy were remedicd without the recipient's rcalising its nature and cxtent.

The way in which analogous functional distinctions may be drawn betwecn other types of utterance will now be obvious, and need not here be laboured. Imperative utterances, for example, have as their primary target the goal-structure rather than the orienting 'map'of the recipient; and so forth.

I have mentioned these tcchnicalities only because I think that a coherent account of scmantics rcquircs us to widen our view of the communicative process (so often discusscd only in terms of source, channcl and sink) to include the wholc pattern of goal-directed activitics within which it plays a part. In ordinary subjcctive tcrms, to have one's 'map' brought up to date is to receive 'information'. 'Information- about-X' is that which determines the form of onc's statc-of- rcadincss for X. In objective terms exactly parallel statcments 108

CHAPTER 9

can be made about the human mechanism, by replacing 'one's' by 'its'. In short, to talk in terms of 'information', 'determination-of-form','map', 'goal', 'state-of-readiness', and the like, provides us with a common conceptual language in which it is relatively easy to make connections between correlated subjcctive and objective data that concern us. Up to a point, we can even frame definitions that can be used interchangeably at the two levels.

The concept of information that emerges in these terms is essentially relative. I have suggested elsewhere that we define 'information', in isolation, as 'that which determincs form'. This definition has the advantage of applying equally well to what 'flows' along artificial cornmunication lincs and what 'passes' between human beings; but it still invitcs us to ask: the form of what?' Conceptually our picture is incomplete unless we specify what information is about -what it represents or betokens. In other words, the concept of information is inseparable from that of meaning.

THE CONCEPT OF MEANING

The purpose of communication being the modification of goal-complexes (in recipicnt and/or originator), it sccms possible to define the meaning of a communication as its seleclive fiunction on the range of possible states of the goal-complex concerned. We could pcrhaps abbreviate this to its orienting function'.

Note first that this too is a relatize concept, allowing cssential distinctions to be drawn (in obvious ways) between (e.g.) mcaning-to-originator and meaning-to-recipient, and between indicative, interrogative and imperative mcanings.

WWe may note further the difference between this definition in terms of selective function, and attempts to definc meaning as the effect produced in the recipient. The cfTect produced by a message may well beloken its meaning; but it would be absurdly restrictive to equate it with the meaning. It may be true that (e.g.) if mcaning is vaguc and ill-defincd, the effect produced is also vague and ill-defined. In that sense many terms that qualify 'meaning' can also qualify 'cffect produced'; but the conceptual reduction of 'mean- ing'to 'effcct' represcnts in fact a confusion between a fiunrtion and the result of its exercise.*

.The point here is related to the distinction made in mathematics between the concept of a (mathematical) function and that of its numerical valucs-a distinction clarified only after much labour by d'Alembert and his successors. COMMUNICATION AND MEANING

109

At the risk of oversiuplification, we might liken the meaning of a message to the 'opcning power' of a key in relation to a given lock. To turn the key has the effecl of opening the lock, but the opening (a change in the lock) merely betokens the opening power of the key, and cannot be cquated with it. Opening power is a property of the key (in relation to that lock) which could in principle be established by inspcction of lock and key, even if the key were never used.

Similar objcctions can clearly be made to the dictum that 'the meaning is the use'. Its intention to be 'operational' is laudable; but it fastens upon the wrong opcration. In the case of our key, the operation required is to look insidc the inechanism of the lock, and scc what would happen ifthe key were used. In the case of a human recipicnt, the corresponding op- eration may well be inpracticablc for good social and surgical reasons; but this is no cxcuse for Procrustean distortion of the conceptual picturc. Not even the most hardened operationalist pretends that all his operations' could be performed in practice: what matters is that they are possible in principle; and in principle (if our notions of the causal organisation of bchaviour are at all valid) the oricnting function of a message (gua potcntial input) could be determined just as readily by advance inspection of the brain, as the opening power of a key by advance inspcction of the lock.

It inay be only fair to point out that what the slogan 'meaning is use'was incant to reject is cqually strongly cxcluded by our present definition- namely, the idea that meating could be defined solcly in terns of the form of the message. While for many purposcs we may discuss the mcaning of recipicnt', it would be philosophical folly to conclude from this that nicaning was an absolute property of an uttcrance, definable without reference to any recipicnt. This would be like arguing that the opening power' of a master key was an absolute property of its profile, definablc without referencc to any lock.

Simply by asking what gives any physical cvent-scqucnce the status of a communication, we can detect the reference to spccific goal-complexcs implicit in cven the most artificial 'languages' of the logician. Thus, for cxample, it is not the rules that give mcaning to the moves in a game of chess. TWhat introduces the clement of meaning is surely the agree- ment of players to abide by those rulcs: that is, to adopt a standard pair of (sub-) goal-complexes. The moves can be said to have their chess meaning (sclective function)only in relation to thosc goal-complexcs. The movement of a black pawn may mcan to the 'white' player a threat, to the 'black' player a relief, and to an ignorant onlooker the displacement of a picce of carved wood. Each reveals his goal-complex (artificial or natural) by the meaning he assigns. In each case, at the mechanical level, we may expcct corresponding diffcrences between the respective 'states of readiness'upon 110

CHAPTER 9

which it impinges, to account for the diverse cffects of the samc physical stimulus.

One final point of great importancc should be noted. Our definition of meaning placcs no rcstriction on the lerels of the goal-complex upon which sclective function may be cxcrcised. Since many sub-goals in the human systcm conccrn intcrnal bodily states (e.g. visceral or hormonal) of which the agent himsclf may not be articulately conscious, it is impossible to regard the full mcaning of an uttcrance to an individual as always coextensive with what he can (evcn in principle) say it means. To say what something mcans to onc is to try to fabricate other verbal sclective opcrators, with identical function; but if onc's power of introspcction is lirnited(as psychologists tcll us it is) then this is only a crude and approx- mate performance at bcst. The sclcctive function of an utterancc for an individual may obviously be pcrfectly well- dcfined, although he can say nothing well-dcfincd about it. It secms important to rid oursclves of the currcnt hercsy that only what can be cxpressed precisely in words has precise mcaning. Once again, we may lack opportunity in practice to observe thhc selective functioning of an utterance on the mechanism cmbodying a human goal-complex; but simply to envisage it in principle should be enough to unscttle any dogmatic restriction of mcaningfulncss to what can be dcscribed in words.

Conversely, it is clear that from our present standpoint an uttcrancc nceds to be viewed as a physical wholc if we arc to make proper scnsc of its semantic function. Important though the phoncmic aspects of the physical stimulus may be, its sclective function for a given recipient has other detcrminants (such as intonation, rhythm, and context or background) which in some cases may conıpletely dominate the operation on his goal-complex. Only our lack of a conventional notation for these other (cqually potcnt) features of uttcrancc can explain the cxtent to which they are ignored, in our legal and social conceptions of truth-telling and lying, for cxample. COMMU.NICATION A.ND MEANING

111

Everybody knows at heart that for some purposcs the phon- emic reduction of an utterancc can be as dangerously inept as a black-and-white photograph of a traffic light. If the investigation of other pcople's idcas is cver to have the status of an exact science, ways must be found to articulate and documcnt all the salicnt featurcs of the communicativc process. There would secm to be no fundamental obstacle to our doing so cventually-or at least doing better than at present-along lincs suggested by our prcsent approach; but to say so is of course to sketch a programme rather than a solution.

FAILURE OF COMMUNICATION

The same analysis that enablcs us to handle the concept of meaning throws interesting light on the different ways in which the communicative process can break doun. As 'failure of communication' must be one of the anthropologist's most common sourccs of frustration, it may be as well to sketch its forimal fcaturcs explicitly from our present viewpoint.

Failure may be partial or total. In every case, it means that the intended and actual sclective functions differ significantly -i.c. sufficiently to transgress the originator's criterion of mismatch'.

Since the originator has the double task of envisaging the goal-complex (the 'lock') upon which he wants to operate, and of designing and emitting a stimulus (the 'key')with the required oricnting function, he can fail if either the 'lock' or his 'key' is significantly different in fact from what he believes or intends it to be. At the worst, his effort can be "incaningless'.

Total meaninglessness can be defined simply as 'alsence of orienting function'(relative to a given recipient). Clearly, we must then distinguish between the mcaninglessne'ss of (a) undrfined utterances (where no structure in the recipient's goal-complex has been pre-established to match the stimuli) and that of(b) illegitimate utterances (where the established selective functions of difi-rent components of an uttrrance are incompatible). Examples of cach respectively might be (a)'the jolks preed'; (b)'the milk is isosccles'. 112

CIIAPTER 9

For the anthropologist, partial breakdown of communica- tion (distortion of incaning) may present the morc sulbtle problcn. Clcarly (in terins of our 'lock-and-key' image) such distortion of thhe intended orienting function can arise from ignorancc of the 'lock', or faulty design and/or use of the 'kcy'. The problems of design and use will not be further claboratcd. Ignorance of the 'lock', however, has two radically different aspects that merit discussion.

First(to drop the metaphor), the originator has to discover and understand the goals and sub-goals of the recipient. Apart from certain major goals common to all human beings, this may present difficulty cnough. Y'et by far the biggest problcm arises at the sccond step-the elucidation of the principles on which thesc goals and sub-goals are hierarchically ordered to form the goal-complex.

I have suggcstcd elsewhere 4.19 that the intcrnal representa- tion of the world of an organism may be thought of as a statistical model of the 'pattern of demand' madc by the world upon the organism. By the 'pattern of demand' I mean not mcrely those features of the world (such as heat and cold)that bear upon and disturb the cquilibrium of the inert organism, but all those that the active organism has to takc into account winen conducting goal-dirccted activity. The suggcstion is that the organising systcm developed to match this pattern of deniand (to do the ncccssary 'taking into account') can ilself serve as the internal representation of the world.

It follows from this (if truc)that the categorics in terms of which the world is pcrceived and conccived of will depend on the various ways in which it has been found to thwart, facilitate and mould the pursuit of the organism's particular goals. Aspccts of the world which call fort]h (or have reccived) no adaptive internal 'matching response' will simply fail to be perccived or conceived of.

The conceptual structurc of the world so perceived will obviously be closely bound up with the structure of the COMMUNICATION AND MEANING

113

organizing systcm. If, for cxample, a regular pattcrn appears in the sequence of demand, then the internal organizcr that is cvolved to 'match' it adaptively will constitute an internal symbol for that pattern. Wherever that pattern rccurs, whether in the input, or in the internal tralfic arnong the organisers themselves, it is likely to arouse this organiscr. The concept which it represents will then be a constitucnt of the new situation as perccived.

Thus, in general, complex situations will tend to find them- selves'matched'(internally represented) by the best possible (hierarchic)combination of the basic organiscrs that previous cxperience of goal-pursuit has cvolved in that individual. Conceptual innovation will not of coursc be impossiblc,21.23 but in the absence of sufficient inccntivc and/or suitable training there are liable to be cpistcmological blind spots in conceptual areas to which no rcadily formed conabination of organisers corresponds.*

Clearly, with a diflerent pattern of past expcrience, or a dillcrent set of goal-prioritics, it is possiblc for onc human organism to have cvolved a single complex organiscr to represent a feature of the world alnost (if not quite)beyond thc conceptual grasp of anothcr, whose organising systcm could cope with it only at the cost of major disinantling and rebuilding operations. Since the same is likely to be truc in rcvcrse, we have here a most potent and subtle sourcc of failure of human communication. The point I would stress is that in thesc situations mcre ostensive dcfinition and exposure to common stiniuli offers no remedy. The two individuals simply do not have the same perceptual expcrience when confronted with the sanic stiniuli, so that ustensive naning could only breed further confusion. Any approach, to be

.Mathematical readers may be reminded of sinilar limitations to the usc-fulness (of (e.g.) Fourirr serics as descriptions of waveforms. Although in throry any waveform can be described as the suut of sine waves, in practice the method becones infinitcly cunbersome for impulsc-typc functions. T'he language of frequency-analysis has a 'blind spot' for the concept of 'sudden change'. 114

CH.IPTER 9

fruitful, must start farther back, by probing the respcctive goal-hierarchics for the disparity of prioritics which has made the conceptual framework of the world turn out so differcntly for cach individual. The participants must not be surpriscd if beyond a ccrtain point the proccss ccascs to be academic and becomcs (in today's jargon)'existential'. For what we have bcen uncovering is one of the relations bctwecn human knowledge and human valucs. T'he goals pursucd in life inevitably condition the ternis in which lifc is perccived and understood. Thcre can be a moral clement in conccptual blindncss.

What then of the implications for anthropology? Evcryonc knows the story of the mcdical missionarics in ccntral Africa who discovered that to disclaini inagical powers was cquivalent to telling thcir tribespcople that they could not help them. But how cffcctivcly can we guard ourselvcs against the samc kind of misundcrstanding in revcrsc? Is it even possiblc in principle? To do so at all thoroughly, we should nced to undcrstand our own goal-complexcs from the outside-and this smacks of 'pulling oncsclf up by onc's own bootstraps'. Pcrhaps in the end the investigator's best hope is to cnlist the aid of his subjccts, in the endcavour to track down his own blind spots. He must rcalisc, of course, that no process of this sort can do morc than change the shapc and location of thcsc blind spots; but at lcast it should Icad to thhc improvemcnt of communication; and at best it may conceptually cnrich onc or both sidcs beyond thcir imagining.

Perhaps a fair illustration might be taken fron thhe diffi- culty, even in his own civilisation, that faccs thc non-rcligious investigator of religious belief. However adcquately he may fcel that he has'tied up' religious practicc in his own catc- gories, he cannot readily ignore thc assuranccs of his subjects that his analysis, whose accuracy they niay not disputc, is missing the point. If genuine religious commitment (as distinct from mcre acccptancc of crcdal affirmations) in- volves the uprooting of a 'sclf-centred' goal-structurc and its COMMUNICATION AND MEANING

115

gradual replacement by a new sct of goal-prioritics, then it is inevitable that, in pursuit of thesc, new catcgories and con- cepts become meaningful and rclevant, even though (in the Christian religion for example) thcy do not nccessarily render the old ones meaningless.

SOCIAL GROUPS AS INFORMATION SYSTEMS

In this concluding section we must glancc at the overall significance of communicative processcs within a social group. By way of introduction to the basic notions, imaginc first two goal-sccking systems of equal power (two thermostatic air-conditioncrs will do) with incompatible goal-scttings, and a common field of opcration. In the ordinary way, each is bound to be driven by its fcedback signal to run cventually flat out' in opposition to the other-one heating, the othcr cooling, so that the tenipcrature lics somewhere between their two goal-scttings.

How could this alsurd and wasteful situation bc rcsolved, or prevented fron arising? In the absencc of a third party, we must imagine one or both systcnis to posscss some kind of additional cflector-system, capable of physical action upon the environment, to be brought in automatically when goal-conflictariscs. The simplest might be a dcstructive weapon of some sort deployed (presumably by cach 'side') witlh the sub-goal of cutting the power to the other, or otherwisc putting it out of action. Given a situation not too synmctrical, one systent could then cmerge triumphant and its primary goal would be attainable.

Suppose, however, that by chancc or ly design, the physical activity of one (or both) succecded in allering the goal-setling of the other. Displaced in onc direction, it would of course make matters worse; but if instead the displacement brought the two goal-settings together, then we would have the beginnings of a wholly different kind of 'resolution'. Instead of being rivals, the two systems could evidently become parlners, 116

CHAPTER 9

sharing the effort of furthering the common goal. The closer the approximation of their respective settings, the greater the economy of total effort.

We can now take up the thread dropped at the end of the Introduction. Consider first the case where onc of two systems (A) keeps its goal-settings totally isolated from outside influence. Here the only mutually viable alternative to deadlock would be the common pursuit of I'sgoals. If, however, the other system (B), though not so isolatcd, has an inbuilt resistance to externally-imposed goal-changes (i.e. evaluates them negatively for feedback purposcs)then beyond a certain point B may 'stick', and destructive tactics may again be the only way out of dcadlock. A situation in whichgoal-adjustment is wholly one way is not fully 'social'. The 'adjusted'member is virtually an extension of the 'adjusting' member.

Consider next, however, the case where the two systems A and B are on an equal footing. Each is open to goal-ad- justment, though each evaluatcs extcmally-imposcd adjust- ment negatively for feedback purposcs. Here a genuincly 'social' situation can develop. Each can pursuc its goals only by taking into account the goals of the other, not only as facts about the world, but as potential members of its oun goal-hierarchy. To the extent that B's goal-directed activity can alter the goals of A, and vice versa, it may become impossible to attribute certain goals to A or B alone. The social unit formed of A+B-in-intcraction becomes a goal- seeking system in its own right.

Clearly, in so far as A and B rctain any individuality within such a systcm, it becomes advantagcous for cach to acquire advance information on the goal-structure of the other. If the cnd-result of interaction must be the mutual adjust- ment of goal-settings, then to prepare some adjustment in advance becomes a positively-cvaluated achievement, by contrast with the negativcly-evaluated status of externally enforced goal-change. The exchange of conventional repre- sentations of goal-structure ('opening their minds to one COMMUNICATION AND MEANING

117

another')becomcs an important social activity. Incrcasing smoothness of rclationship (avoidance of dcadlock and goal- conflict)can result from incrcasing ability to 'convey' (i.e. evoke statcs of readincss for)the outlines and details of the hicrarchic structure of one anothcr's organising systcm. Hence, of course, the importance of congruence between A's and B's basic goal-priorities, noted above. Without this, the proccss of 'touching-up' the recipient's state of readincss to match the originator's may have to be desperatcly indirect and cumbersome, if not impossible.

Once certain basic goal-settings have been approxinated and social goal-pursuit has commenced, cach individual will attach positive value to anything that brings the organising systcm of the other up to date, to match the current state of the field of activity. In short, onc of the goals of cach will be to share information with the other, bringing their respective 'maps' into agrcement. Another will be to share tricks or skills. This mcans inducing the development of similar organising sub-routines in the two goal-complexes. Such sub- routincs may simply organise cxternal effector-action (as in tool-using, climbing, etc.) or they may concern the intcrnal processcs of calculation-in-view-of-cnds (as in solving math- ematical problems). In either case the organisers of sub- routines, once established, take their placcs among the 'conceptual building-bricks' in terms of which the individuals and the social unit form their images of the world.

WWhen the number of members of a social unit increascs beyond two, still another level of complexity opens up. If all could simultaneously adjust one another's goal-scttings into conformity, no special problem would arise; but because of the serial nature of most communicative processcs,what emerges is a self-organizing systcm with internal delays. Such systems are notoriously hard to keep stable. Even with only two members, the familiar exainplc of two people trying to give way to one another on a narrow street shows thhe insidious power of a time-lag to frustrate mutual adjustment. In a 118

CHAPTER 9

large social unit, complctc symmctry is out of the qucstion. IHowever similar the mcmbers may be initially, the problems of organising goal-compatibility requirc some membcrs to take on different rolcs from othcrs if the wholc is to form a stable system. Hierarchic ordering (i.e. asymmctry in relation- ships to prevent vicious closcd loops and deadlocks from forming), and the central coordination of at least some goal- priorities, scem inescapablc.

In such a large group, then, we find oursclves confrontcd with topological problems of sccond order. WWe began by thinking of a goal-sccking system as a pattern or network of interactive elements, which had to cvolve an organising hierarchy in order to cope adcquatcly with a world of hicrar- chically-ordcred complcxity. Considcring the intcraction of two such systcms, we have traccd the ncccssity for communica- tion channcls to develop bctwcen them to prevent dcadlock or mutual destruction. The rcsult of this is the formation of a social unit, with goals assignable to it rather than specifically to any member. IWhen a large number of mcmbers are linkcd by communication channcls in this way to form a goal- directed social network, we find ourselves in many senses back at Stage 1，contemplating (ruefully?) once again the necessity for hierarchic organisation.

There is, however, onc fundamcntal diffcrence. This time, the elements of the system are individuals capable of forming concepts of the system. The conccpts thcy form, in so far as they affcct their goal-complexes, are liable by the same token to affect the nature of the system-and so to alfect their ozen calidity.22a

We cannot, of course, concludc from this that any generalisa- tion regarding a social unit can becomc true (or falsc)if enough members believe it is. IWhat we can affirm, however, is that a gencralisation of this sort cannot be promulgated without exchanging some of its scientific (prediclive) status for an (implicitly or explicitly)normatice one. Like the prc- dictions' of an apprehensive back-seat driver, 'you'll be in the COMMUNICATION AND MEANING

119

ditch in a minute', its scmantic function is to inform,not future expcctation, but present action.

Wc cannot pursue this topic here. I mention it only to warn against over-simple hopcs of what scicntific investigation can do to cstablish prcdictive 'facts' in this arca.

CONCLUSION

We have driven our way up from the Icvel of primitive goal-conflict to that of politics and social organisation, tracing along the way the nmcchanics of communicative processes as far as we could.

Have we donc more than repcat in cumbrous tcrms the commonplaces of the psychologist and anthropologist, with which we have found oursclvcs making contact from tinc to timc? I do not profcss to know. I think the train of development of the prescnt idcas has sccmed at times to have a momentum of its own, suggesting that it might, if followed, lead to genuinely fresh insights into the nature of social organisation; and I am solaced by the thought that this was a task laid down for mc as appropriate to the present occasion. But I inust confess that it scems to mc carly days to en- courage anthropologists to delve deeply into the theory of communication. It is the approach of the information theorist, rather than his theorems and jargon, that may conccivably at this stage have somcthing to offer. My hopc is that at lcast the "flavour'of this approach may emerge clcarly cnough from the prescnt paper to initiate a fruitful discussion. CIIAPTER 10

Linguistic and Non-Linguistic

"Understanding" of Linguistic Tokens"

FOREWORD

During the sumuner of 1963, four symposia comprising a IVorking Session in Afathematical Biology were held at the RAND Corporation. The author participaled in one of these symposia, concerned specifically with questions of" computer comprehension of language."The following short paper was prepared as a basis for discussion. The five participants in the symposiun later co-authored a separale Memorandum presenting some resulls of the discussion and their conclusions.

The present paper explores the distinction between recognizing an utterance, on the one hand, as a"symptom"of the state of affairs in or confronting its originator and, on the other hand, as a linguistic tool. It is suggested that, although only the first kind of understanding is required to enable a computer to accept data and answer questions in cerbal form, such ability is no guarantee of its comprehension of all aspects of language. To attain full linguistic comprchension, the programme must also embody at least a"skclcton representation" of the linguistic context in which an ulterance originates and from which it derives its linguistic significance as a goal-directed operator. By use of this richer model of its situation, a computer should be enabled to meet more sensitice tests of linguistic comprchension.

* Originally a RAND Memo., RM-3892-PR, April 1964.

t M. Kochen, D. M. MacKay, M. IE. Maron, M. Scriven, and L. Uhr, Computers and Comprchension, The R.AND Curporation. LINGUISTIC, NON-LINGUISTIC"UNDERSTANDING"

121

TIIE INADEQUACY OF A"STIMULUS EQUIVALENCE" MODEL There is no great difficulty in programming an artificial agent so that it classifies two sensory inputs as equivalent - so that the flashing of a lamp and the sounding of a bell, for example, evoke the same overt response or set up internally the same state of organization.

In trying to programme such an agent to handle human language intelligently, it is tempting to see the prolblem in similar terms- as one of securing"stimulus cquivalence" between sensory stimuli, represcnting an objcct or a state of affairs, and linguistic stimuli representing the name of the object or state of affairs. The obvious objection to such a simple move, however, is that the reactions appropriate to perception of an object or a statc of affairs are not always or even generally appropriate to perception of its mere name. We do not want our interlocutor to shake in his shoes every time he comes across the word"lion"!

Accordingly, as a second approximation, we might seek rather to secure stimulus equivalence betwcen sensory stimuli, representing a state of affairs, and linguistic stimuli representing assertions of that state of affairs. An artificial agent would then be said to "understand language" if verbal asscrtions, such as, "The cat is on the mat,"or, "This is a square,"had an cquivalent behavioural eflect to that of an optical or other sensory prcsentation of the state of affairs described-cither evoking appropriate responsc or contri- buting an appropriate item to its" cognitive map."

IVithout denying that a performance of this order would be adequate for many practical purposes, the aim of this brief paper is to show that it falls short of human understanding in a critical respect-but one that docs not seem beyond mechanical remedy.

PERCEPTION VERSUS LINGUISTIC UNDERSTANDING

As long as the linguistic assertions offered to an agent are true and unquestionable by definition, it is possible to miss 122

CHAPTER 10

or paper over the differences between perception of states of affairs and linguistic undcrstanding of dcscriptions of them. Thus, in the simplest chess-playing programmcs, no essential distinction can be made between the computcr's "pcrceiving" the contents of (say)a chess-board by sensory means, and its "being told" them verbally. The author has even been assured by one designer that it made no diffcrence to hirn or his machine whether the internally stored represcntation of the board was set up by an optical input via a "pattcrn-recogni- tion"routine, or by a typewritten input in ordinary English via a word-recognition" routine, or by direct feed-in from a suitable punched tape to the storage rcgisters. Thesc were all equivalent channels of communication betwccn the board and the computer, and if the linguistic channcl functioned success- fully the computer must be admitted to"understandlanguage." Any doubts on this score were to be dismissed as shcer"meta- physics."

At first sight there might seem to be a justification for this argument in certain human situations. A blind man, for example, may come to trust a human guide so implicitly that he virtually perceives through his guidc's cyes, and the guide's words become barcly perccived intermediarics in the channel of surrogate-visual communication. An aircraft pilot being talked-down in fog may be in a similar situation. Here we would agrec thhat the sounds coming from the guide's mouth could, in principle. be replaced without loss by "bleeps" or othcr mechanically generated symptoms with the same indicative function, and the distinction between linguistic and non-linguistic undcrstanding would evapo- rate.

All that this proves, however, is that for certain purposes an indicative linguistic form can have the same function as a non-linguistic symptom of the state of affairs indicated; it does not begin to prove the converse-that to understand an indicative uttcrance means no more than to rcact as to symptoms of the state of affairs denoted by it. LINGUISTIC, NON-LINGUISTIC"UNDERSTANDING"

123

The issuc bccomcs clearcr when we considcr cascs in which the actual state of affairs is found not to corrcspond with what is assertcd in an uttcrance.

TIIE INTENTIONAL CHARACTER OF LINGUISTIC

UTTERANCE

Our scnses normally enjoy at lcast as much confidence as our human intcrlocutors; yet our senscs also can mislcad us. When this happens we call it a distortion or an illusion, and explain it in tcrms of passive mcchanical limitations or faults in our sensory apparatus. If a man says,"My eycs deceived me," we recognize the mctaplorical usage, and do not impute any molication to thosc organs. The samc applics a forliori if we arc misled by symptoms from inanimatc appara- tus, or other physical clucs, as when we say, "The fog deccived me into taking the Town Hall for the Post Officc."

If a linguistic uttcrancc turns out to have bcen mislcading, we can of coursc takc a similar attitudc. If thc blind man's guide says Ic is in the Post OfMice and he finds hc is in thc Town Hall, for cxample, he may simply ask, "How [i.e. by what causal scqucnce] has this situation ariscn ?"-just as if he had been using an inanimatc blind-aid. In this case, howcvcr, there cxists also a quitc different kind of qucstion: he may ask, IW'hy [i.c. for what purposc] did you say that?" This kind of rcaction would be mcaninglcss in relation to his cycs, or in rclation to a telcvision link, or any other "motivc- Icss" collcctor of clucs to his whcrcabouts. It points to an aspect of linguistic understanding which diffcrcntiates it from merc interprctation of symptoms. In a word, to perccive an uttcrancc linguistically, rather than symptomatically, is to perceive it as inlentional in form. Whether or not it be uscd as such on a particular occasion, a linguistic uttcrance is a tool. Language is not fully understood by any cntity, whcther natural or artificial, incapablc of percciving this aspcct of it. Wc can if we wish takc this point in two stagcs. The word "lion," we say, denotes the creature. This denoting function is 124

CHAPTER 10

often taken as characteristic of a linguistic token, as distinct from a mere symptom, such as the smell of the lion, the sound of his roar, or the imprint of his paw. Well and good (at least in relation to objects). But how to explicate the notion of "de- noting"? Inevitably, in the end we have to go back to the context for which linguistic tokens were invented-the situation in which one individual wants to adjust the "state of organization" of anothcr, and uses combinations of tokens as tools to that end. Thus, althougl full linguistic understanding of an expression is possible without any rcfercnce to the in- tentions of a particular originator, onc aspcct of it will be beyond any entity incapable of understanding the concept of a tool, and what it means for the expression to be used as such.

Operationally, the notion of "intentional" here admits of mechanistic explication on the same lines as other notions related to "goal-directed,""purposeful" action-in terms of a "variational" criterion.14.15,24 We define a state of affairs X as the aim or goal of an agent A, if A is so organized that any received indication of "mismatch," betwcen the actual state of affairs (say Y) and X, would evoke a search for action (or preparations for action) calculated to reduce the mismatch.* By calling an ullerancé intentional, we imply that its form has been calculatcd with a view to a goal — namely, the detcrmination of somc aspcct of the state of organization of some recipient (known or unknown).

For a recipient to be able to understand this intentional charactcr (whethcr or not he attributes the intention to the current user), his information system must be equipped to represent not only the utterance and what it says, but also its functional significance-which implics the ability to represent it as something designed to be uscd by an originator, similar in linguistic repertoire to the receiver, to achieve a particular end. Without going into detail here, it is clear that this requires internal activity over and above the filling out of a "cognitive * If the aim were to avoid X, "reduce"in the foregoing sentence would be replaced by "increase,"or"maintain above some minimum." LINGUISTIC, NON-LINGUISTIC"UNDERSTANDING"

125

map"in accordance with what the utterance says, as if it were no different from the reading of somc instrumcnts. Complete linguistic comprehension will dcmand internal representation (at least in skeleton form)of the goal-directed feedback loop within which the uttcrance functions or could function-just as understanding of a hammer as a tool (and not merely a lump of matter) would demand some skeleton representation of its function. In cither case, of course, the recipient's own goal-pursuing mechanism could serve as a represcntational surrogate.

Understanding the use of an cxpression by a particular individual in particular circumstances still more clearly requires the system to be capable of modelling the originator as goal-directed, especially if the utterance is directed to the recipient. (One operational implication, for example, will be that if a recipient R, having correctly perceived the intended function of an utterance by originator O, were not to conform to O's intention as perceived, R's system should be to some extent prepared for O to initiate. corrective action, or in some other way-now or in the future-to evince the frustration of his intention (sce Chapters 7 and 8).

SYMPTOMS VERSUS DESCRIPTIONS

A further objection may however be raised to our line of argument. If the originator, though human, can be treated as a physical system, surely once his goal-directing networks have been taken into account there is no difference in principle between the evaluation of his linguistic utterances as clues to the state of affairs giving rise to them, and the evaluation of the pcrformance of some non-linguistic channel, such as a fire alarm, or a barking dog, or a television system? In each case there may be distorting factors to be discovered and allowed for; aftcr all, even a TV channel may reverse black and white!

It can be conceded at once that the linguistic output of an originator whose goals and behaviour pattern are known and 126

CHAPTER 10

stablc could in principle be treated thus: simply as a succession of symploms of the state of affairs, intcrnal and cxtcrnal, that gives rise to them, from which the infcrence to that state could proceed on the same principle as from any other caus- ally coupled symptoms (ringing bells, barking dogs, or spots of light on a TV screen). Our argument has not bcen that this is impossible, but simply that it leaves out an cssential aspect of linguistic understanding. It is precisely the difference between treating an utterance as a symptom, and recognizing it as an intended description of a state of affairs, which differen- tiates most clcarly the non-linguistic from the linguistic aspects of human communication.

In the special case of dialogue, however, there is a still stronger answer. The significant feature of dialogue between two agents who understand language in its intentional aspect is (as we have indicated) that in principle the goal-settings of an originator may not bc treated as (all) fixed —for his goal strategy will in general depend from moment to moment on the way in which the recipient responds to his utterance. We have, in short, a situation of potential goal-conflict. If sufficiently symmetrical, it may in principle preclude either party from acquiring a full mechanical specification of the other, since the mutual backcoupling can systematically invalidate the attcmpt on either side (sce Chapters 9 and 13).

In such reciprocal interactions, then, we can say categori- cally that a complete analysis of utterances as symptoms would be logically impossible for the interlocutor (though not necessarily for a dctached onlookcr with access to their in- ternal workings). When we speak of the linguistic understanding revealcd by human beings in such situations, therefore, we are clearly talking about something clse, for which mcre interpreta- tion of symptoms docs not in this caseoffer a livealternative.

CONCLUSIONS

Our main aim has been to show the operational reality of a distinction, often vaguely alleged, betwveen the level of LINGUISTIC, NON-LINGUISTIC"UNDERSTANDING"

127

"understanding of language" required in a device for the mere acccptance and emission of information in verbal form, and the understanding of language enjoyed by human beings.

Our conclusion, however, is not that artificial agents must be incapable of understanding language in the fullcr human sense. On the contrary, we have glimpsed what seem to be key features of the neccssary mechanism, and the possibilities opened up are richly interesting enough to be explored in more detail clsewhere.

What seems clear, however, is that computer programmes for "language comprehension"which embody no perception of its intentional aspccts do not show an understanding of language in the full sense that human bcings do, and that without certain additional capabilities-notably the ability to embody a skelcton representation of the goal-directedness of their interlocutor and his aims in using words-they cannot fully do so. It is cqually clear that, for many limited but im- portant practical purposes, they need not. CHAPTER 11

Comprehension of Utterances-Some

Concluding Notes"

Utterances are exchanged between agents as a means of: (a)initiating, modifying, or confirming one another's actions (overt or internal) or conditional readiness for action;(b) evoking emotional or other expcriences. The target of an utterance may be: (a) the recipient's "map" of the world (i.c. what he reckons with as fact or possibility in planning and executing action); (b) the recipient's normative system which determincs the conditional priorities of various norms and goals, and actions directed thereto; (c) the recipicnt's (or just the originator's) sensory-aesthetic or other systcms not dircctly concerncd in the organisation of action adaptive to the cxternal world (e.g. certain aspects of poctic utterance, ctc.).

The meaning of an utterance (intended, standard, or re- ceived)can be defined as its selcctive function (intendcd, standard, or actual)on the range of possible states of the appropriate system. Thus, mcaning is defined as a relationship, not an absolute property. An utterance is meaningless if it has no selective function (for one reason or another)on the appropriate range. IWe have to distinguish between meaninglessncss due to: (a)lack of definition of selective function (e.g.nonsense syllables); (b) absence of the appropriate range in recipient (e.g. "colour" to a blind man); (c) incompatibility of two Originally an Appendix (by D. M. MacKay)to "Computers and Comprchension," RAND Mcnio. R.M.-4065-PR, April 1964，by M. Kochen, D. M. MacKay, M. E. Maron, M. Scriven, and L. Uhr. COMPREHENSION OF UTTERANCES

129

or more components of the selective operator (e.g. the milk is isosceles").

Clearly, utterances can be partially meaningful (or meaning- less)under the above heads.

In this framework, misunderstanding can be defined as discrepancy between intcnded or standard and received selec- tive functions. Note, however, that this is the passive sense of misunderstanding (e.g. "a misunderstanding exists")rather than the active sense (e.g. "you are misunderstanding me"). To misunderstand is to perceive an utterance as calling for an adjustment of organization discrepant with that intended or purported.

The last sentence emphasizes that the effort to understand an utterance is an effort to match the rccipient in some sense to the originator; i.e. it presupposes an intention in the originator and an awarcness (explicit or implicit) of this by the recipient. IWe must beware of any bchavioural tests of understanding which omit to test for this.

An utterance as undcrstood by a recipient has two distinct aspects- its form and its weight.

The first determines the form that the recipient's organizing system would assume if the utterance were fully accepted; i.e. if the selective operator it defines were fully applied to the organizing system.

The second determines the actual degree of coupling betwcen the internal representation of this selective operator in the recipient, and his organizing system.

We thus picture the receipt of an utterance as a two-stage process, somewhat like the construction of a patch-board followed by the decision to plug it in-but different in that the final coupling need not be all-or-none.

In these terms, we can briefly characterize the under- standing of a variety of utterances.

(a)A statement is aimed at the recipient's map-making system. Its received weight (the extent to which it is allowed 130 CIHAPTER 11

to determine the form of the map)depends on the recipient's evaluation of the originator's goal in uttering it and of his reliability as a source (e.g. he may ask, "Is he trying to deceive me?"-"Does he have access to necessary data?").

(b)A command is aimed primarily at the recipient's norma- tive system. It is calculated to secure action of a given form by altering the goal-priorities, rather than by mere physical reflex stimulation, of the recipient. Its perception as a command requires recognition that the recipient is in principle under feedback from the originator, with equilibrium dependent on his taking the required action. Its weight depends on the extent to which disequilibrium here is negatively valued (i.e. to ask, "What if I were to disobey?" would be relevant).

(c)A request differs from a command in relying for its weight upon the positive value (to the recipicnt) of satisfying the originator, rather than evoking mere negative avoidance of disequilibrium with him.

(d) A question is aimed formally* at updating the originator's own organizing system, by way of the recipient. Questions may be regarded as requcsts (or commands according to their form or tone) to construct a linguistic tool with the specified updating function. Their weight is thus derived in an analo- gous manner to that of requests and commands, with the added consideration that for many pcople the updating of others is a positively-valued activity in any casc.

(e)An instruction differs from a command in specifying not an action or a goal, but a programme, whose goal may be only conditionally named, if at all (e.g. "To reach the house, drive five miles north on route 1, then two miles east on route 50").

(f)A warning is aimed at the recipient's normative system by way of his map. It presupposes a coupling (usually ncgative) be-

Examination questions mercly require the recipient to answer asif the examiner needrd to be updated. COMPREHENSION OF UTTERANCES

131

tween the internal representation of what the warning indicates and the evaluatory system which determines goal-priorities (e.g. an air-raid warning). Its effective weight depends both on the strength of this coupling and on the recipient's evalua- tion of the motivation and reliability of the originator.

(g)Advice, in general, may include instructions and warn- ings. It is characterized, however, by the implicit or explicit conditional, "If I were in your place ..."The weight claimed by advice thus depends on the extent to which its originator believes himself to have adopted the recipient's goal-structure, etc., when constructing it. The weight actually given it by the recipient will then obviously be calculated from his evidence on this point, as well as from the intelligence, knowl- edge, etc., he attributes to the adviser.

(h)A promise is aimed at the recipient's map of the origina- tor's goal-settings. It indicates not only that the originator shares the recipient's goal named in the promise, but also that he recognizes himself in principle to be under fecdback to the recipient in this connection (as in the case of commands).

As argued in Chapter 8, all utterances also have an indica- tive function, whether or not they are conventionally aimed at the recipient's cognitive map. Thus even a question or a command indicates implicitly certain presuppositions on the part of its originator. Undcrstanding of these indicative aspects may be symptomatic or linguistic or both, and need not coincide with understanding of the conventional (interroga- tive, imperative, or other)aspect. A question such as "How long have you lived in Mexico?", for example (addresscd to someone who ncver has), can be indicatively understood and replied to appropriately, even though it is interrogatively nonsensical. CHAPTER 12

Generators of Information"

FOREWORD

This paper and the following one represent something of a digression, and for this reason find themselves at the end of the collection, out of chronological order. In the first we are back in 1952，wrestling with the relation betucen information and noise and considering in what circumstances events determined (in part) by random noise might be said to generate information. In the second, written by request on a similar topic eleven years later, the main emphasis is on a new point. Over and above any indeterminacy due to physical randomness, it is argued that interlocutors in dialogue hace an irreducible logical indeterminacy for themselces and for each other. This would give their behaviour an irreducible selective information-content for one another ecen if their brains were as physically determinate as clockwork.

INFORMATION AND NOISE

The communication engineer is normally conccrned with information on the move'. He takcs his stochastic proccsscs as they come, and his task is to map them on to a receiving field as efficiently as possible.

In this paper our attention will ınove one stage farther back, to inquire into the conditions under which information may be said to arise, and to discuss in particular the kinds of *Comnuunicalion Theory, W. Jackson (ed.), Academic Press, New York, 1953, 475-85(copyright Academic Press). GENERATORS OF INFORMATION

133

mechanism that could produce 'original' information in the same sense as a human being is said sometimes to do.

Any question of this kind is bedevilled by the multiplicity of complementary senses in which the term 'information'can be used. From the standpoint of information theory, in- formation is defined, in general, as that which causes or logically validates reprcsentational activity-activity in which a structure, purporting to represent something else, is produced or augmented.

This operational definition admits of as many subdivisions as there are distinct classcs of representational activity. The reader is referred to the explanatory glossary (Appendix) prepared for a previous symposium for a fuller discussion of the resulting terminology. IIcre it must suffice to remind oursclves that correspondingly different measures of amount-of- information or information-content offer themsclves according to the aspect of representational activity considered. If we are interested in the actual form and content (the so-called semantic aspects), the indices of metron-content and logon-contcnt are relevant. If only the uncxpectedness of the activity is of interest irrespective of its scmantic significance, then it is the minutencss of the selcction made from the ensemble of cxpccted possibili. ties which is taken as an opcrational index of information-content. This, under the varying names of 'sclective information-content', sclective entropy', 'ncgentropy', or even simply entropy', is the important bulk measure'of information-content used in current communication theory; and it is this measure that we shall have in mind in what follows. By adopting it we imply that we regard the representational activity in which we are interested as a succession of sclective opcrations on an ensemble of possible representations. Since in fact wc shall be concerned with symbolic or pscudo-symbolic) activity, this standpoint is appropriate.

A final cavcat may be entcred against the linguistic crror of confounding 'information' itself with one or another of thesc measurcs of "information- content'. To do so brings the same retribution as would the confounding of'electricity'with 'voltage'or 'amperage'.

Since the notions of noise and randomncss will be pivotal in later discussion, it may be provident now to seck to clarify their relationship to the notions of information theory.

The communication engineer, being concerned ultimately with the faithful reproduction of a mcssage, measures its information-content by its mathematical unexpectedncss. If, therefore, he is asked to reproduce a given 'white-noise'or 'random' signal that he knows to be equally likely to select any one of the ensemble of possible statcs of his channcl, and thus to place the greatest demand on his channel capacity, he 134

CHAPTER 12

will estimate such a signal to have the greatest selective information-content for him per unit of time, irrespective of its apparent senselessncss. However senseless a signal may seem, he is always politely ready to believe that it has operational significance for the ultimate recciver, i.c. that it represents some selective operator on the ultimate recciver's ensemble of significant representations. This docs not of course mean that the receiver in fact carries out selective operations of corre- sponding magnitude, but only that he could do so if the signal were a member of some optimal ensemble of code signals agreed upon with the transmitter. In short, the selective information-content of a signal for a receiver has no direct connection with that for the communication engineer re- sponsible for its passage.

On the other hand, any noise produced in the channel itself counts as negative selective information, because it is pre-empting part of the selective power of the channel and leaving only a residue for the desired signal. In fact, the badly phrased question, 'Is noise information?' exemplifies well the need for 'semantic hygiene' in this field. The question is incomplete. If translated, 'Has noise selective power?' it invites the immediate rejoinder, 'On what ensemble?' To specify the ensemble then removes all the ambiguity and obviates empty debate.

Implicit in the estimation of information-content in terms of selective power there lies a further assumption of communica- tion theory, namely that knowledge of the code is free infor- mation for the receiver. To forget this is to invite apparent paradox. For example, if one out of a row of eight equiprob- able letters ABCDEFGH is selected for me by 'successive halving'(as, e.g. C would be selected by 'left', 'right', 'left'), it is commonly assumed that I am left with only three bits of information. But I was able to interpret 'left''right''left'as C only because I knew also the order in which the eight letters were arranged. I shall need more than three bits of channel capacity to transmit this information to someone GENERATORS OF INFORAIATIO.N

135

else, unlcss I am sure that he has sct up an ensemble of letters in the samc order.

Thesc considerations are of course a commonplacc of practical communication, but arc sometimcs forgotten when attempts are made to measure information-content'in other contexts. The gencral point is thhat even the uttcrance of a single two-valued proposition represents two selcctive operations:

(1)The choice as to which proposition to asscrt or deny.

(2)The choice to assert or deny it.

Communication has been effected, and information is meaningful, only in so far as both selective opcrations have been performed by the recciver.

SOURCES OF INFORMATION

What, then, constitutes a 'source of information'? WWe have seen that any stochastic process which somebody wants to reproduce elsewhere makcs demands on the information capacity of the cngineer's channel, and is thus, by his definition, an information source in a technical sensc. It is a sourcc of surprise. If we accept the definition of information as that which logically validates representational activity, it is undeniable that even a noise gencrator or a random number generator is a source of information in such a case.

Our instinctive objection to this statement reflects the fact that in such a casc no agreed code exists according to which the noise signals could induce us to makc any sclective operations on an ensemblc of significant rcpresentations, in particular on the ensemblc of our own possible responscs. In effcct we want to distinguish between signals with surprisc valuc and signals with mcaning. It may be a pity that communication theory has attached the notion of information so exclusively to the elcment of surprisc, though the engincer can hardly be blamed for assuining the meaningfulness (to someonc or other) 13G

CHAPTER 12

of what comes to his transmitter. One might perhaps try to rigorize usage by drawing the following distinctions:(a)a noisc gencrator, like any unprcdicted scqucncc of cvents, is a source not primarily of information, but, if we must call it a source of something, simply of surprise; (b) it becomes a source of information if and in so far as it leads to representa- tional activity, and its 'output of information' is to be mcas- ured relativcly to the enscmble of reprcscntations on which it cvokes sclective opcrations; (c) a source does not, however, produce significant information unlcss the representational activity evoked has significance for somc recciver.

Thus, for example, a classical monkey on a tcletypewriter would probably make heavicr demands on channel capacity than a human uscr; represcntational activity would ccrtainly occur at the receiving telcprinter, and in a technical scnsc 'information has bcen transmitted'. But becausc the classical monkey sends scquences of letters normally devoid of any agreed sclcctive function for a human rccciver, the latter could without contradiction statc that he reccived no signifi- cant information from them. His private reprcsentation of 'that which is the case' has not been significantly altered.

In short, selcctive information-content docs not mcasure a 'stuff' like water, or elcctric charge, but a relation (sclective power)between a signal and a particular ensemble of represen- tational acts of response. 'S is a source of information' is thus an incomplete sentencc. It must always be complctcd (even if sometimes implicitly)in the form, 'S is a sourcc of information to receiver R'.

Classifying a few typical stochastic processcs undcr these headings, we may rcgard atomic disintcgrations, valvc noise, Brownian movements, random nuinber gencrators, and the like, as 'sources of information' only in the technical sense. They are not normally (except perhaps in cxpcriments of the 'table-turning'type!) generators of significant information.

A source of significant information, as we have scen, must be capable of embodying and abiding by an agreed code or GENERATORS OF INFORMATION

137

symbolic calculus. Can we conceive of a mechanism capable of generating (and not mcrcly reproducing)significant information in this way? Such must now be our inquiry, which may perhaps cast somc intercsting sidclights on the corresponding processcs in the human bcing.

CONCEPT-HANDLING ARTEFACTS

We are familiar in these days with artcfacts* such as digital computcrs which are capable of handling suitably coded logical data, and performing logical deductions. Such artcfacts abide by an agrecd symbolic code, and it is natural to ask whcther they are not sourccs of significant information of the type we are sccking. Unfortunatcly, the strict logician would corrcctly maintain that such computing deviccs arc merely transducers of information supplicd to them by thcir users, and that sincc their output could in principle be predicted completely in advance, they gencratc no sclcctive information whatever.

We might plcad that unless we carry out the predictions we may well be surprised by their output, and in fact receive a grcat dcal of information. This may be conccded. In fact a computer designed for example to play chess might be con- sidcred to engage in meaningful dialogue with a human opponcnt. As long as its choiccs wcre all logically dctermined uniqucly by its data, however, it would be gencrating no sclcctive information, but only reflccting back to its opponcnt the logical implications of the information it reccived as to his last movc. It would, as we say, 'show no originality'.

Now we have scen that a noisc gencrator can bc rcgardcd as a source of completcly original but meaningless information. A logical computer per contra provides completcly unoriginal but rigorously mcaningful information.

.In the sense of 'artificial coutructs', used to escape the associations of the word 'machine'. 138

CIIAPTER 12

It is natural to ask next whether onc could not somehow combine deviccs of the two kinds in such a way as to generate processes at once original and meaningful. Two broad divisions of possible policy are apparent. (a) We may use noise genera- tors to perturb selected functions of a detcrministic logical artefact, or (b) we may devisc an artefact whose elements function statistically, with an inherent but limited indeter- minacy. While the two classcs of artefact so devised could be made behaviourally cquivalent, we may note in passing that there are important philosophical distinctions between them, which nccd not dctain us herc.

It is not proposed to discuss class (a) in detail. Some of the possibilitics of making intelligent use of 'noise' in an artefact dcsigncd to take account of both structural and mctrical aspccts of information (in the scmantic scnse)have already bcen outlined by the author.11(Papcr hcrcafter rcfcrred to as CDA.*)The thesis has since been developed in more gencral terms along the lines of (b).14.15

The crucial feature of artefacts in both the above classes is the introduction of mctastable clements having effectively a variable probability of excitation governed by an input (prefcrably, though not csscntially, a continuously- variable quantity such as bias-voltage, chemical concentration, or the likc) that is in gencral quite separate from the normal cxcitatory input. Thus in class (a), the introduction of random perturbations of "threshold'(e.g. by supcrimposing noisc on the variable cathode-potential of a thyratron)can cause the probability of excitation in response to a given signal to vary smoothly betwçen 0 and I as the mcan threshold Ievel is raised and lowcred. In class (6), elements would be used whose responscs to a given signal depended on intcrnally fluctuating paramcters of statc, as well as on an adjustable bias-level, so that again the range of the latter would cover all possibilitics from the complete inhibition of response to the gencration of spontancous activity at an adjustable frequency.

Dctails of mechanism need not here conccrn us. The basic point is tliat if an artefact is cquipped to reccive and handle and respond to information which is incomplete, by adjusting the relative probabilitics of spontancous changes of statc of its internal reprcsentations according to the probabilitics implicit Relcvant portions of this outline (originally circulated in minco- graphed form) were reproduced as an appendix to the paper presented at the Symposium. GENERATORS OF INFORAIATION

139

in its information, then its activity, while not normally unreasonablc, will frequently be unpredictable in a sense as fundamental as we care to make it by our choice of noise source.'

If, then, the artefact is equipped to handle meaningful symbols according to the rules of normal syntax, its rcactions to a human interlocutor in the ficld of discussion so symbolized may frequcntly amount to the gencration of new information -ncw ideas, for example, tentativcly advanced, yet nor- mally possessing finite chances of meaningfulncss by virtue of the guiding probability configurations under which they have originatcd.

It may be helpful to compare this process with Shannon's statistical method of approximating to English sentences.31.33 By arranging that the relative probabilities of his choiccs of English words reflccted the statistical structure of spoken English, he was ablc to secure a high probability that a ran- dom mcthod of choice would produce meaningful English sequences. Our artefact in effect uses thie same method for disciplining' spontaneous activity into 'making sense', but has as its statistical guide the totality of its current and stored informational input. Its output thus promiscs not mercly meaningfulness but relevance to the dialoguc in proccss.

CODE-GENERATING ARTEFACTS

Thus far our artefacts have had no responsibility for the code in which thcir discourse is framed. Thcir concepts are thosc which we have cquipped them to symbolize. We may reasonably reserve from them such admiration as we might accord an original thinker, until we are convinced that an artefact could originate not only new ideas in terms of old concepts, but new concepts ab initio.

We mist once again be content with only a brief outline of ideas presented in more detail elsewhere;14.15 but mention 140

CIIAPTER 12

of the basic principle will doubtless suggest all the more intercsting possibilities readily cnough.

The key to the design of mechanisms capable of forming their own symbols is the possibility of valuative feed-back on transition probabilities. As this is also a possible key to all analogous problems of self-organization, one may perhaps be forgiven for elucidating it in terms of a simple model, originally constructed to illustrate some points made in CDA. This model has of course no pretensions to animal status, and justifies its existence solely as an explanatory device.

The model, illustratcd in the figure, is made up of three identical units (the number is unrestricted in principle)each comprising a thyratron V which can actuate an electro- magnetic gate G so as to drop a ball-bearing from an aperture A over a two-pan balance B. B is mechanically linked to a potentiometer P, which governs the bias on thyratron V. The anodes of all thyratrons are supplied from a common capacitor C charged through a resistor R.

GI

Ga

G

At

d3

43

V.

v,

I

Pa

Ps

B

Fig. 1. A simple probabilistic artefact illustrating valuative feed-back on

probabilities of excitation

If now Cis allowed to charge slowly, the thyratron with the lowest effective bias, say V, will tend to fire first, discharging C and relcasing a ball from A. Normally this will fall into the right-hand pan of B, causing Pn to rotate and increase the GENERATORS OF INFORMATION

141

bias on V. Thus the norinal effect of a thyratron's firing is to reduce the probability of its firing next timc.

If, however, a target T is placed under d so as to deflcct any balls from A, into the left-hand pan of Bn, the oppositc cffect will occur. The succcss of the modcl in striking the target when V. fires will increase the probability that it will use V, next time.

Evidently, no matter how the biascs on different V's arc set initially, the modcl will tend to an cquilibrium statc in which only the thyratron V, fircs and T is always hit. If morcover we move T to a ncw position, m say, the model will gradually 'unlcarn' its original 'sct' and cventually will be found firing only Vm.

In this examplc randomncss is introduccd only by the fluctuations of the thresholds of the various tlhyratrons, and the 'valuational fced-back' is quantized and rathcr inflcxiblc. It illustratcs cven so the basic principle, whercby an artefact alters the transition probabilitics governing its own activitics according to its cxpcricncc of their relativc success (judged by some gencral critcrion)and diminishcs by a kind of 'natural sclcction'the probabilitics of all cxcept those which have been succcssful often cnough.

Extensions of the principle in all dircctions will now be obvious, and only one need be mentioned. If in practice the target Tis not stationary, but moves albout from position to position in a stationary time scrics, it is casy to arrange the fced-back systcm so that the relative probalbility of firing of the nth thyratron V. tcnds automatically to cqual the rclative frequency with which T is in position n. The artefact is not now playing an 'optimum game', but it has in effcct madc a symbol for an abstraction, namcly the first-ordcr statistical structure of the time serics of positions of T.

Such a symbol is not indeed recognizable as a code group of impulses, but is constituted by the configuration of thresholds of the Vn. In quite a literal sense, the artcfact is symbolizing its(statistical) expectation of what T will do next. 142 CHAPTER 12

Along lincs such as thesc onc can envisage an artcfact capable of forming internal 'symbols' for any rcgularity in the flux of its expericnce, by adapting its 'statc of readiness' to match the rcgularity. The symbols are in fact the threshold configurations responsible for its rcadincss to make the corre- sponding ınatching responses, and, as we have seen, it is possible for an artefact to grope its way' towards the formation of such configurations, if necessary 'from scratch'.

The proccss would of course be grcatly accelerated by cven a modicum of instruction such as a child is givcn; and if the symbols arc to corrcspond to communicable idcas, such instruction (i.e. valuative fecd-back from an cxtcrnal inter- locutor)would be almost indispensable. The point rcmains, however, that such a probabilistic artcfact would always have the power of 'noticing'(prcparing a symbolic statc of rcadiness for)a ncw regularity never bcfore named; and the regularity so symbolizcd nced not always be an abstraction from the flux of incoming data, but may represent the outcome of some spontancous internal scquence of trial and error at the con- ccptual lcvel.

Pcrhaps enough has now bcen said to justify the following summary:

(1)An artefact can be cnvisaged in which activities are of two types, (a) actions (intcrnal or external), (b) adjustments of probabilities of actions. By valuative fecd-back the rcsults of (a)can evoke (b) so that the 'state of readiness'of the artefact -the total transition-probability-matrix (or t.p.m.)-forms in cffect a representation of those rcgularitics of its experience to which it has succcssfully responded.

(2)Such an artefact can not only generatc information spontaneously, but can also form symbols for new concepts excmplificd cither in the flux of its incoming data or in the train of its intcrnal spontancous activity. In cither case the probability of meaningless or unprofitable activity would seen in principle to admit of indefinitc and automatic reduction. GENER.ATORS OF INFORAIATION

143

(3)While all information is thus stored on a long-term basis in the form of the thrcshold configuration detcrmining a t.p.m., the running symbols of a current 'train of thought' will of coursc be the trains of internal activity (at onc or more levels)governed by the corresponding t.p.m.'s.

HUMAN INFORMATION-GENERATORS

Tlhe sidelong glance which we now cast on human proccsscs of thought must be very tentative. We naturally fecl inclined to ask whether human originality may not depend in part on random physiological processes disciplined in a comparable way by the t.p.m. of experience.

At the timc when CDA was written, the digital computcr was in popular vogue as an analoguc of the brain (despite the protests of most physiologists) and an cmphasis on the impor- tance of randomness was unpopular among theorizcrs. Whethcr their opposition was stirred more by the mathematical or the metaphysical inconvenicnce of such considerations is doubt- ful, but in any case the evidence now scems overwhelming that neural processcs could occasionally be subjcct to signifi- cant perturbation by random fluctuations in metabolism and other factors, particularly at any 'switch-points' where the thresholds for cach of two or more alternativcs were nearly equal.

Such perturbations will not in gencral produce surprising effects, since cquality of two thresholds should idcally mcan cqual reasonablencss for cither altcrnativc. They will, how- ever, gencrate choices not prescribed uniqucly by the data, and hence make cssentially new contributions to the directions of corrcsponding mental processcs.

We must, however, retain a reasonable perspective. It seems likcly that the bulk of human discourse is not in fact unpredictable in principle, thouglh this docs not prevent us from describing it as an exchange of information. As usual, we mcasure the informational output of a speaker rclative to the 144

CHAPTER 12

prior ignorance of the receiver. We can, however, remove this relativity by postulating an ideal observer who knows all the input information that has been received by the speaker, and all the transformations (in so far as they are physically determined)that this information will have undergone in him.

Such an observer, if the human speaker were a perfectly determined machine, would never be surprised by anything

he said. For the ideal observer, this hypothetical speaker would not in fact be an information source.

If therefore we accept a physiological basis for thought pro- cesses (however little we understand them), we can distinguish two senses in which a human being can be described as an information source, with two fundamentally different physical correlates.

In perhaps the bulk of his discourse, he acts essentially as a transducer of information received from outside, from others, or from the abundant information source of the world of physical events. He can then be described as only a secondary source of information.

We can, however, recognize a second, if rarer, eventuality arising whenever input data do not completely determine output. The consequences of even a small perturbation may then be incalculably magnified; yet as we have seen the

result will in general be both intelligible and novel in a

fundamental sense. The human being is then unquestionably acting as a primary information source in the technical sense of the term.

CONCLUSION

There is no need to extrapolate this conclusion into some

speculative form. In our abysmal ignorance with regard to

creative thought-processes, we are probably obscuring at this

moment the most vital features that we may eventually see to be 'obvious' in them. We may well content ourselves in GENER.ATORS OF INFORMATION

145

summary with the more healthy permissive statement, that at least one physical process can be envisaged through which the brain, viewed as a physical system, could generate fundamentally original information. This is of coursc no more an cxplanation of such originality than the Unccrtainty Principle is of the timing of spontaneous atomic disintegrations. It might perhaps yield as much enhanced an understanding of what we call randomness' as of the originality'that we link with it. The one clear fact is that we have only the faintest conception of the real nature of cither. CIIAPTER 13

Indeterminacy, Uncertainty and

Information-Content

INDETERMINACY VERSUS UNPREDICTABILITY

To be invitcd to tacklc an unexpccted subjcct is somctimes frustrating, always challenging. In the present instance it was wholly gratifying; for although 'information' is often defined as what removcs 'uncertainty', the interpretation of various "uncertainty principles' in terms of information thcory re- mains more than a little obscure; and the cxcrcise of digging at the obscurity should be healthy.

It may be as well to begin with a basic distinction, betwecn indeterminacy and unpredictabilily. To predict the bchaviour of a large and complex mcchanical system we rcquire to pro- grammc a computcr (artificial or otherwisc) which must in turn be largc enough to take account of all significant inter- actions bctwcen parts of the system. It takes little imagination to rcalize that in quite a small systcm (a cupful of watcr molcculcs, for cxamplc)we might find a complexity beyond the capacity of the largest imaginable computcr, cven if all the necessary data could be collccted. The detailed bchaviour of such a systcm could thus be termed 'irreducilbly unpre- dictablc'. To say this, however, is quitc different from saying Paper read at the Stuttgart Cougress on Information Thcory, April 5th 1963. Sce foreword to Chap. 12. NTZ-Communications Journal, 3，1964，99-101. UNCERTAINTY AND INFORAMATION-CONTENT

147

that the system is 'indeterminate'. A dcterminate systcm may be defined as one for whose every future state there exists now a completely determining formula in the relevant calculus, whether or not the relcvant initial conditions can be ascertaincd and the necessary computing operations carricd out. If they can not, then the system is determinate, but unprediclable. Most large-scale situations as envisaged in classical physics were of this kind.

To describe a system as indeterminate is to imply not only that it is unpredictable, but (much more strongly)that there exists no determining formula whereby future state-descriptions are completely and necessarily implied by present data. In this case knowlcdge of initial conditions is not, even in prin- ciple, equivalent to certain knowledge of future states of the system.

UNCERTAINTY AND INFORMATION-CONTENT

When data D leave an individual I uncertain of a future cvent E, we mcasure the unccrtainty-to-I of E by the weighted mean, II= >p log (L/p), of the logarithmic improbability, log (üp), of each form of E en- visaged as compatible with D. We then say that any fresh datum that changes the uncertainty I/'conveys information'(positive or negative) to I. The maximum change would result if E were uniquely identified or selecled from the range of forms envisaged (hence the term 'sclective in- formation-content' often applied to /I, to distinguish it from 'structural' measures based on analysis of the form of E).

For our present purpose we pass by those situations in which I just happens to be ignorant of data that in principle could be available to him. Obviously, in that case, which is typical of human communication, the sclcctive information- contcnt of E for I depends directly on his ignorance, both of D and of the forms of E compatible with D.

WWhat intcrests us now is the information-content of E when all possible prior data D would still leave its form in some measure undetermined.

Here the distinction between unpredictable and in- detcrminate events becomes important. A sufficiently com- plex yet dctcrminate mechanism (a spun roulette wheel, 148

CHAPTER 13

or even a tossed coin, for example)may leave us irreducibly uncertain of its course. Yet a good Laplacean (ignoring Heiscnberg for the momcnt) would hesitate to ascribe to the outcome any absolute' selcctive information-content, for he would attribute the finite value of H (for us) either to our ignorance of initial conditions or to our limited computing facilities. From a Laplacean point of view the outcome would have no more fundamental novelty than the result of com- puting to 106 decimal placcs, whose 'uncertainty'(errors excepted)is purely relative to the recipient.

If, however, there are ever any events E such that no formula exists whereby prior data D uniquely determine the form of E, then the prior uncertainty of each E is absolute, and its occurrence has an irrcducible selective information- content.

HEISENBERG UNCERTAINTY

The only candidate for such absolute status in physical science is the uncertainty expressed in Heisenberg's Principle, AE Δt > lh. As is well known, this implies that an event whose energy is specified within a margin of uncertainty AE cannot

h

be located in time with less uncertainty than = where h is Planck's Constant and A is a conventional measure of uncertainty related to standard deviation. This cmpirical theorem has two components-the mathematical 'Un- certainty Principle' of Fourier analysis, Av·At ≥ ，and the empirical relation between quantum energy and frequency, E= hv.

Debate still rages as to the 'absolute' character of this uncertainty-i.e. as to whethcr we should ascribe it to 'indetcrminacy' or merely 'unpredictability'. This boils down to the question whether energy must invariably be related to frequency by the formula E = h— which no one can tell. All we can say is that within the calculus of quantum theory(based on the indivisibility of the quantum h)no formula UNCERTAINTY A.VD INFORMATION-CONTE.VT

149

cxists whcreby prior physical data preciscly detcrminc the forrn of atomic cvents.

If we take the proportionality of cnergy and frcqucncy to be absolutc, we are bound to grant that each atomic event has an absolute minimum to its selcctive information-content. The most fully-informed observer could determine only a prior probability-distribution for the spatio-temporal form of the cvent in question. Aftcr the event he can detcrminc another probability-distribution, which will generally be narrower. Standard formulac of information theory can then give a numerical valuc to the 'amount of information generated'in the event.

Thus, to take a simple example, if a sphcrical light-wave is attenuated until the energy in a givein timc-interval is re- duced to a single quantum, the place of impact of the corrc- sponding photon on a (spherical) recciving scrcen may be complctely undetermined by prior physical data. Its prior probability-distribution is uniform. After impact, it can be determined with a precision limited in principle only by the finiteness of the range of interaction p betwecn clementary particles-of the order of 10-13 cm. Hence, with respect to spatial location, the maximum sclective information-content 'generated'(i.e. the maximum in principle attainable) is of the order

log2 (4πr2/πρ²) or 2 (1 + log2 p).

Even if we allow the radius r to expand to the 'Einstcin radius'of the universc, we find that r/p can risc only to the order of 2130. This sets an upper limit (of a kind)to the spatial selective information-content of a single photon- impact, at somewhere betwecn 260 and 270 bits.

It is not suggested that at this stage in science we shall serve much purpose by making such calculations. The example merely illustrates the point that in this context a direct and even quantitative relation can exist between indeterminacy and sclective information-contcnt. 150

CILAPTER 13

HUMAN BEINGS AS INFORMATION SOURCES

We have said that Hcisenberg uncertainty is the only candidate for 'absolute' status in physical scicnce. This mcans that any physical mcchanism coarsc cnough to be insignifi- cantly affcctcd by Hcisenberg uncertainty can be considercd as in principle predictable.

Now among the rclatively coarsc structures of thic world (comparcd with the dimensions of an atom)are the bodics of human beings. Ie are accustomcd to regard human beings as sources of information, in a scnse which is traditionally little short of absolute. Human action, we say, is free-at least to some extcnt, on some occasions. Iuman bcings 'choose' betwecn altcrnativcs, cach of which must (if choosing is to have any mcaning)be 'opcn' to them beforchand. But if the only absolute unccrtainty known to physics is of the Hciscnbcrg variety, what becomes of this traditional conception? Surcly, we may be asked, a human being can no more be a source of information (in any irreducible sense)than a cash register?

In answer to this, some peoplc would question whether human bodies are in fact subjcct to the same physical laws as the rest of the matcrial world. In our present state of ig- norance, no conclusive cvidence exists cither to support or rcfute this suggestion. I shall argue, however, that it is un- neccssary for its purposc; for we shall sce that the actions of human bcings can in fact have an irreducible indetcrminacy, and hencc selcctive information-content, even though their bodics were as mechanical as clockwork.

A NON-EXISTENCE THEOREM

It will be recalled that we defined a system as detcrminate if for every future state there cxisted already a completcly determining formula. By the same token we may definc a futurc event as detcrmincd if there cxists in the common calculus a complete description of it which is already definitive UNCERTAINTY AND INFORMATION-CONTENT

151

and binding on all-whether or not anybody in fact knows it or believes it. We shall now see that for the future decisions of human beings, curiously enough, no such definitive description would exist in the common calculus, even if the human brain and body were as mechanical as clockwork.22.24

To see this, we first observe that any complete dcscription of a human agent must describe, at least by implication, what he believes. It follows that if the agent were himself to believe the description, it could not be valid both before and after his believing it. If valid beforc, then it describes the agent as not believing it, and so would become invalid if he were to believe it. If, however, it were preadjusted so that when believed by the agent it would become a correct description, then ipso facto it could not be a correct description beforehand. In neither case has the purported description any logical claim on the agent; for in the first case he is mani- festly in error if he believes it, since it will then be false; while in the second he is manifestly not in error if he dis- believes it, since it is and will remain false unless he believcs it.

Regardless of the mechanism of their bodies, thereforc, human beings are necessarily impossible of complete future-tense description in terms definitice and binding upon all.

Suppose now that a human bcing A has to make a decision at time t (in the future). If his brain and environment form a rigidly interconnected mechanical system, then for a totally detached observer the description of all future brain-cvents, including those at time t, would be already implicit (ex lypothesi)in the present total state-description, and would therefore have no irreducible selective information-content for that observer.

For A, on the other hand, the observer's arguments, leading to detailed descriptions (predictions) of future brain-cvents, are systematically invalid, if we assume that any change in A's knowledge implies a corresponding change in A's brain-state. The data presupposed in the observer's argumcnts cannot claim to have absolutc validity regardless of whether or not 152 CHAPTER 13

believes them, since (ex hypothesi) they imply a description of what A believes. To 'take a decision' is (by definition) in- compatible with knowing (or bclieving one knows) the out- come already with certainty. Deciding and believing arc here mutually cxclusive.

Hence for the agent A, the prior uncertainty of the out- come at time t is absolute. It is not that there are some data which he needs, but of which he happens to be ignorant; it is rather that for him the crucial olbservations which enable the detached observer to complcte his prediction are not data: they would not be valid were he ()to believe them.

CONTRAST WITH UNCER'TAINTY DUE TO IGNORANCE

In order to make this unique situation clear, we may con- trast it with that of, say, the astronomer who wishes to predict the motions of some hcavenly body, but lacks the necessary data. Here once again we can imaginc an ideal isolated observer to whom all nccessary data arc available, so that all future statc-descriptions are implicit in liis present state-description. In this casc, however, there is no disputing that (discounting relativistic corrections) the obscrvations of the isolated observer are valid data for the astronomer, of which he just happens to be ignorant. IVere he to believe them, he would be correct, and could in principle complcte his prediction. Thus his uncertainty of the astronomical out- come is not absolute, and is radically different from the indetcrminacy (to him)of his future dccisions. In taking decisions he is not merely entitled, but logically obliged, to regard them as undetermincd (in the scnse we have bcen using); for he would be demonstrably in error if he did not. It can of coursc be objccted that we have oversimplificd the astronomer's situation; for in the last analysis his brain is part of the iuniverse that he is trying to prcdict, so that the events in his brain (including those when his knowledge changes)must be considered to havc some slight effect upon UNCERTAINTY AND INFORMATION-CONTENT

153

every other part of the universe, including the hcavenly bodies whose motions he wants to predict. This point is in fact cogently argued by Popper27 in a classic paper. While I do not wish to minimize its philosophical interest, I would, however, emphasize the irrelevance of this extremcly marginal indeterminacy to the issue before us. For the changcs (if any) caused in a heavenly body when the astronomer's knowledge changes are conceptually incidental, in the scnse that one could at least imagine without self-contradiction a shielding process which could intervene betwecn his brain and the objects of his obscrvation, so as to reduce the intcrference to any desired extent. The link we have assumed betwccn the agent's beliefs and the states of his brain, on the other hand, is not of this charactcr. These arc rather two sides of the same coin-two aspects of one complex situation-so that a significant change in knowledge or belief is inseparably expressed and betokened by a significant change in brain- state.

DIALOCUE

So far, it may be objected, we have proved only that a human being is a source of information to himself. We have in fact allowcd that to a completely isolated but fully- informed observer of his brain and environment (if such were possible)his actions could in principle be predictable and devoid of selective information-content. What then of his fellows with whom he engages in dialoguc? Can he in any absolute sense be an information-source for them?

Indeed he can. For in genuine dialogue between two or morc agents, the reciprocal interaction between them is such that for purposes of predictive analysis they become effectively one system (See Chapter 9). It follows that each agent in dialogue becomcs unspecifiable in complete detail not only to himself, but to his interlocutors as well. In the common calculus to which all subscribe, no formula exists which 154

CHAPTER 13

validly specifies in complete detail the future state of any of them. To borrow a metaphor from quantum physics, there are'interaction terms' which remove any possibility that one member of the dialogue could fully spccify another, or be specified by him, as a determinate system. Once again, it is important to see that this is not a matter of 'ignorance'on the part of the members of the dialogue, as if valid determining formulae existed but they could not discover them. Even ifour hypothetical 'fully-informed obscrver' wanted to relieve their uncertainty, he would incvitably discover that at the crucial points he had no information to gire them. For them, any belief in his key observations would be self-refuting, non- sensical.

The absence of determining formulae for human actions in the common calculus is thus not an accidental inadequacy, to be remedicd (in principle) by adding new terms. It is rather the reflection of a stubborn fact about our human situation. So far from being in error to regard one another as absolute' sources of information in dialoguc, it is clear that we should be absolutely in error to do otherwisc.

CONCLUSION

Our conclusion is thus that two kinds of 'absolute'un- ccrtainty beset human knowledge. One is our uncertainty of microphysical atomic bchaviour, due to the finitencss of the quantum of action inseparable from observation. At this level of detail it would scem that atomic events have for us an irreducible(potential)sclcctive information-content.

The sccond type of 'absolute' uncertainty attends our knowledge of onc another in interpersonal dialogue (as distinct from dctached physical observation). Quite in- dependent of any physical indeterminacy of our brain- mechanisms, this uncertainty reflects the fact that, in the public calculus of two or more persons in dialogue, no valid definitive prediction exists for their detailed future behaviour. In UNCERTAINTY AND INFORMATION-CONTENT

155

this relationship the action of each has an irreducible(poten- tial)selective information-content, for his fellows as well as for himself.

Our habit of regarding one another as sources ofinformation in dialogue is thus well founded; for the freedom we attribute to each other is not a matter of convention, but a matter of fact. APPENDIX

The Nomenclature of Information Theory

(1)What Information Theory is About

SUMMARY. In everyday specch we say we have received Information, when we know something that we did not know beforc: when 'what we know' has changed. If then we were able to measure 'what we know', we could talk meaningfully about the amount of information we havc received, in terms of the measurable change it has causcd. This would bc in- valuable in assessing and comparing the efficiency of methods of gaining or communicating information.

Information Theory is concerned with this problem of measuring changes in knowledgc. Its key is the fact that we can represent what we know by means of pictures, sentences, models, or the like. TWhen we receive information, it causes a change in the symbolic picture or representation which we would use to depict what we know. It is found that changes in representations can be measured; so 'amount of information', actually in morc than onc sense, can be given numerical meaning. It is as if we had discovered how to talk quantitativcly about size, through discovering its effects on measuring apparatus. We should at once find that it had the quite different but complementary senscs of volume, area, and length -if not others. The analogy is potentially misleading, but may show us what to expect.

From Proceedings of First London Symposiun on Information Theory, 1950. Reproduced in Proc. 8th Conf. on Cybernctics (H. von Focrster, ed.). Josiah Macy Jr. Foundation, New York, 1951. THE NOMENCLATURE OF INFORMATION THEORY

157

INFORMATION AS SOMETHIING MEASURABLE? A hundred years ago it would have been thought ınerely a pardonable crror if a stranger wcre to suppose'information' to mean something measurable, like energy for example. "Amount of information', or 'information-content', he would be told, is a metaphorical term, and has no numcrical properties. But in fact he would not have been wrong; though he would have been in grave danger of confusion unlcss he lcarned to distinguish between a number of complcmentary senscs of the tcrm.

We might profitably comparc the stranger's position with that of a man who has never heard of the concept of 'size'. He discovers that, in at lcast one scnse of the tcrm, a man,a sack of potatocs, an oildrum, and a tree-stump can all bc said to have 'the same size'. He has now made some progress. At least, he knows that 'size' can not mean any of the propcrties which are not common to all four examplcs. With paticnce, he might eventually arrive at the notion of size by a proccss of elimination. He might cven discover the diffcrent scnses of thc term, and coin the terms 'volumetric sizc' or volumc', 'superficial size' or 'arca', and 'linear size'or 'length', to distinguish threc of its important senses.

But he has also a second linc of approach which is more fruitful. He asks us: 'What differences clocs "size" make in an objcct? In what circumstances do you become awarc of it? To what does size make a difference?' He discovers that we define the sizc (volume, area, etc.) of a body in terms of its ability to cause changes of a certain kind, in ccrtain circum- stances (for examplc, the indication of a point on a scale, as a result of certain well-defined operations with appropriate measuring apparatus). This is his clue. By systematically studying what happens when something is affected by the sizc of an objcct, he discovers the meaning of the term.

Our task is a similar onc. We shall find it profitable to ask: 'To what does information make a difference? WWhat are its cffects?' This will lead us to an 'operational' definition covering all senses of the term, which we can thien cxamine in detail for measurable propcrties. 158

APPENDIX

REPRESENTATIONS

In everyday language we say we have received information, when we know something now that we did not know before. If we are exceptionally honest, or a philosopher, we assert only that we now believe something to be the case which we did not previously believe to be the case. Information makes a difference to what we believe to be the case. It is always information about something. Its effect is to change, in one way or another, the total of 'all that is the case' for us. This rather obvious state- ment is the key to the definition of information. For those to whom'metaphysics' is a bad word, any aura of metaphysical abstruseness which it may have is casily exorcised. IWhat wc know or belicve, in science at least, could in principle be represented in a variety of quite precise ways: we might make a long statement, or draw a symbolic picture, or make a physical model, or send a communication-signal. All the results could in a sense show or embody what we believe: they are what we may call representations: structures which have at least some abstract fealures in common with somcthing else that they purport to represent. These abstract features of representations are what we want to isolate. They form the real currency of scientific intercourse, which is normally obscurcd in wrappings of adventitious detail.

Now that we have established this fundamcntal notion of a representation, information can be described as what we depend on for making statements or other representations. More precisely, we may define information in general as that which justifies representational activity.

CRITERIA OF 'AMOUNT OF INFORMATION'

Right at the start the term 'Amount of Information'or 'Information-Content' takes on two different kinds of mean- ing in answer really to different kinds of question. An example will illustrate the point. Two people A and B are listening THE NOMENCLATURE OF INFORMATION THEORY

159

for a signal which they know will be either a dot or a dash. A dash arrives. A makes various measurements, represents what has happened by a graph, and asserts that there was 'a good deal of information' in the signal. B says 'I knew it would be either a dot or a dash. All I had to do was to print one or other of these prefabricated representations. I gained little information.'

A and B arc not of course in disagreement. For lack of a vocabulary, they arc using the term 'amount of information'as a measure of different things. A is using the term in the sense of what we may call Scientific or Descriptive information-con- tent. This in itself has two aspects, relating roughly to the number of independently variable features (structural inforination-content)and the precision or reliability (metrical information-content)of the representation he has made. The knowledge which he says has increased is knowledge of what has actually happencd and been observed.

WWhat of B? He was not waiting to observe everythiag that happencd. He alrcady knew that for his purposes only two kinds of representation would be needed, and he had pre- fabricated onc of each. The knowledge he acquired was knowledge of which representation to select. B was therefore using 'information'in the sense of 'that which determines choice', and estimating what we may call selective information-content.

One word which was unexpected would have for B more selective information-content than a whole message which he was already sure he would receive.

A's approach is typical of the physicist, who wants to make a reprcscntation of physical events which he must not pre- judge. B's is typical of the communication engincer, whose task is to make a representation, at the end of a communica- tion channel, of something he already knows to be one member of a set of standard representations which he possesses. His conccrn is therefore not with the size or form of a representa- tion, but with its relative rarity, since this will govern the complexity of the 'filing system' he should use to identify it. 160

APPENDIX

Each however may on occasion find both approaches relevant to diffcrent aspects of his work.

To sum up, if we ask how much information there is in a given representation, wc may mean: "How many distinct features has it? How many elementary events docs it de- cribe?' in which case we require answers in terms of Scientific or Descriplice inforination-content; or we may be ignoring questions of the size and complexity of the representation, and thinking instcad of the complexity of the selection process by which it was identified, meaning: 'How unexpected was it? How small a proportion of all representations is of this form? In how many steps were you able to identify it in your"filing cabinct" of possibilities?' In this case our qucstion refers to Selective information-content. Rarity here is the touchstone, as against logical structure in the first case. It will be realised -and this may bc an important help to the understanding of the subject-that the term 'information' means something quite distinct from 'meaning'. If the readcr begins by divorc- ing the two completely, he may find it easier to trace the conncctions in any subsequent reunion.

Our purpose in the explanatory glossary which follows is to see how the terms which have arisen in these different con- nections arc related and to remove any possible misconception that these complementary senses of the term information- content are in any way competitive. The following diagram may help to keep the most important distinctions in mind.

Information: that which determines form

Determinatinn of form

(a)by construction

(b)by selection

No. of degrees Weight of

Unexpectedne

of freedom

evidence (2)Explanatory Glossary

1. THE SCOPE OF INFORMATION THEORY

1.1 Information Theory is concerned with the Representations making of representations--i.e. symbolism in

its most general sensc.

1.1.1 By a representation is meant any structure

(pattern, picture, model) whether abstract or

concrete, of which the features purport to

synbolize or corrcspond in some sensc with

those of some other structure.

1.1.2 The physical processes concerned in the

formation or transformation of a representation

are thus distinguished from other physical

proccsses by the clement of signijficance which

they possess when conceived as representing

something elsc.

1.1.3 For any given structure there may be

scvcral cquivalent representations, defined

as such through posscssing certain abstract

features in common.

1.2 It is these abstract features of representa-

tions which are of interest in Information

Thcory. Its aims are (a) to isolate from their

particular contexts those abstract features of

representations which can remain invariant

undcr reformulation,*(b) to treat quantitatively

the abstract features of processes by which

representations arc made, and (c) to give

quantitative mcanings to the several scnses in

which the notion of amount of information can

be used.

1.3 The scopc of Information Theory thus

includes in principle at lcast threc classes of

activity:

This aspect of the subject is already an established branch-of math- ematics under the name of Representation Theory or Abstract Group Theory. 162

APPENDIX

1.3.1 Making a representation of some physical aspect of expcrience. This is the problem

Scientific or

treated in Scientific or Descriplive Information-

Descriptive

Theory.

Information

1.3.2 Making a representation of some non-

Theory

physical (mental or ideational) aspect of expericnce. This is at the moment outside our concern, being the problem of the Arts.

1.3.3 Making a representation in one space B, of a representation already present in another

Communication space A. This is the problem of Communication

Theory

Theory, B being termed the receicing end and A

Communication the transmitting end of a Communication Channel.

Channel

1.3.3.1 By a space is meant any physical or

Space

abstract mathematical coordinate frame-work or manifold, of any number of dimensions, in which the elements of a represcntation can be ordered.

1.4 These classes are not of course exclusive. The problem of communication in particular is scldom separable from one or both of the first two. In its present state of development Information Thcory is concerned mainly with (1.3.1), the problem of representing the physical world, and(1.3.3), the problem of communicat- ing representations(of any kind). It is communi- cation theory (1.3.3), however, with its immensc practical importance, which has reccived the grcatcst attention; and it is only the logical priority of the other two which prevents it from coming first on the list.

2. INFORMATION The foregoing definition of the scope of In- formation Thcory provides the necessary back-

Information

ground for the definition of Information.

2.1 In all its senses, the term can be covered by a general 'operational' definition (i.c.a definition in terms of what it does: as (e.g.) force is classically defined in terms of the accel- cration which it causes or could cause). The effect of information is a change in a represen- tational construct. EXPLANATORY GLOSS.ARY

163

2.1.1 Information may be dcfincd in the most general sense as that which adds to a representation. 2.2 This leaves open the possibility that infor- mation may be truc or false.

2.2.1 When a represcntation alters, we define the ncw information as true if the change increases the extent of correspondcnce between the representation and the original.

2.2.2 The information is said to be false if the change ddiminishes the cxtent of this correspon- dence.

2.2.3 Strictly, the truth or falschood is an attribute of the resultant representation, but it is customary to attribute it to that which has given rise to the change in the representation.

3. MEASUREMENT OF INFORMATION-CONTENT

Two quite diffcrent but complementary ap- proaches are possiblc to the ncasurcment of Information-Content, and have given rise to uses of the term in quite different senses.

3.1 From a quantitative analysis of what a representation portrays, we can isolate funda- mental nunterical fcaturcs common to all its cquivalent represcntations, and can say that they constitute the 'corpus of information' which it contains or represents.

3.1.1'Information-Content' in this context is a numerical indcx (in one sensc or another) of the 'size' of the representation itself.

3.2 But if instcad of asking 'How niany elc- ments ctc. arc therc in this reprcscntation?' we ask'In how inany stages, and in what way, has it becn buill up?' we arrive at a di:Tcrent kind of mcasure. This becomes clear if we considcr that the samc representation could be constructcd in a number of diffcrent way's according to the amount of prefabrication uscd. 3.2.1 'Information-Content' in this context is a numerical index of the complcxity of the construction-process. 161

APPENDIA

3.3 In the following paragraphs, 4 and 5，thesc two approaches will be discussed. The first has given risc to two complcmentary definitions of what has been called 'amount of information', and the second approach to a third definition. T'hcse, however, are not rivals, but are autono- inously valid measures, appropriatc in answer to different questions.

4. ANALYSIS OF REPRESENTATIONS

4.0.1 Representations communicable in a two- valued (yes or no)form are necessarily quantal in structure, since an imperceptible change' in a two-valued logical form is by definition meaningless. All the changes are discretc, there- fore the clementary concepts of logical represcn- tations are discrcte and enumerable.

4.0.2 In fact a large class of such representations can be reduced to a form made up only of identical elements, so simple that their only attribute is existence (Wittgenstein, Rcf. 40). 'This fact provides a basis for the quantitative analysis of such representations (MacKay, Ref. 11). (Reprcscntations not amenable to precise logical description have not so far been considered in the thcory, though a large class of these might be handled in terms of ap- proximate quantal equivalents representing upper and lower bounds' to their logical content.)

4.0.3 In general a pattern reduced to such fundamental terms will contain a certain num- ber of distinguishable groups or clusters of elements, the clements in cach group being indistinguishable among themsclves. Therc are thus two numerical features of interest.

(1)The number of distinguishable groups or clusters of indistinguishable elements in a representation, and

(2) The number of elements in a given group or cluster. EXPLANATORY' GLOSS.ARI

165

4.0.3.1 The number of groups, and the numbers of their elements, may be thought of as re- spectively analogous to the number of columns and the number of entries per column in a histogram.

4.1 Structural Information-Content

4.1.1 T'he number of distinguishable groups or clusters in a representation -the number of definably independent respects in which it could vary-its dimensionality or number of degrees of freedom or basal multiplicity-is termed

Structural Infor- its Structural Information-Content.

mation-Content

4.1.2 The unit of structural information,

Logon

one logon (Gabor, Ref. 6; MacKay, Ref. 11), is that which cnables one such new distin- guishable group to be defined for a represcn- tation. Thus structural information is not concerned with the number of clements in a pattern, but with the possibility of distinguishing between them.

4.1.2.1 For example, if we are counting identi- cal sheep junping a gate, and we have no sense of time, our rcsult can only be repre- sented by a certain total nurnber; but if we have a clock, we can now define what we mcan by the number in the first minute' and in the second' and so forth, and reprcsent our result by a sct of distinguishhable subtotals. The clock has provided Structural information. In a similar way the ability to distinguish (e.g.) spatial position along the gatc would provide distinguishable subtotals and hence increase the structural information-content of our reprcsentation.

Logon-Content

4.1.3 Logon-content is a convenient term for the structural information-content or number of logons (number of independently variable featurcs)in a representation (c.g. the number of independent cocfficients required to specify a given waveform over a given period of time). 4.1.4 The number oflogons provided by appara- tus per unit of coordinate-space (centimetre, 166

APPENDIX

squarc centimetre, second, etc.) is termed its

Logon-Capacity

logon-capacity.

(possible syn.

4.1.4.1 For example, a channel whose band-

logon-density)

width permits of l independent amplitude read- ings per sccond has a logon-capacity of l: in a microscope, logon-capacity is a measure of resolring-poizer; and so forth.

4.1.5 The reciprocal of logon-capacity is

Structural Scale- terned the strarlural scale-unit for the apparatus.

Unit

4.2 Metrical Information-Content

4.2.1 The number of (indistinguishable)logical elements in a given group or in the total pattern

Metrical

is termed the Metrical Information-Content of the

Information-

group or pattem.

Content

4.2.2 The unit of metrical information, one

Metron

metron, is dcfined as that which supplics one clement for a pattern. Each clement may be considered to represent onc unit of evidence. Thus the amount of metrical information in a pattern measures the weight of evidence to which it is equivalent. Metrical information gives a pattern its weight or density-the 'stuff'out of which the 'structure' is formed.

4.2.3 In a scientific representation, cach metrical unit may be thought of as associated with one elementary event of the sequcncc of physical events which the pattern represents. 4.2.4 Thus the amount of metrical information

Metron-Content in a single logon, or its metron-content, can be

(syn. metrical

thought of as the number of elementary events

information-

which have been subsumed under one head or

content)

'condensed' to form it. For cxample, in the case of a numerical paramctcr, this is a mcasure of the precision with which it has been determined. 4.2.4.1 Notice that these elements are in- distinguishable, so that their number is not the number of binary digits(5.1.3)to which the logon is cquivalent.

4.2.5 WWhen we come to represent the results of physical observations, we are often intercsted in magnitudes which are not directly propor- EXPLANATORY GLOSSARY

167

tionalto the mctron-content. Therepresentations we use do not then show the metron-content explicitly. It must be clcarly realised that metron-content as dcfined is a measurc of the number of clements appearing when what is belicved to have happened is reprcsented in its most fundamental physical terms.

4.2.6 Thus if an estimate is made of a para- meter from a statistical sample, the elementary events conccrned are the arrivals of 'unit- contributions'to the sample. These could be reprcsented by the number of intervals occupicd

Conceptual Scalc on a conceptual scale proportional to metron- content.

4.2.7 On the other hand, the usual represcn- tation shows the magnitude of the paramcter conccrned, and not generally the metron- content, on a lincar scale, graduated in elemen- tary intervals which in the useful limit are just large cnough to give the representation of the magnitude (scalc-reading) a probability

Proper-Scale

of . Such a scale is termed a proper-scale. Now the probable crror, in a normal population, is inversely proportional to the square root of the size of the sample. Hence the magnitude in such a case would be shown as occupying on the proper scale a number of elementary inter- vals proportional only to the square root of the number of clementary events. The number of mctrons is (in this special but common casc)the square of the number of occupicd intcrvals shown in this less fundamcntal physical representation.

4.2.7.1 In conncction with radar information

Numerical

the term numerical energy has becn used to

Energy

represent what is csscntially the metron-content of a signal. It is the ratio (Total energy)/ (Noise-powcr per unit bandwidth).

4.2.8 In general then a clear distinction exists betwecn(a)the fundamental represcn- tation on a conccptual scale showing the invariant number of logical clemcnts, and 168

APPENDIX

(6)the representation of the magnitude which

is of practical interest. In fact the conncction

betwecn the two is little closer than that between

the precision with which a given variable

can be measured and its magnitude. Precision

increases monotonically with metron-content,

but few quantities are linearly related to metron-

contcnt. Power and energy in the classical

case arc among the few exccptions; this accords

with thcir apparently fundamcntal status among

physical concepts.

Scale-Unit

4.2.9'The scale-unit of a magnitude is the nin-

ianum intcrval in terms of which the scale can

usefully or definably be graduated.

4.2.9.1 For a magnitude imprecisely known

it is defined as above (4.2.7) to be cqual to

the probable range of crror. A magnitude

supported by a singlc metron occupics just onc

interval on such a scalc. In practice, larger

units arc often uscd, c.g. range of standard

crror.

4.2.9.2 But it should be remembered that in

theorelical represcntations the size of the scalc- Coincidence-

unit is gencrally limited by our inability to Relations

define a smaller unit in terms of the coinci-

dence-relations out of which physical representa-

tions are constructed.

4.2.10 The nunber of netrons per unit of Metron-Capacity coordinate-spacc is termed the metron-capacity (syn. metron-den- or metron-density of a physical obscrvation- sity)

systeim (cf. 4.1.4).

4.2.11 The coordinatc-interval over which one Conceptual Unit mctron is acquired is termed a conceplual unit Metrical Scale-

or (undesirably) a metrical scale-writ of coordin- Unit

ate.

(undesirablesyn.) 4.2.12 It will be noted that ınetron-content

is necessarily positive.

4.2.13 Returning to the example of the jumping

shecp, let us now suppose that we are trying

to dctermine a figure for the average valuc of

some paramctcr of a sheep, in cach group which

we arc ablc to distinguish. Assuming for the EXPLANATORY' GLOSSARY'

169

sake of illustration that the parameter is nor- mally distributed, the mctron-content of each estimate would be proportional to the number of sheep per group, and the probablc crror in each estimate would be inversely proportional to the square root of this number. Hence the number of proper-scale-intervals occupied by the cstimated parameter would be proportional to the square root of the mctron-content of each group.

4.2.14 The term 'amount of information' in a sense analogous to this was first uscd by R. A. Fisher(Ref. 4)，who defines it as follows: Suppose we have a probability distribution function f(x, xo) showing how in a given population a variable x is distributed about a paramcter xo, c.g. f(x, xo) = Ae-(x-x0)21202. The 'amount of information' in n samples from the population is defined as n times the weighted mean of (8 logf/ axo)2 over the range of x-i.e.

Equivalent forms are

n()dr and -n()fdr.

In the case of a normal distribution, this reduccs to the reciprocal of the variance, provided that the range is independent of xo. It is thus a direct measure of precision, though it is not dimensionless unless suitably normaliscd. 4.3 Representation of Descriptive Information-Content The Descriptive Information-Content of a given representation is specificd by sctting down the metron-content of cach logon. This may be represented in various ways.

4.3.1 One convenient method is to use a multi-

Information-

dimensional information-tector in an information-

Vector

space of which cach axis represents one logon.

Information-

The squares of the components of this vector

Space

are the metron-contcnts of the respective logons. Thus the square of the length of the 170

APPENDIX

vector itself is the total metron-content, the sum of the individual metron-contents.

4.3.1.1 In this reprcscntation theangle between two dircctions has a direct interpretation as a

Relevance

measure of relecance. A dependent statement is defined by a ray in the space, and the metron- content afforded to it by the information is found by squaring the projcction of the infor- mation-vector on the ray.

4.3.1.2 A new complete represenlation may be set up by supplementing this dependent state- ment (4.3.1.1) by a set of othcrs reprcsented by orthogonal rays. This process amounts to a rotation of axes, which leaves us with a new total metron-content equal to the old.

4.3.2 The same proccsscs can be reprcsented in terms of matrix algebra, if the metron- contents of logons are set out initially as the

Information-

elements of a diagonal Information-Matrix.

Matrix

Dependent statements now define vector functions, and thcir metron-content is found by forming scalar products of the form '.I, where I is the information-matrix, a vector function, and its transpose. Under all

Trace(syn. spur, complete(unitary') transformations, the trace

characteristic,

or sum of the diagonal elements of I remains

diagonal sum)

invariant, being the total mctron-content.

4.3.3 An alternative geometrical representation suitable for some particular cases employs a three-dimensional histogram having a coordin- ate and its Fourier-transform (e.g. time and frequency)as its two basal axes. Since the number of logons provided by given apparatus is proportional to the product of bandwidth (g.v.)and conjugate coordinate, the base is divisible into equal cells each representing onc logon. On each cell is erccted a column having a height proportional to the logarithm of metron-content. This gives the total volume of the histogram the same qualitative signifi- cance as the logarithm of the volume spanned by the information-vector of4.3.1. EXPLANATORY GLOSSARY

171

5. COMMUNICATION: REPLICATION OP REPRESENTATIONS

5.1 The problcm of communication usually concerns representations of which all parts exist already in the past expcricnce of the rcceiver. In other words the receiver alrcady possesses prefabricated components of the representation. 5.1.1 In fact it is gencrally assumed to be known that the complcte representation to be

Ensemble

rcplicated is one member of a finite ensemble (g.v.) of possible originals, some of whicl have in the past been communicated more often than others. We may then say that these more common messages'give less information' than the others, using the notion of "infor- mation-content' now in the important sense of para. 3.2.1.

5.1.1.1 Our mcssage is here thought of as telling us to sclect onc prcfabricated representa- tion.

5.1.1.2 We arc not now asking 'How big is it?' or 'How much detail has it?' but rather 'How unusual or uncxpccted is it?' or 'How much trouble will it take to find it in my cnsemble?'

5.1.2 A convenient measure of information- content in this sense is the negative logarithm (base 2) of the prior probability of the representa- tion concerned (Shannon, Ref. 31; Wiener, Rcf.39).

5.1.2.1 The base 2 is chosen becausc a selection among a sct of n possibilitics can be carried out most economically by dividing the total succcssively into halves, quarters, eighths, etc., until the desired member is identified. The number of stages in this process is then the intcger ncarest to, and not less than loga n.

5.1.2.2 The information-measure so defined equals the number of independent choices betuceen equiprobable alternatices which would have to be determincd before the required represcntation could be identified in the cnsemble of which it is a member. (The prior probability measures 172

APPENDIX

the fraction of the members of the ensemble which are of the required kind.)

5.1.2.3 This, like the first two mcasures (paras. 4.1.1 and 4.2.1)，represents a numbcr of logically "atomic" propositions; but this time they dcfine, not the representation, but the selection-process leading to it.

5.1.3 Information-content in the above scnse of that which determines choice may be termed

Selective Infor-

selective infornation content.

mation-Content

5.1.4 The unit of selective information-content,

Binary Digit

one binary digit or bit, is that which determincs a

(syn. bit)

single choice betwecn cquiprobable altcrna- tives.

5.1.5 In a long scqucnce of diffcrent representa. tions of which the ith kind has a prior prob- ability pe (and hence an avcrage frequency of occurrence p), the avcrage amount of selcctive information per represcntation is evidently the weighted mean of -log p over all kinds of representation, or I=-p log A, which apart from some ambiguity of sign in the litera- ture is also the standard definition of the

Entropy

entropy of a selcction.

5.1.5.1 Where representations take the form of continuous functions, II takes the form -[f(x)logf(x) dr, wheref(x) is the probability distribution of the represcntative variable It is thus the weighted mcan of [-log / over the range of x.

5.1.6 In practicc the receipt of a communi- cation-signal disturbed by noise mercly alters the form of f(x)(generally narrowing it), and docs not specify x uniqucly. The amount of selective information rcccived is then de- fined as the difference between the values of H computed before and after receipt of the signal. 5.1.7 When two represcntative variables, x and y say (discrete or continuous), are in qucstion, knowledge of the value of one may affect the prior probability of the other. In the above notation, f(y) depends on x, so that the entropy EXPLANATORY GLOSSARY

173

II of y will also vary with .r. If we picture an ensemble in which valucs of x occur in their

Conditional

expected proportions, we define the conditional

Entropy

entropy of y, lI(y), as the average value of the entropy of y (calculated for each value of x) over all members of this ensenble.

5.1.7.1 This may also be described as the 'weighted mean entropy'of y, weighted by the probability of getting the different values of x. It therefore measures our uncertainty about y when we know x.

5.1.7.2 An analogous conditional cntropy II(x) can be defined for x when y is known.

5.1.8 Where x and y represent respectively the input and output of a noisy communication channel, the conditional entropy H(x)is

Equivocation

termed the equirocation. It is a measure of ambiguity.

5.1.9 The number of bits per second which a

Capacity

channel can transmit is termed its capacity. For the case (5.1.8) it is defined as the maximum af[H(x) - H,(x)]-

5.1.10 The ratio of the entropy of a source to the maximum vahie which it could have while using the same symbols is called its

Relative Entrupy velatire entropy.

5.1.10.1 One mimus the relatice entropy is termed

Redundancy

the redundancy.

5.2 These considerations suggest a more cconomical method of communicating a rep- resentation.

5.2.1 Instead of transmitting a physical rep- resentation of the representation itself, we may transniit a representation of the sclection- process by which it nay be identified in the ensemble of possible representations which is assumed to exist at the receiving end.

5.2.2 A system whereby a representation is defined by a selection-process is termed a

Code-System

code-system.

5.2.3 The corresponding representation of 174

APPENDIX

the selection-proccss transmitted is known as

Code-Signal

a code-signal.

5.2.3.1 As a physical sequence the code- signal will itself have mctrical and structural features as discussed in para. 4，and will be definable by a vector in an information-space. But its structure necd not have anything in common with that of the representation which it identifics.

5.2.3.2 On the other hand, the ordinary case of making physical reprcsentations could be thought of forinally as a special case of coding, one-to-one.

5.3 It follows that the result of an expcriment, as well as a communication-signal, could be anal.

Selective

ysed in terms of its selective information-content.

Information-

Content of a

5.3.1 This is a relative measure, depending

Description

on the number of distinct results which were regarded as cqually probable by the observer. The result observed is thought of as spccify- ing onc of a number of possibilitics alrcady contcmplated by the observer as forming an ensemble in defincd proportions.

5.3.2 The amount of sclective information derived from the expcriment can then be computed in the same way as for a message (5.1).

5.4 The entropy or sclective information- content of a selection should not be facilcly identified with the physical entropy of thermo- dynamics. The two are equivalent only in the particular casc where the ensemble from which the sclection is made is a physical one defincd for a state of thernodynamic cquilibrium.

5.4.1 For cxample, if all n distinguishable voltagc-levels of a transmitted signal are regarded as cquiprobable, the sclective infor- mation-content per logon is proportional to log n. On the other hand, the physical entropy- increase is proportional to (or must exceed)n2 (MacKay, Refs. 12 and 13). EXPLANATORY GLOSSARY

175

5.4.2 Here the corrclation is betwcen metrical

information-content (para. 4.2.7)and physical

entropy-increase. In fact metron-content can

be thought of here as the number of unit-

increases of physical entropy-i.e., of clemen-

tary events-which have becn subsumed under

one head, thereby losing their distinguishability

and potentiality ofscrving as'bits'.

Alphabetical Index of Terms used in Information Theory

and related Communication Theory. References are to

Paragraphs in the Glossary.

Bandwidth

In general terms, the region of Fouricr-space

(g.v.)to which the output of an instrument is

confincd. In particular, the effective frequency-

range (conjugate to a given coordinate)to

which it responds.

Binary digit

(5.1.3)Unit of sclective information-content. Bit Capacity

(5.1.9)Number of bits transmissible per second. Code-system

(5.2.2)

Code-signal

(5.2.3)

Conceptual unit (4.2.11)The coordinate-interval in which one

mctron is acquired. Reciprocal of metron-

density.

Ensemble

A set of possibilitics each of which has a defined

probability.

Entropy

(5.1.5)(a) In statistical mechanics, k times the

weighted mcan of the (negative) logarithm of

the probabilitics of members of an ensemble.

(6)In thermodynamics, that function of state of

a body or system which increases by AQ/T

in a reversible proccss between two states I

and 2, where AQ is the hcat taken up by the

body or system at temperature T.(Dcfinitions

(a)and(b)are equivalent.)

Conditional

(5.1.6)

Relative

(5.1.10) 176

APPENDIX

Equivocation

(5.1.8)

Fourier-space

T'he space whosc dimensions represent variablcs which are Fourier-transforms of coordinatcs (e.g. the frequency conjugatc to the time coordinate).

Information

'That which alters represcntations (2.1).

Information.

content

Metrical

(4.2)A mcasurc of the weight of evidence in a representational pattern.

Selective

(5.1.3)A measure of the unforesceableness of a representation.

Structural

(4.1)The number of indcpcndently variable features or degrecs of freedom of a representa- tion.

Information-

A matrix in which the metrical (and structural)

matrix

information-content of an experiment is spcci- ficd.

Information-

The spacc in which independent logons are

space

represcnted by orthogonal rays, and their metron-contents by the squares of distanccs along these rays. (4.3.1)

Information-

The vector whose components in information-

vector

space are the distances just mentioncd.

Logon

Unit of structural information-content(q.v.).

Logon-capacity

(4.1.4)Number of logons per unit of coordinate

(poss. syn.

space.

Logon-density)

Logon-content

(4.1.3)Number of independently variable

(syn. Structural fcatures.

Information.

content)

Metron

(4.2.2)Unit of netrical inforniation-content (q.v)

Metron-capacity (4.2.10)Cf. logon-capacity.

(syn. Metron-

density)

Metron-content (4.2.4) Measures the weight of evidence to

(syn. Metrical

which a reprcscntation is cquivalent.

Information-

content) EAPLANATORY GLOSSARY'

177

Numerical energy (4.2.7.I) Ratio of (Energy)/(Noise Power

per unit bandwidth). A particular example of

metron-content.

Proper-scale

(4.2.6)A representational scale on which

equalintervals are cquiprobable.

Redundancy

(5.1.10.1)One minus relative entropy.

Representation

(1.1.) A symbolic picture, model, statement,

etc.

Scale-unit

(4.2.9)The minimum interval in terms of

which a scale can definably or usefully be

graduated.

Metrical

(4.2.11)Undesirable equivalent of conceptual

unit. Reciprocal of metron-density.

Structural

(4.1.5)Reciprocal of logon-capacity. (3)Postscript on

Structural Information-Content and Optical

Resolution

(A) Extracts from Quantal Aspects of Scientific

Information

LOGON-CONTENT. It was Kant who said: "reason has

insight only into that which it produces after a plan of its

own." The design of an experiment is essentially the specifica-

tion a priori of a pattern, of categories in terms of which alone

the result can be described. All the events of the experiment

must find a place in one or other of these, though of coursc not

all categories will necessarily find an exemplar in a given

experiment.

Since each independent category enables us to introduce a

measure of differentiation-i.e. of form or structure-into

our account of a result, we can regard knowledge thereof as

providing us with prior or structural information. W'e can there-

fore define a unit of structural information, or (using Gabor's

term) a logon, as that which enables us to formulate one

independent proposition, describing one independent feature

of the result. (Whether when we have formulated the proposi-

tion we shall find any metrical information to give it logical

content, is another matter.) The amount of structural in-

formation in a result, the logon-content, is thus the number of

* First published in Philosophical Nagazine, 1950，41，pp. 289-311. STRUCTURAL INFORMATION-CONTENT

179

independent categorics or degrces of frccdom precisely definable in its description.

LOGON-CAPACITY. In many cases structure is defined in tcrms of a reference-coordinate. For example the density- pattern on a photographic plate can be described by a function of one or more space-coordinatcs; and the structure of a telephone signal can be specificd by a time function. The logon-capacity of an experimental mcthod can in such cases be defined as the number of logons which it specifies per unit of coordinate-interval, or coordinate-space if several coordinates are involved. The total number of indcpendent categories or featurcs in the result is then the integral of the logon-capacity over the cxtent of coordinate-tract occupied.

Thus the logon-capacity of a microscope in a particular region in the focal plane can be defincd in logons/cm.2, and measurcs the resolving-power in that region; for suitable test-objects a resolving power in a given direction can also be defined, in logons/cm. The logon-capacity of a galvanom- eter or a communication-channel is measured in logons per second, and represents the number of (practically)independent readings per second which can be made with the apparatus.

FREQUENCY-RESPONSE. It is useful here to introduce the idca of frequcncy-response in a somewhat generalized form. With instruments measuring functions of time it is common practice to definc pcrformance in terms of the frequency-response of the instruments to sinusoidal inputs of different time-periodicitics. In the same way one can define Fouricr-variables associated with other coordinates, in order to assess the performance of other types of instrumcnts.

For examplc one could use sinusoidal density-patterns of different space-periodicities to define the"frequency-response" of a microscope, if one may so extend the use of the term. In each case a precise mcaning can be given to the frequency- bandwidth of an instrument, as the effective range of input- frequencies(i.e. of the Fouricr-variable) to which it is sensitive. 180

APPENDIX

(For cxample in a microscope this is a space-frequency

range normally extending from zero to a value directly

proportional to the aperture used. It thus measures the

finencss of detail perceptible, in terms of a Fouricr-type of

analysis of the transparency-function which represents the

object. Onc nced hardly say that "frequency" here is quite

distinct from the frcquency of the light used.) It should be

noted that with more than one coordinate the Fourier-

variables must be represented in a Fouricr-spacc in which

"bandwidth" is defined by a "volume" not necessarily

rectangular.*

BANDWIDTH AND LOGON-CAPACITY. The bandwidth of an

instrument in the above sense is dircctly rclated to its logon-

capacity. The relation arises from the well-known uncertainty-

principle which can be written

△f·△q≥K,

(1)

where Af represcnts the effective range of frequencics (con-

jugate to a coordinate g) to which the apparatus is sensitive,

Ag twice the "uncertainty"t in g, and K, a number which

we may take to have the value .

Equation(1) will now be justificd from our present point of

view. It mcans that points on the g-axis cannot be defined

uniquely at closer intervals than K/Af, so that the logon-

capacity is Af/K, or 2 Af. To attempt to talk of "an interval

smaller than Ag" would be to try to construct a logical

pattern identical with that of "a frcqucncy higher than

Af", which cannot by definition appear in any result and is

therefore observationally meaningless. The logon-content

l of an experiment involving a tract of extent g is thus:

l≤ q·△f|K,≤ 2q·Δf

(2)

.The author is indebted to a correspondent for raising this point. tI.c., Ag is the effective range of g. STRUCTURAL INFORA1ATION-CONTE.VT

181

STRUCTURALLY-DEFINED SCALE-UNITS

THE STRUCTURAL INFORMATION-AXIOM. In structural prop- ositions the absolute magnitude of y is irrelevant. They are essentially definitions of propositional functions of which y is to be the argument. Accordingly the scale-unit of g can be defined only in terms of coincidence-relations indepcendent of the magnitude of y. In the forcgoing section we used the concept of bandwidth (gencralized) to define a scalc-unit Ag which was a property of the apparatus used, ascertainable beforehand by an independent experiment, and hence counting as prior information on subsequent occasions. The general relation (1)which we used then can be justified dircctly in terms of our initial axiom that only coincidence- relations or compounds thereof are valid as logical elements in scientific statements.

Let us consider then the case of a simple harmonic function of g, with periodicity f. It will be associated with definitive points on the g-axis, independent of amplitude, whenever the function crosses the axis, i.e. at intervals of half a period. (It is also arguable that ingenious experimentation should make it possible to define the quarter-period or the radian-period independently of amplitude.)

In any case, the scale of g is conceptually provided with a set of points at intervals of K/, where K, is of the order 1.

These points, however, are all logically indistinguishable, representing collcctively a single fact- the accurate value of What we want is a set of uniqucly identifiable points, to serve as labels. To single out desired points we must provide a comparison-pattern to act as a "pointer". For instance a frequency f- Af will producc a pattern coinciding with the first at intervals of K, /Af. If all values of Af from zero can be observed, a continuous range of intervals from infinity down to K/Af can be observationally defined. The structural scale-unit of q, Ag, is thus K,/Af. Conversely, if Aq is an ar- bitrary interal, the number I of logons relating to it which 182

APPENDIX

can be formulated can be written as I ≤ Ag.Af/K, since l is integral. Thus for a single logon Aq·Af ≥ K, (equation(1). (It should be remembered that in practice the terms"effective length" and "bandwidth" often have a slightly different numerical connotation from that here employed.)

RESOLVING-POWER. To illustrate these ideas we may examine the problem of optical resolving-power. As our purpose is only expository we shall consider the somewhat unrealistic case of a narrow rectangular apcrture and an ideal object which can be represented by a transparency- function of only one coordinate, x say, parallel to the long edge of the aperture. The situation can then be represcnted by the two-dimensional diagram of Fig. 1. P is a point on the aper- ture, with coordinates (r, 0) relative to a point O on the object. Light is incident in the direction Oy. The problem has two parts. Firstly, we shall establish a relation between the

↑x

P

N

Ax λ/2 sin 0

Fig. 1 Normal incidence. STRUCTURAL INFORMATION-CONTENT

183

position of P and the information gained through it about the object; and secondly, we can calculate the logon-capacity for a given type of aperture.

Suppose that light of wavelength λ is reccived through P. This makes it possiblc to distinguish logically points along the possible light paths to P at intervals of A/2, so that, with centre P, we can give logical significance to a series of arcs of radii nA/2, where n has integral values. These arcs will intersect the x-axis and establish coincidence-relations with the incident wavefront at intervals of A/2 sin 0, in the vicinity of O. There is thus a correspondence betwcen the point P and a space-function having a periodicity f =(sin 0)/A in the object. Indeed if the aperture is closed everywhere except at P and the pole, N, the pattern secn has just this periodi- city.

This analysis has assumcd that a plane wavefront was incident normally on the x-axis. If instead the light is incident in the xy plane at an angle to Ox (Fig. 2) the possible light- paths from P must be traced through the object to their origin on the incident wavefront; and the logically describable paths will be those whose total lengths are integral multiples of A/2. The corresponding spacc-periodicity defined on the x-axis will then be f = (1/)(sin 0 + sin φ).

To calculate the logon-capacity we nced only observe that the "bandwidth" is directly proportional to the range of sin 0. Thus if 0 can have all values between ±0m, Af =(2 / 入) (sin 0m), and the logon-capacity is (4/)(sin 0m) logons per cm.

This logon-capacity will not, however, be realized in the case of normal incidence, for then f is only (1/A) sin 0m, and only (2/A) sin 0m points are spccificd on the x-axis. Only by increasing to 0m can the full resolving-power be achieved. Increasing ф beyond this value, to give so-called "dark-ground illumination", will increase f but not Af. The number of logons per cm. will not be increased, though owing to the removal of background light the visibility of dctail is generally improved. 184

APPENDIX ↑x

P

N

↑

>

2(sin 0+ sin )

Fig. 2 Incidence at angle d.

(B) The Structural Information-Capacity of

Optical Instruments*

INTRODUCTION

In the theory of communication much use is made of the well-known "sampling theorem"(Gabor, Ref. 6; Shannon, Ref. 31)of Fourier analysis which states that a function re- stricted to a frequency bandwidth IV/scc may be specified uniquely by 2IV equally-spaced samples per sccond. This is * Informction and Control, Academic Press Inc., 1958，1，pp. 148-52. (Copyright Academic Press Inc.) STRUCTURAL INFORMATION-CONTENT

185

usually interpreted as implying that such a signal of duration T has 2TIV degrces of freedom (called "logons" by Gabor). The number of degrees of freedom is taken to be proportional to the area of"Fourier-space"occupied.

In the theory of optical resolving powcr the same ideas can be used without apparent difficulty in the case of a one- dimensional aperture, where aperture-width takes the place of bandwidth, and objcct-length the place of time-duration (MacKay, Ref. 11). Once again the number of dcgrces of freedom appcars to be proportional to the arca of Fourier- space occupied.

When, however, onc considers a two-dimcnsional apcrture, an apparent paradox appcars. Reasoning along the same lincs, one finds the number of degrces of freedom or logon-content of an image to be proportional to the product of the number for each dimension, and hence to the arca of the apcrture(Gabor, Ref. 7; Toraldo di Francia, Ref. 37). This, however, would imply that a microscope with a line-aperture (e.g. a lincar or annular slit of vanishingly small arca), should have no rc- solving-power; whereas it is easily verified that this is not the case.As the width of a rectangular apcrture is diminished to zero, the resolving-power in the corresponding dircction becomes smaller and smaller; but resolution in the othcr direction is unaffected, and the total number of logons tends to a lower limit proportional to the width in that direction. With an annular aperturc this fact is even more convincingly demonstrated. The apparent paradox has led some7 to suggcst that the signal-noise-ratio ought to be brought into the defini- tion of logon-content, while others (Good, Rcf. 8)have sought to resolve it by using notions of one-to-one mapping to throw doubt on the present definition.

THE FORMULA FOR LOGON-CONTENT

I have suggested elsewhere20 that the paradox may be simply resolved without recourse to such complications, * Gabor, personal communication(1953). 186

APPENDIX

for it is not a paradox but a mistakc. The logon-content of a signal occupying bandwidth IV and time T is not 2TIV, but (2TW+ 1)，for the mean value offers one extra degree of freedom. Similarly with a onc-dimensional optical aperturc, of numerical aperture a and an image width X, thelogon-content in di Francia's notation³7 should be [(2aX/) + 1] and not 2aX/λ. A rectangular aperture a x β with an image X x Y gives a logon-content [(2aX/)+ 1][(28Y/A]+1] which tends to [(2aX/) + 1], and not to zero as β tends to zcro*.

It is possible to reach this conclusion in another way by considering the number of logically-discriminablc points in the field of view. In the early paper referred to11 the author showed that this was (2aX/A) in the one-dimensional case, but unfortunatcly pcrpctratcd the same mistake as the communication engincer by idcntifying the logon-content with this number instead of with [(2aX/)+1]. With wisdom after the event, it is obvious that a singlc logically-discrimin- able point divides a field into two logically-discriminable regions, so that the ficld then has not one but two descriptive degrees of freedom or logons. x logically-discriminable points divide the X-dimension into (x+1) discriminable regions; in the other direction ly logically-discriminable points divide the Y-dimcnsion into (ly 1) regions. The result in the two-dimensional case is a logon-content of (lx+ 1)(ly+1). THE RELEVANCE OF NOISE

The correction of this mistake would be a small matter were it not for the doubts which the apparent "paradox"has aroused about the validity of logon-content as an a priori measure of logical dimcnsionality. As mentioncd carlicr, the suggestion has been made, first that logon-content cannot be defined without reference to signal-noise ratio, and second, that "logical dimensionality" is indefinite becausc an n- In his recent book, Scicnce and Information Theory (Academic Press Inc., New York, 1956, p. 97), L. Brillouin has given the corrcct cxpression for the logon-content, although without using the term. STRUCTURAL INFORMATION-CONTENT

187

dimensional function can be "mapped" into a space of fewer dimensions, without loss of "information."

There is of coursc one obvious truth in the first suggestion. If an instrument has a pass-band or aperture which does not have sharply defined margins, the effective bandwidth will depend upon the minimum signal-level which is detcctable- or at least upon the minimum acceptable ratio of marginal to modal values of the transfer function. The conventional definition of "practically independent amplitudes" in such a case remains to be worked out. But in the common case of a "practically rectangular"transfer-function, as with a band- pass filter or a normal microscope-apcrture, any ambiguity is purely marginal, and in no case affects the order of magni- tude of the logon-capacity, in the way that would have been required had the "paradox" been a genuine one.

RE-MAPPING

The second suggestion, which has been recurrent since 1951 at least, as arises I think from a slight confusion. The basic idea of re-mapping can be pictured as the labelling of each point in one space, by a code-number indicating a corresponding point in another space. Thus an optical image made up of 100 independcnt patches of light, each having 10 possible intensities, would normally be describable as having a logical dimensionality or logon-content of 100. It would be idcntified by a point in a space of 100 dimensions, each having 10 discriminable coordinate-valucs. On the other hand, each point in this space could be labelled with a single number in the range 1--10100, so that the whole could be mapped on to a single dimension having 10100 discriminable coordinate-values.

IDENTIFICATION VERSUS RECONSTRUCTION

Why then could not the original image be described as one- dimensional, with a logon-content of unity? The reason is 188

APPENDIX

quite simple. The logon-content of an image measures the dimensionality of the most economical prescription, not for identifying but for constructing it. Bcfore the onc-dimensional signal could be uscd for the reconstruction of the picture, it would have to be "decoded"-turned back into a prescrip- tion of precisely 100 independent intensities. Logon-content, then, is a genuine invariant, a property of the relation-structure of a signal, determining the minimum number of independent steps required for its reconstruction. Sclective information- content, on the other hand-the logarithm of the number of discriminable points or cells in the descriptive space-is also an invariant, determining the minimum number of independent steps required for the identification or selection of a signal from the ensemble of possible signals. If the steps are binary, yes-or-no steps, the selcctive information-content of our optical image is then log2 (10100) or 100 log2 10. It is proportional to logon-content if all degrecs of freedom have the same number of possible coordinate-values; but an increase in sclective information-content by increasing the number of coordinate-valucs would do nothing to enhance logon-content or resolving power. It is indeed quite possible to adopt measures which increase selective information-content to the detriment of logon-content, giving a brighter picture with poorer resolution. This alonc should make it clear that some measure of information other than selective information- content is relevant to the design of optical instruments.

Nothing that has been said precludes the possibility, in- dicated some years ago by the author 16 and others(Blanc- Lapierre, Ref. 2, Toraldo di Francia, Ref. 37) that an image distorted by an instrument of low resolving-power may be refined if prior knowledge of the image is available. Prior knowledge in effect reduces the independence of the com- ponents of the original, so that its effective number of degrees of freedom is reduced. There is then no paradox in the fact that the number of components in the refinedimage may exceed the logon-capacity of the instrument, since these components STRUCTURAL INFORMATION-CONTENT

189

are not independent. A lucid discussion of the possibility has recently been given by Toraldo di Francia.37

CONCLUSIONS

This brief papcr has had but two objects: to correct a small error which the author has shared in propagating, and to dispose of some misapprehensions rcgarding logon-content as an information-mcasure.

We have secn that if the logon-capacity of an instrument be defined as the number of logically-distinguishablc intercals in the field of view, rather than the number of logically- dcfinable points, this increases by I the usually accepted logon- capacity in each direction, so that an image Xx Y transmitted through a rectangular aperturc a x β has a logon-capacity of [(2aX/A)+ 1] [(28Y/) + 1]. This disposes of the paradox that a linear apcrture of negligible area givcs a finite resolving-power.

The suggestion that signal-noisc ratio be invoked in explanation is thus shown to be unnecessary, although when the transfer-function is non-rcctangular one must considcr amplitudcs in determining "effcctive bandwidth". The idea that onc-to-one mapping Icaves dimensionality indcfinite has been shown to rest on a confusion betwecn the rcquirements for reconstruction and for identification of a signal. Logon-content measures the minimum dimcnsionality of the reconstruction- process. For the minimum complexity of a selcction or identification-proccss, on the other hand, the appropriate mcasure is the familiar sclective information-content; but this may be misleading if uscd uncritically as a criterion of optical performance. References

Author's Note: These references are simply a collation of those in the original papers, and are not mcant to be exhaustive.

1. Bar-Hillel, Y. and Camap, R.: Scmantic Information.In

V. Jackson (Ed.), Communication Theory. London: Buttcrworths,

1953,p.503.

2. Blanc-Lapicrre, A.: Application to Optics of ccrtain rcsults

and methods of Information Thcory. In W. Jackson (Ed.),

Communication Theory. London: Butterworths, 1953，p. 513.

3. Dixon, R. M. W.: What is Language?-A new Approach to

Linguistic Descriplion. London: Longmans Linguistics Library,

1965.

4. Fisher, R. A.: The Design of Experiments. Oliver and Boyd,

1935,p.188.

5. Fodor, J. A. and Katz, J. J. (Eds.): The Structure of Language.

Prentice-Hall, 1964.

6. Gabor, D.: Theory of Communication. J. Inst. Elec. Engrs.,

1946,93,I1I,p. 429.

7. -： Optical Transmission. In Information Theory: Third London

Symposium, E.C. Cherry (Ed.). London: Butterworths, 1956, pp.

26-33.

8. Good, I. J.: Discussion in Information Theory: Third London

Symposium, E. C. Cherry (Ed.). London: Butterworths, 1956,

p.33.

9. Kochen, M., MacKay, D. M., Maron, M. E., Scriven, M. and

Uhr, L.: Computers and Comprehension. RAND Memo. RM-4065,

1964.

10. Lorente de No, R.: Transmission of Impulses through Cranial

Motor Nuclei. J. Neurophysiol., 1939，2，p. 422. REFERENCES

191

11. MacKay, D. M.: On the combination of digital and analogical techniques in the design of analytical engines. 1949. Mimeo- graphed. Reprinted as Appendix to Mechanization of Thought Processes (N.P.L. Symp. No. 10, 1958). London: H.M.S.O., 1959,pp.37-52.

12.

: Quantal Aspects of Scientific Information. Phil. Mag., 1950,41,pp.289-311.

13.

- The Nomenclature of Information Theory; Quantal Aspects of Scientific Information; and Entropy, Time and Information. In Proc. of Information-Theory Symp. London; Sept. 1950. Lithoprinted Amer. Inst. Radio Engrs., 1953.

14.

-: Mindlike Behaviour in Artefacts. Brit. J. Phil. of Sci., 1951, II, pp. 105-21； also 1953，III, pp. 352-53.

15.

Mentality in Machines. Proc. Arist. Soc. Suppt., 1952, XXVI, pp. 61-86.

16. —： Brit. Pat. Appln. 29315/48(1948). Outlined in W. Jackson (Ed.), Communication Theory. London: Butterworths, 1952,p.521.

17.-: The Epistemological Problem for Automata. In C. E. Shannon and J. McCarthy (Eds.), Automata Studies. Princeton: Princeton University Press, 1955，pp. 235-51.

18.--: Complementary Measures of Scientific Information- Content. Methodos, 1955，VI, pp. 63-90.

19.--: Towards an Information-Flow Model of Human Behaviour. Brit. J. Psychol., 1956，47，pp. 30-43.

-: Discussion in Information Theory: Third London Symposium, E. C. Cherry(Ed.). London: Butterworths, 1956，p. 32.

21. —： Operational Aspects of Intellect. In Proc. N.P.L. Conf. on Mechanization of Thought Processes, 1958. London: H.M.S.O., 1959,pp.37-52.

2.-: (a) Information Theory and Human Information Systems. Impact of Science on Society, 1957，8，pp. 86-101. (b)On the Logical Indeterminacy of a Free Choice. Mind, 1960, 69, pp.31-40.

23. -： Information and Learning. In H. Billing (Ed.), Learning Automata. Munich: Oldenbourg, 1961，pp. 40-49.

The Use of Behavioural Language to Refer to Mechan- ical Processes. Brit. J. Phil. of Sci., 1962，XIII, pp. 89-103. 192

REFERENCES

25. Mackay, D.M.: Cerebral Organization and the Conscious Control

of Action. In J. C. Eccles (Ed.), Brain and Conscious Experience.

New York: Springer-Verlag, 1966，pp. 422-45.

26. Miller, G. A.: The Magical Number 7 plus or minus 2. Psychol.

Rec., 1956，63，pp. 81-97.

27. Popper, K. R.: Indeterminism in Classical and Quantum

Physics. Brit. J. Phil. of Sci., 1950，1，117-33 and 173-95.

28. Prior, M. and Prior, A.: Erotetic Logic. Philas. Rev., 1955,

LXIV, pp. 43-59.

29. Rosenblueth, A., Wiener, N. and Bigelow, J.: Behaviour,

Purpose and Teleology. Philosophy of Science, 1943，10，pp. 18-24. 30. Russell, B.: Logic and Knowledge (especially "The Philosophy of

Logical Atomism"(1918) and "Logical Atomism"(1924)).

London: G. Allen and Unwin, 1956.

31. Shannon, C. E.: A Mathematical Theory of Communication.

Bell Syst. Tech. J., 1948，27，pp. 379-423； 623-656.

32.--: Communication in the Presence of Noise. Proc. I.R.E.,

1949,37,pp.10-21.

33.--: Prediction and Entropy of Printed English. Bell Syst.

Tech.J., 1951，30，pp. 50-64.

34. -： In H. von Foerster (Ed.), Cybernetics. Trans. of 8th Conf.,

Josiah Macy Jr. Foundation, New York, 1951, p. 219.

35. Shannon, C. E. et al.: In Cybernetics, loc. cit., p. 195.

36. Shannon, C. E. and Weaver, W.: The Mathematical Theory of

Communication. Illinois: University of Illinois Press, 1949.

37. Toraldo di Francia, G.: Resolving Power and Information.

J. Opt. Soc. Am., 1955，45，pp. 497-501.

38. Ullman, S.: The Principles of Senantics. Glasgow: Jackson, 1951. 39. Wiener, N.: Cybernetics. New York: John Wilcy, 1948.

40. Wittgenstein, L.: Philosoplrical Investigations, trans. G. E. M.

Anscombe. Oxford: Oxford University Press, 1953; 2nd Ed.

1958.

41. Yngve, V. H.: The Translation of Languages by Machine.

In E. C. Cherry (Ed.), Information Theory. London: Butterworths,

1956,pp.195-205. Index*

Abstraction, hicrarchy of, 53

Comnitment, religious, 114

Accuracy of measurement, limits to,

Communication,20,74,96,108,

1, 1781T.

171

Actor-language, 58fT.

cross-cultural,105

Adaptive matching-response, 31,

failure of, 111

61-69,73,112

system,15,171

Adaptive trial and error, 69, 72,

untruthful, 29, 163

142

Complemcntarity, 1

Advice, 131

Conditional entropy, 173

Airy disc.5

Conditional probabilities, 34，62，

Ambiguitics of visual perception, 69

73

Amount of information, mcasurcs of,

Conditional probability matrix

10,42、57,158,171-175

(C.P.M.), 84, 95, 106

Artifacts,probabilistic,54,140

Conditional readiness (for behav-

Artificial language(s),35,81,90,

iour), 22, 70

109

Consciousness,53

Attention, 61

Content-clements, 81

Atomic propositions, 2, 59, 81, 172

Content-measures,81

Bandwidth, 175,178ff.

Descriptive information-content, 12

Bar-Hillel, Y., 81

15,45,59,82,159

Basic symbols, 51, 54, 61

Dialogue, 126, 153

Basic vectors, 48, 72

Binary digit, bit, 16, 172

Eddington, A.S., 2, 17

Blanc-Lapicrrc,A.,188

Elementary events, 3, 160

Blind spots, cpistemological, 113

Elementary symbols, 50

Boltzmann, L., 57

Entropy, 3,57,172

Brain mechanisms, 23, 26, 63

conditional, 173

Brillouin,L.,186

relative,173

thermodynamic, 16, 174

Capacity of channel, 15, 134,173

Enscmble

Carnap, R.,81

of possible messages, 57

Central nervous system, 63-66

of states of readiness, 71

Coding, 46, 173

Equivocation, 173

Coincidence relations, 2, 168

Evaluatory feedback, 67, 140ff.

Commands,100,130

Evidence, weight of, 49

*Pagenumbersprinted in italics refer to definitions or explanationsofterins. 194

INDEX

Failure of communication, 111

units of, 4，160fT.

Feed-back,evaluative,67,141

vector,45,71,92,169

Fisher,R.A., 4,5, 169

Information-content,56,157

Fourier analysis, 184

descriptive or scientific, 12, 15,

Fourier-space,185

45,59,82,159

Frequency-response,179

metrical, 4，14，44，48,159,166 sclective, 10-14，71，75，147，159，

Gabor, D., 4，5，165，178，184-185

172

Goal-complex,106,112

semantic, 59, 83

Goal-directed activity, 35, 60, 67,

structural, 14，159，165,178ff.

95,106

Informational efliciency, 3, 15

Goal-settings, hierarchy of, 90, 106 Internal organisers, 113

Good, I. J., 185

Internal representation, 50, 68, 112, 125,142

Interrogative utterances, 31, 97, 107

Heisenberg's Principle of Uncer- Intonation, function of, 32, 98

tainty,1,148

Instructions,130

Hicrarchy

of abstraction,53

of goals, 90, 106

Kantian catcgories, 69

of readincss, 60

of transition probabilities, 69

Learning, 70

Human beings as information Linguistic understanding, 121

Logical atomism, 3, 27

sources, 153

Hyperspace, multidimensional, 44 Logical dimensionality (of repre-

Hypothesis-generation, 53, 70

sentation), 4，5，165，178f. Logical indeterminacy, 132, 147 Logon,4, 165

Ideal language,93

Logon-capacity,166, 179,189

Imagining, 75

Logon- content, 5, 102,165, 178g.

Imperative meaning, 101

Indeterminacy, logical, 132, 147

*Magic number 7'，103

Indicative meaning of a question, Matching response, adaptive, 51,

35,100

61-69,73,112,142

Inductive probability, 81

'Mathematical Theory of Com-

Information, 10，14，19，56，70，76，

munication'(C. E. Shannon),

80,96,108,132,158

5, 79,passim

amount of, 10, 42, 57, 158

Matrix of conditional or transition-

as answer to question, 12

probabilitics (C.P.M.or

Fisher's measure of, 4，169

T.P.M.), 62, 83, 95, 106

gencration of, 137

Meaning

humans as sources of, 153

and information, 5，20，24，46，53，

irrelevant,74

71,79,83,91,96,108

operational definition of, 60, 157

conventional,25,84,90

quantization of, 2,3,164

definition of, 24，71，84，128

semantic, 19，79., 89，95,107

effective, received or understood,

source of 135, 146f., 153

25,72,84

space,44,92,169

imperative, 101

and time, 16

of indicative sentences, 22,96 INDEX

195

intended,25,72

Physiological processes, random,

interrogative, 35,100

143

shades of, 49

Popper, K.S., 153

spectrum of, 48

Potentiation, physiological, G5

symbolic representation of, 72

Probabilistic artifacts, 54,140

Meaningfulness, criterion of, 19, 21,

Probabilitics, conditional, 34，62,73

36,89

Probability-distribution, condition-

Meaninglessness, 21, 36, 85, 111,

al, 73

128

Promises, 131

Mechanical translation, 90

Memory,64-66

Quantization of information, 2, 3,

Messages as'keys', 25，27,109-111

164

Metrical information-content,4,14,

Quantum of action, 1

44,48,159,166

Questions, 31, 73, 130

Metron, metrical unit of informa-

tion, 5, 166

Randomness,133

Microscope, resolving power of, 185

Random physiological processes, 143

Miller, G. A., 103

Rcasoning mechanisms, 46, 49

Mismatch (in feed-back system), G9

Redundancy, 173

Misunderstanding, 129

Relative entropy, 173

Relevance(of information), 49, 56,

Natural selection (of organizing sub-

59,73,170

routincs),141

Religious commitment, 114

Nervous system, 63-66

Repertoire,95

Noise, 134,186

Replication (as a form of repre-

in automata, 136

sentation),50

semantic,74

Representation of meaning, sym-

Numerical energy, 167

bolic, 72

Representations, 3，42,49,68,80，

Occupance-relations, 2

89,112,158,161

Observer-language, 58,61

Requcsts, 100, 130

Operational approach (to informa-

Resolving power

tion theory), 157

of measurements, 1, 16G

Operationalists,27f.

optical,178,185

Optical illusions, 69

Response, matching, G1, G7

Optical resolving power, 178, 185

Response-space, 73

Order-number (of hierarchic level),

Russell, B., 27

102

Organiser, internal,113

Scicntific experimentation, 11, 14

Organising or orientirg function, 36,

Scientific information(measures of),

96m.,108,111

43

Originality, 137

Scientific representation, 3, 164ff.

Second law of thermodynamics, 16

Partial participation (of elements in

Selective function (of message,

concept),47

question),24,35,108

Pattern of demand, 112

Selective information-content, 10-

IPerception, 61, 68, 9G

14,71,75,147,159,172

ambiguitics of, G9

Self-organisation, 140 196

INDEX

Semantic information, information- Toraldodi Francia,G.,185,188-189

content,19,59,79.,95,107 'Tractatus Logico-Philosophicus',

Semantic noise, 74

2, 27

Semantic units (and critcria of Transition-probability matrix,52,62

truthfulncss),28

Translation, mechanical, 90

Shannon, C.E., 5, 19, 43, 59, 79, Transmission, speed of (as adaptive

94,171,184

parameter), G6

Social groups, units, 10G,115- Trial and error (adaptive), 69，72，

118

142

Spectrum of meaning, 48

Truthfulness, criteria of, 28

Specd of transmission (as adaptive

parameter),66

Uncertainty

States of (conditional) readiness,

absolute, 148，150，154

19,34,60,75,142

and information content, 147

ensemble of, 75

principles,1,146

Statistical approximation to Eng- Understanding, non-linguistic ver-

lish,139

sus linguistic, 121

Stimulus equivalence, 121

Unexpectedness as measure of in-

Structural information content, 14,

formation,57,94,133,160

159,165,178.

Units of information, 4,160ff.

Symbolic representation of meaning, Universal language, 77

72

Universals,53

Symbols, basic, intermal,49-54, 113, Unpredictability, 146

141

Synonymy, 86

Valuative feed-back, 67, 140

Values in relation to communica-

Temporal relationships in neural

tion barriers,114

networks,66

Variational approach, 99, 124

Theory of information, glossary of Vector representation of informa-

terms used in, 161-177

tion, 44,71,92,169

Thermodynamics and information Vectors, basic, 48, 72

theory, 16, 174

Visual perception, ambiguities of,69

Thesauri,103

Threshold configurations (as in- Warning(as communication),130

ternal representations),141

Weight of evidence, 4，5，49，166

Threshold-control,G5

Wiener,N., 9, 171

Time and information, 1G

Wittgenstein, L., 2, 27, 30, 1G4


Contents

Introduction

Preface

vii

1. Background

1

Part I. Three Introductory Talks

2. Measuring Information

9

3. Mcaning and Mechanism

19

4. What Makcs a Question?

31

Part II. Information, Communication and

Meaning

5. In Search of Basic Symbols

41

6. Operational Aspccts of Some Fundamental Concepts of Human Communication

56

7. The Place of 'Meaning' in the Theory of Information

79

8. The Informational Analysis of Qucstions and Commands

94

9. Communication and Meaning-a Functional Approach

105

10. Linguistic and Non-Linguistic "Understand- ing" of Linguistic Tokens

120

11. Comprehension of Utterances-Some Conclud- ing Notes

128

12. Generators of Information

132

13. Indeterminacy, Uncertainty and Information- Content

146

Appendix The Nomenclature of Information Thcory with Postcript on Structural Information-Content and Optical Resolution

156

References

190

Index
