# 0801. OCP: The Open-Closed Principle

## Conclusion

The OCP is one of the driving forces behind the architecture of systems. The goal is to make the system easy to extend without incurring a high impact of change. This goal is accomplished by partitioning the system into components, and arranging those components into a dependency hierarchy that protects higher-level components from changes in lower-level components.

OCP 是我们进行系统架构设计的主导原则，其主要目标是让系易于扩展，同时限制其每次被修改所影响的范围。实现方式是通过将系統划分为一系列组件，并且将这些组件间的依赖关系按层次结构进行组织，使得高阶组件不会因低阶组件被修改而受到影响。

## 8.0

The Open-Closed Principle (OCP) was coined in 1988 by Bertrand Meyer. [1] 

It says: A software artifact should be open for extension but closed for modification.

In other words, the behavior of a software artifact ought to be extendible, without having to modify that artifact.

This, of course, is the most fundamental reason that we study software architecture. Clearly, if simple extensions to the requirements force massive changes to the software, then the architects of that software system have engaged in a spectacular failure.

Most students of software design recognize the OCP as a principle that guides them in the design of classes and modules. But the principle takes on even greater significance when we consider the level of architectural components.

A thought experiment will make this clear.

1 Bertrand Meyer. Object Oriented Software Construction, Prentice Hall, 1988, p. 23.

开闭原则（OCP）是 Bertrand Meyer 在 1988 年提出的，该设计原则认为设计良好的计算机软件应该易于扩展，同时抗拒修改。换句话说，一个设计良好的计算机系统应该在不需要修改的前提下就可以轻易被扩展。

其实这也是我们研究软件架构的根本目的。如果对原始需求的小小延伸就需要对原有的软件系统进行大幅修改，那么这个系统的架构设计显然是失败的。尽管大部分软件设计师都已经认可了 OCP 是设计类与模块时的重要原则，但是在软件架构层面，这项原则的意义则更为重大。下面，让我们用一个思想实验来做一些说明。

## 8.1 A Thought Experiment

Imagine, for a moment, that we have a system that displays a financial summary on a web page. The data on the page is scrollable, and negative numbers are rendered in red.

Now imagine that the stakeholders ask that this same information be turned into a report to be printed on a black-and-white printer. The report should be properly paginated, with appropriate page headers, page footers, and column labels. Negative numbers should be surrounded by parentheses.

Clearly, some new code must be written. But how much old code will have to change?

A good software architecture would reduce the amount of changed code to the barest minimum. Ideally, zero.

How? By properly separating the things that change for different reasons (the Single Responsibility Principle), and then organizing the dependencies between those things properly (the Dependency Inversion Principle).

By applying the SRP, we might come up with the data-flow view shown in Figure 8.1. Some analysis procedure inspects the financial data and produces reportable data, which is then formatted appropriately by the two reporter processes.

![](./res/2020016.png)

Figure 8.1  Applying the SRP

The essential insight here is that generating the report involves two separate responsibilities: the calculation of the reported data, and the presentation of that data into a web- and printer-friendly form.

Having made this separation, we need to organize the source code dependencies to ensure that changes to one of those responsibilities do not cause changes in the other. Also, the new organization should ensure that the behavior can be extended without undo modification.

We accomplish this by partitioning the processes into classes, and separating those classes into components, as shown by the double lines in the diagram in Figure 8.2. In this figure, the component at the upper left is the Controller. At the upper right, we have the Interactor. At the lower right, there is the Database. Finally, at the lower left, there are four components that represent the Presenters and the Views.

![](./res/2020017.png)

Figure 8.2  Partitioning the processes into classes and separating the classes into components

Classes marked with `<I> `are interfaces; those marked with `<DS>` are data structures. Open arrowheads are using relationships. Closed arrowheads are implements or inheritance relationships.

The first thing to notice is that all the dependencies are source code dependencies. An arrow pointing from class A to class B means that the source code of class A mentions the name of class B, but class B mentions nothing about class A. Thus, in Figure 8.2, FinancialDataMapper knows about FinancialDataGateway through an implements relationship, but FinancialGateway knows nothing at all about FinancialDataMapper.

The next thing to notice is that each double line is crossed in one direction only. This means that all component relationships are unidirectional, as shown in the component graph in Figure 8.3. These arrows point toward the components that we want to protect from change.

1『想要高层不受底层变动的影响，底层必须依赖于高层。高层是接口类，底层是实现类。举例：B 是高层，A 是底层。谁调用 A 谁依赖于 A。B 直接调用 A 的话，B 依赖于 A，A 的变动会影响到 B。但如果把 A 的实现抽象出一个接口 I，B 调用 I 接口，A 调用 I 接口实现 I，那么 A 依赖于 I 就相当于 A 依赖于 B，A 的变动不会影响到 B，这就实现了依赖倒置。（2021-05-12）』

![](./res/2020018.png)

Figure 8.3  The component relationships are unidirectional

Let me say that again: If component A should be protected from changes in component B, then component B should depend on component A.

We want to protect the Controller from changes in the Presenters. We want to protect the Presenters from changes in the Views. We want to protect the Interactor from changes in — well, anything.

The Interactor is in the position that best conforms to the OCP. Changes to the Database, or the Controller, or the Presenters, or the Views, will have no impact on the Interactor.

Why should the Interactor hold such a privileged position? Because it contains the business rules. The Interactor contains the highest-level policies of the application. All the other components are dealing with peripheral concerns. The Interactor deals with the central concern.

Even though the Controller is peripheral to the Interactor, it is nevertheless central to the Presenters and Views. And while the Presenters might be peripheral to the Controller, they are central to the Views.

Notice how this creates a hierarchy of protection based on the notion of「level.」Interactors are the highest-level concept, so they are the most protected. Views are among the lowest-level concepts, so they are the least protected. Presenters are higher level than Views, but lower level than the Controller or the Interactor.

This is how the OCP works at the architectural level. Architects separate functionality based on how, why, and when it changes, and then organize that separated functionality into a hierarchy of components. Higher-level components in that hierarchy are protected from the changes made to lower-level components.

思想实验

假设我们现在要设计一个在 Web 页面上展示财务数据的系统，页面上的数据要可以滚动显示，其中负值应显示为红色。

接下来，该系统的所有者又要求同样的数据需要形成一个报表，该报表要能用黑白打印机打印，并且其报表格式要得到合理分页，每页都要包含页头、页尾及栏目名。同时，负值应该以括号表示。显然，我们需要增加一些代码来完成这个要求。但在这里我们更关注的问题是，满足新的要求需要更改多少旧代码。一个好的软件架构设计师会努力将旧代码的修改需求量降至最小，甚至为 0。

但该如何实现这一点呢？我们可以先将满足不同需求的代码分组（即 SRP），然后再来调整这些分组之间的依赖关系（即 DIP）。

利用 SRP，我们可以按图 8.1 中所展示的方式来处理数据流。即先用一段分析程序处理原始的财务数据，以形成报表的数据结构，最后再用两个不同的报表生成器来产生报表。这里的核心就是将应用生成报表的过程拆成两个不同的操作。即先计算出报表数据，再生成具体的展示报表（分别以网页及纸质的形式展示）。

接下来，我们就该修改其源代码之间的依赖关系了。这样做的目的是保证其中ー个操作被修改之后不会影响到另外一个操作。同时，我们所构建的新的组织形式应该保证该程序后续在行为上的扩展都无须修改现有代码。

在具体实现上，我们会将整个程序进程划分成一系列的类，然后再将这些类分割成不同的组件。下面，我们用图 8.2 中的那些双线框来具体描述一下个实现。在这个图中，左上角的组件是 Controller，右上角是 Interactor，右下角是 Database，左下角则有四个组件分别用于代表不同的 Presenter 和 View。

在图 8.2 中，用 `<I>` 标记的类代表接口，用 `<DS>` 标记的则代表数据结构；开放箭头指代的是使用关系，闭合箭头则指代了实现与继承关系。

首先，我们在图 8.2 中看到的所有依赖关系都是其源代码中存在的依赖关系。这里，从类 A 指向类 B 的箭头意味着 A 的源代码中涉及了 B，但是 B 的源代码中并不涉及 A。因此在图 8.2 中，FinancialDataMapper 在实现接口时需要知道 FinancialDataGateway 的实现，而 FinancialGateway 则完全不必知道 FinancialDataMapper 的实现。

其次，这里很重要的一点是这些双线框的边界都是单向跨越的。也就是说，上图中所有组件之间的关系都是单向依赖的，如图 8.3 所示，图中的箭头都指向那些我们不想经常更改的组件。让我们再来复述一下这里的设计原则：如果 A 组件不想被 B 组件上发生的修改所影响，那么就应该让 B 组件依赖于 A 组件。

所以现在的情况是，我们不想让发生在 Presenter 上的修改影响到 Controller，也不想让发生在 View 上的修改影响到 Presenter。而最关键的是，我们不想让任何修改影响到 Interactor。其中，Interactor 组件是整个系统中最符合 OCP 的。发生在 Database、Controller、Presenter 甚至 View 上的修改都不会影响到 interactor。

为什么 Interactor 会被放在这么重要的位置上呢？因为它是该程序的业务遇辑所在之处，Interactor 中包含了其最高层次的应用策略。其他组件都只是负责处理周边的辅助逻辑，只有 Interactor 才是核心组件。虽然 Controllers 组件只是 Interactor 的附属品，但它却是 Presenter 和 View 所服务的核心。同样的，虽然 Presenters 组件是 Controller 的附属品，但它却是 View 所服务的核心。

另外需要注意的是，这里利用「层级」这个概念创造了一系列不同的保护层级。譬如，Interactor 是最高层的抽象，所以它被保护得最严密，而 Presenteretview 的层级高，但比 Controller 和 Interactor 的层级低。

以上就是我们在软件架构层次上对 OCP 这一设计原则的应用。软件架构师可以根据相关函数被修改的原因、修改的方式及修改的时间来对其进行分组隔离，并将这些互相隔离的函数分组整理成组件结构，使得高阶组件不会因低阶组件被修改而受到影响。

## 8.2 Directional Control

If you recoiled in horror from the class design shown earlier, look again. Much of the complexity in that diagram was intended to make sure that the dependencies between the components pointed in the correct direction.

For example, the FinancialDataGateway interface between the FinancialReportGenerator and the FinancialDataMapper exists to invert the dependency that would otherwise have pointed from the Interactor component to the Database component. The same is true of the FinancialReportPresenter interface, and the two View interfaces.

依赖方向的控制

如果刚刚的类设计把你吓着了，别害怕！你刚刚在图表中所看到的复杂度是我们想要对组件之间的依赖方向进行控制而产生的。

例如，FinancialReportGenerator 和 FinancialDataMapper 之间的 FinancialDataGateway 接口是为了反转 Interactor 与 Database 之间的依赖关系而产生的。同样的，FinancialReportPresenter 接口与两个 view 接口之间也类似于这种情况。

## 8.3 Information Hiding

The FinancialReportRequester interface serves a different purpose. It is there to protect the FinancialReportController from knowing too much about the internals of the Interactor. If that interface were not there, then the Controller would have transitive dependencies on the FinancialEntities.

Transitive dependencies are a violation of the general principle that software entities should not depend on things they don't directly use. We'll encounter that principle again when we talk about the Interface Segregation Principle and the Common Reuse Principle.

So, even though our first priority is to protect the Interactor from changes to the Controller, we also want to protect the Controller from changes to the Interactor by hiding the internals of the Interactor.

信息隐藏

当然，FinancialReportRequester 接口的作用则完全不同，它的作用是保护 FinancialReportController。不过度依赖于 Interactor 的内部细节。如果没有这个接口，则 Controller 将会传递性地依赖于 FinancialEntities。这种传递性依赖违反了「软件系统不应该依赖其不直接使用的组件」这一基本原则。之后，我们会在讨论接口隔离原则和共同复用原则的时候再次提到这一点。所以，虽然我们的首要目的是为了让 interactor。屏蔽掉发生在 Controller 上的修改，但也需要通过隐藏 Interactor 内部细节的方法来让其屏掉来自 Controller 的依赖。