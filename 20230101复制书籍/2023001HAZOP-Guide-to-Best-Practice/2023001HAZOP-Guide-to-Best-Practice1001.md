## 1001. Advanced Aspects of HAZOP Study

10.1 HAZOP STUDY OF COMPUTER-CONTROLLED PROCESSES

The use of computers to control chemical processes in part or in
entirety is now widespread, and many control devices contain some
form of programmable logic. The number of reported incidents21,22 in
such systems demonstrates their need for effective hazard study. The
introduction of computers has occurred since the original development
of the HAZOP study method and so the technique has had to be
adapted to cover such processes.
The reliability of PESs in safety-related applications is now covered
by international standards such as IEC 6150823 and 61511.14 In the
UK, the PES Guidelines4 give detailed advice and point out the many
types of problems that must be covered and give advice on how to
deal with them. As well as anticipating random hardware failures, it is
necessary to identify, and eliminate or minimize, systemic failures
including those due to:
errors or omissions in system specifications:
errors in design, manufacture, installation, or operation of hardware;
errors or omissions in software.
The specification and planning of a computer-controlled process is
normally examined during HS 2; the detailed search for undetected
errors and omissions occurs during HS 3.
Where safety-related systems are computer-controlled, they must be
designed, installed, operated, and maintained to the specified standard for
their purpose. The performance of the whole system must be demon-
strable, including all elements--from the sensors, through the logic proces-
sors, to the actuators and final process hardware elements such as valves.
HAZOP study has proved to be an effective method of critical
examination of computer-controlled systems. But first there must have
HAZOP: Guide to Best Practice. DOI: http:/dx.doi.org/10.1016/B978-0-323-39460-4.00010-4 Copyright 2015 Elsevier Ltd. All rights reserved. Advanced Aspects of HAZOP Study
63
been an earlier HS 2 to identify the key issues and set out design requirements. Then the HAZOP methodology must be adapted to bring out the computer-related problems as well as the conventional hardware and human factor problems-the recommended approaches are described here.
10.1.1 Hazard Study 2
The title "Safety and Operability Review"(SOR) has commonly been used for the study carried out on a computer-controlled system at the time of HS 2. This should be done at an early stage in the project definition and design stages, as described in Chapter 2, in order to highlight the main hazards and to identify critical safety functions. It is carried out by a small team that includes at least one expert on computer systems.
The team uses a checklist or a set of questions that will help to highlight the key issues-it is not, therefore, following the traditional HAZOP method. Key topics to be considered include:
safety critical protective functions;
interactions between control and protection systems;
the extent of hardwiring of controls, alarms, and trips;
the degree of redundancy and/or diversity required;
independence and common cause failures;
input/output (I/O)arrangements for the control system;
routing of data highways and their vulnerability;
. communication links and speeds;
.program storage method and the security;
positioning and security of the computer hardware;
likely consequences of system failure and of site power failure;
construction of screen pages and alarm displays to assist
troubleshooting.
Where significant hazards are present there will be a layered protec- tion system starting with alarms allowing operator intervention, then actions by the control computer and, ultimately, hardwired or software initiated actions through SISs or safety-related protection systems and demands on the passive protection such as relief valves or actions driven by an independent computer. 64
HAZOP: Guide to Best Practice
10.1.2 Functional Safety and IEC 61508
IEC 6150823 has implications for HAZOP study of computer- controlled processes. Its title has three key terms:
1. Functional safety-that part of the overall safety of the plant,
process, or piece of equipment that depends on a system or equip-
ment operating correctly in response to inputs.
2. The systems covered-any electric, electronic, or PES.
3. Safety-related-that is, systems that are required to perform a
specific function to ensure risks are kept at an acceptable level.
The requirements placed on a safety-related system depend firstly on its function. This will be determined during Hazard Studies 2 and 3 when possible hazardous conditions are identified. Then the perfor- mance required for this safety function must be determined by risk assessment. A key part of the IEC 61508 methodology is the establish- ment of SILs for each hazardous condition, giving the level of reliability required of the protective systems. These can then be specified to match the SIL requirement, and individual components specified accordingly.
The standard uses four SILs. SIL1, the least demanding, specifies a probability of failure on demand (PFD) for low-demand events of between 10-1 and 10-2； the PFD range decreases by an order of magnitude for each step up in the SIL rating. To achieve SIL 3 or 4 is very demanding, usually requiring a high-integrity protective system with multiple sensors and actuators, voting systems, diversity, and redundancy. This is difficult to design, prove, and maintain and so most systems in the chemical process industries tend to be designed to operate with protective systems up to, but not beyond, SIL2.
In order to ensure effective implementation of a safety-related system, it is important to consider it throughout the life cycle of the project and process, including: scope, specification, validation, installa- tion, commissioning, operation, maintenance, and modifications. IEC 61508 covers all these life cycle activities. This standard forms the basis for developing other standards for particular sectors of operations, including BS IEC 6151114 for the process industries.
It is essential that these systems are defined early in the project so that the detailed design can satisfy the overall design intentions and to ensure that all computer-controlled safety-related functions are clearly recognized. If a positive decision is taken to operate with computer-controlled safety-related functions, then very high standards Advanced Aspects of HAZOP Study
65
of design, proving, and maintenance will be required, and a Computer HAZOP (CHAZOP) study will almost certainly be necessary, to meet the reliability required by the Standards.
As well as meeting the required SIL, the systems should be designed to minimize demands on the protection systems from control failures, for example, by spurious trips. It is usual to address the requirements of the standard by having a combination of hardwired or passive protective devices while having the early warning alarms, initial actions, and duplicated safety actions passing through the control computer.
10.1.3 Enhanced HAZOP for Computer-Controlled Systems
The enhanced HAZOP extends the usual conventional HAZOP study to include aspects of the computer-controlled systems. It is suitable when the control system does not have safety-related functions and where the hazards are not exceptionally high and where there is a final level of hardwired protective devices.
The purpose of a conventional HAZOP is to consider possible deviations, using the full P&ID and other relevant design and operating information, and to single out for action those that have significant consequences not adequately controlled by the existing design. When a computer-controlled system is studied, the whole control loop from the field sensor through the logic solver and the final element must be con- sidered. There will also be additional deviations that are due to random failures within the computer hardware. These could be the system as a whole, an individual input and output board, or the operator consoles.
Attention must also be given to the control sequences, and these must be defined in sufficient detail for the exact operating sequence to be understood for each section or stage being reviewed. In addition, it is important to know what status checks are being made by the computer and what actions will be taken by the control system if a fault is detected. The team needs to review and question these actions for each stage.
For an enhanced HAzop. the information needed in addition to that normally used in a study of a conventionally controlled process includes: The specification of the computer hardware, the control language, and the programming method.
The QA checks for the software.
The signals from the plant instrumentation to the computer and the
computer outputs to controls, valves. alarms, etc. 66
HAZOP: Guide to Best Practice
The interface between the operators and the computer and the means of interaction allowed to the operators.
Which safety features are hardwired.
An outline of the control sequence on which the code will be based-probably as a logic diagram. Sufficient information is needed so that the intended progression is known and the response of the control system to a deviation can be evaluated.
The HAZoP follows the conventional method. but common differ-
ences encountered with computer-controlled systems include:
Guidewords: The usual set of guidewords should be used, but the sequence-related guidewords, such as sooner and later, and before and after, become important. Other possibilities are more or less often and interrupt.
Parameters and deviations: While considering only meaningful deviations, a sensible selection must be combined with lateral thinking and imaginative suggestions. A computer-controlled system could introduce new parameters such as data flow, data rate, and response time.
Causes: As well as the usual HAZOP causes, there may now be additional ones that originate in the computer system, such as the reli- ability of power supplies, the possibility of complete or partial hard- ware failure, plus the links and handover sequence. Human factors during interactions with the computer should also be considered.
Consequences and safeguards: The evaluation must ask what information is provided to the computer, how it will be interpreted, and how the control system will react. Again, the interaction between the operators and the computer system may enter the analysis.
It is helpful to ask four key questions when assessing a developing event:
Does the computer know?
What does the computer do?
Does it tell the operator?
What can/does the operator do?
Clearly the HAZOP study team must have sufficiently detailed know- ledge of the intended control and emergency sequences if an accurate evaluation of the consequences is to be made. The team should include both the person responsible for creating the control program and someone who understands the coding process to ensure that there is no uncertainty or ambiguity between the different disciplines involved. Advanced Aspects of HAZOP Study
67
Actions: Many actions will concern the draft control sequence, per-
haps to provide better control, more checks, further information for
the operators, or more alarms. These can benefit from the capacity
of a computer to carry out complex checks and actions with speed
and reliability. There may also be some actions to correct problems
of timing identified in the draft control sequence.
Reporting: The normal requirements for good reporting apply. In
particular, it is essential that all actions are written so those carry-
ing out the programming or coding will be clear what is required.
The report must be clear and meaningful to individuals who were
not part of the team, bearing in mind that the implementation will
rely not only on those versed in the usual engineering disciplines
but will now involve software specialists.
10.1.4 Computer HAZOP (CHAZOP)Study
This staged approach is recommended for complex control systems, when there are major hazards or when safety-related functions come under computer control. An enhanced HAZOP is usually carried out first but, if all the necessary information is available, the two studies may overlap. The timing of the second study can be a problem, in that the detailed coding may not be available until late in the overall development.
10.1.4.1 Detailed Study of Computer Hardware
Details of the second stage computer HAZOP are given in a Health and Safety Executive (HSE) Research Report, 2> and only a brief sum- mary is given here. If done in full, it is a very comprehensive review of the computer hardware and software. It is very time-consuming, espe- cially for batch processes, and therefore should only be used for high hazard activities or new or unusual processes.
All the normal plant documentation used for the first HAZOP study is needed as well as the detailed design specifications for control schemes and protective systems. For this study, the detailed design specifications for all the computer hardware will also be needed, including cabinet details, I/O configurations, alarm and trip schedules, communication links, watchdogs, backups, power supplies, security considerations, and provisions for software modifications. Many of these will have been identified by HS 2.
The team work through the computer system to build up a picture of how it is intended to work and what will happen if any element fails, 68
HAZOP: Guide to Best Practice
identifying all reasonable causes of failure both internal and external to the computer system. In many ways this parallels failure modes and effects analysis (FMEA), by considering all of the failure modes of the key elements in turn. The four key questions used in enhanced HAZOP (see above) will help the team to identify the adequacy of the required response.
This stage of the examination need not be lengthy if equivalent hardware has been considered before for other projects or if there is a consistent, standard policy over hardware, and there are common, tested subroutines in the computer code for actions that recur regularly.
10.1.4.2 Detailed HAZOP of Computer Sequences
This follows the conventional HAZOP method of using guidewords, but in this case it applies them to the steps of the control sequence and the computer actions. It is therefore most usually called a CHAZOP. It can obviously only be carried out when the sequence (but probably not the coding) has been fully developed. It can also be applied to the functional steps of a continuously acting control loop.
The sections or nodes for the HAZOP will follow the steps of the control sequence, and as usual a design intention will be built up for each node. But each design intention is now written from the point of view of the computer functions, for example, "Open Valve XSV0001" or "Sense level in Tank T0002."
The conventional HAZOP guidewords are then used to generate deviations such as nolmorelless signal or nolmorelless/reverse driven, high/low/bad signal, input other than expected, soonerllater valve move- ment, etc. As always, the team needs to use all the guidewords creatively to create meaningful deviations.
The guideword other can be used to include global effects on the computer system such power failures or environmental impacts, if these have not already been picked up under the earlier guidewords. It can also include key overrides of functions and MOC in control logic, and the important security issues associated with both of these.
For each meaningful deviation, the team then looks for realistic causes and examines the possible consequences, following the con- ventional HAZOP structure. For significant consequences, the safe- guards are identified, and again the four key questions will help the team confirm if these are adequate. The result will be a sequence which Advanced Aspects of HAZOP Study
69
has been reviewed systematically for possible deviations at each stage, and therefore will be better able to deal with problems when in opera- tion, neither being unable to recognize what is happening, nor getting stuck in some loop in its internal logic.
For a batch system, this depth of study is very time-consuming but it reflects the fact that the system has to cope with many different circum- stances, each providing opportunities for failure or having different consequences that may not have been identified elsewhere. But, despite the time involved, this method has been demonstrated to provide a thorough way of identifying potential problems in the logic and the components of the computer system.
10.2 HUMAN FACTORS
The purpose of a HAZOP study is to examine possible deviations from the design intention, to find any previously unconsidered causes of deviations, evaluate their potential consequences, and to then review the relevant safeguards before suggesting appropriate actions. Each of these steps may involve people. This may occur through an error that contributes to a hazardous event or reduces the reliability of a control measure that is intended either to prevent the hazard or limit the consequences. Thus, it is essential that team members take account of human behavior and have a realistic understanding of typical human performance in both normal and abnormal conditions. There are several useful documents26-28 relating humans and risk. They give many exam- ples of both large and small incidents where human factors played a significant role, describe the main types of human error and how human behavior relates to these. and include guidance on ways to minimize such errors. Indeed, one approach to the management of human failures is described as a "human-HAZOP." There is no doubt that the regu- lator attaches importance to the qualitative assessment of human fail- ure, backed up where necessary by quantitative assessment. Also there is emphasis on the need to evaluate low-frequency high-consequence events adequately since experience has shown that major process safety incidents are often triggered by human error and organizational failures. This section is intended to provide basic guidance on the human aspects that should be considered in a HAZOP study.
Human behavior falls into three broad patterns. For much of the time, humans operate in a skill-based mode, carrying out familiar tasks and actions without having to think consciously about them. This will 70
HAZOP: Guide to Best Practice
apply in many industrial operations once they become familiar. For non- standard or less familiar tasks, humans move to a rule-based mode-using the available information and trying out a response that seems to fit or has worked in the past. Finally, if nothing easier has worked, they move to a knowledge-based mode, seeking further information and trying to find an explanation that will allow a suitable response. Each of these modes is associated with particular types of error. A HAZOP study team needs to be alert to the possibilities of these errors causing or contributing to unwanted outcomes. The team must try to anticipate possible slips, lapses, mistakes, and deliberate violations.
It should be recognized that errors do not occur because people are stupid or incompetent but as a result of fundamental limitations of human performance that are influenced by equipment design features and opera- tional conditions. An HSE guide26 identifies three contributing aspects- the individual, the job, and the organization. The individual's competence involves skills, personality, attitudes, and risk perception. The job covers the task, workload, environment, display and controls, and procedures. Finally, the organization can affect outcomes through culture, leadership, resources. and communications. However. even accounting for these. it should be recognized that the possibility of human error cannot be absolutely eliminated by training and procedures-these are not adequate control measures for human fallibility.
When carrying out a routine procedure, an operator will mostly work in the skill-based mode. The likely errors here are slips or lapses. It may be that there is an array of buttons, labeled A-E. to operate similar valves on different vessels. Pressing C when it should be B would be a slip. How easily this might occur will depend on many fac- tors such as the layout and design of the control panel (e.g., where equipment elements from different suppliers have different operating controls or philosophies)as well as external influences such as time pressure and fatigue. The consequence could vary from a trivial loss of material to causing a catastrophic runaway reaction. Clearly this is a cause that the HAZOP team should consider. A lapse might happen in a multistep start-up procedure where, say, after completing step 13 the operator is distracted by a phone call or has to briefly attend to another task. Returning to the sequence it is resumed at step 15 and thereby step 14 is omitted. This may have a trivial consequence; it may be recoverable; but it should be considered by the HAZOP team whenever the consequences matter. Advanced Aspects of HAZOP Study
71
The next level of operation in the hierarchy is rule based. When an uncommon event occurs. humans take the available information to see if it fits some previously experienced or learned rule. The sequence followed is "if the symptoms are X then the problem is Y; if the pro- blem is Y then do Z." More than one rule may be tried if the first does not work. If no rule works. then the knowledge-based mode must be tried. New data must be sought and an attempt made to model the pro- cess and use this to select the best actions, improvising in an unfamiliar and possibly critical situation. Not surprisingly mistakes are more likely in these modes. If the knowledge-based mode is called for in a complex system, especially in a critical situation where individuals are highly stressed, the likelihood of successful control and recovery is very low. The HAZOP team must recognize that people under pressure are sus- ceptible to predictable errors due to natural biases within the human cognitive system. People are very bad at recognizing new situations and will tend to jump to hypotheses based on more familiar situations. This can mean that operators will be slow to react to a potentially hazardous mode of operation and assume that the system will, as it usually does. operate safely. People will even try to rationalize weak signals of failure to explain away potential problems; they may even focus inappro- priately on evidence that appears to support their assumptions rather than acknowledge that they may be witnessing a new problem.
An example of these modes of behavior-skill based. rule based. and knowledge based-would be a control room operator realizing that during a routine transfer between vessels that the connecting line instrumentation shows a rising pressure -a skill-based level of opera- tion. Applying experience the first rule might be that a valve is closed in the transfer line and this would be immediately checked. If the valve is found to be open, then there is no other obvious cause. With the pressure still rising, further information and a new model are needed. This material has a high melting point-if the operator knows this, then a line blockage may be suspected and then appropriate actions can be tried. Again, knowledge and experience are crucial to raising the chance of a successful intervention.
Finally, the HAZOP team should be alert to possible violations (i.e., deliberate breaches of rules and procedures). There are many possible reasons why violations may occur. It could be to save time, to make the work physically easier, because it simplifies a procedure or seems more efficient. If done during normal, everyday operations, 72
HAZOP: Guide to best practice
deliberate violations may play a part in eroding safety margins. Where shortcuts in maintenance and calibration tasks, for example, are con- doned as accepted practice, the reliability of designed safety measures can be reduced and may one day lead to a major incident. These vio- lations are most likely to take place if employees have the perception that management want corners cut to save time or to achieve the production schedule. Good design of plant and procedures, involve- ment and education of the operators as well as good management and supervision reduce the likelihood of routine violations, although in an emergency it is possible that irregular steps will be tried.
Within HAZOP study, it is often necessary to assess the likelihood of event frequency. This is usually done by experienced judgment, occasion- ally by semiquantitative assessment and, rarely, by referral for QRA. These approaches can also be applied to human error. For relatively frequent events, an experience-based approach will work. Estimates may also be derived by task analysis methods using a quantitative Human Reliability methodology but this takes considerable effort and requires considerable expertise. At the intermediate level of estimation. there are some helpful observations from within the nuclear industry,29 and it is useful if the team leader or at least one member of the team has know- ledge of these documents. They suggest that there is no task, however simple, for which the failure rate is zero. For the simplest task listed, the selection of a key switch operation rather than a non-key one, the quoted error rate is 1 in 104-this implies that no task is error free. So a study team should never assume that a problem can be eliminated completely by an action that relies entirely upon an operator. At the other extreme, for example, the high-stress situation of large loss of coolant in a nuclear reactor, the probability for "operator fails to act correctly in the first 60 s" is 1. That is it should be assumed that there is no chance at all of correct remedial actions in that time. The situation does not improve greatly over the next 5 min and is not negligible several hours later. Another source of human error can occur at a shift handover where communication and records of previous actions may be poor and an error rate of 1 in 10 is quoted for "personnel on different work shift failing to check the condition of the hardware unless required by checklist."
While these are useful guidelines. it is important to recognize the many other factors that influence human error rates. A comprehensive set of performance-influencing factors(PIFs) has been established.30 These include training, control panel design, competence and Advanced Aspects of HAZOP Study
73
motivation, environment, level of demand and suddenness of onset of events, management attitude to safety, procedures, and communica- tions. There are many more. Understanding these may influence a HAZOP team's suggestions for action. In a modern computer- controlled plant, it can be easy to add an alarm but if this is to be done it must be within the overall design of the alarm and trip system so that the operator is not subjected to alarm and/or mental overload when a major event occurs. When an individual is overloaded with information, they are less likely to separate the critical, top-level information from the unimportant and the trivial, resulting in either inaction or the wrong action. Another state is mind set where the individual uses the information to create an initial, but erroneous, scenario and rejects critical information which shows it to be incorrect.
The HSE document, Identifying Human Failures,31 gives a list (in the following table)of failure types in the form of HAZOP style guidewords which may be used in the search for human error leading to a deviation. Action errors
Checking errors
A1: Operation too long/short
C1: Check omitted
A2: Operation mistimed
C2: Check incomplete
A3: Operation in wrong direction
C3: Right check on wrong object
A4: Operation too little/too much
C4: Wrong check on right object
A5: Operation too fast/too slow
C5: Check too early/too late
A6:Misalign
A7: Right operation on wrong object
Information retrieval errors
A8: Wrong operation on right object
R1: Information not obtained
A9: Operation omitted
R2: Wrong information obtained
A10: Operation incomplete
R3: Information retrieval incomplete
A11: Operation too early/too late
R4: Information incorrectly interpreted Selection errors
Information communication errors
S1: Selection omitted
I1: Information not communicated
S2: Wrong selection made
I2: Wrong information communicated
I3: Information communication
incomplete
Violations
I4: Information communication
unclear
V1: Deliberate actions 74
HAZOP: Guide to best practice
A HAZOP study team would seldom find it necessary to systemati- cally examine all of these possible deviations. In many operations and procedures, the use of appropriate guidewords, which may be problem specific, will help the team decide which of the possible deviations could lead to potential problems. It is unlikely that all of these devia- tions would be found using just the conventional combinations of guidewords and parameters.
The example of a HAZOP study of a procedure (Appendix 5)shows some of the ways that human factors may be identified by the team.
In summary, all HAZOP study teams need to be aware of the potential for human error to generate causes and to influence con- sequences. They need to use the present understanding of human behavior, influencing factors, and the typical probabilities for different types of error. It is also good practice to examine the design of control screens from the perspective of the operator. This will reveal design inadequacies such as when separate elements that should be monitored as part of a routine task are actually presented on separate screens. Such arrangements add workload and complexity and introduce opportunities for confusion and error. In formulating actions, they should consider the required level of human behavior--the skill-based. the rule-based. or the knowledge-based mode-and the actions should reflect the needs for further diagnostics, training, second line of super- vision, or simply an addition in a standard operating procedure(SOP) as illustrated in Appendix 5.
10.3 LINKING HAZOP STUDIES TO LOPA
Layer of protection analysis -LOPA-is a widely used technique to determine the level of protection needed to provide adequate safeguards against major hazards that could arise on a plant or pro- cess. The method, developed in the early 1990s, is well documented32 and is accepted by regulators in many countries as an appropriate method of analyzing identified hazards and assessing if sufficient protective systems are in place to achieve a tolerable risk.33 The first step in LOPA is the classification of the severity of hazard con- sequences if this has not already been carried out by a Hazard Identification process such as HAZOP. For the major consequences such as injury, fatality, or major accident to the environment, the Advanced Aspects of HAZOP Study
75
magnitude of the ultimate, unmitigated consequences (a scenario) is estimated. then a maximum tolerable frequency is assigned from either the company standards or from publically available suggested levels.33 The frequency of the initiating cause(s) is estimated using either a generic value for this type of event such as control system failure or human error or, preferably, by fault tree analysis of the expected sequence for the individual event. Other factors such as "time at risk" for hazards which exist for part of the time and "conditional modifiers"" such as probability of ignition are considered. It is then possible, taking into account all independent protection layers, to estimate the frequency of occurrence of the scenario. that is. the frequency of the top event. Comparison with the target tolerable frequency shows whether the protection is adequate and, if not, the magnitude of the necessary improvements. Where instrumented safety systems are used, their reliability (PFD) is often expressed as an SIL. The further measures to achieve a tolerable frequency may include addition of an SIS -a system designed and evaluated from sensor through control loop to actua- tors -to have a demonstrable PFD at levels such as SIL1 (a PFD between 1% and 10%) or SIL2 (a PFD between 0.1% and 1%). LOPA may be used as a part of HS 2 to ensure that the PFD of each SIS can be covered in the detailed design. Alternatively, or additionally, it can follow HS 3, especially where this involves a full HAZOP study.
As the prime aim of HAZOP study is the identification of hazardous events and evaluation of the consequences. it can clearly link to a LOPA study. since it produces deviations, causes, consequences, and safeguards which feed directly into LOPA. To realize the potential of this link. it is important that the team fully evaluate and record in detail the consequences for each cause of each deviation as well as the safeguards already present in the design. Thus, any possibility of severe injuries or fatalities, of major fire, explosion and toxic releases, or of substantial plant damage and disruption, need to be recorded in the consequence column of the HAZOP report. This highlights scenarios that should be included in the LOPA study. An additional useful item is the teams' view of the likely frequency of the event.
Two outcomes are common during the HAZOP study. If the scenario has already been considered at the hs 2 stage. then the team can immediately review the design and recommended safeguards to confirm their adequacy. If the scenario is new then, as a potential 76
HAZOP: Guide to Best Practice
major event, it will need to be examined using the LOPA method- ology. This requires a LOPA study to follow the HAZOP study either as a resumption of the earlier one or a new study. To be effective the HAZOP team must be on the lookout for potential major con- sequences, even when these are anticipated to be very-low-frequency events. The ultimate consequence should be clearly recorded so that when the records are reviewed they stand out as needing review in the LOPA study. All possible causes should be recorded as these are essential inputs to the LOPA study. Similarly, the existing safeguards should be clearly recorded as they may serve as independent layers of protection against a developing event.
Thus, LOPA and HAZOP study are natural partners in identifying hazards, determining whether existing safeguards are adequate and, if not, specifying the additional levels of protection that are needed for each possible cause of the event. However, if the full benefits are to be realized, it is essential that the HAZOP study has been planned to provide optimal information for the LOPA study. 