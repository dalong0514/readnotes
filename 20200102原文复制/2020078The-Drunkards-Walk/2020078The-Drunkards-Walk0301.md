# 0301. Finding Your Way through a Space of Possibilities

IN THE YEARS leading up to 1576, an oddly attired old man could be found roving with a strange, irregular gait up and down the streets of Rome, shouting occasionally to no one in particular and being listened to by no one at all. He had once been celebrated throughout Europe, a famous astrologer, physician to nobles of the court, chair of medicine at the University of Pavia. He had created enduring inventions, including a forerunner of the combination lock and the universal joint, which is used in automobiles today. He had published 131 books on a wide range of topics in philosophy, medicine, mathematics, and science. In 1576, however, he was a man with a past but no future, living in obscurity and abject poverty. In the late summer of that year he sat at his desk and wrote his final words, an ode to his favorite son, his oldest, who had been executed sixteen years earlier, at age twenty-six. The old man died on September 20, a few days shy of his seventy-fifth birthday. He had outlived two of his three children; at his death his surviving son was employed by the Inquisition as a professional torturer. That plum job was a reward for having given evidence against his father.

Before his death, Gerolamo Cardano burned 170 unpublished manuscripts.1 Those sifting through his possessions found 111 that survived. One, written decades earlier and, from the looks of it, often revised, was a treatise of thirty-two short chapters. Titled The Book on Games of Chance, it was the first book ever written on the theory of randomness. People had been gambling and coping with other uncertainties for thousands of years. Can I make it across the desert before I die of thirst? Is it dangerous to remain under the cliff while the earth is shaking like this? Does that grin from the cave girl who likes to paint buffaloes on the sides of rocks mean she likes me? Yet until Cardano came along, no one had accomplished a reasoned analysis of the course that games or other uncertain processes take. Cardano’s insight into how chance works came embodied in a principle we shall call the law of the sample space. The law of the sample space represented a new idea and a new methodology and has formed the basis of the mathematical description of uncertainty in all the centuries that followed. It is a simple methodology, a laws-of-chance analog of the idea of balancing a checkbook. Yet with this simple method we gain the ability to approach many problems systematically that would otherwise prove almost hopelessly confusing. To illustrate both the use and the power of the law, we shall consider a problem that although easily stated and requiring no advanced mathematics to solve, has probably stumped more people than any other in the history of randomness.

AS NEWSPAPER COLUMNS GO, Parade magazine’s「Ask Marilyn」has to be considered a smashing success. Distributed in 350 newspapers and boasting a combined circulation of nearly 36 million, the question-and-answer column originated in 1986 and is still going strong. The questions can be as enlightening as the answers, an (unscientific) Gallup Poll of what is on Americans’ minds. For instance:

When the stock market closes at the end of the day, why does everyone stand around smiling and clapping regardless of whether the stocks are up or down?

A friend is pregnant with twins that she knows are fraternal. What are the chances that at least one of the babies is a girl?

When you drive by a dead skunk in the road, why does it take about 10 seconds before you smell it? Assume that you did not actually drive over the skunk.

Apparently Americans are a very practical people. The thing to note here is that each of the queries has a certain scientific or mathematical component to it, a characteristic of many of the questions answered in the column.

One might ask, especially if one knows a little something about mathematics and science,「Who is this guru Marilyn?」Well, Marilyn is Marilyn vos Savant, famous for being listed for years in the Guinness World Records Hall of Fame as the person with the world’s highest recorded IQ (228). She is also famous for being married to Robert Jarvik, inventor of the Jarvik artificial heart. But sometimes famous people, despite their other accomplishments, are remembered for something they wished had never happened (「I did not have sexual relations with that woman」). That may be the case for Marilyn, who is most famous for her response to the following question, which appeared in her column one Sunday in September 1990 (I have altered the wording slightly):

Suppose the contestants on a game show are given the choice of three doors: Behind one door is a car; behind the others, goats. After a contestant picks a door, the host, who knows what’s behind all the doors, opens one of the unchosen doors, which reveals a goat. He then says to the contestant,「Do you want to switch to the other unopened door?」Is it to the contestant’s advantage to make the switch?2

The question was inspired by the workings of the television game show Let’s Make a Deal, which ran from 1963 to 1976 and in several incarnations from 1980 to 1991. The show’s main draw was its handsome, amiable host, Monty Hall, and his provocatively clad assistant, Carol Merrill, Miss Azusa (California) of 1957.

It had to come as a surprise to the show’s creators that after airing 4,500 episodes in nearly twenty-seven years, it was this question of mathematical probability that would be their principal legacy. This issue has immortalized both Marilyn and Let’s Make a Deal because of the vehemence with which Marilyn vos Savant’s readers responded to the column. After all, it appears to be a pretty silly question. Two doors are available—open one and you win; open the other and you lose—so it seems self-evident that whether you change your choice or not, your chances of winning are 50/50. What could be simpler? The thing is, Marilyn said in her column that it is better to switch.

Despite the public’s much-heralded lethargy when it comes to mathematical issues, Marilyn’s readers reacted as if she’d advocated ceding California back to Mexico. Her denial of the obvious brought her an avalanche of mail, 10,000 letters by her estimate.3 If you ask the American people whether they agree that plants create the oxygen in the air, light travels faster than sound, or you cannot make radioactive milk safe by boiling it, you will get double-digit disagreement in each case (13 percent, 24 percent, and 35 percent, respectively).4 But on this issue, Americans were united: 92 percent agreed Marilyn was wrong.

Many readers seemed to feel let down. How could a person they trusted on such a broad range of issues be confused by such a simple question? Was her mistake a symbol of the woeful ignorance of the American people? Almost 1,000 PhDs wrote in, many of them math professors, who seemed to be especially irate.5「You blew it,」wrote a mathematician from George Mason University:

Let me explain: If one door is shown to be a loser, that information changes the probability of either remaining choice—neither of which has any reason to be more likely—to 1/2. As a professional mathematician, I’m very concerned with the general public’s lack of mathematical skills. Please help by confessing your error and, in the future, being more careful.

From Dickinson State University came this:「I am in shock that after being corrected by at least three mathematicians, you still do not see your mistake.」From Georgetown:「How many irate mathematicians are needed to change your mind?」And someone from the U.S. Army Research Institute remarked,「If all those PhDs are wrong the country would be in serious trouble.」Responses continued in such great numbers and for such a long time that after devoting quite a bit of column space to the issue, Marilyn decided she would no longer address it.

The army PhD who wrote in may have been correct that if all those PhDs were wrong, it would be a sign of trouble. But Marilyn was correct. When told of this, Paul Erdös, one of the leading mathematicians of the twentieth century, said,「That’s impossible.」Then, when presented with a formal mathematical proof of the correct answer, he still didn’t believe it and grew angry. Only after a colleague arranged for a computer simulation in which Erdös watched hundreds of trials that came out 2 to 1 in favor of switching did Erdös concede he was wrong.6

How can something that seems so obvious be wrong? In the words of a Harvard professor who specializes in probability and statistics,「Our brains are just not wired to do probability problems very well.」7 The great American physicist Richard Feynman once told me never to think I understood a work in physics if all I had done was read someone else’s derivation. The only way to really understand a theory, he said, is to derive it yourself (or perhaps end up disproving it!). For those of us who aren’t Feynman, re-proving other people’s work is a good way to end up untenured and plying our math skills as a checker at Home Depot. But the Monty Hall problem is one of those that can be solved without any specialized mathematical knowledge. You don’t need calculus, geometry, algebra, or even amphetamines, which Erdös was reportedly fond of taking.8 (As legend has it, once after quitting for a month, he remarked,「Before, when I looked at a piece of blank paper my mind was filled with ideas. Now all I see is a blank piece of paper.」) All you need is a basic understanding of how probability works and the law of the sample space, that framework for analyzing chance situations that was first put on paper in the sixteenth century by Gerolamo Cardano.

GEROLAMO CARDANO was no rebel breaking forth from the intellectual milieu of sixteenth-century Europe. To Cardano a dog’s howl portended the death of a loved one, and a few ravens croaking on the roof meant a grave illness was on its way. He believed as much as anyone else in fate, in luck, and in seeing your future in the alignment of planets and stars. Still, had he played poker, he wouldn’t have been found drawing to an inside straight. For Cardano, gambling was second nature. His feeling for it was seated in his gut, not in his head, and so his understanding of the mathematical relationships among a game’s possible random outcomes transcended his belief that owing to fate, any such insight is futile. Cardano’s work also transcended the primitive state of mathematics in his day, for algebra and even arithmetic were yet in their stone age in the early sixteenth century, preceding even the invention of the equal sign.

History has much to say about Cardano, based on both his autobiography and the writings of some of his contemporaries. Some of the writings are contradictory, but one thing is certain: born in 1501, Gerolamo Cardano was not a child you’d have put your money on. His mother, Chiara, despised children, though—or perhaps because—she already had three boys. Short, stout, hot tempered, and promiscuous, she prepared a kind of sixteenth-century morning-after pill when she became pregnant with Gerolamo—a brew of wormwood, burned barleycorn, and tamarisk root. She drank it down in an attempt to abort the fetus. The brew sickened her, but the unborn Gerolamo was unfazed, perfectly content with whatever metabolites the concoction left in his mother’s bloodstream. Her other attempts met with similar failure.

Chiara and Gerolamo’s father, Fazio Cardano, were not married, but they often acted as if they were—they were known for their many loud quarrels. A month before Gerolamo’s birth, Chiara left their home in Milan to live with her sister in Pavia, twenty miles to the south. Gerolamo emerged after three days of painful labor. One look at the infant and Chiara must have thought she would be rid of him after all. He was frail, and worse, lay silent. Chiara’s midwife predicted he’d be dead within the hour. But if Chiara was thinking, good riddance, she was let down again, for the baby’s wet nurse soaked him in a bath of warm wine, and Gerolamo revived. The infant’s good health lasted only a few months, however. Then he, his nurse, and his three half brothers all came down with the plague. The Black Death, as the plague is sometimes called, is really three distinct diseases: bubonic, pneumonic, and septicemic plague. Cardano contracted bubonic, the most common, named for the buboes, the painful egg-size swellings of the lymph nodes that are one of the disease’s prominent symptoms. Life expectancy, once buboes appeared, was about a week.

The Black Death had first entered Europe through a harbor in Messina in northeastern Sicily in 1347, carried by a Genoese fleet returning from the Orient.9 The fleet was quickly quarantined, and the entire crew died aboard the ship—but the rats survived and scurried ashore, carrying both the bacteria and the fleas that would spread them. The ensuing outbreak killed half the city within two months and, eventually, between 25 percent and 50 percent of the population of Europe. Successive epidemics kept coming, tamping down the population of Europe for centuries. The year 1501 was a bad one for the plague in Italy. Gerolamo’s nurse and brothers died. The lucky baby got away with nothing but disfigurement: warts on his nose, forehead, cheeks, and chin. He was destined to live nearly seventy-five years. Along the way there was plenty of disharmony and, in his early years, a good many beatings.

Gerolamo’s father was a bit of an operator. A sometime pal of Leonardo da Vinci’s, he was by profession a geometer, never a profession that brought in much cash. Fazio often had trouble making the rent, so he started a consulting business, providing the highborn with advice on law and medicine. That enterprise eventually thrived, aided by Fazio’s claim that he was descended from a brother of a fellow named Goffredo Castiglioni of Milan, better known as Pope Celestine IV. When Gerolamo reached the age of five, his father brought him into the business—in a manner of speaking. That is, he strapped a pannier to his son’s back, stuffed it with heavy legal and medical books, and began dragging the young boy to meetings with his patrons all over town. Gerolamo would later write that「from time to time as we walked the streets my father would command me to stop while he opened a book and, using my head as a table, read some long passage, prodding me the while with his foot to keep still if I wearied of the great weight.」10

In 1516, Gerolamo decided his best opportunity lay in the field of medicine and announced that he wanted to leave his family’s home in Milan and travel back to Pavia to study there. Fazio wanted him to study law, however, because then he would become eligible for an annual stipend of 100 crowns. After a huge family brawl, Fazio relented, but the question remained: without the stipend, how would Gerolamo support himself in Pavia? He began to save the money he earned reading horoscopes and tutoring pupils in geometry, alchemy, and astronomy. Somewhere along the way he noticed he had a talent for gambling, a talent that would bring him cash much faster than any of those other means.

For anyone interested in gambling in Cardano’s day, every city was Las Vegas. On cards, dice, backgammon, even chess, wagers were made everywhere. Cardano classified these games according to two types: those that involved some strategy, or skill, and those that were governed by pure chance. In games like chess, Cardano risked being outplayed by some sixteenth-century Bobby Fischer. But when he bet on the fall of a couple of small cubes, his chances were as good as anyone else’s. And yet in those games he did have an advantage, because he had developed a better understanding of the odds of winning in various situations than any of his opponents. And so for his entrée into the betting world, Cardano played the games of pure chance. Before long he had set aside over 1,000 crowns for his education—more than a decade’s worth of the stipend his father wanted for him. In 1520 he registered as a student in Pavia. Soon after, he began to write down his theory of gambling.

LIVING WHEN HE DID, Cardano had the advantage of understanding many things that had been Greek to the Greeks, and to the Romans, for the Hindus had taken the first large steps toward employing arithmetic as a powerful tool. It was in that milieu that positional notation in base ten developed, and became standard, around A.D. 700.11 The Hindus also made great progress in the arithmetic of fractions—something crucial to the analysis of probabilities, since the chances of something occurring are always less than one. This Hindu knowledge was picked up by the Arabs and eventually brought to Europe. There the first abbreviations, p for「plus」and m for「minus,」were used in the fifteenth century. The symbols + and - were introduced around the same time by the Germans, but only to indicate excess and deficient weights of chests. It gives one a feeling for some of the challenges Cardano faced to note that the equal sign did not yet exist, to be invented in 1557 by Robert Recorde of Oxford and Cambridge, who, inspired by geometry, remarked that no things could be more nearly alike than parallel lines and hence decided that such lines should denote equality. And the symbol ×, for multiplication, attributable to an Anglican minister, didn’t arrive on the scene until the seventeenth century.

Cardano’s Book on Games of Chance covers card games, dice, backgammon, and astragali. It is not perfect. In its pages are reflected Cardano’s character, his crazy ideas, his wild temper, the passion with which he approached every undertaking—and the turbulence of his life and times. It considers only processes—such as the toss of a die or the dealing of a playing card—in which one outcome is as likely as another. And some points Cardano gets wrong. Still, The Book on Games of Chance represents a beachhead, the first success in the human quest to understand the nature of uncertainty. And Cardano’s method of attacking questions of chance is startling both in its power and in its simplicity.

Not all the chapters of Cardano’s book treat technical issues. For instance, chapter 26 is titled「Do Those Who Teach Well Also Play Well?」(he concludes,「It seems to be a different thing to know and to execute」). Chapter 29 is called「On the Character of Players」(「There are some who with many words drive both themselves and others from their proper senses」). These seem more「Dear Abby」than「Ask Marilyn.」But then there is chapter 14,「On Combined Points」(on possibilities). There Cardano states what he calls「a general rule」—our law of the sample space.

The term sample space refers to the idea that the possible outcomes of a random process can be thought of as the points in a space. In simple cases the space might consist of just a few points, but in more complex situations it can be a continuum, just like the space we live in. Cardano didn’t call it a space, however: the notion that a set of numbers could form a space was a century off, awaiting the genius of Descartes, his invention of coordinates, and his unification of algebra and geometry.

In modern language, Cardano’s rule reads like this: Suppose a random process has many equally likely outcomes, some favorable (that is, winning), some unfavorable (losing). Then the probability of obtaining a favorable outcome is equal to the proportion of outcomes that are favorable. The set of all possible outcomes is called the sample space. In other words, if a die can land on any of six sides, those six outcomes form the sample space, and if you place a bet on, say, two of them, your chances of winning are 2 in 6.

A word on the assumption that all the outcomes are equally likely. Obviously that’s not always true. The sample space for observing Oprah Winfrey’s adult weight runs (historically) from 145 pounds to 237 pounds, and over time not all weight intervals have proved equally likely.12 The complication that different possibilities have different probabilities can be accounted for by associating the proper odds with each possible outcome—that is, by careful accounting. But for now we’ll look at examples in which all outcomes are equally probable, like those Cardano analyzed.

The potency of Cardano’s rule goes hand in hand with certain subtleties. One lies in the meaning of the term outcomes. As late as the eighteenth century the famous French mathematician Jean Le Rond d’Alembert, author of several works on probability, misused the concept when he analyzed the toss of two coins.13 The number of heads that turns up in those two tosses can be 0, 1, or 2. Since there are three outcomes, Alembert reasoned, the chances of each must be 1 in 3. But Alembert was mistaken.

One of the greatest deficiencies of Cardano’s work was that he made no systematic analysis of the different ways in which a series of events, such as coin tosses, can turn out. As we shall see in the next chapter, no one did that until the following century. Still, a series of two coin tosses is simple enough that Cardano’s methods are easily applied. The key is to realize that the possible outcomes of coin flipping are the data describing how the two coins land, not the total number of heads calculated from that data, as in Alembert’s analysis. In other words, we should not consider 0, 1, or 2 heads as the possible outcomes but rather the sequences (heads, heads), (heads, tails), (tails, heads), and (tails, tails). These are the 4 possibilities that make up the sample space.

The next step, according to Cardano, is to sort through the outcomes, cataloguing the number of heads we can harvest from each. Only 1 of the 4 outcomes—(heads, heads)—yields 2 heads. Similarly, only (tails, tails) yields 0 heads. But if we desire 1 head, then 2 of the outcomes are favorable: (heads, tails) and (tails, heads). And so Cardano’s method shows that Alembert was wrong: the chances are 25 percent for 0 or 2 heads but 50 percent for 1 head. Had Cardano laid his cash on 1 head at 3 to 1, he would have lost only half the time but tripled his money the other half, a great opportunity for a sixteenth-century kid trying to save up money for college—and still a great opportunity today if you can find anyone offering it.

A related problem often taught in elementary probability courses is the two-daughter problem, which is similar to one of the questions I quoted from the「Ask Marilyn」column. Suppose a mother is carrying fraternal twins and wants to know the odds of having two girls, a boy and a girl, and so on. Then the sample space consists of all the possible lists of the sexes of the children in their birth order: (girl, girl), (girl, boy), (boy, girl), and (boy, boy). It is the same as the space for the coin-toss problem except for the way we name the points: heads becomes girl, and tails becomes boy. Mathematicians have a fancy name for the situation in which one problem is another in disguise: they call it an isomorphism. When you find an isomorphism, it often means you’ve saved yourself a lot of work. In this case it means we can figure the chances that both children will be girls in exactly the same way we figured the chances of both tosses coming up heads in the coin-toss problem. And so without even doing the analysis, we know that the answer is the same: 25 percent. We can now answer the question asked in Marilyn’s column: the chance that at least one of the babies will be a girl is the chance that both will be girls plus the chance that just one will be a girl—that is, 25 percent plus 50 percent, which is 75 percent.

In the two-daughter problem, an additional question is usually asked: What are the chances, given that one of the children is a girl, that both children will be girls? One might reason this way: since it is given that one of the children is a girl, there is only one child left to look at. The chance of that child’s being a girl is 50 percent, so the probability that both children are girls is 50 percent.

That is not correct. Why? Although the statement of the problem says that one child is a girl, it doesn’t say which one, and that changes things. If that sounds confusing, that’s okay, because it provides a good illustration of the power of Cardano’s method, which makes the reasoning clear.

The new information—one of the children is a girl—means that we are eliminating from consideration the possibility that both children are boys. And so, employing Cardano’s approach, we eliminate the possible outcome (boy, boy) from the sample space. That leaves only 3 outcomes in the sample space: (girl, boy), (boy, girl), and (girl, girl). Of these, only (girl, girl) is the favorable outcome—that is, both children are daughters—so the chances that both children are girls is 1 in 3, or 33 percent. Now we can see why it matters that the statement of the problem didn’t specify which child was a daughter. For instance, if the problem had asked for the chances of both children being girls given that the first child is a girl, then we would have eliminated both (boy, boy) and (boy, girl) from the sample space and the odds would have been 1 in 2, or 50 percent.

One has to give credit to Marilyn vos Savant, not only for attempting to raise public understanding of elementary probability but also for having the courage to continue to publish such questions even after her frustrating Monty Hall experience. We will end this discussion with another question taken from her column, this one from March 1996:

My dad heard this story on the radio. At Duke University, two students had received A’s in chemistry all semester. But on the night before the final exam, they were partying in another state and didn’t get back to Duke until it was over. Their excuse to the professor was that they had a flat tire, and they asked if they could take a make-up test. The professor agreed, wrote out a test, and sent the two to separate rooms to take it. The first question (on one side of the paper) was worth five points. Then they flipped the paper over and found the second question, worth 95 points:「which tire was it?」What was the probability that both students would say the same thing? My dad and I think it’s 1 in 16. Is that right?14

No, it is not: If the students were lying, the correct probability of their choosing the same answer is 1 in 4 (if you need help to see why, you can look at the notes at the back of this book).15 And now that we’re accustomed to decomposing a problem into lists of possibilities, we are ready to employ the law of the sample space to tackle the Monty Hall problem.

AS I SAID EARLIER, understanding the Monty Hall problem requires no mathematical training. But it does require some careful logical thought, so if you are reading this while watching Simpsons reruns, you might want to postpone one activity or the other. The good news is it goes on for only a few pages.

In the Monty Hall problem you are facing three doors: behind one door is something valuable, say a shiny red Maserati; behind the other two, an item of far less interest, say the complete works of Shakespeare in Serbian. You have chosen door 1. The sample space in this case is this list of three possible outcomes:

Maserati is behind door 1.

Maserati is behind door 2.

Maserati is behind door 3.

Each of these has a probability of 1 in 3. Since the assumption is that most people would prefer the Maserati, the first case is the winning case, and your chances of having guessed right are 1 in 3.

Now according to the problem, the next thing that happens is that the host, who knows what’s behind all the doors, opens one you did not choose, revealing one of the sets of Shakespeare. In opening this door, the host has used what he knows to avoid revealing the Maserati, so this is not a completely random process. There are two cases to consider.

One is the case in which your initial choice was correct. Let’s call that the Lucky Guess scenario. The host will now randomly open door 2 or door 3, and, if you choose to switch, instead of enjoying a fast, sexy ride, you’ll be the owner of Troilus and Cressida in the Torlakian dialect. In the Lucky Guess scenario you are better off not switching—but the probability of landing in the Lucky Guess scenario is only 1 in 3.

The other case we must consider is that in which your initial choice was wrong. We’ll call that the Wrong Guess scenario. The chances you guessed wrong are 2 out of 3, so the Wrong Guess scenario is twice as likely to occur as the Lucky Guess scenario. How does the Wrong Guess scenario differ from the Lucky Guess scenario? In the Wrong Guess scenario the Maserati is behind one of the doors you did not choose, and a copy of the Serbian Shakespeare is behind the other unchosen door. Unlike the Lucky Guess scenario, in this scenario the host does not randomly open an unchosen door. Since he does not want to reveal the Maserati, he chooses to open precisely the door that does not have the Maserati behind it. In other words, in the Wrong Guess scenario the host intervenes in what until now has been a random process. So the process is no longer random: the host uses his knowledge to bias the result, violating randomness by guaranteeing that if you switch your choice, you will get the fancy red car. Because of this intervention, if you find yourself in the Wrong Guess scenario, you will win if you switch and lose if you don’t.

To summarize: if you are in the Lucky Guess scenario (probability 1 in 3), you’ll win if you stick with your choice. If you are in the Wrong Guess scenario (probability 2 in 3), owing to the actions of the host, you will win if you switch your choice. And so your decision comes down to a guess: in which scenario do you find yourself? If you feel that ESP or fate has guided your initial choice, maybe you shouldn’t switch. But unless you can bend silver spoons into pretzels with your brain waves, the odds are 2 to 1 that you are in the Wrong Guess scenario, and so it is better to switch. Statistics from the television program bear this out: those who found themselves in the situation described in the problem and switched their choice won about twice as often as those who did not.

The Monty Hall problem is hard to grasp because unless you think about it carefully, the role of the host, like that of your mother, goes unappreciated. But the host is fixing the game. The host’s role can be made obvious if we suppose that instead of 3 doors, there were 100. You still choose door 1, but now you have a probability of 1 in 100 of being right. Meanwhile the chance of the Maserati’s being behind one of the other doors is 99 in 100. As before, the host opens all but one of the doors that you did not pick, being sure not to open the door hiding the Maserati if it is one of them. After he is done, the chances are still 1 in 100 that the Maserati was behind the door you chose and still 99 in 100 that it was behind one of the other doors. But now, thanks to the intervention of the host, there is only one door left representing all 99 of those other doors, and so the probability that the Maserati is behind that remaining door is 99 out of 100!

Had the Monty Hall problem been around in Cardano’s day, would he have been a Marilyn vos Savant or a Paul Erdös? The law of the sample space handles the problem nicely, but we have no way of knowing for sure, for the earliest known statement of the problem (under a different name) didn’t occur until 1959, in an article by Martin Gardner in Scientific American.16 Gardner called it「a wonderfully confusing little problem」and noted that「in no other branch of mathematics is it so easy for experts to blunder as in probability theory.」Of course, to a mathematician a blunder is an issue of embarrassment, but to a gambler it is an issue of livelihood. And so it is fitting that when it came to the first systematic theory of probability, it took Cardano, the gambler, to figure things out.

ONE DAY while Cardano was in his teens, one of his friends died suddenly. After a few months, Cardano noticed, his friend’s name was no longer mentioned by anyone. This saddened him and left a deep impression. How does one overcome the fact that life is transitory? He decided that the only way was to leave something behind—heirs or lasting works of some kind or both. In his autobiography, Cardano describes developing「an unshakable ambition」to leave his mark on the world.17

After obtaining his medical degree, Cardano returned to Milan, seeking employment. While in college he had written a paper,「On the Differing Opinions of Physicians,」that essentially called the medical establishment a bunch of quacks. The Milan College of Physicians now returned the favor, refusing to admit him. That meant he could not practice in Milan. And so, using money he had saved from his tutoring and gambling, Cardano bought a tiny house to the east, in the town of Piove di Sacco. He expected to do good business there because disease was rife in the town and it had no physician. But his market research had a fatal flaw: the town had no doctor because the populace preferred to be treated by sorcerers and priests. After years of intense work and study, Cardano found himself with little income but a lot of spare time on his hands. It proved a lucky break, for he seized the opportunity and began to write books. One of them was The Book on Games of Chance.

In 1532, after five years in Sacco, Cardano moved back to Milan, hoping to have his work published and once again applying for membership in the College of Physicians. On both fronts he was roundly rejected.「In those days,」he wrote,「I was sickened so to the heart that I would visit diviners and wizards so that some solution might be found to my manifold troubles.」18 One wizard suggested he shield himself from moon rays. Another that, on waking, he sneeze three times and knock on wood. Cardano followed all their prescriptions, but none changed his bad fortune. And so, hooded, he took to sneaking from building to building at night, surreptitiously treating patients who either couldn’t afford the fees of sanctioned doctors or else didn’t improve in their care. To supplement the income he earned from that endeavor, he wrote in his autobiography, he was「forced to the dice again so that I could support my wife; and here my knowledge defeated fortune, and we were able to buy food and live, though our lodgings were desolate.」19 As for The Book on Games of Chance, though he would revise and improve the manuscript repeatedly in the years to come, he never again sought to have it published, perhaps because he realized it wasn’t a good idea to teach anyone to gamble as well as he could.

Cardano eventually achieved his goals in life, obtaining both heirs and fame—and a good deal of fortune to boot. The fortune began to accrue when he published a book based on his old college paper, altering the title from the somewhat academic「On the Differing Opinions of Physicians」to the zinger On the Bad Practice of Medicine in Common Use. The book was a hit. And then, when one of his secret patients, a well-known prior of the Augustinian order of friars, suddenly (and in all likelihood by chance) improved and attributed his recovery to Cardano’s care, Cardano’s fame as a physician took off on an upward spiral that reached such heights the College of Physicians felt compelled not only to grant him membership but also to make him its rector. Meanwhile he was publishing more books, and they did well, especially one for the general public called The Practice of Arithmetic. A few years later he published a more technical book, called the Ars magna, or The Great Art, a treatise on algebra in which he gave the first clear picture of negative numbers and a famous analysis of certain algebraic equations. When he reached his early fifties, in the mid-1550s, Cardano was at his peak, chairman of medicine at the University of Pavia and a wealthy man.

His good fortune didn’t last. To a large extent what brought Cardano down was the other part of his legacy—his children. When she was sixteen, his daughter Chiara (named after his mother) seduced his older son, Giovanni, and become pregnant. She had a successful abortion, but it left her infertile. That suited her just fine, for she was boldly promiscuous, even after her marriage, and contracted syphilis. Giovanni went on to become a doctor but was soon more famous as a petty criminal, so famous he was blackmailed into marriage by a family of gold diggers who had proof that he had murdered, by poison, a minor city official. Meanwhile Aldo, Cardano’s younger son who as a child had engaged in the torture of animals, turned that passion into work as a freelance torturer for the Inquisition. And like Giovanni, he moonlighted as a crook.

A few years after his marriage Giovanni gave one of his servants a mysterious mixture to incorporate into a cake for Giovanni’s wife. When she keeled over after enjoying her dessert, the authorities put two and two together. Despite Gerolamo’s spending a fortune on lawyers, his attempts to pull strings, and his testimony on his son’s behalf, young Giovanni was executed in prison a short while later. The drain on Cardano’s funds and reputation made him vulnerable to his old enemies. The senate in Milan expunged his name from the list of those allowed to lecture, and accusing him of sodomy and incest, had him exiled from the province. When Cardano left Milan at the end of 1563, he wrote in his autobiography, he was「reduced once more to rags, my fortune gone, my income ceased, my rents withheld, my books impounded.」20 By that time his mind was going too, and he was given to periods of incoherence. As the final blow, a self-taught mathematician named Niccolò Tartaglia, angry because in Ars magna Cardano had revealed Tartaglia’s secret method of solving certain equations, coaxed Aldo into giving evidence against his father in exchange for an official appointment as public torturer and executioner for the city of Bologna. Cardano was jailed briefly, then quietly lived out his last few years in Rome. The Book on Games of Chance was finally published in 1663, over 100 years after young Cardano had first put the words to paper. By then his methods of analysis had been reproduced and surpassed.

## Notes

1 Alan Wykes, Doctor Cardano: Physician Extraordinary (London: Frederick Muller, 1969). See also Oystein Ore, Cardano: The Gambling Scholar, with a translation of Cardano’s Book on Games of Chance by Sydney Henry Gould (Princeton, N.J.: Princeton University Press, 1953).

2 Marilyn vos Savant,「Ask Marilyn,」Parade, September 9, 1990.

3 Bruce D. Burns and Mareike Wieth,「Causality and Reasoning: The Monty Hall Dilemma,」in Proceedings of the Twenty-fifth Annual Meeting of the Cognitive Science Society, ed. R. Alterman and D. Kirsh (Hillsdale, N.J.: Lawrence Erlbaum Associates, 2003), p. 198.

4 National Science Board, Science and Engineering Indicators—2002 (Arlington, Va.: National Science Foundation, 2002); http://www.nsf.gov/statistics/seind02/. See vol. 2, chap. 7, table 7-10.

5 Gary P. Posner,「Nation’s Mathematicians Guilty of Innumeracy,」Skeptical Inquirer 15, no. 4 (Summer 1991).

6 Bruce Schechter, My Brain Is Open: The Mathematical Journeys of Paul Erdös (New York: Touchstone, 1998), pp. 107–9.

7 Ibid., pp. 189–90, 196–97.

8 John Tierney,「Behind Monty’s Doors: Puzzle, Debate and Answer?」New York Times, July 21, 1991.

9 Robert S. Gottfried, The Black Death: Natural and Human Disaster in Medieval Europe (New York: Free Press, 1985).

10 Gerolamo Cardano, quoted in Wykes, Doctor Cardano, p. 18.

11 Kline, Mathematical Thought, pp. 184–85, 259–60.

12.「Oprah’s New Shape: How She Got It,」O, the Oprah Magazine, January 2003.

13 Lorraine J. Daston, Classical Probability in the Enlightenment (Princeton, N.J.: Princeton University Press, 1998), p. 97.

14 Marilyn vos Savant,「Ask Marilyn,」Parade, March 3, 1996, p. 14.

15 There are four tires on the car, so, letting RF signify「right front,」and so on, there are 16 possible combinations of responses by the two students. If the first response listed represents that of student 1 and the second that of student 2, the possible joint responses are (RF, RF), (RF, LF), (RF, RR), (RF, LR), (LF, RF), (LF, LF), (LF, RR), (LF, LR), (RR, RF), (RR, LF), (RR, RR), (RR, LR), (LR, RF), (LR, LF), (LR, RR), (LR, LR). Of these 16, 4 are in agreement: (RF, RF), (LF, LF), (RR, RR), (LR, LR). Hence the chances are 4 out of 16, or 1 in 4.

16 Martin Gardner,「Mathematical Games,」Scientific American, October 1959, pp. 180–82.

17 Jerome Cardan, The Book of My Life: De Vita Propia Liber, trans. Jean Stoner (Whitefish, Mont.: Kessinger, 2004), p. 35.

18 Cardano, quoted in Wykes, Doctor Cardano, p. 57.

19 Cardano, quoted ibid.

20 Cardano, quoted ibid., p. 172.

0301寻找穿越可能性空间之路

1576 年之前的几年中，人们常常能看到一名着装古怪的老人，他迈着怪异而不规则的步伐，在罗马的大街上游荡，还不时发出几声既不针对特定听众也根本没人听的喊声。作为著名星相师、宫廷贵族的医师、帕维亚大学医学院主席，这个人曾一度被整个欧洲称颂。他有了许多不朽的发明，其中包括组合锁以及如今用于汽车的万能接头的前身。他发表了 131 篇论文，涉及哲学、医学、数学和科学等广泛领域。但在 1576 年，他不过是一个只有过去没有将来的人，一个生活在阴暗和无望的贫困之中的人。这一年夏末，他坐在桌前，写下了最后的话语 —— 为他那 16 年前仅 26 岁就被处死的长子也是他最钟爱的儿子所写的一首颂诗。老人死于 9 月 20 日，离他 75 岁生日只差几天。他三个孩子中的两个都先他而去，而去世时他那唯一健在的儿子，是一名受雇于宗教裁判所的职业拷问者，而这份优差，正是他提供不利于父亲的证据所得的赏赐。

吉罗拉莫·卡尔达诺死前焚烧了 170 份尚未发表的文稿。清理遗物的人发现其中未被烧毁的 111 份，其中有一份包含 32 个短小章节的论文。论文写成于他去世的数十年前，看来还常常被修改。论文名为《机遇博弈》（ The Book on Games of Chance ），它是历史上第一部关于随机性理论的著作。到卡尔达诺生活的时代为止，人们已经在赌博或处理其他不确定性的问题上实践了数千年：我能在渴死之前穿越这片沙漠吗？当大地像现在这样震动的时候，仍然待在山崖下面是不是很危险？那个喜欢在岩石上画水牛的穴居人女孩对我露齿一笑，是不是表示她喜欢我？但直到卡尔达诺之前，还没有人对赌博或其他不确定过程进行过详尽的分析。卡尔达诺对于随机性作用机制的洞察，形成了被称为样本空间定律的原理。样本空间定律是一种新的思想和新的方法论，并成为后世对不确定性进行数学描述的基础。这个方法十分简单：想想我们是怎样让账簿上的收支保持平衡的？将同样的思路写成随机性理论中定律的形式，这就是样本空间定律。方法虽然简单，却能让我们以系统化的方式解决诸多问题，如果没有这个新方法的帮助，那么这些问题可能会让我们陷入绝望的困惑。为了说明这条定律的应用及其威力，让我们考虑一个描述十分简单的问题。解决这个问题并不需要具有高等数学知识，但它难倒的人，却很可能比随机理论历史上的其他任何问题都多。

作为期刊专栏，《大观》杂志的《玛丽莲答客问》是一个公认的成功专栏。它被刊登在 350 份报纸上，并有着引以为豪的近 3600 万份的发行量，这个始于 1986 年的问答专栏至今仍然充满活力。专栏中的问题本身可能与答案一样富有启发性，而这个专栏也可以被视作一个（不那么科学的）调查美国人脑子里在想些什么东西的盖洛普民意测验。例如下面这些问题：

当股票市场在交易日停盘时，为什么每个人都围成一圈站着，还一边微笑一边鼓掌，而不管今天的股票是涨还是跌？

一位朋友怀了对儿异卵双胞胎。双胞胎中至少有一个是女孩的概率是多少？

当你在路上开车经过一只死黄鼠狼时，为什么过了 10 秒钟你才闻到那股臭味？假设你并没有轧过它。

显然，美国人都很现实。需要注意的是，每个问题都涉及一定的科学或数学知识，这也是许多在该专栏得到答复的问题的一个共同特征。

可能有人 —— 特别是对数学和科学知道那么一点儿的人 —— 会问：「谁是这个当家的玛丽莲？」呃…… 玛丽莲就是玛丽莲·莎凡特，她因为多年来占据着《吉尼斯世界纪录保持者：名人堂》的世界最高智商（228）宝座而声名远扬，也因为她嫁给了罗伯特·贾维克 —— 人造心脏的发明者 —— 而广为人知。但不管名人们的成就如何，他们被人们牢记的原因，有时却是一些他们希望从未发生过的事情（比如「我没有和那个女人发生过性关系」）。玛丽莲的情况也大体如此。最让她出名的，就是她对于下面这个问题的回答，这个问题出现在 1990 年 9 月某个周日的专栏中（我稍微改动了问题中的一些措辞）：

假设有一个游戏，游戏者可以在三扇门中做出选择：有一扇门后是一辆汽车，另两扇门后则是山羊。当游戏者选定某一扇门后，游戏的庄家（他知道各扇门后面是什么东西）将打开另外两扇门之一，门后是一只山羊。然后他问游戏者：「你想不想改变你的选择，选另外那扇没打开的门？」请问，如果游戏者的确改变了选择，这个改变对他是否有利？

这个问题的提出，受到电视游戏节目《让我们做笔交易》（ Let’s Make a Deal ）的启发。该节目播放于 1963 年至 1976 年，1980 年到 1991 年还曾改头换面播出过几次。节目最吸引人的，就是英俊和蔼的主持人蒙提·霍尔，以及他那身材惹火的助手、1957 年加利福尼亚州阿苏萨小姐卡萝尔·梅里尔。

对于节目创始人而言，近 27 个年头、4500 期节目留下的主要遗产，却是上面这个概率问题，这不能不说是一件令人吃惊的事情。玛丽莲的读者们对这个问题的热烈甚至是激烈的回应，让她和《让我们做笔交易》这档节目得以史上留名。毕竟，这个问题看起来挺傻的：还有两扇门可以选择 —— 打开对的那扇，你就赢了；打开另一扇，你就输了。因此，看来不言而喻的事实是，不管你改变或不改变选择，赢的机会总是 50 比 50。还有比这更简单的吗？问题在于，玛丽莲在专栏中说，改变选择的赢面更大。

尽管公众对数学问题向来表现出意料之中的死气沉沉，但这一次，玛丽莲的读者们的反应，就如同她是在鼓吹放弃加利福尼亚州并将其交给墨西哥一样激烈。她对一个如此显而易见的事实的否定，带来了雪崩一样的邮件 —— 她估计，这些信件可能有 1 万封之多。而当我们问美国人植物是否产生了空气中的氧气，或者光是否比声音传播得更快，或者把带放射性的牛奶煮沸是否无法令其变得更安全等问题时，回答「否」的比例都达到两位数（分别为 13%、24% 和 35%）。但在玛丽莲这事儿上，美国人团结起来：92% 的人认为玛丽莲错了。

许多读者看起来非常失望：这样一个他们在各类问题上都如此信任有加的人，怎么会在这样一个简单问题上翻了船呢？她的错误是不是美国人那令人哀叹的无知的象征之一？近 1000 名博士 —— 包括许多数学教授，他们似乎对这个错误特别生气 —— 给玛丽莲写了信。「你错得离谱。」一位乔治梅森大学的数学家写道，

让我来解释一下吧，如果一扇失败的门被打开了，那么这个信息将使剩余两个选择各自的获胜概率变为 1/2，因为两者之中的任何一个都没有理由比另一个更可能获胜。作为一名职业数学家，我对于普通民众在数学技能上的匮乏感到忧心。希望您能够通过承认错误，为这种状况的改变尽一点儿力，并请在今后再细心一些。

从迪金森州立大学寄来的是这么一封信：「在至少三位数学家指出之后，您却依然没有认识到自己的错误，这使我震惊。」来自乔治敦大学的信则说：「到底要多少个愤怒的数学家才能使您改变想法？」美国陆军研究所的某博士如此评论：「如果所有这些博士都错了，这个国家就有大麻烦了。」各种反馈的数量如此之多，且持续时间如此之长，以至在这个问题上投入了颇多的栏目空间之后，玛丽莲决定不再讨论这个问题。

那位陆军研究所的博士说得大概没错：如果所有这些博士都错了，那么将是有大麻烦的信号。但玛丽莲确确实实是对的。20 世纪最杰出的数学家之一的保罗·厄多斯在得知此事后说：「这不可能。」甚至在看了正确答案的正式数学证明之后，他不但不相信，反而发火了。直到一名同事通过计算机仿真将这个游戏重复了数百次，并让厄多斯亲眼看到，改变选择相较于不改变选择，胜负之比为 2∶1，在这之后，厄多斯才勉强承认自己错了。

如此明显的一件事怎么可能错呢？按哈佛大学一位概率统计专业教授的话来说，原因在于「我们大脑的构造天生就不能很好地处理概率问题」。伟大的美国物理学家理查德·费曼曾告诉我说，如果只是将别人的推导看了又看，就永远别想理解任何物理学问题。他说，真正理解一个理论的唯一途径，就是自己去完成它的推导（或者可能最后证明它是错的！）。对于我们这些不是费曼的人而言，重新证明他人的工作，是个让自己丢掉在大学里的饭碗并在家得宝的收银员岗位上实践数学技能的好方法。但蒙提·霍尔问题并不需要任何专业数学知识就能解答。你不需要了解微积分、几何、代数甚至苯丙胺 —— 据称厄多斯就很喜欢使用这种兴奋剂。（传说厄多斯在戒了一个月之后说道：「我以前看着一张白纸时，脑子里满是各种各样的点子；现在我看着一张白纸时，那就真的只是一张白纸。」）你所需要的，不过是对概率的运作方式以及样本空间定律的理解，而样本空间定律正是卡尔达诺在 16 世纪首先著之于文、用于分析随机性的理论框架。

卡尔达诺并不是试图打破 16 世纪欧洲的智识氛围的离经叛道者。对他而言，犬吠意味着爱人的死亡，屋顶上几只乌鸦的嘎嘎叫声则意味着一场严重疾病的到来。他跟其他人一样相信命运、运气，也会根据行星和恒星的排列预测未来。尽管如此，如果他也玩扑克，那么他可不会把运气赌在缺了中间一张牌的顺子上。赌博是卡尔达诺的第二天性，他对赌博的感觉并非源于头脑，而是深入骨髓。因此，他对于各种可能发生的随机结果间数学关系的理解，凌驾于「这种理解根本就注定无用」之类的宿命论调之上。卡尔达诺的工作也超越了当时粗糙的数学，因为在 16 世纪早期，代数乃至算术都还处在石器时代，甚至连等号都还没有被发明出来。

根据卡尔达诺的自传以及同时代人的记述，他值得历史的大书特书。尽管有些文献内容相互矛盾，但有一件事可以肯定：生于 1501 年的卡尔达诺，并不是一个值得在他身上进行投资的孩子。尽管 —— 或者说因为 —— 他的母亲基娅拉已经有 3 个儿子了，她却不喜欢小孩子。又矮又壮、脾气火爆且男女关系混乱的基娅拉怀上卡尔达诺后，就自制了一剂 16 世纪的事后避孕药 —— 由苦艾、烧过的大麦粒和柽柳根酿成的酒。她喝下了这碗药酒，希望能将胎儿打掉。药酒虽然令她恶心无比，未出世的卡尔达诺对之却泰然处之，而且显然他对这碗药在母亲血液中留下的代谢产物十分满意。基娅拉其他的尝试也都以差不多的方式宣告失败了。

基娅拉与卡尔达诺的父亲费吉奥·卡尔达诺并没有结婚，但他们经常表现得有如正式夫妻 —— 他们的高声对骂可是相当出名的。在卡尔达诺出生前一个月，基娅拉离开了米兰的家，搬到南边 20 英里的帕维亚与她妹妹同住。在 3 天痛苦吃力的分娩之后，卡尔达诺终于冒出了头。看到这孩子的第一眼基娅拉肯定以为，她总算摆脱这个臭小子了。他看上去十分虚弱，更糟糕的是，他一不哭二不闹，就那么静静地躺着。产婆预言他活不过出生后的一个小时。但如果基娅拉确实曾梦想过「美好解脱」的话，那么她又得失望了：婴儿的乳母用温酒给他泡了个澡，然后，卡尔达诺复活了。不过他良好的健康状况只维持了几个月，就与乳母和三个同母异父的兄弟在大瘟疫中病倒了。黑死病 —— 这场瘟疫的另一个称呼 —— 实际上是三种不同的疾病：腺鼠疫、肺鼠疫和败血症型鼠疫。卡尔达诺患上的是三者中最常见的腺鼠疫，其典型症状之一就是令人痛苦难当、鸡蛋大小的腹股沟淋巴结肿块，这也是该病名称的由来。一旦出现这样的肿块，患者的期望寿命就只有一周左右。

黑死病最初于 1347 年跟随着从东方返回的一支热那亚舰队，由西西里东北城市墨西拿的一个港口进入欧洲。舰队很快被隔离，所有船员都死在船上 —— 但老鼠活了下来，并一路小跑上了岸，身上还带着病菌以及传播病菌的跳蚤。接下来的瘟疫大暴发在两个月内夺去了该城一半人口的性命，并最终杀死了全欧洲 25-50% 的人口。后继的传染病一波波袭来，这使得欧洲人口在几个世纪中一直无法增长。1501 年可算不上什么好年头，因为当年的意大利也有瘟疫流行。卡尔达诺的乳母和兄弟们都死了，但这个走运的孩子活下来，而且没留下什么后遗症，除了破了相：他的鼻子、额头、脸颊以及下巴上都留下了瘤子。他注定要活将近 75 个年头，他拥有的是一条满是冲突的人生之路和饱受打骂的幼年时光。

卡尔达诺的父亲差不多算是个操作员。就职业上来说，他是位几何学家，而且曾是达·芬奇的密友。几何学家从来就不是个赚钱的职位，费吉奥也的确常为租金发愁，因此他做起了事务咨询的买卖，为豪门望族提供法律与医学方面的建议。费吉奥宣称他是米兰的某位戈弗雷多·卡斯蒂廖尼 —— 更为人所知的称呼则是教皇塞莱斯廷四世 —— 的兄弟的后人。得益于此，咨询买卖终于兴旺起来。卡尔达诺 5 岁时，他父亲领他入了行 —— 姑且这么说吧。实际上，他的父亲在他背上绑了个筐，装上沉甸甸的法律和医学书籍，然后拽着小男孩满城跑去跟主顾见面。卡尔达诺后来写道：「有时，当我们走在街上时，父亲会命令我站住，然后打开一本书，拿我的头当桌子，读上长长的几个段落。如果我因为筐子太重而摇晃，他就用鞋尖踢我，让我不要动来动去。」

1516 年，卡尔达诺下定决心，认为他最好的机遇在医学方面。他宣布要离开米兰的家，去帕维亚学习。费吉奥却希望他能学习法律，以便赚取 100 克朗的年薪。一场大吵之后，费吉奥的气顺了些，但问题没有得到解决：如果没有这笔年薪，卡尔达诺怎样才能维持在帕维亚的生活和学习呢？于是卡尔达诺开始为人占星，教小学生几何、炼金术和天文学，并将所挣的钱积攒起来。就在这时的某一天，他发现自己在赌博方面有天分，而这种天分赚钱的速度，比其他方法要快得多。

在卡尔达诺的时代，对任何一个有赌瘾的人来说，每座城市都是拉斯韦加斯。赌纸牌，赌骰子，赌西洋双陆棋，甚至赌国际象棋，到处都可以下注。卡尔达诺将这些赌博分为两类：一类需要策略或技巧，另一类则完全靠运气。在象棋这一类赌博中，卡尔达诺可能会面临被某个 16 世纪的鲍比·费歇尔击败的风险；但如果只是对那一双小小的立方体下注，他的机会就跟其他人一样多了。其实，在后面这一类赌博中，他比别人更有优势，因为与对手相比，他更了解不同局势下获胜可能的大小。于是，作为进入博弈世界的第一步，他玩起了那些纯靠运气的游戏。不久，他就为自己存下了 1000 克朗的教育基金 —— 这比父亲希望他得到的 10 年年薪还要多。1520 年，他在帕维亚注册成为一名学生，没过多长时间便开始了关于赌博理论的写作。

对于古希腊人和罗马人来说，很多东西都是用古希腊文字记述或表达的，而到了卡尔达诺生活的年代，他再去理解这些东西时，便拥有了额外的优势，因为这时印度人已经在把算术用作一种强有力的工具方面，迈出了最初的一大步。正是在这个时期，以 10 为单位的位值制记数法得到发展，并于公元 700 年前后成为标准方法。印度人还在分数算术上取得了巨大进展，而分数运算对于概率分析至关重要，因为事情发生的可能性总是比 1 小。印度人的这些知识被阿拉伯人采用，最终传入欧洲。最初的运算符号缩写 —— p 表示加法，m 表示减法 —— 于 15 世纪被使用，而 + 和 - 也在同一时期被德国人引入，只不过当时仅用来表示箱子超重或欠重。我们如果注意到当时连等号都还没有，大概就能在一定程度上认识到卡尔达诺所面临的挑战了。等号于 1557 年由工作于牛津大学和剑桥大学的罗伯特·雷科德发明。受到几何学的启发，他认为没有什么东西能比两条平行直线更为相似了，因此，这样的两条平行直线段应当被用来表示相等性。而归功于某位英国国教牧师的乘法符号「×」，则要到 17 世纪才会登上历史舞台。

《机遇博弈》涵盖了纸牌、骰子、西洋双陆棋和距骨等赌博游戏。该书并非尽善尽美，书中所反映的，是卡尔达诺的性格、各种疯狂的念头、狂野的脾气、他做任何事情时怀有的激情，以及他的生命和时代中的动荡不安。在某些问题上，卡尔达诺还犯了错。但《机遇博弈》仍然是概率论这个登陆场上的桥头堡，是人类在探索不确定性本质的过程中取得的首次成功。而卡尔达诺用来解决偶然性问题的方法，因其威力和简单而令人惊讶。

这本书并不是每个章节都在谈论技术问题。如第 26 章的标题是「教得好也能玩得好吗？」（他最后的结论是，「知道一件事和实际去做，似乎完全是两码事」），第 29 章名为「论赌徒的性格」（「有些人的话实在太多了，让自己和别人都丧失了理智」），这些内容看起来更像《亲爱的艾比》而非《玛丽莲答客问》。但同样是在这本书中，卡尔达诺在第 14 章「论点数的组合」（论可能性）里，阐述了「一条普适的规则」，即样本空间定律。

「样本空间」一词的含义，是指一个随机过程中每种可能的结果，都可以被视为某空间中的一点。在简单的情形里，这个空间可能仅包含少量几个点；但在更复杂的情况下，它可能如我们所生活的空间那样，是一个连续统。但卡尔达诺并没有称其为「空间」：将数的集合称为空间的描述方式，还要再等一个世纪，到天才的笛卡儿发明了坐标，并统一了代数与几何之后才会出现。

卡尔达诺的规则用现代语言表述大致如下： 假设一个随机过程有若干等可能性结果，这些结果中有些好（即赢的结果），有些不好（输的结果）。那么，获得一个好结果的概率，就等于所有那些好结果在全体结果中所占的比例。而这个由所有可能结果构成的集合，被称为样本空间 。换言之，如果扔出一个骰子 6 个面中任一面的可能性是均等的，那么这 6 个可能出现的面就形成样本空间，而如果对其中两个面下注，获胜的概率就是 2/6。

我再多说一句，所有结果都以等可能性发生的这种假设，显然并非总是成立。如果我们对奥普拉·温弗瑞成年时的体重进行观测，那么可能观察到的体重所构成的样本空间（曾经）是 145 磅到 237 磅，但在我们的观测期间，并非所有的体重区间出现的可能性都相等。不同的可能结果具有不同的发生概率这一事实，使得问题变得更加复杂。不过我们可以通过细致的计算，为每个可能的结果赋予一个适当的概率，从而解决这一问题。不过让我们先来看几个例子，正如卡尔达诺分析的那些例子一样，在我们的例子中，每种结果的发生都具有等可能性。

卡尔达诺规则的有力之处，与某些细微精妙的方面密不可分，其中之一就是「结果」一词的含义。迟至 18 世纪，多部概率论著作的作者、法国著名数学家达朗贝尔在分析扔两枚硬币的问题时，都还错误地使用了这个概念。扔出两枚硬币，则正面朝上的硬币可能的数目为 0、1 或 2。然后，达朗贝尔推论说，既然有这样 3 种结果，那么每种结果出现的可能性就一定是 1/3。他错了。

卡尔达诺工作的一个最大不足，在于他没有系统地分析事件序列不同的可能发生方式，比如连续多次扔硬币所得的结果。下一章我们将会说明，这个工作要到他过世后的下一个世纪，才有人来完成。不过，扔两次硬币的问题足够简单，我们可以很容易把卡尔达诺的方法用上。这种方法的关键在于我们要认识到，所谓可能结果，应该是描述硬币两次掉落得到的正反面朝上情况的数据，而不是由这些数据计算得到的正面朝上的次数。换句话说，可能结果并不是 0、1 或 2 枚硬币正面朝上，而应该是可能出现的投掷结果序列（正，正）、（正，反）、（反，正）和（反，反）。构成样本空间的，便是这 4 种可能的结果。

按卡尔达诺所说，我们接下来应该列好这些结果，并记录每个结果中正面朝上的硬币数目。在这 4 种可能的结果中，只有（正，正）这一种结果能得到两枚正面朝上的硬币。与此类似，只有（反，反）这一种结果让我们两手空空。但有两种结果能给出有一枚正面朝上的情况：（正，反）和（反，正）。卡尔达诺的方法就在这里指出了达朗贝尔的错误之处：出现 0 枚或 2 枚硬币正面朝上的机会各为 25%，但出现 1 枚硬币正面朝上的机会为 50%。如果卡尔达诺以 3 赔 1 的赔率把赌注押在出现一次正面朝上的结果上，那么在一半的赌局中，他会输掉赌注，但在另一半的赌局中，却会赚到 3 倍于赌本的钱。对于一个正在为读大学而积攒学费的 16 世纪的小男孩来说，这个好机会可是了不得的 —— 哪怕在今天，如果找得到愿意出这个赔率的人，那么这也是个了不得的好机会。

一个经常出现在初等概率课程中的相关问题，就是所谓「两女儿问题」。它与我从《玛丽莲答客问》专栏引用的一个问题颇为相似。假设有位母亲怀上了一对儿双胞胎，现在她想知道两个都是女儿或一个儿子一个女儿等这些情况的概率。这个问题的样本空间，由两个孩子按出生先后顺序排列所得的性别列表构成：（女孩，女孩）、（女孩，男孩）、（男孩，女孩）以及（男孩，男孩）。这个样本空间与前面那个扔硬币问题的样本空间其实是一回事，只不过空间中点的命名方式有所不同：「正」变成了「女孩」，而「反」变成了「男孩」。数学家给这种不过是将某个问题换了个说法，变成另一个问题的情况起了个怪名字：同构性。两个问题同构常常意味着我们可以省去很多麻烦。在现在的例子中，同构性意味着两个孩子都是女孩的可能性，等于两枚硬币都是正面朝上的可能性。由此，我们甚至不需要进行任何分析，就能知道问题的答案是一样的：25%。现在，我们就能回答玛丽莲专栏里的那个问题了：两个孩子中至少有一个女孩的可能性，等于两个都是女孩的可能性，再加上两个孩子中仅有一个是女孩的可能性，也就是 25% 加 50% 等于 75%。

在两女儿问题中，常被进一步问及的是：如果两个孩子中有一个是女孩，那么两个孩子都是女孩的可能性是多少？大家可能会推理如下：既然已知一个孩子是女孩，那么只考虑剩下那个孩子的性别即可，而这个孩子是女孩的可能性是 50%，所以两个都是女孩的可能性，也就是 50%。

这个回答并不正确。为什么呢？尽管问题的描述中说有一个孩子是女孩，却并没有说是哪一个。这样一来，情况就有变化了。如果你对此感到糊涂，也请不用担心，这是很正常的，因为这个问题恰恰能展现卡尔达诺方法的威力 —— 它使得推理过程清晰而明了。

两个孩子中有一个是女孩的新信息，意味着我们可以把两个都是男孩的可能，从需要考虑的情况中去掉。因此，在运用卡尔达诺的方法时，我们将（男孩，男孩）这个结果从样本空间中剔除，而新的样本空间就只剩下三种结果：（女孩，男孩）、（男孩，女孩）和（女孩，女孩）。其中只有（女孩，女孩）（即两个孩子都是女儿）这个结果是我们所希望的，因此，两个都是女孩的可能性是 1/3，即 33%。下面我们来看看，不具体指明哪个孩子是女孩这一点，为什么是一个十分重要的因素？如果问题问的是：当第一个孩子是女孩时 ，两个都是女孩的可能性是多少，那么我们应该从样本空间中把（男孩，男孩）和（男孩，女孩）这两个可能都去掉，而所得的概率就是 1/2，即 50%。

我们应当信任玛丽莲，因为她不仅试图提高公众对于基本概率知识的理解，而且勇于继续发表相关的问题，哪怕是在经历了令人沮丧的蒙提·霍尔问题之后仍然如此。作为讨论的结束，我们再来看看她专栏中的另一个刊登于 1996 年 3 月的问题。

下面这个故事是我爸爸在广播里听到的。有两名杜克大学的学生，在整个学期里他们化学测验的成绩都是 A。但在期终考的头天晚上，他们跑到另一个州去参加派对，等返回学校时，考试已经结束。他们向教授解释说车胎没气了，并希望能补考。教授同意了。他出了一份卷子，然后将两人分别安排在两个教室里考试。第一道题（在试卷的一面上）是 5 分，而翻到另一面，则是 95 分的第二题：「哪个车胎没气了？」请问两名学生给出相同答案的可能性是多少？我爸爸和我都觉得是 1/16，对吗？

不，这个答案不对：如果两名学生在撒谎，那么他们碰巧选中相同答案的可能性正确值为 1/4（如果你需要一点儿帮助才能找到原因，那么请看本书后面的注释）。好了，现在我们已经熟悉了将问题分解为一系列可能情况的做法，接下来我们就可以运用样本空间定律来解决蒙提·霍尔问题了。

正如我们之前所说，要理解蒙提·霍尔问题，并不需要什么数学方面的专业训练，但的确需要一点儿细致的逻辑思维。因此，如果你在一边看《辛普森一家》的重播，一边读我们现在这段话，那么最好把其中一件稍微推后一些。不过有个好消息是，要理解我们的问题，只要几页纸就够了。

在蒙提·霍尔问题中，你面对着 3 扇门：其中一扇的后面是个值钱的物件，比如一辆崭新锃亮的红色玛莎拉蒂；而在另两扇门的后面，则是让人兴味索然的什么玩意儿，比如塞尔维亚语的《莎士比亚全集》。假设你选择了 1 号门。这时，样本空间由以下的 3 个可能结果构成：

玛莎拉蒂在 1 号门后。

玛莎拉蒂在 2 号门后。

玛莎拉蒂在 3 号门后。

每种可能的发生概率都是 1/3。我们假定大多数人都对玛莎拉蒂更感兴趣，因此第一种是获胜的结果，而你猜对的可能性为 1/3。

根据问题所说，接下来发生的，就是庄家 —— 他知道每扇门后面是什么东西 —— 打开了那两扇未被选中的门之一，门后是那两套《莎士比亚全集》中的一套。在打开这扇门时，庄家实际上已经根据他掌握的信息，避免打开停着玛莎拉蒂的那扇门。因此，这一行动并不是完全随机的过程。现在考虑两种情况。

第一种情况，你一开始就选对了。我们称这种情况为「走大运」。这时，庄家将随机打开 2 号门或 3 号门，而如果你在庄家开门后改变选择，那么你会成为托拉克（Torlakian）方言版《特洛伊罗斯与克瑞西达》的主人，而不是爽爽地飙一次车。在「走大运」的情况下，不更换选择的结局更好 —— 但「走大运」发生的概率只有 1/3。

另一种情况是你开始时选错了，我们称为「撞霉运」。你开始时选错的可能性是 2/3，因此，「撞霉运」的机会要比「走大运」的机会大上一倍。「撞霉运」与「走大运」相比有何不同呢？在「撞霉运」中，那辆玛莎拉蒂就藏在你没有选的那两扇门之一的后面，而另外一扇的后面则是塞尔维亚语的《莎士比亚全集》。与「走大运」不同，在「撞霉运」的情况下，庄家并非随机地打开一扇你没有选中的门。既然他不想让玛莎拉蒂暴露，所以他有选择性地打开正好没有玛莎拉蒂的那扇门。换句话说，在「撞霉运」中，庄家介入了迄今为止还是随机的游戏过程，而他的介入使得过程不再随机：庄家利用他所掌握的知识，使结果偏离了真正随机的结果，他确保你如果改变选择，就一定能得到那辆迷人的红色轿车，从而打破了游戏的随机性。正是由于庄家的介入，如果你知道自己「撞霉运」了，改变先前的选择就能获胜，否则就输了。

总而言之，如果开始时「走大运」（可能性为 1/3），那么不改变选择能获胜；如果开始时「撞霉运」（可能性为 2/3），那么由于庄家的举动，你可以通过改变选择获胜。因此，最后决策的关键在于如下的猜测：你开始时到底是碰到了哪种情况？如果你觉得是你的第六感或命运的指引让你做出最初的选择，或许就不该更改选择。但除非你能用脑电波把一把银勺子弯成椒盐卷饼，那么「撞霉运」和「走大运」两者的概率之比为 2 比 1，因此你最好还是改变主意，更换你的选择。电视节目的统计数据证实了这一论断：相较于不改变选择的人，那些改变选择的人获胜的次数差不多是前者的两倍。

要理解蒙提·霍尔问题很困难，因为不仔细思考的话，庄家所扮演的角色很容易被忽视，就如同你忽视母亲所做的一切那样。但庄家实际上将这个游戏修整得对游戏者更有利。为了使庄家扮演的角色更明显，我们假设现在游戏中不是 3 扇门，而是 100 扇门。你仍然选择其中一扇，但现在选对的可能性就只有 1/100，而玛莎拉蒂藏在剩下的某扇门后面的可能性是 99/100。跟之前一样，庄家将剩下的 99 扇门中的 98 扇都打开，并确保这些门后都不是玛莎拉蒂。现在，你就该感谢庄家的介入了，因为之前未被选中的 99 扇门，现在只剩下硕果仅存的一个代表，而玛莎拉蒂藏在这扇门后的可能性是 99/100！

如果蒙提·霍尔问题出现在卡尔达诺的时代，他会是玛丽莲还是厄多斯？样本空间定律很漂亮地解决了这个问题，我们却无法确知卡尔达诺到底会成为哪一个，因为该问题最早的（不同名字的）表述，出现在 1959 年马丁·加德纳发表在《科学美国人》杂志的一篇文章中。加德纳称它为「一个能把人搞糊涂的极好的小问题」，并指出「相较于数学领域中其他任何一个分支，概率理论最容易让专家犯下大错」。当然，对数学家而言，犯下这个错误是件很没面子的事情，不过对赌徒而言，这可不仅仅是面子的问题，而且是生计的问题。因此，由赌徒卡尔达诺搞出首个系统性的概率理论，倒是再合适不过了。

在卡尔达诺十来岁的时候，他的一位朋友在某天突然死去。几个月后，卡尔达诺注意到已经不再有人提起这位朋友的姓名。这件事令他很悲伤，也给他留下深刻的印象。生命不过是过眼云烟，谁能改变这个事实呢？在他看来，要改变这一点，就必须在身后留下些什么东西 —— 要么是继承人，要么是不朽的成就，或者两样都有。在自传中，卡尔达诺写下了他希望在世上留下印迹的「不可动摇的野心」。

获得医学学位后，卡尔达诺回到米兰找工作。他在大学时写了一篇《论医生之互不相同的观点》，在文中，他斩钉截铁地把当时的医学称为一堆骗人的东西。米兰医学院在他找工作时还了这份情：他们拒绝承认他的医学学历。这意味着他无法在米兰行医。因此，卡尔达诺用他剩下的靠教书和赌博攒下的积蓄，在米兰东边萨科河畔皮奥韦买了间小屋。当时镇上疾病肆虐，却没有医生，因此，他满心期望在那里做笔好买卖。不过他这次的市场调研有一个致命的缺陷：镇上之所以没有医生，是因为人们更愿意找巫师或牧师来治病。几年勤奋的工作学习下来，卡尔达诺发现他的收入几乎为零，而空闲时间倒是颇多。后来的事实证明，这段时间对他而言是一个幸运的休整期，因为他抓住这个机会开始著书立说，其中之一就是《机遇博弈》。

在萨科河畔待了 5 年后，卡尔达诺于 1532 年搬回米兰，希望在那里把书出版，并再次申请加入米兰医学院。又一次，他在这两条战线上遭遇了彻底的失败。「在那些日子里，」他写道，「我感到如此疲惫，甚至都会去找那些算卦和玩弄巫术的家伙，希望能为接二连三的麻烦找到一个解决之法。」一个巫师建议他把月光挡在屋外，另一个则建议他在起床时打三个喷嚏并敲打木头。卡尔达诺遵照了所有建议，但没有一种方法能改变他的霉运。因此他只好戴上头巾，半夜里鬼鬼祟祟地从一幢房子跑到另一幢房子，秘密医治那些负担不起执业医生的诊疗费，或者在他们的治疗下不见好转的病人。他在自传中还写道，为了弄一点儿额外的钱贴补这样辛苦得来的收入，他「被迫再次拿起骰子，以求养活我的妻子。在骰子上，我的知识战胜了运气，而我们也才能够买得起食物，继续生活，尽管我们租住的地方仍是家徒四壁」。至于《机遇博弈》，他在后来的岁月中不断进行审校修改，却再也没有尝试将它出版。这或许是因为他认识到，把每个人都教得跟自己一样善于赌博，可不是什么好主意。

卡尔达诺终于达成了他的人生目标：他有了继承人，也有了名声 —— 当然还有大笔的财富。他将大学时的论文《论医生之互不相同的观点》改头换面，把原来那个带着一股子学究气的标题，换成了铿锵有力的《论普通用药中的不良做法》，并成书出版。该书畅销一时，他的财富随之慢慢增长。后来，他的那些秘密病人之一，某知名奥古斯丁修会会长，病情突然（而且从各种可能性来看，都应该是碰巧）好转了。病人将痊愈的功劳都归于卡尔达诺的照料，卡尔达诺作为一名医生的名声因此扶摇直上，一飞冲天，以至米兰医学院不得不授予他学院成员的职位，并任命他为院长。与此同时，他出版了更多图书，销量都还不错，特别是为普通大众所写的《算术练习》（ The Practice of Arithmetic ）一书。数年后，他出版了一本技术性更强的书《大术》。这是一部代数论著，它首次清晰地描述了负数，并对若干代数方程进行了分析。在他 50 岁出头，即 16 世纪 50 年代中期时，卡尔达诺达到人生的巅峰，成为帕维亚大学医学院的教授，也成了一个有钱人。

不过他的好运没能持续多久。很大程度上，使卡尔达诺走下坡路的，正是他遗产的另一半 —— 他的孩子们。女儿基娅拉（以他母亲的名字命名）在 16 岁那年勾引了大儿子吉奥瓦尼并怀了孕。尽管成功流产，但她丧失了生育能力。对她来说，这倒没什么不好，因为她在私生活方面实在大胆，甚至在婚后也是如此。最终她感染了梅毒。吉奥瓦尼后来也当了医生，但很快就作为一名卑鄙的罪犯更加出名了。吉奥瓦尼因此不得不近似于被强迫地与一个采金者家庭联姻，因为这家人掌握了他用毒药谋害一名低级市政官员的证据。与此同时，从小就热衷于虐待动物的卡尔达诺的小儿子阿尔多，将这种热情倾注到一份差使上 —— 他成为一名自由职业者式的宗教裁判所拷问者。而且与吉奥瓦尼一样，他还是名兼职骗子。

结婚几年后的一天，吉奥瓦尼把一瓶神秘的混合物交给他的一名佣人，要他把这瓶东西混进给妻子做的蛋糕中。他妻子享用完这份甜点就倒下了。尽管卡尔达诺花了一大笔钱聘请律师，想方设法走后门，还为儿子提供了有利的证言，但当局把各种证据联系起来，仍然在不久之后将年轻的吉奥瓦尼在狱中处决了。耗尽了金钱与名誉的卡尔达诺在老对头的手下变得不堪一击。米兰元老院将他从演讲者名单中抹去，指责他犯下了鸡奸与乱伦的罪行，并将他逐出这个省份。当卡尔达诺在 1563 年年末离开米兰时 —— 他在自传中写道 —— 他「再次成为一个穷光蛋，财富消失了，收入没有了，租金被扣了，书也被没收了」。他的意识也在这时开始消失，对他而言，生活成了不连贯的片段。一个名叫尼科洛·塔尔塔利亚的自学成才的数学家给了他最后一击，因为他对卡尔达诺在《大术》一书中公开了他的某些解方程的绝招怒不可遏。他哄着阿尔多提供了不利于其父亲的证据，而作为交换，阿尔多得到了博洛尼亚城公共拷问者与行刑人的官方委任。卡尔达诺被短暂地关押了一段时间，然后静悄悄地在罗马度过了人生的最后几年。《机遇博弈》最终于 1663 年得以出版，此时距年轻的卡尔达诺在纸上写下这些文字已经过去了 100 多年，而且其他人已经重新发现并超越了他的分析方法。