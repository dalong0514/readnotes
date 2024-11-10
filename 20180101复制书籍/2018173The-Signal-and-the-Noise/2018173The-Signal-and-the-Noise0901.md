Nate Silver.(2012).2018173The-Signal-and-the-Noise.Penguin Group =>  0901Rage Against the Machines

## 0901Rage Against the Machines

The twenty-seven-year-old Edgar Allan Poe, like many others before him, was fascinated by the Mechanical Turk, a contraption that had once beaten Napoleon Bonaparte and Benjamin Franklin at chess. The machine, constructed in Hungary in 1770 before Poe or the United States of America were born, had come to tour Baltimore and Richmond in the 1830s after having wowed audiences around Europe for decades. Poe deduced that it was an elaborate hoax, its cogs and gears concealing a chess master who sat in its cupboards and manipulated its levers to move the pieces about the board and nod its turban-covered head every time that it put its opponent into check.

Poe is regarded as the inventor of the detective story,1 and some of his work in sleuthing the hoax was uncanny. He was rightly suspicious, for instance, that a man (later determined to be the German chess master William Schlumberger) could always be found packing and unpacking the machine but was nowhere to be seen while the game was being played (aha! he was in the box). What was truly visionary about Poe's essay on the Mechanical Turk, however, was his grasp of its implications for what we now call artificial intelligence (a term that would not be coined until 120 years later). His essay expressed a very deep and very modern ambivalence about the prospect that computers might be able to imitate, or improve on, the higher functions of man.

FIGURE 9-1: THE MECHANICAL TURK

Poe recognized just how impressive it might be for a machine to play chess at all. The first mechanical computer, what Charles Babbage called the difference engine, had barely been conceived of at the time that Poe wrote his exposé. Babbage's proposed computer, which was never fully built during his lifetime, might at best hope to approximate some elementary functions like logarithms in addition to carrying out addition, subtraction, multiplication, and division. Poe thought of Babbage's work as impressive enough—but still, all it did was take predictable inputs, turn a few gears, and spit out predictable outputs. There was no intelligence there—it was purely mechanistic. A computer that could play chess, on the other hand, verged on being miraculous because of the judgment required to play the game well.

Poe claimed that if this chess-playing machine were real, it must by definition play chess flawlessly; machines do not make computational errors. He took the fact that the Turk did not play perfect chess—it won most of its games but lost a few—as further proof that it was not a machine but a human-controlled apparatus, full of human imperfections.

Although Poe's logic was flawed, this reverence for machines is still with us today. We regard computers as astonishing inventions, among the foremost expressions of human ingenuity. Bill Gates often polls as among the most admired men in America,2 and Apple and Google among our most admired companies.3 And we expect computers to behave flawlessly and effortlessly, somehow overcoming the imperfections of their creators.

Moreover, we view the calculations of computer programs as unimpeachably precise and perhaps even prophetic. In 2012, a pair of British teenagers were accused of defrauding investors out of more than a million dollars by promoting their stock-picking "robot" named MARL,4 which they claimed could process "1,986,832 mathematical calculations per second" while avoiding "human ‘gut feelings,'" allowing investors to double their money every few hours by following MARL's recommendations for penny stocks.5

Even when computer predictions do not inspire our credulity, they can spark our fears; computers that run programs to forecast the chance of survival for hospital patients, for instance, are sometimes written about in news accounts6 as though they are cousins of the HAL 9000, the computer from 2001: A Space Odyssey, which decided it had no more use for the astronauts and tried to suffocate them.

As we enter the era of Big Data, with information and processing power increasing at exponential rates, it may be time to develop a healthier attitude toward computers and what they might accomplish for us. Technology is beneficial as a labor-saving device, but we should not expect machines to do our thinking for us.

The Birth of the Chess Computer

The Spanish engineer Leonardo Torres y Quevedo built a version of the Mechanical Turk in 1912, which he called El Ajedrecista (the chess player). Although El Ajedrecista is sometimes regarded as the first computer game,7 it was extremely limited in its functionality, restricted to determining positions in an endgame in which there are just three pieces left on the board. (El Ajedrecista also did not have any stereotypical Turkish headgear.)

The father of the modern chess computer was MIT's Claude Shannon, a mathematician regarded as the founder of information theory, who in 1950 published a paper called "Programming a Computer for Playing Chess."8 Shannon identified some of the algorithms and techniques that form the backbone of chess programs today. He also recognized why chess is such an interesting problem for testing the powers of information-processing machines.

Chess, Shannon realized, has an exceptionally clear and distinct goal—achieving checkmate. Moreover, it follows a relatively simple set of rules and has no element of chance or randomness. And yet, as anybody who has played chess has realized (I am not such a good player myself), using those simple rules to achieve that simple goal is not at all easy. It requires deep concentration to survive more than a couple of dozen moves into a chess game, let alone to actually win one. Shannon saw chess as a litmus test for the power of computers and the sort of abilities they might someday possess.

But Shannon, in contrast to some who came after him, did not hold the romanticized notion that computers might play chess in the same way that humans do. Nor did he see their victory over humans at chess as being inevitable. Instead, he saw four potential advantages for computers:

They are very fast at making calculations.

They won't make errors, unless the errors are encoded in the program.

They won't get lazy and fail to fully analyze a position or all the possible moves.

They won't play emotionally and become overconfident in an apparent winning position that might be squandered or grow despondent in a difficult one that might be salvaged.

These were to be weighed, Shannon thought, against four distinctly human advantages:

Our minds are flexible, able to shift gears to solve a problem rather than follow a set of code.

We have the capacity for imagination.

We have the ability to reason.

We have the ability to learn.

It seemed like a fair fight to Shannon. But that was only the case for a few fleeting moments in the mid-1990s, when the Russian grandmaster Garry Kasparov—the best chess player of all time—went up against what was then one of the most advanced computers ever built, IBM's Deep Blue.

Before their match, humans were winning the fight—it wasn't even close. Yet computers have prevailed ever since, and will continue to do so for as long as we live.

Chess, Prediction, and Heuristics

In accordance with Bayes's theorem, prediction is fundamentally a type of information-processing activity—a matter of using new data to test our hypotheses about the objective world, with the goal of coming to truer and more accurate conceptions about it.

Chess might be thought of as analogous to prediction. The players must process information—the position of the thirty-two pieces on the board and their possible moves. They use this information to devise strategies to place their opponent in checkmate. These strategies in essence represent different hypotheses about how to win the game. Whoever succeeds in that task had the better hypothesis.

Chess is deterministic—there is no real element of luck involved. But the same is theoretically true of the weather, as we saw in chapter 4. Our knowledge of both systems is subject to considerable imperfections. In weather, much of the problem is that our knowledge of the initial conditions is incomplete. Even though we have a very good idea of the rules by which the weather system behaves, we have incomplete information about the position of all the molecules that form clouds and rainstorms and hurricanes. Hence, the best we can do is to make probabilistic forecasts.

In chess, we have both complete knowledge of the governing rules and perfect information—there are a finite number of chess pieces, and they're right there in plain sight. But the game is still very difficult for us. Chess speaks to the constraints on our information-processing capabilities—and it might tell us something about the best strategies for making decisions despite them. The need for prediction arises not necessarily because the world itself is uncertain, but because understanding it fully is beyond our capacity.9

Both computer programs and human chess masters therefore rely on making simplifications to forecast the outcome of the game. We can think of these simplifications as "models," but heuristics is the preferred term in the study of computer programming and human decision making. It comes from the same Greek root word from which we derive eureka.10 A heuristic approach to problem solving consists of employing rules of thumb when a deterministic solution to a problem is beyond our practical capacities.

Heuristics are very useful things, but they necessarily produce biases and blind spots.11 For instance, the heuristic "When you encounter a dangerous animal, run away!" is often a useful guide but not when you meet a grizzly bear; she may be startled by your sudden movement and she can easily outrun you. (Instead, the National Park Service advises you to remain as quiet and as still as possible when you encounter a grizzly bear and even to play dead if necessary.12) Humans and computers apply different heuristics when they play chess. When they play against each other, the game usually comes down to who can find his opponent's blind spots first.

Kasparov's Failed Prediction

In January 1988, Garry Kasparov, the top-rated chess player in the world from 1986 until his retirement in 2005,13 predicted that no computer program would be able to defeat a human grandmaster at chess until at least the year 2000.14 "If any grandmaster has difficulties playing computers," he quipped at a press conference in Paris, "I would be happy to provide my advice."15 Later that same year, however, the Danish grandmaster Bent Larsen was defeated by a program named Deep Thought, a graduate-school project by several students at Carnegie Mellon University.

The garden-variety grandmaster, however, was no Kasparov, and when Deep Thought squared off against Kasparov in 1989 it was resoundingly defeated. Kasparov has always respected the role of computing technology in chess, and had long studied with computers to improve his game, but he offered Deep Thought only the faintest praise, suggesting that one day a computer could come along that might require him to exert his "100 percent capabilities" in order to defeat it.16

The programmers behind Deep Thought, led by Feng-hsiung Hsu and Murray Campbell, were eventually hired by IBM, where their system evolved into Deep Blue. Deep Blue did defeat Kasparov in the first game of a match in Philadelphia in 1996, but Kasparov rebounded to claim the rest of the series fairly easily. It was the next year, in a rematch in New York, when the unthinkable happened. Garry Kasparov, the best and most intimidating chess player in history, was intimidated by a computer.

In the Beginning . . .

A chess game, like everything else, has three parts: the beginning, the middle and the end. What's a little different about chess is that each of these phases tests different intellectual and emotional skills, making the game a mental triathlon of speed, strength, and stamina.

In the beginning of a chess game the center of the board is void, with pawns, rooks, and bishops neatly aligned in the first two rows awaiting instructions from their masters. The possibilities are almost infinite. White can open the game in any of twenty different ways, and black can respond with twenty of its own moves, creating 4,000 possible sequences after the first full turn. After the second full turn, there are 71,852 possibilities; after the third, there are 9,132,484. The number of possibilities in an entire chess game, played to completion, is so large that it is a significant problem even to estimate it, but some mathematicians put the number as high as . These are astronomical numbers: as Diego Rasskin-Gutman has written, "There are more possible chess games than the number of atoms in the universe."17

It might seem that at the beginning of the game, when all the pieces are still on the board and the number of possibilities is most limitless, computers are at their greatest strength. As IBM's Web site bragged before the match against Kasparov, their computer could calculate 200 million positions per second. "Incidentally, Garry Kasparov can evaluate approximately three positions per second," it noted snidely.18 How did Kasparov have a chance?

But chess computers had long been rather poor at the opening phase of the game. Although the number of possibilities was the most limitless, the objectives were also the least clear. When there are branches on the tree, calculating 3 moves per second or 200 million is about equally fruitless unless you are harnessing that power in a directed way.

Both computer and human players need to break a chess game down into intermediate goals: for instance, capturing an opponent's pawn or putting their king into check. In the middle of the match, once the pieces are locked in combat and threaten one another, there are many such strategic objectives available. It is a matter of devising tactics to accomplish them, and forecasting which might have the most beneficial effects on the remainder of the game. The goals of the opening moves, however, are more abstract. Computers struggle with abstract and open-ended problems, whereas humans understand heuristics like "control the center of the board" and "keep your pawns organized" and can devise any number of creative ways to achieve them.

Moreover, because the opening moves are more routine to players than positions they may encounter later on, humans can rely on centuries' worth of experience to pick the best moves. Although there are theoretically twenty moves that white might play to open the game, more than 98 percent of competitive chess games begin with one of the best four.19

The problem for humans is that computer programs can systematize this knowledge by studying statistics. Chess databases contain the results of literally hundreds of thousands of games and like any other database can be mined for predictive insight. IBM's programmers studied things like how often each sequence of opening moves had been played and how strong the players were who played them, as well as how often each series of moves resulted in wins, losses, and draws for their respective sides.20 The computer's heuristics for analyzing these statistics could potentially put it on a level playing field with human intuition and experience, if not well ahead of it. "Kasparov isn't playing a computer, he's playing the ghosts of grandmasters past," IBM's Web site said in reference to Deep Blue's deep databases.21

Kasparov's goal, therefore, in his first game of his six-game match against Deep Blue in 1997, was to take the program out of database-land and make it fly blind again. The opening move he played was fairly common; he moved his knight to the square of the board that players know as f3. Deep Blue responded on its second move by advancing its bishop to threaten Kasparov's knight—undoubtedly because its databases showed that such a move had historically reduced white's winning percentage* from 56 percent to 51 percent.

Those databases relied on the assumption, however, that Kasparov would respond as almost all other players had when faced with the position,22 by moving his knight back out of the way. Instead, he ignored the threat, figuring that Deep Blue was bluffing,23 and chose instead to move one of his pawns to pave the way for his bishop to control the center of the board.

Kasparov's move, while sound strategically, also accomplished another objective. He had made just three moves and Deep Blue had made just two, and yet the position they had now achieved (illustrated in figure 9-2) had literally occurred just once before in master-level competition24 out of the hundreds of thousands of games in Deep Blue's database.

Even when very common chess moves are played, there are so many possible branches on the tree that databases are useless after perhaps ten or fifteen moves. In any long game of chess, it is quite likely that you and your opponent will eventually reach some positions that literally no two players in the history of humanity have encountered before. But Kasparov had taken the database out after just three moves. As we have learned throughout this book, purely statistical approaches toward forecasting are ineffective at best when there is not a sufficient sample of data to work with.

Deep Blue would need to "think" for itself.

FIGURE 9-2: POSITION AFTER KASPAROV'S 3RD MOVE IN GAME 1

The Chess Player's Dilemma: Breadth Versus Depth

The middle of a chess game (simply called the midgame) potentially favors the strengths of the computer. With the pieces free to move in the center of the board, there are an average of around forty possible moves rather than twenty for every turn.25 That might not seem like a huge difference, but because the tree of possibilities explodes exponentially, it quickly adds up. Suppose, for instance, that you want to calculate just three full turns ahead (that is, three moves each for you and your opponent, or six total). At the beginning of the game, this function is approximated by the number twenty taken to the sixth power, which is sixty-four million positions, already a gargantuan number. In the midgame, however, you have to calculate forty to the sixth power, or 4.1 billion possibilities. Deep Blue could calculate all those positions in just twenty seconds. Kasparov would require literally forty-three years to do so, even without pausing to eat, sleep, or go to the bathroom.

Great players like Kasparov do not delude themselves into thinking they can calculate all these possibilities. This is what separates elite players from amateurs. In his famous study of chess players, the Dutch psychologist Adriaan de Groot found that amateur players, when presented with a chess problem, often frustrated themselves by looking for the perfect move, rendering themselves incapable of making any move at all.26

Chess masters, by contrast, are looking for a good move—and certainly if at all possible the best move in a given position—but they are more forecasting how the move might favorably dispose their position than trying to enumerate every possibility. It is "pure fantasy," the American grandmaster Reuben Fine wrote,27 to assume that human chess players have calculated every position to completion twenty or thirty moves in advance.

It is not quite as simple as saying that "the perfect is the enemy of the good." If you want to really master a game like chess, you may need to get beyond such simple heuristics. Nevertheless, we are not capable of making perfect decisions when presented with more information than we can process in a limited amount of time. Acknowledging those imperfections may free us to make the best decisions that we can in chess and in other contexts that involve forecasting.

This is not to say that grandmasters like Kasparov don't have any calculations to perform. At the very least, Kasparov might need to devise a tactic, a precise sequence of perhaps three to five moves, to capture an opponent's piece or accomplish some other near-term objective. For each of those moves, he will need to think about how his opponent might respond—all the possible variations in the play—and whether any of them could nullify his tactic. He will also need to consider whether the opponent has laid any traps for him; a strong-looking position can be turned into a checkmate in just a few moves if a player's king is not protected.

Chess players learn through memory and experience where to concentrate their thinking. Sometimes this involves probing many branches of the tree but just a couple of moves down the line; at other times, they focus on just one branch but carry out the calculation to a much greater depth. This type of trade-off between breadth and depth is common anytime that we face a complicated problem. The Defense Department and the CIA, for instance, must decide whether to follow up on a broader array of signals in predicting and preventing potential terrorist attacks, or instead to focus on those consistent with what they view as the most likely threats. Elite chess players tend to be good at metacognition—thinking about the way they think—and correcting themselves if they don't seem to be striking the right balance.

Strategy Versus Tactics

Computer chess machines, to some extent, get to have it both ways. They use heuristics to prune their search trees, focusing more of their processing power on more promising branches rather than calculating every one to the same degree of depth. But because they are so much faster at calculation, they don't have to compromise as much, evaluating all the possibilities a little bit and the most important-seeming ones in greater detail.

But computer chess programs can't always see the bigger picture and think strategically. They are very good at calculating the tactics to achieve some near-term objective but not very strong at determining which of these objectives are most important in the grander scheme of the game.

Kasparov tried to exploit the blind spots in Deep Blue's heuristics by baiting it into mindlessly pursuing plans that did not improve its strategic position. Computer chess programs often prefer short-term objectives that can be broken down and quantized and that don't require them to evaluate the chessboard as a holistic organism. A classic example of the computer's biases is its willingness to accept sacrifices; it is often very agreeable when a strong player offers to trade a better piece for a weaker one.

The heuristic "Accept a trade when your opponent gives up the more powerful piece" is usually a good one—but not necessarily when you are up against a player like Kasparov and he is willing to take the seemingly weaker side of the deal; he knows the tactical loss is outweighed by strategic gain. Kasparov offered Deep Blue such a trade thirty moves into his first game, sacrificing a rook for a bishop,* and to his delight Deep Blue accepted. The position that resulted, as shown in figure 9-3a, helps to illustrate some of the blind spots that result from the computer's lack of strategic thinking.

FIGURE 9-3A: POSITION AFTER KASPAROV'S 32ND MOVE IN GAME 1

Kasparov and Deep Blue each had their own ways of simplifying the position shown in figure 9-3a. Computers break complicated problems down into discrete elements. To Deep Blue, for instance, the position might look more like what you see in figure 9-3b, with each piece assigned a different point value. If you add up the numbers in this way, Deep Blue had the equivalent of a one-pawn advantage over Kasparov, which converts to a win or draw the vast majority of the time.28

FIGURE 9-3B: DISCRETE EVALUATION OF POSITION

Humans, instead, are more capable of focusing on the most important elements and seeing the strategic whole, which sometimes adds up to more than the sum of its parts. To Kasparov, the position looked more like what you see in figure 9-3c, and it was a very good position indeed. What Kasparov sees is that he has three pawns advancing on Deep Blue's king, which has little protection. The king will either need to move out of the way—in which case, Kasparov can move his pawns all the way to Deep Blue's home row and promote* them to queens—or it could potentially be mated. Meanwhile, Kasparov's queen and his bishop, although they are in the lower left-hand corner of the board for now, are capable of moving diagonally across it with relatively little obstruction; they are thus adding to the pressure the vulnerable king already faces from the pawns. Kasparov does not yet know exactly how Deep Blue's king will be mated, but he knows that faced with such pressure the odds are heavily in his favor. Indeed, the strength of Kasparov's position would soon become apparent to Deep Blue, which would resign the game thirteen moves later.

FIGURE 9-3C: HOLISTIC EVALUATION OF POSITION

"Typical computer weakness," Kasparov later said. "I'm sure it was very pleased with the position, but the consequences were too deep for it to judge the position correctly."29

"Human Outcalculates a Calculator," trumpeted the headline in the New York Times,30 which published no fewer than four articles about the game the next day.

But the game had not been without a final twist. It was barely noticed by commentators at the time, but it may have altered chess history.

The Beginning of the End

In the final stage of a chess game, the endgame, the number of pieces on the board are fewer, and winning combinations are sometimes more explicitly calculable. Still, this phase of the game necessitates a lot of precision, since closing out a narrowly winning position often requires dozens of moves to be executed properly without any mistakes. To take an extreme case, the position illustrated in figure 9-4 has been shown to be a winning one for white no matter what black does, but it requires white to execute literally 262 consecutive moves correctly.*

FIGURE 9-4: A WIN FOR WHITE . . . IN 262 MOVES

A human player would almost certainly not solve the position in figure 9-4. However, humans have a lot of practice in completing endgames that might take ten, fifteen, twenty, or twenty-five moves to finish.

The endgame can be a mixed blessing for computers. There are few intermediate tactical goals left, and unless a computer can literally solve the position to the bitter end, it may lose the forest for the trees. However, just as chess computers have databases to cover the opening moves, they also have databases of these endgame scenarios. Literally all positions in which there are six or fewer pieces on the board have been solved to completion. Work on seven-piece positions is mostly complete—some of the solutions are intricate enough to require as many as 517 moves—but computers have memorized exactly which are the winning, losing, and drawing ones.

Thus, something analogous to a black hole has emerged by this stage of the game: a point beyond which the gravity of the game tree becomes inescapable, when the computer will draw all positions that should be drawn and win all of them that should be won. The abstract goals of this autumnal phase of a chess game are replaced by a set of concrete ones: get your queenside pawn to here, and you will win; induce black to move his rook there, and you will draw.

Deep Blue, then, had some incentive to play on against Kasparov in Game 1. Its circuits told it that its position was a losing one, but even great players like Kasparov make serious blunders about once per seventy-five moves.31 One false step by Kasparov might have been enough to trigger Deep Blue's sensors and allow it to find a drawing position. Its situation was desperate, but not quite hopeless.

Instead, Deep Blue did something very strange, at least to Kasparov's eyes. On its forty-fourth turn, Deep Blue moved one of its rooks into white's first row rather than into a more conventional position that would have placed Kasparov's king into check. The computer's move seemed completely pointless. At a moment when it was under assault from every direction, it had essentially passed its turn, allowing Kasparov to advance one of his pawns into black's second row, where it threatened to be promoted to a queen. Even more strangely, Deep Blue resigned the game just one turn later.

What had the computer been thinking? Kasparov wondered. He was used to seeing Deep Blue commit strategic blunders—for example, accepting the bishop-rook exchange—in complex positions where it simply couldn't think deeply enough to recognize the implications. But this had been something different: a tactical error in a relatively simple position—exactly the sort of mistake that computers don't make.

FIGURE 9-5: DEEP BLUE'S PREPLEXING MOVE

"How can a computer commit suicide like that?" Kasparov asked Frederic Friedel, a German chess journalist who doubled as his friend and computer expert, when they studied the match back at the Plaza Hotel that night.32 There were some plausible explanations, none of which especially pleased Kasparov. Perhaps Deep Blue had indeed committed "suicide," figuring that since it was bound to lose anyway, it would rather not reveal any more to Kasparov about how it played. Or perhaps, Kasparov wondered, it was part of some kind of elaborate hustle? Maybe the programmers were sandbagging, hoping to make the hubristic Kasparov overconfident by throwing the first game?

Kasparov did what came most naturally to him when he got anxious and began to pore through the data. With the assistance of Friedel and the computer program Fritz, he found that the conventional play—black moving its rook into the sixth column and checking white's king—wasn't such a good move for Deep Blue after all: it would ultimately lead to a checkmate for Kasparov, although it would still take more than twenty moves for him to complete it.

But what this implied was downright frightening. The only way the computer would pass on a line that would have required Kasparov to spend twenty moves to complete his checkmate, he reasoned, is if it had found another one that would take him longer. As Friedel recalled:

Deep Blue had actually worked it all out, down to the very end and simply chosen the least obnoxious losing line. "It probably saw mates in 20 and more," said Garry, thankful that he had been on the right side of these awesome calculations.33

To see twenty moves ahead in a game as complex as chess was once thought to be impossible for both human beings and computers. Kasparov's proudest moment, he once claimed, had come in a match in the Netherlands in 1999, when he had visualized a winning position some fifteen moves in advance.34 Deep Blue was thought to be limited to a range of six to eight moves ahead in most cases. Kasparov and Friedel were not exactly sure what was going on, but what had seemed to casual observers like a random and inexplicable blunder instead seemed to them to reveal great wisdom.

Kasparov would never defeat Deep Blue again.

Edgar Allan Kasparov

In the second game, the computer played more aggressively, never allowing Kasparov into a comfortable position. The critical sequence came about thirty-five turns in. The material was relatively even: each player had their queen, one of their bishops, both of their rooks and seven of their pawns. But Deep Blue, playing white, had slightly the better of it by having the next move and a queen that had ample room to maneuver. The position (figure 9-6) wasn't quite threatening to Kasparov, but there was the threat of a threat: the next few moves would open up the board and determine whether Deep Blue had a chance to win or whether the game was inevitably headed for a draw.

FIGURE 9-6: DEEP BLUE'S OPTIONS IN 36TH MOVE OF GAME 2

Deep Blue had a couple of moves to consider. It could move its queen into a more hostile position; this would have been the more tactical play. Or it could exchange pawns with white, opening up the left-hand side of the board. This would create a more open, elegant, and strategic position.

The grandmasters commenting on the match uniformly expected Deep Blue to take the first option and advance its queen.35 It was the somewhat more obvious move, and it would be more in character for Deep Blue: computers prefer busy, complex, computationally demanding positions. But after "thinking" for an unusually long time, Deep Blue instead chose the pawn exchange.36

Kasparov looked momentarily relieved, since the pawn swap put less immediate pressure on him. But the more he evaluated the position, the less comfortable he became, biting his knuckles, burying his head in his hands—one audience member thought he caught Kasparov crying.37 Why had Deep Blue not elected to press forward with its queen? Its actual move was not manifestly inferior—indeed, it's a move he could have imagined one of his flesh-and-blood rivals, like his longtime nemesis Anatoly Karpov, trying under the right conditions. But a computer would need a good tactical reason for it—and he simply couldn't figure out what that reason was. Unless his suspicion was correct—Deep Blue was capable of foreseeing twenty or more moves down the road.

Kasparov and Deep Blue played out about eight more turns. To the reporters and experts watching the game, it had become obvious that Kasparov, who had played defensively from the start, had no chance to win. But he might still be able to bring the game to a draw. Then to the surprise of the audience, Kasparov resigned the game after the forty-fifth move. The computer can't have miscalculated, he thought, not when it could think twenty moves ahead. He knew that Deep Blue was going to win, so why deplete his energy when there were four more games left to play?

The crowd in the auditorium burst into robust applause:38 it had been a well-played game, much more so than the first one, and if Deep Blue's checkmate did not seem quite as inevitable to them as it had to Kasparov, it was surely because they hadn't thought about the position as deeply as he had. But they saved their real admiration for Deep Blue: it had played like a human being. "Nice style!" exclaimed Susan Polgar, the women's world champion, to the New York Times.39 "The computer played a champion's style, like Karpov." Joel Benjamin, a grandmaster who had been assisting the Deep Blue team, agreed: "This was not a computer-style game. This was real chess!"

Kasparov hurried out of the Equitable Center that night without speaking to the media, but he had taken his fellow grandmasters' comments to heart. Perhaps Deep Blue was literally human, and not in any existential sense. Perhaps like the Mechanical Turk two centuries earlier, a grandmaster was working surreptitiously to pull its gears behind the scenes. Perhaps Benjamin, a strong player who had once drawn with Kasparov, had not just been coaching Deep Blue but actually intervening on its behalf during the games.

With their minds so powerfully wired to detect patterns, chess champions have a reputation for being slightly paranoid. At a press conference the next day, Kasparov accused IBM of cheating. "Maradona called it the hand of God," he said of the computer's play.40 It was a coy allusion to the goal that the great Argentinean soccer player Diego Maradona had scored in an infamous 1986 World Cup match against England. Replays later revealed that the ball had been put into the net not off his head, but instead, illegally, off his left hand. Maradona claimed that he had scored the goal "un poco con la cabeza de Maradona y otro poco con la mano de Dios"—a little with the head of Maradona and a little with the hand of God. Kasparov, likewise, seemed to think Deep Blue's circuitry had been supplemented with a superior intelligence.

Kasparov's two theories about Deep Blue's behavior were, of course, mutually contradictory—as Edgar Allan Poe's conceptions of the Mechanical Turk had been. The machine was playing much too well to possibly be a computer—or the machine had an intelligence so vast that no human had any hope of comprehending it.

Still, quitting the second game had been a mistake: Deep Blue had not in fact clinched its victory, as Friedel and Yuri Dokhoian, Kasparov's most trusted assistant, sheepishly revealed to him over lunch the next day. After playing out the position on Fritz overnight, they had found a line which in just seven more turns would have forced Deep Blue into perpetual check and given Kasparov his tie.* "That was all?" Kasparov said, staring blankly at the traffic on Fifth Avenue. "I was so impressed by the deep positional play of the computer that I didn't think there was any escape."41

Although at 1-1 the match was still even, Kasparov's confidence was deeply shaken. He had never lost a competitive chess match in his life; now, he was on the ropes. And making matters worse, he had committed a chess sin of the highest order: resigning a game that he could have played to a draw. It was an embarrassing, unprecedented mistake. The journalists and grandmasters covering the match couldn't recall the last time a champion made such an error.

Kasparov resolved that he wouldn't be able to beat Deep Blue by playing the forceful, intimidating style of chess that had made him World Champion. Instead, he would have to try to trick the computer with a cautious and unconventional style, in essence playing the role of the hacker who prods a program for vulnerabilities. But Kasparov's opening move in the third game, while unusual enough to knock Deep Blue out of its databases, was too inferior to yield anything better than a draw. Kasparov played better in the fourth and fifth games, seeming to have the advantage at points in both of them, but couldn't overcome the gravity of Deep Blue's endgame databases and drew both of them as well. The match was square at one win for each player and three ties, with one final game to play.

On the day of the final game, Kasparov showed up at the Equitable Center looking tired and forlorn; Friedel later recalled that he had never seen him in such a dark mood. Playing the black pieces, Kasparov opted for something called the Caro-Kann Defense. The Caro-Kann is considered somewhat weak— black's winning percentage with it is 44.7 percent historically—although far from irredeemable for a player like Karpov who knows it well. But Kasparov did not know the Caro-Kann; he had rarely played it in tournament competition. After just a few moves, he was straining, taking a long time to make decisions that were considered fairly routine. And on his seventh move, he committed a grievous blunder, offering a knight sacrifice one move too early. Kasparov recognized his mistake almost immediately, slumping down in his chair and doing nothing to conceal his displeasure. Just twelve moves later—barely an hour into the game—he resigned, storming away from the table.

Deep Blue had won. Only, it had done so less with a bang than an anticlimactic whimper. Was Kasparov simply exhausted, exacerbating his problems by playing an opening line with which he had little familiarity? Or, as the grandmaster Patrick Wolff concluded, had Kasparov thrown the game,42 to delegitimize Deep Blue's accomplishment? Was there any significance to the fact that the line he had selected, the Caro-Kann, was a signature of Karpov, the rival whom he had so often vanquished?

But these subtleties were soon lost to the popular imagination. Machine had triumphed over man! It was like when HAL 9000 took over the spaceship. Like the moment when, exactly thirteen seconds into "Love Will Tear Us Apart," the synthesizer overpowers the guitar riff, leaving rock and roll in its dust.43

Except it wasn't true. Kasparov had been the victim of a large amount of human frailty—and a tiny software bug.

How to Make a Chess Master Blink

Deep Blue was born at IBM's Thomas J. Watson Center—a beautiful, crescent-shaped, retro-modern building overlooking the Westchester County foothills. In its lobby are replicas of early computers, like the ones designed by Charles Babbage. While the building shows a few signs of rust—too much wood paneling and too many interior offices—many great scientists have called it home, including the mathematician Benoit Mandelbrot, and Nobel Prize winners in economics and physics.

I visited the Watson Center in the spring of 2010 to see Murray Campbell, a mild-mannered and still boyish-looking Canadian who was one of the chief engineers on the project since its days as Deep Thought at Carnegie Mellon. (Today, Campbell oversees IBM's statistical modeling department.) In Campbell's office is a large poster of Kasparov glaring menacingly at a chessboard with the caption:

How Do You Make a Computer Blink?

Kasparov vs. Deep Blue

May 3–11, 1997

In the end, Kasparov, not Deep Blue, blinked, although not quite for the reasons that Campbell and his team were expecting.

Deep Blue was designed with the goal of beating Kasparov and Kasparov specifically. The team tried to predict which opening sequences Kasparov was most likely to use and develop strong counterattacks to them. (Kasparov, indeed, averted the trap by playing opening moves that he had rarely used before in tournament competition.) Because of its mediocre performance against Kasparov in 1996 and its problems against like-minded players in training matches, meanwhile, Deep Blue's processing power was doubled and its heuristics were refined.44 Campbell knew that Deep Blue needed to probe more deeply (but perhaps more selectively) into the search tree to match wits with Kasparov's deep strategic thinking. At the same time, the system was designed to be slightly biased toward complicated positions, which played more to its strengths.

"Positions that are good for computers are complex positions with lots of pieces on the board so there's lots of legal moves available," Campbell told me. "We want the positions where tactics are more important than strategy. So you can do some minor things to encourage that."

In this sense, Deep Blue was more "human" than any chess computer before or since. Although game theory does not come into play in chess to the same degree it does in games of incomplete information like poker, the opening sequences are one potential exception. Making a slightly inferior move to throw your opponent off-balance can undermine months of his preparation time—or months of yours if he knows the right response to it. But most computers try to play "perfect" chess rather than varying their game to match up well against their opponent. Deep Blue instead did what most human players do and leaned into positions where Campbell thought it might have a comparative advantage.

Feature or Bug?

Still, Kasparov's skills were so superior in 1997 that it was really just a matter of programming Deep Blue to play winning chess.

In theory, programming a computer to play chess is easy: if you let a chess program's search algorithms run for an indefinite amount of time, then all positions can be solved by brute force. "There is a well-understood algorithm to solve chess," Campbell told me. "I could probably write the program in half a day that could solve the game if you just let it run long enough." In practice, however, "it takes the lifetime of the universe to do that," he lamented.

Teaching a chess computer how to beat a World Champion, instead, often comes down to a banal process of trial and error. Does allotting the program more time in the endgame and less in the midgame improve performance on balance? Is there a better way to evaluate the value of a knight vis-à-vis a bishop in the early going? How quickly should the program prune dead-looking branches on its search tree even if it knows there is some residual chance that a checkmate or a trap might be lurking there?

By tweaking these parameters and seeing how it played with the changes, Campbell put Deep Blue through many trials. But sometimes it still seemed to make errors, playing strange and unexpected moves. When this happened, Campbell had to ask the age-old programmer's question: was the new move a feature of the program—a eureka moment that indicated it was growing yet more skilled? Or was it a bug?

My general advice, in the broader context of forecasting, is to lean heavily toward the "bug" interpretation when your model produces an unexpected or hard-to-explain result. It is too easy to mistake noise for a signal. Bugs can undermine the hard work of even the strongest forecasters.

Bob Voulgaris, the millionaire basketball bettor I introduced to you in chapter 8, one year decided that he wanted to bet baseball. The simulator he designed consistently recommended "under" bets on the Philadelphia Phillies and the bets weren't doing very well. It turned out that the error came down to a single misplaced character in 10,000 lines of code: his assistant had mistakenly coded the Phillies' home ballpark—Citizens Bank Park, a compact field that boosts offense and home runs—as P-H-l rather than P-H-I. That one line of code had been enough to swamp the signal in his program and tie up Voulgaris's capital in betting on the noise. Voulgaris was so dismayed by the bug that he stopped using his baseball-betting program entirely.

The challenge for Campbell is that Deep Blue long ago became better at chess than its creators. It might make a move that they wouldn't have played, but they wouldn't necessarily know if it was a bug.

"In the early stages of debugging Deep Blue, when it would make a move that was unusual, I would say, ‘Oh, there's something wrong,'" Campbell told me. "We'd dig in and look at the code and eventually figure out what the problem was. But that happened less and less as time went on. As it continued to make these unusual moves, we'd look in and see that it had figured out something that is difficult for humans to see."

Perhaps the most famous moves in chess history were made by the chess prodigy Bobby Fischer in the so-called "Game of the Century" in 1956 (figure 9-7). Fischer, just thirteen years old at the time, made two dramatic sacrifices in his game against the grandmaster Donald Byrne—at one point offering up a knight for no apparent gain, then a few moves later, deliberately leaving his queen unguarded to advance one of his bishops instead. Both moves were entirely right; the destruction that Fischer realized on Byrne from the strategic gain in his position became obvious just a few moves later. However, few grandmasters then or today would have considered Fischer's moves. Heuristics like "Never give up your queen except for another queen or an immediate checkmate" are too powerful, probably because they serve a player well 99 percent of the time.

FIGURE 9-7: BOBBY FISCHER'S FAMOUS SACRIFICES (1956)

When I put the positions into my midrange laptop and ran them on the computer program Fritz, however, it identified Fischer's plays after just a few seconds. In fact, the program considers any moves other than the ones that Fischer made to be grievous errors. In searching through all possible moves, the program identified the situations where the heuristic should be discarded.

We should probably not describe the computer as "creative" for finding the moves; instead, it did so more through the brute force of its calculation speed. But it also had another advantage: it did not let its hang-ups about the right way to play chess get in the way of identifying the right move in those particular circumstances. For a human player, this would have required the creativity and confidence to see beyond the conventional thinking. People marveled at Fischer's skill because he was so young, but perhaps it was for exactly that reason that he found the moves: he had the full breadth of his imagination at his disposal. The blind spots in our thinking are usually of our own making and they can grow worse as we age. Computers have their blind spots as well, but they can avoid these failures of the imagination by at least considering all possible moves.

Nevertheless, there were some bugs in Deep Blue's inventory: not many, but a few. Toward the end of my interview with him, Campbell somewhat mischievously referred to an incident that had occurred toward the end of the first game in their 1997 match with Kasparov.

"A bug occurred in the game and it may have made Kasparov misunderstand the capabilities of Deep Blue," Campbell told me. "He didn't come up with the theory that the move that it played was a bug."

The bug had arisen on the forty-fourth move of their first game against Kasparov; unable to select a move, the program had defaulted to a last-resort fail-safe in which it picked a play completely at random. The bug had been inconsequential, coming late in the game in a position that had already been lost; Campbell and team repaired it the next day. "We had seen it once before, in a test game played earlier in 1997, and thought that it was fixed," he told me. "Unfortunately there was one case that we had missed."

In fact, the bug was anything but unfortunate for Deep Blue: it was likely what allowed the computer to beat Kasparov. In the popular recounting of Kasparov's match against Deep Blue, it was the second game in which his problems originated—when he had made the almost unprecedented error of forfeiting a position that he could probably have drawn. But what had inspired Kasparov to commit this mistake? His anxiety over Deep Blue's forty-fourth move in the first game—the move in which the computer had moved its rook for no apparent purpose. Kasparov had concluded that the counterintuitive play must be a sign of superior intelligence. He had never considered that it was simply a bug.

For as much as we rely on twenty-first-century technology, we still have Edgar Allan Poe's blind spots about the role that these machines play in our lives. The computer had made Kasparov blink, but only because of a design flaw.

What Computers Do Well

Computers are very, very fast at making calculations. Moreover, they can be counted on to calculate faithfully—without getting tired or emotional or changing their mode of analysis in midstream.

But this does not mean that computers produce perfect forecasts, or even necessarily good ones. The acronym GIGO ("garbage in, garbage out") sums up this problem. If you give a computer bad data, or devise a foolish set of instructions for it to analyze, it won't spin straw into gold. Meanwhile, computers are not very good at tasks that require creativity and imagination, like devising strategies or developing theories about the way the world works.

Computers are most useful to forecasters, therefore, in fields like weather forecasting and chess where the system abides by relatively simple and well-understood laws, but where the equations that govern the system must be solved many times over in order to produce a good forecast. They seem to have helped very little in fields like economic or earthquake forecasting where our understanding of root causes is blurrier and the data is noisier. In each of those fields, there were high hopes for computer-driven forecasting in the 1970s and 1980s when computers became more accessible to everyday academics and scientists, but little progress has been made since then.

Many fields lie somewhere in between these two poles. The data is often good but not great, and we have some understanding of the systems and processes that generate the numbers, but not a perfect one. In cases like these, it may be possible to improve predictions through the process that Deep Blue's programmers used: trial and error. This is at the core of business strategy for the company we most commonly associate with Big Data today.

When Trial and Error Works

Visit the Googleplex in Mountain View, California, as I did in late 2009, and it isn't always clear when somebody is being serious and when they're joking around. It's a culture that fosters creativity, with primary colors, volleyball courts, and every conceivable form of two-wheeled vehicle. Google people, even its engineers and economists, can be whimsical and offbeat.

"There are these experiments running all the time," said Hal Varian, the chief economist at Google, when I met him there. "You should think of it as more of an organism, a living thing. I have said that we should be concerned about what happens when it comes alive, like Skynet.* But we made a deal with the governor of California"—at the time, Arnold Schwarzenegger—"to come and aid us."

Google performs extensive testing on search and its other products. "We ran six thousand experiments on search last year and probably another six thousand or so on the ad monetization side," he said. "So Google is doing on a rough order of ten thousand experiments a year."

Some of these experiments are highly visible—occasionally involving rolling out a whole new product line. But most are barely noticeable: moving the placement of a logo by a few pixels, or slightly permuting the background color on an advertisement, and then seeing what effect that has on click-throughs or monetization. Many of the experiments are applied to as few as 0.5 percent of Google's users, depending on how promising the idea seems to be.

When you search for a term on Google, you probably don't think of yourself as participating in an experiment. But from Google's standpoint, things are a little different. The search results that Google returns, and the order in which they appear on the page, represent their prediction about which results you will find most useful.

How is a subjective-seeming quality like "usefulness" measured and predicted? If you search for a term like best new mexican restaurant, does that mean you are planning a trip to Albuquerque? That you are looking for a Mexican restaurant that opened recently? That you want a Mexican restaurant that serves Nuevo Latino cuisine? You probably should have formed a better search query, but since you didn't, Google can convene a panel of 1,000 people who made the same request, show them a wide variety of Web pages, and have them rate the utility of each one on a scale of 0 to 10. Then Google would display the pages to you in order of the highest to lowest average rating.

Google cannot do this for every search request, of course—not when they receive hundreds of millions of search requests per day. But, Varian told me, they do use human evaluators on a series of representative search queries. Then they see which statistical measurements are best correlated with these human judgments about relevance and usefulness. Google's best-known statistical measurement of a Web site is PageRank,45 a score based on how many other Web pages link to the one you might be seeking out. But PageRank is just one of two hundred signals that Google uses46 to approximate the human evaluators' judgment.

Of course, this is not such an easy task—two hundred signals applied to an almost infinite array of potential search queries. This is why Google places so much emphasis on experimentation and testing. The product you know as Google search, as good as it is, will very probably be a little bit different tomorrow.

What makes the company successful is the way it combines this rigorous commitment to testing with its freewheeling creative culture. Google's people are given every inducement to do what people do much better than computers: come up with ideas, a lot of ideas. Google then harnesses its immense data to put these ideas to the test. The majority of them are discarded very quickly, but the best ones survive.

Computer programs play chess in this way, exploring almost all possible options in at least some depth, but focusing their resources on the more promising lines of attack. It is a very Bayesian process: Google is always at a running start, refining its search algorithms, never quite seeing them as finished.

In most cases, we cannot test our ideas as quickly as Google, which gets feedback more or less instantaneously from hundreds of millions of users around the world. Nor do we have access to a supercomputer, as Deep Blue's engineers did. Progress will occur at a much slower rate.

Nevertheless, a commitment to testing ourselves—actually seeing how well our predictions work in the real world rather than in the comfort of a statistical model—is probably the best way to accelerate the learning process.

Overcoming Our Technological Blind Spot

In many ways, we are our greatest technological constraint. The slow and steady march of human evolution has fallen out of step with technological progress: evolution occurs on millennial time scales, whereas processing power doubles roughly every other year.

Our ancestors who lived in caves would have found it advantageous to have very strong, perhaps almost hyperactive pattern-recognition skills—to be able to identify in a split-second whether that rustling in the leaves over yonder was caused by the wind or by an encroaching grizzly bear. Nowadays, in a fast-paced world awash in numbers and statistics, those same tendencies can get us into trouble: when presented with a series of random numbers, we see patterns where there aren't any. (Advertisers and politicians, possessed of modern guile, often prey on the primordial parts of our brain.)

Chess, however, makes for a happy ending. Kasparov and Deep Blue's programmers saw each other as antagonists, but they each taught us something about the complementary roles that computer processing speed and human ingenuity can play in prediction.

In fact, the best game of chess in the world right now might be played neither by man nor machine.47 In 2005, the Web site ChessBase.com, hosted a "freestyle" chess tournament: players were free to supplement their own insight with any computer program or programs that they liked, and to solicit advice over the Internet. Although several grandmasters entered the tournament, it was won neither by the strongest human players nor by those using the most highly regarded software, but by a pair of twentysomething amateurs from New Hampshire, Steven Cramton and Zackary "ZakS" Stephen, who surveyed a combination of three computer programs to determine their moves.48 Cramton and Stephen won because they were neither awed nor intimidated by technology. They knew the strengths and weakness of each program and acted less as players than as coaches.

Be wary, however, when you come across phrases like "the computer thinks the Yankees will win the World Series." If these are used as shorthand for a more precise phrase ("the output of the computer program is that the Yankees will win the World Series"), they may be totally benign. With all the information in the world today, it's certainly helpful to have machines that can make calculations much faster than we can.

But if you get the sense that the forecaster means this more literally—that he thinks of the computer as a sentient being, or the model as having a mind of its own—it may be a sign that there isn't much thinking going on at all. Whatever biases and blind spots the forecaster has are sure to be replicated in his computer program.

We have to view technology as what it always has been—a tool for the betterment of the human condition. We should neither worship at the altar of technology nor be frightened by it. Nobody has yet designed, and perhaps no one ever will, a computer that thinks like a human being.49 But computers are themselves a reflection of human progress and human ingenuity: it is not really "artificial" intelligence if a human designed the artifice.