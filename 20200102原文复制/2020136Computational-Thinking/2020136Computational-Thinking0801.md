# 0801. Teaching Computational Thinking for All

My basic idea is that programming is the most powerful medium of developing the sophisticated and rigorous thinking needed for mathematics, for grammar, for physics, for statistics, and all the「hard」subjects. Maybe I would even include philosophy and historical analysis. In short, I believe more than ever that programming should be a key part of the intellectual development of people growing up.

—— Seymour Papert (Papert, 2005)

Through the 1990s, CT education was mostly the purview of universities; very little CT education was available elsewhere. Pre-college K–12 schools had a scattering of computer courses; most focused on computer literacy and a handful on programming. A tipping point came after 2000 when many people saw how pervasive computing was in everyday work and home life. Educators and policymakers began to agree that understanding the mechanisms of digitalization is an important 21st-century skill.

The previously obscure notion of the algorithm entered everyday conversation as people cited value they had received from algorithms on their web searches, income tax preparation, online shopping, spreadsheets, neatly formatted documents, display-ready presentations, and computerized courses, and then later on smartphones, social networks, ride hailing, short-term renting, dating, finding friends, and much more. It seemed that understanding how it all works is central for coping in the modern world. It was finally time to bring computing to the K–12 level of education.

## 8.1 Computing Education

Getting computing education to K–12 schools was a struggle of a whole different order from getting computing education into universities. Numerous pilot projects to introduce computers in schools foundered because few teachers had any experience with computers and there was little political support in school boards. By the 1980s, a sea change began as more parents and teachers acquired home computers and came to see the growing importance of computing in their own work. The「computer literacy」courses introduced at that time were generally disappointing from the CT perspective because they focused on the use of tools like word processors and spreadsheets, not on programming.

Getting computing education to K-12 schools was a struggle of a whole different order from getting computing education into universities. Courses on computer literacy, later fluency, did not take hold. A computational thinking movement started in 2006 that energized educators and school boards to bring computer courses into all K-12 schools.

In the late 1990s, at the same time when the internet started to become a household commodity, a new education movement favoring「fluency with information technology」over literacy gained momentum and was supported by a popular textbook of the same name. It was an attractive notion that fluency with language and practices of computing would be a powerful asset in the emerging digitalized world. Bringing computing education to schools would enable children to become smart users of computing technology and would introduce them to the limitations and risks of algorithmic processes behind emerging functions such as online purchasing, Internet searching, news services, communication, and later social media. Despite its attraction, the fluency movement did not produce a widespread change in computing education in K–12 schools.

Then, in 2006, Jeannette Wing proposed that computational thinking is what everyone wants; not literacy or fluency. [1] She struck a resonant chord. In the next several years at the US National Science Foundation (NSF), she mobilized $48 million in resources and convinced many people to bring computer courses into all K–12 schools. Their major successes included getting education organizations to issue definitions of CT and associated curricula at different grade levels; training teachers in CS principles; starting a new family of CS-principles introductory courses at universities; and developing a new Advanced Placement curriculum and exam to interface high schools to these new introductory courses. CT went mainstream.

But as suggested above, this success was not easy. School boards in K–12 institutions had a long history of reluctance to add a computing curriculum in their schools. The CT movement brought a turn of mind to many school boards. Without that movement, we would not be talking about computational thinking in K–12 education at the scale we do it today. In this chapter, we will interpret the progression of computing education as a series of waves that started with the form of CT available in the 1950s (algorithmizing and mathematical problem solving), moved to Papert's Mindstorms, then to literacy and fluency, and culminated most recently in a modern version of CT designed for children in schools.

1 Wing (2006)

1-2『

这篇计算机思维的论文之前在多个场合看到过，自己 2019 年下载了的「2019016Computational thinking」并存入了 Zotero。YouTube 也有 Wing 的一个视频，结合起来一起看。（2021-05-25）

[Jeannette Wing: Computational Thinking - YouTube](https://www.youtube.com/watch?v=YVEUOHw3Qb8)

』

## 8.2 General-Purpose Thinking Tools?

Academic education for automatic computing machinery began in the late 1940s, when computing pioneers started educational programs on numerical methods for computing on large-scale machines. These early efforts went mainstream in the 1950s when the mass production of stored-program computers created a demand for a large number of people who could program them. After the early entry by private companies, university educators started organizing conferences to discuss computing education in the mid-1950s. By 1960, some 150 US universities offered some training in computing. There was, however, no standard view on what people needed to know about computing; individual programs depended on local idiosyncrasies such as specific jobs, needs of businesses, personal agendas of the faculty, research contracts, and other stakeholder interests. [2]

Already in those early days some computing educators described their visions of computing as a thinking tool for learning — a tool to deal with problems and questions in many fields besides computer science. Alan Perlis, who founded the computer science department at Carnegie Mellon University, was an outspoken advocate for this vision. He said that computing would be automating processes in many fields, and people in those fields would be「algorithmizing.」With this term, he referred to mental skills for reasoning about problems and developing computational solutions. George Forsythe cited Perlis in his 1958 address for the Mathematical Association of America:「Whereas we think we know something when we learn it, and are convinced we know it when we can teach it, the fact is that we don't really know it until we can code it for an automatic computer!」A decade later, Forsythe echoed the claim that computing provides general-purpose mental tools that would serve a person for a lifetime. Both Perlis and Forsythe firmly believed that everyone in every field will benefit from learning computing's procedural ways of doing things. They believed that computational models would be useful in all fields.

The visions of computing education grew ever more ambitious about what CT will be able to achieve. Marvin Minsky, a famous pioneer in artificial intelligence, argued, in his 1969 Turing Award speech, that computing would surpass mathematics in importance for early education. [3] Donald Knuth, a pioneer in understanding algorithms, argued that teaching a computer to do something forces precision and leads to deeper understanding than traditional means of thinking. [4] Another pioneer argued that the modern successor to「the classical person」would be「Turing's person.」[5] Two famous computing educators wrote that computing's procedural epistemology is creating a revolution in how people think and express themselves. [6] All this optimism about computing skills transferring to general problem solving turned out to be premature, as we discuss next.

2 Tedre, Simon, and Malmi (2018).

3 Minsky (1970)

4 Knuth (1974).

5 Bolter (1984)

6 Abelson and Sussman (1996)

## 8.3 CT Is Not Easily Transferable

The first wave of bringing CT to K–12 schools focused on programming. In the mid-1960s, some US high schools got DEC PDP-8 minicomputers and enterprising teachers organized courses around them. Numerous initiatives for using computers in schools over the 1960s and 1970s led to a few notable innovations. For example, the Little Man Computer for teaching machine languages and computers to students was introduced in 1965; one of the early programming languages for children, Logo, was introduced in 1967; and the famous concept for Dynabook, a children's portable computer, was born in 1968. Although minicomputers and some microcomputers were common in the late 1970s, educators, lacking financial resources and political will, were unable to transform the pilot courses into a large-scale rollout to schools.

The Logo programming language was a standout among the many initiatives of the 1960s. It was not a stand-alone, general programming language. It was a part of an integrated framework of pedagogical, technological, and educational ideas designed by Seymour Papert based in his deeply grounded understanding of how children learn. His 1980 book Mindstorms, written after a decade of research and experimentation with Logo, was a milestone for computing education and teaching computational thinking. Papert coined the phrase「computational thinking」for the practice of procedural thinking he taught to children. He argued that learning is most effective when learners「construct knowledge」 — they acquire practices from being immersed in a world of practices. They build their knowledge from practicing it rather than being told. The learning theory of constructionism became very popular in education. Papert continued to advocate self-directed learning, project learning, meaningful representations, facilitation-based education, and the use of technology to support learning in the classroom. His ideas influenced the Lego company to design and market the children's programmable bricks called Lego Mindstorms.

Teaching fundamental computational thinking skills, such as programming and computer modeling, is much harder than teaching spreadsheets, word processing, and other application tools of computing. Despite the popularity of constructionism, the central idea of Mindstorms — the shift from「learning to program」to「programming to learn」 — was hard to market among teachers. How could we achieve universal teaching of computational thinking without enough willing teachers? Could we rely on a smaller set of interested teachers to teach everybody?

The hope that a small number of teachers could teach CT to everybody was paired with the transfer hypothesis. The hypothesis is a belief that CT is a metacognitive skill learned from programming; students who learn CT in one domain became better problem-solvers in other domains, too. This belief bolstered the position that teaching computing should be an essential element of K–12 education. The most enthusiastic supporters of the hypothesis made claims such as「the concept of procedure is the secret educators have so long been seeking,」and「the pedagogic value of algorithmic approach aids in the understanding of concepts of all kinds.」They argued that teaching programming improves generic thinking skills such as logical thinking and generally「sharpens the mind.」The transfer hypothesis would indeed be important if it could be validated.

Critics of the transfer hypothesis referred to a research base in developmental cognitive science, arguing that there was no evidence of skill-transfer from programming to other subjects. Research with adults did not support transfer of cognitive skills between domains. Programming itself is a complex network of skills including mathematical abilities, conditional reasoning, analogical reasoning, procedural thinking, temporal reasoning, and memory capacity. It was not clear which parts of this complex transferred or not. After much detailed investigation, education researchers eventually concluded there is not enough evidence to accept the transfer hypothesis. It was not compelling as a justification to teach computing in K–12 schools.

Given that the transfer hypothesis does not work, schools needed more teachers who understood CT and could teach it in different contexts. Few teachers understood computers well enough to do this. Teaching a computer literacy course might be within their reach, but that baby step would not qualify them to teach CT. In the mid-2000s, when the US NSF began supporting the training of more computing teachers, the shortage of qualified teachers began to abate.

## 8.4 From Literacy to Fluency

The early advocates of algorithmic thinking would be appalled at many of the「computer literacy」courses in the 1980s and 1990s, which focused on how to use desktop applications, such as word processors, spreadsheets, and sketchpads. Motivated students and teachers found these courses boring. Literacy with desktop software was a far cry from their aspirations to participate in and shape the computer revolution. The professional societies, including ACM, IEEE-CS, and the British Computer Society, offered to help K–12 educators develop computer courses with more depth, but got little buy-in. In 1999, a US National Research Council commission upped the ante, reframing the question from literacy to fluency. Fluency offered capabilities, concepts, and skills essential for some levels of computational thinking. The NRC initiative was paired with a textbook Fluency with Information Technology that became quite popular among high school teachers.

Many schools brought computing into their curricula for pragmatic reasons as they responded to demands from parents and school boards. They sought access to simulations and other teaching software, access to basic programming, participation in the Internet revolution, learning 21st-century skills, preparation for employment in STEM fields, broadened social participation, and a new means for children to express individual creativity. [7] Educators and parents were disposed toward these goals because they believed that learning programming teaches important skills no other subject does, and because they did not want their children to be at a disadvantage in a world increasingly dependent on skills with information and communication technology.

In the 2000s, the entry of programming and computational design into schools was also easier because of advances in programming methodology and technology and changes in what entry-level programmers needed to know. New languages such as Python were much easier to use and hid well the underlying details of the operating system and hardware. Graphical, drag-and-drop user interfaces were very successful. Powerful tools automated significant parts of the programming process.

With all these advancements in programming languages, tools, and methods, programming was accessible to more students and teachers than ever before. There were more opportunities for becoming fluent in computing. But even so, in 2010 many schools had no computer courses or Advanced Placement curriculum in computing. Gaining fluency was not powerful enough to be a driving force.

7 Guzdial (2015)

## 8.5 Computational Thinking Revived

Jeannette Wing's 2006 essay on computational thinking launched a new wave in the movement to provide computing courses for all students in K–12 schools. The term computational thinking resonated and inspired action where literacy and fluency had not. Wing mobilized significant resources at the NSF to bring a large number of researchers into investigations of CT in education, to train a large number of teachers for teaching CT, to mobilize private organizations to produce K–12 curriculum recommendations for CT, and to develop a new Advanced Placement curriculum and exam on computing principles. Wing's essay became one of the most cited in computing education, a rallying point in a global movement to penetrate CT into K–12 education.

Major organizations including CSTA (Computer Science Teachers Association), the British CAS (Computing at School), Code.org, and the Australian ACARA2 (Australian Curriculum, Assessment, and Reporting Authority) developed and recommended curriculum frameworks for K–12 CT. These organizations promoted coding clubs, coding boot camps, and the international movement called「Hour of Code.」CT became a key word gathering hundreds of thousands of hits in news stories, blog postings, book chapters, articles, research projects, and essays on computing education.

The rapid infusion of so many enthusiastic newcomers who were unfamiliar with the long prior history of CT led to considerable confusion about definitions and learning objectives of CT. Some invented new CT frameworks for K–12 schools from scratch, imperfectly reinventing ideas that had been discussed for decades, omitting important ideas, confusing CT with the use of applications, and incorporating into their dogma some serious misconceptions about computing and algorithms. This resulted in a variety of tensions between different groups that used CT. [8] Here are the some of the most common points of contention, many of which can be explained by differences between CT for beginners and CT for professionals — basic CT in K–12 is surely different from advanced CT in higher education — as well as different contexts of application:

1 Whether CT is limited to thinking about the mechanics of constructing algorithms — or includes thinking about machines, computational science, software engineering, and design.

2 Whether CT is mostly about programming — or also encompasses systems, networks, and architectures; or whether it is not really about any of those.

3 Whether the definition, that CT is the formulation of algorithms to solve problems, is too narrow a view of CT's scope.

4 Whether algorithms are only those that fit the strict definition from the theory of computing — or whether algorithms could also be more loosely defined.

5 Whether algorithms necessarily include an abstract machine in the background.

6 Whether algorithms are primarily directions for controlling machines — or are primarily means of expressing procedures.

7 Whether using computational tools teaches CT.

8 Whether carrying out daily step-by-step procedures is a manifestation of CT.

9 Whether CT is learned from practicing programming — or from well-designed learning activities that use steps and rules.

10 Whether learning CT in the context of computing transfers to problem-solving skills in other fields.

11 Whether CT is domain dependent — or is a meta-skill valid in all domains.

12 Whether computational processes are found in nature — or whether they are limited to algorithms and machines.

13 Whether information processing by computers differs from information processing done by humans — and whether「information processing agents」can include things such as molecules, DNA, or quarks.

14 Whether students' learning should be assessed from their demonstrating skill at designing computations — or from their knowledge of certain key concepts.

15 Whether satisfaction of customers with the job that software does should be part of the assessment of software success.

16 Whether K–12 CT education has to stick with strict definitions of computing — or could for pragmatic and pedagogical reasons take some liberties.

We have expressed our stance on these questions at various points throughout this book. We see CT as an old, rich human practice that has been perfected in the modern age of the electronic computer. We see CT as a mental discipline for thinking about designing computations of all kinds, a skill at the advanced levels honed and improved through extensive practice and experience. We see many different levels and styles of CT from basic computing skills and insights to highly advanced, specialized ones. We see that there are many good ways for teaching entry level CT. We see that ultimately nearly all CT will boil down to machine-realizability. We see CT as mostly domain dependent — for example, how you think about computation in biology is different from physics, chemistry, or humanities. We see as wishful the notion that CT is an innate human ability exercised daily by using computational tools and performing routine everyday procedures. We see the attempt to define algorithms as a set of possibly ambiguous steps resolved by human computers as a misunderstanding of computing.

We would like to point out one other movement to bring computing into K–12 schools. Known as CS Unplugged, [9] it seeks to teach computing concepts and practices through games, magic tricks, and activities. It was founded in the late 1990s by Tim Bell, Michael Fellows, and Ian Whitten. It has gained a worldwide following and influenced the design of the ACM K–12 and code.org curriculum recommendations.

In summary, we see plenty of room for a broad, pluralistic approach to teaching computational thinking while remaining faithful to computing's well-honed disciplinary ways of thinking and practicing. Most of all, we hope that all teachers of computing bring their students a good sense of the richness and beauty of the many dimensions of computation.

8 Denning (2017).

9 See [Computer Science Field Guide](https://csfieldguide.org.nz/en/) and [CS Unplugged](https://csunplugged.org/zh-hans/).

## References and Further Reading

Abelson, Harold, and Gerald J. Sussman. (1996). Structure and Interpretation of Computer Programs. 2nd edition. MIT Press.

Bolter, J. David. (1984). Turing's Man: Western Culture in the Computer Age. University of North Carolina Press.

Denning, Peter. (2017). Remaining trouble spots with computational thinking. Communications of the ACM 60 (6) (June): 33–39.

Guzdial, Mark. (2015). Learner-Centered Design of Computing Education: Research on Computing for Everyone. Synthesis Lectures on Human-Centered Informatics. Morgan & Claypool.

Kestenbaum, David. (2005). The challenges of IDC: What have we learned from our past? Communications of the ACM 48 (1): 35–38. [A conversation with Seymour Papert, Marvin Minsky, Alan Kay]

Knuth, Donald E. (1974). Computer science and its relation to mathematics. American Mathematical Monthly 81 (April): 323–343.

Lockwood, James, and Aidan Mooney. (2017). Computational Thinking in Education: Where Does It Fit? A Systematic Literary Review. Technical report, National University of Ireland Maynooth.

Minsky, Marvin. (1970). Form and content in computer science. Journal of the ACM 17 (2): 197–215.

Tedre, Matti, Simon, and Lauri Malmi. (2018). Changing aims of computing education: a historical survey. Computer Science Education, June.

Wing, Jeanette M. (2006). Computational thinking. Communications of the ACM 49 (3): 33–35.