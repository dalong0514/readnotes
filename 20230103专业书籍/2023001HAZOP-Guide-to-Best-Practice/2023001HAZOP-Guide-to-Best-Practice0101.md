## 0101. Introduction

### 1.1 Aims and Objectives 

This book is intended to provide guidance on a specific technique developed for use in the process and chemical industries. The technique described is HAZOP (hazard and operability) study, a detailed method for systematic examination of a well-defined process or operation, either planned or existing.

The HAZOP study method was developed by ICI in the 1960s and its use and development was encouraged by the Chemical Industries Association (CIA) Guide published in 1977. Since then, it has become the technique of choice for many of those involved in the design of new processes and operations. In addition to its power in identifying safety, health, and environmental (SHE) hazards, a HAZOP study can also be used to search for potential operating problems. Not surprisingly, the method has been applied in many different ways within the process industries.1 

While it is frequently used on new facilities, it is now often applied to existing facilities and modifications. It has also been successfully applied to process documentation, pilot plant, and hazardous laboratory operations as well as tasks such as commissioning and decommissioning, emergency operations, and incident investigation.

The objective here is to describe and illustrate the HAZOP study method, showing a variety of uses and some of the approaches that have been successful within the process industry. An important input has come from European Process Safety Centre (EPSC) members where 22 member companies responded in a survey carried out prior to the first edition of this Guide (2000). This identified many features generally regarded as essential to a good study. In addition, many common variations were described. These variations are in part due to the range of problems encountered within industry but also reflect individual choices of style. HAZOP study is a versatile technique and good results may be achieved by several different approaches provided the basic principles are followed. It is hoped that this Guide will help maintain a high standard for HAZOP study within the industry, both by raising quality and encouraging flexibility without putting any unnecessary constraints upon its use and development.

The HAZOP study method is well developed and is useful in most applications. There are other methods, however, that may have to be considered depending on the complexity and hazards of the installation being constructed and the state of the design. This publication does not address these methods in detail but their importance is discussed in Chapter 2. A fuller account is given in the IChemE Guide, Hazard Identification Methods.2 

Finally, three illustrations of process industry applications are given in Appendices 3, 4 and 5. These examples cannot fully represent all the possible applications and process industries and readers new to HAZOP study are advised to consult the reference list, 3-6 the International Electrotechnical Commission (IEC) standard, 7 or guidelines written specifically for other industries.

It is hoped that this guide will help people within the process industries, including all those with responsibilities within safety management systems. Although it is primarily written for HAZOP study leaders, scribes, and members, it may also be of use to those involved in training and plant management.

1.1 研究目的与目标

本书旨在为一种在流程工业和化工行业中广泛应用的特定技术提供指导。这种技术被称为 HAZOP（Hazard and Operability）研究，即危险和可操作性研究，是一种用于系统性审查已明确定义的流程或操作（无论是在规划阶段还是已经存在的）的详细方法。

HAZOP 研究方法最初由英国帝国化学工业公司（Imperial Chemical Industries，ICI）在 20 世纪 60 年代开发，随后在 1977 年发布的英国化学工业协会（Chemical Industries Association，CIA）指南的推动下得到了进一步的使用和发展。从那时起，它已成为许多参与新工艺和操作设计的专业人员的首选技术。HAZOP 研究不仅在识别安全、健康和环境（SHE）危险方面表现出色，还可用于发现潜在的操作问题。因此，这种方法已在流程工业中得到了广泛而多样的应用 [1]。

尽管 HAZOP 研究最初主要用于新建设施，但如今它也经常应用于现有设施的评估和改造。此外，这种方法还被成功地应用到了过程文档编制、试验工厂运行和危险实验室操作等领域，甚至扩展到了调试、退役、应急操作和事故调查等任务中。

本文旨在介绍和阐述危害与可操作性分析（HAZOP）研究方法，展示其在过程工业中的多种应用和一些成功的实践方法。在编写本指南第一版（2000 年）之前，我们进行了一项调查，其中欧洲过程安全中心（EPSC）的 22 家成员公司提供了宝贵的反馈。这些反馈帮助我们确定了许多被普遍认为是高质量研究所必需的关键特征。同时，我们也发现了许多常见的变化形式。这些变化一方面源于工业界面临的各种问题，另一方面也反映了个人的工作风格偏好。

HAZOP 研究是一种灵活多样的技术。只要遵循基本原则，通过不同的方法都可以取得良好的效果。我们希望本指南能够通过提高研究质量和鼓励灵活应用，帮助保持行业内 HAZOP 研究的高标准。同时，我们也注意避免对其使用和发展施加任何不必要的限制。

虽然 HAZOP 研究方法已经相当成熟，并且在大多数情况下都很实用，但在某些情况下，我们可能需要考虑其他方法。这主要取决于正在建造的装置的复杂程度和潜在危险，以及设计的阶段。虽然本文不会详细讨论这些其他方法，但我们会在第 2 章中探讨它们的重要性。如果您想了解更多相关信息，可以参考英国化学工程师协会（IChemE）出版的《危害识别方法》2 指南，其中有更全面的说明。

最后，附录 3、4 和 5 给出了三个流程工业应用的实例。这些例子无法完全涵盖所有可能的应用和流程工业类型。对于刚接触 HAZOP（危险与可操作性）研究的读者，建议参考文献列表 [3-6]、国际电工委员会（IEC）标准 [7]，或其他行业专用指南来获取更多信息。

我们希望本指南能够为流程工业内的各类人员提供帮助，特别是那些在安全管理系统中承担责任的人。虽然本指南主要面向 HAZOP 研究的组长、记录员和团队成员，但也可能对参与培训和工厂管理的人员有所裨益。

### 1.2 Essential Features Of HAZOP Study 

A HAZOP study is a structured analysis of a system, process, or operation for which detailed design information is available, carried out by a multidisciplinary team. The team proceeds on a line-by-line or stage-by-stage examination of a firm design for the process or operation. While being systematic and rigorous, the analysis also aims to be open and creative. This is done by using a set of guidewords in combination with the system parameters to seek meaningful deviations from the design intention. A meaningful deviation is one that is physically possible—for example, no flow, high pressure, or reverse reaction. Deviations such as no temperature or reverse viscosity have no sensible, physical meaning and are not considered. The team concentrates on those deviations that could lead to potential hazards to safety, health, or the environment. It is important to distinguish between the terms hazard and risk. They have been defined 8 as follows: a “hazard” is a physical situation with the potential for human injury, damage to property, damage to the environment, or a combination of these. A “risk” is the likelihood of a specified undesirable event occurring within a specified period or in specified circumstances. It can also be expressed as a combination of likelihood and severity, as illustrated in Figure 1.1.

Figure 1.1 Illustrative risk graph.

In addition to the identification of hazards, it is common practice for the team to search for potential operating problems. These may concern security, human factors, quality, financial loss, or design defects.

Where causes of a deviation are found, the team evaluates the consequences using experience and judgment. If the existing safeguards are adjudged to be inadequate, then the team recommends an action for change or calls for further investigation of the problem. The consequences and related actions may be risk-ranked. The analysis is recorded and presented as a written report which is used in the implementation of the actions.

To avoid misunderstanding and confusion with other forms of process hazard study or project hazard review, the term HAZOP study is reserved for studies which include the essential features outlined earlier in this section. Descriptions such as “coarse scale HAZOP” or “checklist HAZOP” should be avoided.

1.2 HAZOP 研究的核心特征

HAZOP（危害与可操作性分析）研究是一种结构化的分析方法，适用于已有详细设计信息的系统、过程或操作，由多学科团队共同执行。分析团队对既定的过程或操作设计进行逐行或逐阶段的细致检查。尽管这种分析方法系统严谨，但同时也注重开放性和创新性。分析过程中，团队使用一套特定的引导词（guidewords）结合系统参数，寻找与原始设计意图的显著偏差。这里的「显著偏差」指的是物理上可能发生的情况 —— 例如，流量为零、压力过高或反应逆向进行等。而诸如温度为零或粘度反向这类在物理上没有实际意义的偏差则不在考虑范围内。分析团队主要关注那些可能导致安全、健康或环境方面潜在危害的偏差。

在这个过程中，区分「危害」和「风险」这两个概念非常重要。根据定义 [8]：

「危害」是指一种可能对人类造成伤害、导致财产损失、破坏环境或造成这些后果的组合的物理情况。

「风险」则是指在特定时期内或特定情况下，发生某种不良事件的可能性。风险也可以表示为事件发生的可能性与其后果严重程度的组合，如图 1.1 所示。

图 1.1：风险图示例

除了识别潜在危害，团队通常还会寻找可能出现的操作问题。这些问题可能涉及多个方面，包括安防、人为因素、质量控制、财务损失或设计缺陷等。

当团队发现导致偏离正常操作的原因时，他们会根据经验和判断来评估可能造成的后果。如果现有的防护措施被认为不足以应对这些后果，团队就会建议进行相应的改变或呼吁对问题展开更深入的调查。这些后果及相关的应对行动可能会根据风险程度进行排序。整个分析过程都会被记录下来，并以书面报告的形式呈现，这份报告将用于指导后续行动的实施。

为了避免与其他类型的过程危害研究或项目危害审查混淆，「HAZOP 研究」（危害与可操作性分析，Hazard and Operability Study）这一术语专门用于指代包含了本节前面概述的基本特征的研究。应当避免使用诸如「粗略 HAZOP」或「清单 HAZOP」之类的描述，以免引起误解。