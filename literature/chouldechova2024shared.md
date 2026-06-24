                                                      A Shared Standard for Valid Measurement
                                                             of Generative AI Systems’
                                                          Capabilities, Risks, and Impacts


                                            Alexandra Chouldechova∗ Chad Atalla Solon Barocas A. Feder Cooper Emily Corvi
                                                   P. Alex Dow Jean Garcia-Gathright Nicholas Pangakis Stefanie Reed
arXiv:2412.01934v1 [cs.CY] 2 Dec 2024




                                               Emily Sheng Dan Vann Matthew Vogel Hannah Washington Hanna Wallach
                                                                           Microsoft Research

                                                                                         Abstract
                                                     The valid measurement of generative AI (GenAI) systems’ capabilities, risks, and
                                                     impacts forms the bedrock of our ability to evaluate these systems. We introduce
                                                     a shared standard for valid measurement that helps place many of the disparate-
                                                     seeming evaluation practices in use today on a common footing. Our framework,
                                                     grounded in measurement theory from the social sciences, extends the work of
                                                     Adcock and Collier [1] in which the authors formalized valid measurement of con-
                                                     cepts in political science via three processes: systematizing background concepts,
                                                     operationalizing systematized concepts via annotation procedures, and applying
                                                     those procedures to instances. We argue that valid measurement of GenAI systems’
                                                     capabilities, risks, and impacts, further requires systematizing, operationalizing,
                                                     and applying not only the entailed concepts, but also the contexts of interest and the
                                                     metrics used. This involves both descriptive reasoning about particular instances
                                                     and inferential reasoning about underlying populations, which is the purview of
                                                     statistics. By placing many disparate-seeming GenAI evaluation practices on a
                                                     common footing, our framework enables individual evaluations to be better under-
                                                     stood, interrogated for reliability and validity, and meaningfully compared. This is
                                                     an important step in advancing GenAI evaluation practices toward more formalized
                                                     and theoretically grounded processes—i.e., toward a science of GenAI evaluations.

                                        1        Introduction
                                        Whether we are interested in what a generative (GenAI) system is capable of, the risks it poses, or the
                                        impacts of its deployment, we can gain insight into such inquiries by framing them as measurement
                                        tasks of the form: measure the [amount] of a [concept] in [instances] from a [population]. Examples
                                        include evaluating an LLM-based tutoring system’s mathematical reasoning capabilities by measuring
                                        its average (amount) performance (concept) on standardized test questions (instances) from the
                                        Korean CSAT Math Exam (population); or evaluating the risks posed by a conversational search
                                        system by measuring the prevalence (amount) of stereotyping (concept) in the system’s outputs
                                        (instances) in the current US deployment (population). This template is also sufficiently expressive
                                        to capture many of the impact evaluation tasks described by Solaiman et al. [19]. Recent work has
                                        emphasized the need, when carrying out such measurement tasks, to precisely articulate what is being
                                        measured—i.e., to formalize the concept of interest. This includes critical work on dataset diversity
                                        [21], benchmark design for stereotyping and other concepts [2, 11], and model memorization [3, 4, 9].
                                        These critiques parallel those made two decades ago by Adcock and Collier [1], who argued that
                                        political scientists were devoting insufficient attention to measurement validity—i.e., the question of
                                        whether researchers’ reported measurements adequately reflect the concepts they purport to measure.
                                        To facilitate this type of reflection, Adcock & Collier introduced a four-level framework that
                                             ∗
                                                 Corresponding author: alexandrac@microsoft.com


                                        NeurIPS 2024 Workshop on Statistical Foundations of LLMs and Foundation Models (SFLLM).
formalizes the relationship between a concept of interest and reported measurements for that concept
as a structured progression from a background concept (the set of meanings and understandings
associated with the concept), to a systematized concept (precise definitions), to annotation procedures
(procedures for labeling or scoring instances) that operationalize the systematized concept, to the
application of those procedures to obtain scores or labels for one or more instances. Validity concerns
about concepts then arise as slippage between these four levels, such as a failure of the annotation
procedures to capture relevant dimensions of the systematized concept. Using this framework, the
above-mentioned critiques of GenAI evaluations can be posed as failures to systematize nebulous
background concepts (e.g., stereotyping) before jumping to operationalization via annotation
procedures (e.g., instructions that ask crowdworkers to label system outputs as stereotyping or not).

2   Framework Overview
Although we wholeheartedly agree with these critiques, we argue that equal attention should be paid
to validity concerns that arise from the under-specification of amounts, populations, and instances
entailed in such measurement tasks. In other words, valid measurement of GenAI systems’ capabili-
ties, risks, and impacts requires systematizing, operationalizing, and applying not only concepts, but
also amounts, populations, and instances. This involves both descriptive reasoning about particular
instances and inferential reasoning about underlying populations, which is the purview of statistics.
To facilitate reflection on such validity concerns, we introduce an extension of Adcock and Collier’s
framework [1]. A graphical representation of this framework is depicted in Figure 1. We developed
and iteratively refined the framework using numerous examples of GenAI and non-generative AI sys-
tems’ capabilities, risks, and impacts, including topic modeling, representational harm measurement
for multi-modal models, face verification technologies, automated speech recognition, and others.
Like Adcock & Collier’s framework, our framework includes processes, depicted as backward arrows,
for revising and refining earlier levels based on findings, including validity concerns, that arise in
later levels. These revision and refinement processes operate not only within each column (e.g.,
within the “Concept” column, which is adapted from Adcock & Collier’s framework), but also across
the columns. We may find, for example, that the variance of our measurements is too high, leading
us to revise the sampling design or even the annotation procedures to improve estimator stability.
To better understand the elements of our framework, consider the example of measuring stereotyping
in a conversational search system. How we represent an instance (e.g., as a system output vs. as
a system output and its corresponding input) may influence whether a system output is labeled
as stereotyping. Likewise, if we are interested in the prevalence of stereotyping under typical use
post-deployment, but our sampling design (operationalized population) is based on adversarial red
teaming, we are likely to vastly overestimate the prevalence. By structuring the choice of metric
as first defining a target parameter (systematized amount) that is then estimated using statistical
estimators (operationalized amount), we can apply established statistical inference methods to
optimally trade off between bias and variance, adjust for sample bias in the data set (i.e., correct
for mismatches between the systematized population and the sampling design), construct uncertainty
intervals, and perform hypothesis tests. In Figure 2, we provide a high-level example of using
our framework to measure stereotyping in a hypothetical conversational search engine, ChatSearch.

3   Limitations and Future Work
Although our framework brings structure to the question of what should be done when measuring
GenAI systems’ capabilities, risks, and impacts, we offer no guidance on how to accomplish such
measurement tasks. This limitation therefore remains an important direction to explore in future work.
A major limitation of the framework itself is that it does not help with formulating measurement
tasks in the first place, nor does it offer guidance on how to interpret resulting measurements or
what decisions those measurements can or should inform. Just as the initial problem formulation
can have a big effect on the fairness of an ML model [10, 15–17, 20] or the conclusions drawn about
deep-learning optimizer performance [5, 8, 14], what we choose to measure, in what population, and
how we quantify it matters a great deal [6, 7, 13]. The revision and refinement processes provide one
mechanism for revisiting these decisions, but this falls well short of addressing the full complexity of
formulating measurement tasks—an issue that is critically important to evaluations of GenAI systems.


                                                   2
WIDER BIGGER FONT
 Task: measure the [amount] of a [concept] in [instances] from a [population]
            Concept*                          Instance                     Population                          Amount
     Background Concept                 Background Instance            Background Population            Background Amount
  “The broad constellation of        The unit of the [Background     General description of the     The desired quantifier of the
  meanings and                       Population]. This defines       setting we want our            amount, extent, and/or
  understandings associated          what a row of our data set      measurements to reflect.       distribution of the
  with [the] concept.”               represents.                                                    [Background Concept] in
                                                                                                    the [Background
                                                                                                    Population].




                                                                                                                                        Refinement
                                                                                                                                        Revision &
                                                       Systematization**
      Formulating a systematized [element] through reasoning about the background [element] in light of the evaluation goals.

    Systematized Concept               Systematized Instance          Systematized Population           Target Parameter(s)
  An explicit definition of the      Description of the metadata     The types of [Background       Mathematical expression(s)
  concept: The specific              & features recorded for         Instances] we interested in.   defining a target quantity in
  formulation of the concept         each instance—what we           This is the population we      terms of the [Systematized
  to be used in the task.            want the columns of our         want our measurements to       Concept] and
                                     data set to represent.          be representative of or        [Systematized Population].
                                                                     generalize to.                 This is the metric.




                                                                                                                                        Refinement
                                                                                                                                        Revision &
                                                       Operationalization
                  Developing one or more procedures for obtaining realizations of the systematized [element].

      Annotation Procedure(s)            Data Representation               Sampling Design            Statistical Estimator(s)
     The operationalized              The operationalized            The population we have         One or more functions that
     concept. The operational         instance. A description of     access to (study               take a [Data Set] and return
     procedure(s) to be               how an instance will be        population); the unit that     an estimate of the [Target
     employed in labeling or          defined, and precisely how     will be sampled (sampling      Parameter]. Also,
     scoring instances based on       feature values and             unit); and how those units     procedures for other
     their [Data Representation].     metadata will be               will be sampled (sampling      inferential tasks (e.g.,
                                      calculated/obtained.           procedure).                    confidence intervals)




                                                                                                                                        Refinement
                                                                                                                                        Revision &
                                                            Application
                                  Applying operationalization to obtain observations or realizations.

            Annotation(s)                       Data Point                        Data Set                   Measurement(s)
     Label(s) or score(s)              A single observed               A set of [Data Points]           The estimate(s) of the
     obtained by applying the          instance—i.e., a row of the     obtained by applying the         [Target Parameter]
     [Annotation Procedures] to        [Data Set].                     [Sampling Design].               obtained by applying the
     a [Data Point] (instance).                                                                         [Statistical Estimator(s)] to
                                                                                                        the [Data Set]

 * Concept column is adapted from Figure 1 of Adcock and Collier (2001), with minor terminology changes to better
 facilitate discussion of measuring GenAI systems’ capabilities, risks, ad impacts.
 ** Systematization is often called conceptualization when describing the process of producing a systematized concept.


 Figure 1: Our proposed framework for measurement tasks of the form: measure the [amount] of a
 [concept] in [instances] from a [population]. The figure shows how the four elements that make up
 such tasks—amounts, concepts, instances, and populations—are formalized through the sequential
 processes of systematization, operationalization and application. Elements in earlier levels (rows)
 can be revised and refined based on findings, including validity concerns, that arise in later levels.


 4       Conclusion

 Our framework helps place many of the disparate-seeming GenAI evaluation practices in use today
 on a common footing. This enables individual evaluations to be better understood, interrogated
 for reliability and validity, and meaningfully compared. In this way, the framework is intended to
 serve as a shared standard for valid measurement of GenAI systems’ capabilities, risks, and impacts.
 For example, using it allows us to (1) more easily identify and remedy validity concerns; and (2)
 compare different measurement tasks by identifying precisely where within the framework they
 diverge. In other words, our framework enables us not only to “evaluate evaluations” but also to
 improve how evaluations of GenAI systems are designed in the first place, thereby helping advance
 such evaluations from their current state of disparate-seeming and ad hoc practices [12, 18] toward
 more formalized and theoretically grounded processes—i.e., toward a science of GenAI evaluations.


                                                                      3
   ChatSearch example: LLM Stat
   workshop
   Evaluation goals: The product team for ChatSearch, an LLM-enabled conversational search engine,
   wants to assess their system for representational harms. Red teaming results show that the system can
   output responses that stereotype or demean, and they want to quantify the extent of the problem.
   Task: measure the [prevalence] of [stereotyping] for [ChatSearch responses] to user queries from [typical
   user interactions]
          Concept*                             Instance                           Population                           Amount
      Background Concept             Background Instance                    Background Population              Background Amount
   Stereotyping                    ChatSearch response to a                ChatSearch under typical         Prevalence of stereotyping
                                   user query                              use in the current US            among ChatSearch
                                                                           deployment.                      responses.


                                                        Systematization**
     Formulating a systematized [element] through reasoning about the background [element] in light of the evaluation goals.

     Systematized Concept            Systematized Instance                  Systematized Population              Target Parameter(s)
   Negative stereotyping as        Text of the ChatSearch                  All ChatSearch responses          *&' = ℙ'( , -; /, 0 = 1
   systematized through            response, - , along with the            to English-language queries      where ℙ+, denotes
   Speech Act Theory. This         user’s input, / , and                   by US-based users.                L, $, 3 drawn from the
   defines an “oracle”             preceding conversational                                                 systematized population,
   stereotype annotation           history, 0 .                                                             and ! is (systematized)
   function, ! = ! L; $, 3                                                                                  negative stereotyping


                                                        Operationalization
                Developing one or more procedures for obtaining realizations of the systematized [element].

    Annotation Procedure(s)             Data Representation                      Sampling Design               Statistical Estimator(s)
   Automated annotation             Triple of text strings (U, X, Z)       Sample of n = 10,000             Inverse probability weighted
   guidelines providing the         representing the system                responses from logged data       estimator:
   definition of stereotyping       response, U, preceding user            on users with US-based IP         NM )*
   along with positive and          input, X, and past 5 turns of                                                   %
                                                                           addresses. Given N logged             1       1
   negative examples. This          conversational history in              interactions, sample turn i       = P              !̂ L& ; $& , 3&
   defines an annotation            standardized format, Z.                with probability 8('" ), where        +     S($& )
                                                                                                                     &'$
   function, !̂ = !̂ L; $, 3                                               S is higher for input text
                                                                           mentioning social groups.

                                                             Application
                                Applying operationalization to obtain observations or realizations.

           Annotation(s)                        Data Point                            Data Set                       Measurement(s)
   !̂( = !̂ *(; B(, C( ∈ 0,1         7! , '! , (!                          Data set *& , B& , C& for ) =     *4 )*
   label returned by                                                       1, … , + = 10,000                      1
                                                                                                                      $! "
                                                                                                                         1
   automated annotation                                                                                      =       5        ,̂ 7" ; '" , ("
                                                                                                                 100   8('" )
   system indicating whether                                                                                          "#$
   negative stereotyping is
   present in the output *(.




Figure 2: A high-level example of using our framework in a hypothetical evaluation of a conversational
search engine, ChatSearch. Each cell provides an overview of what a complete measurement
procedure instantiated using the framework could look like. Note that a full instantiation would
require providing considerable additional information. For example, a fully systematized complex
concept or the full description of a complex sampling design might require several pages of exposition.


References
 [1] Robert Adcock and David Collier. Measurement validity: A shared standard for qualitative and quantitative
     research. American political science review, 95(3):529–546, 2001.

 [2] Su Lin Blodgett, Gilsinia Lopez, Alexandra Olteanu, Robert Sim, and Hanna Wallach. Stereotyping
     norwegian salmon: An inventory of pitfalls in fairness benchmark datasets. In Proceedings of the
     59th Annual Meeting of the Association for Computational Linguistics and the 11th International Joint
     Conference on Natural Language Processing (Volume 1: Long Papers), pages 1004–1015, 2021.

 [3] Nicholas Carlini, Daphne Ippolito, Matthew Jagielski, Katherine Lee, Florian Tramer, and Chiyuan Zhang.
     Quantifying memorization across neural language models. arXiv preprint arXiv:2202.07646, 2022.


                                                                       4
 [4] A Feder Cooper and James Grimmelmann. The Files are in the Computer: Copyright, Memorization, and
     Generative AI. arXiv preprint arXiv:2404.12590, 2024.
 [5] A. Feder Cooper, Yucheng Lu, Jessica Forde, and Christopher M De Sa. Hyperparameter Optimization Is
     Deceiving Us, and How to Stop It. In M. Ranzato, A. Beygelzimer, Y. Dauphin, P.S. Liang, and J. Wortman
     Vaughan, editors, Advances in Neural Information Processing Systems, volume 34, pages 3081–3095.
     Curran Associates, Inc., 2021.
 [6] A. Feder Cooper, Katherine Lee, Madiha Zahrah Choksi, Solon Barocas, Christopher De Sa, James
     Grimmelmann, Jon Kleinberg, Siddhartha Sen, and Baobao Zhang. Arbitrariness and Social Prediction:
     The Confounding Role of Variance in Fair Classification. Proceedings of the AAAI Conference on Artificial
     Intelligence, 38(20):22004–22012, March 2024.
 [7] Amanda Coston, Alan Mishler, Edward H Kennedy, and Alexandra Chouldechova. Counterfactual risk
     assessments, evaluation, and fairness. In Proceedings of the 2020 conference on fairness, accountability,
     and transparency, pages 582–593, 2020.
 [8] Jesse Dodge, Suchin Gururangan, Dallas Card, Roy Schwartz, and Noah A. Smith. Show Your Work:
     Improved Reporting of Experimental Results. In Proceedings of the 2019 Conference on Empirical
     Methods in Natural Language Processing and the 9th International Joint Conference on Natural Language
     Processing (EMNLP-IJCNLP), pages 2185–2194, Hong Kong, China, November 2019. Association for
     Computational Linguistics.
 [9] Daphne Ippolito, Florian Tramèr, Milad Nasr, Chiyuan Zhang, Matthew Jagielski, Katherine Lee, Christo-
     pher A. Choquette-Choo, and Nicholas Carlini. Preventing Verbatim Memorization in Language Models
     Gives a False Sense of Privacy, 2023. URL https://arxiv.org/abs/2210.17546.
[10] Benjamin Laufer, Thomas Gilbert, and Helen Nissenbaum. Optimization’s neglected normative commit-
     ments. In Proceedings of the 2023 ACM Conference on Fairness, Accountability, and Transparency, pages
     50–63, 2023.
[11] Yu Lu Liu, Su Lin Blodgett, Jackie Cheung, Q. Vera Liao, Alexandra Olteanu, and Ziang Xiao. ECBD:
     Evidence-centered benchmark design for NLP. In Lun-Wei Ku, Andre Martins, and Vivek Srikumar,
     editors, Proceedings of the 62nd Annual Meeting of the Association for Computational Linguistics (Volume
     1: Long Papers), pages 16349–16365, Bangkok, Thailand, August 2024. Association for Computational
     Linguistics. URL https://aclanthology.org/2024.acl-long.861.
[12] Nestor Maslej, Loredana Fattorini, Raymond Perrault, Vanessa Parli, Anka Reuel, Erik Brynjolfsson, John
     Etchemendy, Katrina Ligett, Terah Lyons, James Manyika, Juan Carlos Niebles, Yoav Shoham, Russell
     Wald, and Jack Clark. The AI index 2024 annual report. AI Index Steering Committee, Institute for
     Human-Centered AI, Stanford University, April 2024.
[13] Dylan Mulvin. Proxies: The cultural work of standing in. MIT Press, 2021.
[14] Johan Obando-Ceron, João G. M. Araújo, Aaron Courville, and Pablo Samuel Castro. On the consistency
     of hyper-parameter selection in value-based deep reinforcement learning, 2024. URL https://arxiv.
     org/abs/2406.17523.
[15] Ziad Obermeyer, Brian Powers, Christine Vogeli, and Sendhil Mullainathan. Dissecting racial bias in an
     algorithm used to manage the health of populations. Science, 366(6464):447–453, 2019.
[16] Samir Passi and Solon Barocas. Problem formulation and fairness. In Proceedings of the conference on
     fairness, accountability, and transparency, pages 39–48, 2019.
[17] Shangshu Qian, Hung Viet Pham, Thibaud Lutellier, Zeou Hu, Jungwon Kim, Lin Tan, Yaoliang Yu, Jiahao
     Chen, and Sameena Shah. Are my deep learning systems fair? an empirical study of fixed-seed training. In
     A. Beygelzimer, Y. Dauphin, P. Liang, and J. Wortman Vaughan, editors, Advances in Neural Information
     Processing Systems, 2021. URL https://openreview.net/forum?id=kLWGdQYsmC5.
[18] Kevin Roose. A.I. has a measurement problem. The New York Times, April 2024. URL https://www.
     nytimes.com/2024/04/15/technology/ai-models-measurement.html. Accessed: 2024-09-05.
[19] Irene Solaiman, Zeerak Talat, William Agnew, Lama Ahmad, Dylan Baker, Su Lin Blodgett, Canyu Chen,
     Hal Daumé III, Jesse Dodge, Isabella Duan, et al. Evaluating the social impact of generative ai systems in
     systems and society. arXiv preprint arXiv:2306.05949, 2023.
[20] Jamelle Watson-Daniels, Solon Barocas, Jake M Hofman, and Alexandra Chouldechova. Multi-target
     multiplicity: Flexibility and fairness in target specification under resource constraints. In Proceedings of
     the 2023 ACM Conference on Fairness, Accountability, and Transparency, pages 297–311, 2023.
[21] Dora Zhao, Jerone TA Andrews, Orestis Papakyriakopoulos, and Alice Xiang. Position: Measure dataset
     diversity, don’t just claim it. arXiv preprint arXiv:2407.08188, 2024.




                                                       5
