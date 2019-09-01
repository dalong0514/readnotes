# 
> 2018000模板


15. Local Interaction Models





Every generation laughs at the old fashions, but follows religiously the new.

—Henry David Thoreau



In this chapter, we study two models of local interactions, the local majority model and the Game of Life. These models both take place on a checkerboard consisting of cells that can be in one of two states. Otherwise, the models could not be more different. In the local majority model, cells update by matching the state of the majority of their neighbors. In the Game of Life, cells rely on a more complicated rule with multiple thresholds. The outcomes of the models also differ. The local majority model always converges to an equilibrium, while the Game of Life, depending on its initial configuration, can produce any class of outcome: equilibria, cycles, complexity, or randomness.

The local majority model can be used to explain and predict real-world outcomes in social and physical systems. It can represent discrete choices by conforming individuals or capture physical systems such as spin glasses, where magnetic entities align with neighbors. In contrast, the Game of Life is purely exploratory. It was developed to explore how simple rules can aggregate to produce complex phenomena. In the Game of Life, the periodic patterns, complex sequences, and randomness emerge from the interactions. The model shows how the whole can be different in kind from the parts. As a crude analogy, the human brain also produces emergent phenomena such as emotion, cognition, and consciousness from much simpler parts.

We begin by analyzing the local majority model. We show how a standard coordination game provides microfoundations for the behavioral rule assumed in the model. We can thus interpret the actors in the model as either rule-following agents or rational actors applying a best-response strategy. We then describe the Game of Life and show how it produces complexity from simple rules. The discussion at the end of the chapter highlights the value of exploring with local interaction models.





The Local Majority Model


The local majority model assumes cells arrayed on a checkerboard.1 Each cell is in one of two states, which we refer to as on or off. Initially we assign states randomly; thereafter, a cell’s state depends on the states of its neighbors. The neighbors can be defined in several ways. We take the neighbors of cell C to be the four cells to the north, south, east, and west as well as the four diagonally adjacent cells, creating a neighborhood of size eight.





Local Majority Model


Each cell on a two-dimensional square grid is in one of two states: on or off. Each cell has eight neighbors (shown in the diagram below).2 In each period, a cell is chosen randomly.3 The cell changes its state if and only if five or more of its neighbors are in the other state.





The local interactions in the local majority model includes positive feedbacks: cells match the state of other cells. Figure 15.1 shows a typical equilibrium configuration of the local majority model.

In equilibrium, every cell’s state matches the state of a majority of its neighbors. Equilibrium configurations resemble the black-and-white patchiness of a Holstein cow. While the equilibrium configuration depends on the initial configuration of the cells, the model does not exhibit extreme sensitivity to initial conditions. Switching the state of one cell results in at most small changes in the final configuration. The pattern also depends on the order in which cells are activated. Thus, the model exhibits path dependence. The number of equilibria is enormous. Two equilibria produced by the model look no more alike than two Holsteins in a field.

The model was developed to capture physical systems where each cell’s state represents an atomic spin—think of each cell as a magnet with either a negative or positive charge. Each magnet resides in a local magnetic field that physically drives it to match the spins of its neighbors. The same model can also represent glasses and crystals.





Figure 15.1: Equilibrium Pattern in the Local Majority Model

Here, we use the model to capture local coordination or conformity among people. We think of each cell as representing an individual’s action. The action could be any convention such as shaking hands or bowing, interrupting or raising one’s hand. A person wants to choose an action that matches those of her neighbors. The checkerboard represents the social network. The checkerboard would be an appropriate social network for a homeowner’s decision to maintain a clean yard, plant trees, or practice ecological landscaping or for people in an auditorium deciding whether to give performers a standing ovation.4 While the checkerboard is at best a crude approximation, with it we gain some core intuitions.

If we run the model on a computer, we find it always goes to a patchy equilibrium configuration. In Chapter 16, we learn why. In the physical interpretation of the local majority model, the patchy equilibrium pattern corresponds to a frustrated state. Many cells have some neighbors in the on state and some in the off state. If we interpret the model through a social lens, the frustrated state can be seen as a suboptimal equilibrium. If being on corresponds to greeting people by shaking hands and being off corresponds to greeting people by bowing, then people on the boundaries of the patches experience awkward interactions with some of their neighbors: they bow when others shake, or they shake when others bow. People would be happier overall if everyone chose the same action—that is, if they solved the coordination game. The suboptimal equilibria, the frustrated state, arises because the interaction effects apply locally. If, instead, cells matched the global majority, then very quickly all of the cells would be in the same state. That insight implies that creating common behaviors may require broad influence networks. If people coordinate with their local neighbors, they create pockets of diverse behaviors. Paradoxically, coordination results in diversity.





Pure Coordination Games


In a pure coordination game, each player chooses one of two actions, A or B. If both players choose the same action, each receives a payoff of 1. If they choose different actions, each receives a payoff of zero.

Actions: A

A: 1, 1

B: 0, 0

Actions: B

A: 0, 0

B: 1, 1

A pure coordination game has two efficient equilibria: both players choose A or both players choose B. It also has an inefficient equilibrium, in which each player randomizes between A and B. We can reinterpret the local majority model with each cell being a player who must choose a common action to play against her eight neighbors. If players can change their action only when randomly activated, a player could increase her payoff by choosing the action that matches a majority of her neighbors’ actions. Such a strategy is called a myopic best response because it does not take into account the likely future actions of the neighbors. A player with five neighbors who have chosen B could increase her payoff in the short term by switching from A to B, but if the player and her neighbors are surrounded by a sea of other players choosing A, then she might have a higher expected payoff by staying with A. The key takeaway is that the behavioral rule in the local majority model, though an assumed rule, can be rooted in a game theoretic model.



The paradox of coordination explains differences across groups as idiosyncratic. For some actions—whether your soy sauce or ketchup is stored in the cupboard or in the refrigerator, or whether people wear their shoes in your house or leave them at the door—it is sensible to coordinate with others. The resulting regional variety adds richness to our lives. The tiny ristretto in Italy, the midsized espresso in France, and the enormous kawa ze smietanka (coffee with cream) in Warsaw add to the pleasure of traveling around Europe.

Other differences, though, can be inefficient. Variations of electrical plugs—two prongs here, three prongs there—can be maddening. As the world becomes more integrated, technological coordination failures can be costly. The Swedes decided to switch from driving on the left to driving on the right to match the rest of continental Europe. The switchover, known as Dagen H, occurred at 4:45 a.m. on September 3, 1967. Every car in Sweden—and many Swedes were on the road in the early morning hours to participate in the event—came to an abrupt stop, and then, over the next fifteen minutes, all of the cars maneuvered from the left to the right side of the road. At 5:00 a.m., the cars began moving again on the opposite side of the road. Despite the incentives to coordinate, sometimes people fail to do so. The people of England, though connected by tunnel to the continent, continue to drive on the “wrong” side of the road, as do the island inhabitants of some, though not all, of their former colonies.





The Paradox of Coordination


If people coordinate locally, then global configurations will be patchy and diverse.



When applying this model, we must keep in mind that many coordinated cultural practices, such as how people mourn their dead or celebrate the birth of a child, are not idiosyncratic curiosities but components of culture, a coherent constellation of behaviors, practices, and artifacts that define who a people are and give them a sense of meaning and belonging.5

As we can with any model, we can experiment with parameters and see how doing so affects the results. For the local interaction model, the size of the patches that form in equilibrium increase faster than the neighborhood size. If we make the neighborhoods, that is, the number of squares that influence a square on the grid, twice as large, the patches become more than twice as large. The model therefore suggests that as technology and urbanization bring us closer together, the force of coordination could result in larger homogeneous patches of behaviors and beliefs.

Experiments also show that if we make the configuration a long, narrow rectangle, the model tends to produces horizontal and vertical stripes, as shown in figure 15.2.6 The zebra-like stripes are an equilibrium because each on (off) cell has five on (off) neighbors. This type of pattern would also be an equilibrium on the square, though it rarely occurs. Perplexing findings like this can result in deep dives into rabbit holes of little empirical or theoretical value. They can also provide insights that lead to deeper, unexpected discoveries.

In this instance, the “squares produce Holstein-style patterns and skinny rectangles give zebra-style patterns” result all but begs us to ask if models like this could explain patterns on animal hides. A foray into the literature shows that they can.7





Figure 15.2: Stable Lines in the Local Majority Model





The Game of Life


Our next model, the Game of Life, also assumes cells on a checkerboard that are in one of two states. The key differences will be that the cell’s rule for updating has two thresholds and that all cells update their states synchronously. Thus we can speak of the initial configuration, the configuration at time 1, the configuration at time 2, and so on. Synchronous updating can be thought of as “marching band dynamics” (update! update! update!).8





The Game of Life


Each cell on a dimensional square grid is either alive (on) or dead (off). Each cell’s neighbors consist of the eight adjacent cells on the grid. Cells update their states synchronously using two rules:

Life rule: A dead cell with exactly three live neighbors becomes alive.

Death rule: A live cell with fewer than two or more than three live neighbors dies.



Start with three live cells in a horizontal row, as shown in figure 15.3. In the next period, we get a vertical row of three cells as seen by applying the rules for life and death to each cell. The live cell in the middle has two live neighbors, so it remains alive. The two live cells at the ends each have one live neighbor, so they die. Finally, the cells above and below the live cell in the center both come to life because each has three live neighbors. By symmetry, another update returns to the horizontal row of three cells. If we continue to iterate the rules, the pattern alternates between a horizontal and vertical line—that is, it blinks.





Figure 15.3: A Blinker in the Game of Life

The blinker results from the interactions of cells. It is not assumed. Complex systems scholars refer to this sort of macro-level phenomenon as emergent. Blinkers are among the more common and least impressive of the emergent structures produced by the Game of Life. Figure 15.4 shows three other simple configurations: a block, a glider, and the R-pentomino. The block is an equilibrium configuration. Each live cell has exactly three live neighbors, and each dead cell has at most two live neighbors. No live cells die, and no dead cells come to life. The middle configuration produces a cycle of size 4 that glides diagonally one cell down and to the right. More elaborate configurations, called glider guns, produce an endless stream of gliders. The third configuration, the R-pentomino, creates a complex sequence of patterns. If we run the model for more than a thousand steps on a large grid, it generates gliders and blinkers as well as several small, stable configurations. The Game of Life can also produce randomness.9 Thus, the Game of Life can produce any class of outcome depending on the initial state.

These capabilities raise philosophical questions. The Game of Life consists of two-state cells arranged on a grid that update using simple rules. It can produce elaborate patterns and, with appropriate coding, it can be turned into a universal computer. The initial pattern can be thought of as the input. The rules produce an outcome that can be interpreted as a calculation. We can therefore draw a crude analogy between the model and the human brain, which also consists of spatially connected simple parts that rely on threshold-based rules, albeit more complicated ones. That is not to say that the patterns we see in the Game of Life can explain consciousness. No book exists that is titled The Game of Life: Consciousness Explained, though Daniel Dennett did write a book called Consciousness Explained in which he posits that simple models like the Game of Life can provide insight into how consciousness might have evolved, an insight echoed by the physicist Stephen Hawking, who wrote, “It is possible to imagine that something like the Game of Life, with only a few basic laws, might produce highly complex features, perhaps even intelligence.”10





Figure 15.4: Patterns in the Game of Life





Summary


In this chapter, we studied two models of interacting cells arranged on a grid. The first model, the local majority model, always goes to one of many possible equilibria, and we can interpret the model as analogous to a variety of physical and social processes. The second model, the Game of Life, can produce any class of outcome, from equilibria to randomness. That model claims no explicit connection to the real world. It provides an example of how constructing an alternative reality can produce insights—the emergence of dynamic macro-level structures from microlevel rules—that deepen our understanding of the world. As the Game of Life shows, the whole can perform functions that far exceed the capacities of its parts. If, for example, we create a slanted figure eight by connecting two 3-by-3 boxes at their corners, the Game of Life produces a cyclic pattern of length eight. It cycles through a set of patterns and then returns to the figure eight in exactly eight steps. That a pattern resembling an eight acts “as if” it counts to eight is quite amazing.

To understand how and why the Game of Life produces complexity while the local majority model inexorably moves to an equilibrium, we need additional analytic tools and frameworks. In Chapter 16, we introduce Lyapunov functions, which use difference equations to classify the state of the world. By careful construction of a Lyapunov function, we can explain why the local majority model must head to equilibrium and also why the Game of Life need not.

As a final note, the salience of the question of whether models, and by extension the real world, produce equilibria, patterns, complexity, or randomness arose naturally from our explorations with models. As we explored, we found some models go to equilibria and others do not. We think of using models to answer questions. In this chapter, we saw how models can raise questions as well.




