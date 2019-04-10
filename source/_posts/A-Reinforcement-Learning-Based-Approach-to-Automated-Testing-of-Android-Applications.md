---
title: >-
  A Reinforcement Learning Based Approach to Automated Testing of Android
  Applications
date: 2019-04-10 21:31:37
tags:
categories:
---

# Abstract

近年来，研究人员积极提出了自动化Android应用程序测试的工具。然而，他们的技术仍然遇到重大困难。首先是实现高代码覆盖率的困难，因为应用程序通常有大量的业务和转换的可能的组合，这使得在测试大型系统场景时会非常的耗时和无效。其次是实现广泛的应用功能的困难，因为某些功能只能通过特定的事件序列来实现。因此，在随机测试中，它们的测试频率较低。面对这些问题，我们应用称为Q学习的强化学习算法，以利用随机和基于模型的测试。 Q-learning代理与Android应用程序交互，逐步构建行为模型并基于模型生成测试用例。代理以最佳方式探索应用程序，尽可能多地显示应用程序的功能。与随机和基于模型的测试相比，使用Q学习的探索提高了代码覆盖率，并且能够检测被测应用程序中的故障

KEYWORDS：Android, Test Input Generation, Reinforcement Learning, Q-Learning 

| relevant information |                                                              |
| -------------------- | ------------------------------------------------------------ |
| *作者*               | Thi Anh Tuyet Vuong，<br/>Shingo Takada                      |
| *单位*               | Grad. School of Science and Technology, Keio University Yokohama, Japan<br/>Grad. School of Science and Technology, Keio University Yokohama, Japan |
| *出处*               | A-TEST ’18                                                   |
| *原文地址*           |                                                              |
| *源码地址*           |                                                              |
| *发表时间*           | 2018年                                                       |

# 1. 引言

近年来，全球范围内移动软件的经济增长导致了开发人员对有效测试工具的持续需求。作为对这种需求的回应，研究人员提出了一种不同的工具，可以用尽可能少的人力来自动测试移动应用程序。大多数研究人员选择Android平台来开发他们的工具，因为Android手机的市场份额很大，Android测试工具无疑是有用的，并且与许多开发人员相关。此外，Android平台的开源特性使研究人员更容易访问应用程序和底层操作系统[11]。我们针对Android平台并针对Android应用程序开发测试工具的原因相同。

Android应用程序由一个或多个``activities`组成，这些activities是负责应用程序用户界面（UI）的组件。每个activities都包含各种UI组件，如按钮，文本，复选框等。Android应用程序是基于事件的，这意味着它的行为基于对用户输入事件（UI事件）的响应，如单击，滚动，文本输入它还对来自手机操作系统的系统事件做出反应，如电话呼叫或短信信号等。由于Android应用程序基于事件的特性，相当多的研究都集中在自动生成输入事件以进行测试。无论采用何种技术，目标都是生成相关输入，以尽可能多地显示应用程序的功能。然而，这个领域的研究人员仍面临两个主要挑战：

- 移动应用程序通常包含大量组件和可执行的事件。因此，测试组件和事件的所有可能组合是耗时的，并且难以扩展到大型系统。自动测试工具应仅测试与应用程序相关的事件序列，即导致测试应用程序功能的序列。
- •应用程序的某些功能只能通过特定的事件序列（难以到达的功能）来实现，这使得自动随机测试难以显示和测试它们。

本文的主要贡献是提出强化学习的应用，特别是Q学习，以自动生成Android应用程序的测试输入。使用强化学习，我们构建了一个测试工具，以试错法的方式交互和探索应用程序的功能。在此探索过程中，该工具动态构建应用程序的行为模型，并生成遵循最有可能揭示应用程序功能的事件序列的测试用例。本文还展示了与最先进的自动化测试工具相比较的工具评估。

 本文的结构如下：第2节回顾了Android测试技术的相关工作;第3节介绍Q学习，然后第4节解释了Q-Learning工具的提议方法和实现细节;第5节讨论了对拟议工具的评估，最后第6节总结了论文以及对未来工作的建议。