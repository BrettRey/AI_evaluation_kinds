            Towards Reasoning in Large Language Models: A Survey

                          Jie Huang Kevin Chen-Chuan Chang
          Department of Computer Science, University of Illinois at Urbana-Champaign
                             {jeffhj, kcchang}@illinois.edu




                      Abstract                               they are large enough (Wei et al., 2022a). For ex-
                                                             ample, by providing the models with “chain of
    Reasoning is a fundamental aspect of human               thoughts”, i.e., reasoning exemplars, or a simple
    intelligence that plays a crucial role in activi-        prompt “Let’s think step by step”, these models
    ties such as problem solving, decision making,
                                                             are able to answer questions with explicit reason-
    and critical thinking. In recent years, large
    language models (LLMs) have made signifi-                ing steps (Wei et al., 2022b; Kojima et al., 2022),
    cant progress in natural language processing,            e.g., “all whales are mammals, all mammals have
    and there is observation that these models may           kidneys; therefore, all whales have kidneys.” This
    exhibit reasoning abilities when they are suf-           has sparked considerable interest in the commu-
    ficiently large. However, it is not yet clear to         nity since reasoning ability is a hallmark of human
    what extent LLMs are capable of reasoning.               intelligence that is frequently considered missed
    This paper provides a comprehensive overview
                                                             in current artificial intelligence systems (Marcus,
    of the current state of knowledge on reasoning
    in LLMs, including techniques for improving              2020; Russin et al., 2020; Mitchell, 2021; Bom-
    and eliciting reasoning in these models, meth-           masani et al., 2021).
    ods and benchmarks for evaluating reasoning                 However, despite the strong performance of
    abilities, findings and implications of previous         LLMs on certain reasoning tasks, it remains unclear
    research in this field, and suggestions on future        whether LLMs are actually reasoning and to what
    directions. Our aim is to provide a detailed and
                                                             extent they are capable of reasoning. For exam-
    up-to-date review of this topic and stimulate
    meaningful discussion and future work.1                  ple, Kojima et al. (2022) claim that “LLMs are de-
                                                             cent zero-shot reasoners (p. 1)”, while Valmeekam
1   Introduction                                             et al. (2022) conclude that “LLMs are still far
                                                             from achieving acceptable performance on com-
Reasoning is a cognitive process that involves using         mon planning/reasoning tasks which pose no issues
evidence, arguments, and logic to arrive at conclu-          for humans to do (p. 2).” This limitation is also
sions or make judgments. It plays a central role in          stated by Wei et al. (2022b):
many intellectual activities, such as problem solv-
ing, decision making, and critical thinking. The                “we qualify that although chain of thought emu-
study of reasoning is important in fields like psy-             lates the thought processes of human reasoners,
chology (Wason and Johnson-Laird, 1972), philoso-               this does not answer whether the neural network
phy (Passmore, 1961), and computer science (Huth                is actually reasoning (p. 9).”
and Ryan, 2004), as it helps individuals make deci-             Therefore, in this paper, we aim to provide a
sions, solve problems, and think critically.                 comprehensive overview and engage in an insight-
   Recently, large language models (LLMs)                    ful discussion on the current state of knowledge on
(Brown et al., 2020; Chowdhery et al., 2022; Chung           this fast-evolving topic. We initiate our exploration
et al., 2022; OpenAI, 2022, inter alia) such as Chat-        with a clarification of the concept of reasoning (§2).
GPT have made significant advancements in natu-              Subsequently, we turn our attention to the tech-
ral language processing and related fields. It has           niques for enhancing/eliciting reasoning in LLMs
been shown that these models exhibit emergent be-            (§3), the methods and benchmarks for evaluating
haviors, including the ability to “reason”, when             reasoning in LLMs (§4), and the key findings and
   1
     Paperlist can be found at https://github.com/           implications in this field (§5). Finally, we reflect
jeffhj/LM-reasoning.                                         on and discuss the current state of the field (§6).
                                                        1049
                 Findings of the Association for Computational Linguistics: ACL 2023, pages 1049–1065
                            July 9-14, 2023 ©2023 Association for Computational Linguistics
                                                                                                    Chain of Thought and Its Variants (§3.2.1)
                                                           Fully Supervised Finetuning (§3.1)
                                                                                                    Rationale Engineering (§3.2.2)
                                                           Prompting & In-Context Learning (§3.2)
                                                                                                    Problem Decomposition (§3.2.3)
                         Techniques (§3)
                                                                                                    Others (§3.2.4)
 Reasoning in LLMs




                                                                                                    Reasoning-Enhanced Training & Prompting (§3.3.1)
                                                           Hybrid Method (§3.3)
                                                                                                    Bootstrapping & Self-Improving (§3.3.2)
                                                           End Task Performance (§4.1)
                         Evaluation & Analysis (§4)
                                                           Analysis on Reasoning (§4.2)
                         Findings & Implications (§5)

                         Reflection, Discussion & Future Directions (§6)


                                                            Figure 1: The structure of the paper.


2                    What is Reasoning?                                               based on the best explanation for a given set of
                                                                                      observations. The conclusion is the most likely
Reasoning is the process of thinking about some-
                                                                                      explanation based on the available evidence, but it
thing in a logical and systematic way, using evi-
                                                                                      is not necessarily certain. For example:
dence and past experiences to reach a conclusion or
make a decision (Wason and Johnson-Laird, 1972;                                           • Observation: The car cannot start and there is
Wason, 1968; Galotti, 1989; Fagin et al., 2004;                                             a puddle of liquid under the engine.
McHugh and Way, 2018). Reasoning involves mak-                                            • Conclusion: The most likely explanation is
ing inferences, evaluating arguments, and drawing                                           that the car has a leak in the radiator.
logical conclusions based on available information.                                   Other types of reasoning include analogical reason-
Although “reasoning” is a term that is commonly                                       ing, which involves making comparisons between
used in literature and daily life, it is also an abstract                             two or more things in order to make inferences
concept that can refer to many things. To help the                                    or arrive at conclusions; causal reasoning, which
reader better understand this concept, we summa-                                      involves identifying and understanding the causes
rize several main categories of reasoning that are                                    and effects of events or phenomena; and probabilis-
commonly recognized:                                                                  tic reasoning, which involves making decisions or
                                                                                      arriving at conclusions based on the likelihood or
Deductive reasoning. Deductive reasoning is a
                                                                                      probability of certain outcomes.
type of reasoning in which a conclusion is drawn
based on the truth of the premises. In deductive                                      Formal Reasoning vs Informal Reasoning. For-
reasoning, the conclusion must necessarily follow                                     mal reasoning is a systematic and logical process
from the premises, meaning that if the premises are                                   that follows a set of rules and principles, often used
true, the conclusion must also be true. For example:                                  in mathematics and logic. Informal reasoning is a
             • Premise: All mammals have kidneys.                                     less structured approach that relies on intuition, ex-
             • Premise: All whales are mammals.                                       perience, and common sense to draw conclusions
             • Conclusion: All whales have kidneys.                                   and solve problems, and is often used in everyday
                                                                                      life. Formal reasoning is more structured and reli-
Inductive reasoning. Inductive reasoning is a type                                    able, while informal reasoning is more adaptable
of reasoning in which a conclusion is drawn based                                     and open-ended, but may also be less reliable. We
on observations or evidence. The conclusion is                                        refer the reader to Galotti (1989); Bronkhorst et al.
likely to be true based on the available evidence,                                    (2020) for a detailed distinction between them.
but it is not necessarily certain. For example:
                                                                                      Reasoning in Language Models. The concept of
             • Observation: Every time we see a creature                              reasoning in language models has been around for
               with wings, it is a bird.                                              some time, but there is not a clear definition of
             • Observation: We see a creature with wings.                             what it entails. In the literature, the term “reason-
             • Conclusion: The creature is likely to be a bird.                       ing” is often used to refer to informal reasoning,
Abductive reasoning. Abductive reasoning is a                                         although it is not always explicitly stated that it
type of reasoning in which a conclusion is drawn                                      is informal (Cobbe et al., 2021; Wei et al., 2022b,
                                                                                1050
inter alia). Different forms of reasoning may be                   language models to solve competition mathematics
used depending on the task, benchmark, or method                   problems by generating full step-by-step solutions,
being used, e.g., deductive reasoning (Cobbe et al.,               though the accuracy is relatively low. Nye et al.
2021; Creswell et al., 2022; Han et al., 2022b, in-                (2022) train language models to do multi-step rea-
ter alia), inductive reasoning (Yang et al., 2022;                 soning for program synthesis/execution by generat-
Misra et al., 2022, inter alia) or abductive reason-               ing “scratchpads”, i.e., intermediate computations,
ing (Wiegreffe et al., 2022; Lampinen et al., 2022;                before producing the final answers. We refer the
Jung et al., 2022, inter alia). In this paper, we                  reader to Helwe et al. (2021); Bhargava and Ng
encompass various forms of reasoning, with a par-                  (2022)’s survey for more studies in this line.
ticular focus on “informal deductive reasoning” in                    There are two major limitations of fully super-
large language models since it is a widely used                    vised finetuning. First, it requires a dataset contain-
form in which the conclusion is guaranteed to be                   ing explicit reasoning, which can be difficult and
true as long as the premises are true.                             time-consuming to create. Additionally, the model
                                                                   is only trained on a specific dataset, which limits
3    Towards Reasoning in Large Language                           its application to a specific domain and may result
     Models                                                        in the model relying on artifacts in the training data
Reasoning, particularly multi-step reasoning, is of-               rather than actual reasoning to make predictions.
ten seen as a weakness in language models and
                                                                   3.2     Prompting & In-Context Learning
other NLP models (Bommasani et al., 2021; Rae
et al., 2021; Valmeekam et al., 2022). Recent re-                  Large language models such as GPT-3 (Brown
search has suggested that reasoning ability may                    et al., 2020) have demonstrated remarkable few-
emerge in language models at a certain scale, such                 shot performance across a variety of tasks through
as models with over 100 billion parameters (Wei                    in-context learning. These models can be prompted
et al., 2022a,b; Cobbe et al., 2021). In this paper,               with a question and a few ⟨input, output⟩ exemplars
we follow Wei et al. (2022a) in considering rea-                   to potentially solve a problem through “reasoning”,
soning as an ability that is rarely present in small-              either implicitly or explicitly. However, research
scale models like GPT-2 (Radford et al., 2019) and                 has shown that these models still fall short when
BERT (Devlin et al., 2019), and therefore focus                    it comes to tasks that require multiple steps of rea-
on techniques applicable to improving or eliciting                 soning to solve (Bommasani et al., 2021; Rae et al.,
“reasoning”2 in LLMs such as GPT-3 (Brown et al.,                  2021; Valmeekam et al., 2022). This may be due
2020) and PaLM (Chowdhery et al., 2022).                           to a lack of exploration into the full capabilities of
                                                                   these models, as recent studies have suggested.
3.1 Fully Supervised Finetuning
                                                                   3.2.1    Chain of Thought and Its Variants
Before discussing reasoning in large language mod-
els, it is worth mentioning there is research work-                To encourage LLMs to engage in reasoning rather
ing on eliciting/improving reasoning in small lan-                 than simply providing answers directly, we may
guage models through fully supervised finetuning                   guide LLMs to generate “reasoning” explicitly.
on specific datasets. For example, Rajani et al.                   One approach for doing this is chain-of-thought
(2019) finetune a pretrained GPT model (Radford                    prompting, proposed by Wei et al. (2022b). This
et al., 2018) to generate rationales that explain                  approach involves providing a few examples of
model predictions with the built CoS-E dataset,                    “chain of thought” (CoT), which are intermediate
and find that models trained with explanations                     natural language reasoning steps, in the prompt to
perform better on commonsense question answer-                     LLMs (Figure 2). Specifically, in CoT prompting,
ing tasks (Talmor et al., 2019). Talmor et al.                     ⟨input, output⟩ demonstrations are replaced with
(2020) train RoBERTa (Liu et al., 2019) to per-                    ⟨input, chain of thought, output⟩ triples, e.g., “[in-
form reasoning/inference based on both implicit                    put] Roger has 5 tennis balls. He buys 2 more cans
pre-trained knowledge and explicit free-text state-                of tennis balls. Each can has 3 tennis balls. How
ments. Hendrycks et al. (2021) finetune pretrained                 many tennis balls does he have now? [chain of
                                                                   thought] Roger started with 5 balls. 2 cans of 3
    2
      It is important to note that the term “reasoning” in this    tennis balls each is 6 tennis balls. 5 + 6 = 11. [out-
paper does not necessarily imply that LLMs are truly capable
of reasoning or that they are able to reason in the same way       put] The answer is 11.” In this way, given a target
that humans do. We will discuss this issue in more detail in §6.   question, the model learns to generate explicit ratio-
                                                               1051
                                         [Input] Roger has 5 tennis balls. He buys 2 more cans of tennis
                                         balls. Each can has 3 tennis balls. How many tennis balls does he
                                         have now? [Rationale] Roger started with 5 balls. 2 cans of 3 tennis
                                         balls each is 6 tennis balls. 5 + 6 = 11. [Output] The answer is 11.
              Rationale Refinement
                                                                                                   Rationale Verification
                    Input A, Rationale A, Output A
                                                                                         Rationale* 1
     Exemplars      Input B, Rationale B, Output B
                                                                 LLM                     Rationale* 2              Output*
                    Input C, Rationale C, Output C
                                                                                         Rationale* 3
                               Input*
                                                                    Rationale Exploration

Figure 2: An illustration of Chain-of-Thought Prompting and Rationale Engineering, where asterisk (*) denotes the
target problem to be solved.


nale before producing the final answer. Experimen-                (2022) apply chain of thought to solve multimodal
tal results show that this simple idea can improve                science questions.
LLMs’ few-shot performance on arithmetic, sym-
bolic, and commonsense reasoning tasks, some-                     3.2.2      Rationale Engineering
times to a striking degree.                                       The original version of chain-of-thought prompting,
   There are several variants of chain-of-thought                 proposed by Wei et al. (2022b), relies on manually
prompting that have been proposed in the literature,              crafted examples of intermediate reasoning steps
in a different form or to solve a specific problem.               and applies greedy decoding in the generation. Ra-
   Different Form: Kojima et al. (2022) intro-                    tionale engineering aims to more effectively elicit
duce Zero-shot-CoT, in which LLMs are simply                      or utilize reasoning in LLMs. This can be achieved
prompted with the phrase “Let’s think step by step”               through rationale refinement, which involves cre-
after the input, in order to elicit reasoning without             ating more effective examples of reasoning steps,
the need for few-shot demonstrations. Madaan et al.               or through rationale exploration and rationale ver-
(2022); Gao et al. (2022); Chen et al. (2022) find                ification, which involve exploring and verifying
that LLMs trained with code, e.g., Codex (Chen                    the rationales produced by LLMs. A summary of
et al., 2021), can achieve better performance on                  raltionale engineering is illustrated in Figure 2.
reasoning tasks by framing reasoning as code gen-                 Rationale refinement. The choice of exemplars
eration. Wang et al. (2022a) propose to iteratively               can significantly affect the few-shot performance of
prompt chain of thought. He et al. (2023) attempt                 LLMs, as demonstrated in research such as Liu et al.
to retrieve external knowledge in CoT to improve                  (2022b), which also appears in chain-of-thought
faithfulness of reasoning.                                        prompting. Rationale refinement aims to create
   Specific Problem/Setting: Before chain of                      and refine rationale examples that are better able to
thought, Nye et al. (2022) also try to use intermedi-             elicit reasoning in LLMs. Fu et al. (2022b) propose
ate computations, named “scratchpads”, to improve                 complexity-based prompting to create rationales
language models’ reasoning performance in both                    with more reasoning steps. Their experiments show
finetuning and few-shot regimes, with a particular                that the performance of LLMs improves with the in-
focus on programs. Shi et al. (2022) attempt to                   creased rationale complexity. Similarly, Zhou et al.
solve multilingual reasoning tasks with CoT in the                (2022c) propose algorithmic prompting, which sug-
native language, CoT in English (regardless of the                gests that providing more thorough examples of
problem language), and CoT in English (with the                   solutions can help improve reasoning performance
problem translated to English). Chen (2022) apply                 on some simple math calculations. Zhang et al.
CoT to table-based reasoning, finding that LLMs                   (2022b) design Auto-CoT to automatically con-
can achieve strong performance on table tasks with                struct exemplars by partitioning questions from
only one exemplar. Prystawski et al. (2022) demon-                a given dataset into clusters and then using Zero-
strate that CoT can improve LLMs’ performance                     Shot-CoT (Kojima et al., 2022) to generate the
on paraphrase selection for metaphors. Lu et al.                  rationale for a representative question from each
                                                            1052
cluster. The analysis shows that making exemplars        position or divide and conquer (Talmor and Berant,
diverse is important in prompting LLMs to produce        2018; Min et al., 2019; Perez et al., 2020).
better rationales.                                          Based on this idea, Zhou et al. (2022a) pro-
                                                         pose least-to-most prompting, which consists of
Rationale exploration. In addition to providing
                                                         two steps: decomposing the complex problem into
better exemplars, we can allow LLMs to fully ex-
                                                         subproblems and solving these subproblems in a
plore various ways of reasoning to improve their
                                                         specific order, with each subproblem being facil-
performance on reasoning tasks, named rationale
                                                         itated by the answers obtained from previously
exploration. Based on the idea that complex prob-
                                                         solved subproblems. As follow-up work, Droz-
lems often admit multiple ways of thinking that
                                                         dov et al. (2022) introduce dynamic least-to-most
can lead to their unique correct answer, Wang et al.
                                                         prompting, which is designed to solve more realis-
(2022c) present a decoding strategy called self-
                                                         tic semantic parsing problems by decomposing the
consistency to improve upon the traditional greedy
                                                         problems with prompting-based syntactic parsing
decoding used in chain-of-thought prompting. This
                                                         and dynamically selecting exemplars based on the
strategy involves sampling a diverse set of ratio-
                                                         decomposition. In addition, Khot et al. (2022) de-
nales, rather than just the greedy one, and selecting
                                                         sign decomposed prompting, which breaks down
the most consistent answer by marginalizing out
                                                         a complex problem into subproblems that can be
the sampled rationales. The idea is also used in
                                                         handled by a shared library of prompting-based
Fu et al. (2022b) to vote over the top complex ra-
                                                         LLMs, each specialized in a particular subprob-
tionales. To further improve performance, Li et al.
                                                         lem. Furthermore, Dua et al. (2022) develop suc-
(2022b) suggest providing different demonstrations
                                                         cessive prompting, which iteratively decomposes a
for each question by sampling exemplars from an
                                                         complex problem into a simple problem, with the
exemplar base, in order to increase the diversity of
                                                         next subproblem prediction having access to the
the sampled rationales.
                                                         answers to the previous subproblems. While the
Rationale verification. Ensuring that the ratio-         above methods decompose or solve compositional
nales produced by LLMs are valid is critical, as in-     questions with multiple forward passes, Press et al.
correct rationales can lead to incorrect final predic-   (2022) suggest decomposing and solving the input
tions (Ye and Durrett, 2022). To address this issue,     question in one forward pass using CoT prompting.
the process of rationale verification aims to verify     Overall, these techniques show promise for helping
whether the rationales produced by LLMs lead to          LLMs to solve complex tasks by decomposing the
the correct final answers. Cobbe et al. (2021) pro-      problem into more manageable subproblems.
pose augmenting LLMs with a trained verifier that
assigns a score to each rationale and solution gen-      3.2.4   Others
erated by the LLM, selecting the highest-ranked          There are other techniques that have been devel-
solution as the final answer when solving math           oped to facilitate reasoning in LLMs for specific
word problems. Li et al. (2022b) also use this tech-     tasks or settings. For instance, Creswell et al.
nique to guide rationale selection, in conjunction       (2022); Creswell and Shanahan (2022) introduce a
with the process of rationale exploration. Differ-       selection-inference framework that uses LLMs as
ent from the above methods that train an external        modules to select and infer reasoning steps from
verifier to verify the rationales, Weng et al. (2022)    a set of facts that culminate in the final answer.
suggest using LLMs themselves as the verifiers.          Kazemi et al. (2022) suggest using backward chain-
                                                         ing, i.e., from goal to the set of facts that support
3.2.3 Problem Decomposition                              it, instead of forward chaining like Creswell et al.
Chain-of-thought prompting, while effective for          (2022); Creswell and Shanahan (2022). In addition,
eliciting reasoning in LLMs, can struggle with com-      Jung et al. (2022) propose a method for solving
plex tasks, e.g., tasks that require compositional       binary questions by prompting LLMs abductively
generalization (Lake and Baroni, 2018; Keysers           and recursively to rationalize each option. Zhou
et al., 2020). To solve a complex problem, it is         et al. (2022b) design a technique for performing
helpful to first break it down into smaller, more        numerical reasoning on complex numbers by re-
manageable subproblems. By solving each of these         placing the complex numbers with simple numbers
subproblems, we can effectively solve the complex        to produce simpler expressions, and then using
problem. This technique is called problem decom-         these expressions to perform calculations on the
                                                     1053
complex numbers. There are also efforts to distill               finetuning and scratchpad prompting results in a
reasoning from LLMs into smaller models, such                    significant improvement in LLMs’ ability to gener-
as the work by Li et al. (2022a); Shridhar et al.                alize to longer problems, while this phenomenon
(2022); Magister et al. (2022). Finally, we refer the            is not observed in the standard fully supervised
reader to Dohan et al. (2022)’s position paper on                finetuning paradigm.
language model cascade, which presents a unify-
ing framework for understanding chain-of-thought                 3.3.2    Bootstrapping & Self-Improving
prompting and research in this line.                             Instead of finetuning LLMs on pre-built datasets
                                                                 that include reasoning, there are studies that have
3.3 Hybrid Method
                                                                 explored the idea of using LLMs to self-improve
While “prompting” techniques can help elicit or                  their reasoning abilities through a process known
better utilize reasoning in large language models                as bootstrapping. One example of this is the Self-
to solve reasoning tasks, they do not actually im-               Taught Reasoner (STaR) introduced by Zelikman
prove the reasoning capabilities of the LLMs them-               et al. (2022), in which a LLM is trained and refined
selves, as the parameters of the models remain un-               on its own output iteratively. Specifically, with CoT
changed. In contrast, the “hybrid approach” aims to              prompting, the model first generates initial ratio-
simultaneously improve the reasoning capabilities                nales. And then, the model is finetuned on ratio-
of LLMs and make better use of these models in                   nales that lead to correct answers. This process can
order to solve complex problems. This approach in-               be repeated, with each iteration resulting in an im-
volves both enhancing the reasoning capabilities of              proved model that can generate better training data,
the LLMs and using techniques such as prompting                  which in turn leads to further improvements. As a
to effectively utilize these capabilities.                       follow-up to this work, Huang et al. (2022a) show
3.3.1 Reasoning-Enhanced Training and                            that LLMs are able to self-improve their reasoning
         Prompting                                               abilities without the need for supervised data by
                                                                 leveraging the self-consistency of reasoning (Wang
One approach to improving the reasoning capabili-
                                                                 et al., 2022c).
ties of LLMs is to pretrain or finetune the models
on datasets that include “reasoning”. Lewkowycz
                                                                 4     Measuring Reasoning in Large
et al. (2022); Taylor et al. (2022) find that LLMs
                                                                       Language Models
trained on datasets containing scientific and math-
ematical data can achieve better performance on                  We summarize methods and benchmarks for evalu-
reasoning tasks like quantitative reasoning prob-                ating reasoning abilities of LLMs in this section.
lems when using CoT prompting3 . Pi et al. (2022)
show that continually pretraining with SQL data                  4.1     End Task Performance
can boost the performance of language models, e.g.,
                                                                 One way to measure reasoning abilities of LLMs is
T5 (Raffel et al., 2020), on natural language rea-
                                                                 to report their performance, e.g., accuracy, on end
soning such as numerical reasoning and logical rea-
                                                                 tasks that require reasoning. We list some common
soning. Furthermore, Chung et al. (2022) develop
                                                                 benchmarks as follows.
Flan models by finetuning PaLM (Chowdhery et al.,
2022) and T5 (Raffel et al., 2020) with 1.8k fine-               Arithmetic Reasoning. Arithmetic reasoning is
tuning tasks, including CoT data, and find that                  the ability to understand and apply mathemat-
CoT data are critical to keeping reasoning abilities.            ical concepts and principles in order to solve
Similarly, Yu et al. (2022) finetune OPT (Zhang                  problems involving arithmetic operations. This
et al., 2022a) on 10 reasoning datasets and observe              involves using logical thinking and mathemat-
that it can improve some reasoning capabilities of               ical principles to determine the correct course
LLMs. Anil et al. (2022) study the length gener-                 of action when solving mathematical problems.
alization abilities of LLMs, i.e., whether LLMs                  Representative benchmarks for arithmetic rea-
learned with short problem instances can general-                soning include GSM8K (Cobbe et al., 2021),
ize to long ones. They discover that the combina-                Math (Hendrycks et al., 2021), MathQA (Amini
tion of few-shot scratchpad (or chain of thought)                et al., 2019), SVAMP (Patel et al., 2021), AS-
    3
      This may also be true for models trained with code (Chen   Div (Miao et al., 2020), AQuA (Ling et al., 2017),
et al., 2021; Fu et al., 2022a).                                 and MAWPS (Roy and Roth, 2015). It is worth
                                                             1054
mentioning that Anil et al. (2022) generate the Par-   because most existing evaluations focus on their ac-
ity Datasets and the Boolean Variable Assignment       curacy on end tasks, rather than directly assessing
Dataset for analyzing the length generalization ca-    their reasoning steps. While some error analysis
pabilities of LLMs (§3.3.1).                           has been conducted on the generated rationales of
Commonsense Reasoning. Commonsense Rea-                LLMs (Wei et al., 2022b; Kojima et al., 2022, inter
soning is the use of everyday knowledge and under-     alia), this analysis has often been limited in depth.
standing to make judgments and predictions about          There have been some efforts to develop metrics
new situations. It is a fundamental aspect of human    and benchmarks that enable a more formal/deep
intelligence that enables us to navigate our envi-     analysis of reasoning in LLMs. Golovneva et al.
ronment, understand others, and make decisions         (2022) design ROSCOE, a set of interpretable, de-
with incomplete information. Benchmarks that can       tailed step-by-step evaluation metrics covering vari-
be used for testing commonsense reasoning abili-       ous perspectives including semantic alignment, log-
ties of LLMs include CSQA (Talmor et al., 2019),       ical inference, semantic similarity, and language
StrategyQA (Geva et al., 2021), and ARC (Clark         coherence. Saparov and He (2022) create a syn-
et al., 2018). We refer the reader to Bhargava and     thetic dataset called PrOntoQA that is generated
Ng (2022)’s survey for more work in this domain.       from real or fictional ontologies. Each example
                                                       in the dataset has a unique proof, which can be
Symbolic Reasoning. Symbolic reasoning is a            converted to simple sentences and back again, al-
form of reasoning that involves the manipulation       lowing for a formal analysis of each reasoning step.
of symbols according to formal rules. In symbolic      Han et al. (2022a) introduce a dataset called FO-
reasoning, we use abstract symbols to represent        LIO to test the first-order logic reasoning capabil-
concepts and relationships, and then manipulate        ities of LLMs. FOLIO contains first-order logic
those symbols according to precise rules in order      reasoning problems that require models to deter-
to draw conclusions or solve problems. Two bench-      mine the correctness of conclusions given a set of
marks of symbolic reasoning are presented in Wei       premises. In addition, Wang et al. (2022b) conduct
et al. (2022b), including Last Letter Concatenation    ablation experiments on CoT and find that LLMs
and Coin Flip.                                         may also perform reasoning while prompting with
Others. In practice, there are many benchmarks         invalid rationals. Their study also suggests that be-
that can be used to evaluate reasoning abilities       ing relevant to the query and correctly ordering the
of LLMs (indirectly), as long as the downstream        reasoning steps are important for CoT prompting.
task involves reasoning. BIG-bench (Srivastava            In summary, most existing studies primarily re-
et al., 2022), for example, includes over 200 tasks    port the performance of the models on downstream
that test a range of reasoning skills, including       reasoning tasks, without a detailed examination of
tasks like Date Understanding, Word Sorting, and       the quality of the rationales produced. This leaves
Causal Judgement. Other benchmarks, such as            open the question of whether the models are ac-
SCAN (Lake and Baroni, 2018) and the one pro-          tually able to reason in a way that is similar to
posed by Anil et al. (2022), focus on evaluating       human reasoning, or whether they are simply able
generalization ability. LLMs can also be tested on     to achieve good performance on the tasks through
their table reasoning abilities using benchmarks       other means. Further research is needed to more
such as WikiTableQA (Pasupat and Liang, 2015),         formally analyze the reasoning abilities of LLMs.
FetaQA (Nan et al., 2022), as suggested by Chen
(2022). In addition, there are benchmarks for eval-    5   Findings and Implications
uating LLMs’ generative relational reasoning abil-
                                                       In this section, we summarize the important find-
ities, such as CommonGen (Lin et al., 2020; Liu
                                                       ings and implications of studies on reasoning in
et al., 2022a) and Open Relation Modeling (Huang
                                                       large language models.
et al., 2022b,d).
                                                       Reasoning seems an emergent ability of LLMs.
4.2 Analysis on Reasoning                              Wei et al. (2022a,b); Suzgun et al. (2022) show that
Although LLMs have demonstrated impressive per-        reasoning ability appears to emerge only in large
formance on various reasoning tasks, the extent to     language models like GPT-3 175B, as evidenced by
which their predictions are based on true reasoning    significant improvements in performance on rea-
or simple heuristics is not always clear. This is      soning tasks at a certain scale (e.g., 100 billion
                                                   1055
parameters). This suggests that it may be more ef-      Han et al. (2022a); Ruis et al. (2022). For in-
fective to utilize large models for general reasoning   stance, Valmeekam et al. (2022) find that even in
problems rather than training small models for spe-     relatively simple commonsense planning domains
cific tasks. However, the reason for this emergent      that humans would have no trouble navigating,
ability is not yet fully understood. We refer the       LLMs such as GPT-3 (Brown et al., 2020) and
reader to Wei et al. (2022a); Fu et al. (2022a) for     BLOOM (Scao et al., 2022) struggle to perform
some potential explanations.                            effectively. These findings suggest that existing
                                                        benchmarks may be too simple to accurately gauge
Chain of thought elicits “reasoning” of LLMs.           the true reasoning abilities of LLMs, and that more
The use of chain-of-thought (CoT) prompts (Wei          challenging tasks may be needed to fully evaluate
et al., 2022b) has been shown to improve the per-       their abilities in this regard.
formance of LLMs on various reasoning tasks,
as demonstrated in the experiments of Wei et al.        6   Reflection, Discussion, and Future
(2022a,b); Suzgun et al. (2022). Additionally,              Directions
Saparov and He (2022) (§4.2) find that, when us-
ing CoT prompts, LLMs are able to produce valid         Why reasoning? Reasoning is the process of think-
individual proof steps, even when the synthetic on-     ing about something in a logical and systematic
tology is fictional or counterfactual. However, they    way, and it is a key aspect of human intelligence.
may sometimes choose the wrong steps when mul-          By incorporating reasoning capabilities into lan-
tiple options are available, leading to incomplete      guage models, we can enable them to perform tasks
or incorrect proofs. Moreover, for many reasoning       that require more complex and nuanced thinking,
tasks where the performance of standard prompting       such as problem solving, decision making, and
grows smoothly with model scale, chain-of-thought       planning (Huang et al., 2022e,f; Song et al., 2022).
prompting can lead to dramatic performance im-          This can improve the performance of these mod-
provement. In addition to these benefits, the use of    els on downstream tasks and increase their out-of-
CoT prompts has been shown to improve the out-of-       distribution robustness (Wei et al., 2022a,b; Suzgun
distribution robustness of LLMs (Wei et al., 2022b;     et al., 2022; Zhou et al., 2022a; Anil et al., 2022).
Zhou et al., 2022a; Anil et al., 2022, inter alia),     In addition, reasoning can make language models
an advantage that is not typically observed with        more explainable and interpretable, as it provides
standard prompting or fully supervised finetuning       explicit rationales for their predictions.
paradigms.                                              Right task/application? As Valmeekam et al.
                                                        (2022) point out, current benchmarks may not ade-
LLMs show human-like content effects on rea-            quately reflect the reasoning capabilities of LLMs.
soning. According to Dasgupta et al. (2022), LLMs       In addition, tasks such as solving simple math prob-
exhibit reasoning patterns that are similar to those    lems and concatenating letters in strings (§4.1) are
of humans as described in the cognitive literature.     artificial and do not accurately reflect real-world
For example, the models’ predictions are influ-         situations. To truly understand the reasoning ability
enced by both prior knowledge and abstract rea-         of LLMs, it is important to consider more realistic
soning, and their judgments of logical validity are     and meaningful applications such as decision mak-
impacted by the believability of the conclusions.       ing (Edwards, 1954), legal reasoning (Levi, 2013),
These findings suggest that, although language          and scientific reasoning (Zimmerman, 2000). Our
models may not always perform well on reasoning         ultimate goal should not be to enable LLMs to solve
tasks, their failures often occur in situations that    simple math problems, which can be simply done
are challenging for humans as well. This provides       with other programs. When conducting relevant
some evidence that language models may “reason”         research, it is essential to ask whether the specific
in a way that is similar to human reasoning.            task being tackled is meaningful and whether the
LLMs are still unskilled at complex reasoning.          proposed method can be generalized to more real-
Although LLMs seem to possess impressive rea-           istic tasks and applications.
soning capabilities with the techniques described       Are language models really able to reason?
in §3, they still struggle with more complex rea-       There are several indications that LLMs are able
soning tasks or those involving implicature, accord-    to reason, including 1) high performance on vari-
ing to studies such as Valmeekam et al. (2022);         ous tasks requiring reasoning (Suzgun et al., 2022);
                                                    1056
2) the ability to reason step-by-step with chain-               While techniques like chain-of-thought prompt-
of-thought prompting (Wei et al., 2022b); and 3)                ing (Wei et al., 2022b) may help to elicit reasoning
the reflection of human-like content effects on rea-            abilities in large language models, they cannot en-
soning (Dasgupta et al., 2022). However, these                  able the models to solve tasks beyond their current
findings are not sufficient to conclude that LLMs               capabilities. To truly enhance reasoning in LLMs,
can truly reason. For 1), it is not clear whether the           we need to utilize training data, model architecture,
models are making predictions based on reasoning                and optimization objectives that are designed to
or heuristics (Patel et al., 2021). For many existing           encourage reasoning. For example, finetuning a
benchmarks on reasoning, actually, we can design                model with a dataset including CoT data has been
a program with heuristic rules to achieve very high             shown to improve reasoning (Chung et al., 2022),
performance. We usually do not think a program                  and models can also self-improve through the pro-
relying on heuristic rules is capable of reasoning.             cess of bootstrapping their reasoning (Zelikman
For 2), although the models seem to reason step-                et al., 2022; Huang et al., 2022a). There is still
by-step, the generated rationales may be incorrect              much research that needs to be done in this area,
and inconsistent. It is possible that the models are            and we look forward to future progress in improv-
“generating reasoning-like response” rather than                ing reasoning in large language models.
“reasoning step-by-step”. For 3), while LLMs dis-
play some human-like reasoning patterns, this does              7   Conclusion
not necessarily mean that they behave like humans.
                                                                In this paper, we have provided a detailed and up-
   Additionally, there are several observations that            to-date review of the current state of knowledge
suggest LLMs may not be capable of reasoning:                   on reasoning in large language models. We have
1) LLMs still struggle with tasks that require com-             discussed techniques for improving and eliciting
plex reasoning (Valmeekam et al., 2022; Han et al.,             reasoning in LLMs, methods and benchmarks for
2022a; Ruis et al., 2022). If LLMs are really de-               evaluating reasoning abilities, and the findings and
cent reasoners, they should handle tasks that can               implications of previous studies in this topic. While
be simply solved by humans through reasoning;                   LLMs have made significant progress in natural
2) LLMs make mistakes in their reasoning, as ex-                language processing and related fields, it remains
plained above; 3)#4 The performance of LLMs on                  unclear to what extent they are capable of true rea-
downstream tasks has been found to be sensitive to              soning or whether they are simply using memorized
the frequency of certain terms, such as numbers, in             patterns and heuristics to solve problems. Further
the training data (Razeghi et al., 2022; Jung et al.,           research is needed to fully understand the reason-
2022), which would not be expected if the models                ing abilities of LLMs, improve LLMs’ reasoning
were solving mathematical problems through rea-                 capabilities, and determine their potential for use
soning; 4)# Language models have been found to                  in a variety of applications. We hope that this paper
struggle with associating relevant information that             will serve as a useful overview of the current state
they have memorized (Huang et al., 2022c).                      of the field and stimulate further discussion and
   Overall, it is still too early to draw a conclusion          research on this interesting and important topic.
about the proposed question. In fact, there is also an
ongoing debate about whether language models can                Limitations
actually understand language or capture meaning
(Bender and Koller, 2020; Li et al., 2021; Manning,             In this paper, we provide an overview of the current
2022; Piantasodi and Hill, 2022). Further in-depth              state of knowledge on reasoning in large language
analysis of factors such as training data, model                models. Reasoning is a broad concept that encom-
architecture, and optimization objectives is needed,            passes various forms, making it impractical to sum-
as well as the development of better benchmarks                 marize all related work in a single paper. Therefore,
for measuring the reasoning capabilities of LLMs.               we focus on deductive reasoning, as it is the most
However, it is clear that the current models are not            commonly studied in the literature. Other forms of
yet capable of robust reasoning.                                reasoning such as inductive reasoning (Yang et al.,
                                                                2022; Misra et al., 2022, inter alia) and abductive
Improving reasoning capabilities of LLMs.                       reasoning (Wiegreffe et al., 2022; Lampinen et al.,
    4 #
        indicates the finding has not been carefully examined   2022; Jung et al., 2022, inter alia) may not be dis-
in language models with more than 100 billion parameters.       cussed in depth.
                                                            1057
   Additionally, given the rapid evolution and sig-         on reasoning, hallucination, and interactivity. ArXiv
nificance of reasoning within large language mod-           preprint, abs/2302.04023.
els, it is crucial to note that new contributions may    Emily M. Bender and Alexander Koller. 2020. Climbing
have emerged in the field concurrent with the writ-        towards NLU: On meaning, form, and understanding
ing of this paper. An additional resource to consider      in the age of data. In Proceedings of the 58th Annual
is a parallel survey by Qiao et al. (2022), which em-      Meeting of the Association for Computational Lin-
                                                           guistics, pages 5185–5198, Online. Association for
phasizes reasoning via language model prompting.           Computational Linguistics.
Our coverage may not extend to papers released
during or after 2023 such as evaluation on Chat-         Prajjwal Bhargava and Vincent Ng. 2022. Common-
                                                           sense knowledge reasoning and generation with pre-
GPT (Bang et al., 2023; Zheng et al., 2023). As            trained language models: A survey. Proceedings of
such, we recommend readers to check the papers             the AAAI Conference on Artificial Intelligence.
that cite this survey for a more comprehensive and
                                                         Rishi Bommasani, Drew A Hudson, Ehsan Adeli,
updated understanding of this field.                       Russ Altman, Simran Arora, Sydney von Arx,
                                                           Michael S Bernstein, Jeannette Bohg, Antoine Bosse-
Acknowledgements                                           lut, Emma Brunskill, et al. 2021. On the opportuni-
                                                           ties and risks of foundation models. ArXiv preprint,
We would like to thank Jason Wei (OpenAI) and              abs/2108.07258.
Denny Zhou (Google DeepMind) for their valu-
able advice and constructive feedback on this work.      Hugo Bronkhorst, Gerrit Roorda, Cor Suhre, and Mar-
                                                           tin Goedhart. 2020. Logical reasoning in formal
This material is based upon work supported by              and everyday reasoning tasks. International Journal
the National Science Foundation IIS 16-19302 and           of Science and Mathematics Education, 18(8):1673–
IIS 16-33755, Zhejiang University ZJU Research             1694.
083650, IBM-Illinois Center for Cognitive Com-
                                                         Tom B. Brown, Benjamin Mann, Nick Ryder, Melanie
puting Systems Research (C3SR) and IBM-Illinois            Subbiah, Jared Kaplan, Prafulla Dhariwal, Arvind
Discovery Accelerator Institute (IIDAI), gift grants       Neelakantan, Pranav Shyam, Girish Sastry, Amanda
from eBay and Microsoft Azure, UIUC OVCR                   Askell, Sandhini Agarwal, Ariel Herbert-Voss,
CCIL Planning Grant 434S34, UIUC CSBS Small                Gretchen Krueger, Tom Henighan, Rewon Child,
                                                           Aditya Ramesh, Daniel M. Ziegler, Jeffrey Wu,
Grant 434C8U, and UIUC New Frontiers Initiative.           Clemens Winter, Christopher Hesse, Mark Chen, Eric
Any opinions, findings, and conclusions or recom-          Sigler, Mateusz Litwin, Scott Gray, Benjamin Chess,
mendations expressed in this publication are those         Jack Clark, Christopher Berner, Sam McCandlish,
of the author(s) and do not necessarily reflect the        Alec Radford, Ilya Sutskever, and Dario Amodei.
                                                           2020. Language models are few-shot learners. In Ad-
views of the funding agencies.                             vances in Neural Information Processing Systems 33:
                                                           Annual Conference on Neural Information Process-
                                                           ing Systems 2020, NeurIPS 2020, December 6-12,
References                                                 2020, virtual.
Aida Amini, Saadia Gabriel, Shanchuan Lin, Rik           Mark Chen, Jerry Tworek, Heewoo Jun, Qiming
  Koncel-Kedziorski, Yejin Choi, and Hannaneh Ha-         Yuan, Henrique Ponde de Oliveira Pinto, Jared Ka-
  jishirzi. 2019. MathQA: Towards interpretable math      plan, Harri Edwards, Yuri Burda, Nicholas Joseph,
  word problem solving with operation-based for-          Greg Brockman, et al. 2021. Evaluating large lan-
  malisms. In Proceedings of the 2019 Conference          guage models trained on code. ArXiv preprint,
  of the North American Chapter of the Association for    abs/2107.03374.
  Computational Linguistics: Human Language Tech-
  nologies, Volume 1 (Long and Short Papers), pages      Wenhu Chen. 2022. Large language models are few (1)-
  2357–2367, Minneapolis, Minnesota. Association for       shot table reasoners. ArXiv preprint, abs/2210.06710.
  Computational Linguistics.
                                                         Wenhu Chen, Xueguang Ma, Xinyi Wang, and
Cem Anil, Yuhuai Wu, Anders Andreassen, Aitor             William W Cohen. 2022. Program of thoughts
  Lewkowycz, Vedant Misra, Vinay Ramasesh, Am-            prompting: Disentangling computation from reason-
  brose Slone, Guy Gur-Ari, Ethan Dyer, and Behnam        ing for numerical reasoning tasks. ArXiv preprint,
  Neyshabur. 2022. Exploring length generaliza-           abs/2211.12588.
  tion in large language models. ArXiv preprint,
  abs/2207.04901.                                        Aakanksha Chowdhery, Sharan Narang, Jacob Devlin,
                                                           Maarten Bosma, Gaurav Mishra, Adam Roberts,
Yejin Bang, Samuel Cahyawijaya, Nayeon Lee, Wen-           Paul Barham, Hyung Won Chung, Charles Sutton,
  liang Dai, Dan Su, Bryan Wilie, Holy Lovenia, Ziwei      Sebastian Gehrmann, et al. 2022. Palm: Scaling
  Ji, Tiezheng Yu, Willy Chung, et al. 2023. A multi-      language modeling with pathways. ArXiv preprint,
  task, multilingual, multimodal evaluation of chatgpt     abs/2204.02311.

                                                     1058
Hyung Won Chung, Le Hou, Shayne Longpre, Bar-            Yao Fu, Hao Peng, and Tushar Khot. 2022a. How does
  ret Zoph, Yi Tay, William Fedus, Eric Li, Xuezhi         gpt obtain its ability? tracing emergent abilities of
  Wang, Mostafa Dehghani, Siddhartha Brahma, et al.        language models to their sources.
  2022. Scaling instruction-finetuned language models.
  ArXiv preprint, abs/2210.11416.                        Yao Fu, Hao Peng, Ashish Sabharwal, Peter Clark,
                                                           and Tushar Khot. 2022b. Complexity-based prompt-
Peter Clark, Isaac Cowhey, Oren Etzioni, Tushar Khot,      ing for multi-step reasoning.    ArXiv preprint,
  Ashish Sabharwal, Carissa Schoenick, and Oyvind          abs/2210.00720.
  Tafjord. 2018. Think you have solved question an-
  swering? try arc, the ai2 reasoning challenge. ArXiv   Kathleen M Galotti. 1989. Approaches to studying for-
  preprint, abs/1803.05457.                                mal and everyday reasoning. Psychological bulletin,
                                                           105(3):331.
Karl Cobbe, Vineet Kosaraju, Mohammad Bavar-
  ian, Jacob Hilton, Reiichiro Nakano, Christopher       Luyu Gao, Aman Madaan, Shuyan Zhou, Uri Alon,
  Hesse, and John Schulman. 2021. Training veri-           Pengfei Liu, Yiming Yang, Jamie Callan, and Gra-
  fiers to solve math word problems. ArXiv preprint,       ham Neubig. 2022. Pal: Program-aided language
  abs/2110.14168.                                          models. ArXiv preprint, abs/2211.10435.

Antonia Creswell and Murray Shanahan. 2022. Faith-       Mor Geva, Daniel Khashabi, Elad Segal, Tushar Khot,
  ful reasoning using large language models. ArXiv        Dan Roth, and Jonathan Berant. 2021. Did aristotle
  preprint, abs/2208.14271.                               use a laptop? a question answering benchmark with
                                                          implicit reasoning strategies. Transactions of the
Antonia Creswell, Murray Shanahan, and Irina Higgins.     Association for Computational Linguistics, 9:346–
  2022. Selection-inference: Exploiting large language    361.
  models for interpretable logical reasoning. ArXiv
  preprint, abs/2205.09712.                              Olga Golovneva, Moya Chen, Spencer Poff, Martin
                                                           Corredor, Luke Zettlemoyer, Maryam Fazel-Zarandi,
Ishita Dasgupta, Andrew K Lampinen, Stephanie CY           and Asli Celikyilmaz. 2022. Roscoe: A suite of
   Chan, Antonia Creswell, Dharshan Kumaran,               metrics for scoring step-by-step reasoning. ArXiv
   James L McClelland, and Felix Hill. 2022. Lan-          preprint, abs/2212.07919.
   guage models show human-like content effects on
   reasoning. ArXiv preprint, abs/2207.07051.            Simeng Han, Hailey Schoelkopf, Yilun Zhao, Zhenting
                                                           Qi, Martin Riddell, Luke Benson, Lucy Sun, Eka-
Jacob Devlin, Ming-Wei Chang, Kenton Lee, and              terina Zubova, Yujie Qiao, Matthew Burtell, et al.
   Kristina Toutanova. 2019. BERT: Pre-training of         2022a. Folio: Natural language reasoning with first-
   deep bidirectional transformers for language under-     order logic. ArXiv preprint, abs/2209.00840.
   standing. In Proceedings of the 2019 Conference of
   the North American Chapter of the Association for     Simon Jerome Han, Keith Ransom, Andrew Perfors,
  Computational Linguistics: Human Language Tech-          and Charles Kemp. 2022b. Human-like property
   nologies, Volume 1 (Long and Short Papers), pages       induction is a challenge for large language models.
  4171–4186, Minneapolis, Minnesota. Association for
   Computational Linguistics.                            Hangfeng He, Hongming Zhang, and Dan Roth. 2023.
                                                           Rethinking with retrieval: Faithful large language
David Dohan, Winnie Xu, Aitor Lewkowycz, Ja-               model inference. ArXiv preprint, abs/2301.00303.
  cob Austin, David Bieber, Raphael Gontijo Lopes,
  Yuhuai Wu, Henryk Michalewski, Rif A Saurous,          Chadi Helwe, Chloé Clavel, and Fabian M Suchanek.
  Jascha Sohl-Dickstein, et al. 2022. Language model       2021. Reasoning with transformer-based models:
  cascades. ArXiv preprint, abs/2207.10342.                Deep learning, but shallow reasoning. In 3rd Confer-
                                                           ence on Automated Knowledge Base Construction.
Andrew Drozdov, Nathanael Schärli, Ekin Akyürek,
  Nathan Scales, Xinying Song, Xinyun Chen, Olivier      Dan Hendrycks, Collin Burns, Saurav Kadavath, Akul
  Bousquet, and Denny Zhou. 2022. Compositional            Arora, Steven Basart, Eric Tang, Dawn Song, and
  semantic parsing with large language models. ArXiv       Jacob Steinhardt. 2021. Measuring mathematical
  preprint, abs/2209.15003.                                problem solving with the math dataset. In Proceed-
                                                           ings of the Neural Information Processing Systems
Dheeru Dua, Shivanshu Gupta, Sameer Singh, and             Track on Datasets and Benchmarks, volume 1.
  Matt Gardner. 2022. Successive prompting for
  decomposing complex questions. ArXiv preprint,         Jiaxin Huang, Shixiang Shane Gu, Le Hou, Yuexin
  abs/2212.04092.                                           Wu, Xuezhi Wang, Hongkun Yu, and Jiawei Han.
                                                            2022a. Large language models can self-improve.
Ward Edwards. 1954. The theory of decision making.          ArXiv preprint, abs/2210.11610.
 Psychological bulletin, 51(4):380.
                                                         Jie Huang, Kevin Chang, Jinjun Xiong, and Wen-mei
Ronald Fagin, Joseph Y Halpern, Yoram Moses, and            Hwu. 2022b. Open relation modeling: Learning
  Moshe Vardi. 2004. Reasoning about knowledge.             to define relations between entities. In Findings of
  MIT press.                                                the Association for Computational Linguistics: ACL

                                                     1059
  2022, pages 297–308, Dublin, Ireland. Association        Takeshi Kojima, Shixiang Shane Gu, Machel Reid, Yu-
  for Computational Linguistics.                             taka Matsuo, and Yusuke Iwasawa. 2022. Large lan-
                                                             guage models are zero-shot reasoners. In Advances
Jie Huang, Hanyin Shao, and Kevin Chen-Chuan Chang.          in Neural Information Processing Systems.
   2022c. Are large pre-trained language models leak-
   ing your personal information? In Findings of the       Brenden M. Lake and Marco Baroni. 2018. General-
   Association for Computational Linguistics: EMNLP          ization without systematicity: On the compositional
   2022, pages 2038–2047, Abu Dhabi, United Arab             skills of sequence-to-sequence recurrent networks. In
   Emirates. Association for Computational Linguistics.      Proceedings of the 35th International Conference on
                                                             Machine Learning, ICML 2018, Stockholmsmässan,
Jie Huang, Kerui Zhu, Kevin Chen-Chuan Chang, Jinjun         Stockholm, Sweden, July 10-15, 2018, volume 80 of
   Xiong, and Wen-mei Hwu. 2022d. DEER: Descrip-             Proceedings of Machine Learning Research, pages
   tive knowledge graph for explaining entity relation-      2879–2888. PMLR.
   ships. In Proceedings of the 2022 Conference on
   Empirical Methods in Natural Language Processing,       Andrew K Lampinen, Ishita Dasgupta, Stephanie CY
   pages 6686–6698, Abu Dhabi, United Arab Emirates.         Chan, Kory Matthewson, Michael Henry Tessler, An-
   Association for Computational Linguistics.                tonia Creswell, James L McClelland, Jane X Wang,
                                                             and Felix Hill. 2022. Can language models learn
Wenlong Huang, Pieter Abbeel, Deepak Pathak, and             from explanations in context? In Findings of the
 Igor Mordatch. 2022e. Language models as zero-              Association for Computational Linguistics: EMNLP
 shot planners: Extracting actionable knowledge for          2022.
 embodied agents. In Proceedings of the 39th Inter-
 national Conference on Machine Learning, volume           Edward H Levi. 2013. An introduction to legal reason-
 162 of Proceedings of Machine Learning Research,            ing. University of Chicago Press.
 pages 9118–9147. PMLR.
                                                           Aitor Lewkowycz, Anders Andreassen, David Dohan,
Wenlong Huang, Fei Xia, Ted Xiao, Harris Chan, Jacky         Ethan Dyer, Henryk Michalewski, Vinay Ramasesh,
  Liang, Pete Florence, Andy Zeng, Jonathan Tompson,         Ambrose Slone, Cem Anil, Imanol Schlag, Theo
  Igor Mordatch, Yevgen Chebotar, et al. 2022f. Inner        Gutman-Solo, et al. 2022. Solving quantitative
  monologue: Embodied reasoning through planning             reasoning problems with language models. ArXiv
 with language models. In 2022 Conference on Robot           preprint, abs/2206.14858.
 Learning.                                                 Belinda Z. Li, Maxwell Nye, and Jacob Andreas. 2021.
                                                             Implicit representations of meaning in neural lan-
Michael Huth and Mark Ryan. 2004. Logic in Computer          guage models. In Proceedings of the 59th Annual
  Science: Modelling and reasoning about systems.            Meeting of the Association for Computational Lin-
  Cambridge university press.                                guistics and the 11th International Joint Conference
                                                             on Natural Language Processing (Volume 1: Long
Jaehun Jung, Lianhui Qin, Sean Welleck, Faeze Brah-
                                                             Papers), pages 1813–1827, Online. Association for
   man, Chandra Bhagavatula, Ronan Le Bras, and
                                                             Computational Linguistics.
  Yejin Choi. 2022. Maieutic prompting: Logically
   consistent reasoning with recursive explanations. The   Shiyang Li, Jianshu Chen, Yelong Shen, Zhiyu Chen,
  2022 Conference on Empirical Methods for Natural           Xinlu Zhang, Zekun Li, Hong Wang, Jing Qian,
  Language Processing.                                       Baolin Peng, Yi Mao, et al. 2022a. Explanations
                                                             from large language models make small reasoners
Seyed Mehran Kazemi, Najoung Kim, Deepti Bhatia,             better. ArXiv preprint, abs/2210.06726.
  Xin Xu, and Deepak Ramachandran. 2022. Lam-
  bada: Backward chaining for automated reasoning in       Yifei Li, Zeqi Lin, Shizhuo Zhang, Qiang Fu, Bei Chen,
  natural language. ArXiv preprint, abs/2212.13894.          Jian-Guang Lou, and Weizhu Chen. 2022b. On the
                                                              advance of making language models better reasoners.
Daniel Keysers, Nathanael Schärli, Nathan Scales,            ArXiv preprint, abs/2206.02336.
  Hylke Buisman, Daniel Furrer, Sergii Kashubin,
  Nikola Momchev, Danila Sinopalnikov, Lukasz              Bill Yuchen Lin, Wangchunshu Zhou, Ming Shen, Pei
  Stafiniak, Tibor Tihon, Dmitry Tsarkov, Xiao Wang,         Zhou, Chandra Bhagavatula, Yejin Choi, and Xiang
  Marc van Zee, and Olivier Bousquet. 2020. Measur-          Ren. 2020. CommonGen: A constrained text gen-
  ing compositional generalization: A comprehensive          eration challenge for generative commonsense rea-
  method on realistic data. In 8th International Confer-     soning. In Findings of the Association for Computa-
  ence on Learning Representations, ICLR 2020, Addis         tional Linguistics: EMNLP 2020, pages 1823–1840,
  Ababa, Ethiopia, April 26-30, 2020. OpenReview.net.        Online. Association for Computational Linguistics.

Tushar Khot, Harsh Trivedi, Matthew Finlayson, Yao         Wang Ling, Dani Yogatama, Chris Dyer, and Phil Blun-
  Fu, Kyle Richardson, Peter Clark, and Ashish Sab-          som. 2017. Program induction by rationale genera-
  harwal. 2022. Decomposed prompting: A modular              tion: Learning to solve and explain algebraic word
  approach for solving complex tasks. ArXiv preprint,        problems. In Proceedings of the 55th Annual Meet-
  abs/2210.02406.                                            ing of the Association for Computational Linguistics

                                                       1060
  (Volume 1: Long Papers), pages 158–167, Vancouver,        Kanishka Misra, Julia Taylor Rayz, and Allyson Et-
  Canada. Association for Computational Linguistics.          tinger. 2022. A property induction framework
                                                              for neural language models.      ArXiv preprint,
Chenzhengyi Liu, Jie Huang, Kerui Zhu, and Kevin              abs/2205.06910.
  Chen-Chuan Chang. 2022a. Dimongen: Diver-
  sified generative commonsense reasoning for ex-           Melanie Mitchell. 2021. Abstraction and analogy-
  plaining concept relationships. ArXiv preprint,            making in artificial intelligence. Annals of the New
  abs/2212.10545.                                            York Academy of Sciences, 1505(1):79–101.

Jiachang Liu, Dinghan Shen, Yizhe Zhang, Bill Dolan,        Linyong Nan, Chiachun Hsieh, Ziming Mao, Xi Victoria
   Lawrence Carin, and Weizhu Chen. 2022b. What               Lin, Neha Verma, Rui Zhang, Wojciech Kryściński,
   makes good in-context examples for GPT-3? In               Hailey Schoelkopf, Riley Kong, Xiangru Tang,
   Proceedings of Deep Learning Inside Out (DeeLIO            Mutethia Mutuma, Ben Rosand, Isabel Trindade,
   2022): The 3rd Workshop on Knowledge Extrac-               Renusree Bandaru, Jacob Cunningham, Caiming
   tion and Integration for Deep Learning Architectures,      Xiong, Dragomir Radev, and Dragomir Radev. 2022.
   pages 100–114, Dublin, Ireland and Online. Associa-        FeTaQA: Free-form table question answering. Trans-
   tion for Computational Linguistics.                        actions of the Association for Computational Linguis-
                                                              tics, 10:35–49.
Yinhan Liu, Myle Ott, Naman Goyal, Jingfei Du, Man-
  dar Joshi, Danqi Chen, Omer Levy, Mike Lewis,             Maxwell Nye, Anders Johan Andreassen, Guy Gur-Ari,
  Luke Zettlemoyer, and Veselin Stoyanov. 2019.              Henryk Michalewski, Jacob Austin, David Bieber,
  Roberta: A robustly optimized bert pretraining ap-         David Dohan, Aitor Lewkowycz, Maarten Bosma,
  proach. ArXiv preprint, abs/1907.11692.                    David Luan, Charles Sutton, and Augustus Odena.
                                                             2022. Show your work: Scratchpads for interme-
Pan Lu, Swaroop Mishra, Tony Xia, Liang Qiu, Kai-            diate computation with language models. In Deep
  Wei Chang, Song-Chun Zhu, Oyvind Tafjord, Peter            Learning for Code Workshop.
  Clark, and Ashwin Kalyan. 2022. Learn to explain:
  Multimodal reasoning via thought chains for science       OpenAI. 2022. Chatgpt: Optimizing language models
  question answering. In Advances in Neural Informa-          for dialogue. OpenAI.
  tion Processing Systems.
                                                            John Arthur Passmore. 1961. Philosophical reasoning.
Aman Madaan, Shuyan Zhou, Uri Alon, Yiming Yang,
 and Graham Neubig. 2022. Language models of code           Panupong Pasupat and Percy Liang. 2015. Composi-
 are few-shot commonsense learners. In Proceedings            tional semantic parsing on semi-structured tables. In
 of the 2022 Conference on Empirical Methods in               Proceedings of the 53rd Annual Meeting of the As-
 Natural Language Processing (EMNLP).                         sociation for Computational Linguistics and the 7th
                                                              International Joint Conference on Natural Language
Lucie Charlotte Magister, Jonathan Mallinson, Jakub           Processing (Volume 1: Long Papers), pages 1470–
  Adamek, Eric Malmi, and Aliaksei Severyn. 2022.             1480, Beijing, China. Association for Computational
  Teaching small language models to reason. ArXiv             Linguistics.
  preprint, abs/2212.08410.
                                                            Arkil Patel, Satwik Bhattamishra, and Navin Goyal.
Christopher D Manning. 2022. Human language under-            2021. Are NLP models really able to solve simple
  standing & reasoning. Daedalus, 151(2):127–138.             math word problems? In Proceedings of the 2021
                                                              Conference of the North American Chapter of the
Gary Marcus. 2020. The next decade in ai: four steps          Association for Computational Linguistics: Human
  towards robust artificial intelligence. ArXiv preprint,     Language Technologies, pages 2080–2094, Online.
  abs/2002.06177.                                             Association for Computational Linguistics.
Conor McHugh and Jonathan Way. 2018. What is rea-           Ethan Perez, Patrick Lewis, Wen-tau Yih, Kyunghyun
  soning? Mind, 127(505):167–196.                             Cho, and Douwe Kiela. 2020. Unsupervised question
                                                              decomposition for question answering. In Proceed-
Shen-yun Miao, Chao-Chun Liang, and Keh-Yih Su.               ings of the 2020 Conference on Empirical Methods
  2020. A diverse corpus for evaluating and developing        in Natural Language Processing (EMNLP), pages
  English math word problem solvers. In Proceedings           8864–8880, Online. Association for Computational
  of the 58th Annual Meeting of the Association for           Linguistics.
  Computational Linguistics, pages 975–984, Online.
  Association for Computational Linguistics.                Xinyu Pi, Qian Liu, Bei Chen, Morteza Ziyadi, Zeqi Lin,
                                                              Yan Gao, Qiang Fu, Jian-Guang Lou, and Weizhu
Sewon Min, Victor Zhong, Luke Zettlemoyer, and Han-           Chen. 2022. Reasoning like program executors. In
  naneh Hajishirzi. 2019. Multi-hop reading compre-           Proceedings of the 2022 Conference on Empirical
  hension through question decomposition and rescor-          Methods in Natural Language Processing (EMNLP).
  ing. In Proceedings of the 57th Annual Meeting of
  the Association for Computational Linguistics, pages      Steven T Piantasodi and Felix Hill. 2022. Meaning
  6097–6109, Florence, Italy. Association for Compu-          without reference in large language models. ArXiv
  tational Linguistics.                                        preprint, abs/2208.02957.

                                                        1061
Ofir Press, Muru Zhang, Sewon Min, Ludwig Schmidt,          Abulhair Saparov and He He. 2022. Language models
  Noah A Smith, and Mike Lewis. 2022. Measuring               are greedy reasoners: A systematic formal analysis of
  and narrowing the compositionality gap in language          chain-of-thought. ArXiv preprint, abs/2210.01240.
  models. ArXiv preprint, abs/2210.03350.
                                                            Teven Le Scao, Angela Fan, Christopher Akiki, El-
Ben Prystawski, Paul Thibodeau, and Noah Goodman.             lie Pavlick, Suzana Ilić, Daniel Hesslow, Roman
  2022. Psychologically-informed chain-of-thought             Castagné, Alexandra Sasha Luccioni, François Yvon,
  prompts for metaphor understanding in large lan-            Matthias Gallé, et al. 2022. Bloom: A 176b-
  guage models. ArXiv preprint, abs/2209.08141.               parameter open-access multilingual language model.
                                                              ArXiv preprint, abs/2211.05100.
Shuofei Qiao, Yixin Ou, Ningyu Zhang, Xiang Chen,
  Yunzhi Yao, Shumin Deng, Chuanqi Tan, Fei Huang,          Freda Shi, Mirac Suzgun, Markus Freitag, Xuezhi Wang,
  and Huajun Chen. 2022. Reasoning with lan-                   Suraj Srivats, Soroush Vosoughi, Hyung Won Chung,
  guage model prompting: A survey. ArXiv preprint,            Yi Tay, Sebastian Ruder, Denny Zhou, et al. 2022.
  abs/2212.09597.                                              Language models are multilingual chain-of-thought
                                                               reasoners. ArXiv preprint, abs/2210.03057.
Alec Radford, Karthik Narasimhan, Tim Salimans, Ilya
  Sutskever, et al. 2018. Improving language under-         Kumar Shridhar, Alessandro Stolfo, and Mrinmaya
  standing by generative pre-training.                        Sachan. 2022. Distilling multi-step reasoning ca-
                                                              pabilities of large language models into smaller mod-
Alec Radford, Jeffrey Wu, Rewon Child, David Luan,            els via semantic decompositions. ArXiv preprint,
  Dario Amodei, Ilya Sutskever, et al. 2019. Language         abs/2212.00193.
  models are unsupervised multitask learners. OpenAI
                                                            Chan Hee Song, Jiaman Wu, Clayton Washington,
  blog, 1(8):9.
                                                              Brian M Sadler, Wei-Lun Chao, and Yu Su. 2022.
Jack W Rae, Sebastian Borgeaud, Trevor Cai, Katie             Llm-planner: Few-shot grounded planning for em-
   Millican, Jordan Hoffmann, Francis Song, John              bodied agents with large language models. ArXiv
  Aslanides, Sarah Henderson, Roman Ring, Susan-              preprint, abs/2212.04088.
   nah Young, et al. 2021. Scaling language models:         Aarohi Srivastava, Abhinav Rastogi, Abhishek Rao,
   Methods, analysis & insights from training gopher.         Abu Awal Md Shoeb, Abubakar Abid, Adam Fisch,
  ArXiv preprint, abs/2112.11446.                             Adam R Brown, Adam Santoro, Aditya Gupta, Adrià
                                                              Garriga-Alonso, et al. 2022. Beyond the imitation
Colin Raffel, Noam Shazeer, Adam Roberts, Katherine           game: Quantifying and extrapolating the capabilities
  Lee, Sharan Narang, Michael Matena, Yanqi Zhou,             of language models. ArXiv preprint, abs/2206.04615.
  Wei Li, Peter J Liu, et al. 2020. Exploring the limits
  of transfer learning with a unified text-to-text trans-   Mirac Suzgun, Nathan Scales, Nathanael Schärli, Se-
  former. J. Mach. Learn. Res., 21(140):1–67.                 bastian Gehrmann, Yi Tay, Hyung Won Chung,
                                                              Aakanksha Chowdhery, Quoc V Le, Ed H Chi, Denny
Nazneen Fatema Rajani, Bryan McCann, Caiming                  Zhou, et al. 2022. Challenging big-bench tasks and
  Xiong, and Richard Socher. 2019. Explain your-              whether chain-of-thought can solve them. ArXiv
  self! leveraging language models for commonsense            preprint, abs/2210.09261.
  reasoning. In Proceedings of the 57th Annual Meet-
  ing of the Association for Computational Linguistics,     Alon Talmor and Jonathan Berant. 2018. The web as
  pages 4932–4942, Florence, Italy. Association for           a knowledge-base for answering complex questions.
  Computational Linguistics.                                  In Proceedings of the 2018 Conference of the North
                                                              American Chapter of the Association for Computa-
Yasaman Razeghi, Robert L Logan IV, Matt Gardner,             tional Linguistics: Human Language Technologies,
  and Sameer Singh. 2022. Impact of pretraining term          Volume 1 (Long Papers), pages 641–651, New Or-
  frequencies on few-shot reasoning. ArXiv preprint,          leans, Louisiana. Association for Computational Lin-
  abs/2202.07206.                                             guistics.
Subhro Roy and Dan Roth. 2015. Solving general arith-       Alon Talmor, Jonathan Herzig, Nicholas Lourie, and
  metic word problems. In Proceedings of the 2015             Jonathan Berant. 2019. CommonsenseQA: A ques-
  Conference on Empirical Methods in Natural Lan-             tion answering challenge targeting commonsense
  guage Processing, pages 1743–1752, Lisbon, Portu-           knowledge. In Proceedings of the 2019 Conference
  gal. Association for Computational Linguistics.             of the North American Chapter of the Association for
                                                              Computational Linguistics: Human Language Tech-
Laura Ruis, Akbir Khan, Stella Biderman, Sara Hooker,         nologies, Volume 1 (Long and Short Papers), pages
  Tim Rocktäschel, and Edward Grefenstette. 2022.             4149–4158, Minneapolis, Minnesota. Association for
  Large language models are not zero-shot communi-            Computational Linguistics.
  cators. ArXiv preprint, abs/2210.14986.
                                                            Alon Talmor, Oyvind Tafjord, Peter Clark, Yoav Gold-
Jacob Russin, Randall C O’Reilly, and Yoshua Bengio.          berg, and Jonathan Berant. 2020. Leap-of-thought:
   2020. Deep learning needs a prefrontal cortex. Work        Teaching pre-trained models to systematically rea-
   Bridging AI Cogn Sci, 107:603–616.                         son over implicit knowledge. In Advances in Neural

                                                        1062
  Information Processing Systems 33: Annual Confer-        Zonglin Yang, Li Dong, Xinya Du, Hao Cheng, Erik
  ence on Neural Information Processing Systems 2020,        Cambria, Xiaodong Liu, Jianfeng Gao, and Furu
  NeurIPS 2020, December 6-12, 2020, virtual.                Wei. 2022. Language models as inductive reason-
                                                             ers. ArXiv preprint, abs/2212.10923.
Ross Taylor, Marcin Kardas, Guillem Cucurull, Thomas
  Scialom, Anthony Hartshorn, Elvis Saravia, Andrew        Xi Ye and Greg Durrett. 2022. The unreliability of
  Poulton, Viktor Kerkez, and Robert Stojnic. 2022.          explanations in few-shot prompting for textual rea-
  Galactica: A large language model for science. ArXiv       soning. Advances in neural information processing
  preprint, abs/2211.09085.                                  systems.

Karthik Valmeekam, Alberto Olmo, Sarath Sreedharan,        Ping Yu, Tianlu Wang, Olga Golovneva, Badr
  and Subbarao Kambhampati. 2022. Large language             Alkhamissy, Gargi Ghosh, Mona Diab, and Asli Ce-
  models still can’t plan (a benchmark for llms on plan-     likyilmaz. 2022. Alert: Adapting language models
  ning and reasoning about change). In NeurIPS 2022          to reasoning tasks. ArXiv preprint, abs/2212.08286.
  Foundation Models for Decision Making Workshop.
                                                           Eric Zelikman, Yuhuai Wu, Jesse Mu, and Noah Good-
Boshi Wang, Xiang Deng, and Huan Sun. 2022a. Itera-           man. 2022. STar: Bootstrapping reasoning with rea-
  tively prompt pre-trained language models for chain         soning. In Advances in Neural Information Process-
  of thought. In The 2022 Conference on Empirical             ing Systems.
  Methods for Natural Language Processing.
                                                           Susan Zhang, Stephen Roller, Naman Goyal, Mikel
Boshi Wang, Sewon Min, Xiang Deng, Jiaming Shen,             Artetxe, Moya Chen, Shuohui Chen, Christopher De-
  You Wu, Luke Zettlemoyer, and Huan Sun. 2022b.             wan, Mona Diab, Xian Li, Xi Victoria Lin, et al.
  Towards understanding chain-of-thought prompting:          2022a. Opt: Open pre-trained transformer language
  An empirical study of what matters. ArXiv preprint,        models. ArXiv preprint, abs/2205.01068.
  abs/2212.10001.
                                                           Zhuosheng Zhang, Aston Zhang, Mu Li, and Alex
Xuezhi Wang, Jason Wei, Dale Schuurmans, Quoc Le,            Smola. 2022b. Automatic chain of thought prompt-
  Ed Chi, and Denny Zhou. 2022c. Self-consistency            ing in large language models. ArXiv preprint,
  improves chain of thought reasoning in language            abs/2210.03493.
  models. ArXiv preprint, abs/2203.11171.                  Shen Zheng, Jie Huang, and Kevin Chen-Chuan Chang.
                                                             2023. Why does chatgpt fall short in providing truth-
Peter C Wason. 1968. Reasoning about a rule. Quar-
                                                             ful answers? ArXiv preprint, abs/2304.10513.
  terly journal of experimental psychology, 20(3):273–
  281.                                                     Denny Zhou, Nathanael Schärli, Le Hou, Jason Wei,
                                                             Nathan Scales, Xuezhi Wang, Dale Schuurmans,
Peter Cathcart Wason and Philip Nicholas Johnson-            Olivier Bousquet, Quoc Le, and Ed Chi. 2022a.
  Laird. 1972. Psychology of reasoning: Structure            Least-to-most prompting enables complex reason-
  and content, volume 86. Harvard University Press.          ing in large language models. ArXiv preprint,
                                                             abs/2205.10625.
Jason Wei, Yi Tay, Rishi Bommasani, Colin Raffel,
   Barret Zoph, Sebastian Borgeaud, Dani Yogatama,         Fan Zhou, Haoyu Dong, Qian Liu, Zhoujun Cheng,
   Maarten Bosma, Denny Zhou, Donald Metzler, et al.         Shi Han, and Dongmei Zhang. 2022b. Reflection of
   2022a. Emergent abilities of large language models.       thought: Inversely eliciting numerical reasoning in
  Transactions on Machine Learning Research.                 language models via solving linear systems. ArXiv
                                                             preprint, abs/2210.05075.
Jason Wei, Xuezhi Wang, Dale Schuurmans, Maarten
   Bosma, brian ichter, Fei Xia, Ed H. Chi, Quoc V Le,     Hattie Zhou, Azade Nova, Hugo Larochelle, Aaron
   and Denny Zhou. 2022b. Chain of thought prompt-           Courville, Behnam Neyshabur, and Hanie Sedghi.
   ing elicits reasoning in large language models. In        2022c. Teaching algorithmic reasoning via in-
  Advances in Neural Information Processing Systems.         context learning. ArXiv preprint, abs/2211.09066.
Yixuan Weng, Minjun Zhu, Shizhu He, Kang Liu,              Corinne Zimmerman. 2000. The development of
  and Jun Zhao. 2022. Large language models are              scientific reasoning skills. Developmental review,
  reasoners with self-verification. ArXiv preprint,          20(1):99–149.
  abs/2212.09561.

Sarah Wiegreffe, Jack Hessel, Swabha Swayamdipta,
  Mark Riedl, and Yejin Choi. 2022. Reframing
  human-AI collaboration for generating free-text ex-
  planations. In Proceedings of the 2022 Conference
  of the North American Chapter of the Association
  for Computational Linguistics: Human Language
  Technologies, pages 632–658, Seattle, United States.
  Association for Computational Linguistics.

                                                       1063
    ACL 2023 Responsible NLP Checklist
A For every submission:
    3 A1. Did you describe the limitations of your work?
    
      See the limitation section

     A2. Did you discuss any potential risks of your work?
      Not applicable. Left blank.
    3 A3. Do the abstract and introduction summarize the paper’s main claims?
    
      See the abstract and introduction section
    3 A4. Have you used AI writing assistants when working on this paper?
    
      We wrote part of the appendix with ChatGPT assistance (e.g., to generate an initial description for
      commonsense reasoning). The generated text is carefully revised and examined by the authors.

B  Did you use or create scientific artifacts?
    Not applicable. Left blank.

     B1. Did you cite the creators of artifacts you used?
      Not applicable. Left blank.

     B2. Did you discuss the license or terms for use and / or distribution of any artifacts?
      Not applicable. Left blank.

     B3. Did you discuss if your use of existing artifact(s) was consistent with their intended use, provided
      that it was specified? For the artifacts you create, do you specify intended use and whether that is
      compatible with the original access conditions (in particular, derivatives of data accessed for research
      purposes should not be used outside of research contexts)?
      Not applicable. Left blank.

     B4. Did you discuss the steps taken to check whether the data that was collected / used contains any
      information that names or uniquely identifies individual people or offensive content, and the steps
      taken to protect / anonymize it?
      Not applicable. Left blank.

     B5. Did you provide documentation of the artifacts, e.g., coverage of domains, languages, and
      linguistic phenomena, demographic groups represented, etc.?
      Not applicable. Left blank.

     B6. Did you report relevant statistics like the number of examples, details of train / test / dev splits,
      etc. for the data that you used / created? Even for commonly-used benchmark datasets, include the
      number of examples in train / validation / test splits, as these provide necessary context for a reader
      to understand experimental results. For example, small differences in accuracy on large test sets may
      be significant, while on small test sets they may not be.
      Not applicable. Left blank.

C     
      7 Did you run computational experiments?
    Left blank.

     C1. Did you report the number of parameters in the models used, the total computational budget
      (e.g., GPU hours), and computing infrastructure used?
      No response.
The Responsible NLP Checklist used at ACL 2023 is adopted from NAACL 2022, with the addition of a question on AI writing
assistance.


                                                         1064
     C2. Did you discuss the experimental setup, including hyperparameter search and best-found
      hyperparameter values?
      Not applicable. Left blank.

     C3. Did you report descriptive statistics about your results (e.g., error bars around results, summary
      statistics from sets of experiments), and is it transparent whether you are reporting the max, mean,
      etc. or just a single run?
      Not applicable. Left blank.

     C4. If you used existing packages (e.g., for preprocessing, for normalization, or for evaluation), did
      you report the implementation, model, and parameter settings used (e.g., NLTK, Spacy, ROUGE,
      etc.)?
      Not applicable. Left blank.

D     
      7 Did you use human annotators (e.g., crowdworkers) or research with human participants?
    Left blank.

     D1. Did you report the full text of instructions given to participants, including e.g., screenshots,
      disclaimers of any risks to participants or annotators, etc.?
      Not applicable. Left blank.

     D2. Did you report information about how you recruited (e.g., crowdsourcing platform, students)
      and paid participants, and discuss if such payment is adequate given the participants’ demographic
      (e.g., country of residence)?
      Not applicable. Left blank.

     D3. Did you discuss whether and how consent was obtained from people whose data you’re
      using/curating? For example, if you collected data via crowdsourcing, did your instructions to
      crowdworkers explain how the data would be used?
      Not applicable. Left blank.

     D4. Was the data collection protocol approved (or determined exempt) by an ethics review board?
      Not applicable. Left blank.

     D5. Did you report the basic demographic and geographic characteristics of the annotator population
      that is the source of the data?
      Not applicable. Left blank.




                                                    1065
