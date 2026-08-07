
# STYLE GUIDE — Ciencia de Datos Vault

## Purpose

This file defines the writing, pedagogical, academic, and structural standards for all notes in this vault.

The vault is intended to become a **long-term knowledge base for a university Master's degree in Data Mining and Data Science**.

Its purpose is not only to store class notes.

It must progressively become a coherent technical textbook and reference system that connects:

- Mathematics
    
- Statistics
    
- Algorithms and programming
    
- Data Science
    
- Machine Learning
    
- Data Mining
    
- Databases
    
- Data visualization
    
- Python and its scientific ecosystem
    
- Supporting technologies and tools
    

All generated or modified notes must follow this guide unless the user explicitly requests a different style.

---

# 1. Core principle

Write in a:

> **textbook-oriented, STE-inspired technical style**

with:

> **graduate-level academic depth and beginner-friendly explanations**

The most important rule is:

> **Simplify the explanation, not the knowledge.**

Never reduce the academic content only because it is difficult.

Do not remove:

- mathematics;
    
- derivations;
    
- algorithms;
    
- statistical assumptions;
    
- theoretical distinctions;
    
- edge cases;
    
- limitations;
    
- formal terminology;
    
- implementation details that are academically relevant.
    

Instead, explain them better.

The final note must contain the depth expected from a Master's student, while remaining understandable to someone encountering the concept for the first time.

---

# 2. Model of the reader

Assume that the reader is intelligent and capable of understanding advanced material.

However:

> **Do not assume that the reader already understands the concept being explained.**

Do not treat any non-trivial intermediate step as "obvious."

Do not confuse intelligence with prior knowledge.

A mathematically sophisticated concept can still require a very basic introduction.

When explaining something difficult, assume that the reader may initially ask questions such as:

- What problem are we trying to solve?
    
- Why do we need this?
    
- What does this symbol mean?
    
- Why is this operation valid?
    
- Why are we dividing by this value?
    
- Why do we square this quantity?
    
- Why does this function return this object?
    
- What changed between these two lines of code?
    
- What does the result actually tell me?
    
- Why would I use this instead of another method?
    

Answer these questions before they become obstacles.

---

# 3. Academic depth

These are graduate-level notes.

Do not lower the academic level to make the text easier.

A difficult subject must still be treated with appropriate rigor.

For advanced topics, include the relevant:

- definitions;
    
- notation;
    
- assumptions;
    
- mathematical development;
    
- derivations;
    
- algorithms;
    
- theoretical properties;
    
- interpretation;
    
- limitations;
    
- practical implementation.
    

Do not replace theory with a recipe.

Bad:

> Use this function to calculate the confidence interval.

Better:

Explain:

1. what a confidence interval tries to estimate;
    
2. what uncertainty it represents;
    
3. which sampling distribution is involved;
    
4. which assumptions are required;
    
5. how the interval is constructed;
    
6. how it must be interpreted;
    
7. common incorrect interpretations;
    
8. how to calculate it with Python.
    

The goal is not merely to know **which command to run**.

The goal is to understand **why the command is mathematically and statistically meaningful**.

---

# 4. Preferred pedagogical sequence

For difficult concepts, use the following progression when appropriate:

> **problem → intuition → prerequisites → formal definition → development → example → interpretation → implementation → assumptions → limitations → connections**

Not every note requires every stage.

Use the stages that improve understanding.

## 4.1 Problem

Start by explaining what problem motivates the concept.

Before explaining a tool, method, formula, or algorithm, answer:

> Why does this concept exist?

Example:

Before defining variance, explain why the mean alone cannot describe how dispersed the observations are.

Before explaining `groupby()`, explain why we often need to calculate statistics separately for different groups.

Before explaining gradient descent, explain why some optimization problems cannot be solved conveniently with a closed-form expression.

---

## 4.2 Intuition

Give the simplest correct mental model.

The intuition must help the reader understand the formal explanation that follows.

Do not use an analogy as a substitute for the real concept.

An analogy is a bridge.

It is not the destination.

If an analogy is used, explicitly transition from the analogy to the technical explanation.

---

## 4.3 Prerequisites

Identify concepts required to understand the current topic.

If the prerequisite is simple, explain it briefly.

If it already has a note in the vault, link it.

Example:

> To understand covariance, first recall the idea of deviation from the mean and [[medidas de dispersión]].

Do not unnecessarily repeat an entire prerequisite note.

Do not create conceptual jumps merely to keep the note short.

---

## 4.4 Formal definition

After intuition is established, introduce the correct formal terminology.

Use the terminology expected in textbooks, documentation, academic papers, and professional practice.

Never avoid an important technical term merely because the term is difficult.

Instead:

1. introduce the term;
    
2. define it;
    
3. explain it in plain language;
    
4. continue using the correct term consistently.
    

Example:

> **Agregación** es una operación que resume múltiples observaciones mediante uno o más valores. Calcular la media de cada grupo es una agregación.

After this definition, use **agregación** consistently.

---

## 4.5 Development

Explain how the concept works.

Do not skip intermediate reasoning.

For mathematics, derive results when the derivation is relevant.

For algorithms, explain the sequence of operations.

For code, explain how the library translates the underlying concept into an API.

---

## 4.6 Example

Use a concrete example.

Prefer:

- small datasets;
    
- small numbers;
    
- realistic situations;
    
- examples that can be inspected manually.
    

Show important intermediate steps.

The purpose of the example is to expose the mechanism.

It is not only to demonstrate syntax.

---

## 4.7 Interpretation

Never stop at a numerical result, table, model output, or graph.

Explain what it means.

Bad:

> The correlation is 0.72.

Better:

> The correlation is 0.72. This indicates a relatively strong positive linear association between the variables in this dataset.

Then explain what this result does **not** imply when relevant.

For example:

> Correlation alone does not establish causality.

---

## 4.8 Implementation

When the concept has a computational implementation, connect theory with code.

The order should normally be:

> **concept → implementation**

not:

> **library function → concept**

The reader must understand what Python is implementing.

---

## 4.9 Assumptions and limitations

Explain assumptions when they affect validity or interpretation.

Do not hide assumptions in an advanced footnote if they are necessary to use the method correctly.

Explain what can happen when an assumption fails.

---

## 4.10 Connections

Connect the concept with existing knowledge in the vault.

Useful connections include:

- theoretical prerequisite;
    
- related statistical method;
    
- mathematical foundation;
    
- Python implementation;
    
- visualization;
    
- alternative method;
    
- later application in Machine Learning.
    

Use Obsidian links when the connection provides real navigational or conceptual value.

---

# 5. STE-inspired writing rules

Use Simplified Technical English principles as a writing philosophy.

Do not attempt strict ASD-STE100 compliance.

The objective is clarity, consistency, and low ambiguity.

## Prefer

- direct sentences;
    
- short or medium-length sentences;
    
- one main idea per sentence;
    
- active voice when natural;
    
- concrete verbs;
    
- consistent terminology;
    
- explicit references;
    
- logical sequence;
    
- precise nouns;
    
- clear transitions.
    

## Avoid

- unnecessarily complex syntax;
    
- ornamental language;
    
- academic-sounding filler;
    
- vague pronouns;
    
- unnecessary synonyms;
    
- rhetorical padding;
    
- long sentences containing several independent ideas;
    
- inflated vocabulary used only to sound sophisticated.
    

Bad:

> La anteriormente mencionada metodología constituye una herramienta sumamente poderosa que permite llevar a cabo una gran variedad de operaciones de considerable utilidad.

Better:

> `groupby()` permite dividir las observaciones en grupos y aplicar una operación a cada grupo.

---

# 6. Write naturally in Spanish

The explanatory language of the vault is Spanish unless the user explicitly requests another language.

Write natural technical Spanish.

Do not produce literal translations from English documentation.

Keep unchanged when appropriate:

- Python syntax;
    
- function names;
    
- class names;
    
- method names;
    
- parameters;
    
- library names;
    
- mathematical notation;
    
- established technical terminology.
    

Some English terms are standard in Data Science.

Examples:

- dataset
    
- feature
    
- target
    
- pipeline
    
- estimator
    
- fit
    
- transform
    
- train/test split
    
- overfitting
    
- underfitting
    

When an English technical term can cause confusion, define it the first time.

Example:

> Una **feature** es una variable que se utiliza como entrada de un modelo.

After the definition, use the chosen term consistently.

Do not alternate unnecessarily between:

> feature / característica / predictor / variable explicativa

unless the distinction itself is relevant.

---

# 7. Avoid artificial LLM writing

The notes must not sound generated.

Avoid generic introductions such as:

> En el fascinante mundo de la ciencia de datos...

> Hoy en día los datos son cada vez más importantes...

> Pandas es una poderosa y versátil biblioteca...

Do not add conclusions merely because a text generator expects every document to have one.

Avoid repetitive phrases such as:

- es importante destacar;
    
- cabe destacar;
    
- cabe mencionar;
    
- vale la pena señalar;
    
- es fundamental tener en cuenta;
    
- herramienta poderosa;
    
- herramienta robusta;
    
- herramienta versátil.
    

If something matters, state why it matters.

Bad:

> Es importante destacar que la media es sensible a valores atípicos.

Better:

> La media es sensible a valores atípicos. Un valor extremo puede desplazarla considerablemente.

---

# 8. Explain from first principles

When a concept is difficult, reconstruct it from simpler ideas.

Do not present an advanced result as an isolated fact to memorize.

For example, when explaining sample variance:

Do not simply show:

[  
s^2 = \frac{\sum_{i=1}^{n}(x_i-\bar{x})^2}{n-1}  
]

Explain:

1. why each observation is compared with the mean;
    
2. what a deviation represents;
    
3. why raw deviations cannot simply be added;
    
4. why squaring solves that problem;
    
5. what the sum of squared deviations represents;
    
6. why a normalization is necessary;
    
7. why sample variance uses (n-1) instead of (n);
    
8. what the resulting value means.
    

Only then treat the formula as something the reader can use fluently.

---

# 9. Mathematics

Mathematics must be rigorous but readable.

## Before a formula

Explain what quantity we are trying to calculate.

## When introducing a formula

Define all important symbols.

Example:

[  
\bar{x} = \frac{1}{n}\sum_{i=1}^{n}x_i  
]

where:

- (x_i) is observation (i);
    
- (n) is the number of observations;
    
- (\bar{x}) is the sample mean.
    

Then explain the expression in words:

> Add all observations and divide the result by the number of observations.

## After a formula

Explain:

- why it has that structure;
    
- how it is calculated;
    
- what its result represents.
    

## Derivations

Include derivations when they improve academic understanding.

Do not omit intermediate algebraic steps merely because they are straightforward for an expert.

However, do not expand trivial algebra endlessly when it adds no pedagogical value.

The reader should be able to reconstruct the reasoning.

## Mathematical notation

Explain unfamiliar notation when it first appears.

This includes symbols such as:

- (\sum)
    
- (\prod)
    
- (\mu)
    
- (\sigma)
    
- (x_i)
    
- (P(A))
    
- (P(A\mid B))
    
- (E[X])
    
- (\operatorname{Var}(X))
    
- derivatives;
    
- gradients;
    
- vectors;
    
- matrices.
    

Do not assume notation explains itself.

---

# 10. Statistics

Statistical notes require special care because correct calculation does not guarantee correct interpretation.

When applicable, explain:

- the question being answered;
    
- population;
    
- sample;
    
- parameter;
    
- statistic;
    
- random variable;
    
- estimator;
    
- sampling distribution;
    
- assumptions;
    
- hypotheses;
    
- test statistic;
    
- significance level;
    
- p-value;
    
- confidence interval;
    
- effect size;
    
- uncertainty;
    
- interpretation;
    
- limitations.
    

Maintain explicit distinctions between:

- population and sample;
    
- parameter and statistic;
    
- estimator and estimate;
    
- descriptive and inferential statistics;
    
- association and causation;
    
- statistical significance and practical relevance;
    
- probability and likelihood;
    
- standard deviation and standard error.
    

Never write:

> The test proves that...

unless the statement is genuinely justified.

Prefer language that reflects uncertainty correctly.

---

# 11. Algorithms and programming

Programming notes must teach both the code and the computational idea.

When relevant, explain:

1. the problem;
    
2. the algorithm or procedure;
    
3. the state that changes during execution;
    
4. the control flow;
    
5. a manual example;
    
6. pseudocode;
    
7. Python implementation;
    
8. complexity or performance implications.
    

Do not present Python syntax as if it were the underlying concept.

For example:

A dictionary is a Python data structure.

A key-value mapping is the more general concept.

A `for` loop is syntax for expressing iteration.

Iteration is the underlying computational idea.

Explain both levels when relevant.

---

# 12. Technology notes

Notes inside technology areas such as:

- Pandas;
    
- NumPy;
    
- SciPy;
    
- statsmodels;
    
- Matplotlib;
    
- Seaborn;
    
- scikit-learn;
    
- Docker;
    

must not become copies of API documentation.

Their purpose is to **teach the technology in the context of Data Science**.

Use this general sequence when appropriate:

## What problem does it solve?

Explain why the functionality exists.

## Mental model

Explain what the library is doing conceptually.

## Basic syntax

Show the minimum useful syntax.

## Important parameters

Explain only parameters that matter for understanding or common use.

Do not copy every parameter from the API reference.

## Return value

Explain what type of object is returned.

Explain its shape or structure when relevant.

## Example

Provide a small executable example.

## Read the code

Break down an important expression step by step.

Example:

```python
df.groupby("department")["salary"].mean()
```

Explain:

1. `groupby("department")` creates groups according to `department`.
    
2. `["salary"]` selects the variable to analyze.
    
3. `mean()` calculates the mean inside each group.
    

## Output

Show or describe the important result.

Explain how to interpret it.

## Common mistakes

Explain realistic mistakes.

## Connections

Link the technology to the theoretical concept that it implements.

---

# 13. Theory and implementation are separate layers

Never confuse an implementation with the concept itself.

Examples:

- `pandas.DataFrame.groupby()` is an implementation of grouped operations.
    
- `scipy.stats.ttest_ind()` is an implementation of a statistical test.
    
- `LinearRegression` is a scikit-learn estimator implementing a regression method.
    
- `np.mean()` computes a mean; it is not the definition of the arithmetic mean.
    

When appropriate, explicitly structure the explanation as:

> **Conceptually**

followed by:

> **In Python**

This separation is especially important throughout the vault.

---

# 14. Code examples

Code must be pedagogically useful.

Prefer examples that are:

- small;
    
- executable;
    
- deterministic when possible;
    
- focused on one idea;
    
- free of irrelevant setup.
    

Do not introduce a 50-row DataFrame to explain one parameter.

Use meaningful variable names.

Avoid placeholder names such as `x`, `a`, or `foo` when a meaningful name would improve understanding.

Short mathematical examples can still use conventional notation.

## Explain important code

Do not assume code explains itself.

Explain:

- what enters;
    
- what operation occurs;
    
- what is returned;
    
- what changes;
    
- what does not change;
    
- how to interpret the result.
    

## Show outputs selectively

Show output when it helps the reader understand:

- shape;
    
- type;
    
- values;
    
- index;
    
- columns;
    
- model result;
    
- statistical result.
    

Do not fill notes with large raw outputs.

---

# 15. Visualizations

A graph is part of the explanation.

Do not insert a graph without explaining what the reader should observe.

For statistical and visualization notes, explain when relevant:

- x-axis;
    
- y-axis;
    
- visual encoding;
    
- scale;
    
- groups;
    
- distribution;
    
- patterns;
    
- outliers;
    
- uncertainty;
    
- potential misleading interpretations.
    

Use diagrams when they reduce conceptual complexity.

Do not use diagrams only as decoration.

---

# 16. Notes of class

A class note must preserve the intellectual sequence of the class.

Its purpose is to capture:

- what the professor taught;
    
- the order in which ideas appeared;
    
- examples;
    
- exercises;
    
- remarks;
    
- questions;
    
- connections;
    
- important warnings.
    

Do not transform a class note into an unrelated encyclopedia article.

However, expand explanations when the original class material assumes knowledge that the reader may not yet have.

If supplementary bibliography improves understanding, integrate it without destroying the narrative of the class.

A class note should answer:

> What was taught, why does it matter, and how does it connect with the rest of the Master's program?

Concepts that deserve independent long-term treatment should be extracted or linked to atomic concept notes.

---

# 17. Concept notes

A concept note must be **atomic but complete**.

It should focus on one concept or one tightly coupled distinction.

Examples:

- población y muestra;
    
- parámetro vs estadístico;
    
- grados de libertad;
    
- valores atípicos;
    
- matriz;
    
- derivada;
    
- función de verosimilitud.
    

A concept note must be understandable independently from the class where the concept first appeared.

A useful structure is:

1. short explanation;
    
2. formal definition;
    
3. intuition;
    
4. example;
    
5. mathematical detail when relevant;
    
6. why it matters;
    
7. related concepts.
    

Do not turn an atomic concept note into an entire chapter.

Do not duplicate a long explanation already available elsewhere.

Link instead.

---

# 18. Mathematics notes

Mathematics notes must connect formal mathematics with its later role in Data Science.

When useful, include:

- intuitive meaning;
    
- algebraic meaning;
    
- geometric meaning;
    
- formal definition;
    
- derivation;
    
- numerical example;
    
- visualization;
    
- computational interpretation;
    
- Data Science application.
    

For example, a vector should not be explained only as:

> an ordered list of numbers.

Also explain, progressively, that it can represent:

- a point;
    
- a direction;
    
- an observation;
    
- a feature vector;
    
- model parameters;
    
- gradients.
    

Do not force Data Science applications into every paragraph.

First teach the mathematics correctly.

Then build the connection.

---

# 19. Machine Learning and Data Mining

For future Machine Learning and Data Mining notes, explain when applicable:

- problem definition;
    
- supervised or unsupervised setting;
    
- input variables;
    
- target;
    
- model output;
    
- representation;
    
- objective function;
    
- loss function;
    
- optimization;
    
- training;
    
- validation;
    
- hyperparameters;
    
- assumptions;
    
- bias;
    
- variance;
    
- overfitting;
    
- underfitting;
    
- evaluation metrics;
    
- generalization;
    
- limitations.
    

Explain the mathematical or statistical mechanism before relying on library abstractions.

A scikit-learn pipeline must not become a substitute for understanding what each transformation and estimator does.

---

# 20. Comparisons

Explicitly compare concepts that are commonly confused.

Examples:

- parameter vs statistic;
    
- population vs sample;
    
- variance vs standard deviation;
    
- covariance vs correlation;
    
- probability vs likelihood;
    
- `loc` vs `iloc`;
    
- `merge` vs `concat`;
    
- `agg()` vs `transform()`;
    
- classification vs regression;
    
- normalization vs standardization.
    

A comparison should explain:

- what they share;
    
- how they differ;
    
- why the distinction matters;
    
- when each one is appropriate.
    

Use a table when it makes the distinction easier to inspect.

---

# 21. Common mistakes and misconceptions

Include common mistakes when they have genuine educational value.

Do not invent errors only to fill a section.

When documenting a mistake:

1. show the mistaken idea;
    
2. explain why it is wrong;
    
3. give the correct mental model.
    

Example:

> `groupby()` does not normally produce the final aggregated result by itself. It first creates a `GroupBy` object. An operation such as `mean()`, `sum()`, or `agg()` then produces a result.

Misconceptions are especially valuable in:

- Statistics;
    
- Probability;
    
- Linear Algebra;
    
- Calculus;
    
- Machine Learning.
    

---

# 22. Obsidian links

Use `[[wikilinks]]` to build a connected knowledge graph.

Create a link when it improves:

- conceptual navigation;
    
- prerequisite navigation;
    
- theory-to-implementation connections;
    
- cross-subject understanding.
    

Examples:

> La desviación estándar es una [[medidas de dispersión|medida de dispersión]].

> `groupby()` permite aplicar agregaciones a grupos; varias de esas agregaciones corresponden a [[medidas de posición]] o [[medidas de dispersión]].

Do not link every occurrence of every technical term.

Too many links create noise.

Do not invent a target note unless there is a clear reason to create it.

Prefer linking to an existing relevant note.

---

# 23. Callouts

Use Obsidian callouts deliberately.

Recommended semantics:

### `[!abstract]`

Main idea or chapter summary.

### `[!definition]`

Formal or concise definition.

### `[!example]`

Worked example or concrete case.

### `[!important]`

A fact required for correct understanding.

### `[!warning]`

A common error, invalid interpretation, dangerous assumption, or important limitation.

### `[!tip]`

A useful mental model, shortcut, connection, or practical advice.

### `[!note]`

Supplementary information that is useful but not part of the central explanation.

Do not put every paragraph inside a callout.

Callouts must create hierarchy, not visual noise.

---

# 24. Sources and bibliography

Use the sources available in the vault as the foundation of the content.

## For university subjects

Class material defines the expected scope and emphasis.

Use textbooks and bibliography to:

- expand explanations;
    
- fill missing intermediate steps;
    
- provide formal foundations;
    
- improve examples;
    
- clarify ambiguities.
    

Class material does not override factual correctness.

If a source appears to conflict with another authoritative source, do not silently choose one.

Identify the conflict when it is relevant.

## For technologies

Prefer official documentation for:

- API behavior;
    
- parameters;
    
- return types;
    
- version-dependent functionality.
    

Use textbooks and educational references for:

- intuition;
    
- pedagogy;
    
- broader context;
    
- examples.
    

## Source discipline

Do not invent:

- definitions;
    
- citations;
    
- functions;
    
- parameters;
    
- mathematical properties;
    
- historical claims;
    
- API behavior.
    

Do not reproduce source text mechanically.

Synthesize it into a coherent educational explanation.

---

# 25. Do not over-document APIs

A technology note is not a replacement for official documentation.

Do not enumerate every method, class, or parameter.

Prioritize what contributes to a coherent learning path.

Explain common functionality deeply before rare functionality superficially.

For important parameters, explain:

- what the parameter controls;
    
- its default behavior when useful;
    
- what changes when it is modified;
    
- when the reader is likely to use it.
    

Advanced parameters can appear later.

---

# 26. Progressive depth

A note must become more technical as the reader advances through it.

Do not open with edge cases.

Prefer:

> basic idea → normal behavior → formal detail → advanced behavior → limitations

This creates two useful reading modes:

### First reading

The reader can understand the concept without immediately processing every advanced detail.

### Review

The reader can later use the same note as a technical reference.

---

# 27. Do not optimize for shortness

Short notes are not automatically good notes.

Long notes are not automatically good notes.

Use the length required to explain the subject correctly.

Reduce:

- repetition;
    
- filler;
    
- redundant examples;
    
- decorative prose.
    

Do not reduce:

- reasoning;
    
- necessary definitions;
    
- mathematical development;
    
- important examples;
    
- interpretation.
    

The goal is **high information density with low cognitive friction**.

---

# 28. Do not optimize for sophistication

Complex prose does not make content more academic.

Academic depth comes from:

- precision;
    
- rigor;
    
- evidence;
    
- theory;
    
- reasoning;
    
- mathematical development;
    
- correct interpretation.
    

If a difficult idea can be explained with simple language, use simple language.

Prefer:

> technical content written simply

over:

> simple content written technically.

---

# 29. Knowledge graph philosophy

The vault is not a collection of isolated Markdown files.

It is a connected knowledge system.

Whenever relevant, connect:

> Mathematics → Statistics → Algorithms → Technologies → Machine Learning → Applications

Examples:

A note about variance can connect to:

- standard deviation;
    
- covariance;
    
- bias-variance tradeoff;
    
- `numpy.var`;
    
- `pandas.DataFrame.var`;
    
- statistical estimators.
    

A note about matrices can later connect to:

- linear transformations;
    
- covariance matrices;
    
- regression;
    
- PCA;
    
- neural networks.
    

A Pandas note can connect an API operation back to the statistical or algorithmic concept it implements.

Create these connections when they improve understanding.

Do not force artificial links.

---

# 30. Preserve the vault structure

Respect the existing organization, templates, frontmatter conventions, naming conventions, folders, diagrams, and links.

Do not reorganize the vault unless explicitly requested.

When modifying an existing note:

- preserve useful existing content;
    
- improve rather than blindly rewrite;
    
- preserve valid links;
    
- preserve frontmatter;
    
- avoid deleting details from class material;
    
- integrate new explanations coherently.
    

Before creating a new note, determine whether the content:

- belongs in an existing note;
    
- deserves an atomic concept note;
    
- belongs to a technology learning path;
    
- belongs to a class note.
    

Avoid duplicate notes that explain the same concept independently.

---

# 31. Final quality standard

Before finishing any substantial note, internally verify the following.

## Academic correctness

- Is the content technically correct?
    
- Is the depth appropriate for graduate study?
    
- Are important assumptions present?
    
- Are important limitations present?
    
- Are theoretical distinctions preserved?
    

## Pedagogy

- Can someone encountering this concept for the first time follow the explanation?
    
- Did I explain what problem the concept solves?
    
- Did I explain why it works?
    
- Did I avoid unexplained conceptual jumps?
    
- Did I explain difficult terminology?
    
- Did I interpret results instead of only presenting them?
    

## Mathematics

- Are formulas motivated?
    
- Are symbols explained?
    
- Are relevant derivation steps present?
    
- Is the result interpreted?
    

## Code

- Does the code illustrate the concept?
    
- Is important code explained?
    
- Is the return value understood?
    
- Is the output interpreted?
    
- Did I separate the underlying concept from its implementation?
    

## Writing

- Is the prose direct?
    
- Is terminology consistent?
    
- Are sentences unnecessarily complex?
    
- Did I remove filler?
    
- Does the text sound like a technical textbook rather than generic AI-generated prose?
    

## Vault integration

- Are useful related notes linked?
    
- Did I avoid unnecessary links?
    
- Did I preserve existing structure?
    
- Did I avoid duplicated explanations?
    

---

# 32. Ultimate test

The ideal note should satisfy two readers simultaneously.

### Reader A — First contact

This reader says:

> "I have never understood this concept before."

The explanation should allow this reader to build the idea from the beginning.

### Reader B — Master's student reviewing for an exam

This reader says:

> "I already studied this. I need the rigorous definition, formulas, assumptions, interpretation, and connections."

The same note should remain useful to this reader.

If satisfying Reader A requires removing material needed by Reader B, the solution is not to remove the material.

**Improve the explanation and organize the depth progressively.**

---

# 33. Final writing objective

The final result should feel like:

> **a graduate-level technical textbook written by an exceptional teacher who refuses to skip the intermediate steps that textbooks usually assume the reader already understands.**

The reader should never think:

> "I understand the words, but I have no idea why this follows from the previous paragraph."

The reader should instead be able to move progressively from:

> "I know nothing about this."

to:

> "I understand the intuition."

to:

> "I understand the formal definition."

to:

> "I understand the mathematics or algorithm."

to:

> "I can interpret the result."

to:

> "I can implement it."

to:

> "I understand its assumptions and limitations."

to:

> "I can connect it with the rest of Data Science."