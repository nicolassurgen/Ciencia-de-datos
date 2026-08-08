José Unpingco
Python for
Probability,
Statistics,
and Machine
Learning
Python for Probability, Statistics, and Machine
Learning
José Unpingco
Python for Probability,
Statistics, and Machine
Learning
123
José Unpingco
San Diego, CA
USA
Additional material to this book can be downloaded from http://extras.springer.com.
```
ISBN 978-3-319-30715-2 ISBN 978-3-319-30717-6 (eBook)
```
DOI 10.1007/978-3-319-30717-6
Library of Congress Control Number: 2016933108
© Springer International Publishing Switzerland 2016
This work is subject to copyright. All rights are reserved by the Publisher, whether the whole or part
of the material is concerned, specifically the rights of translation, reprinting, reuse of illustrations,
recitation, broadcasting, reproduction on microfilms or in any other physical way, and transmission
or information storage and retrieval, electronic adaptation, computer software, or by similar or dissimilar
methodology now known or hereafter developed.
The use of general descriptive names, registered names, trademarks, service marks, etc. in this
publication does not imply, even in the absence of a specific statement, that such names are exempt from
the relevant protective laws and regulations and therefore free for general use.
The publisher, the authors and the editors are safe to assume that the advice and information in this
book are believed to be true and accurate at the date of publication. Neither the publisher nor the
authors or the editors give a warranty, express or implied, with respect to the material contained herein or
for any errors or omissions that may have been made.
Printed on acid-free paper
This Springer imprint is published by Springer Nature
The registered company is Springer International Publishing AG Switzerland
To Irene, Nicholas, and Daniella, for all their
patient support.
Preface
This book will teach you the fundamental concepts that underpin probability and
statistics and illustrates how they relate to machine learning via the Python language
and its powerful extensions. This is not a good first book in any of these topics
because we assume that you already had a decent undergraduate-level introduction
to probability and statistics. Furthermore, we also assume that you have a good grasp
of the basic mechanics of the Python language itself. Having said that, this book is
appropriate if you have this basic background and want to learn how to use the
scientific Python toolchain to investigate these topics. On the other hand, if you are
comfortable with Python, perhaps through working in another scientific field, then
this book will teach you the fundamentals of probability and statistics and how to use
these ideas to interpret machine learning methods. Likewise, if you are a practicing
```
engineer using a commercial package (e.g., Matlab, IDL), then you will learn how to
```
effectively use the scientific Python toolchain by reviewing concepts with which you
are already familiar.
The most important feature of this book is that everything in it is reproducible
```
using Python. Specifically, all of the code, all of the figures, and (most of) the text is
```
available in the downloadable supplementary materials that correspond to this book
as IPython Notebooks. IPython Notebooks are live interactive documents that allow
you to change parameters, recompute plots, and generally tinker with all of the
ideas and code in this book. I urge you to download these IPython Notebooks and
follow along with the text to experiment with the topics covered. I guarantee doing
this will boost your understanding because the IPython Notebooks allow for
interactive widgets, animations, and other intuition-building features that help make
many of these abstract ideas concrete. As an open-source project, the entire sci-
entific Python toolchain, including the IPython Notebook, is freely available.
Having taught this material for many years, I am convinced that the only way to
learn is to experiment as you go. The text provides instructions on how to get
started installing and configuring your scientific Python environment.
This book is not designed to be exhaustive and reflects the author’s eclectic
background in industry. The focus is on fundamentals and intuitions for day-to-day
vii
work, especially when you must explain the results of your methods to a
nontechnical audience. We have tried to use the Python language in the most
expressive way possible while encouraging good Python coding practices.
Acknowledgments
I would like to acknowledge the help of Brian Granger and Fernando Perez, two
of the originators of the Jupyter/IPython Notebook, for all their great work, as well
as the Python community as a whole, for all their contributions that made this book
possible. Additionally, I would also like to thank Juan Carlos Chavez for his
thoughtful review. Hans Petter Langtangen is the author of the Doconce [19]
document preparation system that was used to write this text. Thanks to Geoffrey
Poore [31] for his work with PythonTeX and LATEX.
San Diego, California
February 2016
viii Preface
Contents
1 Getting Started with Scientific Python. . . . . . . . . . . . . . . . . . . . . . . 1
1.1 Installation and Setup . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 3
1.2 Numpy . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 4
1.2.1 Numpy Arrays and Memory . . . . . . . . . . . . . . . . . . . . 6
1.2.2 Numpy Matrices . . . . . . . . . . . . . . . . . . . . . . . . . . . . 9
1.2.3 Numpy Broadcasting . . . . . . . . . . . . . . . . . . . . . . . . . 10
1.2.4 Numpy Masked Arrays . . . . . . . . . . . . . . . . . . . . . . . . 12
1.2.5 Numpy Optimizations and Prospectus . . . . . . . . . . . . . . 12
1.3 Matplotlib . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 13
1.3.1 Alternatives to Matplotlib . . . . . . . . . . . . . . . . . . . . . . 15
1.3.2 Extensions to Matplotlib . . . . . . . . . . . . . . . . . . . . . . . 16
1.4 IPython. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 16
1.4.1 IPython Notebook . . . . . . . . . . . . . . . . . . . . . . . . . . . 18
1.5 Scipy . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 20
1.6 Pandas . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 21
1.6.1 Series . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 21
1.6.2 Dataframe . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 23
1.7 Sympy . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 25
1.8 Interfacing with Compiled Libraries . . . . . . . . . . . . . . . . . . . . . 27
1.9 Integrated Development Environments . . . . . . . . . . . . . . . . . . . 28
1.10 Quick Guide to Performance and Parallel Programming . . . . . . . 29
1.11 Other Resources. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 32
References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 32
2 Probability . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 35
2.1 Introduction. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 35
2.1.1 Understanding Probability Density . . . . . . . . . . . . . . . . 36
2.1.2 Random Variables . . . . . . . . . . . . . . . . . . . . . . . . . . . 37
2.1.3 Continuous Random Variables . . . . . . . . . . . . . . . . . . . 42
2.1.4 Transformation of Variables Beyond Calculus . . . . . . . . 45
ix
2.1.5 Independent Random Variables . . . . . . . . . . . . . . . . . . 47
2.1.6 Classic Broken Rod Example . . . . . . . . . . . . . . . . . . . 49
2.2 Projection Methods . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 50
2.2.1 Weighted Distance . . . . . . . . . . . . . . . . . . . . . . . . . . . 53
2.3 Conditional Expectation as Projection . . . . . . . . . . . . . . . . . . . . 54
2.3.1 Appendix . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 60
2.4 Conditional Expectation and Mean Squared Error . . . . . . . . . . . 60
2.5 Worked Examples of Conditional Expectation and Mean Square
Error Optimization . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
2.5.1 Example . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
2.5.2 Example . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 68
2.5.3 Example . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 70
2.5.4 Example . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 73
2.5.5 Example . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 74
2.5.6 Example . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77
2.6 Information Entropy . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 78
2.6.1 Information Theory Concepts . . . . . . . . . . . . . . . . . . . 79
2.6.2 Properties of Information Entropy . . . . . . . . . . . . . . . . 81
2.6.3 Kullback-Leibler Divergence . . . . . . . . . . . . . . . . . . . . 82
2.7 Moment Generating Functions . . . . . . . . . . . . . . . . . . . . . . . . . 83
2.8 Monte Carlo Sampling Methods. . . . . . . . . . . . . . . . . . . . . . . . 87
2.8.1 Inverse CDF Method for Discrete Variables . . . . . . . . . 88
2.8.2 Inverse CDF Method for Continuous Variables . . . . . . . 90
2.8.3 Rejection Method. . . . . . . . . . . . . . . . . . . . . . . . . . . . 92
2.9 Useful Inequalities . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
2.9.1 Markov’s Inequality . . . . . . . . . . . . . . . . . . . . . . . . . . 96
2.9.2 Chebyshev’s Inequality . . . . . . . . . . . . . . . . . . . . . . . . 97
2.9.3 Hoeffding’s Inequality . . . . . . . . . . . . . . . . . . . . . . . . 98
References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
3 Statistics . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
3.1 Introduction. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
3.2 Python Modules for Statistics . . . . . . . . . . . . . . . . . . . . . . . . . 102
3.2.1 Scipy Statistics Module. . . . . . . . . . . . . . . . . . . . . . . . 102
3.2.2 Sympy Statistics Module. . . . . . . . . . . . . . . . . . . . . . . 103
3.2.3 Other Python Modules for Statistics . . . . . . . . . . . . . . . 104
3.3 Types of Convergence . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 104
3.3.1 Almost Sure Convergence . . . . . . . . . . . . . . . . . . . . . . 105
3.3.2 Convergence in Probability . . . . . . . . . . . . . . . . . . . . . 107
3.3.3 Convergence in Distribution . . . . . . . . . . . . . . . . . . . . 109
3.3.4 Limit Theorems . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 110
3.4 Estimation Using Maximum Likelihood . . . . . . . . . . . . . . . . . . 111
3.4.1 Setting Up the Coin Flipping Experiment . . . . . . . . . . . 113
3.4.2 Delta Method . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 123
x Contents
3.5 Hypothesis Testing and P-Values . . . . . . . . . . . . . . . . . . . . . . . 125
3.5.1 Back to the Coin Flipping Example . . . . . . . . . . . . . . . 126
3.5.2 Receiver Operating Characteristic. . . . . . . . . . . . . . . . . 130
3.5.3 P-Values . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 132
3.5.4 Test Statistics . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 133
3.5.5 Testing Multiple Hypotheses . . . . . . . . . . . . . . . . . . . . 140
3.6 Confidence Intervals . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 141
3.7 Linear Regression . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 144
3.7.1 Extensions to Multiple Covariates . . . . . . . . . . . . . . . . 154
3.8 Maximum A-Posteriori . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 158
3.9 Robust Statistics . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 164
3.10 Bootstrapping . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 171
3.10.1 Parametric Bootstrap . . . . . . . . . . . . . . . . . . . . . . . . . 175
3.11 Gauss Markov . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 176
3.12 Nonparametric Methods . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 180
3.12.1 Kernel Density Estimation. . . . . . . . . . . . . . . . . . . . . . 180
3.12.2 Kernel Smoothing . . . . . . . . . . . . . . . . . . . . . . . . . . . 183
3.12.3 Nonparametric Regression Estimators . . . . . . . . . . . . . . 188
3.12.4 Nearest Neighbors Regression . . . . . . . . . . . . . . . . . . . 189
3.12.5 Kernel Regression . . . . . . . . . . . . . . . . . . . . . . . . . . . 193
3.12.6 Curse of Dimensionality . . . . . . . . . . . . . . . . . . . . . . . 194
References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 196
4 Machine Learning . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 197
4.1 Introduction. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 197
4.2 Python Machine Learning Modules . . . . . . . . . . . . . . . . . . . . . 197
4.3 Theory of Learning . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 201
4.3.1 Introduction to Theory of Machine Learning . . . . . . . . . 203
4.3.2 Theory of Generalization. . . . . . . . . . . . . . . . . . . . . . . 207
4.3.3 Worked Example for Generalization/Approximation
Complexity . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 209
4.3.4 Cross-Validation . . . . . . . . . . . . . . . . . . . . . . . . . . . . 215
4.3.5 Bias and Variance . . . . . . . . . . . . . . . . . . . . . . . . . . . 219
4.3.6 Learning Noise . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 222
4.4 Decision Trees. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 225
4.4.1 Random Forests . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 232
4.5 Logistic Regression . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 234
4.5.1 Generalized Linear Models . . . . . . . . . . . . . . . . . . . . . 239
4.6 Regularization . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 240
4.6.1 Ridge Regression . . . . . . . . . . . . . . . . . . . . . . . . . . . . 244
4.6.2 Lasso . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 248
4.7 Support Vector Machines . . . . . . . . . . . . . . . . . . . . . . . . . . . . 250
4.7.1 Kernel Tricks . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 253
4.8 Dimensionality Reduction . . . . . . . . . . . . . . . . . . . . . . . . . . . . 256
4.8.1 Independent Component Analysis. . . . . . . . . . . . . . . . . 260
Contents xi
4.9 Clustering . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 264
4.10 Ensemble Methods . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 268
4.10.1 Bagging . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 268
4.10.2 Boosting . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 271
References . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 273
Index . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 275
xii Contents
Notation
Symbol Meaning
σ Standard deviation
μ Mean
V Variance
E Expectation
```
f(x) Function of x
```
x ! y Mapping from x to y
```
(a, b) Open interval
```
[a, b] Closed interval
```
(a, b] Half-open interval
```
Δ Differential of
Π Product operator
Σ Summation of
xj j Absolute value of x
xk k Norm of x
#A Number of elements in A
A \ B Intersection of sets A, B
A [ B Union of sets A, B
A × B Cartesian product of sets A, B
2 Element of
∧ Logical conjunction
¬ Logical negation
```
{} Set delimiters
```
P XjYð Þ Probability of X given Y
8 For all
9 There exists
A  B A is a subset of B
A  B A is a proper subset of B
```
f X(x) Probability density function of random variable X
```
```
FX(x) Cumulative density function of random variable X
```
- Distributed according to
xiii
∝ Proportional to
≜ Equal by definition
:¼ Equal by definition
⊥ Perpendicular to
∴ Therefore
⟹ Implies
≡ Equivalent to
X Matrix X
x Vector x
```
sgn(x) Sign of x
```
R Real line
Rn n-dimensional vector space
Rmn m × n-dimensional matrix space
```
U ða;bÞ Uniform distribution on the interval (a, b)
```
```
N ðμ; σ2Þ Normal distribution with mean μ and variance σ2
```
!as Converges almost surely
!d Converges in distribution
!P Converges in probability
xiv Notation
About the Author
Dr. José Unpingco earned his PhD from the University of California, San Diego
in 1998 and has since worked in industry as an engineer, consultant, and instructor
on a wide-variety of advanced data processing and analysis topics, with a rich
experience in multiple machine learning technologies. He has been the onsite
technical director for large-scale signal and image processing for the Department of
```
Defense (DoD), where he also spearheaded the DoD-wide adoption of the Scientific
```
Python. As the primary Scientific Python instructor for the DoD, he has taught
Python to over 600 scientists and engineers. He is currently the technical director
for data science for a non-profit medical research organization in San Diego,
California.
xv
Chapter 1
Getting Started with Scientific Python
Python went mainstream years ago. It is now part of many undergraduate curricula
in engineering and computer science. Great books and interactive on-line tutorials
are easy to find. In particular, Python is well-established in web programming with
frameworks such as Django and CherryPy, and is the back-end platform for many
high-traffic sites.
Beyond web programming, there is an ever-expanding list of third-party exten-
sions that reach across many scientific disciplines, from linear algebra to visualization
to machine learning. For these applications, Python is the software glue that permits
easy exchange of methods and data across core routines typically written in Fortran
or C. Scientific Python has been fundamental for almost two decades in government,
academia, and industry. For example, NASA’s Jet Propulsion Laboratory uses it for
interfacing Fortran/C++ libraries for planning and visualization of spacecraft trajec-
tories. The Lawrence Livermore National Laboratory uses scientific Python for a
wide variety of computing tasks, some involving routine text processing, and others
```
involving advanced visualization of vast data sets (e.g. VISIT [1]). Shell Research,
```
Boeing, Industrial Light and Magic, Sony Entertainment, and Procter & Gamble use
scientific Python on a daily basis for data processing and analysis. Python is thus
well-established and continues to extend into many different fields.
Python is a language geared towards scientists and engineers who may not have
formal software development training. It is used to prototype, design, simulate, and
test without getting in the way because Python provides an inherently easy and
incremental development cycle, interoperability with existing codes, access to a large
base of reliable open source codes, and a hierarchical compartmentalized design
philosophy. It is known that productivity is strongly influenced by the workflow of
```
the user, (e.g., time spent running versus time spent programming) [2]. Therefore,
```
Python can dramatically enhance user-productivity.
Python is an interpreted language. This means that Python codes run on a
Python virtual machine that provides a layer of abstraction between the code and
the platform it runs on, thus making codes portable across different platforms. For
© Springer International Publishing Switzerland 2016
J. Unpingco, Python for Probability, Statistics, and Machine Learning,
DOI 10.1007/978-3-319-30717-6_1
1
2 1 Getting Started with Scientific Python
example, the same script that runs on a Windows laptop can also run on a Linux-based
supercomputer or on a mobile phone. This makes programming easier because the
virtual machine handles the low-level details of implementing the business logic of
the script on the underlying platform.
Python is a dynamically typed language, which means that the interpreter itself
```
figures out the representative types (e.g., floats, integers) interactively or at run-time.
```
This is in contrast to a language like Fortran that have compilers that study the code
from beginning to end, perform many compiler-level optimizations, link intimately
with the existing libraries on a specific platform, and then create an executable that
is henceforth liberated from the compiler. As you may guess, the compiler’s access
to the details of the underlying platform means that it can utilize optimizations
that exploit chip-specific features and cache memory. Because the virtual machine
abstracts away these details, it means that the Python language does not have pro-
grammable access to these kinds of optimizations. So, where is the balance between
the ease of programming the virtual machine and these key numerical optimizations
that are crucial for scientific work?
The balance comes from Python’s native ability to bind to compiled Fortran and C
libraries. This means that you can send intensive computations to compiled libraries
directly from the interpreter. This approach has two primary advantages. First, it give
you the fun of programming in Python, with its expressive syntax and lack of visual
clutter. This is a particular boon to scientists who typically want to use software as
a tool as opposed to developing software as a product. The second advantage is that
you can mix-and-match different compiled libraries from diverse research areas that
were not otherwise designed to work together. This works because Python makes
it easy to allocate and fill memory in the interpreter, pass it as input to compiled
libraries, and then retrieve the output back at the interpreter.
Moreover, Python provides a multiplatform solution for scientific codes. As an
open-source project, Python itself is available anywhere you can build it, even though
it typically comes standard nowadays, as part of many operating systems. This means
that once you have written your code in Python, you can just transfer the script to
another platform and run it, as long as the compiled libraries are also available
there. What if the compiled libraries are absent? Building and configuring compiled
libraries across multiple systems used to be a painstaking job, but as scientific Python
has matured, a wide range of libraries have now become available across all of the
```
major platforms (i.e., Windows, MacOS, Linux, Unix) as prepackaged distributions.
```
Finally, scientific Python facilitates maintainability of scientific codes because
Python syntax is clean, free of semi-colon litter and other visual distractions that
makes code hard to read and easy to obfuscate. Python has many built-in testing,
documentation, and development tools that ease maintenance. Scientific codes are
usually written by scientists unschooled in software development, so having solid
software development tools built into the language itself is a particular boon.
1.1 Installation and Setup 3
1.1 Installation and Setup
The easiest way to get started is to download the freely available Anaconda distrib-
```
ution provided by Continuum Analytics (continuum.io), which is available for
```
all of the major platforms. On Linux, even though most of the toolchain is available
via the built-in Linux package manager, it is still better to install the Anaconda distri-
```
bution because it provides its own powerful package manager (i.e., conda) that can
```
keep track of changes in the software dependencies of the packages that it supports.
Note that if you do not have administrator privileges, there is also a corresponding
miniconda distribution that does not require these privileges.
Regardless of your platform, we recommend Python version 2.7. Python 2.7 is
the last of the Python 2.x series and guarantees backwards compatibility with legacy
codes. Python 3.x makes no such guarantees. Although all of the key components of
scientific Python are available in version 3.x, the safest bet is to stick with version
2.7. Alternatively, one compromise is to write in a hybrid dialect of Python that
is the intersection of elements of versions 2.7 and 3.x. The six module enables
this transition by providing utility functions for 2.5 and newer codes. There is also a
Python 2.7 to 3.x converter available as the 2to3 module but it may be hard to debug
```
or maintain the so-converted code; nonetheless, this might be a good option for small,
```
self-contained libraries that do not require further development or maintenance.
You may have encountered other Python variants on the web, such as
```
IronPython (Python implemented in C#) and Jython (Python implemented
```
```
in Java). In this text, we focus on the C-implementation of Python (i.e., known as
```
```
CPython), which is, by far, the most popular implementation. These other Python
```
```
variants permit specialized, native interaction with libraries in C# or Java (respec-
```
```
tively), which is still possible (but clunky) using the CPython. Even more Python
```
variants exist that implement the low-level machinery of Python differently for vari-
ous reasons, beyond interacting with native libraries in other languages. Most notable
```
of these is Pypy that implements a just-in-time compiler (JIT) and other powerful
```
optimizations that can substantially speed up pure Python codes. The downside of
```
Pypy is that its coverage of some popular scientific modules (e.g., Matplotlib, Scipy)
```
is limited or non-existent which means that you cannot use those modules in code
meant for Pypy.
You may later want to use a Python module that is not maintained by Anaconda’s
conda manager. Because Anaconda comes with the pip package manager, which
is the main one used outside of scientific Python, you can simply do
Terminal> pip install package_name
and pip will run out to the web and download the package you want and its dependen-
cies and install them in the existing Anaconda directory tree. This works beautifully
in the case where the package in question is pure-Python, without any system-specific
dependencies. Otherwise, this can be a real nightmare, especially on Windows, which
lacks freely available Fortran compilers. If the module in question is a C-library, one
way to cope is to install the freely available Visual Studio Community Edition,
4 1 Getting Started with Scientific Python
which usually has enough to compile many C-codes. This platform dependency is
the problem that conda was designed to solve by making the binary dependencies of
the various platforms available instead of attempting to compile them. On a Windows
system, if you installed Anaconda and registered it as the default Python installation
```
(it asks during the install process), then you can use the high-quality Python wheel
```
files on Christoph Gohlke’s laboratory site at the University of California, Irvine
where he kindly makes a long list of scientific modules available. 1 Failing this, you
can try the binstar.org site, which is a community-powered repository of mod-
ules that conda is capable of installing, but which are not formally supported by
Anaconda. Note that binstar allows you to share scientific Python configurations
with your remote colleagues using authentication so that you can be sure that you
are downloading and running code from users you trust.
Again, if you are on Windows, and none of the above works, then you may
want to consider installing a full virtual machine solution, as provided by VMWare’s
```
Player or Oracle’s VirtualBox (both freely available under liberal terms). Using
```
either of these, you can set up a Linux machine running on top of Windows, which
should cure these problems entirely! The great part of this approach is that you
can share directories between the virtual machine and the Windows system so that
you don’t have to maintain duplicate data files. Anaconda Linux images are also
available on the cloud by IAAS providers like Amazon Web Services and Microsoft
Azure. Note that for the vast majority of users, especially newcomers to Python,
the Anaconda distribution should be more than enough on any platform. It is just
worth highlighting the Windows-specific issues and associated workarounds early on.
Note that there are other well-maintained scientific Python Windows installers like
WinPython and PythonXY. These provide the spyder integrated development
environment, which is very Matlab-like environment for transitioning Matlab users.
1.2 Numpy
As we touched upon earlier, to use a compiled scientific library, the memory allocated
in the Python interpreter must somehow reach this library as input. Furthermore, the
output from these libraries must likewise return to the Python interpreter. This two-
```
way exchange of memory is essentially the core function of the Numpy (numerical
```
```
arrays in Python) module. Numpy is the de-facto standard for numerical arrays in
```
Python. It arose as an effort by Travis Oliphant and others to unify the numerical
arrays in Python. In this section, we provide an overview and some tips for using
Numpy effectively, but for much more detail, Travis’ book [3] is a great place to start
and is available for free online.
1 Wheel files are a Python distribution format that you download and install using pip as in pip
```
install file.whl. Christoph names files according to Python version (e.g., cp27 means
```
```
Python 2.7) and chipset (e.g., amd32 vs. Intel win32).
```
1.2 Numpy 5
Numpy provides specification of byte-sized arrays in Python. For example, below
```
we create an array of three numbers, each of four-bytes long (32 bits at 8 bits per byte)
```
as shown by the itemsize property. The first line imports Numpy as np, which is
the recommended convention. The next line creates an array of 32 bit floating point
numbers. The itemize property shows the number of bytes per item.
```
>>> import numpy as np # recommended convention>>> x = np.array([1,2,3],dtype=np.float32)
```
```
>>> xarray([ 1., 2., 3.], dtype=float32)
```
>>> x.itemsize4
In addition to providing uniform containers for numbers, Numpy provides a com-
```
prehensive set of unary functions (i.e., ufuncs) that process arrays element-wise with-
```
out additional looping semantics. Below, we show how to compute the element-wise
sine using Numpy,
```
>>> np.sin(np.array([1,2,3],dtype=np.float32) )array([ 0.84147096, 0.90929741, 0.14112 ], dtype=float32)
```
This computes the sine of the input array [1,2,3], using Numpy’s unary function,
np.sin. There is another sine function in the built-in math module, but the Numpy
```
version is faster because it does not require explicit looping (i.e., using a for loop)
```
over each of the elements in the array. That looping happens in the compiled np.sin
```
function itself. Otherwise, we would have to do looping explicitly as in the following:
```
```
>>> from math import sin>>> [sin(i) for i in [1,2,3] ] # list comprehension
```
[0.8414709848078965, 0.9092974268256817, 0.1411200080598672]
Numpy uses common-sense casting rules to resolve the output types. For example,
if the inputs had been an integer-type, the output would still have been a floating point
type. In this example, we provided a Numpy array as input to the sine function. We
could have also used a plain Python list instead and Numpy would have built the
```
intermediate Numpy array (e.g., np.sin([1,1,1])). The Numpy documentation
```
```
provides a comprehensive (and very long) list of available ufuncs.
```
Numpy arrays come in many dimensions. For example, the following shows a
two-dimensional 2 × 3 array constructed from two conforming Python lists.
```
>>> x=np.array([ [1,2,3],[4,5,6] ])>>> x.shape
```
```
(2, 3)
```
Note that Numpy is limited to 32 dimensions unless you build it for more. 2 Numpy
arrays follow the usual Python slicing rules in multiple dimensions as shown below
where the : colon character selects all elements along a particular axis.
```
>>> x=np.array([ [1,2,3],[4,5,6] ])>>> x[:,0] # 0th column
```
```
array([1, 4])>>> x[:,1] # 1st column
```
```
array([2, 5])
```
2 See arrayobject.h in the Numpy source code.
6 1 Getting Started with Scientific Python
```
>>> x[0,:] # 0th rowarray([1, 2, 3])
```
```
>>> x[1,:] # 1st rowarray([4, 5, 6])
```
You can also select sub-sections of arrays by using slicing as shown below.
```
>>> x=np.array([ [1,2,3],[4,5,6] ])>>> x
```
```
array([ [1, 2, 3],[4, 5, 6] ])
```
```
>>> x[:,1:] # all rows, 1st thru last columnarray([ [2, 3],
```
```
[5, 6] ])>>> x[:,::2] # all rows, every other column
```
```
array([ [1, 3],[4, 6] ])
```
```
>>> x[:,::-1] # reverse order of columnsarray([ [3, 2, 1],
```
```
[6, 5, 4] ])
```
1.2.1 Numpy Arrays and Memory
Some interpreted languages implicitly allocate memory. For example, in Matlab,
you can extend a matrix by simply tacking on another dimension as in the following
Matlab session:
```
>> x=ones(3,3)x =
```
1 1 11 1 1
```
1 1 1>> x(:,4)=ones(3,1) % tack on extra dimension
```
```
x = 1 1 1 1
```
1 1 1 11 1 1 1
```
>> size(x)ans =
```
3 4
This works because Matlab arrays use pass-by-value semantics so that slice opera-
tions actually copy parts of the array as needed. By contrast, Numpy uses pass-by-
reference semantics so that slice operations are views into the array without implicit
copying. This is particularly helpful with large arrays that already strain available
```
memory. In Numpy terminology, slicing creates views (no copying) and advanced
```
indexing creates copies. Let’s start with advanced indexing.
```
If the indexing object (i.e., the item between the brackets) is a non-tuple sequence
```
```
object, another Numpy array (of type integer or boolean), or a tuple with at least
```
one sequence object or Numpy array, then indexing creates copies. For the above
example, to accomplish the same array extension in Numpy, you have to do something
like the following
1.2 Numpy 7
```
>>> x = np.ones((3,3))>>> x
```
```
array([ [ 1., 1., 1.],[ 1., 1., 1.],
```
```
[ 1., 1., 1.] ])>>> x[:,[0,1,2,2] ] # notice duplicated last dimension
```
```
array([ [ 1., 1., 1., 1.],[ 1., 1., 1., 1.],
```
```
[ 1., 1., 1., 1.] ])>>> y=x[:,[0,1,2,2] ] # same as above, but do assign it to y
```
Because of advanced indexing, the variable y has its own memory because the
relevant parts of x were copied. To prove it, we assign a new element to x and see
that y is not updated.
>>> x[0,0]=999 # change element in x>>> x # changed
```
array([ [ 999., 1., 1.],[ 1., 1., 1.],
```
```
[ 1., 1., 1.] ])>>> y # not changed!
```
```
array([ [ 1., 1., 1., 1.],[ 1., 1., 1., 1.],
```
```
[ 1., 1., 1., 1.] ])
```
```
However, if we start over and construct y by slicing (which makes it a view) as shown
```
below, then the change we made does affect y because a view is just a window into
the same memory.
```
>>> x = np.ones((3,3))>>> y = x[:2,:2] # view of upper left piece
```
>>> x[0,0] = 999 # change value>>> x
```
array([ [ 999., 1., 1.], # see the change?[ 1., 1., 1.],
```
```
[ 1., 1., 1.] ])>>> y
```
```
array([ [ 999., 1.], # changed y also![ 1., 1.] ])
```
Note that if you want to explicitly force a copy without any indexing tricks, you
```
can do y=x.copy(). The code below works through another example of advanced
```
indexing versus slicing.
```
>>> x = np.arange(5) # create array>>> x
```
```
array([0, 1, 2, 3, 4])>>> y=x[ [0,1,2] ] # index by integer list to force copy
```
```
>>> yarray([0, 1, 2])
```
>>> z=x[:3] # slice creates view>>> z # note y and z have same entries
```
array([0, 1, 2])>>> x[0]=999 # change element of x
```
```
>>> xarray([999, 1, 2, 3, 4])
```
```
>>> y # note y is unaffected,array([0, 1, 2])
```
```
>>> z # but z is (it’s a view).array([999, 1, 2])
```
8 1 Getting Started with Scientific Python
In this example, y is a copy, not a view, because it was created using advanced
indexing whereas z was created using slicing. Thus, even though y and z have the
same entries, only z is affected by changes to x. Note that the flags.ownsdata
property of Numpy arrays can help sort this out until you get used to it.
Manipulating memory using views is particularly powerful for signal and image
processing algorithms that require overlapping fragments of memory. The following
is an example of how to use advanced Numpy to create overlapping blocks that do
not actually consume additional memory,
```
>>> from numpy.lib.stride_tricks import as_strided>>> x = arange(16)
```
```
>>> y=as_strided(x,(7,4),(8,4)) # overlapped entries>>> y
```
```
array([ [ 0, 1, 2, 3],[ 2, 3, 4, 5],
```
[ 4, 5, 6, 7],[ 6, 7, 8, 9],
[ 8, 9, 10, 11],[10, 11, 12, 13],
```
[12, 13, 14, 15] ])
```
The above code creates a range of integers and then overlaps the entries to create a
7 × 4 Numpy array. The final argument in the as_strided function are the strides,
which are the steps in bytes to move in the row and column dimensions, respectively.
Thus, the resulting array steps four bytes in the column dimension and eight bytes in
the row dimension. Because the integer elements in the Numpy array are four bytes,
this is equivalent to moving by one element in the column dimension and by two
elements in the row dimension. The second row in the Numpy array starts at eight
```
bytes (two elements) from the first entry (i.e., 2) and then proceeds by four bytes (by
```
```
one element) in the column dimension (i.e., 2,3,4,5). The important part is that
```
memory is re-used in the resulting 7 × 4 Numpy array. The code below demonstrates
this by reassigning elements in the original x array. The changes show up in the y
array because they point at the same allocated memory.
>>> x[::2]=99 # assign every other value
>>> x
```
array([99, 1, 99, 3, 99, 5, 99, 7, 99, 9, 99, 11, 99, 13, 99, 15])
```
>>> y # the changes appear because y is a view
```
array([ [99, 1, 99, 3],
```
[99, 3, 99, 5],
[99, 5, 99, 7],
[99, 7, 99, 9],
[99, 9, 99, 11],
[99, 11, 99, 13],
```
[99, 13, 99, 15] ])
```
Bear in mind that as_strided does not check that you stay within memory block
bounds. So, if the size of the target matrix is not filled by the available data, the
remaining elements will come from whatever bytes are at that memory location. In
other words, there is no default filling by zeros or other strategy that defends memory
block bounds. One defense is to explicitly control the dimensions as in the following
code,
1.2 Numpy 9
```
>>> n = 8 # number of elements>>> x = arange(n) # create array
```
```
>>> k = 5 # desired number of rows>>> y = as_strided(x,(k,n-k+1),(x.itemsize,)*2)
```
```
>>> yarray([ [0, 1, 2, 3],
```
[1, 2, 3, 4],[2, 3, 4, 5],
```
[3, 4, 5, 6],[4, 5, 6, 7] ])
```
1.2.2 Numpy Matrices
Matrices in Numpy are similar to Numpy arrays but they can only have two dimen-
sions. They implement row-column matrix multiplication as opposed to element-wise
multiplication. If you have two matrices you want to multiply, you can either create
them directly or convert them from Numpy arrays. For example, the following shows
how to create two matrices and multiply them.
```
>>> import numpy as np>>> A=np.matrix([ [1,2,3],[4,5,6],[7,8,9] ])
```
```
>>> x=np.matrix([ [1],[0],[0] ])>>> A*x
```
```
matrix([ [1],[4],
```
```
[7] ])
```
This can also be done using arrays as shown below,
```
>>> A=np.array([ [1,2,3],[4,5,6],[7,8,9] ])>>> x=np.array([ [1],[0],[0] ])
```
```
>>> A.dot(x)array([ [1],
```
```
[4],[7] ])
```
Numpy arrays support elementwise multiplication, not row-column multiplication.
You must use Numpy matrices for this kind of multiplication unless use the inner
```
product np.dot, which also works in multiple dimensions (see np.tensordot
```
```
for more general dot products).
```
It is unnecessary to cast everything to matrices for multiplication. In the next
example, everything until last line is a Numpy array and thereafter we cast the array
as a matrix with np.matrix which then uses row-column multiplication. Note that
it is unnecessary to cast the x variable as a matrix because the left-to-right order
of the evaluation takes care of that automatically. If we need to use A as a matrix
elsewhere in the code then we should bind it to another variable instead of re-casting
it every time. If you find yourself casting back and forth for large arrays, passing the
```
copy=False flag to matrix avoids the expense of making a copy.
```
```
>>> A=np.ones((3,3))>>> type(A) # array not matrix
```
```
<type ’numpy.ndarray’>>>> x=np.ones((3,1)) # array not matrix
```
>>> A*x
10 1 Getting Started with Scientific Python
```
array([ [ 1., 1., 1.],[ 1., 1., 1.],
```
```
[ 1., 1., 1.] ])>>> np.matrix(A)*x # row-column multiplication
```
```
matrix([ [ 3.],[ 3.],
```
```
[ 3.] ])
```
1.2.3 Numpy Broadcasting
Numpy broadcasting is a powerful way to make implicit multidimensional grids for
expressions. It is probably the single most powerful feature of Numpy and the most
difficult to grasp. Proceeding by example, consider the vertices of a two-dimensional
unit square as shown below,
```
>>> X,Y=np.meshgrid(np.arange(2),np.arange(2))>>> X
```
```
array([ [0, 1],[0, 1] ])
```
```
>>> Yarray([ [0, 0],
```
```
[1, 1] ])
```
Numpy’s meshgrid creates two-dimensional grids. The X and Y arrays have
```
corresponding entries match the coordinates of the vertices of the unit square (e.g.,
```
```
(0, 0), (0, 1), (1, 0), (1, 1)). To add the x and y-coordinates, we could use X and Y
```
as in X+Y shown below, The output is the sum of the vertex coordinates of the unit
square.
```
>>> X+Yarray([ [0, 1],
```
```
[1, 2] ])
```
Because the two arrays have compatible shapes, they can be added together element-
wise. It turns out we can skip a step here and not bother with meshgrid to implicitly
obtain the vertex coordinates by using broadcasting as shown below
```
>>> x = np.array([0,1])>>> y = np.array([0,1])
```
```
>>> xarray([0, 1])
```
```
>>> yarray([0, 1])
```
```
>>> x + y[:,None] # add broadcast dimensionarray([ [0, 1],
```
```
[1, 2] ])>>> X+Y
```
```
array([ [0, 1],[1, 2] ])
```
On line 7 the None Python singleton tells Numpy to make copies of y along this
dimension to create a conformable calculation. Note that np.newaxis can be used
instead of None to be more explicit. The following lines show that we obtain the
same output as when we used the X+Y Numpy arrays. Note that without broadcasting
1.2 Numpy 11
```
x+y=array([0, 2]) which is not what we are trying to compute. Let’s continue
```
with a more complicated example where we have differing array shapes.
```
>>> x = np.array([0,1])>>> y = np.array([0,1,2])
```
```
>>> X,Y = np.meshgrid(x,y)>>> X
```
```
array([ [0, 1], # duplicate by row[0, 1],
```
```
[0, 1] ])>>> Y
```
```
array([ [0, 0], # duplicate by column[1, 1],
```
```
[2, 2] ])>>> X+Y
```
```
array([ [0, 1],[1, 2],
```
```
[2, 3] ])>>> x+y[:,None] # same as with meshgrid
```
```
array([ [0, 1],[1, 2],
```
```
[2, 3] ])
```
In this example, the array shapes are different, so the addition of x and y is
not possible without Numpy broadcasting. The last line shows that broadcasting
generates the same output as using the compatible array generated by meshgrid.
This shows that broadcasting works with different array shapes. For the sake of
comparison, on line 3, meshgrid creates two conformable arrays, X and Y. On the
last line, x+y[:,None] produces the same output as X+Y without the meshgrid.
We can also put the None dimension on the x array as x[:,None]+y which would
give the transpose of the result.
Broadcasting works in multiple dimensions also. The output shown has shape
```
(4,3,2). On the last line, the x+y[:,None] produces a two-dimensional array
```
which is then broadcast against z[:,None,None], which duplicates itself along
```
the two added dimensions to accommodate the two-dimensional result on its left (i.e.,
```
```
x + y[:,None]). The caveat about broadcasting is that it can potentially create
```
large, memory-consuming, intermediate arrays. There are methods for controlling
this by re-using previously allocated memory but that is beyond our scope here.
Formulas in physics that evaluate functions on the vertices of high dimensional grids
are great use-cases for broadcasting.
```
>>> x = np.array([0,1])>>> y = np.array([0,1,2])
```
```
>>> z = np.array([0,1,2,3])>>> x+y[:,None]+z[:,None,None]
```
```
array([ [ [0, 1],[1, 2],
```
[2, 3] ],[ [1, 2],
[2, 3],[3, 4] ],
[ [2, 3],[3, 4],
[4, 5] ],[ [3, 4],
```
[4, 5],[5, 6] ] ])
```
12 1 Getting Started with Scientific Python
1.2.4 Numpy Masked Arrays
Numpy provides a powerful method to temporarily hide array elements without
changing the shape of the array itself,
```
>>> from numpy import ma # import masked arrays>>> x = np.arange(10)
```
```
>>> y = ma.masked_array(x, x<5)>>> print y
```
[-- -- -- -- -- 5 6 7 8 9]>>> print y.shape
```
(10,)
```
```
Note that the elements in the array for which the logical condition (x < 5) is true
```
are masked, but the size of the array remains the same. This is particularly useful in
plotting categorical data, where you may only want those values that correspond to
a given category for part of the plot. Another common use is for image processing,
wherein parts of the image may need to be excluded from subsequent processing.
Note that creating a masked array does not force an implicit copy operation unless
```
copy=True argument is used. For example, changing an element in x does change
```
the corresponding element in y, even though y is a masked array,
>>> x[-1] = 99 # change this>>> print x
>>> print y # masked array changed![ 0 1 2 3 4 5 6 7 8 99]
[-- -- -- -- -- 5 6 7 8 99]
1.2.5 Numpy Optimizations and Prospectus
The scientific Python community continues to push the frontier of scientific com-
puting. Several important extensions to Numpy are under active development. First,
Numba is a compiler that generates optimized machine code from pure Python code
using the LLVM compiler infrastructure. LLVM started as a research project at
the University of Illinois to provide a target-independent compilation strategy for
arbitrary programming languages and is now a well-established technology. The
combination of LLVM and Python via Numba means that accelerating a block of
Python code can be as easy as putting a @numba.jit decorator above the function
definition, but this doesn’t work for all situations. Numba can target general graphics
```
processing units (GPGPUs) also.
```
Blaze is considered the next generation of Numpy and generalizes the semantics
of Numpy for very large data sets that exist on a variety of backend filesystems.
```
This means that Blaze is designed to handle out-of-core (i.e., too big to fit in a
```
```
single workstation’s RAM) data manipulations and computations using the familiar
```
```
operations from Numpy. Further, Blaze offers tight integration with Pandas (see
```
```
Sect. 1.6) dataframes. Roughly speaking, Blaze understands how to unpack Python
```
expressions and translate them for a variety of distributed backend data services
```
upon which the computing will actually happen (i.e., using blaze.compute).
```
1.2 Numpy 13
This means that Blaze separates the expression of the computation from the particular
implementation on a given backend.
Building on his amazing work on PyTables, Francesc Alted has been working on
the bcolz module which is a compressed columnar data container. Also motivated
by out-of-core data and computing, bcolz tries to relieve the stress of the memory
subsystem by compressing data in memory and then interleaving computations on
the compressed data in an intelligent way. This approach takes advantage of emerging
architectures that have more cores and wider vector units.
1.3 Matplotlib
Matplotlib is the primary visualization tool for scientific graphics in Python. Like all
great open-source projects, it originated to satisfy a personal need. At the time of its
inception, John Hunter primarily used Matlab for scientific visualization, but as he
began to integrate data from disparate sources using Python, he realized he needed
a Python solution for visualization, so he single-handedly wrote Matplotlib. Since
those early years, Matplotlib has displaced the other competing methods for two-
dimensional scientific visualization and today is a very actively maintained project,
even without John Hunter, who sadly passed away in 2012.
John had a few basic requirements for Matplotlib:
• Plots should look publication quality with beautiful text.
• Plots should output Postscript for inclusion within LATEX documents and publica-
tion quality printing.
```
• Plots should be embeddable in a Graphical User Interface (GUI) for application
```
development.
• The code should be mostly Python to allow for users to become developers.
• Plots should be easy to make with just a few lines of code for simple graphs.
Each of these requirements has been completely satisfied and Matplotlib’s capabili-
ties have grown far beyond these requirements. In the beginning, to ease the transition
from Matlab to Python, many of the Matplotlib functions were closely named after
the corresponding Matlab commands. The community has moved away from this
style and, even though you will still find the old Matlab-esque style used in the
on-line Matplotlib documentation.
The following shows the quickest way to draw a plot using Matplotlib and the
plain Python interpreter. Later, we’ll see how to do this even faster using IPython. The
first line imports the requisite module as plt which is the recommended convention.
The next line plots a sequence of numbers generated using Python’s range function.
Note the output list contains a Line2D object. This is an artist in Matplotlib parlance.
```
Finally, the plt.show() function draws the plot in a GUI figure window.
```
14 1 Getting Started with Scientific Python
Fig. 1.1 The Matplotlib figure window. The icons on the bottom allow some limited plot-editing
tools
```
>>> import matplotlib.pyplot as plt>>> plt.plot(range(10))
```
```
[<matplotlib.lines.Line2D object at 0x00CB9770>]>>> plt.show() # unnecessary in IPython (discussed later)
```
```
If you try this in your own plain Python interpreter (and you should), you will see
```
that you cannot type in anything further in the interpreter until the figure window
```
(i.e., something like Fig. 1.1) is closed. This is because the plt.show() function
```
preoccupies the interpreter with the controls in the GUI and blocks further interaction.
As we discuss below, IPython provides ways to get around this blocking so you can
simultaneously interact with the interpreter and the figure window.3
As shown in Fig. 1.1, the plot function returns a list containing the Line2D
object. More complicated plots yield larger lists filled with artists. The suggestion
is that artists draw on the canvas contained in the Matplotlib figure. The final line
is the plt.show function that provokes the embedded artists to render on the
Matplotlib canvas. The reason this is a separate function is that plots may have
dozens of complicated artists and rendering may be a time-consuming task to only
```
3 You can also do this in the plain Python interpreter by doing import matplotlib;
```
```
matplotlib.interactive(True).
```
1.3 Matplotlib 15
be undertaken at the end, when all the artists have been mustered. Matplotlib supports
plotting images, contours, and many others that we cover in detail in the following
chapters.
Even though this is the quickest way to draw a plot in Matplotlib, it is not recom-
mended because there are no handles to the intermediate products of the plot such
as the plot’s axis. While this is okay for a simple plot like this, later on we will see
how to construct complicated plots using the recommended method. There is a close
working relationship between Numpy and Matplotlib and you can load Matplotlib’s
plotting functions and Numpy’s functions simultaneously using pylab as from
matplotlib.pylab import *. Although importing everything this way as a
standard practice is not recommended because of namespace pollution.
One of the best ways to get started with Matplotlib is to browse the extensive on-
line gallery of plots on the main Matplotlib site. Each plot comes with corresponding
source code that you can use as a starting point for your own plots. In Sect. 1.4, we
discuss special magic commands that make this particularly easy. The annual John
```
Hunter: Excellence in Plotting Contest provides fantastic, compelling examples of
```
scientific visualizations that are possible using Matplotlib.
1.3.1 Alternatives to Matplotlib
Even though Matplotlib is unbeatable for script-based plotting, there are some alter-
natives for specialized scientific graphics that may be of interest.
```
Chaco is part of the Enthought Tool-Suite (ETS) and implements many real-
```
time data visualization concepts and corresponding widgets. It is available on all of
the major platforms and is also actively maintained and well-documented. Chaco
is geared towards GUI application development, rather than script-based data visu-
alization. It depends on the Traits package, which is also available in ETS and
in the Enthought Canopy. If you don’t want to use Canopy, then you have to build
Chaco and its dependencies separately. On Linux, this should be straight-forward,
but potentially a nightmare on Windows if not for Christoph Gohlke’s installers or
Anaconda’s conda package manager.
If you require real-time data display and tools for volumetric data rendering and
complicated 3D meshes with isosurfaces, then PyQtGraph is an option. PyQtGraph
is a pure-Python graphics and GUI library that depends on Python bindings for the Qt
```
GUI library (i.e., PySide or PyQt4) and Numpy. This means that the PyQtGraph
```
```
relies on these other libraries (especially Qt’s GraphicsView framework) for the
```
heavy-duty numbercrunching and rendering. This package is actively maintained,
```
but is still pretty new, with good (but not comprehensive) documentation. You also
```
need to grasp a few Qt-GUI development concepts to use this effectively. Mayavi
```
is another Enthought-supported 3D visualization package that sits on VTK (open-
```
```
source C++ library for 3D visualization). Like Chaco, it is a toolkit for scientific
```
GUI development as opposed to script-based plotting. To use it effectively, you need
16 1 Getting Started with Scientific Python
```
to already know (or be willing to learn) about graphics pipelines. This package is
```
actively supported and well-documented.
An alternative that comes from the R community is ggplot which is a Python
port of the ggplot2 package that is fundamental to statistical graphics in R. From
the Python standpoint, the main advantage of ggplot is the tight integration with
the Pandas dataframe, which makes it easy to draw beautifully formatted statistical
graphs. The downside of this package is that it applies un-Pythonic semantics based
on the Grammer of Graphics [4], which is nonetheless a well-thought-out method
for articulating complicated graphs. Of course, because there are two-way bridges
```
between Python and R via the R2Py module (among others), it is workable to send
```
Numpy arrays to R for native ggplot2 rendering and then retrieve the so-computed
graphic back into Python. This is a workflow that is lubricated by the IPython Note-
book via the rmagic extension. Thus, it is quite possible to get the best of both
worlds via the IPython Notebook and this kind of multi-language workflow is quite
common in data analysis communities.
1.3.2 Extensions to Matplotlib
Initially, to encourage adoption of Matplotlib from Matlab, many of the graphical
sensibilities were adopted from Matlab to preserve the look and feel for transitioning
users. Modern sensibilities and prettier default plots are possible because Matplotlib
provides the ability to drill down and tweak just about every element on the canvas.
However, this can be tedious to do and several alternatives offer relief. For statistical
plots, the first place to look is the seaborn module that includes a vast array of
beautifully formatted plots including violin plots, kernel density plots, and bivari-
ate histograms. The seaborn gallery includes samples of available plots and the
corresponding code that generates them. Note that importing seaborn hijacks the
default settings for all plots, so you have to coordinate this if you only want to use
```
seaborn for some (not all) of your visualizations in a given session. Note that you
```
can find the defaults for Matplotlib in the matplotlib.rcParams dictionary.
The prettyplotlib module, like seaborn, provides an intelligent default
color palate based on Cynthia Brewer’s work on color perception
```
(c.f. colorbrewer2.org). Unfortunately, this work is no longer supported by
```
the author, but still provides a great set of plotting tools and designs for building
beautiful data visualizations.
1.4 IPython
IPython [5] originated as a way to enhance Python’s basic interpreter for smooth
interactive scientific development. In the early days, the most important enhancement
was tab-completion for dynamic introspection of workspace variables. For example,
1.4 IPython 17
you can start IPython at the commandline by typing ipython and then you should
see something like the following in your terminal:
```
Python 2.7.11 |Continuum Analytics, Inc.| (default, Dec 7 2015, 14:00
```
Type "copyright", "credits" or "license" for more information.
IPython 4.0.0 -- An enhanced Interactive Python.
? -> Introduction and overview of IPython’s features.
help -> Python’s own help system.
object? -> Details about ’object’, use ’object??’ for extra details.
In [1]:
Next, creating a string as shown and hitting the TAB key after the dot character
initiates the introspection, showing all the functions and attributes of the string
object in x.
In [1]: x = ’this is a string’
In [2]: x.<TAB>
x.capitalize x.format x.isupper x.rindex x.strip
x.center x.index x.join x.rjust x.swapcase
x.count x.isalnum x.ljust x.rpartition x.title
x.decode x.isalpha x.lower x.rsplit x.translate
x.encode x.isdigit x.lstrip x.rstrip x.upper
x.endswith x.islower x.partition x.split x.zfill
x.expandtabs x.isspace x.replace x.splitlines
x.find x.istitle x.rfind x.startswith
To get help about any of these, you simply add the ? character at the end as shown
below,
In [2]: x.center?
```
Type: builtin_function_or_method
```
String Form:<built-in method center of str object at 0x03193390>
```
Docstring:
```
```
S.center(width[, fillchar]) -> string
```
Return S centered in a string of length width. Padding is
```
done using the specified fill character (default is a space)
```
and IPython provides the built-in help documentation. Note that you can also get this
```
documentation with help(x.center) which works in the plain Python interpreter
```
as well.
The combination of dynamic tab-based introspection and quick interactive help
accelerates development because you can keep your eyes and fingers in one place as
you work. This was the original IPython experience, but IPython has since grown
into a complete framework for delivering a rich scientific computing workflow that
retains and enhances these fundamental features.
18 1 Getting Started with Scientific Python
1.4.1 IPython Notebook
As you may have noticed investigating Python on the web, most Python users are
web-developers, not scientific programmers, meaning that the Python stack is very
well developed for web technologies. The genius of the IPython development team
was to leverage these technologies for scientific computing by embedding IPython
in modern web-browsers. In fact, this strategy has been so successful that IPython
has moved into other languages beyond Python such as Julia and R as the Jupyter
project. 4
You can start the IPython Notebook with the following commandline:
’jupyter notebook’. After starting the notebook, you should see something
like the following in the terminal,
[W 10:26:55.332 NotebookApp] ipywidgets package not installed. Widgets
[I 10:26:55.348 NotebookApp] Serving notebooks from local directory: D:\
[I 10:26:55.351 NotebookApp] 0 active kernels
[I 10:26:55.351 NotebookApp] The IPython Notebook is running at: http://
[I 10:26:55.351 NotebookApp] Use Control-C to stop this server and shut
The first line reveals where IPython looks for default settings. The next line shows
where it looks for documents in the IPython Notebook format. The third line
```
shows that the IPython Notebook started a web-server on the local machine (i.e.,
```
```
127.0.0.1) on port number 8888. This is the address your browser needs to
```
connect to the IPython session although your default browser should have opened
automatically to this address. The port number and other configuration options are
available either on the commandline or in the profile file shown in the first line.
If you are on a Windows platform and you do not get this far, then the Window’s
firewall is probably blocking the port. For additonal configuration help, see the main
```
IPython site (www.ipython.org) or e-mail the very responsive IPython mailing
```
```
list (ipython-dev@scipy.org).
```
When IPython starts, it initiates many small Python processes that use the
blazing-fast ZeroMQ message passing framework for interprocess-communication,
along with the web-sockets protocol for back-and-forth communication with the
browser. To start IPython and get around your default browser, you can use the
additonal —no-browser flag and then manually type in the local host address
```
http://127.0.0.1:8888 into your favorite browser to get started. Once all
```
that is settled, you should see something like the following Fig. 1.2.
You can create a new document by clicking the New Notebook button shown in
Fig. 1.2. Then, you should see something like Fig. 1.3. To start using the IPython Note-
book, you just start typing code in the shaded textbox and then hit SHIFT+ENTER
to execute the code in that IPython cell. Figure 1.4 shows the dynamic introspection
in the pulldown menu when you type the TAB key after the x.. Context-based help is
also available as before by using the ? suffix which opens a help panel at the bottom
of the browser window. There are many amazing features including the ability to
4 Because we are primarily focused on Python in this text we will continue to refer to IPython and
the IPython Notebook instead of to the more general Jupyter project. At the time of this writing,
the re-factorization of IPython into Jupyter has not been completed.
1.4 IPython 19
Fig. 1.2 The IPython Notebook dashboard
Fig. 1.3 A new IPython Notebook
share notebooks between different users and to run IPython Notebooks in the Ama-
zon cloud, but these features go beyond our scope here. Check the ipython.org
website or peek at the mailing list for the lastest work on these fronts.
The IPython Notebook supports high-quality mathematical typesetting using
MathJaX, which is a JavaScript implementation of most of LATEX, as well as video and
other rich content. The concept of consolidating mathematical algorithm descriptions
and the code that implements those algorithms into a shareable document is more
important than all of these amazing features. There is no understating the importance
```
of this in practice because the algorithm documentation (if it exists) is usually in one
```
format and completely separate from the code that implements it. This common
practice leads to un-synchronized documentation and code that renders one or the
20 1 Getting Started with Scientific Python
Fig. 1.4 IPython Notebook pulldown completion menu
other useless. The IPython Notebook solves this problem by putting everything into a
living shareable document based upon open standards and freely available software.
IPython Notebooks can even be saved as static HTML documents for those without
Python!
Finally, IPython provides a large set of magic commands for creating macros,
profiling, debugging, and viewing codes. A full list of these can be found by typing
in %lsmagic in IPython. Help on any of these is available using the ? character
suffix. Some frequently used commands include the %cd command that changes
the current working directory, the %ls command that lists the files in the current
directory, and the %hist command that shows the history of previous commands
```
(including optional searching). The most important of these for new users is probably
```
the %loadpy command that can load scripts from the local disk or from the web.
Using this to explore the Matplotlib gallery is a great way to experiment with and
re-use the plots there.
1.5 Scipy
Scipy was the first consolidated module for a wide range of compiled libraries,
```
all based on Numpy arrays. Scipy includes numerous special functions (e.g., Airy,
```
```
Bessel, elliptical) as well as powerful numerical quadrature routines via the QUAD-
```
```
PACK Fortran library (see scipy.integrate), where you will also find other
```
quadrature methods. Note that some of the same functions appear in multiple
places within Scipy itself as well as in Numpy. Additionally, Scipy provides access
to the ODEPACK library for solving differential equations. Lots of statistical
1.5 Scipy 21
functions, including random number generators, and a wide variety of probabil-
ity distributions are included in the scipy.stats module. Interfaces to the For-
tran MINPACK optimization library are provided via scipy.optimize. These
include methods for root-finding, minimization and maximization problems, with
and without higher-order derivatives. Methods for interpolation are provided in the
scipy.interpolate module via the FITPACK Fortran package. Note that some
of the modules are so big that you do not get all of them with import scipy
because that would take too long to load. You may have to load some of these pack-
ages individually as import scipy.interpolate, for example.
As we discussed, the Scipy module is already packed with an extensive list of
scientific codes. For that reason, the scikits modules were originally established
as a way to stage candidates that could eventually make it into the already stuffed
Scipy module, but it turns out that many of these modules became so successful on
their own that they will never be integrated into Scipy proper. Some examples include
sklearn for machine learning and scikit-image for image processing.
1.6 Pandas
Pandas [6] is a powerful module that is optimized on top of Numpy and provides
a set of data structures particularly suited to time-series and spreadsheet-style data
```
analysis (think of pivot tables in Excel). If you are familiar with the R statistical
```
package, then you can think of Pandas as providing a Numpy-powered dataframe for
Python.
1.6.1 Series
There are two primary data structures in Pandas. The first is the Series object
which combines an index and corresponding data values.
```
>>> import pandas as pd # recommended convention>>> x=pd.Series(index = range(5),data=[1,3,9,11,12])
```
>>> x0 1
1 32 9
3 114 12
The main thing to keep in mind with Pandas is that these data structures were orig-
inally designed to work with time-series data. In that case, the index in the data
structures corresponds to a sequence of ordered time-stamps. In the general case, the
index must be a sort-able array-like entity. For example,
```
>>> x=pd.Series(index = [’a’,’b’,’d’,’z’,’z’],data=[1,3,9,11,12])>>> x
```
22 1 Getting Started with Scientific Python
a 1b 3
d 9z 11
z 12
Note the duplicated z entries in the index. We can get at the entries in the Series
in a number of ways. First, we can used the dot notation to select as in the following:
>>> x.a1
>>> x.zz 11
z 12
We can also use the indexed-position of the entries with iloc as in the following:
>>> x.iloc[:3]a 1
b 3d 9
which uses the same slicing syntax as Numpy arrays. You can also slice across the
index, even if it is not numeric with loc as in the following:
>>> x.loc[’a’:’d’]a 1
b 3d 9
which you can get directly from the usual slicing notation:
>>> x[’a’:’d’]a 1
b 3d 9
Note that, unlike Python, slicing this way includes the endpoints. While that is
very interesting, the main power of Pandas comes from its power to aggregate and
group data. In the following, we build a more interesting Series object,
```
>>> x = pd.Series(range(5),[1,2,11,9,10])1 0
```
2 111 2
9 310 4
and then group it in the following:
```
>>> grp=x.groupby(lambda i:i%2) # odd or even>>> grp.get_group(0) # even group
```
2 110 4
```
>>> grp.get_group(1) # odd group1 0
```
11 29 3
The first line groups the elements of the Series object by whether or not the index
is even or odd. The lambda function returns 0 or 1 depending on whether or not the
```
corresponding index is even or odd, respectively. The next line shows the 0 (even)
```
1.6 Pandas 23
```
group and then the one after shows the 1 (odd) group. Now, that we have separate
```
groups, we can perform a wide-variety of summarizations on the group. You can think
of these as reducing each group into a single value. For example, in the following,
we get the maximum value of each group:
```
>>> grp.max() # max in each group0 4
```
1 3
Note that the operation above returns another Series object with an index cor-
responding to the [0,1] elements.
1.6.2 Dataframe
The Pandas DataFrame is an encapsulation of the Series that extends to two-
dimensions. One way to create a DataFrame is with dictionaries as in the following:
```
>>> df = pd.DataFrame({’col1’: [1,3,11,2], ’col2’: [9,23,0,2]})col1 col2
```
0 1 91 3 23
2 11 03 2 2
```
Note that the keys in the input dictionary are now the column-headings (labels) of the
```
DataFrame, with each corresponding column matching the list of corresponding
values from the dictionary. Like the Series object, the DataFrame also has in
index, which is the [0,1,2,3] column on the far-left. We can extract elements
from each column using the iloc method as discussed earlier as shown below:
>>> df.iloc[:2,:2] # get sectioncol1 col2
0 1 91 3 23
or by directly slicing or by using the dot notation as shown below:
>>> df[’col1’] # indexing0 1
1 32 11
3 2>>> df.col1 # use dot notation
0 11 3
2 113 2
Subsequent operations on the DataFrame preserve its column-wise structure as in
the following:
```
>>> df.sum()col1 17
```
col2 34
where each column was totaled. Grouping and aggregating with the dataframe is
even more powerful than with Series. Let’s construct the following dataframe,
24 1 Getting Started with Scientific Python
```
>>> df = pd.DataFrame({’col1’: [1,1,0,0], ’col2’: [1,2,3,4]})col1 col2
```
0 1 11 1 2
2 0 33 0 4
In the above dataframe, note that the col1 column has only two entries. We can
group the data using this column as in the following:
```
>>> grp=df.groupby(’col1’)>>> grp.get_group(0)
```
col1 col22 0 3
```
3 0 4>>> grp.get_group(1)
```
col1 col20 1 1
1 1 2
Note that each group corresponds to entries for which col1 was either of its two
values. Now that we have grouped on col1, as with the Series object, we can also
functionally summarize each of the groups as in the following:
```
>>> grp.sum()col2
```
col10 7
1 3
where the sum is applied across each of the Dataframes present in each group. Note
that the index of the output above is each of the values in the original col1.
The Dataframe can compute new columns based on existing columns using the
eval method as shown below:
```
>>> df[’sum_col’]=df.eval(’col1+col2’)>>> df
```
col1 col2 sum_col0 1 1 2
1 1 2 32 0 3 3
3 0 4 4
Note that you can assign the output to a new column to the Dataframe as shown. 5
We can group by multiple columns as shown below:
```
>>> grp=df.groupby([’sum_col’,’col1’])
```
Doing the sum operation on each group gives the following:
```
>>> res=grp.sum()>>> res
```
col2sum_col col1
2 1 13 0 3
1 24 0 4
5 Note this kind of on-the-fly memory extension is not possible in regular Numpy. For example,
```
x = np.array([1,2]); x[3]=3 generates an error.
```
1.6 Pandas 25
This output is much more complicated than anything we have seen so far, so let’s
carefully walk through it. Below the headers, the first row 2 1 1 indicates that for
```
sum_col=2 and for all values of col1 (namely, just the value 1), the value of col2
```
is 1. For the next row, the same pattern applies except that for sum_col=3, there are
now two values for col1, namely 0 and 1, which each have their corresponding two
values for the sum operation in col2. This layered display is one way to look at the
result. Note that the layers above are not uniform. Alternatively, we can unstack
this result to obtain the following tabular view of the previous result:
```
>>> res.unstack()col2
```
col1 0 1sum_col
2 NaN 13 3 2
4 4 NaN
The NaN values indicate positions in the table where there is no entry. For exam-
```
ple, for the pair (sum_col=2,col2=0), there is no corresponding value in the
```
Dataframe, as you may verify by looking at the penultimate code block. There is also
```
no entry corresponding to the (sum_col=4,col2=1) pair. Thus, this shows that
```
the original presentation in the penultimate code block is the same as this one, just
without the above-mentioned missing entries indicated by NaN.
We have barely scratched the surface of what Pandas is capable of and we have
completely ignored its powerful features for managing dates and times. The text by
Mckinney [6] is a very complete and happily readable introduction to Pandas. The
online documentation and tutorials at the main Pandas site are also great for diving
deeper into Pandas.
1.7 Sympy
Sympy [7] is the main computer algebra module in Python. It is a pure-Python
package with no platform-dependencies. With the help of multiple Google Summer of
Code sponsorships, it has grown into a powerful computer algebra system with many
collateral projects that make it faster and integrate it tighter with Numpy and IPython
```
(among others). Sympy’s on-line tutorial is excellent and allows interacting with its
```
embedded code samples in the browser by running the code on the Google App
Engine behind the scenes. This provides an excellent way to interact and experiment
with Sympy.
If you find Sympy too slow or need algorithms that it does not implement, then
SAGE is your next stop. The SAGE project is a consolidation of over 70 of the
best open source packages for computer algebra and related computation. Although
Sympy and SAGE share code freely between them, SAGE is a specialized build of
the Python kernel to facilitate deep integration with the underlying libraries. Thus,
```
it is not a pure-Python solution for computer algebra (i.e., not as portable) and it is a
```
proper superset of Python with its own extended syntax. The choice between SAGE
26 1 Getting Started with Scientific Python
and Sympy really depends on whether or not you intend primarily work in SAGE or
just need occasional computer algebra support in your existing Python code.
An important new development regarding SAGE is the freely available SAGE
```
Cloud (https://cloud.sagemath.com/), sponsored by University of Washington that
```
allows you to use SAGE entirely in the browser with no additional setup. Both
SAGE and Sympy offer tight integration with the IPython Notebook for mathematical
typesetting in the browser using MathJaX.
To get started with Sympy, you must import the module as usual,
>>> import sympy as S # might take awhile
which may take a bit because it is a big package. The next step is to create a Sympy
variable as in the following:
```
>>> x = S.symbols(’x’)
```
Now we can manipulate this using Sympy functions and Python logic as shown
```
below:
```
```
>>> p=sum(x**i for i in range(3)) # 2nd order polynomial>>> p
```
x**2 + x + 1
Now, we can find the roots of this polynomial using Sympy functions,
```
>>> S.solve(p) # solves p == 0[-1/2 - sqrt(3)*I/2, -1/2 + sqrt(3)*I/2]
```
There is also a sympy.roots function that provides the same output but as a
dictionary.
```
>>> S.roots(p){-1/2 - sqrt(3)*I/2: 1, -1/2 + sqrt(3)*I/2: 1}
```
We can also have more than one symbolic element in any expression as in the fol-
```
lowing:
```
>>> from sympy.abc import a,b,c # quick way to get common symbols>>> p = a* x**2 + b*x + c
```
>>> S.solve(p,x) # specific solving for x-variable[(-b + sqrt(-4*a*c + b**2))/(2*a), -(b + sqrt(-4*a*c + b**2))/(2*a)]
```
which is the usual quadratic formula for roots. Sympy also provides many mathe-
matical functions designed to work with Sympy variables. For example,
```
>>> S.exp(S.I*a) #using Sympy exponential
```
We can expand this using expand_complex to obtain the following:
```
>>> S.expand_complex(S.exp(S.I*a))I*exp(-im(a))*sin(re(a)) + exp(-im(a))*cos(re(a))
```
which gives us Euler’s formula for the complex exponential. Note that Sympy does
not know whether or not a is itself a complex number. We can fix this by making
that fact part of the construction of a as in the following:
1.7 Sympy 27
```
>>> a = S.symbols(’a’,real=True)>>> S.expand_complex(S.exp(S.I*a))
```
```
I*sin(a) + cos(a)
```
Note the much simpler output this time because we have forced the additional con-
dition on a.
A powerful way to use Sympy is to construct complicated expressions that you
can later evaluate using Numpy via the lambdify method. For example,
```
>>> y = S.tan(x) * x + x**2>>> yf= S.lambdify(x,y,’numpy’)
```
```
>>> y.subs(x,.1) # evaluated using Sympy0.0200334672085451
```
```
>>> yf(.1) # evaluated using Numpy0.0200334672085451
```
After creating the Numpy function with lambdify, you can use Numpy arrays as
input as shown:
```
>>> yf(np.arange(3)) # input is Numpy array
```
```
array([ 0. , 2.55740772, -0.37007973])
```
```
>>> [ y.subs(x,i).evalf() for i in range(3) ] # need extra work for Sympy
```
[0, 2.55740772465490, -0.370079726523038]
We can get the same output using Sympy, but that requires the extra programming
logic shown to do the vectorizing that Numpy performs natively.
Once again, we have merely scratched the surface of what Sympy is capable of
and the on-line interactive tutorial is the best place to learn more. Sympy also allows
automatic mathematical typesetting within the IPython Notebook using LATEX so the
```
so-constructed notebooks look almost publication-ready (see sympy.latex) and
```
can be made so with the ipython nbconvert command. This makes it easier
to jump the cognitive gap between the Python code and the symbology of traditional
mathematics.
1.8 Interfacing with Compiled Libraries
As we have discussed, Python for scientific computing really consists of gluing
together different scientific libraries written in a compiled language like C or Fortran.
Ultimately, you may want to use libraries not available with existing Python bindings.
There are many, many options for doing this. The most direct way is to use the
built-in ctypes module which provides tools for providing input/output pointers
to the library’s functions just as if you were calling them from a compiled language.
This means that you have to know the function signatures in the library exactly—how
many bytes for each input and how many bytes for the output. You are responsible
for building the inputs exactly the way the library expects and collecting the resulting
outputs. Even though this seems tedious, Python bindings for vast libraries have been
built this way.
If you want an easier way, then SWIG is an automatic wrapper generating tool
```
that can provide bindings to a long list of languages, not just Python; so if you need
```
28 1 Getting Started with Scientific Python
bindings for multiple languages, then this is your best and only option. Using SWIG
consists of writing an interface file so that the compiled Python dynamically linked
```
library (Python PYD) can be readily imported into the Python interpreter. Huge and
```
```
complex libraries like Trilinos (Sandia National Labs) have been interfaced to Python
```
using SWIG, so it is a well-tested option. SWIG also supports Numpy arrays.
However, the SWIG model assumes that you want to continue developing primar-
ily in C/Fortran and you are hooking into Python for usability or other reasons. On
the other hand, if you start developing algorithms in Python and then want to speed
them up, then Cython is an excellent option because it provides a mixed language
that allows you to have both C-language and Python code intermixed. Like SWIG,
you have to write additional files in this hybrid Python/C dialect to have Cython
generate the C-code that you will ultimately compile. The best part of Cython
is the profiler that can generate an HTML report showing where the code is slow
and could benefit from translation to Cython. The IPython Notebook integrates
nicely with Cython via its %cython magic command. This means you can write
Cython code in a cell in IPython Notebook and the notebook will handle all of the
tedious details like setting up the intermediate files to actually compile the Cython
extension. Cython also supports Numpy arrays.
Cython and SWIG are just two of the ways to create Python bindings for your
```
favorite compiled libraries. Other notable (but less popular) options include FWrap,
```
f2py, CFFI, and weave. It is also possible to use Python’s own API directly, but
this is a difficult undertaking that is hard to justify given the existence of so many
well-developed alternatives.
1.9 Integrated Development Environments
```
For those who prefer Integrated Development Environments (IDEs), there is a lot
```
to choose from. The most comprehensive is Enthought Canopy, which includes a
rich, syntax-highlighted editor, integrated help, debugger, and even integrated train-
ing. If you are already familiar with Eclipse from other projects, or do mixed-
language programming, then there is a Python plugin called PyDev that contains all
usual features from Eclipse with a Python debugger. Wingware provides an afford-
able professional-level IDE with multi-project management support and unusually
clairvoyant code-completion that works even in debug-mode. Another favorite is
PyCharm, which also supports multiple languages and is particularly popular among
Python web-developers because it provides powerful templates for popular web
frameworks like Django. NinjaIDE is relatively new, but has quickly developed a
strong following among Python newcomers because of its beautiful interface and
easy-to-get-started framework. If you are a VIM user, then the Jedi plugin provides
excellent code-completion that works well with pylint, which provides static code
```
analysis (i.e., identifies missing modules and typos). Naturally, emacs has many
```
related plugins for developing in Python. Note that are many other options, but I
have tried to emphasize those most suitable for Python beginners.
1.10 Quick Guide to Performance and Parallel Programming 29
1.10 Quick Guide to Performance and Parallel
Programming
There are many options available to improve the performance of your Python codes.
The first thing to determine is what is limiting your computation. It could be CPU
```
speed (unlikely), memory limitations (out-of-core computing), or it could be data
```
```
transfer speed (waiting on data to arrive for processing). If your code is pure-Python,
```
then you can try running it with Pypy, which is is an alternative Python implementa-
tion that employs a just-in-time compiler. If your code does not experience a massive
speed-up with Pypy, then there is probably something external to the code that is
```
slowing it down (e.g., disk access or network access). If Pypy doesn’t make any
```
sense because you are using many compiled modules that Pypy does not support,
then there are many diagnostic tools available.
Python has its own built-in profiler cProfile you can invoke from the command
line as in the following
>>> python -m cProfile -o program.prof my_program.py
The output of the profiler is saved to the program.prof file. This file can be visual-
ized in runsnakerun to get a nice graphical picture of where the code is spending
the most time. The task manager on your operating system can also provide clues as
your program runs to see how it is consuming resources. The line_profiler by
Robert Kern provides an excellent way to see how the code is spending its time by
annotating each line of the code by its timings. In combination with runsnakerun,
this narrows down problems to the line-level from the function-level.
The most common situation is that your program is waiting on data from disk
or from some busy network resource. This is a common situation in web program-
ming and there are lots of well-established tools to deal with this. Python has a
multiprocessing module that is part of the standard library. This makes it easy
to spawn child worker processes that can break off and individually process small
parts of a big job. However, it is still your responsibility as the programmer to figure
out how to distribute the data for your algorithm. Using this module means that the
individual processes are to be managed by the operating system, which will be in
charge of balancing the load.
The basic template for using multiprocessing is the following:
# filename multiprocessing_demo.pyimport multiprocessing
```
import timedef worker(k):
```
```
’worker function’print ’am starting process %d’ % (k)
```
```
time.sleep(10) # wait ten secondsprint ’am done waiting!’
```
return
```
if __name__ == ’__main__’:for i in range(10):
```
```
p = multiprocessing.Process(target=worker, args=(i,))p.start()
```
30 1 Getting Started with Scientific Python
Then, you run this program at the terminal as in the following,
Terminal> python multiprocessing_demo.py
It is crucially important that you run the program from the terminal this way. It is not
possible to do this interactively from within IPython, say. If you look at the process
manager on the operating system, you should see a number of new Python processes
loitering for ten seconds. You should also see the output of the print statements
above. Naturally, in a real application, you would be assigning some meaningful work
for each of the workers and figuring out how to send partially finished pieces between
individual workers. Doing this is complex and easy to get wrong, so Python 3.2 has
the helpful concurrent.futures module that has thankfully been back-ported
to Python 2.7 and is available on pypi.
# filename: concurrent_demo.py
import futures
import time
```
def worker(k):
```
’worker function’
```
print ’am starting process %d’ % (k)
```
```
time.sleep(10) # wait ten seconds
```
print ’am done waiting!’
return
```
def main():
```
```
with futures.ProcessPoolExecutor(max_workers=3) as executor:
```
```
list(executor.map(worker,range(10)))
```
if __name__ == ’__main__’:
```
main()
```
Terminal> python concurrent_demo.py
You should see something like the following in the terminal. Note that we explicitly
restricted the number of processes to three.
am starting process 0am starting process 1
am starting process 2am done waiting!
am done waiting!...
The futures module is built on top of multiprocessing and makes it eas-
ier to use for this kind of simple task. Note that there are also versions of both that
use threads instead of processes while maintaining the same usage pattern. The main
difference between threads and processes is that processes have their own compart-
```
mentalized resources. The C-language Python (i.e., CPython) implementation uses
```
```
a Global Interpreter Lock (GIL) that prevents threads from locking up on internal
```
data structures. This is a course-grained locking mechanism where one thread may
individually run faster because it does not have to keep track of all the bookkeep-
ing involved in running multiple threads simultaneously. The downside is that you
cannot run multiple threads simultaneously to speed up certain tasks.
1.10 Quick Guide to Performance and Parallel Programming 31
There is no corresponding locking problem with processes but these are somewhat
slower to start up because each process has to create its own private workspace
for data structures that may be transferred between them. However, each process
can certainly run independently and simultaneously once all that is set up. Note
that certain alternative implementations of Python like IronPython use a finer-grain
threading design rather than a GIL approach. As a final comment, on modern systems
with multiple cores, it could be that multiple threads actually slow things down
because the operating system may have to switch threads between different cores.
This creates additional overheads in the thread switching mechanism that ultimately
slow things down.
IPython itself has a parallel programming framework built into it that is powerful
and easy-to-use. The first step is to fire up separate IPython engines at the terminal
as in the following,
Terminal> ipcluster start --n=4
Then, in an IPython window, you can get the client,
```
In [1]: from IPython.parallel import Client...: rc = Client()
```
The client has a connection to each of the processes we started before using
ipcluster. To use all of the engines, we assign the DirectView object from
the client as in the following,
In [2]: dview = rc[:]
Now, we can apply functions for each of the engines. For example, we can get the
process identifiers using the os.getpid function,
```
In [3]: import osIn [4]: dview.apply_sync(os.getpid)
```
Out[4]: [6824, 4752, 8836, 3124]
Once the engines are up and running, data can be distributed to them using scatter,
```
In [5]: dview.scatter(’a’,range(10))Out[5]: <AsyncResult: finished>
```
```
In [6]: dview.execute(’print a’).display_outputs()[stdout:0] [0, 1, 2]
```
[stdout:1] [3, 4, 5][stdout:2] [6, 7]
[stdout:3] [8, 9]
Note that the execute method evaluates the given string in each engine. Now that
the data have been sprinkled among the active engines, we can do further computing
on them,
```
In [7]: dview.execute(’b=sum(a)’)Out[7]: <AsyncResult: finished>
```
```
In [8]: dview.execute(’print b’).display_outputs()[stdout:0] 3
```
[stdout:1] 12[stdout:2] 13
[stdout:3] 17
32 1 Getting Started with Scientific Python
In this example, we added up the individual a sub-lists available on each of the
engines. We can gather up the individual results into a single list as in the following,
```
In [9]: dview.gather(’b’).rOut[9]: [3, 12, 13, 17]
```
This is one of the simplest mechanisms for distributing work to the individual engines
and collecting the results. Unlike the other methods we discussed, you can do this
iteratively, which makes it easy to experiment with how you want to distribute and
compute with the data. The IPython documentation has many more examples of par-
allel programming styles that include running the engines on cloud resources, super-
computer clusters, and across disparate networked computing resources. Although
there are many other specialized parallel programming packages, IPython provides
the best trade-off for generality against complexity across all of the major platforms.
1.11 Other Resources
The Python community is filled with super-smart and amazingly helpful people. One
of the best places to get help with scientific Python is the www.stackoverflow.
com site which hosts a competitive Q&A forum that is particularly welcoming for
Python newbies. Several of the key Python developers regularly participate there and
```
the quality of the answers is very high. The mailing lists for any of the key tools (e.g.,
```
```
Numpy, IPython, Matplotlib) are also great for keeping up with the newest devel-
```
opments. Anything written by Hans Petter Langtangen [8] is excellent, especially if
you have a physics background. The Scientific Python conference held annually in
Austin is also a great place to see your favorite developers in person, ask questions,
and participate in the many interesting sub-groups organized around niche topics.
The PyData workshop is a semi-annual meeting focused on Python for large-scale
data-intensive processing. The PyVideo site provides links to videos of talks and
tutorials related to Python from around the world. A great article that summarizes
best practices in Python for science is [9].
References
1. H. Childs, E.S. Brugger, K.S. Bonnell, J.S. Meredith, M. Miller, B.J. Whitlock, N. Max, A
```
contract-based system for large data visualization. IEEE Vis. 2005, 190–198 (2005)
```
2. MIT Graduate Class Experimental Data. Interactive supercomputings star-p platform: Parallel
```
MATLAB and MPI homework classroom study on high level language productivity (HPEC,
```
```
2006)
```
3. T.E. Oliphant, A Guide to NumPy (Trelgol Publishing, 2006)
4. L. Wilkinson, D. Wills, D. Rope, A. Norton, R. Dubbs, The Grammar of Graphics. Statistics
```
and Computing (Springer, 2006)
```
5. F. Perez, B.E. Granger et al., IPython Software Package for Interactive Scientific Computing.
```
http://ipython.org/
```
References 33
6. W. McKinney, Python for Data Analysis: Data Wrangling with Pandas, NumPy, and IPython
```
(O’Reilly, 2012)
```
7. O. Certik et al., SymPy: Python Library for Symbolic Mathematics. http://sympy.org/
8. H.P. Langtangen, Texts in Computational Science and Engineering, in Python Scripting for
```
Computational Science, vol. 3, 3rd edn. (Springer, 2009)
```
9. D.A. Aruliah, C.T. Brown, N.P.C. Hong, M. Davis, R.T. Guy, S.H.D. Haddock, K. Huff, I.
Mitchell, M.D. Plumbley, B. Waugh, E.P. White, G. Wilson, P. Wilson, Best practices for sci-
```
entific computing. CoRR, (2012). arXiv:abs/1210.0530
```
Chapter 2
Probability
2.1 Introduction
This chapter takes a geometric view of probability theory and relates it to familiar
concepts in linear algebra and geometry. This approach connects your natural geomet-
ric intuition to the key abstractions in probability that can help guide your reasoning.
This is particularly important in probability because it is easy to be misled. We need
a bit of rigor and some intuition to guide us.
```
In grade school, you were introduced to the natural numbers (i.e., 1,2,3,...)
```
and you learned how to manipulate them by operations like addition, subtraction,
and multiplication. Later, you were introduced to positive and negative numbers and
were again taught how to manipulate them. Ultimately, you were introduced to the
calculus of the real line, and learned how to differentiate, take limits, and so on. This
progression provided more abstractions, but also widened the field of problems you
could successfully tackle. The same is true of probability. One way to think about
probability is as a new number concept that allows you to tackle problems that have
a special kind of uncertainty built into them. Thus, the key idea is that there is some
```
number, say x, with a traveling companion, say, f (x), and this companion represents
```
the uncertainties about the value of x as if looking at the number x through a frosted
```
window. The degree of opacity of the window is represented by f (x). If we want to
```
```
manipulate x, then we have to figure out what to do with f (x). For example if we
```
```
want y = 2x, then we have to understand how f (x) generates f (y).
```
Where is the random part? To conceptualize this, we need still another analogy:
```
think about a beehive with the swarm around it representing f (x), and the hive itself,
```
which you can barely see through the swarm, as x. The random piece is you don’t
know which bee in particular is going to sting you! Once this happens the uncertainty
```
evaporates. Up until that happens, all we have is a concept of a swarm (i.e., density of
```
```
bees) which represents a potentiality of which bee will ultimately sting. In summary,
```
one way to think about probability is as a way of carrying through mathematical
```
reasoning (e.g., adding, subtracting, taking limits) with a notion of potentiality that
```
is so-transformed by these operations.
© Springer International Publishing Switzerland 2016
J. Unpingco, Python for Probability, Statistics, and Machine Learning,
DOI 10.1007/978-3-319-30717-6_2
35
36 2 Probability
2.1.1 Understanding Probability Density
In order to understand the heart of modern probability, which is built on the Lesbesgue
theory of integration, we need to extend the concept of integration from basic calculus.
To begin, let us consider the following piecewise function
```
f (x) =
```
⎧
⎪⎨
⎪⎩
1 if 0 < x ≤ 1
2 if 1 < x ≤ 2
0 otherwise
as shown in Fig. 2.1. In calculus, you learned Riemann integration, which you can
apply here as ∫ 2
0
```
f (x)dx = 1 + 2 = 3
```
which has the usual interpretation as the area of the two rectangles that make up
```
f (x). So far, so good.
```
With Lesbesgue integration, the idea is very similar except that we focus on the
```
y-axis instead of moving along the x-axis. The question is given f (x) = 1, what
```
is the set of x values for which this is true? For our example, this is true whenever
```
x ∈ (0, 1]. So now we have a correspondence between the values of the function
```
```
(namely, 1 and 2) and the sets of x values for which this is true, namely, {(0, 1]} and
```
```
{(1, 2]}, respectively. To compute the integral, we simply take the function values
```
```
(i.e., 1,2) and some way of measuring the size of the corresponding interval (i.e., μ)
```
as in the following:
Fig. 2.1 Simple
piecewise-constant function
2.1 Introduction 37
∫ 2
0
```
f dμ = 1μ({(0, 1]}) + 2μ({(1, 2]})
```
We have suppressed some of the notation above to emphasize generality. Note that
```
we obtain the same value of the integral as in the Riemann case when μ((0, 1]) =
```
```
μ((1, 2]) = 1. By introducing the μ function as a way of measuring the intervals
```
above, we have introduced another degree of freedom in our integration. This accom-
modates many weird functions that are not tractable using the usual Riemann theory,
but we refer you to a proper introduction to Lesbesgue integration for further study
[1]. Nonetheless, the key step in the above discussion is the introduction of the μ
function, which we will encounter again as the so-called probability density function.
2.1.2 Random Variables
Most introductions to probability jump straight into random variables and then
explain how to compute complicated integrals. The problem with this approach is
that it skips over some of the important subtleties that we will now consider. Unfortu-
nately, the term random variable is not very descriptive. A better term is measurable
function. To understand why this is a better term, we have to dive into the formal
constructions of probability by way of a simple example.
Consider tossing a fair six-sided die. There are only six outcomes possible,
```
Ω = {1, 2, 3, 4, 5, 6}
```
As we know, if the die is fair, then the probability of each outcome is 1/6. To say
```
this formally, the measure of each set (i.e., {1}, {2}, . . . , {6}) is μ({1}) = μ({2}) . . . =
```
```
μ({6}) = 1/6. In this case, the μ function we discussed earlier is the usual probability
```
mass function, denoted by P. The measurable function maps a set into a number on
```
the real line. For example, {1}  → 1 is one such uninteresting function.
```
Now, here’s where things get interesting. Suppose you were asked to construct
a fair coin from the fair die. In other words, we want to throw the die and then
record the outcomes as if we had just tossed a fair coin. How could we do this?
One way would be to define a measurable function that says if the die comes up
3 or less, then we declare heads and otherwise declare tails. This has some strong
intuition behind it, but let’s articulate it in terms of formal theory. This strategy
```
creates two different non-overlapping sets {1, 2, 3} and {4, 5, 6}. Each set has the
```
same probability measure,
```
P({1, 2, 3}) = 1/2
```
```
P({4, 5, 6}) = 1/2
```
```
And the problem is solved. Everytime the die comes up {1, 2, 3}, we record heads
```
and record tails otherwise.
38 2 Probability
Is this the only way to construct a fair coin experiment from a fair die? Alterna-
```
tively, we can define the sets as {1}, {2}, {3, 4, 5, 6}. If we define the corresponding
```
measure for each set as the following
```
P({1}) = 1/2
```
```
P({2}) = 1/2
```
```
P({3, 4, 5, 6}) = 0
```
then, we have another solution to the fair coin problem. To implement this, all we do
is ignore every time the die shows 3,4,5,6 and throw again. This is wasteful, but
it solves the problem. Nonetheless, we hope you can see how the interlocking pieces
of the theory provide a framework for carrying the notion of uncertainty/potentiality
```
from one problem to the next (e.g., from the fair die to the fair coin).
```
Let’s consider a slightly more interesting problem where we toss two dice. We
assume that each throw is independent, meaning that the outcome of one does not
influence the other. What are the sets in this case? They are all pairs of possible
outcomes from two throws as shown below,
```
Ω = {(1, 1), (1, 2), . . . , (5, 6), (6, 6)}
```
What are the measures of each of these sets? By virtue of the independence claim,
the measure of each is the product of the respective measures of each element. For
instance,
```
P((1, 2)) = P({1})P({2}) = 162
```
With all that established, we can ask the following question: what is the probability
that the sum of the dice equals seven? As before, the first thing to do is characterize
```
the measurable function for this as X : (a, b)  → (a + b). Next, we associate all of
```
```
the (a, b) pairs with their sum. We can create a Python dictionary for this as shown,
```
```
d={(i,j):i+j for i in range(1,7) for j in range(1,7)}
```
```
The next step is to collect all of the (a, b) pairs that sum to each of the possible values
```
from two to twelve.
```
from collections import defaultdictdinv = defaultdict(list)
```
```
for i,j in d.iteritems():dinv[j].append(i)
```
Programming Tip
The defaultdict object from the built-in collections module creates dic-
tionaries with default values when it encounters a new key. Otherwise, we
would have had to create default values manually for a regular dictionary.
2.1 Introduction 39
For example, dinv[7] contains the following list of pairs that sum to seven,
```
[(1, 6), (2, 5), (5, 2), (6, 1), (4, 3), (3, 4)]
```
The next step is to compute the probability measured for each of these items.
Using the independence assumption, this means we have to compute the sum of the
products of the individual item probabilities in dinv. Because we know that each
outcome is equally likely, the probability of every term in the sum equals 1/36. Thus,
all we have to do is count the number of items in the corresponding list for each key in
```
dinv and divide by 36. For example, dinv[11] contains [(5, 6), (6, 5)].
```
The probability of 5+6=6+5=11 is the probability of this set which is composed
```
of the sum of the probabilities of the individual elements (5,6),(6,5). In this
```
```
case, we have P(11) = P({(5, 6)}) + P({(6, 5)}) = 1/36 + 1/36 = 2/36. Repeating
```
this procedure for all the elements, we derive the probability mass function as shown
below,
```
X={i:len(j)/36. for i,j in dinv.iteritems() }print X
```
```
{2: 0.027777777777777776,3: 0.05555555555555555,
```
4: 0.08333333333333333,5: 0.1111111111111111,
6: 0.1388888888888889,7: 0.16666666666666666,
8: 0.1388888888888889,9: 0.1111111111111111,
10: 0.08333333333333333,11: 0.05555555555555555,
```
12: 0.027777777777777776}
```
Programming Tip
In the preceding code note that 36. is written with the trailing decimal mark.
This is a good habit to get into because division in Python 2.x is integer division
by default, which is not what we want here. This can be fixed with a top-level
from__future__ import division, but that’s easy to forget to do,
especially when you are passing code around and others may not reflexively
do the future import.
The above example exposes the elements of probability theory that are in play
for this simple problem while deliberately suppressing some of the gory technical
details. With this framework, we can ask other questions like what is the probability
that half the product of three dice will exceed the their sum? We can solve this using
the same method as in the following. First, let’s create the first mapping,
```
d={(i,j,k):((i*j*k)/2>i+j+k) for i in range(1,7)for j in range(1,7)
```
```
for k in range(1,7)}
```
40 2 Probability
The keys of this dictionary are the triples and the values are the logical values of
whether or not half the product of three dice exceeds their sum. Now, we do the
inverse mapping to collect the corresponding lists,
```
dinv = defaultdict(list)for i,j in d.iteritems(): dinv[j].append(i)
```
Note that dinv contains only two keys, True and False. Again, because the dice
are independent, the probability of any triple is 1/63 . Finally, we collect this for each
outcome as in the following,
```
X={i:len(j)/6.0**3 for i,j in dinv.iteritems() }print X
```
```
{False: 0.37037037037037035, True: 0.6296296296296297}
```
Thus, the probability of half the product of three dice exceeding their sum is
```
136/(6.0**3) = 0.63. The set that is induced by the random variable has
```
```
only two elements in it, True and False, with P(True) = 136/216 and P(False) =
```
1 − 136/216.
As a final example to exercise another layer of generality, let is consider the first
problem with the two dice where we want the probability of a seven, but this time
one of the dice is no longer fair. The distribution for the unfair die is the following:
```
P({1}) = P({2}) = P({3}) = 19
```
```
P({4}) = P({5}) = P({6}) = 29
```
From our earlier work, we know the elements corresponding to the sum of seven
are the following:
```
{(1, 6), (2, 5), (3, 4), (4, 3), (5, 2), (6, 1)}
```
Because we still have the independence assumption, all we need to change is the
probability computation of each of elements. For example, given that the first die is
the unfair one, we have
```
P((1, 6)) = P(1)P(6) = 19 × 16
```
```
and likewise for (2, 5) we have the following:
```
```
P((2, 5)) = P(2)P(5) = 19 × 16
```
and so forth. Summing all of these gives the following:
```
PX (7) = 19 × 16 + 19 × 16 + 19 × 16 + 29 × 16 + 29 × 16 + 29 × 16 = 16
```
2.1 Introduction 41
Let’s try computing this using Pandas instead of Python dictionaries. First, we
construct a DataFrame object with an index of tuples consisting of all pairs of
possible dice outcomes.
>>> from pandas import DataFrame
```
>>> d=DataFrame(index=[(i,j) for i in range(1,7) for j in range(1,7)],
```
```
... columns=[’sm’,’d1’,’d2’,’pd1’,’pd2’,’p’])
```
Now, we can populate the columns that we set up above where the outcome of the
first die is the d1 column and the outcome of the second die is d2,
>>> d.d1=[i[0] for i in d.index]
>>> d.d2=[i[1] for i in d.index]
Next, we compute the sum of the dices in the sm column,
```
>>> d.sm=map(sum,d.index)
```
With that established, the DataFrame now looks like the following:
```
>>> d.head(5) # show first five lines
```
sm d1 d2 pd1 pd2 p
```
(1, 1) 2 1 1 NaN NaN NaN
```
```
(1, 2) 3 1 2 NaN NaN NaN
```
```
(1, 3) 4 1 3 NaN NaN NaN
```
```
(1, 4) 5 1 4 NaN NaN NaN
```
```
(1, 5) 6 1 5 NaN NaN NaN
```
```
Next, we fill out the probabilities for each face of the unfair die (d1) and the fair die
```
```
(d2),
```
>>> d.loc[d.d1<=3,’pd1’]=1/9.
>>> d.loc[d.d1 > 3,’pd1’]=2/9.
>>> d.pd2=1/6.
```
>>> d.head(10)
```
sm d1 d2 pd1 pd2 p
```
(1, 1) 2 1 1 0.1111111 0.166667 NaN
```
```
(1, 2) 3 1 2 0.1111111 0.166667 NaN
```
```
(1, 3) 4 1 3 0.1111111 0.166667 NaN
```
```
(1, 4) 5 1 4 0.1111111 0.166667 NaN
```
```
(1, 5) 6 1 5 0.1111111 0.166667 NaN
```
```
(1, 6) 7 1 6 0.1111111 0.166667 NaN
```
```
(2, 1) 3 2 1 0.1111111 0.166667 NaN
```
```
(2, 2) 4 2 2 0.1111111 0.166667 NaN
```
```
(2, 3) 5 2 3 0.1111111 0.166667 NaN
```
```
(2, 4) 6 2 4 0.1111111 0.166667 NaN
```
Finally, we can compute the joint probabilities for the sum of the shown faces as the
```
following:
```
42 2 Probability
>>> d.p = d.pd1 * d.pd2
```
>>> d.head(5)
```
sm d1 d2 pd1 pd2 p
```
(1, 1) 2 1 1 0.1111111 0.166667 0.01851852
```
```
(1, 2) 3 1 2 0.1111111 0.166667 0.01851852
```
```
(1, 3) 4 1 3 0.1111111 0.166667 0.01851852
```
```
(1, 4) 5 1 4 0.1111111 0.166667 0.01851852
```
```
(1, 5) 6 1 5 0.1111111 0.166667 0.01851852
```
With all that established, we can compute the density of all the dice outcomes by
using groupby as in the following,
```
>>> d.groupby(’sm’)[’p’].sum()
```
sm
2 0.018519
3 0.037037
4 0.055556
5 0.092593
6 0.129630
7 0.166667
8 0.148148
9 0.129630
10 0.111111
11 0.074074
12 0.037037
```
Name: p, dtype: float64
```
These examples have shown how the theory of probability breaks down sets and
measurements of those sets and how these can be combined to develop the probability
mass functions for new random variables.
2.1.3 Continuous Random Variables
The same ideas work with continuous variables but managing the sets becomes
trickier because the real line, unlike discrete sets, has many limiting properties already
built into it that have to be handled carefully. Nonetheless, let’s start with an example
that should illustrate the analogous ideas. Suppose a random variable X is uniformly
distributed on the unit interval. What is the probability that the variable takes on
values less than 1/2?
In order to build intuition onto the discrete case, let’s go back to our dice-throwing
experiment with the fair dice. The sum of the values of the dice is a measurable
function,
```
Y : {1, 2, . . . , 6}2  → {2, 3, . . . , 12}
```
That is, Y is a mapping of the cartesian product of sets to a discrete set of out-
comes. In order to compute probabilities of the set of outcomes, we need to derive
the probability measure for Y, PY, from the corresponding probability measures for
2.1 Introduction 43
each die. Our previous discussion went through the mechanics of that. This means
that
```
PY : {2, 3, . . . , 12}  → [0, 1]
```
Note there is a separation between the function definition and where the target items
of the function are measured in probability. More bluntly,
```
Y : A  → B
```
with,
```
PY : B  → [0, 1]
```
Thus, to compute PY , which is derived from other random variables, we have to
express the equivalence classes in B in terms of their progenitor A sets.
The situation for continuous variables follows the same pattern, but with many
more deep technicalities that we are going to skip. For the continuous case, the
random variable is now,
```
X : R  → R
```
with corresponding probability measure,
```
PX : R  → [0, 1]
```
But where are the corresponding sets here? Technically, these are the Borel sets,
but we can just think of them as intervals. Returning to our question, what is the
probability that a uniformly distributed random variable on the unit interval takes
values less than 1/2? Rephrasing this question according to the framework, we have
the following:
```
X : [0, 1]  → [0, 1]
```
with corresponding,
```
PX : [0, 1]  → [0, 1]
```
To answer the question, by the definition of the uniform random variable on the unit
interval, we compute the following integral,
```
PX ([0, 1/2]) = PX (0 < X < 1/2) =
```
∫ 1/2
0
```
dx = 1/2
```
where the above integral’s dx sweeps through intervals of the B-type. The measure of
```
any dx interval (i.e., A-type set) is equal to dx, by definition of the uniform random
```
variable. To get all the moving parts into one notationally rich integral, we can also
write this as,
```
PX (0 < X < 1/2) =
```
∫ 1/2
0
```
dPX (dx) = 1/2
```
44 2 Probability
Now, let’s consider a slightly more complicated and interesting example. As
before, suppose we have a uniform random variable, X and let us introduce another
random variable defined,
```
Y = 2X
```
Now, what is the probability that 0 < Y < 12 ? To express this in our framework, we
write,
```
Y : [0, 1]  → [0, 2]
```
with corresponding,
```
PY : [0, 2]  → [0, 1]
```
To answer the question, we need to measure the set [0,1/2], with the probability
```
measure for Y , PY ([0, 1/2]). How can we do this? Because Y is derived from the X
```
random variable, as with the fair-dice throwing experiment, we have to create a set
```
of equivalences in the target space (i.e., B-type sets) that reflect back on the input
```
```
space (i.e., A-type sets). That is, what is the interval [0,1/2] equivalent to in terms
```
of the X random variable? Because, functionally, Y = 2X, then the B-type interval
[0,1/2] corresponds to the A-type interval [0,1/4]. From the probability measure of
X, we compute this with the integral,
```
PY ([0, 1/2]) = PX ([0, 1/4]) =
```
∫ 1/4
0
```
dx = 1/4
```
Now, let’s up the ante and consider the following random variable,
```
Y = X2
```
where now X is still uniformly distributed, but now over the interval [−1/2, 1/2].
We can express this in our framework as,
```
Y : [−1/2, 1/2]  → [0, 1/4]
```
with corresponding,
```
PY : [0, 1/4]  → [0, 1]
```
```
What is the PY (Y < 1/8)? In other words, what is the measure of the set BY =
```
[0, 1/8]? As before, because X is derived from our uniformly distributed random
variable, we have to reflect the BY set onto sets of the A-type. The thing to recognize
is that because X2 is symmetric about zero, all BY sets reflect back into two sets.
This means that for any set BY , we have the correspondence BY = A+X ∪ A−X . So, we
have,
```
BY =
```
```
{
```
0 < Y < 18
```
}
```
=
```
{
```
0 < X < 1√
8
```
} ⋃ {
```
− 1√
8
< X < 0
```
}
```
2.1 Introduction 45
From this perspective, we have the following solution,
```
PY (BY ) = P(A+X )/2 + P(A−X )/2
```
where the 12 comes from normalizing the PY to one. Also,
A+X =
```
{
```
0 < X < 1√
8
```
}
```
A−X =
```
{
```
− 1√
8
< X < 0
```
}
```
Therefore,
```
PY (BY ) = 1
```
2
√
8
- 1
2
√
8
```
because P(A+X ) = P(A−X ) = 1/
```
√
8. Let’s see if this comes out using the usual
transformation of variables method from calculus. Using this method, the density
```
f Y (y) = f X (√y)/(2√y) = 12√y . Then, we obtain,
```
∫ 18
0
1
2√y dy =
1√
8
which is what we got using the sets method. Note that you would favor the calculus
method in practice, but it is important to understand the deeper mechanics, because
sometimes the usual calculus method fails, as the next problem shows.
2.1.4 Transformation of Variables Beyond Calculus
Suppose X and Y are uniformly distributed in the unit interval and we define Z as
```
Z = XY − X
```
```
What is the f Z (z)? If you try this using the usual calculus method, you will fail (try
```
```
it!). The problem is one of the technical prerequisites for the calculus method is not
```
in force.
The key observation is that Z /∈ [−1, 0]. If this were possible, the X and Y
would have different signs, which cannot happen, given that X and Y are uniformly
distributed over [0, 1]. Now, let’s consider when Z > 0. In this case, Y > X because
Z cannot be positive otherwise. For the density function, we are interested in the set
```
{0 < Z < z}. We want to compute
```
46 2 Probability
```
P(Z < z) =
```
∫ ∫
B1d XdY
with,
```
B1 = {0 < Z < z}
```
Now, we have to translate that interval into an interval relevant to X and Y . For
```
0 < Z , we have Y > X. For Z < z, we have Y > X (1/z + 1). Putting this together
```
gives
```
A1 = {max(X, X (1/z + 1)) < Y < 1}
```
Integrating this over Y as follows,
∫ 1
0
```
{max(X, X (1/z + 1)) < Y < 1}dY = z − X − X zz where z > X1 − X
```
and integrating this one more time over X gives
∫ z1+z
0
−X + z − X z
z d X =
z
```
2(z + 1) where z > 0
```
Note that this is the computation for the probability itself, not the probability density
function. To get that, all we have to do is differentiate the last expression to obtain
```
f Z (z) = 1(z + 1)2 where z > 0
```
Now we need to compute this density using the same process for when z < −1.
We want the interval Z < z for when z < −1. For a fixed z, this is equivalent to
```
X (1 + 1/z) < Y . Because z is negative, this also means that Y < X. Under these
```
terms, we have the following integral,
∫ 1
0
```
{X (1/z + 1) < Y < X}dY = − Xz where z < −1
```
and integrating this one more time over X gives the following
− 12z where z < −1
To get the density for z < −1, we differentiate this with respect to z to obtain the
following,
```
f Z (z) = 12z2 where z < −1
```
2.1 Introduction 47
Putting this all together, we obtain,
```
f Z (z) =
```
⎧
⎪⎨
⎪⎩
```
1(z+1)2 if z > 0
```
12z2 if z < −1
0 otherwise
We will leave it as an exercise to show that this integrates out to one.
2.1.5 Independent Random Variables
Independence is a standard assumption. Mathematically, the necessary and sufficient
condition for independence between two random variables X and Y is the following:
```
P(X, Y ) = P(X)P(Y )
```
Two random variables X and Y are uncorrelated if,
```
E(X − X )E(Y − Y ) = 0
```
```
where X = E(X) Note that uncorrelated random variables are sometimes called
```
orthogonal random variables. Uncorrelatedness is a weaker property than indepen-
dence, however. For example, consider the discrete random variables X and Y uni-
```
formly distributed over the set {1, 2, 3} where
```
```
X =
```
⎧
⎪⎨
⎪⎩
1 if ω = 1
0 if ω = 2
−1 if ω = 3
and also,
```
Y =
```
⎧
⎪⎨
⎪⎩
0 if ω = 1
1 if ω = 2
0 if ω = 3
```
Thus, E(X) = 0 and E(X Y ) = 0, so X and Y are uncorrelated. However, we have
```
```
P(X = 1, Y = 1) = 0  = P(X = 1)P(Y = 1) = 19
```
48 2 Probability
So, these two random variables are not independent. Thus, uncorrelatedness does not
imply independence, generally, but there is the important case of Gaussian random
variables for which it does. To see this, consider the probability density function for
two zero-mean, unit-variance Gaussian random variables X and Y ,
```
f X,Y (x, y) = e
```
x2 −2ρx y+y22
```
(ρ2 −1)
```
2π
√
1 − ρ2
```
where ρ := E(X Y ) is the correlation coefficient. In the uncorrelated case where
```
ρ = 0, the probability density function factors into the following,
```
f X,Y (x, y) = e
```
```
− 12 (x2 +y2 )
```
2π =
e− x
22
√
2π
e− y
22
√
2π
```
= f X (x) f Y (y)
```
which means that X and Y are independent.
Independence and conditional independence are closely related, as in the
```
following:
```
```
P(X, Y |Z ) = P(X|Z )P(Y |Z )
```
which says that X and Y and independent conditioned on Z . Conditioning inde-
pendent random variables can break their independence. For example, consider two
```
independent Bernoulli-distributed random variables, X1, X2 ∈ {0, 1}. We define
```
```
Z = X1 + X2 . Note that Z ∈ {0, 1, 2}. In the case where Z = 1, we have,
```
```
P(X1|Z = 1) > 0
```
```
P(X2|Z = 1) > 0
```
Even though X1, X2 are independent, after conditioning on Z , we have the following,
```
P(X1 = 1, X2 = 1|Z = 1) = 0  = P(X1 = 1|Z = 1)P(X2 = 1|Z = 1)
```
Thus, conditioning on Z breaks the independence of X1, X2 . This also works in the
opposite direction — conditioning can make dependent random variables indepen-
dent. Define Z n = ∑ni X i with X i independent, integer-valued random variables.
The Z n variables are dependent because they stack the same telescoping set of X i
variables. Consider the following,
```
P(Z1 = i, Z3 = j|Z2 = k) = P(Z1 = i, Z2 = k, Z3 = j)P(Z
```
```
2 = k)
```
```
(2.1.5.1)
```
```
= P(X1 = i)P(X2 = k − i)P(X3 = j − k)P(Z
```
```
2 = k)
```
```
(2.1.5.2)
```
2.1 Introduction 49
where the factorization comes from the independence of the X i variables. Using the
definition of conditional probability,
```
P(Z1 = i|Z2) = P(Z1 = i, Z2 = k)P(Z
```
```
2 = k)
```
We can continue to expand Eq. 2.1.5,
```
P(Z1 = i, Z3 = j|Z2 = k) = P(Z1 = i|Z2) P(X3 = j − k)P(Z2 = k)P(Z
```
```
2 = k)
```
```
= P(Z1 = i|Z2)P(Z3 = j|Z2)
```
```
where P(X3 = j − k)P(Z2 = k) = P(Z3 = j, Z2). Thus, we see that depen-
```
dence between random variables can be broken by conditioning to create condition-
ally independent random variables. As we have just witnessed, understanding how
conditioning influences independence is important and is the main topic of study
in Probabilistic Graphical Models, a field with many algorithms and concepts to
extract these notions of conditional independence from graph-based representations
of random variables.
2.1.6 Classic Broken Rod Example
Let’s do one last example to exercise fluency in our methods by considering the
following classic problem: given a rod of unit-length, broken independently and
randomly at two places, what is the probability that you can assemble the three
remaining pieces into a triangle? The first task is to find a representation of a triangle
as an easy-to-apply constraint. What we want is something like the following:
```
P( triangle exists ) =
```
∫ 1
0
∫ 1
0
```
{ triangle exists }d XdY
```
where X and Y are independent and uniformly distributed in the unit-interval. Heron’s
formula for the area of the triangle,
```
area =
```
√
```
(s − a)(s − b)(s − c)s
```
```
where s = (a + b + c)/2 is what we need. The idea is that this yields a valid area
```
only when each of the terms under the square root is greater than or equal to zero.
Thus, suppose that we have
```
a = X
```
```
b = Y − X
```
```
c = 1 − Y
```
50 2 Probability
assuming that Y > X. Thus, the criterion for a valid triangle boils down to
```
{(s > a) ∧ (s > b) ∧ (s > c) ∧ (X < Y )}
```
After a bit of manipulation, this consolidates into:
```
{ 1
```
2 < Y < 1
∧ 1
```
2 (2Y − 1) < X <
```
1
2
```
}
```
which we integrate out by d X first to obtain
```
P( triangle exists ) =
```
∫ 1
0
∫ 1
0
```
{ 1
```
2 < Y < 1
∧ 1
```
2 (2Y − 1) < X <
```
1
2
```
}
```
d XdY
```
P( triangle exists ) =
```
∫ 1
```
12(1 − Y )dY
```
and then by dY to obtain finally,
```
P( triangle exists ) = 18
```
when Y > X. By symmetry, we get the same result for X > Y . Thus, the final result
is the following:
```
P( triangle exists ) = 18 + 18 = 14
```
We can quickly check using this result using Python for the case Y > X using
the following code:
>>> import numpy as np
```
>>> x,y = np.random.rand(2,1000) # uniform rv
```
```
>>> a,b,c = x,(y-x),1-y # 3 sides
```
```
>>> s = (a+b+c)/2
```
```
>>> np.mean((s>a) & (s>b) & (s>c) & (y>x)) # approx 1/8=0.125
```
0.115
Programming Tip
The chained logical & symbols above tell Numpy that the logical operation
should be considered element-wise.
2.2 Projection Methods
The concept of projection is key to developing an intuition about conditional proba-
bility. We already have a natural intuition of projection from looking at the shadows
of objects on a sunny day. As we will see, this simple idea consolidates many abstract
2.2 Projection Methods 51
Fig. 2.2 Given the point y
```
(black square) we want to
```
find the x along the line that
is closest to it. The gray
circle is the locus of points
within a fixed distance
from y
ideas in optimization and mathematics. Consider Fig. 2.2 where we want to find a
```
point along the blue line (namely, x) that is closest to the black square (namely, y).
```
In other words, we want to inflate the gray circle until it just touches the black line.
Recall that the circle boundary is the set of points for which
√
```
(y − x)T (y − x) = ‖y − x‖ = 
```
for some value of . So we want a point x along the line that satisfies this for the
smallest . Then, that point will be the closest point on the black line to the black
square. It may be obvious from the diagram, but the closest point on the line occurs
where the line segment from the black square to the black line is perpedicular to the
line. At this point, the gray circle just touches the black line. This is illustrated below
in Fig. 2.3.
Programming Tip
Figure 2.2 uses the matplotlib.patches module. This module contains
primitive shapes like circles, ellipses, and rectangles that can be assembled into
complex graphics. As shown in the code in the IPython Notebook correspond-
ing to this chapter, after importing a particular shape, you can apply that shape
to an existing axis using the add_patch method. The patches themselves
can by styled using the usual formatting keywords like color and alpha.
52 2 Probability
Fig. 2.3 The closest point
on the line occurs when the
line is tangent to the circle.
When this happens, the black
```
line and the line (minimum
```
```
distance) are perpedicular
```
Now that we can see what’s going on, we can construct the solution analytically. We
can represent an arbitrary point along the black line as:
```
x = αv
```
where α ∈ R slides the point up and down the line with
```
v = [1, 1]T
```
Formally, v is the subspace onto which we want to project y. At the closest point,
```
the vector between y and x (the error vector above) is perpedicular to the line. This
```
means that
```
(y − x)T v = 0
```
and by substituting and working out the terms, we obtain
α = y
T v
‖v‖2
The error is the distance between αv and y. This is a right triangle, and we can use
the Pythagorean theorem to compute the squared length of this error as
```
2 = ‖(y − x)‖2 = ‖y‖2 − α2‖v‖2 = ‖y‖2 − ‖y
```
T v‖2
‖v‖2
2.2 Projection Methods 53
where ‖v‖2 = vT v. Note that since 2 ≥ 0, this also shows that
‖yT v‖ ≤ ‖y‖‖v‖
which is the famous and useful Cauchy-Schwarz inequality which we will exploit
later. Finally, we can assemble all of this into the projection operator
```
Pv = 1‖v‖2 vvT
```
With this operator, we can take any y and find the closest point on v by doing
Pv y = v
```
( vT y
```
‖v‖2
```
)
```
where we recognize the term in parenthesis as the α we computed earlier. It’s called
```
an operator because it takes a vector (y) and produces another vector (αv). Thus,
```
projection unifies geometry and optimization.
2.2.1 Weighted Distance
We can easily extend this projection operator to cases where the measure of distance
between y and the subspace v is weighted. We can accommodate these weighted
distances by re-writing the projection operator as
```
Pv = v v
```
T QT
```
vT Qv (2.2.1.1)
```
where Q is positive definite matrix. In the previous case, we started with a point
y and inflated a circle centered at y until it just touched the line defined by v and
this point was closest point on the line to y. The same thing happens in the general
case with a weighted distance except now we inflate an ellipse, not a circle, until the
ellipse touches the line.
```
Note that the error vector (y − αv) in Fig. 2.4 is still perpendicular to the line
```
```
(subspace v), but in the space of the weighted distance. The difference between the
```
```
first projection (with the uniform circular distance) and the general case (with the
```
```
elliptical weighted distance) is the inner product between the two cases. For example,
```
in the first case we have yT v and in the weighted case we have yT QT v. To move
from the uniform circular case to the weighted ellipsoidal case, all we had to do was
change all of the vector inner products. Before we finish, we need a formal property
of projections:
Pv Pv = Pv
54 2 Probability
Fig. 2.4 In the weighted
case, the closest point on the
line is tangent to the ellipse
and is still perpedicular in
the sense of the weighted
distance
known as the idempotent property which basically says that once we have projected
onto a subspace, subsequent projections leave us in the same subspace. You can
verify this by computing Eq. 2.2.1.
```
Thus, projection ties a minimization problem (closest point to a line) to an alge-
```
```
braic concept (inner product). It turns out that these same geometric ideas from linear
```
algebra [2] can be translated to the conditional expectation. How this works is the
subject of our next section.
2.3 Conditional Expectation as Projection
Now that we understand projection methods geometrically, we can apply them to
conditional probability. This is the key concept that ties probability to geometry,
optimization, and linear algebra.
Inner Product for Random Variables. From our previous work on projection for
vectors in Rn , we have a good geometric grasp on how projection is related to
```
Minimum Mean Squared Error (MMSE). By one abstract step, we can carry all of
```
our geometric interpretations to the space of random variables. For example, we
previously noted that at the point of projection, we had the following orthogonal
```
(i.e., perpendicular vectors) condition,
```
```
(y − vopt )T v = 0
```
which by noting the inner product slightly more abstractly as 〈x, y〉 = xT y, we can
express as
〈y − vopt , v〉 = 0
2.3 Conditional Expectation as Projection 55
and by defining the inner product for the random variables X and Y as
```
〈X, Y 〉 = E(X Y )
```
we have the same relationship:
```
〈X − h opt (Y ), Y 〉 = 0
```
which holds not for vectors in Rn , but for random variables X and Y and functions of
those random variables. Exactly why this is true is technical, but it turns out that one
can build up the entire theory of probability this way [3], by using the expectation as
an inner product.
Furthermore, by abstracting out the inner product concept, we have connected
```
minimum-mean-squared-error (MMSE) optimization problems, geometry, and ran-
```
dom variables. That’s a lot of mileage to get a out of an abstraction and it enables
us to shift between these interpretations to address real problems. Soon, we’ll do
this with some examples, but first we collect the most important result that flows
naturally from this abstraction.
Conditional Expectation as Projection. The conditional expectation is the mini-
```
mum mean squared error (MMSE) solution to the following problem 1 :
```
minh
∫
R
```
(x − h(y))2dx
```
```
with the minimizing h opt (Y ) as
```
```
h opt (Y ) = E(X|Y )
```
```
which is another way of saying that among all possible functions h(Y ), the one
```
```
that minimizes the MSE is E(X|Y ). From our previous discussion on projection, we
```
noted that these MMSE solutions can be thought of as projections onto a subspace
that characterizes Y . For example, we previously noted that at the point of projection,
we have perpendicular terms,
```
〈X − h opt (Y ), Y 〉 = 0 (2.3.0.2)
```
but since we know that the MMSE solution
```
h opt (Y ) = E(X|Y )
```
we have by direct substitution,
```
E(X − E(X|Y ), Y ) = 0 (2.3.0.3)
```
1 See appendix for proof using the Cauchy-Schwarz inequality.
56 2 Probability
That last step seems pretty innocuous, but it ties MMSE to conditional expectation to
the inner project abstraction, and in so doing, reveals the conditional expectation to be
a projection operator for random variables. Before we develop this further, let’s grab
some quick dividends. From the previous equation, by linearity of the expectation,
we obtain,
```
E(X Y ) = E(Y E(X|Y ))
```
which is the so-called tower property of the expectation. Note that we could have
found this by using the formal definition of conditional expectation,
```
E(X|Y ) =
```
∫
R2
```
x f X,Y (x, y)f
```
```
Y (y)
```
dxdy
and brute-force direct integration,
```
E(Y E(X|Y )) =
```
∫
R
y
∫
R
```
x f X,Y (x, y)f
```
```
Y (y)
```
```
f Y (y)dxdy
```
=
∫
R2
```
x y f X,Y (x, y)dxdy
```
```
= E(X Y )
```
which is not very geometrically intuitive. This lack of geometric intuition makes it
hard to apply these concepts and keep track of these relationships.
We can keep pursuing this analogy and obtain the length of the error term from
the orthogonality property of the MMSE solution as,
```
〈X − h opt (Y ), X − h opt (Y )〉 = 〈X, X〉 − 〈h opt (Y ), h opt (Y )〉
```
and then by substituting all the notation we obtain
```
E(X − E(X|Y ))2 = E(X)2 − E(E(X|Y ))2
```
which would be tough to compute by direct integration.
```
To formally establish that E(X|Y ) is in fact a projection operator we need to
```
show idempotency. Recall that idempotency means that once we project something
onto a subspace, further projections do nothing. In the space of random variables,
```
E(X|·) is the idempotent projection as we can show by noting that
```
```
h opt = E(X|Y )
```
is purely a function of Y , so that
```
E(h opt (Y )|Y ) = h opt (Y )
```
2.3 Conditional Expectation as Projection 57
because Y is fixed, this verifies idempotency. Thus, conditional expectation is the
corresponding projection operator for random variables. We can continue to carry
```
over our geometric interpretations of projections for vectors (v) into random vari-
```
```
ables (X). With this important result, let’s consider some examples of conditional
```
expectations obtained by using brute force to find the optimal MMSE function h opt
as well as by using our new perspective on conditional expectation.
Example Suppose we have a random variable, X, then what constant is closest to
```
X in the sense of the mean-squared-error (MSE)? In other words, which c ∈ R
```
minimizes the following mean squared error:
```
MSE = E(X − c)2
```
we can work this out many ways. First, using calculus-based optimization,
```
E(X − c)2 = E(c2 − 2cX + X2) = c2 − 2cE(X) + E(X2)
```
and then take the first derivative with respect to c and solve:
```
copt = E(X)
```
Remember that X may potentially take on many values, but this says that the closest
```
number to X in the MSE sense is E(X). This is intuitively pleasing. Coming at this
```
same problem using our inner product, from Eq. 2.3.0.3 we know that at the point of
projection
```
E((X − copt )1) = 0
```
where the 1 represents the space of constants we are projecting onto. By linearity of
the expectation, gives
```
copt = E(X)
```
```
Using the projection approach, because E(X|Y ) is the projection operator, with
```
```
Y = Ω (the entire underlying probability space), we have, using the definition of
```
conditional expectation:
```
E(X|Y = Ω) = E(X)
```
This is because of the subtle fact that a random variable over the entire Ω space can
```
only be a constant. Thus, we just worked the same problem three ways (optimization,
```
```
orthogonal inner products, projection).
```
Example Let’s consider the following example with probability density f X,Y = x +y
```
where (x, y) ∈ [0, 1]2 and compute the conditional expectation straight from the
```
```
definition:
```
```
E(X|Y ) =
```
∫ 1
0
```
x f X,Y (x, y)f
```
```
Y (y)
```
```
dx =
```
∫ 1
0
x x + yy + 1/2 dx = 3y + 26y + 3
58 2 Probability
That was pretty easy because the density function was so simple. Now, let’s do it the
```
hard way by going directly for the MMSE solution h(Y ). Then,
```
```
MSE = minh
```
∫ 1
0
∫ 1
0
```
(x − h(y))2 f X,Y (x, y)dxdy
```
= minh
∫ 1
0
```
yh2(y) − yh(y) + 13 y + 12 h2(y) − 23 h(y) + 14 dy
```
Now we have to find a function h that is going to minimize this. Solving for a function,
as opposed to solving for a number, is generally very, very hard, but because we
are integrating over a finite interval, we can use the Euler-Lagrange method from
variational calculus to take the derivative of the integrand with respect to the function
```
h(y) and set it to zero. Using Euler-Lagrange methods, we obtain the following result,
```
```
2yh(y) − y + h(y) − 23 = 0
```
Solving this gives
```
h opt (y) = 3y + 26y + 3
```
which is what we obtained before. Finally, we can solve this using our inner product
in Eq. 2.3.0.2 as
```
E((X − h(Y ))Y ) = 0
```
Writing this out gives,
∫ 1
0
∫ 1
0
```
(x − h(y))y(x + y)dxdy =
```
∫ 1
0
1
```
6 y(−3(2y + 1)h(y) + 3y + 2)dy = 0
```
and the integrand must be zero,
```
2y + 3y2 − 3yh(y) − 6y2h(y) = 0
```
```
and solving this for h(y) gives the same solution:
```
```
h opt (y) = 3y + 26y + 3
```
Thus, doing it by the brute force integration from the definition, optimization, or
```
inner product gives us the same answer; but, in general, no method is necessarily
```
easiest because they both involve potentially difficult or impossible integration, opti-
mization, or functional equation solving. The point is that now that we have a deep
toolbox, we can pick and choose which tools we want to apply for different problems.
2.3 Conditional Expectation as Projection 59
Before we leave this example, let’s use Sympy to verify the length of the error
```
function we found earlier for this example:
```
```
E(X − E(X|Y ))2 = E(X)2 − E(E(X|Y ))2
```
that is based on the Pythagorean theorem. First, we need to compute the marginal
densities,
>>> from sympy.abc import y,x
>>> from sympy import integrate, simplify
>>> fxy = x + y # joint density
```
>>> fy = integrate(fxy,(x,0,1)) # marginal density
```
```
>>> fx = integrate(fxy,(y,0,1)) # marginal density
```
Then, we need to write out the conditional expectation,
```
>>> EXY = (3*y+2)/(6*y+3) # conditional expectation
```
```
Next, we can compute the left side, E(X − E(X|Y ))2 , as the following,
```
>>> # from the definition
```
>>> LHS=integrate((x-EXY)**2*fxy,(x,0,1),(y,0,1))
```
>>> LHS # left-hand-side
```
-log(216)/144 + log(72)/144 + 1/12
```
```
We can similarly compute the right side, E(X)2 − E(E(X|Y ))2 , as the following,
```
>>> # using Pythagorean theorem
```
>>> RHS=integrate((x)**2*fx,(x,0,1))-integrate((EXY)**2*fy,(y,0,1))
```
>>> RHS # right-hand-side
```
-log(216)/144 + log(72)/144 + 1/12
```
Finally, we can verify that the left and right sides match,
```
>>> print simplify(LHS-RHS)==0
```
True
In this section, we have pulled together all the projection and least-squares opti-
mization ideas from the previous sections to connect geometric notions of projection
from vectors in Rn to random variables. This resulted in the remarkable realization
that the conditional expectation is in fact a projection operator for random variables.
Knowing this allows to approach difficult problems in multiple ways, depending on
which way is more intuitive or tractable in a particular situation. Indeed, finding the
right problem to solve is the hardest part, so having many ways of looking at the
same concepts is crucial.
For much more detailed development, the book by Mikosch [4] has some excel-
lent sections covering much of this material with a similar geometric interpretation.
Kobayashi [5] does too. Nelson [3] also has a similar presentation based on hyper-real
numbers.
60 2 Probability
2.3.1 Appendix
We want to prove that we the conditional expectation is the minimum mean squared
error minimizer of the following:
```
J = minh
```
∫
R2
```
|X − h(Y )|2 f X,Y (x, y)dxdy
```
We can expand this as follows,
```
J = minh
```
∫
R2
```
|X|2 f X,Y (x, y)dxdy +
```
∫
R2
```
|h(Y )|2 f X,Y (x, y)dxdy
```
−
∫
R2
```
2X h(Y ) f X,Y (x, y)dxdy
```
To minimize this, we have to maximize the following:
```
A = maxh
```
∫
R2
```
X h(Y ) f X,Y (x, y)dxdy
```
Breaking up the integral using the definition of conditional expectation
```
A = maxh
```
∫
R
```
(∫
```
R
```
X f X|Y (x|y)dx
```
```
)
```
```
h(Y ) f Y (y)dy (2.3.1.1)
```
= maxh
∫
R
```
E(X|Y )h(Y ) f Y (Y )dy (2.3.1.2)
```
From properties of the Cauchy-Schwarz inequality, we know that the maximum
```
happens when h opt (Y ) = E(X|Y ), so we have found the optimal h(Y ) function as:
```
```
h opt (Y ) = E(X|Y )
```
which shows that the optimal function is the conditional expectation.
2.4 Conditional Expectation and Mean Squared Error
In this section, we work through a detailed example using conditional expectation
```
and optimization methods. Suppose we have two fair six-sided die (X and Y ) and we
```
want to measure the sum of the two variables as Z = X + Y . Further, let’s suppose
that given Z , we want the best estimate of X in the mean-squared-sense. Thus, we
want to minimize the following:
```
J (α) =
```
∑
```
(x − αz)2P(x, z)
```
2.4 Conditional Expectation and Mean Squared Error 61
where P is the probability mass function for this problem. The idea is that when
we have solved this problem, we will have a function of Z that is going to be the
minimum MSE estimate of X. We can substitute in for Z in J and get:
```
J (α) =
```
∑
```
(x − α(x + y))2P(x, y)
```
Let’s work out the steps in Sympy in the following:
>>> import sympy as S
>>> from sympy.stats import density, E, Die
```
>>> x=Die(’D1’,6) # 1st six sided die
```
```
>>> y=Die(’D2’,6) # 2nd six sides die
```
```
>>> a=S.symbols(’a’)
```
>>> z = x+y # sum of 1st and 2nd die
```
>>> J = E((x-a*(x+y))**2) # expectation
```
```
>>> print S.simplify(J)
```
329*a**2/6 - 329*a/6 + 91/6
With all that setup we can now use basic calculus to minimize the objective function J ,
```
>>> sol,=S.solve(S.diff(J,a),a) # using calculus to minimize
```
>>> print sol # solution is 1/2
1/2
Programming Tip
Sympy has a stats module that can do some basic work with expressions
involving probability densities and expectations. The above code uses its E
```
function to compute the expectation.
```
This says that z/2 is the MSE estimate of X given Z which means geometrically
```
(interpreting the MSE as a squared distance weighted by the probability mass func-
```
```
tion) that z/2 is as close to x as we are going to get for a given z.
```
```
Let’s look at the same problem using the conditional expectation operator E(·|z)
```
and apply it to our definition of Z . Then
```
E(z|z) = E(x + y|z) = E(x|z) + E(y|z) = z
```
using the linearity of the expectation. Now, since by the symmetry of the problem
```
(i.e., two identical die), we have
```
```
E(x|z) = E(y|z)
```
we can plug this in and solve
```
2E(x|z) = z
```
62 2 Probability
Fig. 2.5 The values of Z are
in yellow with the
corresponding values for X
and Y on the axes. The gray
scale colors indicate the
underlying joint probability
density
which once again gives,
```
E(x|z) = z2
```
which is equal to the estimate we just found by minimizing the MSE. Let’s explore
this further with Fig. 2.5. Figure 2.5 shows the values of Z in yellow with the corre-
sponding values for X and Y on the axes. Suppose z = 2, then the closest X to this
```
is X = 1, which is what E(x|z) = z/2 = 1 gives. What happens when Z = 7? In
```
this case, this value is spread out diagonally along the X axis so if X = 1, then Z is
6 units away, if X = 2, then Z is 5 units away and so on.
Now, back to the original question, if we had Z = 7 and we wanted to get as close
as we could to this using X, then why not choose X = 6 which is only one unit away
from Z ? The problem with doing that is X = 6 only occurs 1/6 of the time, so we
are not likely to get it right the other 5/6 of the time. So, 1/6 of the time we are one
unit away but 5/6 of the time we are much more than one unit away. This means that
the MSE score is going to be worse. Since each value of X from 1 to 6 is equally
likely, to play it safe, we choose 7/2 as the estimate, which is what the conditional
expectation suggests.
We can check this claim with samples using Sympy below:
>>> import numpy as np
>>> from sympy import stats
>>> # Eq constrains Z
```
>>> samples_z7 = lambda : stats.sample(x, S.Eq(z,7))
```
>>> #using 6 as an estimate
```
>>> mn= np.mean([(6-samples_z7())**2 for i in range(100)])
```
>>> #7/2 is the MSE estimate
```
>>> mn0= np.mean([(7/2.-samples_z7())**2 for i in range(100)])
```
```
>>> print ’MSE=%3.2f using 6 vs MSE=%3.2f using 7/2 ’ % (mn,mn0)
```
```
MSE=10.85 using 6 vs MSE=2.29 using 7/2
```
2.4 Conditional Expectation and Mean Squared Error 63
Programming Tip
```
The stats.sample(x, S.Eq(z,7)) function call samples the x vari-
```
able subject to a condition on the z variable. In other words, it generates
random samples of x die, given that the sum of the outcomes of that die and
the y die add up to z==7.
Please run the above code repeatedly in the Jupyter/IPython Notebook corresponding
```
to this section until you have convinced yourself that the E(x|z) gives the lower MSE
```
every time. To push this reasoning, let’s consider the case where the die is so biased
so that the outcome of 6 is ten times more probable than any of the other outcomes.
That is,
```
P(6) = 2/3
```
```
whereas P(1) = P(2) = . . . = P(5) = 1/15. We can explore this using Sympy as
```
in the following:
>>> # here 6 is ten times more probable than any other outcome
```
>>> x=stats.FiniteRV(’D3’,{1:1/15., 2:1/15.,
```
... 3:1/15., 4:1/15.,
```
... 5:1/15., 6:2/3.})
```
As before, we construct the sum of the two dice, and plot the corresponding proba-
bility mass function in Fig. 2.6. As compared with Fig. 2.5, the probability mass has
been shifted away from the smaller numbers.
Fig. 2.6 The values of Z are
in yellow with the
corresponding values for X
and Y on the axes
64 2 Probability
Let’s see what the conditional expectation says about how we can estimate X from
Z .
```
>>> E(x, S.Eq(z,7)) # conditional expectation E(x|z=7)
```
5.00000000000000
```
Now that we have E(x|z = 7) = 5, we can generate samples as before and see if
```
this gives the minimum MSE.
```
>>> samples_z7 = lambda : stats.sample(x, S.Eq(z,7))
```
>>> #using 6 as an estimate
```
>>> mn= np.mean([(6-samples_z7())**2 for i in range(100)])
```
>>> #5 is the MSE estimate
```
>>> mn0= np.mean([(5-samples_z7())**2 for i in range(100)])
```
```
>>> print ’MSE=%3.2f using 6 vs MSE=%3.2f using 5 ’ % (mn,mn0)
```
```
MSE=2.69 using 6 vs MSE=2.33 using 5
```
Using a simple example, we have emphasized the connection between minimum
mean squared error problems and conditional expectation. Hopefully, the last two fig-
ures helped expose the role of the probability density. Next, we’ll continue revealing
the true power of the conditional expectation as we continue to develop corresponding
geometric intuition.
2.5 Worked Examples of Conditional Expectation
and Mean Square Error Optimization
Brzezniak [6] is a great book because it approaches conditional expectation through
a sequence of exercises, which is what we are trying to do here. The main differ-
ence is that Brzezniak takes a more abstract measure-theoretic approach to the same
problems. Note that you do need to grasp measure theory for advanced areas in
probability, but for what we have covered so far, working the same problems in his
text using our methods is illuminating. It always helps to have more than one way
to solve any problem. I urge you to get a copy of his book or at least look at some
pages on Google Books. I have numbered the examples corresponding to the book
and tried to follow its notation.
2.5.1 Example
This is Example 2.1 from Brzezniak. Three coins, 10p, 20p and 50p are tossed. The
values of the coins that land heads up are totaled. What is the expected total given
```
that two coins have landed heads-up. In this case we have we want to compute E(ξ |η)
```
where
ξ := 10X10 + 20X20 + 50X50
2.5 Worked Examples of Conditional Expectation and Mean Square Error Optimization 65
```
where X i ∈ {0, 1} and where X10 is the Bernoulli-distributed random variable cor-
```
```
responding to the 10p coin (and so on). Thus, ξ represents the total value of the
```
heads-up coins. The η represents the condition that only two of the three coins are
heads-up,
```
η := X10 X20(1 − X50) + (1 − X10)X20 X50 + X10(1 − X20)X50
```
and is a function that is non-zero only when two of the three coins lands heads-up.
Each triple term catches each of these three possibilities. For example, the first term
equals one when the 10p and 20p are heads up and the 50p is heads down. The
remaining terms are zero.
To compute the conditional expectation, we want to find a function h of η that
```
minimizes the mean-squared-error (MSE),
```
```
MSE =
```
∑
```
X∈{0,1}3
```
1
```
2 3 (ξ − h(η))
```
2
```
where the sum is taken over all possible triples of outcomes for {X10, X20, X50}
```
because each of the three coins has a 12 chance of coming up heads.
```
Now, the question boils down to how can we characterize the function h(η)? Note
```
```
that η  → {0, 1} so h takes on only two values. So, the orthogonal inner product
```
condition is the following:
```
〈ξ − h(η), η〉 = 0
```
But, because are only interested in η = 1, this simplifies to
```
〈ξ − h(1), 1〉 = 0
```
```
〈ξ, 1〉 = 〈h(1), 1〉
```
This doesn’t look so hard to evaluate but we have to compute the integral over the
```
set where η = 1. In other words, we need the set of triples {X10, X20, X50} where
```
η = 1. That is, we can compute
∫
```
{η=1}
```
```
ξ d X = h(1)
```
∫
```
{η=1}
```
d X
```
which is what Brzezniak does. Instead, we can define h(η) = αη and then find α.
```
Re-writing the orthogonal condition gives
〈ξ − η, αη〉 = 0
〈ξ, η〉 = α〈η, η〉
α = 〈ξ, η〉〈η, η〉
66 2 Probability
where
〈ξ, η〉 =
∑
```
X∈{0,1}3
```
1
```
2 3 (ξ η)
```
```
Note that we can just sweep over all triples {X10, X20, X50} because the definition
```
```
of h(η) zeros out when η = 0 anyway. All we have to do is plug everything in and
```
solve. This tedious job is perfect for Sympy.
>>> import sympy as S
```
>>> X10,X20,X50 = S.symbols(’X10,X20,X50’,real=True)
```
>>> xi = 10*X10+20*X20+50*X50
```
>>> eta = X10*X20*(1-X50)+X10*(1-X20)*(X50)+(1-X10)*X20*(X50)
```
```
>>> num=S.summation(xi*eta,(X10,0,1),(X20,0,1),(X50,0,1))
```
```
>>> den=S.summation(eta*eta,(X10,0,1),(X20,0,1),(X50,0,1))
```
>>> alpha=num/den
>>> print alpha # alpha=160/3
160/3
This means that
```
E(ξ |η) = 1603 η
```
which we can check with a quick simulation
```
>>> import pandas as pd>>> d = pd.DataFrame(columns=[’X10’,’X20’,’X50’])
```
```
>>> d.X10 = np.random.randint(0,2,1000)>>> d.X10 = np.random.randint(0,2,1000)
```
```
>>> d.X20 = np.random.randint(0,2,1000)>>> d.X50 = np.random.randint(0,2,1000)
```
Programming Tip
The code above creates an empty Pandas data frame with the named columns.
The next four lines assigns values to each of the columns.
The code above simulates flipping the three coins 1000 times. Each column of the
dataframe is either 0 or 1 corresponding to heads-down or heads-up, respectively.
The condition is that two of the three coins have landed heads-up. Next, we can group
```
the columns according to their sums. Note that the sum can only be in {0, 1, 2, 3}
```
corresponding to 0 heads-up, 1 heads-up, and so on.
```
>>> grp=d.groupby(d.eval(’X10+X20+X50’))
```
2.5 Worked Examples of Conditional Expectation and Mean Square Error Optimization 67
Programming Tip
The eval function of the Pandas data frame takes the named columns and
evaluates the given formula. At the time of this writing, only simple formulas
involving primitive operations are possible.
Next, we can get the 2 group, which corresponds to exactly two coins having landed
heads-up, and then evaluate the sum of the values of the coins. Finally, we can take
the mean of these sums.
```
>>> grp.get_group(2).eval(’10*X10+20*X20+50*X50’).mean()52.719999999999999
```
The result is close to 160/3=53.33 which supports the analytic result. The
following code shows that we can accomplish the same simulation using pure Numpy.
>>> import numpy as np>>> from numpy import array
```
>>> x=np.random.randint(0,2,(3,1000))>>> print np.dot(x[:,x.sum(axis=0)==2].T,array([10,20,50])).mean()
```
52.698998418555611
In this case, we used the Numpy dot product to compute the value of the heads-
```
up coins. The sum(axis=0)==2 part selects the columns that correspond to two
```
heads-up coins.
Still another way to get at the same problem is to forego the random sampling
part and just consider all possibilities exhaustively using the itertools module
in Python’s standard library.
```
>>> import itertools as it>>> list(it.product((0,1),(0,1),(0,1)))
```
```
[(0, 0, 0),(0, 0, 1),
```
```
(0, 1, 0),(0, 1, 1),
```
```
(1, 0, 0),(1, 0, 1),
```
```
(1, 1, 0),(1, 1, 1)]
```
Note that we need to call list above in order to trigger the iteration in it.
product. This is because the itertools module is generator-based so does
```
not actually do the iteration until it is iterated over (by list in this case). This
```
```
shows all possible triples (X10, X20, X50) where 0 and 1 indicate heads-down and
```
heads-up, respectively. The next step is to filter out the cases that correspond to two
heads-up coins.
```
>>> list(it.ifilter(lambda i:sum(i)==2,it.product((0,1),(0,1),(0,1)))))[(0, 1, 1), (1, 0, 1), (1, 1, 0)]
```
Next, we need to compute the sum of the coins and combine the prior code.
68 2 Probability
```
>>> map(lambda k:10*k[0]+20*k[1]+50*k[2],... it.ifilter(lambda i:sum(i)==2,
```
```
... it.product((0,1),(0,1),(0,1))))[70, 60, 30]
```
The mean of the output is 53.33, which is yet another way to get the same result.
For this example, we demonstrated the full spectrum of approaches made possible
using Sympy, Numpy, and Pandas. It is always valuable to have multiple ways of
approaching the same problem and cross-checking the result.
2.5.2 Example
This is Example 2.2 from Brzezniak. Three coins, 10p, 20p and 50p are tossed as
before. What is the conditional expectation of the total amount shown by the three
coins given the total amount shown by the 10p and 20p coins only? For this problem,
ξ :=10X10 + 20X20 + 50X50
```
η :=30X10 X20 + 20(1 − X10)X20 + 10X10(1 − X20)
```
```
which takes on four values η  → {0, 10, 20, 30} and only considers the 10p and 20p
```
```
coins. In contrast to the last problem, here we are interested in h(η) for all of the
```
```
values of η. Naturally, there are only four values for h(η) corresponding to each of
```
these four values. Let’s first consider η = 10. The orthogonal condition is then
```
〈ξ − h(10), 10〉 = 0
```
```
The domain for η = 10 is {X10 = 1, X20 = 0, X50} which we can integrate out of
```
the expectation below,
```
E{X10 =1,X20 =0,X50 }(ξ − h(10))10 = 0
```
```
E{X50 }(10 − h(10) + 50X50) = 0
```
```
10 − h(10) + 25 = 0
```
```
which gives h(10) = 35. Repeating the same process for η ∈ {20, 30} gives h(20) =
```
```
45 and h(30) = 55, respectively. This is the approach Brzezniak takes. On the other
```
```
hand, we can just look at affine functions, h(η) = aη+b and use brute-force calculus.
```
>>> from sympy.abc import a,b>>> h = a*eta + b
```
>>> eta = X10*X20*30 + X10*(1-X20)*(10)+ (1-X10)*X20*(20)>>> MSE=S.summation((xi-h)**2*S.Rational(1,8),(X10,0,1),
```
```
... (X20,0,1),... (X50,0,1))
```
```
>>> sol=S.solve([S.diff(MSE,a),S.diff(MSE,b)],(a,b))>>> print sol
```
```
{b: 25, a: 1}
```
2.5 Worked Examples of Conditional Expectation and Mean Square Error Optimization 69
Programming Tip
The Rational function from Sympy code expresses a rational number that
Sympy is able to manipulate as such. This is different that specifying a fraction
like 1/8., which Python would automatically compute as a floating point
```
number (i.e., 0.125). The advantage of using Rational is that Sympy can
```
later produce rational numbers as output, which are sometimes easier to make
sense of.
This means that
```
E(ξ |η) = 25 + η (2.5.2.1)
```
```
since η takes on only four values, {0, 10, 20, 30}, we can write this out explicitly as
```
```
E(ξ |η) =
```
⎧
⎪⎪⎪
⎨
⎪⎪⎪
⎩
25 for η = 0
35 for η = 10
45 for η = 20
55 for η = 30
```
(2.5.2.2)
```
Alternatively, we can use orthogonal inner products to write out the following con-
```
ditions:
```
```
〈ξ − h(η), η〉 = 0 (2.5.2.3)
```
```
〈ξ − h(η), 1〉 = 0 (2.5.2.4)
```
Writing these out and solving for a and b is tedious and a perfect job for Sympy.
Starting with Eq. 2.5.2.3,
```
>>> expr = expr=S.expand((xi-h)*eta)>>> print expr
```
-100*X10**2*a + 100*X10**2 - 400*X10*X20*a + 400*X10*X20 + 500*X10*X50- 10*X10*b - 400*X20**2*a + 400*X20**2 + 1000*X20*X50 - 20*X20*b
```
and then because E(X2i ) = 1/2 = E(X i ), we make the following substitutions
```
```
>>> expr.xreplace({X10**2:0.5, X20**2:0.5,X10:0.5,X20:0.5,X50:0.5})-350.0*a - 15.0*b + 725.0
```
We can do this for the other orthogonal inner product in Eq. 2.5.2.4 as follows,
Programming Tip
Because Sympy symbols are hashable, they can be used as keys in Python
dictionaries as in the xreplace function above.
70 2 Probability
```
>>> print S.expand((xi-h)*1).xreplace({X10**2:0.5,... X20**2:0.5,
```
... X10:0.5,... X20:0.5,
```
... X50:0.5})-15.0*a - b + 40.0
```
Then, combining this result with the previous one and solving for a and b gives,
```
>>> print S.solve([-350.0*a-15.0*b+725.0,-15.0*a-b+40.0]){b: 25.0000000000000, a: 1.00000000000000}
```
which again gives us the final solution,
```
E(ξ |η) = 25 + η
```
The following is a quick simulation to demonstrate this. We can build on the Pandas
dataframe we used for the last example and create a new column for the sum of the
10p and 20p coins, as shown below.
```
>>> d[’sm’] = d.eval(’X10*10+X20*20’)
```
We can group this by the values of this sum,
```
>>> d.groupby(’sm’).mean()X10 X20 X50
```
sm0 0 0 0.484000
10 1 0 0.47983920 0 1 0.503876
30 1 1 0.524590
But we want the expectation of the value of the coins
```
>>> d.groupby(’sm’).mean().eval(’10*X10+20*X20+50*X50’)sm
```
0 24.20000010 33.991935
20 45.19379830 56.229508
which is very close to our analytical result in Eq. 2.5.2.2.
2.5.3 Example
This is Example 2.3 paraphrased from Brzezniak. Given X uniformly distributed on
```
[0, 1], find E(ξ |η) where
```
```
ξ(x) = 2x2
```
```
η(x) =
```
⎧
⎪⎨
⎪⎩
1 if x ∈ [0, 1/3]
```
2 if x ∈ (1/3, 2/3)
```
```
0 if x ∈ (2/3, 1]
```
2.5 Worked Examples of Conditional Expectation and Mean Square Error Optimization 71
Note that this problem is different from the previous two because the sets that char-
acterize η are intervals instead of discrete points. Nonetheless, we will eventually
```
have three values for h(η) because η  → {0, 1, 2}. For η = 1, we have the orthogonal
```
conditions,
```
〈ξ − h(1), 1〉 = 0
```
which boils down to
```
E{x∈[0,1/3]}(ξ − h(1)) = 0
```
∫ 13
0
```
(2x2 − h(1))dx = 0
```
```
and then by solving this for h(1) gives h(1) = 2/24. This is the way Brzezniak
```
```
works this problem. Alternatively, we can use h(η) = a + bη + cη2 and brute force
```
calculus. Note the Piecewise object in sympy is not complete at this point in its
development, so we’ll have to be exceptionally verbose in the following,
```
x,c,b,a=S.symbols(’x,c,b,a’)xi = 2*x**2
```
```
eta=S.Piecewise((1,S.And(S.Gt(x,0),S.Lt(x,S.Rational(1,3)))), # 0 < x < 1/3
```
```
(2,S.And(S.Gt(x,S.Rational(1,3)),S.Lt(x,S.Rational(2,3)))), # 1/3 < x < 2/3,
```
```
(0,S.And(S.Gt(x,S.Rational(2,3)),S.Lt(x,1)))) # 1/3 < x < 2/3
```
```
h = a + b*eta + c*eta**2J=S.integrate((xi-h)**2,(x,0,1))
```
```
sol=S.solve([S.diff(J,a),S.diff(J,b),
```
```
S.diff(J,c),],
```
```
(a,b,c))
```
```
>>> print sol{c: 8/9, b: -20/9, a: 38/27}
```
```
>>> print S.piecewise_fold(h.subs(sol))Piecewise((2/27,And(x<1/3,x>0)),
```
```
(14/27,And(x<2/3,x>1/3)),(38/27,And(x<1,x>2/3)))
```
Thus, collecting this result gives:
```
E(ξ |η) = 3827 − 209 η + 89 η2
```
which can be re-written as a piecewise function of x,
```
E(ξ |η(x)) =
```
⎧
⎪⎨
⎪⎩
227 for 0 < x < 13
1427 for 13 < x < 23
3827 for 23 < x < 1
```
(2.5.3.1)
```
72 2 Probability
Alternatively, we can use the orthogonal inner product conditions directly by
```
choosing h(η) = c + ηb + η2a,
```
```
〈ξ − h(η), 1〉 = 0
```
```
〈ξ − h(η), η〉 = 0
```
```
〈ξ − h(η), η2〉 = 0
```
and then solving for a,b, and c.
```
>>> x,a,b,c,eta = S.symbols(’x,a,b,c,eta’,real=True)>>> xi = 2*x**2
```
```
>>> eta=S.Piecewise((1,S.And(S.Gt(x,0),... S.Lt(x,S.Rational(1,3)))), # 0 < x < 1/3
```
```
... (2,S.And(S.Gt(x,S.Rational(1,3)),... S.Lt(x,S.Rational(2,3)))), # 1/3 < x < 2/3,
```
```
... (0,S.And(S.Gt(x,S.Rational(2,3)),... S.Lt(x,1)))) # 1/3 < x < 2/3
```
>>> h = c+b*eta+a*eta**2
Then, the orthogonal conditions become,
```
>>> S.integrate((xi-h)*1,(x,0,1))-5*a/3 - b - c + 2/3
```
```
>>> S.integrate((xi-h)*eta,(x,0,1))-3*a - 5*b/3 - c + 10/27
```
```
>>> S.integrate((xi-h)*eta**2,(x,0,1))-17*a/3 - 3*b - 5*c/3 + 58/81
```
Now, we just combine the three equations and solve for the parameters,
>>> eqs=[ -5*a/3 - b - c + 2/3,... -3*a - 5*b/3 - c + 10/27,
```
... -17*a/3 - 3*b - 5*c/3 + 58/81]>>> sol=S.solve(eqs)
```
```
>>> print sol{a: 0.888888888888889, c: 1.40740740740741, b: -2.22222222222222}
```
We can assemble the final result by substituting in the solution,
```
>>> print S.piecewise_fold(h.subs(sol))Piecewise((0.0740740740740740, And (x < 1/3, x > 0)),
```
```
(0.518518518518518, And (x < 2/3, x > 1/3)),(1.40740740740741, And (x < 1, x > 2/3)))
```
which is the same as our analytic result in Eq. 2.5.3.1, just in decimal format.
Programming Tip
The definition of Sympy’s piecewise function is verbose because of the way
Python parses inequality statements. As of this writing, this has not been rec-
onciled in Sympy, so we have to use the verbose declaration.
2.5 Worked Examples of Conditional Expectation and Mean Square Error Optimization 73
To reinforce our result, let’s do a quick simulation using Pandas.
```
>>> d = pd.DataFrame(columns=[’x’,’eta’,’xi’])>>> d.x = np.random.rand(1000)
```
>>> d.xi = 2*d.x**2
Now, we can use the pd.cut function to group the x values in the following,
```
>>> pd.cut(d.x,[0,1/3,2/3,1]).head()0 (0.667, 1]
```
```
1 (0, 0.333]2 (0.667, 1]
```
```
3 (0.333, 0.667]4 (0.333, 0.667]
```
```
Name: x, dtype: categoryCategories (3, object): [(0, 0.333] < (0.333, 0.667] < (0.667, 1] ]
```
```
Note that the head() call above is only to limit the printout shown. The categories
```
listed are each of the intervals for eta that we specified using the [0,1/3,2/3,1]
list. Now that we know how to use pd.cut, we can just compute the mean on each
group as shown below,
```
>>> d.groupby(pd.cut(d.x,[0,1/3,2/3,1])).mean()[’xi’]x
```
```
(0, 0.333] 0.069240(0.333, 0.667] 0.520154
```
```
(0.667, 1] 1.409747Name: xi, dtype: float64
```
which is pretty close to our analytic result in Eq. 2.5.3.1. Alternatively,
sympy.stats has some limited tools for the same calculation.
```
>>> from sympy.stats import E, Uniform>>> x=Uniform(’x’,0,1)
```
```
>>> E(2*x**2,S.And(x < S.Rational(1,3), x > 0))2/27
```
```
>>> E(2*x**2,S.And(x < S.Rational(2,3), x > S.Rational(1,3)))14/27
```
```
>>> E(2*x**2,S.And(x < 1, x > S.Rational(2,3)))38/27
```
which again gives the same result still another way.
2.5.4 Example
```
This is Example 2.4 from Brzezniak. Find E(ξ |η) for
```
```
ξ(x) = 2x2
```
η =
```
{
```
2 if 0 ≤ x < 12
x if 12 < x ≤ 1
74 2 Probability
Once again, X is uniformly distributed on the unit interval. Note that η is no longer
```
discrete for every domain. For the domain 0 < x < 1/2, h(2) takes on only one
```
value, say, h0 . For this domain, the orthogonal condition becomes,
```
E{η=2}((ξ(x) − h0)2) = 0
```
which simplifies to,
∫ 1/2
0
2x2 − h0dx = 0
∫ 1/2
0
2x2dx =
∫ 1/2
0
h0dx
```
h0 = 2
```
∫ 1/2
0
2x2dx
```
h0 = 16
```
```
For the other domain where {η = x} in Eq. 2.5.4, we again use the orthogonal
```
condition,
```
E{η=x}((ξ(x) − h(x))x) = 0
```
∫ 1
1/2
```
(2x2 − h(x))xdx = 0
```
```
h(x) = 2x2
```
Assembling the solution gives,
```
E(ξ |η(x)) =
```
```
{ 1
```
6 for 0 ≤ x < 12
2x2 for 12 < x ≤ 1
although this result is not explicitly written as a function of η.
2.5.5 Example
```
This is Exercise 2.6 in Brzezniak. Find E(ξ |η) where
```
```
ξ(x) = 2x2
```
```
η(x) = 1 − |2x − 1|
```
2.5 Worked Examples of Conditional Expectation and Mean Square Error Optimization 75
and X is uniformly distributed in the unit interval. We can write this out as a piecewise
```
function in the following,
```
η =
```
{
```
2x for 0 ≤ x < 12
2 − 2x for 12 < x ≤ 1
```
The discontinuity is at x = 1/2. Let’s start with the {η = 2x} domain.
```
```
E{η=2x}((2x2 − h(2x))2x) = 0
```
∫ 1/2
0
```
(2x2 − h(2x))2xdx = 0
```
```
We can make this explicitly a function of η by a change of variables (η = 2x) which
```
gives ∫ 1
0
```
(η2/2 − h(η)) η2 dη = 0
```
```
Thus, for this domain, h(η) = η2/2. Note that due to the change of variables, h(η)
```
is valid defined over η ∈ [0, 1].
```
For the other domain where {η = 2 − 2x}, we have
```
```
E{η=2−2x}((2x2 − h(2 − 2x))(2 − 2x)) = 0
```
∫ 1
1/2
```
(2x2 − h(2 − 2x))(2 − 2x)dx = 0
```
Once again, a change of variables makes the η dependency explicit using η = 2 − 2x
which gives
∫ 1
0
```
((2 − η)2/2 − h(η)) η2 dη = 0
```
```
h(η) = (2 − η)2/2
```
Once again, the change of variables means this solution is valid over η ∈ [0, 1].
```
Thus, because both pieces are valid over the same domain (η ∈ [0, 1]), we can just
```
add them to get the final solution,
```
h(η) = η2 − 2η + 2
```
A quick simulation can help bear this out.
>>> from pandas import DataFrame
>>> import numpy as np
```
>>> d = DataFrame(columns=[’xi’,’eta’,’x’,’h’,’h1’,’h2’])
```
>>> # 100 random samples
76 2 Probability
```
>>> d.x = np.random.rand(100)
```
```
>>> d.xi = d.eval(’2*x**2’)
```
```
>>> d.eta =1-abs(2*d.x-1)
```
```
>>> d.h1=d[(d.x<0.5)].eval(’eta**2/2’)
```
```
>>> d.h2=d[(d.x>=0.5)].eval(’(2-eta)**2/2’)
```
```
>>> d.fillna(0,inplace=True)
```
>>> d.h = d.h1+d.h2
```
>>> d.head()
```
xi eta x h h1 h2
0 1.728372 0.140768 0.929616 1.728372 0.000000 1.728372
1 0.200187 0.632751 0.316376 0.200187 0.200187 0.000000
2 0.067652 0.367838 0.183919 0.067652 0.067652 0.000000
3 0.083690 0.409121 0.204560 0.083690 0.083690 0.000000
4 0.644623 0.864550 0.567725 0.644623 0.000000 0.644623
Note that we have to be careful where we apply the individual solutions using the
```
slice (d.x<0.5) index. The fillna part ensures that the default NaN that fills out
```
the empty row-etries is replaced with zero before combining the individual solutions.
Otherwise, the NaN values would circulate through the rest of the computation. The
following is the essential code that draws Fig. 2.7.
```
from matplotlib.pyplot import subplotsfig,ax=subplots()
```
```
ax.plot(d.xi,d.eta,’.’,alpha=.3,label=’$\eta$’)ax.plot(d.xi,d.h,’k.’,label=’$h(\eta)$’)
```
```
ax.legend(loc=0,fontsize=18)ax.set_xlabel(’$2 xˆ2$’,fontsize=18)
```
```
ax.set_ylabel(’$h(\eta)$’,fontsize=18)
```
Programming Tip
Basic LATEX formatting works for the labels in Fig. 2.7. The loc=0 in the
legend function is the code for the best placement for the labels in the leg-
end. The individual labels should be specified when the elements are drawn
individually, otherwise they will be hard to separate out later. This is accom-
plished using the label keyword in the plot commands.
```
Figure 2.7 shows the ξ data plotted against η and h(η) = E(ξ |η). Points on
```
```
the diagonal are points where ξ and E(ξ |η) match. As shown by the dots, there
```
is no agreement between the raw η data and ξ . Thus, one way to think about the
conditional expectation is as a functional transform that bends the curve onto the
```
diagonal line. The black dots plot ξ versus E(ξ |η) and the two match everywhere
```
along the diagonal line. This is to be expected because the conditional expectation
is the MSE best estimate for ξ among all functions of η.
2.5 Worked Examples of Conditional Expectation and Mean Square Error Optimization 77
Fig. 2.7 The diagonal line
shows where the conditional
expectation equals the ξ
function
2.5.6 Example
```
This is Exercise 2.14 from Brzezniak. Find E(ξ |η) where
```
```
ξ(x) = 2x2
```
η =
```
{
```
2x if 0 ≤ x < 12
2x − 1 if 12 < x ≤ 1
and X is uniformly distributed in the unit interval. This is the same as the last example
and the only difference here is that η is not continuous at x = 12 , as before. The first
part is exactly the same as the first part of the prior example so we will skip it here.
The second part follows the same reasoning as the last example, so we will just write
```
the answer for the {η = 2x − 1} case as the following
```
```
h(η) = (1 + η)
```
2
2 , ∀η ∈ [0, 1]
and then adding these up as before gives the full solution:
```
h(η) = 12 + η + η2
```
The interesting part about this example is shown in Fig. 2.8. The dots show where
```
η is discontinuous and yet the h(η) = E(ξ |η) solution is equal to ξ (i.e., matches
```
78 2 Probability
Fig. 2.8 The diagonal line
shows where the conditional
expectation equals the ξ
function
```
the diagonal). This illustrates the power of the orthogonal inner product technique,
```
which does not need continuity or complex set-theoretic arguments to calculate solu-
tions. By contrast, I urge you to consider Brzezniak’s solution to this problem which
requires such methods.
Extending projection methods to random variables provides multiple ways for
calculating solutions to conditional expectation problems. In this section, we also
worked out corresponding simulations using a variety of Python modules. It is always
advisable to have more than one technique at hand to cross-check potential solutions.
We worked out some of the examples in Brzezniak’s book using our methods as a way
to show multiple ways to solve the same problem. Comparing Brzezniak’s measure-
theoretic methods to our less abstract techniques is a great way to get a handle on
both concepts, which are important for advanced study in stochastic process.
2.6 Information Entropy
We are in a position to discuss information entropy. This will give us a powerful per-
spective on how information passes between experiments, and will prove important
in certain machine learning algorithms.
There used to be a TV game show where the host would hide a prize behind one of
three doors and the contestant would have to pick one of the doors. However, before
opening the door of the contestant’s choice, the host would open one of the other
doors and ask the contestant if she wanted to change her selection. This is the classic
Monty Hall problem. The question is should the contestant stay with her original
2.6 Information Entropy 79
choice or switch after seeing what the host has revealed? From the information
theory perspective, does the information environment change when the host reveals
what is behind one of the doors? The important detail here is that the host never
opens the door with the prize behind it, regardless of the contestant’s choice. That is,
the host knows where the prize is, but he does not reveal that information directly to
the contestant. This is the fundamental problem information theory addresses—how
to aggregate and reason about partial information. We need a concept of information
that can accommodate this kind of question.
2.6.1 Information Theory Concepts
The Shannon information content of an outcome x is defined as,
```
h(x) = log 21P(x)
```
```
where P(x) is the probability of x. The entropy of the ensemble X is defined to be
```
the Shannon information content of
```
H (X) =
```
∑
x
```
P(x) log 21P(x)
```
```
It is no accident that the entropy has this functional form as the expectation of h(x).
```
It leads to a deep and powerful theory of information.
To get some intuition about what information entropy means, consider a sequence
of three-bit numbers where each individual bit is equally likely. Thus, the individual
```
information content of a single bit is h(x) = log 2(2) = 1. The units of entropy
```
are bits so this says that information content of a single bit is one bit. Because the
three-bit number has elements that are mutually independent and equally likely, the
```
information entropy of the three-bit number is h(X) = 2 3 × log2(2 3)/8 = 3. Thus,
```
the basic idea of information content at least makes sense at this level.
A better way to interpret this question is as how much information would I have
to provide in order to uniquely encode an arbitrary three-bit number? In this case,
you would have to answer three questions: Is the first bit zero or one? Is the second
bit zero or one? Is the third bit zero or one? Answering these questions uniquely
specifies the unknown three-bit number. Because the bits are mutually independent,
knowing the state of any of the bits does not inform the remainder.
Next, let’s consider a situation that lacks this mutual independence. Suppose in a
group of nine otherwise identical balls there is a heavier one. Furthermore, we also
have a measuring scale that indicates whether one side is heavier, lighter, or equal
to the other. How could we identify the heavier ball? At the outset, the information
```
content, which measures the uncertainty of the situation is log 2(9) because one of the
```
nine balls is heavier. Figure 2.9 shows one strategy. We could arbitrarily select out
80 2 Probability
Fig. 2.9 One heavy ball is hidden among eight identical balls. By weighing groups sequentially,
we can determine the heavy ball
```
one of the balls (shown by the square), leaving the remaining eight to be balanced.
```
The thick, black horizontal line indicates the scale. The items below and above this
line indicate the counterbalanced sides of the scale.
If we get lucky, the scale will report that the group of four walls on either side
of the balance are equal in weight. This means that the ball that was omitted is the
heavier one. This is indicated by the hashed left-pointing arrow. In this case, all the
uncertainty has evaporated, and the informational value of that one weighing is equal
```
to log 2(9). In other words, the scale has reduced the uncertainty to zero (i.e., found
```
```
the heavy ball). On the other hand, the scale could report that the upper group of four
```
```
balls is heavier (black, upward-pointing arrow) or lighter (gray, downward-pointing
```
```
arrow). In this case, we cannot isolate the heavier ball until we perform all of the
```
indicated weighings, moving from left-to-right. Specifically, the four balls on the
heavier side have to be split by a subsequent weighing into two balls and then to one
ball before the heavy ball can be identified. Thus, this process takes three weighings.
```
The first one has information content log 2(9/8), the next has log 2(4), and the final
```
```
one has log 2(2). Adding all these up sums to log 2(9). Thus, whether or not the heavier
```
```
ball is isolated in the first weighing, the strategy consumes log2(9) bits, as it must,
```
to find the heavy ball.
However, this is not the only strategy. Figure 2.10 shows another. In this approach,
the nine balls are split up into three groups of three balls apiece. Two groups are
weighed. If they are of equal weight, then this means the heavier ball is in the group
```
that was left out (dashed arrow). Then, this group is split into two groups, with
```
one element left out. If the two balls on the scale weigh the same, then it means the
excluded one is the heavy one. Otherwise, it is one of the balls on the scale. The same
```
process follows if one of the initially weighed groups is heavier (black upward-facing
```
2.6 Information Entropy 81
Fig. 2.10 For this strategy, the balls are broken up into three groups of equal size and subsequently
weighed
```
arrow) or lighter (gray lower-facing arrow). As before the information content of the
```
```
situation is log 2(9). The first weighing reduces the uncertainty of the situation by
```
```
log2(3) and the subsequent weighing reduces it by another log 2(3). As before, these
```
```
sum to log 2(9), but here we only need two weighings whereas the first strategy in
```
Fig. 2.9 takes an average of 1/9 + 3 ∗ 8/9 ≈ 2.78 weighings, which is more than two.
Why does the second strategy use fewer weighings? To reduce weighings, we need
each weighing to adjudicate equally probable situations as many times as possible.
```
Choosing one of the nine balls at the outset (i.e., first strategy in Fig. 2.9) does not
```
do this because the probability of selecting the correct ball is 1/9. This does not
create a equiprobable situation in the process. The second strategy leaves an equally
```
probable situation at every stage (see Fig. 2.10), so it extracts the most information
```
out of each weighing as possible. Thus, the information content tells us how many bits
```
of information have to be resolved using any strategy (i.e., log 2(9) in this example).
```
```
It also illuminates how to efficiently remove uncertainty; namely, by adjudicating
```
equiprobable situations as many times as possible.
2.6.2 Properties of Information Entropy
Now that we have the flavor of the concepts, consider the following properties of the
information entropy,
```
H (X) ≥ 0
```
```
with equality if and only if P(x) = 1 for exactly one x. Intuitively, this means that
```
```
when just one of the items in the ensemble is known absolutely (i.e., with P(x) =
```
```
1), the uncertainty collapses to zero. Also note that entropy is maximized when
```
P is uniformly distributed across the elements of the ensemble. This is illustrated
in Fig. 2.11 for the case of two outcomes. In other words, information entropy is
82 2 Probability
Fig. 2.11 The information
entropy is maximized when
```
p = 1/2
```
maximized when the two conflicting alternatives are equally probable. This is the
mathematical reason why using the scale in the last example to adjudicate equally
probable situations was so useful for abbreviating the weighing process.
Most importantly, the concept of entropy extends jointly as follows,
```
H (X, Y ) =
```
∑
x,y
```
P(x, y) log 21P(x, y)
```
If and only if X and Y are independent, entropy becomes additive,
```
H (X, Y ) = H (X) + H (Y )
```
2.6.3 Kullback-Leibler Divergence
Notions of information entropy lead to notions of distance between probability dis-
tributions that will become important for machine learning methods. The Kullback-
Leibler divergence between two probability distributions P and Q that are defined
over the same set is defined as,
```
D K L (P, Q) =
```
∑
x
```
P(x) log 2P(x)Q(x)
```
```
Note that D K L (P, Q) ≥ 0 with equality if and only if P = Q. Sometimes the
```
Kullback-Leibler divergence is called the Kullback-Leibler distance, but it is not
formally a distance metric because it is asymmetrical in P and Q. The Kullback-
Leibler divergence defines a relative entropy as the loss of information if P is modeled
2.6 Information Entropy 83
in terms of Q. There is an intuitive way to interpret the Kullback-Leibler divergence
and understand its lack of symmetry. Suppose we have a set of messages to transmit,
```
each with a corresponding probability {(x1, P(x1)), (x2, P(x2)), . . . , (x n , P(x n ))}.
```
Based on what we know about information entropy, it makes sense to encode the
```
length of the message by log2 1p(x) bits. This parsimonious strategy means that more
```
frequent messages are encoded with fewer bits. Thus, we can rewrite the entropy of
the situation as before,
```
H (X) =
```
∑
k
```
P(x k ) log 21P(x
```
```
k )
```
Now, suppose we want to transmit the same set of messages, but with a different set
```
of probability weights, {(x1, Q(x1)), (x2, Q(x2)), . . . , (x n , Q(x n ))}. In this situation,
```
we can define the cross-entropy as
```
Hq (X) =
```
∑
k
```
P(x k ) log 21Q(x
```
```
k )
```
Note that only the purported length of the encoded message has changed, not the
probability of that message. The difference between these two is the Kullback-Leibler
divergence,
```
D K L (P, Q) = Hq (X) − H (X) =
```
∑
x
```
P(x) log 2P(x)Q(x)
```
In this light, the Kullback-Leibler divergence is the average difference in the encoded
lengths of the same set of messages under two different probability regimes. This
should help explain the lack of symmetry of the Kullback-Leibler divergence — left
to themselves, P and Q would provide the optimal-length encodings separately, but
there can be no necessary symmetry in how each regime would rate the informational
```
value of each message (Q(x i ) versus P(x i )). Given that each encoding is optimal-
```
length in its own regime means that it must therefore be at least sub-optimal in
another, thus giving rise to the Kullback-Leibler divergence. In the case where the
encoding length of all messages remains the same for the two regimes, then the
Kullback-Leibler divergence is zero.2
2.7 Moment Generating Functions
Generating moments usually involves integrals that are extremely difficult to com-
pute. Moment generating functions make this much, much easier. The moment gen-
erating function is defined as,
2 The best, easy-to-understand presentation of this material is chapter four of Mackay’s text [7].
Another good reference is chapter four of [8].
84 2 Probability
```
M(t) = E(exp(t X))
```
```
The first moment is the mean, which we can easily compute from M(t) as,
```
```
d M(t)
```
```
dt =
```
d
```
dt E(exp(t X)) = E
```
d
```
dt (exp(t X))
```
```
= E(X exp(t X))
```
Now, we have to set t = 0 and we have the mean,
```
M(1) (0) = E(X)
```
continuing this derivative process again, we obtain the second moment as,
```
M(2) (t) = E(X2 exp(t X))
```
```
M(2) (0) = E(X2)
```
With this in hand, we can easily compute the variance as,
```
V(X) = E(X2) − E(X)2 = M(2) (0) − M(1) (0)2
```
Example Returning to our favorite binomial distribution, let’s compute some
moments using Sympy.
>>> import sympy as S
>>> from sympy import stats
```
>>> p,t = S.symbols(’p t’,positive=True)
```
```
>>> x=stats.Binomial(’x’,10,p)
```
```
>>> mgf = stats.E(S.exp(t*x))
```
```
Now, let’s compute the first moment (aka, mean) using the usual integration method
```
and using moment generating functions,
```
>>> print S.simplify(stats.E(x))
```
10*p
```
>>> print S.simplify(S.diff(mgf,t).subs(t,0))
```
10*p
Otherwise, we can compute this directly as follows,
```
>>> print S.simplify(stats.moment(x,1)) # mean
```
10*p
```
>>> print S.simplify(stats.moment(x,2)) # 2nd moment
```
```
10*p*(9*p + 1)
```
2.7 Moment Generating Functions 85
In general, the moment generating function for the binomial distribution is the fol-
lowing,
```
M X (t) =
```
```
(
```
p
```
(
```
e t − 1
```
)
```
- 1
```
)n
```
A key aspect of moment generating functions is that they are unique identifiers
of probability distributions. By the uniqueness theorem, given two random variables
X and Y , if their respective moment generating functions are equal, then the corre-
sponding probability distribution functions are equal.
Example Let’s use the uniqueness theorem to consider the following problem. Sup-
pose we know that the probability distribution of X given U = p is binomial with
parameters n and p. For example, suppose X represents the number of heads in n
coin flips, given the probability of heads is p. We want to find the unconditional
distribution of X. Writing out the moment generating function as the following,
```
E(e t X |U = p) = ( pe t + 1 − p)n
```
Because U is uniform over the unit interval, we can integrate this part out
```
E(e t X ) =
```
∫ 1
0
```
( pe t + 1 − p)n dp
```
= 1n + 1e
```
t (n+1)−1
```
e t − 1
```
= 1n + 1 (1 + e t + e2t + e3t + · · · + e nt )
```
Thus, the moment generating function of X corresponds to that of a random variable
that is equally likely to be any of the values 0, 1, . . . , n. This is another way of saying
```
that the distribution of X is discrete uniform over {0, 1, . . . , n}. Concretely, suppose
```
we have a box of coins whose individual probability of heads is unknown and that
we dump the box on the floor, spilling all of the coins. If we then count the number
of coins facing heads-up, that distribution is uniform.
Moment generating functions are useful for deriving distributions of sums of
independent random variables. Suppose X1 and X2 are independent and Y = X1 +
X2 . Then, the moment generating function of Y follows from the properties of the
expectation,
```
M Y (t) = E(e tY ) = E(e t X1+t X2 )
```
```
= E(e t X1 e t X2 ) = E(e t X1 )E(e t X2 )
```
```
= M X1 (t)M X2 (t)
```
86 2 Probability
Example Suppose we have two normally distributed random variables, X1 ∼
```
N (μ1, σ1) and X2 ∼ N (μ2, σ2). We can save some tedium by exploring this in
```
Sympy,
```
>>> S.var(’x:2’,real=True)
```
```
(x0, x1)
```
```
>>> S.var(’mu:2’,real=True)
```
```
(mu0, mu1)
```
```
>>> S.var(’sigma:2’,positive=True)
```
```
(sigma0, sigma1)
```
```
>>> S.var(’t’,positive=True)
```
t
```
>>> x0=stats.Normal(x0,mu0,sigma0)
```
```
>>> x1=stats.Normal(x1,mu1,sigma1)
```
Programming Tip
The S.var function defines the variable and injects it into the global
namespace. This is sheer laziness. It is more expressive to define variables
```
explicitly as in x = S.symbols(’x’). Also notice that we used the Greek
```
names for the mu and sigma variables. This will come in handy later when
we want to render the equations in the Jupyter/IPython notebook which under-
```
stands how to typeset these symbols in LATEX. The var(’x:2’) creates
```
two symbols, x0 and x1. Using the colon this way makes it easy to generate
array-like sequences of symbols.
In the next block we compute the moment generating functions
```
>>> mgf0=S.simplify(stats.E(S.exp(t*x0)))
```
```
>>> mgf1=S.simplify(stats.E(S.exp(t*x1)))
```
```
>>> mgfY=S.simplify(mgf0*mgf1)
```
The moment generating functions an individual normally distributed random variable
is the following,
eμ0 t+
σ 20 t22
Note the coefficients of t. To show that Y is normally distributed, we want to match
the moment generating function of Y to this format. The following is the form of the
moment generating function of Y ,
```
M Y (t) = e t2 (2μ0 +2μ1+σ 20 t+σ 21 t)
```
We can extract the exponent using Sympy and collect on the t variable using the
following code,
```
>>> S.collect(S.expand(S.log(mgfY)),t)
```
```
t**2*(sigma0**2/2 + sigma1**2/2) + t*(mu0 + mu1)
```
2.7 Moment Generating Functions 87
Fig. 2.12 The histogram approximates the target probability density
Thus, by the uniqueness theorem, Y is normally distributed with μY = μ0 + μ1 and
σ 2Y = σ 20 + σ 21 .
Programming Tip
When using the Jupyter/IPython notebook, you can do S.init_printing
to get the mathematical typesetting to work in the browser. Otherwise, if
you want to keep the raw expression and to selectively render to LATEX,
then you can from IPython.display import Math, and then use
```
Math(S.latex(expr)) to see the typeset version of the expression.
```
2.8 Monte Carlo Sampling Methods
So far, we have studied analytical ways to transform random variables and how to
augment these methods using Python. In spite of all this, we frequently must resort
to purely numerical methods to solve real-world problems. Hopefully, now that we
have seen the deeper theory, these numerical methods feel more concrete. Suppose
```
we want to generate samples of a given density, f (x), given we already can generate
```
samples from a uniform distribution, U[0, 1]. How do we know a random sample v
```
comes from the f (x) distribution? One approach is to look at how a histogram of
```
```
samples of v approximates f (x). Specifically,
```
```
P(v ∈ NΔ (x)) = f (x)Δx (2.8.0.1)
```
88 2 Probability
which says that the probability that a sample is in some NΔ neighborhood of x is
```
approximately f (x)Δx. Figure 2.12 shows the target probability density function
```
```
f (x) and a histogram that approximates it. The histogram is generated from samples
```
v. The hatched rectangle in the center illustrates Eq. 2.8.0.1. The area of this rectangle
```
is approximately f (x)Δx where x = 0, in this case. The width of the rectangle is
```
```
NΔ (x) The quality of the approximation may be clear visually, but to know that v
```
```
samples are characterized by f (x), we need the statement of Eq. 2.8.0.1, which says
```
that the proportion of samples v that fill the hatched rectangle is approximately equal
```
to f (x)Δx.
```
Now that we know how to evaluate samples v that are characterized by the density
```
f (x), let’s consider how to create these samples for both discrete and continuous
```
random variables.
2.8.1 Inverse CDF Method for Discrete Variables
Suppose we want to generate samples from a fair six-sided die. Our workhouse
uniform random variable is defined continuously over the unit interval and the fair
six-sided die is discrete. We must first create a mapping between the continuous
random variable u and the discrete outcomes of the die. This mapping is shown in
Fig. 2.13 where the unit interval is broken up into segments, each of length 1/6.
Each individual segment is assigned to one of the die outcomes. For example, if
```
u ∈ [1/6, 2/6), then the outcome for the die is 2. Because the die is fair, all segments
```
on the unit interval are the same length. Thus, our new random variable v is derived
from u by this assignment.
For example, for v = 2, we have,
```
P(v = 2) = P(u ∈ [1/6, 2/6)) = 1/6
```
```
where, in the language of the Eq. 2.8.0.1, f (x) = 1 (uniform distribution), Δx = 1/6,
```
```
and NΔ (2) = [1/6, 2/6). Naturally, this pattern holds for all the other die outcomes
```
```
in {1, 2, 3, . . . , 6}. Let’s consider a quick simulation to make this concrete. The
```
following code generates uniform random samples and stacks them in a Pandas
dataframe.
Fig. 2.13 A uniform distribution random variable on the unit interval is assigned to the six outcomes
of a fair die using these segements
2.8 Monte Carlo Sampling Methods 89
import pandas as pdimport numpy as np
```
from pandas import DataFrameu= np.random.rand(100)
```
```
df = DataFrame(data=u,columns=[’u’])
```
```
The next block uses pd.cut to map the individual samples to the set {1, 2, . . . , 6}
```
labeled v.
```
labels = [1,2,3,4,5,6]df[’v’]=pd.cut(df.u,np.linspace(0,1,7),
```
```
include_lowest=True,labels=labels)
```
This is what the dataframe contains. The v column contains the samples drawn from
the fair die.
```
>>> df.head()u v
```
0 0.876426 61 0.360385 3
2 0.427294 33 0.833833 6
4 0.112139 1
The following is a count of the number of samples in each group. There should be
roughly the same number of samples in each group because the die is fair.
```
>>> df.groupby(’v’).count()u
```
v1 18
2 123 20
4 135 15
6 22
So far, so good. We now have a way to simulate a fair die from a uniformly distributed
random variable.
To extend this to unfair die, we need only make some small adjustments to this
```
code. For example, suppose that we want an unfair die so that P(1) = P(2) = P(3) =
```
```
1/12 and P(4) = P(5) = P(6) = 1/4. The only change we have to make is with
```
pd.cut as follows,
```
df[’v’]=pd.cut(df.u,[0,1/12,2/12,3/12,2/4,3/4,1],include_lowest=True,labels=labels)
```
```
>>> df.groupby(’v’).count()/df.shape[0]u
```
v1 0.08
2 0.103 0.09
4 0.235 0.19
6 0.31
90 2 Probability
where now these are the individual probabilities of each digit. You can take more
than 100 samples to get a clearer view of the individual probabilities but the mech-
anism for generating them is the same. The method is called the inverse CDF3
```
method because the CDF (namely,[0,1/12,2/12,3/12,2/4,3/4,1]) in the
```
```
last example has been inverted (using the pd.cut method) to generate the samples.
```
The inversion is easier to see for continuous variables, which we consider next.
2.8.2 Inverse CDF Method for Continuous Variables
The method above applies to continuous random variables, but now we have to use
squeeze the intervals down to individual points. In the example above, our inverse
```
function was a piecewise function that operated on uniform random samples. In this
```
case, the piecewise function collapses to a continuous inverse function. We want to
generate random samples for a CDF that is invertible. As before, the criterion for
generating an appropriate sample v is the following,
```
P(F(x) < v < F(x + Δx)) = F(x + Δx) − F(x) =
```
∫ x+Δx
x
```
f (u)du ≈ f (x)Δx
```
which is saying that the probability that the sample v is contained in a Δx interval is
```
approximately equal to the density function, f (x)Δx, at that point. Once again, the
```
```
trick is to use a uniform random sample u and an invertible CDF F(x) to construct
```
these samples. Note that for a uniform random variable u ∼ U[0, 1], we have,
```
P(x < F−1(u) < x + Δx) = P(F(x) < u < F(x + Δx))
```
```
= F(x + Δx) − F(x)
```
=
∫ x+Δx
x
```
f ( p)dp ≈ f (x)Δx
```
```
This means that v = F−1(u) is distributed according to f (x), which is what we
```
want.
Let’s try this to generate samples from the exponential distribution,
```
fα (x) = αe−αx
```
which has the following CDF,
```
F(x) = 1 − e−αx
```
```
3 Cumulative density function. Namely, F(x) = P(X < x).
```
2.8 Monte Carlo Sampling Methods 91
Fig. 2.14 The samples
created using the inverse cdf
method match the
exponential reference
distribution
and corresponding inverse,
```
F−1(u) = 1α ln 1(1 − u)
```
Now, all we have to do is generate some uniformly distributed random samples and
then feed them into F−1 .
>>> from numpy import array, log
>>> import scipy.stats
>>> alpha = 1. # distribution parameter
>>> nsamp = 1000 # num of samples
>>> # define uniform random variable
```
>>> u=scipy.stats.uniform(0,1)
```
>>> # define inverse function
```
>>> Finv=lambda u: 1/alpha*log(1/(1-u))
```
>>> # apply inverse function to samples
```
>>> v = array(map(Finv,u.rvs(nsamp)))
```
Now, we have the samples from the exponential distribution, but how do we
know the method is correct with samples distributed accordingly? Fortunately,
scipy.stats already has a exponential distribution, so we can check our work
```
against the reference using a probability plot (i.e., also known as a quantile-quantile
```
```
plot). The following code sets up the probability plot from scipy.stats.
```
```
fig,ax=subplots()scipy.stats.probplot(v,(1,),dist=’expon’,plot=ax)
```
```
Note that we have to supply an axes object (ax) for it to draw on. The result is
```
Fig. 2.14. The more the samples line match the diagonal line, the more they match
```
the reference distribution (i.e., exponential distribution in this case). You may also
```
want to try dist=norm in the code above To see what happens when the normal
distribution is the reference distribution.
92 2 Probability
2.8.3 Rejection Method
In some cases, inverting the CDF may be impossible. The rejection method can handle
this situation. The idea is to pick two uniform random variables u1, u2 ∼ U[a, b] so
that
P
```
(
```
```
u1 ∈ NΔ (x)
```
∧
```
u2 < f (u1)M
```
```
)
```
```
≈ Δxb − af (u1)M
```
```
where we take x = u1 and f (x) < M. This is a two-step process. First, draw u1
```
```
uniformly from the interval [a, b]. Second, feed it into f (x) and if u2 < f (u1)/M,
```
```
then you have a valid sample for f (x). Thus, u1 is the proposed sample from f that
```
may or may not be rejected depending on u2 . The only job of the M constant is to
```
scale down the f (x) so that the u2 variable can span the range. The efficiency of
```
this method is the probability of accepting u1 which comes from integrating out the
above approximation,
```
∫ f (x)
```
```
M(b − a) dx =
```
1
```
M(b − a)
```
∫
```
f (x)dx = 1M(b − a)
```
This means that we don’t want an unecessarily large M because that makes it more
likely that samples will be discarded.
Let’s try this method for a density that does not have a continuous inverse. 4
```
f (x) = exp
```
```
(
```
```
− (x − 1)
```
2
2x
```
)
```
```
(x + 1)/12
```
where x > 0. The following code implements the rejection plan.
>>> import numpy as np
```
>>> x = np.linspace(0.001,15,100)
```
```
>>> f= lambda x: np.exp(-(x-1)**2/2./x)*(x+1)/12.
```
```
>>> fx = f(x)
```
>>> M=0.3 # scale factor
```
>>> u1 = np.random.rand(10000)*15 # uniform random samples scaled out
```
```
>>> u2 = np.random.rand(10000) # uniform random samples
```
```
>>> idx,= np.where(u2<=f(u1)/M) # rejection criterion
```
>>> v = u1[idx]
Figure 2.15 shows a histogram of the so-generated samples that nicely fits the prob-
ability density function. The title in the figure shows the efficiency, which is poor. It
means that we threw away most of the proposed samples. Thus, even though there
is nothing conceptually wrong with this result, the low efficiency must be fixed,
as a practical matter. Figure 2.16 shows where the proposed samples were rejected.
```
Samples under the curve were retained (i.e., u2 < f (u1)M ) but the vast majority of the
```
samples are outside this umbrella.
4 Note that this example density does not exactly integrate out to one like a probability density
```
function should, but the normalization constant for this is distracting for our purposes here.
```
2.8 Monte Carlo Sampling Methods 93
Fig. 2.15 The rejection method generate samples in the histogram that nicely match the target
distribution. Unfortunately, the efficiency is not so good
Fig. 2.16 The proposed samples under the curve were accepted and the others were not. This shows
the majority of samples were rejected
```
The rejection method uses u1 to select along the domain of f (x) and the other
```
u2 uniform random variable decides whether to accept or not. One idea would be to
```
choose u1 so that x values are coincidentally those that are near the peak of f (x),
```
instead of uniformly anywhere in the domain, especially near the tails, which are low
```
probability anyway. Now, the trick is to find a new density function g(x) to sample
```
from that has a similiar concentration of probability density. One way it to familiarize
oneself with the probability density functions that have adjustable parameters and
fast random sample generators already. There are lots of places to look and, chances
are, there is likely already such a generator for your problem. Otherwise, the family
of β densities is a good place to start.
```
To be explicit, what we want is u1 ∼ g(x) so that, returning to our earlier argument,
```
P
```
(
```
```
u1 ∈ NΔ (x)
```
∧
```
u2 < f (u1)M
```
```
)
```
```
≈ g(x)Δx f (u1)M
```
94 2 Probability
but this is not what we need here. The problem is with the second part of the logical ∧
conjunction. We need to put something there that will give us something proportional
```
to f (x). Let us define the following,
```
```
h(x) = f (x)g(x) (2.8.3.1)
```
with corresponding maximum on the domain as hmax and then go back and construct
the second part of the clause as
P
```
(
```
```
u1 ∈ NΔ (x)
```
∧
```
u2 < h(u1)h
```
max
```
)
```
```
≈ g(x)Δx h(u1)h
```
max
```
= f (x)/ hmax
```
Recall that satisfying this criterion means that u1 = x. As before, we can estimate
the probability of acceptance of the u1 as 1/ hmax .
```
Now, how to construct the g(x) function in the denominator of Eq. 2.8.3.1? Here’s
```
where familarity with some standard probability densities pays off. For this case, we
```
choose the chi-squared distribution. The following plots the g(x) and f (x) (left plot)
```
```
and the corresponding h(x) = f (x)/g(x) (right plot). Note that g(x) and f (x) have
```
```
peaks that almost coincide, which is what we are looking for (Fig. 2.17).
```
```
>>> ch=scipy.stats.chi2(4) # chi-squared
```
```
>>> h = lambda x: f(x)/ch.pdf(x) # h-function
```
Now, let’s generate some samples from this χ2 distribution with the rejection method.
```
>>> hmax=h(x).max()
```
```
>>> u1 = ch.rvs(5000) # samples from chi-square distribution
```
```
>>> u2 = np.random.rand(5000)# uniform random samples
```
```
>>> idx = (u2 <= h(u1)/hmax) # rejection criterion
```
>>> v = u1[idx] # keep these only
Using the χ2 distribution with the rejection method results in throwing away
less than 10 % of the generated samples compared with our prior example where
we threw out at least 80 %. This is dramatically more efficient. Figure 2.18 shows
```
Fig. 2.17 The plot on the right shows h(x) = f (x)/g(x) and the one on the left shows f (x) and
```
```
g(x) separately
```
2.8 Monte Carlo Sampling Methods 95
Fig. 2.18 Using the updated
method, the histogram
matches the target
probability density function
with high efficiency
Fig. 2.19 Fewer proposed
points were rejected in this
case, which means better
efficiency
that the histogram and the probability density function match. For completeness,
```
Fig. 2.19 shows the samples with the corresponding threshold h(x)/ hmax that was
```
used to select them.
In this section, we investigated how to generate random samples from a given
distribution, beit discrete or continuous. For the continuous case, the key issue was
whether or not the cumulative density function had a continuous inverse. If not,
we had to turn to the rejection method, and find an appropriate related density that
we could easily sample from to use as part of a rejection threshold. Finding such a
```
function is an art, but many families of probability densities have been studied over
```
the years that already have fast random number generators.
The rejection method has many complicated extensions that involve careful par-
titioning of the domains and lots of special methods for corner cases. Nonetheless,
all of these advanced techniques are still variations on the same fundamental theme
we illustrated here [9, 10].
2.9 Useful Inequalities
In practice, few quantities can be analytically calculated. Some knowledge of
bounding inequalities helps find the ballpark for potential solutions. This sections
discusses three key inequalities that are important for probability, statistics, and
machine learning.
96 2 Probability
2.9.1 Markov’s Inequality
```
Let X be a non-negative random variable and suppose that E(X) < ∞. Then, for
```
any t > 0,
```
P(X > t) ≤ E(X)t
```
This is a foundational inequality that is used as a stepping stone to other inequalities.
It is easy to prove. Because X > 0, we have the following,
```
E(X) =
```
∫ ∞
0
```
x f x (x)dx =
```
∫ t
0
```
x f x (x)dx
```
︸ ︷︷ ︸
omit this
+
∫ ∞
t
```
x f x (x)dx
```
≥
∫ ∞
t
```
x f x (x)dx ≥ t
```
∫ ∞
t
```
x f x (x)dx = tP(X > t)
```
The step that establishes the inequality is the part where the
∫ t
```
0 x f x (x)dx is omitted.
```
```
For a particular f x (x) that my be concentrated around the [0, t] interval, this could
```
be a lot to throw out. For that reason, the Markov Inequality is considered a loose
inequality, meaning that there is a substantial gap between both sides of the inequality.
For example, as shown in Fig. 2.20, the χ2 distribution has a lot of its mass on the left,
which would be omitted in the Markov Inequality. Figure 2.21 shows the two curves
established by the Markov Inequality. The gray shaded region is the gap between
```
the two terms and indicates that looseness of the bound (fatter shaded region) for
```
this case.
Fig. 2.20 The χ21 density
has much of its weight on the
left, which is excluded in the
establishment of the Markov
Inequality
2.9 Useful Inequalities 97
Fig. 2.21 The shaded area
shows the region between the
curves on either side of the
Markov Inequality
2.9.2 Chebyshev’s Inequality
```
Chebyshev’s Inequality drops out directly from the Markov Inequality. Let μ = E(X)
```
```
and σ 2 = V(X). Then, we have
```
```
P(|X − μ| ≥ t) ≤ σ
```
2
t2
```
Note that if we normalize so that Z = (X − μ)/σ , we have P(|Z | ≥ k) ≤ 1/k2 . In
```
```
particular, P(|Z | ≥ 2) ≤ 1/4. We can illustrate this inequality using Sympy statistics
```
module,
>>> import sympy
>>> import sympy.stats as ss
```
>>> t=sympy.symbols(’t’,real=True)
```
```
>>> x=ss.ChiSquared(’x’,1)
```
To get the left side of the Chebyshev inequality, we have to write this out as the
following conditional probability,
```
>>> r = ss.P((x-1) > t,x>1)+ss.P(-(x-1) > t,x<1)
```
This is because of certain limitations in the statistics module at this point in its devel-
opment regarding the absolute value function. We could take the above expression,
which is a function of t and attempt to compute the integral, but that would take a
```
very long time (the expression is very long and complicated, which is why we did
```
```
not print it out above). This is because Sympy is a pure-python module that does not
```
utilize any C-level optimizations under the hood. In this situation, it’s better to use the
```
built-in cumulative density function as in the following (after some rearrangement
```
```
of the terms),
```
98 2 Probability
Fig. 2.22 The shaded area
shows the region between the
curves on either side of the
Chebyshev Inequality
```
>>> w=(1-ss.cdf(x)(t+1))+ss.cdf(x)(1-t)
```
To plot this, we can evaluate it at a variety of t values by using the .subs substitution
method, but it is more convenient to use the lambdify method to convert the
expression to a function.
```
>>> fw=sympy.lambdify(t,w)
```
Then, we can evaluate this function using something like
```
>>> map(fw,[0,1,2,3,4])
```
[1.0,0.157299207050285,0.08326451666355039,0.045500263896358
75,0.0253473186774682]
to produce the following Fig. 2.22.
Programming Tip
Note that we cannot use vectorized inputs for the lambdify function because
it contains embedded functions that are only available in Sympy. Otherwise, we
```
could have used lambdify(t,fw,numpy) to specify the corresponding
```
functions in Numpy to use for the expression.
2.9.3 Hoeffding’s Inequality
Hoeffding’s Inequality is similar, but less loose, than Markov’s Inequality. Let
```
X1, . . . , X n be iid observations such that E(X i ) = μ and a ≤ X i ≤ b. Then,
```
for any  > 0, we have
2.9 Useful Inequalities 99
Fig. 2.23 This shows the
Markov and Hoeffding
bounds for the case of ten
identically and uniformly
distributed random variables
```
P(|X n − μ| ≥ ) ≤ 2 exp(−2n2/(b − a)2)
```
where X n = 1n∑ni X i . Note that we further assume that the individual random
variables are bounded.
```
Corollary If X1, . . . , X n are independent with P(a ≤ X i ≤ b) = 1 and all with
```
```
E(X i ) = μ. Then, we have
```
|X n − μ| ≤
√
c
2n log
2
δ
```
where c = (b−a)2 . We will see this inequality again in the machine learning chapter.
```
Figure 2.23 shows the Markov and Hoeffding bounds for the case of ten identically
and uniformly distributed random variables, X i ∼ U[0, 1]. The solid line shows
```
P(|X n − 1/2| > ). Note that the Hoeffding Inequality is tighter than the Markov
```
Inequality and that both of them merge when  gets big enough.
References
1. F. Jones, Lebesgue Integration on Euclidean Space, Jones and Bartlett Books in Mathematics
```
(Jones and Bartlett, London, 2001)
```
2. G. Strang, Linear Algebra and Its Applications (Elsevier Science, 2014). https://books.google.
com/books?id=9A7jBQAAQBAJ, ISBN 9781483265117
3. E. Nelson, Radically Elementary Probability Theory, Annals of Mathematics Studies (Princeton
```
University Press, Princeton, 1987)
```
4. T. Mikosch, Elementary Stochastic Calculus with Finance in View, Advanced Series on Statis-
```
tical Science & Applied Probability (World Scientific, Singapore, 1998)
```
5. H. Kobayashi, B.L. Mark, W. Turin, Probability, Random Processes, And Statistical Analysis:
Applications To Communications, Signal Processing, Queueing Theory And Mathematical
```
Finance, Engineering Pro Collection (Cambridge University Press, Cambridge, 2011)
```
100 2 Probability
6. Z. Brzezniak, T. Zastawniak, Basic Stochastic Processes: A Course Through Exercises, Springer
```
Undergraduate Mathematics Series (Springer, London, 1999)
```
7. D.J.C. MacKay, Information Theory, Inference and Learning Algorithms (Cambridge Univer-
```
sity Press, Cambridge, 2003)
```
8. T. Hastie, R. Tibshirani, J. Friedman, The Elements of Statistical Learning: Data Mining,
```
Inference, and Prediction, Springer Series in Statistics (Springer, New York, 2013)
```
9. W.L. Dunn, J.K. Shultis, Exploring Monte Carlo Methods (Elsevier Science, Boston, 2011)
10. N.L. Johnson, S. Kotz, N. Balakrishnan, Continuous Univariate Distributions, vol. 2, Wiley
```
Series in Probability and Mathematical Statistics: Applied Probability and Statistics (Wiley &
```
```
Sons, New York, 1995)
```
Chapter 3
Statistics
3.1 Introduction
To get started thinking about statistics, consider the three famous problems
• Suppose you have a bag filled with colored marbles. You close your eyes and reach
into it and pull out a handful of marbles, what can you say about what is in the
bag?
• You arrive in a strange town and you need a taxicab. You look out the window,
and in the dark, you can just barely make out the number on the roof of one of
the cabs. In this town, you know they label the cabs sequentially. How many cabs
does the town have?
• You have already taken the entrance exam twice and you want to know if it’s worth
it to take it a third time in the hopes that your score will improve. Because only
the last score is reported, you are worried that you may do worse the third time.
How do you decide whether or not to take the test again?
Statistics provides a structured way to approach each of these problems. This is
important because it is easy to be fooled by your biases and intuitions. Unfortunately,
the field does not provide a single way to do this, which explains the many library
shelves that groan under the weight of statistics texts. This means that although many
statistical quantities are easy to compute, these are not so easy to justify, explain,
or even understand. Fundamentally, when we start with just the data, we lack the
underlying probability density that we discussed in the last chapter. This removes
key structures that we have to compensate for in however we choose to process the
data. In the following, we consider some of the most powerful statistical tools in the
Python arsenal and suggest ways to think through them
© Springer International Publishing Switzerland 2016
J. Unpingco, Python for Probability, Statistics, and Machine Learning,
DOI 10.1007/978-3-319-30717-6_3
101
102 3 Statistics
3.2 Python Modules for Statistics
3.2.1 Scipy Statistics Module
```
Although there are some basic statistical functions in Numpy (e.g., mean, std,
```
```
median), the real repository for statistical functions is in scipy.stats. There
```
are over eighty continuous probability distributions implemented in scipy.stats
and an additional set of more than ten discrete distributions, along with many other
supplementary statistical functions that we will select from in what follows.
To get started with scipy.stats, you have to load the module and create an
object that has the distribution you’re interested in. For example,
```
>>> import scipy.stats # might take awhile>>> n = scipy.stats.norm(0,10) # create normal distrib
```
The n variable is an object that represents a normally distributed random variable
with mean zero and standard deviation, σ = 10. Note that the more general term
for these two parameters is location and scale, respectively. Now that we have this
defined, we can compute mean, as in the following:
```
>>> n.mean() # we already know this from its definition!0
```
We can also compute higher order moments as
```
>>> n.moment(4)30000
```
The main public methods for continuous random variables are
• rvs: random variates
• pdf: probability density function
• cdf: cumulative distribution function
```
• sf: survival Function (1-CDF)
```
```
• ppf: percent point function (Inverse of CDF)
```
```
• isf: inverse survival function (Inverse of SF)
```
```
• stats: mean, variance, (Fisher’s) skew, or (Fisher’s) kurtosis
```
• moment: non-central moments of the distribution
For example, we can compute the value of the pdf at a specific point.
```
>>> n.pdf(0)0.039894228040143268
```
or, the cdf for the same random variable.
```
>>> n.cdf(0)0.5
```
3.2 Python Modules for Statistics 103
You can also create samples from this distribution as in the following:
```
>>> n.rvs(10)array([ -8.11311677, 1.48034316, 1.0824489 , -4.38642452,
```
```
23.69872505, -22.19428082, -7.19207387, 10.6447697,3.4549407 , 1.67282213])
```
Many common statistical tests are already built-in. For example, Shapiro-Wilks tests
the null hypothesis that the data were drawn from a normal distribution, 1 as in the
```
following:
```
```
>>> scipy.stats.shapiro(n.rvs(100))(0.9914381504058838, 0.779195249080658)
```
The second value in the tuple is the p-value.
3.2.2 Sympy Statistics Module
Sympy has its own much smaller, but still extremely useful statistics module that
enables symbolic manipulation of statistical quantities. For example,
```
>>> from sympy import stats>>> X = stats.Normal(’x’,0,10) # create normal random variable
```
We can obtain the probability density function as,
```
>>> from sympy.abc import x>>> stats.density(X)(x)
```
```
sqrt(2)*exp(-x**2/200)/(20*sqrt(pi))
```
and we can evaluate the cumulative density function as the following,
```
>>> stats.cdf(X)(0)1/2
```
```
Note that you can evaluate this numerically by using the evalf() method on the
```
output. Sympy provides intuitive ways to consider standard probability questions by
using the stats.P function, as in the following:
```
>>> stats.P(X>0) # prob X >0?1/2
```
There is also a corresponding expectation function, stats.E you can use to com-
pute complicated expectations using all of Sympy’s powerful built-in integration
```
machinery. For example we can compute, E(√|X|) in the following,
```
```
>>> stats.E(abs(X)**(1/2)).evalf()2.59995815363879
```
Unfortunately, there is very limited support for multivariate distributions at the time
of this writing.
1 We will explain null hypothesis and the rest of it later.
104 3 Statistics
3.2.3 Other Python Modules for Statistics
There are many other important Python modules for statistical work. Two important
modules are Seaborn and Statsmodels. As we discussed earlier, Seaborn is library
built on top of Matplotlib for very detailed and expressive statistical visualizations,
ideally suited for exploratory data analysis. Statsmodels is designed to complement
Scipy with descriptive statistics, estimation, and inference for a large variety of
```
statistical models. Statsmodels includes (among many others) generalized linear
```
models, robust linear models, and methods for timeseries analysis, with an emphasis
on econometric data and problems. Both these modules are well supported and very
well documented and designed to integrate tightly into Matplotlib, Numpy, Scipy,
and the rest of the scientific Python stack. Because the focus of this text is more
conceptual as opposed to domain-specific, I have chosen not to emphasize either of
these, notwithstanding how powerful each is.
3.3 Types of Convergence
The absence of the probability density for the raw data means that we have to argue
about sequences of random variables in a structured way. From basic calculus, recall
the following convergence notation,
x n → x o
for the real number sequence x n . This means that for any given  > 0, no matter how
small, we can exhibit a m such that for any n > m, we have
|x n − x o| < 
Intuitively, this means that once we get past m in the sequence, we get as to within 
of x o. This means that nothing surprising happens in the sequence on the long march
to infinity, which gives a sense of uniformity to the convergence process. When we
argue about convergence for statistics, we want to same look-and-feel as we have
here, but because we are now talking about random variables, we need other concepts.
There are two moving parts for random variables. Recall that random variables are
really functions that map sets into the real line: X : Ω  → R. Thus, one part to keep
track of is the behavior of the subsets of Ω while arguing about convergence. The
other part is the sequence of values that the random variable takes on the real line
and how those behave in the convergence process.
3.3 Types of Convergence 105
3.3.1 Almost Sure Convergence
The most straightforward extension into statistics of this convergence concept is
convergence with probability one, which is also known as almost sure convergence,
which is the following,
```
P{for each  > 0 there is n > 0 such that for all n > n, |X n − X| < } = 1
```
```
(3.3.1.1)
```
Note the similarity to the prior notion of convergence for real numbers. When this
happens, we write this as X nas→ X. In this context, almost sure convergence means
that if we take any particular ω ∈ Ω and then look at the sequence of real numbers
that are produced by each of the random variables,
```
(X1(ω), X2(ω), X3(ω), . . . , X n (ω))
```
then this sequence is just a real-valued sequence in the sense of our convergence
on the real line and converges in the same way. If we collect all of the ω for which
this is true and the measure of that collection equals one, then we have almost sure
convergence of the random variable. Notice how the convergence idea applies to both
```
sides of the random variable: the (domain) Ω side and the (co-domain) real-valued
```
side.
An equivalent and more compact way of writing this is the following,
P
```
(
```
```
ω ∈ Ω : limn→∞ X n (ω) = X (ω)
```
```
)
```
= 1
Example To get some feel for the mechanics of this kind of convergence consider the
following sequence of uniformly distributed random variables on the unit interval,
X n ∼ U[0, 1]. Now, consider taking the maximum of the set of n such variables as
the following,
```
X(n) = max{X1, . . . , X n }
```
In other words, we scan through a list of n uniformly distributed random variables
```
and pick out the maximum over the set. Intuitively, we should expect that X(n) should
```
somehow converge to one. Let’s see if we can make this happen almost surely. We
want to exhibit m so that the following is true,
```
P(|1 − X(n)|) <  when n > m
```
```
Because X(n) < 1, we can simplify this as the following,
```
```
1 − P(X(n) < ) = 1 − (1 − )m −→m→∞ 1
```
106 3 Statistics
Thus, this sequence converges almost surely. We can work this example out in Python
using Scipy to make it concrete with the following code,
```
>>> from scipy import stats>>> u=stats.uniform()
```
```
>>> xn = lambda i: u.rvs(i).max()>>> xn(5)
```
0.96671783848200299
```
Thus, the xn variable is the same as the X(n) random variable in our example.
```
Figure 3.1 shows a plot of these random variables for different values of n and multiple
```
realizations of each random variable (multiple gray lines). The dark horizontal line is
```
at the 0.95 level. For this example, suppose we are interested in the convergence of
the random variable to within 0.05 of one so we are interested in the region between
one and 0.95. Thus, in our Eq. 3.3.1.1,  = 0.05. Now, we have to find n to get
the almost sure convergence. From Fig. 3.1, as soon as we get past n > 60, we can
see that all the realizations start to fit in the region above the 0.95 horizontal line.
However, there are still some cases where a particular realization will skip below
this line. To get the probability guarantee of the definition satisfied, we have to make
sure that for whatever n we settle on, the probability of this kind of noncompliant
behavior should be extremely small, say, less than 1 %. Now, we can compute the
following to estimate this probability for n = 60 over 1000 realizations,
```
>>> import numpy as np>>> np.mean([xn(60) > 0.95 for i in range(1000)])
```
0.96099999999999997
So, the probability of having a noncompliant case beyond n > 60 is pretty good, but
```
not still what we are after (0.99). We can solve for the m in our analytic proof of
```
convergence by plugging in our factors for  and our desired probability constraint,
```
>>> print np.log(1-.99)/np.log(.95)89.7811349607
```
Now, rounding this up and re-visiting the same estimate as above,
```
>>> import numpy as np>>> np.mean([xn(90) > 0.95 for i in range(1000)])
```
0.995
Fig. 3.1 Almost sure
convergence example for
multiple realizations of the
limiting sequence
3.3 Types of Convergence 107
which is the result we were looking for. The important thing to understand from
this example is that we had to choose convergence criteria for both the values of the
```
random variable (0.95) and for the probability of achieving that level (0.99) in
```
order to compute the m. Informally speaking, almost sure convergence means that
not only will any particular X n be close to X for large n, but whole sequence of
values will remain close to X with high probability.
3.3.2 Convergence in Probability
A weaker kind of convergence is convergence in probability which means the fol-
```
lowing:
```
```
P(| X n − X |> ) → 0
```
as n → ∞ for each  > 0.
This is notationally shown as X nP→ X. For example, let’s consider the following
sequence of random variables where X n = 1/2n with probability p n and where
X n = c with probability 1 − p n . Then, we have X nP→ 0 as p n → 1. This is
allowable under this notion of convergence because a diminishing amount of non-
```
converging behavior (namely, when X n = c) is possible. Note that we have said
```
nothing about how p n → 1.
Example To get some sense of the mechanics of this kind of convergence, let
```
{X1, X2, X3, . . .} be the indicators of the corresponding intervals,
```
```
(0, 1], (0, 12 ], ( 12 , 1], (0, 13 ], ( 13 , 23 ], ( 23 , 1]
```
In other words, just keep splitting the unit interval into equal chunks and enumerate
those chunks with X i . Because each X i is an indicator function, it takes only two
```
values: zero and one. For example, for X2 = 1 if 0 < x ≤ 1/2 and zero otherwise.
```
```
Note that x ∼ U(0, 1). This means that P(X2 = 1) = 1/2. Now, we want to com-
```
```
pute the sequence of P(X n > ) for each n for some  ∈ (0, 1). For X1 , we have
```
```
P(X1 > ) = 1 because we already chose  in the interval covered by X1 . For X2 ,
```
```
we have P(X2 > ) = 1/2, for X3 , we have P(X3 > ) = 1/3, and so on. This
```
```
produces the following sequence: (1, 12 , 12 , 13 , 13 , . . .). The limit of the sequence is
```
```
zero so that X nP→ 0. However, for every x ∈ (0, 1), the sequence of function values
```
```
of X n (x) consists of infinitely many zeros and ones (remember that indicator func-
```
```
tions can evaluate to either zero or one). Thus, the set of x for which the sequence
```
```
X n (x) converges is empty because the sequence bounces between zero and one. This
```
means that almost sure convergence fails here even though we have convergence
in probability. The key distinction is that convergence in probability considers the
108 3 Statistics
convergence of a sequence of probabilities whereas almost sure convergence is con-
cerned about the sequence of values of the random variables over sets of events that
```
fill out the underlying probability space entirely (i.e., with probability one).
```
This is a good example so let’s see if we can make it concrete with some Python.
The following is a function to compute the different subintervals,
```
>>> make_interval= lambda n: np.array(zip(range(n+1),range(1,n+1)))/n
```
Now, we can use this function to create a Numpy array of intervals, as in the example,
```
>>> intervals= np.vstack([make_interval(i) for i in range(1,5)])>>> print intervals
```
[ [ 0. 1. ][ 0. 0.5 ]
[ 0.5 1. ][ 0. 0.33333333]
[ 0.33333333 0.66666667][ 0.66666667 1. ]
[ 0. 0.25 ][ 0.25 0.5 ]
[ 0.5 0.75 ][ 0.75 1. ] ]
```
The following function computes the bit string in our example, {X1, X2, . . . , X n },
```
```
>>> bits= lambda u:((intervals[:,0] < u) & (u<=intervals[:,1])).astype(int)
```
```
>>> bits(u.rvs())
```
```
array([1, 0, 1, 0, 0, 1, 0, 0, 0, 1])
```
Now that we have the individual bit strings, to show convergence we want to show
that the probability of each entry goes to a limit. For example, using ten realizations,
```
>>> print np.vstack([bits(u.rvs()) for i in range(10)])[ [1 1 0 1 0 0 0 1 0 0]
```
[1 1 0 1 0 0 0 1 0 0][1 1 0 0 1 0 0 1 0 0]
[1 0 1 0 0 1 0 0 1 0][1 0 1 0 0 1 0 0 1 0]
[1 1 0 0 1 0 0 1 0 0][1 1 0 1 0 0 1 0 0 0]
[1 1 0 0 1 0 0 1 0 0][1 1 0 0 1 0 0 1 0 0]
[1 1 0 1 0 0 1 0 0 0] ]
We want the limiting probability of a one in each column to convert to a limit. We
can estimate this over 1000 realizations using the following code,
```
>>> np.vstack([bits(u.rvs()) for i in range(1000)]).mean(axis=0)array([ 1. , 0.493, 0.507, 0.325, 0.34 , 0.335, 0.253, 0.24 ,
```
```
0.248, 0.259])
```
```
Note that these entries should approach the (1, 12 , 12 , 13 , 13 , . . .) sequence we found
```
earlier. Figure 3.2 shows the convergence of these probabilities for a large number
of intervals. Eventually, the probability shown on this graph will decrease to zero
with large enough n. Again, note that the individual sequences of zeros and ones
do not converge, but the probabilities of these sequences converge. This is the key
difference between almost sure convergence and convergence in probability. Thus,
convergence in probability does not imply almost sure convergence. Conversely,
almost sure convergence does imply convergence in probability.
3.3 Types of Convergence 109
Fig. 3.2 Convergence in
probability for the random
variable sequence
The following notation should help emphasize the difference between almost sure
convergence and convergence in probability, respectively,
P
```
(
```
limn→∞ |X n − X| < 
```
)
```
```
= 1(almost sure convergence)
```
```
limn→∞ P(|X n − X| < ) = 1(convergence in probability)
```
3.3.3 Convergence in Distribution
So far, we have been discussing convergence in terms of sequences of probabilities
or sequences of values taken by the random variable. By contrast, the next major
kind of convergence is convergence in distribution where
```
limn→∞ Fn (t) = F(t)
```
for all t for which F is continuous and F is the cumulative density function. For this
case, convergence is only concerned with the cumulative density function, written
as X nd→ X.
Example To develop some intuition about this kind of convergence, consider a
sequence of X n Bernoulli random variables. Furthermore, suppose these are all
really just the same random variable X. Trivially, X nd→ X. Now, suppose we define
```
Y = 1 − X, which means that Y has the same distribution as X. Thus, X nd→ Y . By
```
contrast, because |X n − Y | = 1 for all n, we can never have almost sure convergence
or convergence in probability. Thus, convergence in distribution is the weakest of
the three forms of convergence in the sense that it is implied by the other two, but
implies neither of the two.
110 3 Statistics
```
As another striking example, we could have Ynd→ Z where Z ∼ N (0, 1), but
```
we could also have Ynd→ −Z . That is, Yn could converge in distribution to either Z
or −Z . This may seem ambiguous, but this kind of convergence is practically very
useful because it allows for complicated distributions to be approximated by simpler
distributions.
3.3.4 Limit Theorems
Now that we have all of these notions of convergence, we can apply them to different
situations and see what kinds of claims we can construct from them.
```
Weak Law of Large Numbers. Let {X1, X2, . . . , X n } be an iid set of random vari-
```
```
ables with finite mean E(X k ) = μ and finite variance. Let X n = 1n∑k X k . Then, we
```
have X nP→ μ. This result is important because we frequently estimate parameters
using an averaging process of some kind. This basically justifies this in terms of con-
vergence in probability. Informally, this means that the distribution of X n becomes
concentrated around μ as n → ∞.
```
Strong Law of Large Numbers. Let {X1, X2, . . . , } be an iid set of random variables.
```
Suppose that μ = E|X i | < ∞, then X nas→ μ. The reason this is called the strong
law is that it implies the weak law because almost sure convergence implies conver-
gence in probability. The so-called Komogorov criterion gives the convergence of
the following,
∑
k
σ2k
k2
as a sufficient condition for concluding that the Strong Law applies to the sequence
```
{X k } with corresponding {σ2k }.
```
As an example, consider an infinite sequence of Bernoulli trials with X i = 1 if
the ith trial is successful. Then X n is the relative frequency of successes in n trials
```
and E(X i ) is the probability p of success on the ith trial. With all that established,
```
the Weak Law says only that if we consider a sufficiently large and fixed n, the
probability that the relative frequency will converge to p is guaranteed. The Strong
```
Law states that if we regard the observation of all the infinite {X i } as one performance
```
of the experiment, the relative frequency of successes will almost surely converge to
p. The difference between the Strong Law and the Weak Law of large numbers is
subtle and rarely arises in practical applications of probability theory.
Central Limit Theorem. Although the Weak Law of Large Numbers tells us that
the distribution of X n becomes concentrated around μ, it does not tell us what that
```
distribution is. The Central Limit Theorem (CLT) says that X n has a distribution that
```
is approximately Normal with mean μ and variance σ2/n. Amazingly, nothing is
3.3 Types of Convergence 111
assumed about the distribution of X i , except the existence of the mean and variance.
```
The following is the Central Limit Theorem: Let {X1, X2, . . . , X n } be iid with mean
```
μ and variance σ2 . Then,
Z n =
```
√n(X
```
```
n − μ)
```
σ
```
P−→ Z ∼ N (0, 1)
```
The loose interpretation of the Central Limit Theorem is that X n can be legitimately
approximated by a Normal distribution. Because we are talking about convergence
in probability here, claims about probability are legitimized, not claims about the
random variable itself. Intuitively, this shows that normality arises from sums of
small, independent disturbances of finite variance. Technically, the finite variance
assumption is essential for normality. Although the Central Limit Theorem provides
a powerful, general approximation, the quality of the approximation for a particular
```
situation still depends on the original (usually unknown) distribution.
```
3.4 Estimation Using Maximum Likelihood
The estimation problem starts with the desire to infer something meaningful from
data. For parametric estimation, the strategy is to postulate a model for the data and
then use the data to fit model parameters. This leads to two fundamental questions:
where to get the model and how to estimate the parameters? The first question is
best answered by the maxim: all models are wrong, some are useful. In other words,
choosing a model depends as much on the application as on the model itself. Think
about models as building different telescopes to view the sky. No one would ever
claim that the telescope generates the sky! It is same with data models. Models give
us multiple perspectives on the data that themselves are proxies for some deeper
underlying phenomenon.
Some categories of data may be more commonly studied using certain types of
models, but this is usually very domain-specific and ultimately depends on the aims
of the analysis. In some cases, there may be strong physical reasons behind choosing
a model. For example, one could postulate that the model is linear with some noise
as in the following:
```
Y = a X + 
```
which basically says that you, as the experimenter, dial in some value for X and
then read off something directly proportional to X as the measurement, Y , plus some
additive noise that you attribute to jitter in the apparatus. Then, the next step is to
estimate the paramater a in the model, given some postulated claim about the nature
of . How to compute the model parameters depends on the particular methodology.
The two broad rubrics are parametric and non-parametric estimation. In the former,
we assume we know the density function of the data and then try to derive the
112 3 Statistics
embedded parameters for it. In the latter, we claim only to know that the density
```
function is a member of a broad class of density functions and then use the data to
```
characterize a member of that class. Broadly speaking, the former consumes less
data than the latter, because there are fewer unknowns to compute from the data.
Let’s concentrate on parametric estimation for now. The tradition is to denote
the unknown parameter to be estimated as θ which is a member of a large space of
alternates, Θ. To judge between potential θ values, we need an objective function,
```
known as a risk function, L(θ, ˆθ), where ˆθ(x) is an estimate for the unknown θ that
```
is derived from the available data x. The most common and useful risk function is
the squared error loss,
```
L(θ, ˆθ) = (θ − ˆθ)2
```
Although neat, this is not practical because we need to know the unknown θ to
compute it. The other problem is because ˆθ is a function of the observed data, it is
also a random variable with its own probability density function. This leads to the
notion of the expected risk function,
```
R(θ, ˆθ) = Eθ(L(θ, ˆθ)) =
```
∫
```
L(θ, ˆθ(x)) f (x; θ)dx
```
In other words, given a fixed θ, integrate over the probability density function of the
```
data, f (x), to compute the risk. Plugging in for the squared error loss, we compute
```
the mean squared error,
```
Eθ(θ − ˆθ)2 =
```
∫
```
(θ − ˆθ)2 f (x; θ)dx
```
This has the important factorization into the bias,
```
bias = Eθ( ˆθ) − θ
```
```
with the corresponding variance, Vθ ( ˆθ) as in the following mean squared error (MSE):
```
```
Eθ(θ − ˆθ)2 = bias 2 + Vθ( ˆθ)
```
This is an important trade-off that we will return to repeatedly. The idea is the bias is
```
nonzero when the estimator ˆθ, integrated over all possible data, f (x), does not equal
```
the underlying target parameter θ. In some sense, the estimator misses the target, no
matter how much data is used. When the bias equals zero, the estimated is unbiased.
For fixed MSE, low bias implies high variance and vice-versa. This trade-off was
once not emphasized and instead much attention was paid to the smallest variance
```
of unbiased estimators (see Cramer-Rao bounds). In practice, understanding and
```
exploiting the trade-off between bias and variance and reducing the MSE is more
important.
3.4 Estimation Using Maximum Likelihood 113
With all this set up, we can now ask how bad can bad get by examining mini-
max risk,
```
Rmmx = infˆ
```
θ
sup
θ
```
R(θ, ˆθ)
```
where the inf is take over all estimators. Intuitively, this means if we found the
worst possible θ and swept over all possible parameter estimators ˆθ, and then took
the smallest possible risk we could find, we would have the minimax risk. Thus, an
estimator, ˆθmmx , is a minimax estimator if it achieves this feat,
sup
θ
```
R(θ, ˆθmmx) = infˆ
```
θ
sup
θ
```
R(θ, ˆθ)
```
```
In other words, even in the face of the worst θ (i.e., the supθ), ˆθmmx still achieves the
```
minimax risk. There is a greater theory that revolves around minimax estimators of
various kinds, but this is far beyond our scope here. The main thing to focus on is
that under certain technical but easily satisfiable conditions, the maximum likelihood
estimator is approximately minimax. Maximum likelihood is the subject of the next
section. Let’s get started with the simplest application: coin-flipping.
3.4.1 Setting Up the Coin Flipping Experiment
```
Suppose we have coin and want to estimate the probability of heads ( p) for it. We
```
model the distribution of heads and tails as a Bernoulli distribution with the following
probability mass function:
```
φ(x) = p x (1 − p) (1−x)
```
where x is the outcome, 1 for heads and 0 for tails. Note that maximum likelihood is
a parametric method that requires the specification of a particular model for which
we will compute embedded parameters. For n independent flips, we have the joint
density as the product of n of these functions as in,
```
φ(x) =
```
n∏
```
i=1
```
```
p xi (1 − p) (1−x i )
```
The following is the likelihood function,
```
L( p; x) =
```
n∏
```
i=1
```
```
p x i (1 − p)1−x i
```
114 3 Statistics
This is basically notation. We have just renamed the previous equation to emphasize
the p parameter, which is what we want to estimate.
The principle of maximum likelihood is to maximize the likelihood as the func-
tion of p after plugging in all of the x i data. We then call this maximizer ˆp which
is a function of the observed x i data, and as such, is a random variable with its
own distribution. This method therefore ingests data and an assumed model for the
probability density, and produces a function that estimates the embedded parameter
in the assumed probability density. Thus, maximum likelihood generates the func-
tions of data that we need in order to get at the underlying parameters of the model.
Note that there is no limit to the ways we can functionally manipulate the data we
have collected. The maximum likelihood principle gives us a systematic method for
constructing these functions subject to the assumed model. This is a point worth
```
emphasizing: the maximum likelihood principle yields functions as solutions the
```
same way solving differential equations yields functions as solutions. It is very, very
much harder to produce a function than to produce a value as a solution, even with
the assumption of a convenient probability density. Thus, the power of the principle
is that you can construct such functions subject to the model assumptions.
Simulating the Experiment. We need the following code to simulate coin flipping.
>>> from scipy.stats import bernoulli>>> p_true=1/2.0 # estimate this!
```
>>> fp=bernoulli(p_true) # create bernoulli random variate>>> xs = fp.rvs(100) # generate some samples
```
>>> print xs[:30] # see first 30 samples[0 1 0 1 1 0 0 1 1 1 0 1 1 1 0 1 1 0 1 1 0 1 0 0 1 1 0 1 0 1]
Now, we can write out the likelihood function using Sympy. Note that we give the
Sympy variables the positive=True attribute upon construction because this
eases Sympy’s internal simplification algorithms.
```
>>> import sympy>>> x,p,z=sympy.symbols(’x p z’, positive=True)
```
```
>>> phi=p**x*(1-p)**(1-x) # distribution function>>> L=np.prod([phi.subs(x,i) for i in xs]) # likelihood function
```
```
>>> print L # approx 0.5?p**57*(-p + 1)**43
```
Note that, once we plug in the data, the likelihood function is solely a function of
```
the unknown parameter ( p in this case). The following code uses calculus to find
```
the extrema of the likelihood function. Note that taking the log of L makes the
maximization problem tractable but doesn’t change the extrema.
```
>>> logL=sympy.expand_log(sympy.log(L))>>> sol,=sympy.solve(sympy.diff(logL,p),p)
```
>>> print sol57/100
3.4 Estimation Using Maximum Likelihood 115
Programming Tip
Note that sol,=sympy.solve statement includes a comma after the sol
variable. This is because the solve function returns a list containing a sin-
gle element. Using this assignment unpacks that single element into the sol
variable directly. This is another one of the many small elegancies of Python.
The following code generates Fig. 3.3.
```
fig,ax=subplots()x=np.linspace(0,1,100)
```
```
ax.plot(x,map(sympy.lambdify(p,logJ,’numpy’),x),’k-’,lw=3)ax.plot(sol,logJ.subs(p,sol),’o’,
```
```
color=’gray’,ms=15,label=’Estimated’)ax.plot(p_true,logJ.subs(p,p_true),’s’,
```
```
color=’k’,ms=15,label=’Actual’)ax.set_xlabel(’$p$’,fontsize=18)
```
```
ax.set_ylabel(’Likelihood’,fontsize=18)ax.set_title(’Estimate not equal to true value’,fontsize=18)
```
```
ax.legend(loc=0)
```
Programming Tip
```
In the prior code, we use the lambdify function in lambdify(p,logJ,
```
```
’ numpy’) to take a Sympy expression and convert it into a Numpy version
```
that is easier to compute. The lambdify function has an extra argument
where you can specify the function space that it should use to convert the
expression. In the above this is set to Numpy.
Fig. 3.3 Maximum likelihood estimate versus true parameter. Note that the estimate is slightly off
from the true value. This is a consequence of the fact that the estimator is a function of the data and
lacks knowledge of the true underlying value
116 3 Statistics
```
Figure 3.3 shows that our estimator ˆp (circle) is not equal to the true value of
```
```
p (square), despite being the maximum of the likelihood function. This may sound
```
```
disturbing, but keep in mind this estimate is a function of the random data; and since
```
that data can change, the ultimate estimate can likewise change. I invite you to run this
code in the corresponding IPython notebook a few times to observe this. Remember
that the estimator is a function of the data and is thus also a random variable, just
like the data is. This means it has its own probability distribution with corresponding
mean and variance. So, what we are observing is a consequence of that variance.
Figure 3.4 shows what happens when you run many thousands of coin experi-
ments and compute the maximum likelihood estimate for each experiment, given a
particular number of samples per experiment. This simulation gives us a histogram
of the maximum likelihood estimates, which is an approximation of the probability
distribution of the ˆp estimator itself. This figure shows that the sample mean of the
```
estimator (μ = 1n∑ ˆpi ) is pretty close to the true value, but looks can be deceiving.
```
The only way to know for sure is to check if the estimator is unbiased, namely, if
```
E( ˆp) = p
```
Because this problem is simple, we can solve for this in general noting that the terms
above are either p, if x i = 1 or 1 − p if x i = 0. This means that we can write
```
L( p|x) = p
```
∑ni=1 x i
```
(1 − p)n−
```
∑ni=1 x i
with corresponding logarithm as
```
J = log(L( p|x)) = log( p)
```
n∑
```
i=1
```
```
x i + log(1 − p)
```
```
(
```
n −
n∑
```
i=1
```
x i
```
)
```
Fig. 3.4 Histogram of maximum likelihood estimates. The title shows the estimated mean and
standard deviation of the samples
3.4 Estimation Using Maximum Likelihood 117
Taking the derivative of this gives:
d J
```
dp =
```
1
p
n∑
```
i=1
```
```
x i + (n −
```
∑n
```
i=1 x i )
```
p − 1
and solving this for p leads to
ˆp = 1n
n∑
```
i=1
```
x i
This is our estimator for p. Up until now, we have been using Sympy to solve for
this based on the data x i but now that we have it analytically we don’t have to solve
for it each time. To check if this estimator is biased, we compute its expectation:
E
```
(
```
ˆp
```
)
```
= 1n
n∑
i
```
E(x i ) = 1n nE(x i )
```
by linearity of the expectation and where
```
E(x i ) = p
```
Therefore,
E
```
(
```
ˆp
```
)
```
= p
This means that the estimator is unbiased. Similarly,
E
```
(
```
ˆp2
```
)
```
= 1n2 E
⎡
⎣
```
( n∑
```
```
i=1
```
x i
```
)2⎤
```
⎦
and where
E
```
(
```
x2i
```
)
```
= p
and by the independence assumption,
E
```
(
```
x i x j
```
)
```
```
= E(x i )E(x j ) = p2
```
Thus,
E
```
(
```
ˆp2
```
)
```
=
```
( 1
```
n2
```
)
```
n
[
```
p + (n − 1) p2
```
]
118 3 Statistics
So, the variance of the estimator, ˆp, is the following:
```
V( ˆp) = E
```
```
(
```
ˆp2
```
)
```
− E
```
(
```
ˆp
```
)2
```
```
= p(1 − p)n
```
Note that the n in the denominator means that the variance asymptotically goes to zero
```
as n increases (i.e., we consider more and more samples). This is good news because
```
it means that more and more coin flips lead to a better estimate of the underlying p.
Unfortunately, this formula for the variance is practically useless because we
need p to compute it and p is the parameter we are trying to estimate in the first
place! However, this is where the plug-in principle2 saves the day. It turns out in this
situation, you can simply substitute the maximum likelihood estimator, ˆp, for the p
```
in the above equation to obtain the asymptotic variance for V( ˆp). The fact that this
```
works is guaranteed by the asymptotic theory of maximum likelihood estimators.
```
Nevertheless, looking at V( ˆp)2 , we can immediately notice that if p = 0, then
```
there is no estimator variance because the outcomes are guaranteed to be tails. Also,
for any n, the maximum of this variance happens at p = 1/2. This is our worst case
scenario and the only way to compensate is with larger n.
All we have computed is the mean and variance of the estimator. In general, this
is insufficient to characterize the underlying probability density of ˆp, except if we
somehow knew that ˆp were normally distributed. This is where the powerful Central
Limit Theorem we discussed in Sect. 3.3.4 comes in. The form of the estimator, which
is just a sample mean, implies that we can apply this theorem and conclude that ˆp is
asymptotically normally distributed. However, it doesn’t quantify how many samples
n we need. In our simulation this is no problem because we can generate as much
data as we like, but in the real world, with a costly experiment, each sample may be
precious. 3
In the following, we won’t apply the Central Limit Theorem and instead proceed
analytically.
Probability Density for the Estimator. To write out the full density for ˆp, we first
have to ask what is the probability that the estimator will equal a specific value and
the tally up all the ways that could happen with their corresponding probabilities.
For example, what is the probability that
ˆp = 1n
n∑
```
i=1
```
x i = 0
2 This is also known as the invariance property of maximum likelihood estimators. It basically states
```
that the maximum likelihood estimator of any function, say, h(θ), is the same h with the maximum
```
```
likelihood estimator for θ substituted in for θ; namely, h(θM L ).
```
3 It turns out that the central limit theorem augmented with an Edgeworth expansion tells us that
convergence is regulated by the skewness of the distribution [1]. In other words, the more symmetric
the distribution, the faster it converges to the normal distribution according to the central limit
theorem.
3.4 Estimation Using Maximum Likelihood 119
This can only happen one way: when x i = 0 ∀i. The probability of this happening
can be computed from the density
```
f (x, p) =
```
n∏
```
i=1
```
```
(
```
```
p x i (1 − p)1−x i
```
```
)
```
f
```
( n∑
```
```
i=1
```
x i = 0, p
```
)
```
```
= (1 − p)n
```
```
Likewise, if {x i } has only one nonzero element, then
```
f
```
( n∑
```
```
i=1
```
x i = 1, p
```
)
```
= np
n−1∏
```
i=1
```
```
(1 − p)
```
where the n comes from the n ways to pick one element from the n elements x i .
Continuing this way, we can construct the entire density as
f
```
( n∑
```
```
i=1
```
x i = k, p
```
)
```
=
```
(n
```
k
```
)
```
```
p k (1 − p)n−k
```
where the first term on the right is the binomial coefficient of n things taken k at a
time. This is the binomial distribution and it’s not the density for ˆp, but rather for
n ˆp. We’ll leave this as-is because it’s easier to work with below. We just have to
remember to keep track of the n factor.
Confidence Intervals Now that we have the full density for ˆp, we are ready to ask
some meaningful questions. For example, what is the probability the estimator is
within  fraction of the true value of p?
P
```
(
```
| ˆp − p| ≤  p
```
)
```
More concretely, we want to know how often the estimated ˆp is trapped within  of
the actual value. That is, suppose we ran the experiment 1000 times to generate 1000
different estimates of ˆp. What percentage of the 1000 so-computed values are trapped
within  of the underlying value. Rewriting the above equation as the following,
P
```
(
```
p −  p < ˆp < p +  p
```
)
```
= P
```
(
```
np − n p <
n∑
```
i=1
```
x i < np + n p
```
)
```
```
Let’s plug in some live numbers here for our worst case scenario (i.e., highest variance
```
```
scenario) where p = 1/2. Then, if  = 1/100, we have
```
120 3 Statistics
P
```
(
```
99n
100 <
n∑
```
i=1
```
x i < 101n100
```
)
```
Since the sum in integer-valued, we need n > 100 to even compute this. Thus, if
```
n = 101 we have,
```
P
```
(
```
9999
200 <
101∑
```
i=1
```
x i < 10201200
```
)
```
= f
```
( 101∑
```
```
i=1
```
x i = 50, p
```
)
```
. . .
=
```
(101
```
50
```
)
```
```
(1/2)50(1 − 1/2)101−50 = 0.079
```
This means that in the worst-case scenario for p = 1/2, given n = 101 trials, we
will only get within 1 % of the actual p = 1/2 about 8 % of the time. If you feel
disappointed, that only means you’ve been paying attention. What if the coin was
really heavy and it was hard work to repeat this 101 times?
Let’s come at this another way: given I could only flip the coin 100 times, how
```
close could I come to the true underlying value with high probability (say, 95 %)? In
```
this case, instead of picking a value for , we are solving for . Plugging in gives,
P
```
(
```
50 − 50 <
100∑
```
i=1
```
x i < 50 + 50
```
)
```
= 0.95
which we have to solve for . Fortunately, all the tools we need to solve for this are
```
already in Scipy (Fig. 3.5).
```
>>> from scipy.stats import binom>>> # n=100, p = 0.5, distribution of the estimator phat
```
>>> b=binom(100,.5)>>> # symmetric sum the probability around the mean
```
```
>>> g = lambda i:b.pmf(np.arange(-i,i)+50).sum()>>> print g(10) # approx 0.95
```
0.953955933071
Fig. 3.5 Probability mass
```
function for ˆp. The two
```
vertical lines form the
confidence interval
3.4 Estimation Using Maximum Likelihood 121
The two vertical lines in the plot show how far out from the mean we have to go to
accumulate 95 % of the probability. Now, we can solve this as
50 + 50 = 60
which makes  = 1/5 or 20 %. So, flipping 100 times means I can only get within
```
20 % of the real p 95 % of the time in the worst case scenario (i.e., p = 1/2). The
```
following code verifies the situation.
```
>>> from scipy.stats import bernoulli>>> b=bernoulli(0.5) # coin distribution
```
```
>>> xs = b.rvs(100) # flip it 100 times>>> phat = np.mean(xs) # estimated p
```
```
>>> print abs(phat-0.5) < 0.5*0.20 # make it w/in interval?True
```
Let’s keep doing this and see if we can get within this interval 95 % of the time.
```
>>> out=[]>>> b=bernoulli(0.5) # coin distribution
```
```
>>> for i in range(500): # number of tries... xs = b.rvs(100) # flip it 100 times
```
```
... phat = np.mean(xs) # estimated p... out.append(abs(phat-0.5) < 0.5*0.20 ) # within 20% ?
```
...>>> # percentage of tries w/in 20\,% interval
```
>>> print 100*np.mean(out)97.4
```
Well, that seems to work! Now we have a way to get at the quality of the estimator, ˆp.
Maximum Likelihood Estimator Without Calculus The prior example showed
how we can use calculus to compute the maximum likelihood estimator. It’s important
to emphasize that the maximum likelihood principle does not depend on calculus
and extends to more general situations where calculus is impossible. For example,
let X be uniformly distributed in the interval [0, θ]. Given n measurements of X, the
likelihood function is the following:
```
L(θ) =
```
n∏
```
i=1
```
1
θ =
1
θn
where each x i ∈ [0, θ]. Note that the slope of this function is not zero anywhere so
the usual calculus approach is not going to work here. Because the likelihood is the
product of the individual uniform densities, if any of the x i values were outside of the
proposed [0, θ] interval, then the likelihood would go to zero, because the uniform
density is zero outside of the [0, θ]. Naturally, this is no good for maximization.
Thus, observing that the likelihood function is strictly decreasing with increasing θ,
we conclude that the value for θ that maximizes the likelihood is the maximum of
the x i values. To summarize, the maximum likelihood estimator is the following:
θM L = maxi x i
122 3 Statistics
As always, we want the distribution of this estimator to judge its performance. In
this case, this is pretty straightforward. The cumulative density function for the max
```
function is the following:
```
P
```
(
```
ˆθM L < v
```
)
```
```
= P(x0 ≤ v ∧ x1 ≤ v . . . ∧ x n ≤ v)
```
and since all the x i are uniformly distributed in [0, θ], we have
P
```
(
```
ˆθM L < v
```
)
```
=
```
( v
```
θ
```
)n
```
So, the probability density function is then,
```
fˆθM L (θM L ) = nθn−1M L θ−n
```
```
Then, we can compute the E(θM L ) = (θn)/(n + 1) with corresponding variance as
```
```
V(θM L ) = (θ2n)/(n + 1)2/(n + 2).
```
For a quick sanity check, we can write the following simulation for θ = 1 as in
the following:
```
>>> from scipy import stats>>> rv = stats.uniform(0,1) # define uniform random variable
```
```
>>> mle=rv.rvs((100,500)).max(0) # max along row-dimension>>> print mean(mle) # approx n/(n+1) = 100/101 ˜= 0.99
```
```
0.989942138048>>> print var(mle) #approx n/(n+1)**2/(n+2) ˜= 9.61E-5
```
9.95762009884e-05
Programming Tip
```
The max(0) suffix on for the mle computation takes the maximum of the
```
```
so-computed array along the row (axis=0) dimension.
```
```
You can also plot hist(mle) to see the histogram of the simulated maximum
```
likelihood estimates and match it up against the probability density function we
derived above.
In this section, we explored the concept of maximum likelihood estimation using a
coin flipping experiment both analytically and numerically with the scientific Python
stack. We also explored the case when calculus is not workable for maximum likeli-
hood estimation. There are two key points to remember. First, maximum likelihood
estimation produces a function of the data that is itself a random variable, with its
own probability distribution. We can get at the quality of the so-derived estimators
by examining the confidence intervals around the estimated values using the prob-
ability distributions associated with the estimators themselves. Second, maximum
likelihood estimation applies even in situations where using basic calculus is not
applicable [2].
3.4 Estimation Using Maximum Likelihood 123
3.4.2 Delta Method
The Central Limit Theorem provides a way to get at the distribution of a random
variable. However, sometimes we are more interested in a function of the random
variable. In order to extend and generalize the central limit theorem in this way,
we need the Taylor series expansion. Recall that the Taylor series expansion is an
approximation of a function of the following form,
```
Tr (x) =
```
r∑
```
i=0
```
```
g(i) (a)
```
```
i! (x − a)
```
i
this basically says that a function g can be adequately approximated about a point
a using a polynomial based on its derivatives evaluated at a. Before we state the
general theorem, let’s examine an example to understand how the mechanics work.
```
Example Suppose that X is a random variable with E(X) = μ = 0. Furthermore,
```
```
supposedly have a suitable function g and we want the distribution of g(X). Applying
```
the Taylor series expansion, we obtain the following,
```
g(X) ≈ g(μ) + g′(μ)(X − μ)
```
```
If we use g(X) as an estimator for g(μ), then we can say that we approximately have
```
the following
```
E(g(X)) = g(μ)
```
```
V(g(X)) = (g′(μ))2V(X)
```
Concretely, suppose we want to estimate the odds, p1− p . For example, if p = 2/3,
then we say that the odds is 2:1 meaning that the odds of the one outcome are twice
```
as likely as the odds of the other outcome. Thus, we have g( p) = p1− p and we want
```
```
to find V(g( ˆp)). In our coin-flipping problem, we have the estimator ˆp = 1n∑ X k
```
from the Bernoulli-distributed data X k individual coin-flips. Thus,
```
E( ˆp) = p
```
```
V( ˆp) = p(1 − p)n
```
124 3 Statistics
```
Now, g′( p) = 1/(1 − p)2 , so we have,
```
```
V(g( ˆp)) = (g′( p))2V( ˆp)
```
=
```
( 1
```
```
(1 − p)2
```
```
)2 p(1 − p)
```
n
```
= pn(1 − p)3
```
```
which is an approximation of the variance of the estimator g( ˆp). Let’s simulate this
```
and see how it agrees.
>>> from scipy import stats>>> # compute MLE estimates
```
>>> d=stats.bernoulli(0.1).rvs((10,5000)).mean(0)>>> # avoid divide-by-zero
```
```
>>> d=d[np.logical_not(np.isclose(d,1))]>>> # compute odds ratio
```
```
>>> odds = d/(1-d)>>> print ’odds ratio=’,np.mean(odds),’var=’,np.var(odds)
```
odds ratio= 0.122892063492 var= 0.0179795009221
The first number above is the mean of the simulated odds ratio and the second is
the variance of the estimate. According to the variance estimate above, we have
```
V(g(1/10)) ≈ 0.0137, which is not too bad for this approximation. Recall we want
```
to estimate the odds from the ˆp. The code above takes 5000 estimates of the ˆp to
```
estimate V(g). The odds ratio for p = 1/10 is 1/9 ≈ 0.111.
```
Programming Tip
The code above uses the np.isclose function to identify the ones from the
simulation and the np.logical_not removes these elements from the data
because the odds ratio has a zero in the denominator for these values.
Let’s try this again with a probability of heads of 0.5 instead of 0.3.
```
>>> from scipy import stats>>> d=stats.bernoulli(.5).rvs((10,5000)).mean(0)
```
```
>>> d=d[np.logical_not(np.isclose(d,1))]>>> print ’odds ratio=’,np.mean(d),’var=’,np.var(d)
```
odds ratio= 0.499379627777 var= 0.0245123227629
The odds ratio is this case is equal to one, which is not close to what was reported.
```
According to our approximation, we have V(g) = 0.4, which does not look like
```
what our simulation just reported. This is because the approximation is best when
```
the odds ratio is nearly linear and worse otherwise (Fig. 3.6).
```
3.5 Hypothesis Testing and P-Values 125
Fig. 3.6 The odds ratio is
close to linear for small
values but becomes
unbounded as p approaches
one. The delta method is
more effective for small
underlying values of p,
where the linear
approximation is better
3.5 Hypothesis Testing and P-Values
It is sometimes very difficult to unequivocally attribute outcomes to causal factors.
For example, did your experiment generate the outcome you were hoping for or not?
Maybe something did happen, but the effect is not pronounced enough to separate it
from inescapable measurement errors or other factors in the ambient environment?
Hypothesis testing is a powerful statistical method to address these questions. Let’s
begin by again considering our coin-tossing experiment with unknown parameter
p. Recall that the individual coin-flips are Bernoulli distributed. The first step is to
establish separate hypotheses. First, H0 is the so-called null hypothesis. In our case
this can be
```
H0 : θ < 12
```
and the alternative hypothesis is then
```
H1 : θ ≥ 12
```
With this set up, the question now boils down to figuring out which hypothesis the
data is most consistent with. To choose between these, we need a statistical test
```
that is a function, G, of the sample set Xn = {X i }n into the real line, where X i is
```
```
the heads or tails outcome (X i ∈ {0, 1}). In other words, we compute G(Xn ) and
```
```
check if it exceeds a threshold c. If not, then we declare H0 (otherwise, declare H1 ).
```
Notationally, this is the following:
```
G(Xn ) < c ⇒ H0
```
```
G(Xn ) ≥ c ⇒ H1
```
126 3 Statistics
Table 3.1 Truth table for hypotheses testing
Declare H0 Declare H1
```
H0 True Correct False positive (Type I error)
```
```
H1 True False negative (Type II error) Correct (true-detect)
```
In summary, we have the observed data Xn and a function G that maps that data
onto the real line. Then, using the constant c as a threshold, the inequality effectively
divides the real line into two parts, one corresponding to each of the hypotheses.
Whatever this test G is, it will make mistakes of two types—false negatives and
false positives. The false positives arise from the case where we declare H0 when
the test says we should declare H1 . This is summarized in the Table 3.1.
```
For this example, here are the false positives (aka false alarms):
```
```
PFA = P
```
```
(
```
```
G(Xn ) > c | θ ≤ 12
```
```
)
```
Or, equivalently,
```
PFA = P (G(Xn ) > c | H0)
```
Likewise, the other error is a false negative, which we can write analogously as
```
PFN = P (G(Xn ) < c|H1)
```
By choosing some acceptable values for either of these errors, we can solve for the
other one. The practice is usually to pick a value of PFA and then find the correspond-
ing value of PFN. Note that it is traditional in engineering to speak about detection
probability, which is defined as
```
PD = 1 − PFN = P (G(Xn ) > c | H1)
```
In other words, this is the probability of declaring H1 when the test exceeds the
threshold. This is otherwise known as the probability of a true detection or true-
detect.
3.5.1 Back to the Coin Flipping Example
In our previous maximum likelihood discussion, we wanted to derive an estimator for
the value of the probability of heads for the coin flipping experiment. For hypthesis
testing, we want to ask a softer question: is the probability of heads greater or less
than 1/2 ? As we just established, this leads to the two hypotheses:
3.5 Hypothesis Testing and P-Values 127
```
H0 : θ < 12
```
versus,
```
H1 : θ > 12
```
Let’s assume we have five observations. Now we need the G function and a threshold
c to help pick between the two hypotheses. Let’s count the number of heads observed
in five observations as our criterion. Thus, we have
```
G(X5) :=
```
5∑
```
i=1
```
X i
and, suppose further that we pick H1 only if exactly five out of five observations are
heads. We’ll call this the all-heads test.
Now, because all of the X i are random variables, so is G and we must find the
corresponding probability mass function for G. Assuming the individual coin tosses
are independent, the probability of five heads is θ5 . This means that the probability
```
of rejecting the H0 hypothesis (and choosing H1 , because there are only two choices
```
```
here) based on the unknown underlying probability is θ5 . In the parlance, this is
```
known and the power function as in denoted by β as in
```
β(θ) = θ5
```
Let’s get a quick plot this in Fig. 3.7.
Now, we have the following false alarm probability,
```
PFA = P(G(Xn ) = 5|H0) = P(θ5|H0)
```
Notice that this is a function of θ, which means there are many false alarm probability
values that correspond to this test. To be on the conservative side, we’ll pick the
```
supremum (i.e., maximum) of this function, which is known as the size of the test,
```
traditionally denoted by α,
Fig. 3.7 Power function for
the all-heads test. The dark
circle indicates the value of
the function indicating α
128 3 Statistics
α = sup
θ∈Θ0
```
β(θ)
```
```
with domain Θ0 = {θ < 1/2} which in our case is
```
α = sup
θ< 12
θ5 =
```
( 1
```
2
```
)5
```
= 0.03125
Likewise, for the detection probability,
```
PD (θ) = P(θ5|H1)
```
which is again a function of the parameter θ. The problem with this test is that the
PD is pretty low for most of the domain of θ. For instance, values in the nineties for
PD only happen when θ > 0.98. In other words, if the coin produces heads 98 times
out of 100, then we can detect H1 reliably. Ideally, we want a test that is zero for the
```
domain corresponding to H0 (i.e., Θ0 ) and equal to one otherwise. Unfortunately,
```
even if we increase the length of the observed sequence, we cannot escape this effect
with this test. You can try plotting θn for larger and larger values of n to see this.
Majority Vote Test. Due to the problems with the detection probability in the all-
heads test, maybe we can think of another test that will have the performance we
want? Suppose we reject H0 if the majority of the observations are heads. Then,
using the same reasoning as above, we have
```
β(θ) =
```
5∑
```
k=3
```
```
(5
```
k
```
)
```
```
θk (1 − θ)5−k
```
Figure 3.8 shows the power function for both the majority vote and the all-heads
tests.
In this case, the new test has size
α = sup
θ< 12
```
θ5 + 5θ4 (−θ + 1) + 10θ3 (−θ + 1)2 = 12
```
Fig. 3.8 Compares the
power function for the
all-heads test with that of the
majority-vote test
3.5 Hypothesis Testing and P-Values 129
As before we only get to upwards of 90 % for detection probability only when the
underlying parameter θ > 0.75. Let’s see what happens when we consider more than
five samples. For example, let’s suppose that we have n = 100 samples and we want
to vary the threshold for the majority vote test. For example, let’s have a new test
where we declare H1 when k = 60 out of the 100 trials turns out to be heads. What
is the β function in this case?
```
β(θ) =
```
100∑
```
k=60
```
```
(100
```
k
```
)
```
```
θk (1 − θ)100−k
```
This is too complicated to write by hand, but the statistics module in Sympy has all
the tools we need to compute this.
```
>>> from sympy.stats import P, Binomial>>> theta = S.symbols(’theta’,real=True)
```
```
>>> X = Binomial(’x’,100,theta)>>> beta_function = P(X>60)
```
```
>>> print beta_function.subs(theta,0.5) # alpha0.0176001001088524
```
```
>>> print beta_function.subs(theta,0.70)0.979011423996075
```
These results are much better than before because the β function is much steeper.
If we declare H1 when we observe 60 out of 100 trials are heads, then we wrongly
declare heads approximately 1.8 % of the time. Otherwise, if it happens that the true
value for p > 0.7, we will conclude correctly approximately 97 % of the time. A
quick simulation can sanity check these results as shown below:
```
>>> from scipy import stats>>> rv=stats.bernoulli(0.5) # true p = 0.5
```
```
>>> # number of false alarms ˜ 0.018>>> print sum(rv.rvs((1000,100)).sum(axis=1)>60)/1000.
```
0.025
The above code is pretty dense so let’s unpack it. In the first line, we use the
scipy.stats module to define the Bernoulli random variable for the coin flip.
Then, we use the rvs method of the variable to generate 1000 trials of the experi-
ment where each trial consists of 100 coin flips. This generates a 1000 × 100 matrix
where the rows are the individual trials and the columns are the outcomes of each
```
respective set of 100 coin flips. The sum(axis=1) part computes the sum across
```
the columns. Because the values of the embedded matrix are only 1 or 0 this gives
us the count of flips that are heads per row. The next >60 part computes the boolean
1000-long vector of values that are bigger than 60. The final sum adds these up.
Again, because the entries in the array are True or False the sum computes the
count of times the number of heads has exceeded 60 per 100 coin flips in each of
1000 trials. Then, dividing this number by 1000 gives a quick approximation of false
alarm probability we computed above for this case where the true value of p = 0.5.
130 3 Statistics
3.5.2 Receiver Operating Characteristic
Because the majority vote test is a binary test, we can compute the Receiver Operating
```
Characteristic (ROC) which is the graph of the (PFA, PD ). The term comes from radar
```
systems but is a very general method for consolidating all of these issues into a single
graph. Let’s consider a typical signal processing example with two hypotheses. In
H0 , there is noise but no signal present at the receiver,
```
H0 : X = 
```
```
where  ∼ N (0, σ2) represents additive noise. In the alternative hypothesis, there is
```
a deterministic signal at the receiver,
```
H1 : X = μ + 
```
Again, the problem is to choose between these two hypotheses. For H0 , we have
```
X ∼ N (0, σ2) and for H1 , we have X ∼ N (μ, σ2). Recall that we only observe
```
values for x and must pick either H0 or H1 from these observations. Thus, we need
a threshold, c, to compare x against in order to distinguish the two hypotheses.
Figure 3.9 shows the probability density functions under each of the hypotheses.
The dark vertical line is the threshold c. The gray shaded area is the probability of
detection, PD and the shaded area is the probability of false alarm, PFA. The test
evaluates every observation of x and concludes H0 if x < c and H1 otherwise.
Programming Tip
The shading shown in Fig. 3.9 comes from Matplotlib’s fill_between
function. This function has a where keyword argument to specify which part
of the plot to apply shading with specified color keyword argument. Note
there is also a fill_betweenx function that fills horizontally. The text
```
function can place formatted text anywhere in the plot and can utilize basic
```
LATEX formatting. See the IPython notebook corresponding to this section for
the source code.
As we slide the threshold left and right along the horizontal axis, we naturally
change the corresponding areas under each of the curves shown in Fig. 3.9 and thereby
change the values of PD and PFA. The contour that emerges from sweeping the
threshold this way is the ROC as shown in Fig. 3.10. This figure also shows the
diagonal line which corresponds to making decisions based on the flip of a fair coin.
Any meaningful test must do better than coin flipping so the more the ROC bows
up to the top left corner of the graph, the better. Sometimes ROCs are quantified into
```
a single number called the area under the curve (AUC), which varies from 0.5 to
```
1.0 as shown. In our example, what separates the two probability density functions
is the value of μ. In a real situation, this would be determined by signal processing
3.5 Hypothesis Testing and P-Values 131
Fig. 3.9 The two density functions for the H0 and H1 hypotheses. The shaded gray area is the
detection probability and the shaded blue area is the probability of false alarm. The vertical line is
the decision threshold
methods that include many complicated trade-offs. The key idea is that whatever
those trade-offs are, the test itself boils down to the separation between these two
density functions—good tests separate the two density functions and bad tests do
not. Indeed, when there is no separation, we arrive at the diagonal-line coin-flipping
situation we just discussed.
What values for PD and PFA are considered acceptable depends on the application.
For example, suppose you are testing for a fatal disease. It could be that you are
willing to except a relatively high PFA value if that corresponds to a good PD because
the test is relatively cheap to administer compared to the alternative of missing a
detection. On the other hand, may be a false alarm triggers an expensive response, so
Fig. 3.10 The Receiver
Operating Characteristic
```
(ROC) corresponding to
```
Fig. 3.9
132 3 Statistics
that minimizing these alarms is more important than potentially missing a detection.
These trade-offs can only be determined by the application and design factors.
3.5.3 P-Values
There are a lot of moving parts in hypothesis testing. What we need is a way to
consolidate the findings. The idea is that we want to find the minimum level at
which the test rejects H0 . Thus, the p-value is the probability, under H0 , that the test-
statistic is at least as extreme as what was actually observed. Informally, this means
that smaller values imply that H0 should be rejected, although this doesn’t mean that
large values imply that H0 should be retained. This is because a large p-value can
arise from either H0 being true or the test having low statistical power.
```
If H0 is true, the p-value is uniformly distributed in the interval (0, 1). If H1 is
```
true, the distribution of the p-value will concentrate closer to zero. For continuous
distributions, this can be proven rigorously and implies that if we reject H0 when
the corresponding p-value is less than α, then the probability of a false alarm is α.
```
Perhaps it helps to formalize this a bit before computing it. Suppose τ (X) is a test
```
statistic that rejects H0 as it gets bigger. Then, for each sample x, corresponding to
the data we actually have on-hand, we define
```
p(x) = sup
```
θ∈Θ0
```
Pθ(τ (X) > τ (x))
```
```
This equation states that the supremum (i.e., maximum) probability that the test
```
```
statistic, τ (X), exceeds the value for the test statistic on this particular data (τ (x))
```
over the domain Θ0 is defined as the p-value. Thus, this embodies a worst-case
scenario over all values of θ.
Here’s one way to think about this. Suppose you rejected H0 , and someone says
that you just got lucky and somehow just drew data that happened to correspond to
a rejection of H0 . What p-values provide is a way to address this by capturing the
odds of just a favorable data-draw. Thus, suppose that your p-value is 0.05. Then,
what you are showing is that the odds of just drawing that data sample, given H0 is
in force, is just 5 %. This means that there’s a 5 % chance that you somehow lucked
out and got a favorable draw of data.
Let’s make this concrete with an example. Given, the majority-vote rule above,
suppose we actually do observe three of five heads. Given the H0 , the probability of
observing this event is the following:
```
p(x) = sup
```
θ∈Θ0
5∑
```
k=3
```
```
(5
```
k
```
)
```
```
θk (1 − θ)5−k = 12
```
3.5 Hypothesis Testing and P-Values 133
For the all-heads test, the corresponding computation is the following:
```
p(x) = sup
```
θ∈Θ0
θ5 = 12 5 = 0.03125
From just looking at these p-values, you might get the feeling that the second test
```
is better, but we still have the same detection probability issues we discussed above;
```
so, p-values help in summarizing some aspects of our hypothesis testing, but they do
not summarize all the salient aspects of the entire situation.
3.5.4 Test Statistics
As we have seen, it is difficult to derive good test statistics for hypothesis testing
without a systematic process. The Neyman-Pearson Test is derived from fixing a
```
false-alarm value (α) and then maximizing the detection probability. This results in
```
the Neyman-Pearson Test,
```
L(x) = f X|H1 (x)f
```
```
X|H0 (x)
```
H1
≷
H0
γ
where L is the likelihood ratio and where the threshold γ is chosen such that
∫
```
x:L(x)>γ
```
```
f X|H0 (x)dx = α
```
The Neyman-Pearson Test is one of a family of tests that use the likelihood ratio.
Example Suppose we have a receiver and we want to distinguish whether just noise
```
(H0 ) or signal pluse noise (H1 ) is received. For the noise-only case, we have x ∼
```
```
N (0, 1) and for the signal pluse noise case we have x ∼ N (1, 1). In other words, the
```
mean of the distribution shifts in the presence of the signal. This is a very common
problem in signal processing and communications. The Neyman-Pearson Test then
boils down to the following,
```
L(x) = e− 12 +x
```
H1
≷
H0
γ
Now we have to find the threshold γ that solves the maximization problem that char-
acterizes the Neyman-Pearson Test. Taking the natural logarithm and re-arranging
gives,
x
H1
≷
H0
1
2 + log γ
134 3 Statistics
The next step is find γ corresponding to the desired α by computing it from the
following,
∫ ∞
1/2+log γ
```
f X|H0 (x)dx = α
```
For example, taking α = 1/100, gives γ ≈ 6.21. To summarize the test in this case,
we have,
x
H1
≷
H0
2.32
Thus, if we measure X and see that its value exceeds the threshold above, we declare
H1 and otherwise declare H0 . The following code shows how to solve this example
using Sympy and Scipy. First, we set up the likelihood ratio,
>>> import sympy as S>>> from sympy import stats
```
>>> s = stats.Normal(’s’,1,1) # signal+noise>>> n = stats.Normal(’n’,0,1) # noise
```
```
>>> x = S.symbols(’x’,real=True)>>> L = stats.density(s)(x)/stats.density(n)(x)
```
Next, to find the γ value,
```
>>> g = S.symbols(’g’,positive=True) # define gamma>>> v=S.integrate(stats.density(n)(x),
```
```
... (x,S.Rational(1,2)+S.log(g),S.oo))
```
Programming Tip
Providing additional information regarding the Sympy variable by using the
keyword argument positive=True helps the internal simplification algo-
rithms work faster and better. This is especially useful when dealing with
complicated integrals that involve special functions. Furthermore, note that
we used the Rational function to define the 1/2 fraction, which is another
way of providing hints to Sympy. Otherwise, it’s possible that the floating-point
representation of the fraction could disguise the simple fraction and thereby
miss internal simplification opportunities.
We want to solve for g in the above expression. Sympy has some built-in numerical
solvers as in the following,
```
>>> print S.nsolve(v-0.01,3.0) # approx 6.216.21116124253284
```
Note that in this situation it is better to use the numerical solvers because Sympy
solve may grind along for a long time to resolve this.
3.5 Hypothesis Testing and P-Values 135
Generalized Likelihood Ratio Test. The likelihood ratio test can be generalized
using the following statistic,
```
Λ(x) = supθ∈Θ0 L(θ)sup
```
```
θ∈Θ L(θ)
```
```
= L(
```
```
ˆθ0)
```
```
L( ˆθ)
```
```
where ˆθ0 maximizes L(θ) subject to θ ∈ Θ0 and ˆθ is the maximum likelihood
```
estimator. The intuition behind this generalization of the Likelihood Ratio Test is
that the denomimator is the usual maximum likelihood estimator and the numerator
```
is the maximum likelihood estimator, but over a restricted domain (Θ0 ). This means
```
that the ratio is always less than unity because the maximum likelihood estimator
over the entire space will always be at least as maximal as that over the more restricted
space. When this Λ ratio gets small enough, it means that the maximum likelihood
```
estimator over the entire domain (Θ) is larger which means that it is safe to reject the
```
null hypothesis H0 . The tricky part is that the statistical distribution of Λ is usually
eye-wateringly difficult. Fortunately, Wilks Theorem says that with sufficiently large
n, the distribution of −2 log Λ is approximately chi-square with r − r0 degrees of
freedom, where r is the number of free parameters for Θ and r0 is the number of
free parameters in Θ0 . With this result, if we want an approximate test at level α,
```
we can reject H0 when −2 log Λ ≥ χ2r−r0 (α) where χ2r−r0 (α) denotes the 1 − α
```
quantile of the χ2r−r0 chi-square distribution. However, the problem with this result is
that there is no definite way of knowing how big n should be. The advantage of this
generalized likelihood ratio test is that it can test multiple hypotheses simultaneously,
as illustrated in the following example.
Example Let’s return to our coin-flipping example, except now we have three dif-
ferent coins. The likelihood function is then,
```
L( p1, p2, p3) = binom(k1; n1, p1)binom(k2; n2, p2)binom(k3; n3, p3)
```
where binom is the binomial distribution with the given parameters. For example,
```
binom(k; n, p) =
```
n∑
```
k=0
```
```
(n
```
k
```
)
```
```
p k (1 − p)n−k
```
The null hypothesis is that all three coins have the same probability of heads, H0 : p =
```
p1 = p2 = p3 . The alternative hypothesis is that at least one of these probabilites is
```
different. Let’s consider the numerator of the Λ first, which will give us the maximum
likelihood estimator of p. Because the null hypothesis is that all the p values are
equal, we can just treat this as one big binomial distribution with n = n1 + n2 + n3
and k = k1 + k2 + k3 is the total number of heads observed for any coin. Thus, under
the null hypothesis, the distribution of k is binomial with parameters n and p. Now,
136 3 Statistics
what is the maximum likelihood estimator for this distribution? We have worked this
problem before and have the following,
ˆp0 = kn
In other words, the maximum likelihood estimator under the null hypothesis is the
proportion of ones observed in the sequence of n trials total. Now, we have to substi-
tute this in for the likelihood under the null hypothesis to finish the numerator of Λ,
```
L( ˆp0, ˆp0, ˆp0) = binom(k1; n1, ˆp0)binom(k2; n2, ˆp0)binom(k3; n3, ˆp0)
```
For the denomimator of Λ, which represents the case of maximizing over the entire
space, the maximum likelihood estimator for each separate binomial distribution is
likewise,
ˆpi = k in
i
which makes the likelihood in the denominator the following,
```
L( ˆp1, ˆp2, ˆp3) = binom(k1; n1, ˆp1)binom(k2; n2, ˆp2)binom(k3; n3, ˆp3)
```
```
for each of the i ∈ {1, 2, 3} binomial distributions. Then, the Λ statistic is then the
```
following,
```
Λ(k1, k2, k3) = L( ˆp0, ˆp0, ˆp0)L( ˆp
```
```
1, ˆp2, ˆp3)
```
Wilks theorems states that −2 log Λ is chi-square distributed. We can compute this
example with the statistics tools in Sympy and Scipy.
>>> from scipy.stats import binom, chi2
>>> import numpy as np
>>> # some sample parameters
>>> p0,p1,p2 = 0.3,0.4,0.5
>>> n0,n1,n2 = 50,180,200
```
>>> brvs= [ binom(i,j) for i,j in zip((n0,n1,n2),(p0,p1,p2))]
```
```
>>> def gen_sample(n=1):
```
... ’generate samples from separate binomial distributions’
... if n==1:
```
... return [i.rvs() for i in brvs]
```
... else:
```
... return [gen_sample() for k in range(n)]
```
...
3.5 Hypothesis Testing and P-Values 137
Programming Tip
Note the recursion in the definition of the gen_sample function where a
conditional clause of the function calls itself. This is a quick way to reusing
code and generating vectorized output. Using np.vectorize is another
way, but the code is simple enough in this case to use the conditional clause. In
Python, it is generally bad for performance to have code with nested recursion
because of how the stack frames are managed. However, here we are only
recursing once so this is not an issue.
Next, we compute the logarithm of the numerator of the Λ statistic,
```
>>> k0,k1,k2 = gen_sample()>>> print k0,k1,k2
```
```
12 68 103>>> pH0 = sum((k0,k1,k2))/sum((n0,n1,n2))
```
```
>>> numer = np.sum([np.log(binom(ni,pH0).pmf(ki))... for ni,ki in
```
```
... zip((n0,n1,n2),(k0,k1,k2))])>>> print numer
```
-15.5458638366
Note that we used the null hypothesis estimate for the ˆp0 . Likewise, for the logarithm
of the denominator we have the following,
```
>>> denom = np.sum([np.log(binom(ni,pi).pmf(ki))... for ni,ki,pi in
```
```
... zip((n0,n1,n2),(k0,k1,k2),(p0,p1,p2))])>>> print denom
```
-8.42410648079
Now, we can compute the logarithm of the Λ statistic as follows and see what the
corresponding value is according to Wilks theorem,
```
>>> chsq=chi2(2)>>> logLambda =-2*(numer-denom)
```
>>> print logLambda14.2435147116
```
>>> print 1- chsq.cdf(logLambda)0.000807346708329
```
Because the value reported above is less than the 5 % significance level, we reject
the null hypothesis that all the coins have the same probability of heads. Note that
there are two degrees of freedom because the difference in the number of parameters
```
between the null hypothesis ( p) and the alternative ( p1, p2, p3 ) is two. We can build
```
a quick Monte Carlo simulation to check the probability of detection for this example
using the following code, which is just a combination of the last few code blocks,
```
>>> c= chsq.isf(.05) # 5% significance level>>> out = []
```
```
>>> for k0,k1,k2 in gen_sample(100):... pH0 = sum((k0,k1,k2))/sum((n0,n1,n2))
```
```
... numer = np.sum([np.log(binom(ni,pH0).pmf(ki))... for ni,ki in
```
```
... zip((n0,n1,n2),(k0,k1,k2))])
```
138 3 Statistics
```
... denom = np.sum([np.log(binom(ni,pi).pmf(ki))... for ni,ki,pi in
```
```
... zip((n0,n1,n2),(k0,k1,k2),(p0,p1,p2))])... out.append(-2*(numer-denom)>c)
```
```
...>>> print np.mean(out) # estimated probability of detection
```
0.59
The above simulation shows the estimated probability of detection, for this set of
example parameters. This relative low probability of detection means that while
```
the test is unlikely (i.e., at the 5 % significance level) to mistakenly pick the null
```
```
hypothesis, it is likewise missing many of the H1 cases (i.e., low probability of
```
```
detection). The trade-off between which is more important is up to the particular
```
context of the problem. In some situations, we may prefer additional false alarms in
exchange for missing fewer H1 cases.
Permutation Test. The Permutation Test is good way to test whether or not samples
samples come from the same distribution. For example, suppose that
X1, X2, . . . , X m ∼ F
and also,
Y1, Y2, . . . , Yn ∼ G
That is, Yi and X i come from different distributions. Suppose we have some test
statistic, for example
```
T (X1, . . . , X m , Y1, . . . , Yn ) = |X − Y |
```
```
Under the null hypothesis for which F = G, any of the (n + m)! permutations are
```
```
equally likely. Thus, suppose for each of the (n + m)! permutations, we have the
```
computed statistic,
```
{T1, T2, . . . , T(n+m)! }
```
Then, under the null hypothesis, each of these values is equally likely. The distribution
```
of T under the null hypothesis is the permutation distribution that puts weight 1/(n +
```
```
m)! on each T -value. Suppose t o is the observed value of the test statistic and assume
```
that large T rejects the null hypothesis, then the p-value for the permutation test is
the following,
```
P(T > t o) = 1(n + m)!
```
```
(n+m)!∑
```
```
j=1
```
```
I (T j > t o)
```
```
where I () is the indicator function. For large (n + m)!, we can sample randomly
```
from the set of all permutations to estimate this p-value.
3.5 Hypothesis Testing and P-Values 139
Example Let’s return to our coin-flipping example from last time, but now we have
only two coins. The hypothesis is that both coins have the same probability of heads.
We can use the built-in function in Numpy to compute the random permutations.
```
>>> x=binom(10,0.3).rvs(5) # p=0.3>>> y=binom(10,0.5).rvs(3) # p=0.5
```
```
>>> z = np.hstack([x,y]) # combine into one array>>> t_o = abs(x.mean()-y.mean())
```
```
>>> out = [] # output container>>> for k in range(1000):
```
```
... perm = np.random.permutation(z)... T=abs(perm[:len(x)].mean()-perm[len(x):].mean())
```
```
... out.append((T>t_o))...
```
```
>>> print ’p-value = ’, np.mean(out)p-value = 0.0
```
Note that the size of total permutation space is 8! = 40320 so we are taking relatively
```
few (i.e., 100) random permutations from this space.
```
Wald Test. The Wald Test is an asympotic test. Suppose we have H0 : θ = θ0 and
otherwise H1 : θ = θ0 , the corresponding statistic is defined as the following,
```
W =
```
ˆθn − θ0
se
where ˆθ is the maximum likelihood estimator and se is the standard error,
```
se =
```
√
```
V( ˆθn )
```
```
Under general conditions, W d→ N (0, 1). Thus, an asympotic test at level α rejects
```
```
when |W | > zα/2 where zα/2 corresponds to P(|Z | > zα/2) = α with Z ∼ N (0, 1).
```
For our favorite coin-flipping example, if H0 : θ = θ0 , then
```
W =
```
ˆθ − θ0
√
```
ˆθ(1 − ˆθ)/n
```
We can simulate this using the following code at the usual 5 % significance level,
>>> from scipy import stats>>> theta0 = 0.5 # H0
```
>>> k=np.random.binomial(1000,0.3)>>> theta_hat = k/1000. # MLE
```
```
>>> W = (theta_hat-theta0)/np.sqrt(theta_hat*(1-theta_hat)/1000)>>> c = stats.norm().isf(0.05/2) # z_{alpha/2}
```
```
>>> print abs(W)>c # if true, reject H0True
```
This rejects H0 because the true θ = 0.3 and the null hypothesis is that θ = 0.5.
Note that n = 1000 in this case which puts us well inside the asympotic range of
the result. We can re-do this example to estimate the detection probability for this
example as in the following code,
140 3 Statistics
```
>>> theta0 = 0.5 # H0>>> c = stats.norm().isf(0.05/2.) # z_{alpha/2}
```
```
>>> out = []>>> for i in range(100):
```
```
... k=np.random.binomial(1000,0.3)... theta_hat = k/1000. # MLE
```
```
... W = (theta_hat-theta0)/np.sqrt(theta_hat*(1-theta_hat)/1000.)... out.append(abs(W)>c) # if true, reject H0
```
```
...>>> print np.mean(out) # detection probability
```
1.0
3.5.5 Testing Multiple Hypotheses
Thus far, we have focused primarily on two competing hypotheses. Now, we con-
sider multiple comparisons. The general situation is the following. We test the null
hypothesis against a sequence of n competing hypotheses Hk . We obtain p-values
```
for each hypothesis so now we have multiple p-values to consider { p k }. To boil this
```
sequence down to a single criterion, we can make the following argument. Given
n independent hypotheses that are all untrue, the probability of getting at least one
false alarm is the following,
```
PFA = 1 − (1 − p0)n
```
```
where p0 is the individual p-value threshold (say, 0.05). The problem here is that
```
PFA → 1 as n → ∞. If we want to make many comparisons at once and control the
overall false alarm rate the overall p-value should be computed under the assumption
that none of the competing hypotheses is valid. The most common way to address
this is with the Bonferroni correction which says that the individual significance level
should be reduced to p/n. Obviously, this makes it much harder to declare signif-
icance for any particular hypothesis. The natural consequence of this conservative
restriction is to reduce the statistical power of the experiment, thus making it more
likely the true effects will be missed.
In 1995, Benjamini and Hochberg devised a simple method that tells which
p-values are statistically significant. The procedure is to sort the list of p-values
```
in ascending order, choose a false-discovery rate (say, q), and then find the largest
```
p-value in the sorted list such that p k ≤ kq/n, where k is the p-value’s position in the
sorted list. Finally, declare that p k value and all the others less than it statistically sig-
nificant. This procedure guarantees that the proportion of false-positives is less than
```
q (on average). The Benjamini-Hochberg procedure (and its derivatives) is fast and
```
effective and is widely used for testing hundreds of primarily false hypotheses when
studying genetics or diseases. Additionally, this procedure provides better statistical
power than the Bonferroni correction.
In this section, we discussed the structure of statistical hypothesis testing and
defined the various terms that are commonly used for this process, along with
the illustrations of what they mean in our running coin-flipping example. From an
3.5 Hypothesis Testing and P-Values 141
engineering standpoint, hypothesis testing is not as common as confidence-intervals
and point estimates. On the other hand, hypothesis testing is very common in social
and medical science, where one must deal with practical constraints that may limit
the sample size or other aspects of the hypothesis testing rubric. In engineering, we
can usually have much more control over the samples and models we employ because
they are typically inanimate objects that can be measured repeatedly and consistently.
This is obviously not so with human studies, which generally have other ethical and
legal considerations.
3.6 Confidence Intervals
In a previous coin-flipping discussion, we discussed estimation of the underlying
probability of getting a heads. There, we derived the estimator as
ˆp n = 1n
n∑
```
i=1
```
X i
```
where X i ∈ {0, 1}. Confidence intervals allow us to estimate how close we can get
```
to the true value that we are estimating. Logically, that seems strange, doesn’t it? We
```
really don’t know the exact value of what we are estimating (otherwise, why estimate
```
```
it?), and yet, somehow we know how close we can get to something we admit we
```
don’t know? Ultimately, we want to make statements like the probability of the value
in a certain interval is 90 %. Unfortunately, that is something we will not be able to
say using our methods. Note that Bayesian estimation gets closer to this statement
by using credible intervals, but that is a story for another day. In our situation, the
best we can do is say roughly the following: if we ran the experiment multiple times,
then the confidence interval would trap the true parameter 90 % of the time.
Let’s return to our coin-flipping example and see this in action. One way to get at
a confidence interval is to use Hoeffding’s inequality from Sect. 2.9.3 specialized to
our Bernoulli variables as
```
P(| ˆp n − p |> ) ≤ 2 exp(−2n2)
```
Now, we can form the interval I = [ ˆp n − n , ˆp n + n ], where n is carefully
constructed as
n =
√
1
2n log
2
α
which makes the right-side of the Hoeffding inequality equal to α. Thus, we finally
have
```
P( p /∈ I) = P
```
```
(
```
| ˆp n − p |> n
```
)
```
≤ α
142 3 Statistics
```
Thus, P( p ∈ I) ≥ 1 − α. As a numerical example, let’s take n = 100, α = 0.05,
```
then plugging into everything we have gives n = 0.136. So, the 95 % confidence
interval here is therefore
```
I = [ ˆp n − n , ˆp n + n ] = [ ˆp n − 0.136, ˆp n + 0.136]
```
The following code sample is a simulation to see if we can really trap the under-
lying parameter in our confidence interval.
>>> from scipy import stats>>> import numpy as np
```
>>> b= stats.bernoulli(.5) # fair coin distribution>>> nsamples = 100
```
```
>>> # flip it nsamples times for 200 estimates>>> xs = b.rvs(nsamples*200).reshape(nsamples,-1)
```
```
>>> phat = np.mean(xs,axis=0) # estimated p>>> # edge of 95\,% confidence interval
```
```
>>> epsilon_n=np.sqrt(np.log(2/0.05)/2/nsamples)>>> pct=np.logical_and(phat-epsilon_n<=0.5,
```
```
... 0.5 <= (epsilon_n +phat)... ).mean()*100
```
>>> print ’Interval trapped correct value ’, pct,’% of the time’Interval trapped correct value 99.5 % of the time
The result shows that the estimator and the corresponding interval was able to trap the
true value at least 95 % of the time. This is how to interpret the action of confidence
intervals.
However, the usual practice is to not use Hoeffding’s inequality and instead use
arguments around asymptotic normality. The definition of the standard error is the
```
following:
```
```
se =
```
√
```
V( ˆθn )
```
where ˆθn is the point-estimator for the parameter θ, given n samples of data X n , and
```
V( ˆθn ) is the variance of ˆθn . Likewise, the estimated standard error iŝ se. For example,
```
in our coin-flipping example, the estimator was ˆp = ∑ X i /n with corresponding
```
variance V( ˆp n ) = p(1 − p)/n. Plugging in the point estimate gives us the estimated
```
standard error:̂ se =
√
```
ˆp(1 − ˆp)/n. Because maximum likelihood estimators are
```
```
asymptotically normal,4 we know that ˆp n ∼ N ( p,̂ se2). Thus, if we want a 1 − α
```
confidence interval, we can compute
```
P(| ˆp n − p |< ξ) > 1 − α
```
```
but since we know that ( ˆp n − p) is asymptotically normal, N (0,̂ se2), we can instead
```
compute
4 Certain technical regularity conditions must hold for this property of maximum likelihood estimator
to work. See [2] for more details.
3.6 Confidence Intervals 143
Fig. 3.11 The gray circles
are the point estimates that
are bounded above and
below by both asymptotic
confidence intervals and
Hoeffding intervals. The
asymptotic intervals are
tighter because the
underpinning asymptotic
assumptions are valid for
these estimates
∫ ξ
−ξ
```
N (0,̂ se2)dx > 1 − α
```
This looks ugly to compute because we need to find ξ, but Scipy has everything we
need for this.
```
>>> # compute estimated se for all trials>>> se=np.sqrt(phat*(1-phat)/xs.shape[0])
```
```
>>> # generate random variable for trial 0>>> rv=stats.norm(0, se[0])
```
```
>>> # compute 95\,% confidence interval for that trial 0>>> np.array(rv.interval(0.95))+phat[0]
```
```
array([ 0.42208023, 0.61791977])>>> def compute_CI(i):
```
```
... return stats.norm.interval(0.95,loc=i,... scale=np.sqrt(i*(1-i)/xs.shape[0]))
```
```
...>>> lower,upper = compute_CI(phat)
```
Figure 3.11 shows the asymptotic confidence intervals and the Hoeffding-derived
confidence intervals. As shown, the Hoeffding intervals are a bit more generous
than the asymptotic estimates. However, this is only true so long as the asympotic
approximation is valid. In other words, there exists some number of n samples for
which the asymptotic intervals may not work. So, even though they may be a bit
more generous, the Hoeffding intervals do not require arguments about asymptotic
convergence. In practice, nonetheless, asymptotic convergence is always in play
```
(even if not explicitly stated).
```
Confidence Intervals and Hypothesis testing. It turns out that there is a close
dual relationship between hypothesis testing and confidence intervals. To see this in
action, consider the following hypothesis test for a normal distribution, H0 : μ = μ0
versus H1 : μ = μ0 . A reasonable test has the following rejection region:
```
{
```
```
x :| ¯x − μ0 |> zα/2σ√n
```
```
}
```
144 3 Statistics
```
where P(Z > zα/2) = α/2 and P(−zα/2 < Z < zα/2) = 1 − α and where
```
```
Z ∼ N (0, 1). This is the same thing as saying that the region corresponding to
```
acceptance of H0 is then,
```
¯x − zα/2σ√n ≤ μ0 ≤ ¯x + zα/2σ√n (3.6.0.1)
```
```
Because the test has size α, the false alarm probability, P(H0 rejected | μ =
```
```
μ0) = α. Likewise, the P(H0 accepted | μ = μ0) = 1 − α. Putting this all
```
together with interval defined above means that
P
```
(
```
¯x − zα/2σ√n ≤ μ0 ≤ ¯x + zα/2σ√n
∣∣
∣H0
```
)
```
= 1 − α
Because this is valid for any μ0 , we can drop the H0 condition and say the following:
P
```
(
```
¯x − zα/2σ√n ≤ μ0 ≤ ¯x + zα/2σ√n
```
)
```
= 1 − α
As may be obvious by now, the interval in Eq. 3.6.0.1 above is the 1−α confidence
interval! Thus, we have just obtained the confidence interval by inverting the accep-
tance region of the level α test. The hypothesis test fixes the parameter and then asks
```
what sample values (i.e., the acceptance region) are consistent with that fixed value.
```
Alternatively, the confidence interval fixes the sample value and then asks what para-
```
meter values (i.e., the confidence interval) make this sample value most plausible.
```
```
Note that sometimes this inversion method results in disjoint intervals (known as
```
```
confidence sets).
```
3.7 Linear Regression
Linear regression gets to the heart of statistics: Given a set of data points, what is
the relationship of the data in-hand to data yet seen? How should information from
one data set propagate to other data? Linear regression offers the following model to
address this question:
```
E(Y |X = x) ≈ ax + b
```
That is, given specific values for X, assume that the conditional expectation is a linear
```
function of those specific values. However, because the observed values are not the
```
expectations themselves, the model accommodates this with an additive noise term.
```
In other words, the observed variable (a.k.a. response, target, dependent variable) is
```
modeled as,
```
E(Y |X = x i ) + i ≈ ax + b + i = y
```
3.7 Linear Regression 145
```
where E(i ) = 0 and the i are iid and where the distribution function of i depends
```
on the problem, even though it is often assumed Gaussian. The X = x values are
known as independent variables, covariates, or regressors.
Let’s see if we can use all of the methods we have developed so far to understand
this form of regression. The first task is to determine how to estimate the unknown
```
linear parameters, a and b. To make this concrete, let’s assume that  ∼ N (0, σ2).
```
```
Bear in mind that E(Y |X = x) is a deterministic function of x. In other words, the
```
variable x changes with each draw, but after the data have been collected these are no
longer random quantities. Thus, for fixed x, y is a random variable generated by .
Perhaps we should denote  as x to emphasize this, but because  is an independent,
```
identically-distributed (iid) random variable at each fixed x, this would be excessive.
```
Because of Gaussian additive noise, the distribution of y is completely characterized
by its mean and variance.
```
E(y) = ax + b
```
```
V(y) = σ2
```
Using the maximum likelihood procedure, we write out the log-likelihood function as
```
L(a, b) =
```
n∑
```
i=1
```
```
log N (ax i + b, σ2) ∝ 12σ2
```
n∑
```
i=1
```
```
(yi − ax i − b)2
```
Note that we suppressed the terms that are irrelevent to the maximum-finding. Taking
the derivative of this with respect to a gives the following equation:
```
∂L(a, b)
```
∂a = 2
n∑
```
i=1
```
```
x i (b + ax i − yi ) = 0
```
Likewise, we do the same for the b parameter
```
∂L(a, b)
```
∂b = 2
n∑
```
i=1
```
```
(b + ax i − yi ) = 0
```
The following code simulates some data and uses Numpy tools to compute the
parameters as shown,
```
>>> import numpy as np>>> a = 6;b = 1 # parameters to estimate
```
```
>>> x = np.linspace(0,1,100)>>> y = a*x + np.random.randn(len(x))+b
```
```
>>> p,var_=np.polyfit(x,y,1,cov=True) # fit data to line>>> y_ = np.polyval(p,x) # estimated by linear regression
```
146 3 Statistics
Fig. 3.12 The panel on the left shows the data and regression line. The panel on the right shows a
histogram of the regression errors
The graph on the left of Fig. 3.12 shows the regression line plotted against the data.
The estimated parameters are noted in the title. The histogram on the right of Fig. 3.12
shows the residual errors in the model. It is always a good idea to inspect the residuals
of any regression for normality. These are the differences between the fitted line for
each x i value and the corresponding yi value in the data. Note that the x term does
not have to be uniformly monotone.
To decouple the deterministic variation from the random variation, we can fix the
index and write separate problems of the form
```
yi = ax i + b + i
```
```
where i ∼ N (0, σ2). What could we do with just this one component of the prob-
```
```
lem? In other words, suppose we had m-samples of this component as in {yi,k }mk=1 .
```
Following the usual procedure, we could obtain estimates of the mean of yi as
ˆyi = 1m
m∑
```
k=1
```
yi,k
However, this tells us nothing about the individual parameters a and b because they
are not separable in the terms that are computed, namely, we may have
```
E(yi ) = ax i + b
```
but we still only have one equation and the two unknowns, a and b. How about if we
consider and fix another component j as in
y j = ax j + b + i
3.7 Linear Regression 147
Then, we have
```
E(y j ) = ax j + b
```
so at least now we have two equations and two unknowns and we know how to
estimate the left hand sides of these equations from the data using the estimators ˆyi
```
and ˆy j . Let’s see how this works in the code sample below (Fig. 3.13).
```
>>> x0, xn =x[0],x[80]>>> # generate synthetic data
```
>>> y_0 = a*x0 + np.random.randn(20)+b>>> y_1 = a*xn + np.random.randn(20)+b
```
```
>>> # mean along sample dimension>>> yhat = np.array([y_0,y_1]).mean(axis=1)
```
```
>>> a_,b_=np.linalg.solve(np.array([ [x0,1],... [xn,1] ]),yhat)
```
Programming Tip
The prior code uses the solve function in the Numpy linalg module,
which contains the core linear algebra codes in Numpy that incorporate the
battle-tested LAPACK library.
We can write out the solution for the estimated parameters for this case where x0 = 0
ˆa = ˆyi − ˆy0x
i
ˆb = ˆy0
Fig. 3.13 The fitted and true lines are plotted with the data values. The squares at either end of the
solid line show the mean value for each of the data groups shown
148 3 Statistics
The expectations and variances of these estimators are the following,
```
E( ˆa) = ax ix
```
i
= a
```
E( ˆb) = b
```
```
V( ˆa) = 2σ
```
2
x2i
```
V( ˆb) = σ2
```
The expectations show that the estimators are unbiased. The estimator ˆa has a variance
that decreases as larger points x i are selected. That is, it is better to have samples
further out along the horizontal axis for fitting the line. This variance quantifies the
leverage of those distant points.
Regression From Projection Methods. Let’s see if we can apply our knowledge of
projection methods to the general case. In vector notation, we can write the following:
```
y = ax + b1 + 
```
where 1 is the vector of all ones. Let’s use the inner-product notation,
```
〈x, y〉 = E(xT y)
```
Then, by taking the inner-product with some x1 ∈ 1⊥ we obtain, 5
〈y, x1〉 = a〈x, x1〉
```
Recall that E() = 0. We can finally solve for a as
```
ˆa = 〈y, x1〉〈x, x
1〉
```
(3.7.0.2)
```
That was pretty neat but now we have the mysterious x1 vector. Where does this
come from? If we project x onto the 1⊥, then we get the MMSE approximation to x
in the 1⊥ space. Thus, we take
```
x1 = P1⊥ (x)
```
Remember that P1⊥ is a projection matrix so the length of x1 is at most x. This means
that the denominator in the ˆa equation above is really just the length of the x vector
```
in the coordinate system of P1⊥ . Because the projection is orthogonal (namely, of
```
```
minimum length), the Pythagorean theorem gives this length as the following:
```
5 The space of all vectors, a such that 〈a, 1〉 = 0 is denoted 1⊥.
3.7 Linear Regression 149
〈x, x1〉2 = 〈x, x〉 − 〈1, x〉2
The first term on the right is the length of the x vector and last term is the length
of x in the coordinate system orthogonal to P1⊥ , namely that of 1. We can use this
geometric interpretation to understand what is going on in typical linear regression in
much more detail. The fact that the denominator is the orthogonal projection of x tells
```
us that the choice of x1 has the strongest effect (i.e., largest value) on reducing the
```
variance of ˆa. That is, the more x is aligned with 1, the worse the variance of ˆa. This
makes intuitive sense because the closer x is to 1, the more constant it is, and we have
already seen from our one-dimensional example that distance between the x terms
pays off in reduced variance. We already know that ˆa is an unbiased estimator and
because we chose x1 deliberately as a projection, we know that it is also of minimum
variance. Such estimators are known as Minimum-Variance Unbiased Estimators
```
(MVUE).
```
In the same spirit, let’s examine the numerator of ˆa in Eq. 3.7.0.2. We can write
x1 as the following
```
x1 = x − P1 x
```
where P1 is projection matrix of x onto the 1 vector. Using this, the numerator of ˆa
becomes
〈y, x1〉 = 〈y, x〉 − 〈y, P1 x〉
Note that,
```
P1 = 11T 1n
```
so that writing this out explicitly gives
〈y, P1 x〉 =
```
(
```
yT 1
```
) (
```
1T x
```
)
```
/n =
```
(∑
```
yi
```
) (∑
```
x i
```
)
```
/n
and similarly, we have the following for the denominator:
〈x, P1 x〉 =
```
(
```
xT 1
```
) (
```
1T x
```
)
```
/n =
```
(∑
```
x i
```
) (∑
```
x i
```
)
```
/n
So, plugging all of this together gives the following,
ˆa = x
```
T y − (∑ x i )(∑ yi )/n
```
```
xT x − (∑ x i )2/n
```
150 3 Statistics
with corresponding variance,
```
V( ˆa) = σ2 ‖x1‖
```
2
〈x, x1〉2
= σ
2
```
‖x‖2 − n(x2)
```
Using the same approach with ˆb gives,
ˆb = 〈y, x
⊥ 〉
```
〈1, x⊥ 〉 (3.7.0.3)
```
```
= 〈y, 1 − Px(1)〉〈1, 1 − P
```
```
x(1)〉
```
```
(3.7.0.4)
```
= x
```
T x(∑ yi )/n − xT y(∑ x i )/n
```
```
xT x − (∑ x i )2/n (3.7.0.5)
```
where
```
Px = xx
```
T
‖x‖2
with variance
```
V( ˆb) = σ2 〈1 − Px(1), 1 − Px(1)〉〈1, 1 − P
```
```
x(1)〉2
```
= σ
2
```
n − (nx)2‖x‖2
```
Qualifying the Estimates. Our formulas for the variance above include the unknown
σ2 , which we must estimate from the data itself using our plug-in estimates. We can
form the residual sum of squares as
```
RSS =
```
∑
i
```
( ˆax i + ˆb − yi )2
```
Thus, the estimate of σ2 can be expressed as
ˆσ2 = RSSn − 2
3.7 Linear Regression 151
where n is the number of samples. This is also known as the residual mean square. The
```
n − 2 represents the degrees of freedom (df). Because we estimated two parameters
```
from the same data we have n − 2 instead of n. Thus, in general, df = n − p,
where p is the number of estimated parameters. Under the assumption that the noise
is Gaussian, the RSS/σ2 is chi-squared distributed with n − 2 degrees of freedom.
```
Another important term is the sum of squares about the mean, (a.k.a corrected sum
```
```
of squares),
```
```
SYY =
```
∑
```
(yi − ¯y)2
```
The SYY captures the idea of not using the x i data and just using the mean of the yi
data to estimate y. These two terms lead to the R2 term,
```
R2 = 1 − RSSSYY
```
Note that for perfect regression, R2 = 1. That is, if the regression gets each yi data
point exactly right, then RSS = 0 this term equals one. Thus, this term is used to
measure of goodness-of-fit. The stats module in scipy computes many of these
terms automatically,
```
from scipy import statsslope,intercept,r_value,p_value,stderr = stats.linregress(x,y)
```
where the square of the r_value variable is the R2 above. The computed p-value is
the two-sided hypothesis test with a null hypothesis that the slope of the line is zero.
In other words, this tests whether or not the linear regression makes sense for the data
for that hypothesis. The Statsmodels module provides a powerful extension to Scipy’s
stats module by making it easy to do regression and keep track of these parameters.
Let’s reformulate our problem using the Statsmodels framework by creating a Pandas
dataframe for the data,
import statsmodels.formula.api as smffrom pandas import DataFrame
```
import numpy as npd = DataFrame({’x’:np.linspace(0,1,10)}) # create data
```
```
d[’y’] = a*d.x+ b + np.random.randn(*d.x.shape)
```
Now that we have the input data in the above Pandas dataframe, we can perform the
regression as in the following,
```
results = smf.ols(’y ˜ x’, data=d).fit()
```
The ∼ symbol is notation for y = ax + b + , where the constant b is implicit in
this usage of Statsmodels. The names in the string are taken from the columns in the
dataframe. This makes it very easy to build models with complicated interactions
between the named columns in the dataframe. We can examine a report of the model
fit by looking at the summary,
152 3 Statistics
```
print results.summary2()Results: Ordinary least squares
```
===================================================================Model: OLS Adj. R-squared: 0.808
Dependent Variable: y AIC: 28.1821Date: 0000-00-00 00:00 BIC: 00.0000
No. Observations: 10 Log-Likelihood: -12.091Df Model: 1 F-statistic: 38.86
```
Df Residuals: 8 Prob (F-statistic): 0.000250R-squared: 0.829 Scale: 0.82158
```
-------------------------------------------------------------------Coef. Std.Err. t P>|t| [0.025 0.975]
-------------------------------------------------------------------Intercept 1.5352 0.5327 2.8817 0.0205 0.3067 2.7637
x 5.5990 0.8981 6.2340 0.0003 3.5279 7.6701
There is a lot more here than we have discussed so far, but the Statsmodels doc-
umentation is the best place to go for complete information about this report. The
F-statistic attempts to capture the contrast between including the slope parameter or
leaving it off. That is, consider two hypotheses:
```
H0 : E(Y |X = x) = b
```
```
H1 : E(Y |X = x) = b + ax
```
In order to quantify how much better adding the slope term is for the regression, we
compute the following:
```
F = SYY − RSSˆσ2
```
The numerator computes the difference in the residual squared errors between includ-
ing the slope in the regression or just using the mean of the yi values. Once again, if we
```
assume (or can claim asymptotically) that the  noise term is Gaussian,  ∼ N (0, σ2),
```
then the H0 hypothesis will follow an F-distribution6 with degrees of freedom from
```
the numerator and denominator. In this case, F ∼ F(1, n−2). The value of this statis-
```
tic is reported by Statsmodels above. The corresponding reported probability shows
the chance of F exceeding its computed value if H0 were true. So, the take-home
message from all this is that including the slope leads to a much smaller reduction
in squared error than could be expected from a favorable draw of n points of this
data, under the Gaussian additive noise assumption. This is evidence that including
the slope is meaningful for this data.
The Statsmodels report also shows the adjusted R2 term. This is a correction to
the R2 calculation that accounts for the number of parameters p that the regression
is fitting and the sample size n,
```
Adjusted R2 = 1 − RSS/(n − p)SYY/(n − 1)
```
```
6 The F(m, n) F-distribution has two integer degree-of-freedom parameters, m and n.
```
3.7 Linear Regression 153
```
This is always lower than R2 except when p = 1 (i.e., estimating only b). This
```
becomes a better way to compare regressions when one is attempting to fit many
parameters with comparatively small n.
Linear Prediction. Using linear regression for prediction introduces some other
issues. Recall the following expectation,
```
E(Y |X = x) ≈ ˆax + ˆb
```
where we have determined ˆa and ˆb from the data. Given a new point of interest, x p ,
we would certainly compute
ˆy p = ˆax p + ˆb
as the predicted value for ˆy p . This is the same as saying that our best prediction
for y based on x p is the above conditional expectation. The variance for this is the
following,
```
V(y p ) = x2p V( ˆa) + V( ˆb) + 2x p cov( ˆa ˆb)
```
Note that we have the covariance above because ˆa and ˆb are derived from the same
data. We can work this out below using our previous notation from Eq. 3.7.0.2,
```
cov( ˆa ˆb) = x
```
```
T1 V{yyT }x⊥
```
```
(xT1 x)(1T x⊥) =
```
xT1 σ2Ix⊥
```
(xT1 x)(1T x⊥)
```
=σ2 x
T1 x⊥
```
(xT1 x)(1T x⊥) = σ
```
```
2 (x − P1x)T x⊥
```
```
(xT1 x)(1T x⊥)
```
=σ2 −x
T P T1 x⊥
```
(xT1 x)(1T x⊥) = σ
```
2 −xT 1n 11T x⊥
```
(xT1 x)(1T x⊥)
```
=σ2 −x
T 1n 1
```
(xT1 x) =
```
−σ2 x∑
```
ni=1(x2i − x2)
```
After plugging all this in, we obtain the following,
```
V(y p ) = σ2
```
x2p − 2x p x + ‖x‖2/n
‖x‖2 − nx2
where, in practice, we use the plug-in estimate for the σ2 .
There is an important consequence for the confidence interval for y p . We cannot
```
simply use the square root of V(y p ) to form the confidence interval because the
```
model includes the extra  noise term. In particular, the parameters were computed
154 3 Statistics
using a set of statistics from the data, but now must include different realizations for
the noise term for the prediction part. This means we have to compute
```
η2 = V(y p ) + σ2
```
```
Then, the 95 % confidence interval y p ∈ (y p − 2 ˆη, y p + 2 ˆη) is the following,
```
```
P(y p − 2 ˆη < y p < y p + 2 ˆη) ≈ P(−2 < N (0, 1) < 2) ≈ 0.95
```
where ˆη comes from substituting the plug-in estimate for σ.
3.7.1 Extensions to Multiple Covariates
With all the machinery we have, it is a short notational hop to consider multiple
regressors as in the following,
```
Y = Xβ + 
```
```
with the usual E() = 0 and V() = σ2I. Thus, X is a n × p full rank matrix of
```
regressors and Y is the n-vector of observations. Note that the constant term has been
incorporated into X as a column of ones. The corresponding estimated solution for
β is the following,
```
ˆβ = (XT X)−1XT Y
```
with corresponding variance,
```
V( ˆβ) = σ2(XT X)−1
```
and with the assumption of Gaussian errors, we have
```
ˆβ ∼ N (β, σ2(XT X)−1)
```
The unbiased estimate of σ2 is the following,
ˆσ2 = 1n − p
∑
ˆ2i
where ˆ = X ˆβ − Y is the vector of residuals. Tukey christened the following matrix
```
as the hat matrix (a.k.a. influence matrix),
```
```
V = X(XT X)−1XT
```
3.7 Linear Regression 155
because it maps Y into ˆY,
ˆY = VY
As an exercise you can check that V is a projection matrix. Note that that matrix is
solely a function of X. The diagonal elements of V are called the leverage values
and are contained in the closed interval [1/n, 1]. These terms measure of distance
between the values of x i and the mean values over the n observations. Thus, the
leverage terms depend only on X. This is the generalization of our initial discussion
of leverage where we had multiple samples at only two x i points. Using the hat
matrix, we can compute the variance of each residual, ei = ˆy − yi as
```
V(ei ) = σ2(1 − vi )
```
where vi = Vi,i . Given the above-mentioned bounds on vi , these are always less
than σ2 .
Degeneracy in the columns of X can become a problem. This is when two or
more of the columns become co-linear. We have already seen this with our single
regressor example wherein x close to 1 was bad news. To compensate for this effect
we can load the diagonal elements and solve for the unknown parameters as in the
following,
```
ˆβ = (XT X + αI)−1XT Y
```
where α > 0 is a tunable hyper-parameter. This method is known as ridge regression
and was proposed in 1970 by Hoerl and Kenndard. It can be shown that this is the
equivalent to minimizing the following objective,
‖Y − Xβ‖2 + α‖β‖2
In other words, the length of the estimated β is penalized with larger α. This has the
effect of stabilizing the subsequent inverse calculation and also providing a means
to trade bias and variance, which we will discuss at length in Sect. 4.6.
Interpreting Residuals. Our model assumes an additive Gaussian noise term. We
can check the voracity of this assumption by examining the residuals after fitting.
The residuals are the difference between the fitted values and the original data
ˆi = ˆax i + ˆb − yi
While the p-value and the F-ratio provide some indication of whether or not comput-
ing the slope of the regression makes sense, we can get directly at the key assumption
of additive Gaussian noise.
156 3 Statistics
For sufficiently small dimensions, the scipy.stats.probplot we discussed
in the last chapter provides quick visual evidence one way or another by plotting the
standardized residuals,
r i = eiˆσ√1 − v
i
```
The other part of the iid assumption implies homoscedasticity (all r i have equal
```
```
variances). Under the additive Gaussian noise assumption, the ei should also be
```
```
distributed according to N (0, σ2(1 − vi )). The normalized residuals r i should then
```
```
be distributed according to N (0, 1). Thus, the presence of any r i /∈ [−1.96, 1.96]
```
should not be common at the 5 % significance level and is thereby breeds suspicion
regarding the homoscedasticity assumption.
The Levene test in scipy.stats.leven tests the null hypothesis that all the
variances are equal. This basically checks whether or not the standardized residuals
vary across x i more than expected. Under the homoscedasticity assumption, the
variance should be independent of x i . If not, then this is a clue that there is a missing
```
variable in the analysis or that the variables themselves should be transformed (e.g.,
```
```
using the log function) into another format that can reduce this effect. Also, we can
```
use weighted least-squares instead of ordinary least-squares.
Variable Scaling. It is tempting to conclude in a multiple regression that small
coefficients in any of the β terms implies that those terms are not important. However,
simple unit conversions can cause this effect. For example, if one of the regressors
is in units of kilometers and the others are in meters, then just the scale factor can
give the impression of outsized or under-sized effects. The common way to account
for this is to scale the regressors so that
x′ = x − ¯xσ
x
This has the side effect of converting the slope parameters into correlation coeffi-
cients, which is bounded by ±1.
Influential Data. We have already discussed the idea of leverage. The concept
of influence combines leverage with outliers. To understand influence, consider
Fig. 3.14.
The point on the right in Fig. 3.14 is the only one that is contributing to the
calculation of the slope for the fitted line. Thus, it is very influential in this sense.
Cook’s distance is a good way to get at this concept numerically. To compute this,
we have to compute the jth component of the estimated target variable with the ith
```
point deleted. We call this ˆy j (i). Then, we compute the following,
```
```
Di =
```
∑
```
j ( ˆy j − ˆy j (i) )2
```
```
p/n ∑j ( ˆy j − y j )2
```
3.7 Linear Regression 157
Fig. 3.14 The point on the
right has outsized influence
in this data because it is the
only one used to determine
the slope of the fitted line
Fig. 3.15 The calculated
Cook’s distance for the data
in Fig. 3.14
```
where, as before, p is the number of estimated terms (e.g., p = 2 in the bivariate
```
```
case). This calculation emphasizes the effect of the outlier by predicting the target
```
variable with and without each point. In the case of Fig. 3.14, losing any of the points
on the left cannot change the estimated target variable much, but losing the single
point on the right surely does. The point on the right does not seem to be an outlier
```
(it is on the fitted line), but this is because it is influential enough to rotate the line
```
to align with it. Cook’s distance helps capture this effect by leaving each sample
out and re-fitting the remainder as shown in the last equation. Figure 3.15 shows the
calculated Cook’s distance for the data in Fig. 3.14, showing that the data point on the
```
right (sample index 5) has outsized influence on the fitted line. As a rule of thumb,
```
Cook’s distance values greater than one are suspect.
As another illustration of influence, consider Fig. 3.16 which shows some data that
```
nicely line up, but with one outlier (filled black circle) in the upper panel. The lower
```
panel shows so-computed Cook’s distance for this data. As shown Cook’s distance
emphasizes the presence of the outlier. Because the calculation involves leaving a
single sample out and re-calculating the rest, it can be a time-consuming operation
158 3 Statistics
Fig. 3.16 The upper panel
shows data that fit on a line
```
and an outlier point (filled
```
```
black circle). The lower
```
panel shows the calculated
Cook’s distance for the data
in upper panel and shows
```
that the tenth point (i.e., the
```
```
outlier) has disproportionate
```
influence
suitable to relatively small data sets. There is always the temptation to downplay the
importance of outliers because they conflict with a favored model, but outliers must
be carefully examined to understand why the model is unable to capture them. It
could be something as simple as faulty data collection, or it could be an indication
of deeper issues that have been overlooked. The following code shows how Cook’s
distance was compute for Figs. 3.15 and 3.16.
```
>>> fit = lambda i,x,y: np.polyval(np.polyfit(x,y,1),i)>>> omit = lambda i,x: ([k for j,k in enumerate(x) if j !=i])
```
```
>>> def cook_d(k):... num = sum((fit(j,omit(k,x),omit(k,y))- fit(j,x,y))**2 for j in x)
```
```
... den = sum((y-np.polyval(np.polyfit(x,y,1),x))**2/len(x)*2)... return num/den
```
...
Programming Tip
The function omit sweeps through the data and excludes the ith data element.
The embedded enumerate function associates every element in the iterable
with its corresponding index.
3.8 Maximum A-Posteriori
We saw with maximum likelihood estimation how we could use the principle of
maximum likelihood to derive a formula of the data that would estimate the underly-
```
ing parameters (say, θ). Under that method, the parameter was fixed, but unknown.
```
If we change our perspective slightly and consider the underlying parameter as a
random variable in its own right, this leads to additional flexibility in estimation.
This method is the simplest of the family of Bayesian statistical methods and is most
closely related to maximum likelihood estimation. It is very popular in communi-
cations and signal processing and is the backbone of many important algorithms in
those areas.
3.8 Maximum A-Posteriori 159
Given that the parameter θ is also a random variable, it has a joint distribution
```
with the other random variables, say, f (x, θ). Bayes’ theorem gives the following:
```
```
P(θ|x) = P(x|θ)P(θ)P(x)
```
```
The P(x|θ) term is the usual likelihood term we have seen before. The term in the
```
denominator is prior probability of the data x and it explicitly makes a very powerful
```
claim: even before collecting or processing any data, we know what the probability
```
```
of that data is. The P(θ) is the prior probability of the parameter. In other words,
```
regardless of the data that is collected, this is the probability of the parameter itself.
In a particular application, whether or not you feel justified making these claims is
something that you have to reconcile for yourself and the problem at hand. There are
many persuasive philosophical arguments one way or the other, but the main thing
to keep in mind when applying any method is whether or not the assumptions are
reasonable for the problem at hand.
```
However, for now, let’s just assume that we somehow have P(θ) and the next step
```
is the maximizing of this expression over the θ. Whatever results from that maximiza-
```
tion is the maximum a-posteriori (MAP) estimator for θ. Because the maximization
```
```
takes place with respect to θ and not x, we can ignore the P(x) part. To make things
```
concrete, let us return to our original coin flipping problem. From our earlier analysis,
we know that the likelihood function for this problem is the following:
```
(θ) := θk (1 − θ) (n−k)
```
where the probability of the coin coming up heads is θ. The next step is the prior
```
probability, P(θ). For this example, we will choose the β(6, 6) distribution (shown in
```
```
the top left panel of Fig. 3.17). The β family of distributions is a gold mine because
```
it allows for a wide variety of distributions using few input parameters. Now that
```
we have all the ingredients, we turn to maximizing the posterior function, P(θ|x).
```
Because the logarithm is convex, we can use it to make the maximization process
easier by converting the product to a sum without changing the extrema that we
```
are looking for. Thus, we prefer the to work with the logarithm of P(θ|x) as in the
```
following.
```
L := log P(θ|x) = log (θ) + log P(θ) − log P(x)
```
This is tedious to do by hand and therefore an excellent job for Sympy.
>>> import sympy>>> from sympy import stats as st
>>> from sympy.abc import p,k,n# setup objective function using sympy.log
```
>>> obj=sympy.expand_log(sympy.log(p**k*(1-p)**(n-k)*st.density(st.Beta(’p’,6,6))(p)))
```
```
# use calculus to maximize objective>>> sol=sympy.solve(sympy.simplify(sympy.diff(obj,p)),p)[0]
```
```
>>> sol(k + 5)/(n + 10)
```
160 3 Statistics
```
Fig. 3.17 The prior probability is the β(6, 6) distribution shown in the top left panel. The dots near
```
the peaks of each of the subgraphs indicate the MAP estimate at that frame
which means that our MAP estimator of θ is the following:
ˆθM A P = k + 5
n + 10
where k is the number of heads in the sample. This is obviously a biased estimator
of θ,
```
E( ˆθM A P ) = 5 + nθ10 + n = θ
```
But is this bias bad? Why would anyone want a biased estimator? Remember that
```
we constructed this entire estimator using the idea of the prior probability of P(θ)
```
```
which favors (biases!) the estimate according to the prior. For example, if θ = 1/2,
```
3.8 Maximum A-Posteriori 161
the MAP estimator evaluates to ˆθM A P = 1/2. No bias there! This is because the peak
of the prior probability is at θ = 1/2.
To compute the corresponding variance for this estimator, we need this interme-
diate result,
```
E( ˆθ2M A P ) = 25 + 10nθ + nθ((n − 1) p + 1)(10 + n)2
```
which gives the following variance,
```
V( ˆθM A P ) = n(1 − θ)θ(n + 10)2
```
```
Let’s pause and compare this to our previous maximum likelihood (ML) estimator
```
shown below:
ˆθM L = 1
n
n∑
```
i=1
```
X i = kn
As we discussed before, the ML-estimator is unbiased with the following variance.
```
V( ˆθM L ) = θ(1 − θ)n
```
How does this variance compare to that of the MAP? The ratio of the two is the
```
following:
```
```
V( ˆθM A P )
```
```
V( ˆθM L )
```
= n
2
```
(n + 10)2
```
This ratio shows that the variance for the MAP-estimator is smaller than that of
the ML-estimator. This is payoff for having a biased MAP-estimator—it requires
fewer samples to estimate if the underlying parameter is consistent with the prior
probability. If not, then it will take more samples to pull the estimator away from the
bias. In the limit as n → ∞, the ratio goes to one. This means that the benefit of the
reduced variance vanishes with enough samples.
The above discussion admits a level of arbitrariness via the prior distribution. We
don’t have to choose just one prior, however. The following shows how we can use
the previous posterior distribution as the prior for the next posterior distribution,
```
P(θ|x k+1) = P(x k+1|θ)P(θ|x k )P(x
```
```
k+1)
```
This is a very different strategy because we are using every data sample x k as a
parameter for the posterior distribution instead of lumping all the samples together
```
in a summation (this is where we got the k term in the prior case). This case is much
```
162 3 Statistics
harder to analyze because now every incremental posterior distribution is itself a
random function because of the injection of the x random variable. On the other
hand, this is more in line with more general Bayesian methods because it is clear
that the output of this estimation process is a posterior distribution function, not just
a single parameter estimate.
Figure 3.17 illustrates this method. The graph in the top row, far left shows the prior
```
probability (β(6, 6)) and the dot on the top shows the most recent MAP-estimate for
```
θ. Thus, before we obtain any data, the peak of the prior probability is the estimate.
The next graph to right shows the effect of x0 = 0 on the incremental prior probability.
Note that the estimate has barely moved to the left. This is because the influence of
```
the data has not caused the prior probability to drift away from the original β(6, 6)-
```
distribution. The first two rows of the figure all have x k = 0 just to illustrate how far
left the original prior probability can be moved by those data. The dots on the tops of
the sub-graphs show how the MAP estimate changes frame-by-frame as more data
is incorporated. The remaining graphs, proceeding top-down, left-to-right show the
incremental change in the prior probability for x k = 1. Again, this shows how far to
the right the estimate can be pulled from where it started. For this example, there are
an equal number of x k = 0 and x k = 1 data, which corresponds to θ = 1/2.
Programming Tip
Although the IPython Notebook accompanying this section has the full source
code, the following is a quick paraphrase of how Fig. 3.17 was constructed.
The first step is to recursively create the posteriors from the data. Note the
example data is sorted to make the progression easy to see as a sequence.from sympy.abc import p,x
```
from scipy.stats import density, Beta, Bernoulliprior = density(Beta(’p’,6,6))(p)
```
```
likelihood=density(Bernoulli(’x’,p))(x)data = (0,0,0,0,0,0,0,1,1,1,1,1,1,1,1)
```
```
posteriors = [prior]for i in data:
```
```
posteriors.append(posteriors[-1]*likelihood.subs(x,i))
```
With the posteriors in hand, the next step is to compute the peak values at each
frame using the fminbound function from Scipy’s optimize module.
```
pvals = linspace(0,1,100)mxvals = []
```
```
for i,j in zip(ax.flat,posteriors):i.plot(pvals,sympy.lambdify(p,j)(pvals),color=’k’)
```
```
mxval = fminbound(sympy.lambdify(p,-j),0,1)mxvals.append(mxval)
```
```
h = i.axis()[-1]i.axis(ymax=h*1.3)
```
```
i.plot(mxvals[-1],h*1.2,’ok’)i.plot(mxvals[:-1],[h*1.2]*len(mxvals[:-1]),’o’)
```
3.8 Maximum A-Posteriori 163
```
Fig. 3.18 For this example, the prior probability is the β(1.3, 1.3) distribution, which has a wider
```
```
main lobe than the β(6, 6) distribution. The dots near the peaks of each of the subgraphs indicate
```
the MAP estimate at that frame
The Fig. 3.18 is the same as Fig. 3.17 except that the initial prior probability is
```
the β(1.3, 1.3)-distribution, which has a wider lobe that the β(6, 6)-distribution. As
```
shown in the figure, this prior has the ability to be swayed more violently one way
or the other based on the x k data that is incorporated. This means that it can more
quickly adapt to data that is not so consistent with the initial prior and thus does not
require a large amount of data in order to unlearn the prior probability. Depending
on the application, the ability to unlearn the prior probability or stick with it is a
design problem for the analyst. In this example, because the data are representative
of a θ = 1/2 parameter, both priors eventually settle on an estimated posterior that
```
is about the same. However, if this had not been the case (θ = 1/2), then the second
```
prior would have produced a better estimate for the same amount of data. 7
7 The IPython Notebook corresponding to this chapter contains the source code sot hat you can try
different combinations of priors and data values.
164 3 Statistics
Fig. 3.19 The credible
interval in Bayesian
maximum a-posteriori is the
interval corresponding to the
shaded region in the
posterior density
Because we have the entire posterior density available, we can compute something
that is closely related to the confidence interval we discussed earlier, except in this
situation, given the Bayesian interpretation, it is called a credible interval or credible
set. The idea is that we want to find a symmetric interval around the peak that accounts
```
for 95 % (say) of the posterior density. This means that we can then say the probability
```
that the estimated parameter is within the credible interval is 95 %. The computation
requires significant numerical processing because even though we have the posterior
density in hand, it is hard to integrate analytically and requires numerical quadrature
```
(see Scipy’s integrate module). Figure 3.19 shows extent of the interval and the
```
shaded region under the posterior density that accounts for 95 %.
3.9 Robust Statistics
```
We considered Maximum Likelihood Estimation (MLE) and Maximum A-Posteriori
```
```
(MAP) estimation and in each case we started out with a probability density function
```
of some kind and we further assumed that the samples were identically distributed and
```
independent (iid). The idea behind robust statistics [3] is to construct estimators that
```
can survive the weakening of either or both of these assumptions. More concretely,
suppose you have a model that works great except for a few outliers. The temptation
is to just ignore the outliers and proceed. Robust estimation methods provide a
disciplined way to handle outliers without cherry-picking data that works for your
favored model.
The Notion of Location. The first notion we need is location, which is a generaliza-
tion of the idea of central value. Typically, we just use an estimate of the mean for
this, but we will see later why this could be a bad idea. The general idea of location
satisfies the following requirements Let X be a random variable with distribution F,
```
and let θ(X) be some descriptive measure of F. Then θ(X) is said to be a measure
```
of location if for any constants a and b, we have the following:
3.9 Robust Statistics 165
```
θ(X + b) = θ(X) + b (3.9.0.1)
```
```
θ(−X) = −θ(X) (3.9.0.2)
```
```
X ≥ 0 ⇒ θ(X) ≥ 0 (3.9.0.3)
```
```
θ(a X) = aθ(X) (3.9.0.4)
```
```
The first condition is called location equivariance (or shift-invariance in signal
```
```
processing lingo). The fourth condition is called scale equivariance, which means
```
that the units that X is measured in should not effect the value of the location estima-
tor. These requirements capture the intuition of centrality of a distribution, or where
most of the probability mass is located.
For example, the sample mean estimator is ˆμ = 1n∑ X i . The first requirement is
```
obviously satisfied as ˆμ = 1n∑(X i + b) = b + 1n∑ X i = b + ˆμ. Let us consider the
```
second requirement: ˆμ = 1n∑ −X i = − ˆμ. Finally, the last requirement is satisfied
with ˆμ = 1n∑ a X i = a ˆμ.
Robust Estimation and Contamination. Now that we have the generalized location
of centrality embodied in the location parameter, what can we do with it? Previously,
we assumed that our samples were all identically distributed. The key idea is that the
samples might be actually coming from a single distribution that is contaminated by
another nearby distribution, as in the following:
```
F(X) = G(X) + (1 − )H (X)
```
where  randomly toggles between zero and one. This means that our data samples
```
{X i } actually derived from two separate distributions, G(X) and H (X). We just
```
don’t know how they are mixed together. What we really want is an estimator that
```
captures the location of G(X) in the face of random intermittent contamination by
```
```
H (X). For example, it may be that this contamination is responsible for the outliers
```
in a model that otherwise works well with the dominant F distribution. It can get
even worse than that because we don’t know that there is only one contaminating
```
H (X) distribution out there. There may be a whole family of distributions that are
```
```
contaminating G(X). This means that whatever estimators we construct have to be
```
derived from a more generalized family of distributions instead of from a single
distribution, as the maximum-likelihood method assumes. This is what makes robust
estimation so difficult—it has to deal with spaces of function distributions instead
of parameters from a particular probability distribution.
Generalized Maximum Likelihood Estimators. M-estimators are generalized
maximum likelihood estimators. Recall that for maximum likelihood, we want to
maximize the likelihood function as in the following:
```
Lμ(x i ) =
```
∏
```
f0(x i − μ)
```
166 3 Statistics
and then to find the estimator ˆμ so that
```
ˆμ = arg maxμ Lμ(x i )
```
So far, everything is the same as our usual maximum-likelihood derivation except
```
for the fact that we don’t assume a specific f0 as the distribution of the {X i }. Making
```
the definition of
ρ = − log f0
we obtain the more convenient form of the likelihood product and the optimal ˆμ as
ˆμ = arg minμ
∑
```
ρ(x i − μ)
```
If ρ is differentiable, then differentiating this with respect to μ gives
∑
```
ψ(x i − ˆμ) = 0 (3.9.0.5)
```
with ψ = ρ′, the first derivative of ρ, and for technical reasons we will assume that ψ
is increasing. So far, it looks like we just pushed some definitions around, but the key
idea is we want to consider general ρ functions that may not be maximum likelihood
estimators for any distribution. Thus, our focus is now on uncovering the nature of ˆμ.
```
Distribution of M-estimates. For a given distribution F, we define μ0 = μ(F) as
```
the solution to the following
```
EF (ψ(x − μ0)) = 0
```
```
It is technical to show, but it turns out that ˆμ ∼ N (μ0, vn ) with
```
```
v = EF (ψ(x − μ0)
```
```
2)
```
```
(EF (ψ′(x − μ0)))2
```
Thus, we can say that ˆμ is asymptotically normal with asymptotic value μ0 and
asymptotic variance v. This leads to the efficiency ratio which is defined as the
```
following:
```
```
Eff( ˆμ) = v0v
```
where v0 is the asymptotic variance of the MLE and measures how near ˆμ is to the
optimum. In other words, this provides a sense of how much outlier contamination
costs in terms of samples. For example, if for two estimates with asymptotic vari-
ances v1 and v2 , we have v1 = 3v2 , then first estimate requires three times as many
observations to obtain the same variance as the second. Furthermore, for the sample
3.9 Robust Statistics 167
```
mean (i.e., ˆμ = 1n∑ X i ) with F = N , we have ρ = x2/2 and ψ = x and also ψ′ = 1.
```
```
Thus, we have v = V(x). Alternatively, using the sample median as the estimator
```
```
for the location, we have v = 1/(4 f (μ0)2). Thus, if we have F = N (0, 1), for the
```
sample median, we obtain v = 2π/4 ≈ 1.571. This means that the sample median
takes approximately 1.6 times as many samples to obtain the same variance for the
location as the sample mean. The sample median is far more immune to the effects
of outliers than the sample mean, so this gives a sense of how much this robustness
costs in samples.
M-Estimates as Weighted Means. One way to think about M-estimates is a weighted
means. Operationally, this means that we want weight functions that can circumscribe
the influence of the individual data points, but, when taken as a whole, still provide
```
good estimated parameters. Most of the time, we have ψ(0) = 0 and ψ′(0) exists so
```
that ψ is approximately linear at the origin. Using the following definition:
```
W (x) =
```
```
{
```
```
ψ(x)/x if x = 0
```
```
ψ′(x) if x = 0
```
We can write our Eq. 3.9.0.5 as follows:
∑
```
W (x i − ˆμ)(x i − ˆμ) = 0 (3.9.0.6)
```
Solving this for ˆμ yields the following,
ˆμ =
∑ w
i x i∑
wi
```
where wi = W (x i − ˆμ). This is not practically useful because the wi contains ˆμ,
```
which is what we are trying to solve for. The question that remains is how to pick the
ψ functions. This is still an open question, but the Huber functions are a well-studied
choice.
Huber Functions. The family of Huber functions is defined by the following:
```
ρk (x) =
```
```
{
```
x2 if |x| ≤ k
2k|x| − k2 if |x| > k
```
with corresponding derivatives 2ψk (x) with
```
```
ψk (x) =
```
```
{
```
x if |x| ≤ k
```
sgn(x)k if |x| > k
```
168 3 Statistics
Fig. 3.20 This shows the
Huber weight function,
```
W2(x) and some cartoon
```
data points that are insiders
or outsiders as far as the
robust location estimate is
concerned
where the limiting cases k → ∞ and k → 0 correspond to the mean and median,
```
respectively. To see this, take ψ∞ = x and therefore W (x) = 1 and thus the defining
```
Eq. 3.9.0.6 results in
n∑
```
i=1
```
```
(x i − ˆμ) = 0
```
and then solving this leads to ˆμ = 1n∑ x i . Note that choosing k = 0 leads to the
sample median, but that is not so straightforward to solve for. Nonetheless, Huber
functions provide a way to move between two extremes of estimators for location
```
(namely, the mean vs. the median) with a tunable parameter k. The W function
```
corresponding to Huber’s ψ is the following:
```
W k (x) = min
```
```
{
```
1, k|x|
```
}
```
Figure 3.20 shows the Huber weight function for k = 2 with some sample points. The
idea is that the computed location, ˆμ is computed from Eq. 3.9.0.6 to lie somewhere
```
in the middle of the weight function so that those terms (i.e., insiders) have their
```
values fully reflected in the location estimate. The black circles are the outliers that
have their values attenuated by the weight function so that only a fraction of their
presence is represented in the location estimate.
Breakdown Point. So far, our discussion of robustness has been very abstract. A
more concrete concept of robustness comes from the breakdown point. In the simplest
terms, the breakdown point describes what happens when a single data point in an
estimator is changed in the most damaging way possible. For example, suppose we
have the sample mean, ˆμ = ∑ x i /n, and we take one of the x i points to be infinite.
What happens to this estimator? It also goes infinite. This means that the breakdown
point of the estimator is 0 %. On the other hand, the median has a breakdown point
of 50 %, meaning that half of the data for computing the median could go infinite
without affecting the median value. The median is a rank statistic that cares more
3.9 Robust Statistics 169
about the relative ranking of the data than the values of the data, which explains its
robustness.
The simpliest but still formal way to express the breakdown point is to take n data
```
points, D = {(x i , yi )}. Suppose T is a regression estimator that yields a vector of
```
regression coefficients, θ,
```
T (D) = θ
```
Likewise, consider all possible corrupted samples of the data D′. The maximum bias
caused by this contamination is the following:
```
biasm = sup
```
D′
```
‖T (D′) − T (D)‖
```
where the sup sweeps over all possible sets of m contaminated samples. Using this,
the breakdown point is defined as the following:
m = min
```
{ m
```
```
n : biasm → ∞
```
```
}
```
For example, in our least-squares regression, even one point at infinity causes an
infinite T . Thus, for least-squares regression, m = 1/n. In the limit n → ∞, we
have m → 0.
Estimating Scale. In robust statistics, the concept of scale refers to a measure of
the dispersion of the data. Usually, we use the estimated standard deviation for this,
but this has a terrible breakdown point. Even more troubling, in order to get a good
estimate of location, we have to either somehow know the scale ahead of time,
or jointly estimate it. None of these methods have easy-to-compute closed form
solutions and must be computed numerically.
The most popular method for estimating scale is the median absolute deviation
```
MAD = Med(|x − Med(x)|)
```
In words, take the median of the data x and then subtract that median from the data
itself, and then take the median of the absolute value of the result. Another good
dispersion estimate is the interquartile range,
```
IQR = x(n−m+1) − x(n)
```
```
where m = [n/4]. The x(n) notation means the nth data element after the data have
```
```
been sorted. Thus, in this notation, max(x) = x(n). In the case where x ∼ N (μ, σ2),
```
then MAD and IQR are constant multiples of σ such that the normalized MAD is the
following,
```
MADN(x) = MAD0.675
```
170 3 Statistics
The number comes from the inverse CDF of the normal distribution corresponding
to the 0.75 level. Given the complexity of the calculations, jointly estimating both
location and scale is a purely numerical matter. Fortunately, the Statsmodels module
has many of these ready to use. Let’s create some contaminated data in the following
code,
import statsmodels.api as smfrom scipy import stats
```
data=np.hstack([stats.norm(10,1).rvs(10),stats.norm(0,1).rvs(100)])
```
These data correspond to our model of contamination that we started this section
with. As shown in the histogram in Fig. 3.21, there are two normal distributions,
one centered neatly at zero, representing the majority of the samples, and another
coming less regularly from the normal distribution on the right. Notice that the group
```
of infrequent samples on the right separates the mean and median estimates (vertical
```
```
dotted and dashed lines). In the absence of the contaminating distribution on the
```
right, the standard deviation for this data should be close to one. However, the usual
```
non-robust estimate for standard deviation (np.std) comes out to approximately
```
```
three. Using the MADN estimator (sm.robust.scale.mad(data)) we obtain
```
approximately 1.25. Thus, the robust estimate of dispersion is less moved by the
presence of the contaminating distribution.
The generalized maximum likelihood M-estimation extends to joint scale and
location estimation using Huber functions. For example,
```
huber = sm.robust.scale.Huber()loc,scl=huber(data)
```
which implements Huber’s proposal two method of joint estimation of location and
scale. This kind of estimation is the key ingredient to robust regression methods,
many of which are implemented in Statsmodels in statsmodels.formula.api
.rlm. The corresponding documentation has more information.
Fig. 3.21 Histogram of sample data. Notice that the group of infrequent samples on the right
separates the mean and median estimates indicated by the vertical lines
3.10 Bootstrapping 171
3.10 Bootstrapping
As we have seen, outside of some toy problems, it can be very difficult or impossible
to determine the probability density distribution of the estimator of some quantity.
The idea behind the bootstrap is that we can use computation to approximate these
functions which would otherwise be impossible to solve for analytically.
Let’s start with a simple example. Suppose we have the following set of random
```
variables, {X1, X2, . . . , X n } where each X k ∼ F. In other words the samples are
```
all drawn from the same unknown distribution F. Having run the experiment, we
thereby obtain the following sample set:
```
{x1, x2, . . . , x n }
```
The sample mean is computed from this set as,
¯x = 1n
n∑
```
i=1
```
x i
```
The next question is how close is the sample mean to the true mean, θ = EF (X).
```
Note that the second central moment of X is as follows:
```
μ2(F) := EF (X2) − (EF (X))2
```
The standard deviation of the sample mean, ¯x, given n samples from an underlying
distribution F, is the following:
```
σ(F) = (μ2(F)/n)1/2
```
```
Unfortunately, because we have only the set of samples {x1, x2, . . . , x n } and not F
```
itself, we cannot compute this and instead must use the estimated standard error,
```
¯σ = ( ¯μ2/n)1/2
```
```
where ¯μ2 = ∑(x i − ¯x)2/(n − 1), which is the unbiased estimate of μ2(F). However,
```
that is not the only way to proceed. Instead, we could replace F by some estimate,
```
ˆF obtained as a piecewise function of {x1, x2, . . . , x n } by placing probability mass
```
1/n on each x i . With that in place, we can compute the estimated standard error as
the following:
```
ˆσB = (μ2( ˆF)/n)1/2
```
which is called the bootstrap estimate of the standard error. Unfortunately, the story
effectively ends here. In even a slightly more general setting, there is no clean formula
```
σ(F) within which F can be swapped for ˆF.
```
172 3 Statistics
This is where the computer saves the day. We actually do not need to know the
```
formula σ(F) because we can compute it using a resampling method. The key idea
```
```
is to sample with replacement from {x1, x2, . . . , x n }. The new set of n independent
```
```
draws (with replacement) from this set is the bootstrap sample,
```
```
y∗ = {x∗1 , x∗2 , . . . , x∗n }
```
The Monte Carlo algorithm proceeds by first by selecting a large number of
```
bootstrap samples, {y∗k }, then computing the statistic on each of these samples, and
```
then computing the sample standard deviation of the results in the usual way. Thus,
the bootstrap estimate of the statistic θ is the following,
ˆθ∗B = 1
B
∑
k
```
ˆθ∗(k)
```
with the corresponding square of the sample standard deviation as
ˆσ2B = 1B − 1
∑
k
```
( ˆθ∗(k) − ˆθ∗B )2
```
The process is much simpler than the notation implies. Let’s explore this with a
simple example using Python. The next block of code sets up some samples from a
```
β(3, 2) distribution,
```
>>> import numpy as np>>> from scipy import stats
```
>>> rv = stats.beta(3,2)>>> xsamples = rv.rvs(50)
```
Because this is simulation data, we already know that the mean is μ1 = 3/5 and the
standard deviation of the sample mean for n = 50 is ¯σ = 1/
√
1250, which we will
verify this later.
```
Figure 3.22 shows the β(3, 2) distribution and the corresponding histogram of the
```
samples. The histogram represents ˆF and is the distribution we sample from to obtain
the bootstrap samples. As shown, the ˆF is a pretty crude estimate for the F density
```
(smooth solid line), but that’s not a serious problem insofar as the following bootstrap
```
estimates are concerned. In fact, the approximation ˆF has a naturally tendency to
```
pull towards where most of the probability mass is. This is a feature, not a bug; and is
```
the underlying mechanism for why bootstrapping works, but the formal proofs that
exploit this basic idea are far out of our scope here. The next block generates the
bootstrap samples
```
>>> yboot = np.random.choice(xsamples,(100,50))>>> yboot_mn = yboot.mean()
```
and the bootstrap estimate is therefore,
```
>>> np.std(yboot.mean(axis=1)) # approx sqrt(1/1250)0.025598763883825811
```
3.10 Bootstrapping 173
```
Fig. 3.22 The β(3, 2) distribution and the histogram that approximates it
```
Fig. 3.23 For each bootstrap draw, we compute the sample mean. This is the histogram of those
sample means that will be used to compute the bootstrap estimate of the standard deviation
Figure 3.23 shows the distribution of computed sample means from the bootstrap
samples. As promised, the next block shows how to use sympy.stats to compute
```
the β(3, 2) parameters we quoted earlier.
```
>>> import sympy as S>>> import sympy.stats
```
>>> for i in range(50): # 50 samples... # load sympy.stats Beta random variables
```
```
... # into global namespace using exec... execstring = "x%d = S.stats.Beta(’x’+str(%d),3,2)"%(i,i)
```
```
... exec(execstring)...
```
>>> # populate xlist with the sympy.stats random variables>>> # from above
```
>>> xlist = [eval(’x%d’%(i)) for i in range(50) ]>>> # compute sample mean
```
```
>>> sample_mean = sum(xlist)/len(xlist)>>> # compute expectation of sample mean
```
```
>>> sample_mean_1 = S.stats.E(sample_mean)>>> # compute 2nd moment of sample mean
```
```
>>> sample_mean_2 = S.stats.E(S.expand(sample_mean**2))>>> # standard deviation of sample mean
```
```
>>> # use sympy sqrt function>>> sigma_smn = S.sqrt(sample_mean_2-sample_mean_1**2) # 1/sqrt(1250)
```
```
>>> print sigma_smnsqrt(2)/50
```
174 3 Statistics
Programming Tip
Using the exec function enables the creation of a sequence of Sympy ran-
dom variables. Sympy has the var function which can automatically create
a sequence of Sympy symbols, but there is no corresponding function in the
statistics module to do this for random variables.
Example Recall the delta method from Sect. 3.4.2. Suppose we have a set of Bernoulli
```
coin-flips (X i ) with probability of head p. Our maximum likelihood estimator of p
```
```
is ˆp = ∑ X i /n for n flips. We know this estimator is unbiased with E( ˆp) = p and
```
```
V( ˆp) = p(1 − p)/n. Suppose we want to use the data to estimate the variance of
```
```
the Bernoulli trials (V(X) = p(1 − p)). By the notation the delta method, g(x) =
```
```
x(1−x). By the plug-in principle, our maximum likelihood estimator of this variance
```
```
is then ˆp(1 − ˆp). We want the variance of this quantity. Using the results of the delta
```
method, we have
```
V(g( ˆp)) = (1 − 2 ˆp)2V( ˆp)
```
```
V(g( ˆp)) = (1 − 2 ˆp)2 ˆp(1 − ˆp)n
```
Let’s see how useful this is with a short simulation.
>>> from scipy import stats>>> import numpy as np
```
>>> p= 0.25 # true head-up probability>>> x = stats.bernoulli(p).rvs(10)
```
>>> print x[0 0 0 0 0 0 1 0 0 0]
The maximum likelihood estimator of p is ˆp = ∑ X i /n,
```
>>> phat = x.mean()>>> print phat
```
0.1
Then, plugging this into the delta method approximant above,
```
>>> print (1-2*phat)**2*(phat)**2/10.0.00064
```
Now, let’s try this using the bootstrap estimate of the variance
```
>>> phat_b=np.random.choice(x,(50,10)).mean(1)>>> print np.var(phat_b*(1-phat_b))
```
0.005049
This shows that the delta method’s estimated variance is different from the bootstrap
method, but which one is better? For this situation we can solve for this directly using
Sympy
3.10 Bootstrapping 175
>>> import sympy as S>>> from sympy.stats import E, Bernoulli
```
>>> xdata =[Bernoulli(i,p) for i in S.symbols(’x:10’)]>>> ph = sum(xdata)/float(len(xdata))
```
```
>>> g = ph*(1-ph)
```
Programming Tip
```
The argument in the S.symbols(’x:10’) function returns a sequence of
```
Sympy symbols named x1,x2 and so on. This is shorthand for creating and
naming each symbol sequentially.
```
Note that g is the g( ˆp) = ˆp(1 − ˆp) whose variance we are trying to estimate. Then,
```
we can plug in for the estimated ˆp and get the correct value for the variance,
```
>>> print E(g**2) - E(g)**20.00442968750000000
```
This case is generally representative—the delta method tends to underestimate the
variance and the bootstrap estimate is better here.
3.10.1 Parametric Bootstrap
```
In the previous example, we used the {x1, x2, . . . , x n } samples themselves as the basis
```
for ˆF by weighting each with 1/n. An alternative is to assume that the samples come
from a particular distribution, estimate the parameters of that distribution from the
sample set, and then use the bootstrap mechanism to draw samples from the assumed
distribution, using the so-derived parameters. For example, the next code block does
this for a normal distribution.
```
>>> rv = stats.norm(0,2)>>> xsamples = rv.rvs(45)
```
```
>>> # estimate mean and var from xsamples>>> mn_ = np.mean(xsamples)
```
```
>>> std_ = np.std(xsamples)>>> # bootstrap from assumed normal distribution with
```
```
>>> # mn_,std_ as parameters>>> rvb = stats.norm(mn_,std_) #plug-in distribution
```
```
>>> yboot = rvb.rvs(1000)
```
Recall the sample variance estimator is the following:
```
S2 = 1n − 1
```
∑
```
(X i − ¯X)2
```
```
Assuming that the samples are normally distributed, this means that (n − 1)S2/σ2
```
has a chi-squared distribution with n − 1 degrees of freedom. Thus, the variance,
```
V(S2) = 2σ4/(n − 1). Likewise, the MLE plug-in estimate for this is V(S2) =
```
```
2 ˆσ4/(n − 1) The following code computes the variance of the sample variance, S2
```
using the MLE and bootstrap methods.
176 3 Statistics
```
>>> # MLE-Plugin Variance of the sample mean>>> print 2*(std_**2)**2/9. # MLE plugin
```
2.22670148618>>> # Bootstrap variance of the sample mean
```
>>> print yboot.var()3.29467885682
```
```
>>> # True variance of sample mean>>> print 2*(2**2)**2/9.
```
3.55555555556
This shows that the bootstrap estimate is better here than the MLE plugin estimate.
Note that this technique becomes even more powerful with multivariate distri-
butions with many parameters because all the mechanics are the same. Thus, the
bootstrap is a great all-purpose method for computing standard errors, but, in the
limit, is it converging to the correct value? This is the question of consistency. Unfor-
tunately, to answer this question requires more and deeper mathematics than we can
get into here. The short answer is that for estimating standard errors, the bootstrap
is a consistent estimator in a wide range of cases and so it definitely belongs in your
toolkit.
3.11 Gauss Markov
In this section, we consider the famous Gauss-Markov problem which will give
us an opportunity to use all the material we have so far developed. The Gauss-
Markov model is the fundamental model for noisy parameter estimation because it
estimates unobservable parameters given a noisy indirect measurement. Incarnations
of the same model appear in all studies of Gaussian models. This case is an excellent
opportunity to use everything we have so far learned about projection and conditional
expectation.
Following Luenberger [4] let’s consider the following problem:
```
y = Wβ + 
```
where W is a n × m matrix, and y is a n × 1 vector. Also,  is a n-dimensional
normally distributed random vector with zero-mean and covariance,
```
E(T ) = Q
```
Note that engineering systems usually provide a calibration mode where you can
estimate Q so it’s not fantastical to assume you have some knowledge of the noise
statistics. The problem is to find a matrix K so that ˆβ = Ky approximates β. Note
that we only have knowledge of β via y so we can’t measure it directly. Further, note
that K is a matrix, not a vector, so there are m × n entries to compute.
3.11 Gauss Markov 177
We can approach this problem the usual way by trying to solve the MMSE
```
problem:
```
```
minK E(‖ ˆβ − β‖2)
```
which we can write out as
```
minK E(‖ ˆβ − β‖2) = minK E(‖Ky − β‖2) = minK E(‖KWβ + K − β‖2)
```
and since  is the only random variable here, this simplifies to
```
minK ‖KWβ − β‖2 + E(‖K‖2)
```
The next step is to compute
```
E(‖K‖2) = E(T KT KT ) = Tr(KE(T)KT ) = Tr(KQKT )
```
using the properties of the trace of a matrix. We can assemble everything as
```
minK ‖KWβ − β‖2 + Tr(KQKT )
```
Now, if we were to solve this for K, it would be a function of β, which is the same
thing as saying that the estimator, ˆβ, is a function of what we are trying to estimate,
β, which makes no sense. However, writing this out tells us that if we had KW = I,
then the first term vanishes and the problem simplifies to
```
minK Tr(KQKT )
```
with the contraint,
```
KW = I
```
This requirement is the same as asserting that the estimator is unbiased,
```
E( ˆβ) = KWβ = β
```
To line this problem up with our earlier work, let’s consider the ith column of K, ki .
Now, we can re-write the problem as
```
mink (kTi Qki )
```
178 3 Statistics
with
kTi W = ei
and from our previous work on contrained optimization, we know the solution to
```
this:
```
```
ki = Q−1W(WT Q−1 W)−1ei
```
Now all we have to do is stack these together for the general solution:
```
K = (WT Q−1 W)−1WT Q−1
```
It’s easy when you have all of the concepts lined up! For completeness, the covariance
of the error is
```
E( ˆβ − β)( ˆβ − β)T = E(KT KT ) = KQKT = (WT Q−1W)−1
```
Figure 3.24 shows the simulated y data as red circles. The black dots show the
corresponding estimates, ˆβ for each sample. The black lines show the true value of β
versus the average of the estimated β-values,̂ βm . The matrix K maps the red circles
in the corresponding dots. Note there are many possible ways to map the red circles
to the plane, but the K is the one that minimizes the MSE for β.
Fig. 3.24 The red circles
show the points to be
estimated in the xy-plane by
the black points
3.11 Gauss Markov 179
Fig. 3.25 Focusing on the
xy-plane in Fig. 3.24, the
dashed line shows the true
value for β versus the mean
of the estimated valueŝ βm
Programming Tip
Although the full source code is available in the corresponding IPython Note-
book, the following snippets provide a quick walkthrough. To simulate the
target data, we define the relevant matrices below,
```
Q = np.eye(3)*0.1 # error covariance matrix# this is what we are trying estimate
```
```
beta = matrix(ones((2,1)))W = matrix([ [1,2],
```
```
[2,3],[1,1] ])
```
Then, we generate the noise terms and create the simulated data, y,
```
ntrials = 50epsilon = np.random.multivariate_normal((0,0,0),Q,ntrials).T
```
```
y=W*beta+epsilon
```
Figure 3.25 shows more detail in the horizontal xy-plane of Fig. 3.24. Figure 3.25
shows the dots, which are individual estimates of ˆβ from the corresponding simulated
```
y data. The dashed line is the true value for β and the filled line (̂ βm ) is the average
```
of all the dots. The gray ellipse provides an error ellipse for the covariance of the
estimated β values.
Programming Tip
Although the full source code is available in the corresponding IPython Note-
book, the following snippets provide a quick walkthrough of the construction
of Fig. 3.25. To draw the ellipse, we need to import the patch primitive,
from matplotlib.patches import Ellipse
To compute the parameters of the error ellipse based on the covariance matrix
of the individual estimates of β in the bm_cov variable below,
180 3 Statistics
```
U,S,V = linalg.svd(bm_cov)err = np.sqrt((matrix(bm))*(bm_cov)*(matrix(bm).T))
```
```
theta = np.arccos(U[0,1])/np.pi*180
```
Then, we draw the add the scaled ellipse in the following,
```
ax.add_patch(Ellipse(bm,err*2/np.sqrt(S[0]),err*2/np.sqrt(S[1]),
```
```
angle=theta,color=’gray’))
```
3.12 Nonparametric Methods
So far, we have considered parametric methods that reduce inference or prediction to
parameter-fitting. However, for these to work, we had to assume a specific functional
form for the unknown probability distribution of the data. Nonparametric methods
eliminate the need to assume a specific functional form by generalizing to classes of
functions.
3.12.1 Kernel Density Estimation
We have already made heavy use of this method with the histogram, which is a
special case of kernel density estimation. The histogram can be considered the crudest
and most useful nonparametric method, that estimates the underlying probability
distribution of the data.
To be formal and place the histogram on the same footing as our earlier estimations,
suppose that X = [0, 1]d is the d dimensional unit cube and that h is the bandwidth
```
or size of a bin or sub-cube. Then, there are N ≈ (1/ h)d such bins, each with
```
```
volume h d , {B1, B2, . . . , B N }. With all this in place, we can write the histogram has
```
a probability density estimator of the form,
```
ˆp h (x) =
```
N∑
```
k=1
```
ˆθk
```
h I (x ∈ Bk )
```
where
ˆθk = 1
n
n∑
```
j=1
```
```
I (X j ∈ Bk )
```
```
is the fraction of data points (X k ) in each bin, Bk . We want to bound the bias and
```
```
variance of ˆp h (x). Keep in mind that we are trying to estimate a function of x, but
```
the set of all possible probability distribution functions is extremely large and hard to
3.12 Nonparametric Methods 181
manage. Thus, we need to restrict our attention to the following class of probability
distribution of so-called Lipschitz functions,
```
P(L) = { p : | p(x) − p(y)| ≤ L‖x − y‖, ∀ x, y}
```
```
Roughly speaking, these are the density functions whose slopes (i.e., growth rates)
```
are bounded by L. It turns out that the bias of the histogram estimator is bounded in
the following way,
∫
```
| p(x) − E( ˆp h (x))|dx ≤ Lh
```
√
d
Similarly, the variance is bounded by the following,
```
V( ˆp h (x)) ≤ Cnh d
```
for some constant C. Putting these two facts together means that the risk is
bounded by,
```
R( p, ˆp) =
```
∫
```
E( p(x) − ˆp h (x))2dx ≤ L2h2d + Cnh d
```
This upper bound is minimized by choosing
```
h =
```
```
( C
```
L2nd
```
) 1d+2
```
In particular, this means that,
sup
```
p∈P(L)
```
```
R( p, ˆp) ≤ C0
```
```
( 1
```
n
```
) 2d+2
```
where the constant C0 is a function of L. There is a theorem [2] that shows this bound
in tight, which basically means that the histogram is a really powerful probability
density estimator for Lipschitz functions with risk that goes as
```
( 1
```
n
```
) 2d+2
```
. Note that this
class of functions is not necessarily smooth because the Lipschitz condition admits
non-smooth functions. While this is a reassuring result, we typically do not know
```
which function class (Lipschitz or not) a particular probability belongs to ahead of
```
time. Nonetheless, the rate at which the risk changes with both dimension d and
n samples would be hard to understand without this result. Figure 3.26 shows the
```
probability distribution function of the β(2, 2) distribution compared to computed
```
histograms for different values of n. The box plots on each of the points show
how the variation in each bin of the histogram reduces with increasing n. The risk
```
function R( p, ˆp) above is based upon integrating the squared difference between the
```
```
histogram (as a piecewise function of x) and the probability distribution function.
```
182 3 Statistics
Fig. 3.26 The box plots on each of the points show how the variation in each bin of the histogram
reduces with increasing n
Programming Tip
The corresponding IPython notebook has the complete source code that gen-
```
erates Fig. 3.26; however, the following snippet is the main element of the
```
code.
```
def generate_samples(n,ntrials=500):phat = np.zeros((nbins,ntrials))
```
```
for k in range(ntrials):d = rv.rvs(n)
```
```
phat[:,k],_=histogram(d,bins,density=True)return phat
```
The code uses the histogram function from Numpy. To be consistent
```
with the risk function R( p, ˆp), we have to make sure the bins keyword
```
argument is formatted correctly using a sequence of bin-edges instead of just a
single integer. Also, the density=True keyword argument normalizes the
histogram appropriately so that the comparison between it and the probability
distribution function of the simulated beta distribution is correctly scaled.
3.12 Nonparametric Methods 183
3.12.2 Kernel Smoothing
We can extend our methods to other function classes using kernel functions. A one-
dimensional smoothing kernel is a smooth function K with the following properties,
∫
```
K (x)dx = 1
```
∫
```
x K (x)dx = 0
```
0 <
∫
```
x2 K (x)dx < ∞
```
```
For example, K (x) = I (x)/2 is the boxcar kernel, where I (x) = 1 when |x| ≤ 1
```
and zero otherwise. The kernel density estimator is very similar to the histogram,
except now we put a kernel function on every point as in the following,
```
ˆp(x) = 1n
```
n∑
```
i=1
```
1
h d K
```
( ‖x − X
```
i ‖
h
```
)
```
where X ∈ Rd . Figure 3.27 shows an example of a kernel density estimate using a
```
Gaussian kernel function, K (x) = e−x2 /2/
```
√
2π. There are five data points shown
```
by the vertical lines in the upper panel. The dotted lines show the individual K (x)
```
```
function at each of the data points. The lower panel shows the overall kernel density
```
estimate, which is the scaled sum of the upper panel.
There is an important technical result in [2] that states that kernel density estima-
tors are minimax in the sense we discussed in the maximum likelihood Sect. 3.4. In
broad strokes, this means that the analogous risk for the kernel density estimator is
approximately bounded by the following factor,
```
R( p, ˆp)  n− 2m2m+d
```
for some constant C where m is a factor related to bounding the derivatives of the
probability density function. For example, if the second derivative of the density
```
function is bounded, then m = 2. This means that the convergence rate for this
```
estimator decreases with increasing dimension d.
Cross-Validation. As a practical matter, the tricky part of the kernel density esti-
```
mator (which includes the histogram as a special case) is that we need to somehow
```
compute the bandwidth h term using data. There are several rule-of-thumb meth-
ods that for some common kernels, including Silverman’s rule and Scott’s rule for
```
Gaussian kernels. For example, Scott’s factor is to simply compute h = n−1/(d+4) and
```
```
Silverman’s is h = (n(d +2)/4)(−1/(d+4)). Rules of this kind are derived by assuming
```
184 3 Statistics
Fig. 3.27 The upper panel
shows the individual kernel
functions placed at each of
the data points. The lower
panel shows the composite
kernel density estimate
which is the sum of the
individual functions in the
upper panel
```
the underlying probability density function is of a certain family (e.g., Gaussian),
```
and then deriving the best h for a certain type of kernel density estimator, usually
```
equipped with extra functional properties (say, continuous derivatives of a certain
```
```
order). In practice, these rules seem to work pretty well, especially for uni-modal
```
probability density functions. Avoiding these kinds of assumptions means computing
the bandwidth from data directly and that is where cross validation comes in.
Cross-validation is a method to estimate the bandwidth from the data itself. The
```
idea is to write out the following Integrated Squared Error (ISE),
```
```
ISE( ˆp h , p) =
```
∫
```
( p(x) − ˆp h (x))2dx
```
=
∫
```
ˆp h (x)2dx − 2
```
∫
```
p(x) ˆp h dx +
```
∫
```
p(x)2dx
```
The problem with this expression is the middle term, 8
∫
```
p(x) ˆp h dx
```
```
where p(x) is what we are trying to estimate with ˆp h . The form of the last expression
```
```
looks like an expectation of ˆp h over the density of p(x), E( ˆp h ). The approach is to
```
approximate this with the mean,
```
E( ˆp h ) ≈ 1n
```
n∑
```
i=1
```
```
ˆp h (X i )
```
The problem with this approach is that ˆp h is computed using the same data that the
approximation utilizes. The way to get around this is to split the data into two equally
```
sized chunks D1 , D2 ; and then compute ˆp h for a sequence of different h values over
```
8 The last term is of no interest because we are only interested in relative changes in the ISE.
3.12 Nonparametric Methods 185
```
the D1 set. Then, when we apply the above approximation for the data (Z i ) in the
```
D2 set,
```
E( ˆp h ) ≈ 1|D
```
2|
∑
Z i ∈D2
```
ˆp h (Z i )
```
Plugging this approximation back into the integrated squared error provides the
objective function,
ISE ≈
∫
```
ˆp h (x)2dx − 2|D
```
2|
∑
Z i ∈D2
```
ˆp h (Z i )
```
Some code will make these steps concrete. We will need some tools from Scikit-learn.
>>> from sklearn.cross_validation import train_test_split>>> from sklearn.neighbors.kde import KernelDensity
The train_test_split function makes it easy to split and keep track of the D1
and D2 sets we need for cross validation. Scikit-learn already has a powerful and
flexible implementation of kernel density estimators. To compute the objective func-
tion, we need some basic numerical integration tools from Scipy. For this example,
```
we will generate samples from a β(2, 2) distribution, which is implemented in the
```
stats submodule in Scipy.
>>> from scipy.integrate import quad>>> from scipy import stats
```
>>> rv= stats.beta(2,2)>>> n=100 # number of samples to generate
```
```
>>> d = rv.rvs(n)[:,None] # generate samples as column-vector
```
Programming Tip
The use of the [:,None] in the last line formats the Numpy array returned by
the rvs function into a Numpy vector with a column dimension of one. This is
required by the KernelDensity constructor because the column dimension
```
is used for different features (in general) for Scikit-learn. Thus, even though
```
we only have one feature, we still need to comply with the structured input
that Scikit-learn relies upon. There are many ways to inject the additional
dimension other than using None. For example, the more cryptic, np.c_, or
the less cryptic [:,np.newaxis] can do the same, as can the np.reshape
function.
The next step is to split the data into two halves and loop over each of the h i band-
widths to create a separate kernel density estimator based on the D1 data,
```
>>> train,test,_,_=train_test_split(d,d,test_size=0.5)>>> kdes=[KernelDensity(bandwidth=i).fit(train)
```
... for i in [.05,0.1,0.2,0.3] ]
186 3 Statistics
Programming Tip
Note that the single underscore symbol in Python refers to the last evaluated
result. the above code unpacks the tuple returned by train_test_split
into four elements. Because we are only interested in the first two, we assign
the last two to the underscore symbol. This is a stylistic usage to make it clear
to the reader that the last two elements of the tuple are unused. Alternatively,
we could assign the last two elements to a pair of dummy variables that we
do not use later, but then the reader skimming the code may think that those
dummy variables are relevant.
The last step is to loop over the so-created kernel density estimators and compute
the objective function.
>>> import numpy as np>>> for i in kdes:
```
... f = lambda x: np.exp(i.score_samples(x))... f2 = lambda x: f(x)**2
```
```
... print ’h=%3.2f\t %3.4f’%(i.bandwidth,quad(f2,0,1)[0]... -2*np.mean(f(test)))
```
...h=0.05 -1.1323
```
h=0.10 -1.1336h=0.20 -1.1330
```
```
h=0.30 -1.0810
```
Programming Tip
The lambda functions defined in the last block are necessary because Scikit-
learn implements the return value of the kernel density estimator as a logarithm
via the score_samples function. The numerical quadrature function quad
from Scipy computes the
∫
```
ˆp h (x)2dx part of the objective function.
```
Scikit-learn has many more advanced tools to automate this kind of hyper-
```
parameter (i.e., kernel density bandwidth) search. To utilize these advanced tools,
```
we need to format the current problem slightly differently by defining the following
```
wrapper class (Fig. 3.28).
```
```
>>> class KernelDensityWrapper(KernelDensity):... def predict(self,x):
```
```
... return np.exp(self.score_samples(x))... def score(self,test):
```
```
... f = lambda x: self.predict(x)... f2 = lambda x: f(x)**2
```
```
... return -(quad(f2,0,1)[0]-2*np.mean(f(test)))...
```
This is tantamount to reorganizing the above previous code into functions that Scikit-
learn requires. Next, we create the dictionary of parameters we want to search over
```
(params) below and then start the grid search with the fit function,
```
3.12 Nonparametric Methods 187
Fig. 3.28 Each line above is a different kernel density estimator for the given bandwidth as an
approximation to the true density function. A plain histogram is imprinted on the bottom for reference
```
>>> from sklearn.grid_search import GridSearchCV>>> params = {’bandwidth’:np.linspace(0.01,0.5,10)}
```
```
>>> clf = GridSearchCV(KernelDensityWrapper(), param_grid=params,cv=2)>>> clf.fit(d)
```
```
GridSearchCV(cv=2,estimator=KernelDensityWrapper(algorithm=’auto’,atol=0,bandwidth=1.0,
```
```
breadth_first=True,kernel=’gaussian’,leaf_size=40,metric=’euclidean’,metric_params=None,rtol=0),
```
```
fit_params={},iid=True,loss_func=None,n_jobs=1,param_grid={’bandwidth’:array([0.01,0.06444,0.11889,0.17333,0.22778,0.28222,
```
```
0.33667,0.39111,0.44556,0.5])},pre_dispatch=’2*n_jobs’,refit=True,score_func=None,scoring=None, verbose=0)
```
```
>>> print clf.best_params_{’bandwidth’: 0.17333333333333334}
```
The grid search iterates over all the elements in the params dictionary and reports
the best bandwidth over that list of parameter values. The cv keyword argument
above specifies that we want to split the data into two equally-sized sets for training
and testing. We can also examine the values of the objective function for each point
on the grid as follow,
```
>>> from pprint import pprint>>> pprint(clf.grid_scores_)
```
```
[mean: 0.60758, std: 0.07695, params: {’bandwidth’: 0.01},mean: 1.06325, std: 0.03866, params: {’bandwidth’: 0.064444444444444443},
```
```
mean: 1.11859, std: 0.02093, params: {’bandwidth’: 0.11888888888888888},mean: 1.13187, std: 0.01397, params: {’bandwidth’: 0.17333333333333334},
```
```
mean: 1.12007, std: 0.01043, params: {’bandwidth’: 0.22777777777777777},mean: 1.09186, std: 0.00794, params: {’bandwidth’: 0.28222222222222221},
```
```
mean: 1.05391, std: 0.00601, params: {’bandwidth’: 0.33666666666666667},mean: 1.01126, std: 0.00453, params: {’bandwidth’: 0.39111111111111108},
```
```
mean: 0.96717, std: 0.00341, params: {’bandwidth’: 0.44555555555555554},mean: 0.92355, std: 0.00257, params: {’bandwidth’: 0.5}]
```
188 3 Statistics
Programming Tip
The pprint function makes the standard output prettier. The only reason for
using it here is to get it to look good on the printed page. Otherwise, the IPython
notebook handles the visual rendering of output embedded in the notebook via
its internal display framework.
Keep in mind that the grid search examines multiple folds for cross validation
to compute the above means and standard deviations. Note that there is also a
RandomizedSearchCV in case you would rather specify a distribution of para-
meters instead of a list. This is particularly useful for searching very large parameter
spaces where an exhaustive grid search would be too computationally expensive.
Although kernel density estimators are easy to understand and have many attractive
analytical properties, they become practically prohibitive for large, high-dimensional
data sets.
3.12.3 Nonparametric Regression Estimators
Beyond estimating the underlying probability density, we can use nonparametric
methods to compute estimators of the underlying function that is generating the
data. Nonparametric regression estimators of the following form are known as linear
smoothers,
```
ˆy(x) =
```
n∑
```
i=1
```
```
i (x)yi
```
To understand the performance of these smoothers, we can define the risk as the
following,
```
R( ˆy, y) = E
```
```
(
```
1
n
n∑
```
i=1
```
```
( ˆy(x i ) − y(x i ))2
```
```
)
```
and find the best ˆy that minimizes this. The problem with this metric is that we do
```
not know y(x), which is why we are trying to approximate it with ˆy(x). We could
```
construct an estimation by using the data at hand as in the following,
```
ˆR( ˆy, y) = 1
```
n
n∑
```
i=1
```
```
( ˆy(x i ) − Yi )2
```
```
where we have substituted the data Yi for the unknown function value, y(x i ). The
```
problem with this approach is that we are using the data to estimate the function and
3.12 Nonparametric Methods 189
then using the same data to evaluate the risk of doing so. This kind of double-dipping
leads to overly optimistic estimators. One way out of this conundrum is to use leave-
one-out cross validation, wherein the ˆy function is estimated using all but one of the
```
data pairs, (X i , Yi ). Then, this missing data element is used to estimate the above
```
risk. Notationally, this is written as the following,
```
ˆR( ˆy, y) = 1
```
n
n∑
```
i=1
```
```
( ˆy(−i) (x i ) − Yi )2
```
```
where ˆy(−i) denotes computing the estimator without using the ith data pair. Unfortu-
```
nately, for anything other than relatively small data sets, it quickly becomes compu-
tationally prohibitive to use leave-one-out cross validation in practice. We’ll get back
to this issue shortly, but let’s consider a concrete example of such a nonparametric
smoother.
3.12.4 Nearest Neighbors Regression
The simplest possible nonparametric regression method is the k-nearest neighbors
regression. This is easier to explain in words than to write out in math. Given an input
x, find the closest one of the k clusters that contains it and then return the mean of
the data values in that cluster. As a univariate example, let’s consider the following
chirp waveform,
```
y(x) = cos
```
```
(
```
2π
```
(
```
f o x + BW x
2
2τ
```
))
```
This waveform is important in high-resolution radar applications. The f o is the start
frequency and BW/τ is the frequency slope of the signal. For our example, the fact
that it is nonuniform over its domain is important. We can easily create some data
by sampling the chirp as in the following,
>>> import numpy as np>>> from numpy import cos, pi
```
>>> xi = np.linspace(0,1,100)[:,None]>>> xin = np.linspace(0,1,12)[:,None]
```
>>> f0 = 1 # init frequency>>> BW = 5
```
>>> y = cos(2*pi*(f0*xin+(BW/2.0)*xin**2))
```
We can use this data to construct a simple nearest neighbor estimator using Scikit-
learn,
```
>>> from sklearn.neighbors import KNeighborsRegressor>>> knr=KNeighborsRegressor(2)
```
```
>>> knr.fit(xin,y)KNeighborsRegressor(algorithm=’auto’,leaf_size=30,metric=’minkowski’,
```
```
metric_params=None,n_neighbors=2,p=2,weights=’uniform’)
```
190 3 Statistics
Fig. 3.29 The dotted line shows the chirp signal and the solid line shows the nearest neighbor
estimate. The gray circles are the sample points that we used to fit the nearest neighbor estimator.
The shaded area shows the gaps between the estimator and the unsampled chirp
Programming Tip
Scikit-learn has a fantastically consistent interface. The fit function above
fits the model parameters to the data. The corresponding predict function
returns the output of the model given an arbitrary input. We will spend a lot
more time on Scikit-learn in the machine learning chapter. The [:,None]
part at the end is just injecting a column dimension into the array in order to
satisfy the dimensional requirements of Scikit-learn.
```
Figure 3.29 shows the sampled signal (gray circles) against the values generated by
```
```
the nearest neighbor estimator (solid line). The dotted line is the full unsampled
```
chirp signal, which increases in frequency with x. This is important for our example
because it adds a non-stationary aspect to this problem in that the function gets
progressively wigglier with increasing x. The area between the estimated curve and
the signal is shaded in gray. Because the nearest neighbor estimator uses only two
nearest neighbors, for each new x, it finds the two adjacent X i that bracket the x
in the training data and then averages the corresponding Yi values to compute the
estimated value. That is, if you take every adjacent pair of sequential gray circles in
the Figure, you find that the horizontal solid line splits the pair on the vertical axis.
We can adjust the number of nearest neighbors by changing the constructor,
```
>>> knr=KNeighborsRegressor(3)>>> knr.fit(xin,y)
```
```
KNeighborsRegressor(algorithm=’auto’,leaf_size=30,metric=’minkowski’,metric_params=None,n_neighbors=3,p=2,weights=’uniform’)
```
3.12 Nonparametric Methods 191
Fig. 3.30 This is the same as Fig. 3.29 except that here there are three nearest neighbors used to
build the estimator
which produces the following corresponding Fig. 3.30.
For this example, Fig. 3.30 shows that with more nearest neighbors the fit performs
poorly, especially towards the end of the signal, where there is increasing variation,
because the chirp is not uniformly continuous.
Scikit-learn provides many tools for cross validation. The following code sets up
the tools for leave-one-out cross validation,
```
>>> from sklearn.cross_validation import LeaveOneOut>>> loo=LeaveOneOut(len(xin))
```
The LeaveOneOut object is an iterable that produces a set of disjoint indices of
```
the data—one for fitting the model (training set) and one for evaluating the model
```
```
(testing set), as shown in the next short sample,
```
```
>>> pprint(list(LeaveOneOut(3)))[(array([1, 2]), array([0])),
```
```
(array([0, 2]), array([1])),(array([0, 1]), array([2]))]
```
The next block loops over the disjoint sets of training and test indicies iterates pro-
vided by the loo variable to evaluate the estimated risk, which is accumulated in
the out list.
>>> out=[]>>> for train_index, test_index in loo:
```
... _=knr.fit(xin[train_index],y[train_index])... out.append((knr.predict(xi[test_index])-y[test_index])**2)
```
```
...>>> print ’Leave-one-out Estimated Risk: ’,np.mean(out),
```
Leave-one-out Estimated Risk: 1.03517136627
The last line in the code above reports leave-one-out’s estimated risk.
Linear smoothers of this type can be rewritten in using the following matrix,
```
S =
```
[
```
i (x j )
```
]
i, j
192 3 Statistics
so that
ˆy = Sy
where y = [Y1, Y2, . . . , Yn ] ∈ Rn and ˆy =
[
```
ˆy(x1), ˆy(x2), . . . , ˆy(x n )
```
]
∈ Rn . This
leads to a quick way to approximate leave-one-out cross validation as the following,
ˆR = 1
n
n∑
```
i=1
```
```
( y
```
```
i − ˆy(x i )
```
1 − Si,i
```
)2
```
However, this does not reproduce the approach in the code above because it assumes
```
that each ˆy(−i) (x i ) is consuming one fewer nearest neighbor than ˆy(x).
```
We can get this S matrix from the knr object as in the following,
```
>>> _= knr.fit(xin,y) # fit on all data>>> S=(knr.kneighbors_graph(xin)).todense()/float(knr.n_neighbors)
```
The todense part reformats the sparse matrix that is returned into a regular Numpy
matrix. The following shows a subsection of this S matrix,
>>> print S[:5,:5][ [ 0.33333333 0.33333333 0.33333333 0. 0. ]
[ 0.33333333 0.33333333 0.33333333 0. 0. ][ 0. 0.33333333 0.33333333 0.33333333 0. ]
[ 0. 0. 0.33333333 0.33333333 0.33333333][ 0. 0. 0. 0.33333333 0.33333333] ]
The sub-blocks show the windows of the y data that are being processed by the
nearest neighbor estimator. For example,
```
>>> print np.hstack([knr.predict(xin[:5]),(S*y)[:5] ])#columns match[ [ 0.55781314 0.55781314]
```
[ 0.55781314 0.55781314][-0.09768138 -0.09768138]
[-0.46686876 -0.46686876][-0.10877633 -0.10877633] ]
Or, more concisely checking all entries for approximate equality,
```
>>> print np.allclose(knr.predict(xin),S*y)True
```
which shows that the results from the nearest neighbor object and the matrix multiply
match.
Programming Tip
Note that because we formatted the returned S as a Numpy matrix, we auto-
matically get the matrix multiplication instead of default element-wise multi-
plication in the S*y term.
3.12 Nonparametric Methods 193
3.12.5 Kernel Regression
For estimating the probability density, we started with the histogram and moved to
the more general kernel density estimate. Likewise, we can also extend regression
from nearest neighbors to kernel-based regression using the Nadaraya-Watson kernel
regression estimator. Given a bandwidth h > 0, the kernel regression estimator is
defined as the following,
```
ˆy(x) =
```
∑n
```
i=1 K
```
```
( x−x i
```
h
```
)
```
Yi∑
```
ni=1 K ( x−x i
```
h
```
)
```
```
Unfortunately, Scikit-learn does not implement this regression estimator; however,
```
Jan Hendrik Metzen makes a compatible version available on github.com.
>>> from kernel_regression import KernelRegression
This code makes it possible to internally optimize over the bandwidth parameter
using leave-one-out cross validation by specifying a grid of potential bandwidth
```
values (gamma), as in the following,
```
```
>>> kr = KernelRegression(gamma=np.linspace(6e3,7e3,500))>>> kr.fit(xin,y)
```
```
KernelRegression(gamma=6000.0,kernel=’rbf’)
```
```
Figure 3.31 shows the kernel estimator (heavy black line) using the Gaussian kernel
```
```
compared to the nearest neighbor estimator (solid light black line). As before, the
```
data points are shown as circles. Figure 3.31 shows that the kernel estimator can pick
out the sharp peaks that are missed by the nearest neighbor estimator.
Fig. 3.31 The heavy black line is the Gaussian kernel estimator. The light black line is the nearest
neighbor estimator. The data points are shown as gray circles. Note that unlike the nearest neighbor
estimator, the Gaussian kernel estimator is able to pick out the sharp peaks in the training data
194 3 Statistics
Thus, the difference between nearest neighbor and kernel estimation is that the
latter provides a smooth moving averaging of points whereas the former provides a
discontinuous averaging. Note that kernel estimates suffer near the boundaries where
there is mismatch between the edges and the kernel function. This problem gets
worse in higher dimensions because the data naturally drift towards the boundaries
```
(this is a consequence of the curse of dimensionality). Indeed, it is not possible to
```
```
simultaneously maintain local accuracy (i.e., low bias) and a generous neighborhood
```
```
(i.e., low variance). One way to address this problem is to create a local polynomial
```
regression using the kernel function as a window to localize a region of interest. For
example,
```
ˆy(x) =
```
n∑
```
i=1
```
K
```
( x − x
```
i
h
```
)
```
```
(Yi − α − βx i )2
```
and now we have to optimize over the two linear parameters α and β. This method
is known as local linear regression [5, 6]. Naturally, this can be extended to higher-
order polynomials. Note that these methods are not yet implemented in Scikit-learn.
3.12.6 Curse of Dimensionality
The so-called curse of dimensionality occurs as we move into higher and higher
dimensions. The term was coined by Bellman in 1961 while he was studying adaptive
control processes. Nowadays, the term is vaguely refers to anything that becomes
more complicated as the number of dimensions increases substantially. Nevertheless,
the concept is useful for recognizing and characterizing the practical difficulties of
high-dimensional analysis and estimation.
Consider the volume of an n-dimensional sphere,
```
Vs (n, r) =
```
```
{
```
```
πn/2 r n(n/2)! if n is even
```
```
2n π(n−1)/2 r(n−1)(n−1)! ((n − 1)/2)! if n is odd (3.12.6.1)
```
```
Further, consider the sphere Vs (n, 1/2) enclosed by an n dimensional unit cube. The
```
```
volume of the cube is always equal to one, but limn→∞ Vs (n, 1/2) = 0. What does
```
this mean? It means that the volume of the cube is pushed away from its center,
where the embedded hypersphere lives. Specifically, the distance from the center of
the cube to its vertices in n dimensions is √n/2, whereas the distance from the center
of the inscribing sphere is 1/2. This diagonal distance goes to infinity as n does. For
a fixed n, the tiny spherical region at the center of the cube has many long spines
attached to it, like a hyper-dimensional sea urchin or porcupine.
3.12 Nonparametric Methods 195
Fig. 3.32 Two dimensional scatter of points randomly and independently uniformly distributed in
the unit square. Note that most of the points are contained in the circle. Counter to intuition, this
does not persist as the number of dimensions increases
What are the consequences of this? For methods that rely on nearest neighbors,
exploiting locality to lower bias becomes intractable. For example, suppose we have
an n dimensional space and a point near the origin we want to localize around.
To estimate behavior around this point, we need to average the unknown function
about this point, but in a high-dimensional space, the chances of finding neighbors
to average are slim. Looked at from the opposing point of view, suppose we have a
binary variable, as in the coin-flipping problem. If we have 1000 trials, then, based
on our earlier work, we can be confident about estimating the probability of heads.
Now, suppose we have 10 binary variables. Now we have 2 10 = 1024 vertices to
estimate. If we had the same 1000 points, then at least 24 vertices would not get any
data. To keep the same resolution, we would need 1000 samples at each vertex for
a grand total of 1000 × 1024 ≈ 10 6 data points. So, for a ten fold increase in the
number of variables, we now have about 1000 more data points to collect to maintain
the same statistical resolution. This is the curse of dimensionality.
Perhaps some code will clarify this. The following code generates samples in two
dimensions that are plotted as points in Fig. 3.32 with the inscribed circle in two
dimensions. Note that for d = 2 dimensions, most of the points are contained in the
circle.
```
>>> import numpy as np>>> v=np.random.rand(1000,2)-1/2.
```
The next code block describes the core computation in Fig. 3.33. For each of the
dimensions, we create a set of uniformly distributed random variates along each
dimension and then compute how close each d dimensional vector is to the origin.
Those that measure one half are those contained in the hypersphere. The histogram
196 3 Statistics
Fig. 3.33 Each panel shows the histogram of lengths of uniformly distributed d dimensional
random vectors. The population to the left of the dark vertical line are those that are contained
in the inscribed hypersphere. This shows that fewer points are contained in the hypersphere with
increasing dimension
of each measurement is shown in the corresponding panel in the Fig. 3.33. The dark
vertical line shows the threshold value. Values to the left of this indicate the population
that are contained in the hypersphere. Thus, Fig. 3.33 shows that as d increases, fewer
points are contained in the inscribed hypersphere. The following code paraphrases
the content of Fig. 3.33
```
for d in [2,3,5,10,20,50]:v=np.random.rand(5000,d)-1/2.
```
```
hist([np.linalg.norm(i) for i in v])
```
References
1. W. Feller, An Introduction to Probability Theory and Its Applications: Volume One (Wiley, 1950)
2. L. Wasserman, All of Statistics: a Concise Course in Statistical Inference (Springer, 2004)
3. R.A. Maronna, D.R. Martin, V.J. Yohai, Robust Statistics: Theory and Methods, Wiley Series in
```
Probability and Statistics (Wiley, Chichester, 2006)
```
4. D.G. Luenberger, Optimization by Vector Space Methods, Professional Series (Wiley, 1968)
5. C. Loader, Local Regression and Likelihood (Springer, New York, 2006)
6. T. Hastie, R. Tibshirani, J. Friedman, The Elements of Statistical Learning: Data Mining, Infer-
```
ence, and Prediction, Springer Series in Statistics (Springer, New York, 2013)
```
Chapter 4
Machine Learning
4.1 Introduction
Machine Learning is a huge and growing area. In this chapter, we cannot possibly
even survey this area, but we can provide some context and some connections to
probability and statistics that should make it easier to think about machine learning
and how to apply these methods to real-world problems. The fundamental problem
of statistics is basically the same as machine learning: given some data, how to
make it actionable? For statistics, the answer is to construct analytic estimators using
powerful theory. For machine learning, the answer is algorithmic prediction. Given
a data set, what forward-looking inferences can we draw? There is a subtle bit in this
```
description: how can we know the future if all we have is data about the past? This
```
is the crux of the matter for machine learning, as we will explore in the chapter.
4.2 Python Machine Learning Modules
Python provides many bindings for machine learning libraries, some specialized for
technologies such as neural networks, and others geared towards novice users. For our
discussion, we focus on the powerful and popular Scikit-learn module. Scikit-learn
is distinguished by its consistent and sensible API, its wealth of machine learning
algorithms, its clear documentation, and its readily available datasets that make it
easy to follow along with the online documentation. Like Pandas, Scikit-learn relies
on Numpy for numerical arrays. Since its release in 2007, Scikit-learn has become
the most widely-used, general-purpose, open-source machine learning modules that
is popular in both industry and academia. As with all of the Python modules we use,
Scikit-learn is available on all the major platforms.
To get started, let’s revisit the familiar ground of linear regression using
Scikit-learn. First, let’s create some data.
© Springer International Publishing Switzerland 2016
J. Unpingco, Python for Probability, Statistics, and Machine Learning,
DOI 10.1007/978-3-319-30717-6_4
197
198 4 Machine Learning
>>> import numpy as np>>> from matplotlib.pylab import subplots
```
>>> from sklearn.linear_model import LinearRegression>>> X = np.arange(10) # create some data
```
```
>>> Y = X+np.random.randn(10) # linear with noise
```
We next import and create an instance of the LinearRegression class from
Scikit-learn.
```
>>> from sklearn.linear_model import LinearRegression>>> lr=LinearRegression() # create model
```
Scikit-learn has a wonderfully consistent API. All Scikit-learn objects use the fit
method to compute model parameters and the predict method to evaluate the
model. For the LinearRegression instance, the fit method computes the coef-
ficients of the linear fit. This method requires a matrix of inputs where the rows are
the samples and the columns are the features. The target of the regression are the Y
values, which must be correspondingly shaped, as in the following,
```
>>> X,Y = X.reshape((-1,1)), Y.reshape((-1,1))>>> lr.fit(X,Y)
```
```
LinearRegression(copy_X=True, fit_intercept=True, normalize=False)>>> lr.coef_
```
```
array([ [ 0.94211853] ])
```
Programming Tip
```
The negative one in the reshape((-1,1)) call above is for the truly lazy.
```
Using a negative one tells Numpy to figure out what that dimension should be
given the other dimension and number of array elements.
the coef_ property of the linear regression object shows the estimated parameters for
the fit. The convention is to denote estimated parameters with a trailing underscore.
The model has a score method that computes the R2 value for the regression.
Recall from our statistics chapter Sect. 3.7 that the R2 value is an indicator of the
```
quality of the fit and varies between zero (bad fit) and one (perfect fit).
```
```
>>> lr.score(X,Y)0.9059042979442371
```
Now, that we have this fitted, we can evaluate the fit using the predict method,
```
>>> xi = np.linspace(0,10,15) # more points to draw>>> xi = xi.reshape((-1,1)) # reshape as columns
```
```
>>> yp = lr.predict(xi)
```
4.2 Python Machine Learning Modules 199
Fig. 4.1 The Scikit-learn
module can easily perform
basic linear regression. The
circles show the training
data and the fitted line is
shown in black
The resulting fit is shown in Fig. 4.1.
Multilinear Regression. The Scikit-learn module easily extends linear regression
to multiple dimensions. For example, for multi-linear regression,
```
y = α0 + α1 x1 + α2 x2 + · · · + αn x n
```
```
The problem is to find all of the α terms given the training set {x1, x2, . . . , x n , y}.
```
We can create another example data set and see how this works,
```
>>> X=np.random.randint(20,size=(10,2))>>> Y=X.dot([1, 3])+1 + np.random.randn(X.shape[0])*20
```
Figure 4.2 shows the two dimensional regression example, where the size of the
circles is proportional to the targetted Y value. Note that we salted the output with
random noise just to keep things interesting. Nonetheless, the interface with Scikit-
learn is the same,
Fig. 4.2 Scikit-learn can
easily perform multi-linear
regression. The size of the
circles indicate the value of
the two-dimensional
```
function of (X1, X2)
```
200 4 Machine Learning
```
>>> lr=LinearRegression()>>> lr.fit(X,Y)
```
```
LinearRegression(copy_X=True, fit_intercept=True, normalize=False)>>> print lr.coef_
```
[ 0.35171694 4.04064287]
Note that the coef_ variable now has two terms in it, corresponding to the two input
dimensions. Note that the constant offset is already built-in and is an option on the
LinearRegression constructor. Figure 4.3 shows how the regression performs.
Polynomial Regression. We can extend this to include polynomial regression by
using the PolynomialFeatures in the preprocessing sub-module. To keep
it simple, let’s go back to our one-dimensional example. First, let’s create some
synthetic data,
```
>>> from sklearn.preprocessing import PolynomialFeatures>>> X = np.arange(10).reshape(-1,1) # create some data
```
```
>>> Y = X+X**2+X**3+ np.random.randn(*X.shape)*80
```
Next, we have to create a transformation from X to a polynomial of X,
```
>>> qfit = PolynomialFeatures(degree=2) # quadratic>>> Xq = qfit.fit_transform(X)
```
>>> print Xq[ [ 1 0 0]
[ 1 1 1][ 1 2 4]
[ 1 3 9][ 1 4 16]
[ 1 5 25][ 1 6 36]
[ 1 7 49][ 1 8 64]
[ 1 9 81] ]
Note there is an automatic constant term in the output 0th column where fit_
transform has mapped the single-column input into a set of columns representing
the individual polynomial terms. The middle column has the linear term, and the last
Fig. 4.3 The predicted data
is plotted in black. It
overlays the training data,
indicating a good fit
4.2 Python Machine Learning Modules 201
Fig. 4.4 The title shows the
R2 score for the linear and
quadratic rogressions
has the quadratic term. With these polynomial features stacked as columns of Xq,
all we have to do is fit and predict again. The following draws a comparison
```
between the linear regression and the quadratic repression (Fig. 4.4),
```
```
>>> lr=LinearRegression() # create linear model>>> qr=LinearRegression() # create quadratic model
```
```
>>> lr.fit(X,Y) # fit linear modelLinearRegression(copy_X=True, fit_intercept=True, normalize=False)
```
```
>>> qr.fit(Xq,Y) # fit quadratic modelLinearRegression(copy_X=True, fit_intercept=True, normalize=False)
```
```
>>> lp = lr.predict(xi)>>> qp = qr.predict(qfit.fit_transform(xi))
```
This just scratches the surface of Scikit-learn. We will go through many more
```
examples later, but the main thing is to concentrate on the usage (i.e., fit, predict)
```
which is standardized across all of the machine learning methods that are imple-
mented in Scikit-learn.
4.3 Theory of Learning
There is nothing so practical as a good theory. In this section, we establish the formal
framework for thinking about machine learning. This framework will help us think
beyond particular methods for machine learning so we can integrate new methods
or combine existing methods intelligently.
Both machine learning and statistics share the common goal of trying to derive
understanding from data. Some historical perspective helps. Most of the methods
in statistics were derived towards the start of the 20th century when data were hard
to come by. Society was preoccupied with the potential dangers of human over-
population and work was focused on studying agriculture and crop yields. At this
time, even a dozen data points was considered plenty. Around the same time, the
202 4 Machine Learning
deep foundations of probability were being established by Kolmogorov. Thus, the
lack of data meant that the conclusions had to be buttressed by strong assumptions
and solid mathematics provided by the emerging theory of probability. Furthermore,
inexpensive powerful computers were not yet widely available. The situation today
is much different: there are lots of data collected and powerful and easily program-
mable computers are available. The important problems no longer revolve around a
dozen data points on a farm acre, but rather millions of points on a square millimeter
of a DNA microarray. Does this mean that statistics will be superseded by machine
learning?
In contrast to classical statistics, which is concerned with developing models
that characterize, explain, and describe phenomena, machine learning is primarily
concerned with prediction, usually at the expense of all else. Areas like exploratory
statistics are very closely related to machine learning, but the degree of emphasis on
prediction is still distinguishing. In some sense, this is unavoidable due the size of the
data machine learning can reduce. In other words, machine learning can help distill
a table of a million columns into one hundred columns, but can we still interpret one
hundred columns meaningfully? In classical statistics, this was never an issue because
data were of a much smaller scale. Whereas mathematical models, usually normal
distributions, fitted with observations are common in statistics, machine learning
uses data to construct models that sit on complicated data structures and exploit
nonlinear optimizations that lack closed-form solutions. A common maxim is that
statistics is data plus analytical theory and machine learning is data plus computable
structures. This makes it seem like machine learning is completely ad-hoc and devoid
of underlying theory, but this is not the case, and both machine learning and statistics
share many important theoretical results. By way of contrast, let us consider a concrete
problem.
```
Let’s consider the classic balls in urns problem (see Fig. 4.5): we have an urn
```
containing red and blue balls and we draw five balls from the urn, note the color
of each ball, and then try to determine the proportion of red and blue balls in the
urn. We have already studied many statistical methods for dealing with this problem
in previous sections. Now, let’s generalize the problem slightly. Suppose the urn is
filled with white balls and there is some target unknown function f that paints each
```
selected ball either red or blue (see Fig. 4.6). The machine learning problem is how
```
to find the f function, given only the observed red/blue balls. So far, this doesn’t
sound much different from the statistical problem. However, now we want to take
our estimated f function, say, ˆf , and use it to predict the next handful of balls from
another urn. Now, here’s where the story takes a sharp turn. Suppose the next urn
already has some red and blue balls in it? Then, applying the function f may result
```
in purple balls which were not seen in the training data (see Fig. 4.7). Now, what
```
can we do? We have just scraped the surface of the issues machine learning must
confront using methods that are not part of the statistics canon.
4.3 Theory of Learning 203
Fig. 4.5 In the classical
statistics problem, we
observe a sample and model
what the urn contains
Fig. 4.6 In the machine
learning problem, we want
the function that colors the
marbles
Fig. 4.7 The problem is
further complicated because
we may see colored marbles
that were not present in the
original problem
4.3.1 Introduction to Theory of Machine Learning
Some formality and an example can get us going. We define the unknown target
```
function, f : X  → Y. The training set is {(x, y)} which means that we only see
```
the function’s inputs/outputs. The hypothesis set H is the set of all possible guesses
at f . This is the set from which we will ultimately draw our final estimate, ˆf . The
machine learning problem is how to derive the best element from the hypothesis set by
using the training set. Let’s consider a concrete example in the code below. Suppose
```
X consists of all three-bit vectors (i.e., X = {000, 001, . . . , 111}) as in the code
```
below,
>>> import pandas as pd>>> import numpy as np
```
>>> from pandas import DataFrame>>> df=DataFrame(index=pd.Index([’{0:04b}’.format(i) for i in range(2**4)],
```
```
... dtype=’str’,... name=’x’),columns=[’f’])
```
204 4 Machine Learning
Programming Tip
The string specification above uses Python’s advanced string formatting mini-
language. In this case, the specification says to convert the integer into a fixed-
```
width, four-character (04b) binary representation.
```
Next, we define the target function f below which just checks if the number of zeros
in the binary representation exceeds the number of ones. If so, then the function
```
outputs 1 and 0 otherwise (i.e., Y = {0, 1}).
```
```
>>> df.f=np.array(df.index.map(lambda i:i.count(’0’))... > df.index.map(lambda i:i.count(’1’)),dtype=int)
```
```
>>> df.head(8) # show top half onlyf
```
x0000 1
0001 10010 1
0011 00100 1
0101 00110 0
0111 0
The hypothesis set for this problem is the set of all possible functions of X . The
set D represents all possible input/output pairs. The corresponding hypothesis set
H has 2 16 elements, one of which matches f . There are 2 16 elements in the hypothesis
set because for each of sixteen input elements, there are two possible corresponding
values zero or one for each input. Thus, the size of the hypothesis set is 2 × 2 ×· · ·×
2 = 2 16 . Now, presented with a training set consisting of the first eight input/output
```
pairs, our goal is to minimize errors over the training set (Ein( ˆf )). There are 2 8
```
elements from the hypothesis set that exactly match f over the training set. But how
to pick among these 2 8 elements? It seems that we are stuck here. We need another
element from the problem in order to proceed. The extra piece we need is to assume
```
that the training set represents a random sampling (in-sample data) from a greater
```
```
population (out-of-sample data) that would be consistent with the population that ˆf
```
would ultimately predict upon. In other words, we are assuming a stable probability
structure for both the in-sample and out-of-sample data. This is a major assumption!
There is a subtle consequence of this assumption—whatever the machine learning
method does once deployed, in order for it to continue to work, it cannot disturb the
data environment that it was trained on. Said differently, if the method is not to be
trained continuously, then it cannot break this assumption by altering the genera-
tive environment that produced the data it was trained on. For example, suppose we
develop a model that predicts hospital readmissions based on seasonal weather and
patient health. Because the model is so effective, in the next six months, the hos-
pital forestalls readmissions by delivering interventions that improve patient health.
Clearly using the model cannot change seasonal weather, but because the hospital
used the model to change patient health, the training data used to build the model is
4.3 Theory of Learning 205
no longer consistent with the forward-looking health of the patients. Thus, there is
little reason to think that the model will continue to work as well going forward.
Returning to our example, let’s suppose that the first eight elements from X are
twice as likely as the last eight. The following code is a function that generates
elements from X according to this distribution.
```
>>> np.random.seed(12)>>> def get_sample(n=1):
```
```
... if n==1:... return ’{0:04b}’.format(np.random.choice(range(8)*2+range(8,16)))
```
```
... else:... return [get_sample(1) for _ in range(n)]
```
...
Programming Tip
The function that returns random samples uses the np.random.choice
```
function from Numpy which takes samples (with replacement) from the given
```
iterable. Because we want the first eight numbers to be twice as frequent as the
```
rest, we simply repeat them in the iterable using range(8)*2. Recall that
```
multiplying a Python list by an integer duplicates the entire list by that integer.
It does not do element-wise multiplication as with Numpy arrays. If we wanted
```
the first eight to be 10 times more frequent, then we would use range(8)*10,
```
for example. This is a simple but powerful technique that requires very little
code. Note that the p keyword argument in np.random.choice also pro-
vides an explicit way to specify more complicated distributions.
The next block applies the function definition f to the sampled data to generate the
training set consisting of eight elements.
```
>>> train=df.f.ix[get_sample(8)] # 8-element training set>>> train.index.unique().shape # how many unique elements?
```
```
(6,)
```
Notice that even though there are eight elements, there is redundancy because these
are drawn according to an underlying probability. Otherwise, if we just got all sixteen
different elements, we would have a training set consisting of the complete specifi-
cation of f and then we would therefore know what h ∈ H to pick! However, this
effect gives us a clue as to how this will ultimately work. Given the elements in the
training set, consider the set of elements from the hypothesis set that exactly match.
How to choose among these? The answer is it does not matter! Why? Because under
the assumption that the prediction will be used in an environment that is determined
by the same probability, getting something outside of the training set is just as likely
as getting something inside the training set. The size of the training set is key here—
the bigger the training set, the less likely that there will be real-world data that fall
outside of it and the better ˆf will perform. 1 The following code shows the elements
of the training set in the context of all possible data.
```
1 This assumes that the hypothesis set is big enough to capture the entire training set (which it is for
```
```
this example). We will discuss this trade-off in greater generality shortly.
```
206 4 Machine Learning
```
>>> df[’fhat’]=df.f.ix[train.index.unique()]>>> df.fhat
```
x0000 NaN
0001 NaN0010 1
0011 00100 1
0101 NaN0110 0
0111 NaN1000 1
1001 01010 NaN
1011 NaN1100 NaN
1101 NaN1110 NaN
1111 NaNName: fhat, dtype: float64
Note that there are NaN symbols where the training set had no values. For definiteness,
we fill these in with zeros, although we can fill them with anything we want so long
as whatever we do is not determined by the training set.
```
>>> df.fhat.fillna(0,inplace=True) #final specification of fhat
```
Now, let’s pretend we have deployed this and generate some test data.
```
>>> test= df.f.ix[get_sample(50)]>>> (df.ix[test.index][’fhat’] != test).mean()
```
0.17999999999999999
The result shows the error rate, given the probability mechanism that is generating
the data. The following Pandas-fu compares the overlap between the training set and
the test set in the context of all possible data. The NaN values show the rows where
the test data had items absent in the training data. Recall that the method returns zero
for these items. As shown, sometimes this works in its favor, and sometimes not.
```
>>> pd.concat([test.groupby(level=0).mean(),... train.groupby(level=0).mean()],
```
```
... axis=1,... keys=[’test’,’train’])
```
test train0000 1 NaN
0001 1 NaN0010 1 1
0011 0 00100 1 1
0101 0 NaN0110 0 0
0111 0 NaN1000 1 1
1001 0 01010 0 NaN
1011 0 NaN1100 0 NaN
1101 0 NaN1110 0 NaN
1111 0 NaN
4.3 Theory of Learning 207
Note that where the test data and training data share elements, they agree. When the
test set produced an unseen element, it produces a match or not.
Programming Tip
The pd.concat function concatenates the two Series objects in the list.
The axis=1 means join the two objects along the columns where each newly
created column is named according to the given keys. The level=0 in
the groupby for each of the Series objects means group along the index.
Because the index corresponds to the 4-bit elements, this accounts for repetition
in the elements. The mean aggregation function computes the values of the
```
function for each 4-bit element. Because all functions in each respective group
```
have the same value, the mean just picks out that value because the average
of a list of constants is that constant.
Now, we are in position to ask how big the training set should be to achieve a
level of performance. For example, on average, how many in-samples do we need
```
for a given error rate? For this problem, we can ask how large (on average) must
```
the training set be in order to capture all of the possibilities and achieve perfect out-
of-sample error rates? For this problem, this turns out to be sixty-three.2 Let’s start
over and retrain with these many in-samples.
```
>>> train=df.f.ix[get_sample(63)]>>> del df[’fhat’]
```
```
>>> df[’fhat’]=df.f.ix[train.index.unique()]>>> df.fhat.fillna(0,inplace=True) #final specification of fhat
```
```
>>> test= df.f.ix[get_sample(50)]>>> (df.fhat.ix[test] != df.f.ix[test]).mean() # error rate
```
0.0
Notice that this bigger training set has a better error rate because it is able to identify
the best element from the hypothesis set because the training set captured more of
the complexity of the unknown f . This example shows the trade-offs between the
size of the training set, the complexity of the target function, the probability structure
of the data, and the size of the hypothesis set.
4.3.2 Theory of Generalization
What we really want to know is how the our method will perform once deployed.
It would be nice to have some kind of performance guarantee. In other words, we
worked hard to minimize the errors in the training set, but what errors can we expect
```
at deployment? In training, we minimized the in-sample error, Ein( ˆf ), but that’s not
```
```
good enough. We want guarantees about the out-of-sample error, Eout( ˆf ). This is
```
2 This is a slight generalization of the classic coupon collector problem.
208 4 Machine Learning
what generalization means in machine learning. The mathematical statement of this
is the following,
P
```
(
```
```
|Eout( ˆf ) − Ein( ˆf )| > 
```
```
)
```
< δ
for a given  and δ. Informally, this says that the probability of the respective errors
differing by more than a given  is less than some quantity, δ. This basically means
that whatever the performance on the training set, it should probably be pretty close
to the corresponding performance once deployed. Note that this does not say that
```
the in-sample errors (Ein) are any good in an absolute sense. It just says that we
```
would not expect much different after deployment. Thus, good generalization means
no surprises after deployment, not necessarily good performance, by any means.
There are two main ways to get at this: cross-validation and probability inequalities.
Let’s consider the latter first. There are two entangled issues: the complexity of the
hypothesis set and the probability of the data. It turns out we can separate these two
by deriving a separate notion of complexity free from any particular data probability.
VC Dimension. We first need a way to quantify model complexity. Following
```
Wasserman [1], let A be a class of sets and F = {x1, x2, . . . , x n }, a set of n data
```
points. Then, we define
```
NA(F) = # {F ∩ A : A ∈ A}
```
This counts the number of subsets of F that can be extracted by the sets of A. The
```
number of items in the set (i.e., cardinality) is noted by the # symbol. For example,
```
```
suppose F = {1} and A = {(x ≤ a)}. In other words, A consists of all intervals
```
```
closed on the right and parameterized by a. In this case we have NA(F) = 1 because
```
all elements can be extracted from F using A.
The shatter coefficient is defined as,
```
s(A, n) = maxF∈FnNA(F)
```
where F consists of all finite sets of size n. Note that this sweeps over all finite sets
so we don’t need to worry about any particular data set of finitely many points. The
definition is concerned with A and how its sets can pick off elements from the data
set. A set F is shattered by A if it can pick out every element in it. This provides
a sense of how the complexity in A consumes data. In our last example, the set of
```
half-closed intervals shattered every singleton set {x1}.
```
Now, we come to the main definition of the Vapnik-Chervonenkis [2] dimension
```
dVC which defined as the largest k for which s(A, n) = 2k , except in the case where
```
```
s(A, n) = 2n for which it is defined as infinity. For our example where F = {x1},
```
```
we already saw that A shatters F. How about when F = {x1, x2}? Now, we have
```
two points and we have to consider whether all subsets can be extracted by A. In
this case, there are four subsets,
```
{
```
```
Ø, {x1} , {x2} , {x1, x2}
```
```
}
```
. Note that Ø denotes the
4.3 Theory of Learning 209
empty set. The empty set is easily extracted—pick a so that it is smaller than both
x1 and x2 . Assuming that x1 < x2 , we can get the next set by choosing x1 < a < x2 .
The last set is likewise do-able by choosing x2 < a. The problem is that we cannot
```
capture the third set, {x2}, without capturing x1 as well. This means that we cannot
```
shatter any finite set with n = 2 using A. Thus, dVC = 1.
Here is the climatic result
```
Eout( ˆf ) ≤ Ein( ˆf ) +
```
√
8
n ln
```
( 4((2n)dVC + 1)
```
δ
```
)
```
with probability at least 1 − δ. This basically says that the expected out-of-sample
error can be no worse than the in-sample error plus a penalty due to the complexity
of the hypothesis set. The expected in-sample error comes from the training set but
the complexity penalty comes from just the hypothesis set, so we have disentangled
these two issues.
A general result like this, for which we do not worry about the probability of the
data, is certain to be pretty generous, but nonetheless, it tells us how the complexity
```
penalty enters into the out-of-sample error. In other words, the bound on Eout( ˆf )
```
gets worse for a more complex hypothesis set. Thus, this generalization bound is a
```
useful guideline but not very practical if we want to get a good estimate of Eout( ˆf ).
```
4.3.3 Worked Example for Generalization/Approximation
Complexity
The stylized curves in Fig. 4.8 illustrate the idea that there is some optimal point of
complexity that represents the best generalization given the training set.
Fig. 4.8 In the ideal
situation, there is a best
model that represents the
optimal trade-off between
complexity and error. This is
shown by the vertical line
210 4 Machine Learning
To get a firm handle on these curves, let’s develop a simple one-dimensional
machine learning method and go through the steps to create this graph. Let’s sup-
```
pose we have a training set consisting of x-y pairs {(x i , yi )}. Our method groups
```
the x-data into intervals and then averages the y-data in those intervals. Predict-
ing for new x-data means simply identifying the interval containing the new data
then reporting the corresponding value. In other words, we are building a simple
one-dimensional, nearest neighbor classifier. For example, suppose the training set
x-data is the following,
```
>>> train=DataFrame(columns=[’x’,’y’])>>> train[’x’]=np.sort(np.random.choice(range(2**10),size=90))
```
```
>>> train.x.head(10) # first ten elements0 15
```
1 302 45
3 654 76
5 826 115
7 1458 147
9 158Name: x, dtype: int32
In this example, we took a random set of 10-bit integers. To group these into, say,
ten intervals, we simply use Numpy reshape as in the following,
```
>>> train.x.reshape(10,-1)array([ [ 15, 30, 45, 65, 76, 82, 115, 145, 147],
```
[158, 165, 174, 175, 181, 209, 215, 217, 232],[233, 261, 271, 276, 284, 296, 318, 350, 376],
[384, 407, 410, 413, 452, 464, 472, 511, 522],[525, 527, 531, 534, 544, 545, 548, 567, 567],
[584, 588, 610, 610, 641, 645, 648, 659, 667],[676, 683, 684, 697, 701, 703, 733, 736, 750],
[754, 755, 772, 776, 790, 794, 798, 804, 830],[831, 834, 861, 883, 910, 910, 911, 911, 937],
```
[943, 946, 947, 955, 962, 962, 984, 989, 998] ])
```
```
where every row is one of the groups. Note that the range of each group (i.e., length
```
```
of the interval) is not preassigned, and is learned from the training data. For this
```
example, the y-values correspond to the number of ones in the bit representation of
the x-values. The following code defines this target function,
```
>>> f_target=np.vectorize(lambda i:sum(map(int,i)))
```
Programming Tip
The above function uses np.vectorize which is a convenience method
in Numpy that converts plain Python functions into Numpy versions. This
basically saves additional looping semantics and makes it easier to use with
other Numpy arrays and functions.
4.3 Theory of Learning 211
Next, we create the bit representations of all of the x-data below and then complete
training set y-values,
```
>>> train[’xb’]= train.x.map(’{0:010b}’.format)>>> train.y=train.xb.map(f_target)
```
```
>>> train.head(5)x y xb
```
0 15 4 00000011111 30 4 0000011110
2 45 4 00001011013 65 2 0001000001
4 76 3 0001001100
To train on this data, we just group by the specified amount and then average the
y-data over each group.
```
>>> train.y.reshape(10,-1).mean(axis=1)array([ 3.55555556, 4.88888889, 4.44444444, 4.88888889, 4.11111111,
```
4. , 6. , 5.11111111, 6.44444444, 6.66666667])
Note that the axis=1 keyword argument just means average across the columns.
So far, this defines the training. To predict using this method, we have to extract the
edges from each of the groups and then fill in with the group-wise mean we just
computed for y. The following code extracts the edges of each group.
```
>>> le,re=train.x.reshape(10,-1)[:,[0,-1] ].T>>> print le # left edge of group
```
[ 15 158 233 384 525 584 676 754 831 943]>>> print re # right edge of group
[147 232 376 522 567 667 750 830 937 998]
Next, we compute the group-wise means and assign them to their respective edges.
```
>>> val = train.y.reshape(10,-1).mean(axis=1).round()>>> func = pd.Series(index=range(1024))
```
>>> func[le]=val # assign value to left edge>>> func[re]=val # assign value to right edge
>>> func.iloc[0]=0 # default 0 if no data>>> func.iloc[-1]=0 # default 0 if no data
```
>>> func.head()0 0
```
1 NaN2 NaN
3 NaN4 NaN
```
dtype: float64
```
Note that the Pandas Series object automatically fills in unassigned values with
NaN. We have thus far only filled in values at the edges of the groups. Now, we need
to fill in the intermediate values.
```
>>> fi=func.interpolate(’nearest’)>>> fi.head()
```
0 01 0
2 03 0
4 0dtype: float64
212 4 Machine Learning
Fig. 4.9 The vertical lines show the training data and the thick black line is the approximant we
have learned from the training data
The interpolate method of the Series object can apply a wide variety of
powerful interpolation methods, but we only need the simple nearest neighbor method
to create our piecewise approximant. Figure 4.9 shows how this looks for the training
data we have created.
Now, with all that established, we can now draw the curves for this machine
```
learning method. Instead of partitioning the training data for cross-validation (which
```
```
we’ll discuss later), we can simulate test data using the same mechanism as for the
```
training data, as shown next,
```
>>> test=pd.DataFrame(columns=[’x’,’xb’,’y’])>>> test[’x’]=np.random.choice(range(2**10),size=500)
```
```
>>> test.xb= test.x.map(’{0:010b}’.format)>>> test.y=test.xb.map(f_target)
```
```
>>> test.sort(columns=[’x’],inplace=True)
```
The curves are the respective errors for the training data and the testing data. For our
error measure, we use the mean-squared-error,
```
Eout = 1n
```
n∑
```
i=1
```
```
( ˆf (x i ) − yi )2
```
```
where {(x i , yi )}ni=1 come from the test data. The in-sample error (Ein) is defined
```
the same except for the in-sample data. In this example, the size of each group is
proportional to dVC, so the more groups we choose, the more complexity in the fitting.
Now, we have all the ingredients to understand the trade-offs of complexity versus
error.
Figure 4.10 shows the curves for our one-dimensional clustering method. The
dotted line shows the mean-squared-error on the training set and the other line shows
the same for the test data. The shaded region is the complexity penalty of this method.
Note that with enough complexity, the method can exactly memorize the testing
```
data, but that only penalizes the testing error (Eout). This effect is exactly what the
```
Vapnik-Chervonenkis theory expresses. The horizontal axis is proportional to the
4.3 Theory of Learning 213
Fig. 4.10 The dotted line shows the mean-squared-error on the training set and the other line shows
the same for the test data. The shaded region is the complexity penalty of this method. Note that
as the complexity of the model increases, the training error decreases, and the method essentially
memorizes the data. However, this improvement in training error comes at the cost of larger testing
error
VC-dimension. In this case, complexity boils down to the number of intervals used
in the sectioning. At the far right, we have as many intervals as there are elements
in the data set, meaning that every element is wrapped in its own interval. The
average value of the data in that interval is therefore just the corresponding y value
because there are no other elements to average over. The Jupyter/IPython notebook
corresponding to the section has the code to generate these curves so you can see
how these curves change with bigger or smaller data sets.
Before we leave this problem, there is another way to visualize the performance of
our learning method. This problem can be thought of as a multi-class identification
problem. Given a 10-bit integer, the number of ones in its binary representation is in
```
one of the classes {0, 1, . . . , 10}. The output of the model tries to put each integer
```
in its respective class. How well this was done can be visualized using a confusion
matrix as shown in the next code block,
```
>>> from sklearn.metrics import confusion_matrix>>> cmx=confusion_matrix(test.y.values,fi[test.x].values)
```
>>> print cmx[ [ 1 0 0 0 0 0 0 0 0 0]
[ 1 0 1 0 1 1 0 0 0 0][ 0 0 3 9 7 4 0 0 0 5]
[ 1 0 3 23 19 6 6 0 2 0][ 0 0 1 26 27 14 27 2 2 0]
[ 0 0 3 15 31 28 30 8 1 0][ 0 0 1 8 18 20 25 23 2 2]
[ 1 0 1 10 5 13 7 19 3 6][ 4 0 1 2 0 2 2 7 4 3]
[ 2 0 0 0 0 1 0 0 0 0] ]
The rows of this 10×10 matrix show what the true class was and the columns indicate
the class that the model predicted. The numbers in the matrix indicate the number of
times that association was made. For example, the first row shows that there was one
214 4 Machine Learning
```
entry in the test set with no ones in its binary representation (i.e., namely the number
```
```
zero) and it was correctly classified (namely, it is in the first row, first column of the
```
```
matrix). The second row shows there were four entries total in the test set with a binary
```
representation containing exactly a single one. This was incorrectly classified as the
```
0-class (i.e., first column) once, the 2-class (third column) once, the 4-class (fifth
```
```
column) once, and the 5-class (sixth column) once. It was never classified correctly
```
because the second column is zero for this row. In other words, the diagonal entries
show the number of times it was correctly classified.
Using this matrix, we can easily estimate the true-detection probability that we
covered earlier in our hypothesis testing section,
```
>>> print cmx.diagonal()/cmx.sum(axis=1)[ 1. 0. 0.10714286 0.38333333 0.27272727 0.24137931
```
0.25252525 0.29230769 0.16 0. ]
In other words, the first element is the probability of detecting 0 when 0 is in force,
the second element is the probability of detecting 1 when 1 is in force, and so on. We
can likewise compute the false-alarm rate for each of the classes in the following,
```
>>> print (cmx.sum(axis=0) - cmx.diagonal())/(cmx.sum()-cmx.sum(axis=1))[ 0.01803607 0. 0.02330508 0.15909091 0.20199501 0.15885417
```
0.17955112 0.09195402 0.02105263 0.03219316]
Programming Tip
The Numpy sum function can sum across a particular axis or, if the axis is
unspecified, will sum all entries of the array.
In this case, the first element is the probability that 0 is declared when another
category is in force, the next element is the probability that 1 is declared when
another category is in force, and so on. For a decent classifier, we want a true-
detection probability to be greater than the corresponding false-alarm rate, otherwise
the classifier is no better than a coin-flip. Note that, at the time of this writing, Scikit-
learn has limited tools for this kind of multiple class classification task.
The missing feature of this problem, from the learning algorithm standpoint, is
that we did not supply the bit representation of every element which was used to
derive the target variable, y. Instead, we just used the integer value of each of the
10-bit numbers, which essentially concealed the mechanism for creating the y values.
In other words, there was a unknown transformation from the input space X to Y
that the learning algorithm had to overcome, but that it could not overcome, at least
not without memorizing the training data. This lack of knowledge is a key issue
in all machine learning problems, although we have made it explicit here with this
stylized example. This means that there may be one or more transformations from
X → X ′ that can help learning algorithm get traction on the so-transformed space
while providing a better trade-off between generalization and approximation than
could have been achieved otherwise. Finding such transformations is called feature
engineering.
4.3 Theory of Learning 215
4.3.4 Cross-Validation
In the last section, we explored a stylized machine learning example to understand
the issues of complexity in machine learning. However, to get an estimate of out-
of-sample errors, we simply generated more synthetic data. In practice, this is not an
option, so we need to estimate these errors from the training set itself. This is what
cross-validation does. The simplest form of cross-validation is k-fold validation. For
example, if K = 3, then the training data is divided into three sections wherein each
of the three sections is used for testing and the remaining two are used for training.
This is implemented in Scikit-learn as in the following,
>>> import numpy as np>>> from sklearn.cross_validation import KFold
```
>>> data =np.array([’a’,]*3+[’b’,]*3+[’c’,]*3) # example>>> print data
```
```
[’a’ ’a’ ’a’ ’b’ ’b’ ’b’ ’c’ ’c’ ’c’]>>> for train_idx,test_idx in KFold(len(data),3):
```
... print train_idx,test_idx...
[3 4 5 6 7 8] [0 1 2][0 1 2 6 7 8] [3 4 5]
[0 1 2 3 4 5] [6 7 8]
In the code above, we construct a sample data array and then see how KFold splits
it up into indicies for training and testing, respectively. Notice that there are no
duplicated elements in each row between training and testing indicies. To examine
the elements of the data set in each category, we simply use each of the indicies as
in the following,
```
>>> for train_idx,test_idx in KFold(len(data),3):... print ’training’, data[ train_idx ]
```
... print ’testing’ , data[ test_idx ]...
training [’b’ ’b’ ’b’ ’c’ ’c’ ’c’]testing [’a’ ’a’ ’a’]
training [’a’ ’a’ ’a’ ’c’ ’c’ ’c’]testing [’b’ ’b’ ’b’]
training [’a’ ’a’ ’a’ ’b’ ’b’ ’b’]testing [’c’ ’c’ ’c’]
This shows how each group is used in turn for training/testing. There is no random
shuffling of the data unless the shuffle keyword argument is given. The error over
the test set is th cross-validation error. The idea is to postulate models of differing
complexity and then pick the one with the best cross-validation error. For example,
suppose we had the following sine wave data,
```
>>> xi = np.linspace(0,1,30)>>> yi = np.sin(2*np.pi*xi)
```
and we want to fit this with polynomials of increasing order.
Figure 4.11 shows the individual folds in each panel. The circles represent the
training data. The diagonal line is the fitted polynomial. The gray shaded areas
indicate the regions of errors between the fitted polynomial and the held-out testing
data. The larger the gray area, the bigger the cross-validation errors, as are reported
in the title of each frame.
216 4 Machine Learning
After reviewing the last three figures and averaging the cross-validation errors, the
one with the least average error is declared the winner. Thus, cross-validation provides
a method of using a single data set to make claims about unseen out-of-sample data
insofar as the model with the best complexity can be determined. The entire process
to generate the above figures can be captured using cross_val_score as shown
```
for the linear regression (compare the output with the values in the titles in each panel
```
```
of Fig. 4.11),
```
>>> from sklearn.metrics import make_scorer, mean_squared_error>>> from sklearn.cross_validation import cross_val_score
```
>>> from sklearn.linear_model import LinearRegression>>> Xi = xi.reshape(-1,1) # refit column-wise
```
```
>>> Yi = yi.reshape(-1,1)>>> lf = LinearRegression()
```
```
>>> scores = cross_val_score(lf,Xi,Yi,cv=4,... scoring=make_scorer(mean_squared_error))
```
>>> print scores[ 0.3554451 0.33131438 0.50454257 0.45905672]
Programming Tip
The make_scorer function is a wrapper that enables cross_val_score
to compute scores from the given estimator’s output.
Fig. 4.11 This shows the folds and errors for the linear model. The shaded areas show the errors
```
in each respective test set (i.e., cross-validation scores) for the linear model
```
4.3 Theory of Learning 217
The process can be further automated by using a pipeline as in the following,
>>> from sklearn.pipeline import Pipeline>>> from sklearn.preprocessing import PolynomialFeatures
```
>>> polyfitter = Pipeline([(’poly’, PolynomialFeatures(degree=3)),... (’linear’, LinearRegression())])
```
```
>>> polyfitter.get_params(){’linear’: LinearRegression(copy_X=True, fit_intercept=True, normalize=False),
```
’linear__copy_X’: True,’linear__fit_intercept’: True,
```
’linear__normalize’: False,’poly’: PolynomialFeatures(degree=3, include_bias=True, interaction_only=False),
```
’poly__degree’: 3,’poly__include_bias’: True,
```
’poly__interaction_only’: False}
```
The Pipeline object is a way of stacking standard steps into one big estimator,
while respecting the usual fit and predict interfaces. The output of the get_
params function contains the polynomial degrees we previously looped over to
create Fig. 4.11, etc. We will use these named parameters in the next code block. To
do this automatically using this polyfitter estimator, we need the Grid Search
Cross Validation object, GridSearchCV. The next step is to use this to create the
grid of parameters we want to loop over as in the following,
```
>>> from sklearn.grid_search import GridSearchCV>>> gs=GridSearchCV(polyfitter,{’poly__degree’:[1,2,3]},cv=4)
```
The gs object will loop over the polynomial degrees up to cubic using four-fold cross
validation cv=4, like we did manually earlier. The poly__degree item comes
from the previous get_params call. Now, we just apply the usual fit method on
the training data,
```
>>> _=gs.fit(Xi,Yi)>>> gs.grid_scores_
```
```
[mean: -3.48744, std: 2.51765, params: {’poly__degree’: 1},mean: -36.06830, std: 28.84096, params: {’poly__degree’: 2},
```
```
mean: -0.07906, std: 0.95040, params: {’poly__degree’: 3}]
```
the scores shown correspond to the cross validation scores for each of the parame-
```
ters (e.g., polynomial degrees) using four-fold cross-validation. Note that the higher
```
scores are better here and the cubic polynomial is best, as we observed earlier.
The default R2 metric is used for the scoring in this case as opposed to mean-
squared-error. The validation results of this pipeline for the quadratic fit are shown
in Fig. 4.12, and for the cubic fit, in Fig. 4.13. This can be changed by passing
```
the scoring=make_scorer(mean_squared_error) keyword argument to
```
GridSearchCV. There is also RandomizedSearchCV that does does not nec-
essarily evaluate every point on the grid and instead randomly samples the grid
according to an input probability distribution. This is very useful for a large number
of hyper-parameters.
218 4 Machine Learning
Fig. 4.12 This shows the folds and errors as in Figs. 4.10 and 4.11. The shaded areas show the
errors in each respective test set for the quadratic model
Fig. 4.13 This shows the folds and errors. The shaded areas show the errors in each respective test
set for the cubic model
4.3 Theory of Learning 219
4.3.5 Bias and Variance
So far, we have been thinking about the average error in terms of in-samples and
out-samples, but this depends on a particular training data set. What we want is a
concept that extends to all possible training data and captures the performance of
the estimator in that setting. For example, our ultimate estimator, ˆf is derived from
```
a particular set of training data (D) and is thus denoted, ˆfD . This makes the out-
```
```
of-sample error explicitly, Eout( ˆfD ). To eliminate the dependence on a particular
```
set of training data set, we have to compute the expectation across all training data
sets,
```
ED Eout( ˆfD ) = bias + var
```
where
```
bias(x) = ( ˆf (x) − f (x))2
```
and
```
var(x) = ED ( ˆfD (x) − ˆf (x))2
```
and where ˆf is the mean of all estimators for all data sets. There is nothing to say that
such a mean is an estimator that could have arisen from any particular training data,
however. It just implies that for any particular point x, the mean of the values of all the
```
estimators is ˆf (x). Therefore, bias captures the sense that, even if all possible data
```
were presented to the learning method, it would still differ from the target function
by this amount. On the other hand var shows the variation in the final hypothesis,
depending on the training data set, notwithstanding the target function. Thus, the
tension between approximation and generalization is captured by these two terms.
For example, suppose there is only one hypothesis. Then, var = 0 because there
can be no variation due to a particular set of training data because no matter what
that training data is, the learning method always selects the one and only hypothesis.
In this case, the bias could be very large, because there is no opportunity for the
learning method to alter the hypothesis due to the training data, and the method can
only ever pick the single hypothesis!
Let’s construct an example to make this concrete. Suppose we have a hypothesis set
```
consisting of all linear regressions without an intercept term, h(x) = ax. The training
```
```
data consists of only two points {(x i , sin(πx i ))}2i=1 where x i is drawn uniformly from
```
the interval [−1, 1]. From Sect. 3.7 on linear regression, we know that the solution
for a is the following,
```
a = x
```
T y
```
xT x (4.3.5.1)
```
220 4 Machine Learning
Fig. 4.14 For a two-element
training set consisting of the
points shown, the line is the
best fit over the hypothesis
```
set, h(x) = ax
```
```
where x = [x1, x2] and y = [y1, y2]. The ˆf (x) represents the solution over all
```
possible sets of training data for a fixed x. The following code shows how to construct
the training data,
```
>>> from scipy import stats>>> def gen_sindata(n=2):
```
```
... x=stats.uniform(-1,1) # define random variable... v = x.rvs((n,1)) # generate sample
```
```
... y = np.sin(np.pi*v) # use sample for sine... return (v,y)
```
...
Again, using Scikit-learn’s LinearRegression object, we can compute the a
parameter. Note that we have to set fit_intercept=False keyword to suppress
```
the default automatic fitting of the intercept (Fig. 4.14).
```
```
>>> lr = LinearRegression(fit_intercept=False)>>> lr.fit(*gen_sindata(2))
```
```
LinearRegression(copy_X=True, fit_intercept=False, normalize=False)>>> lr.coef_
```
```
array([ [ 2.0570357] ])
```
Programming Tip
Note that we designed gen_sindata to return a tuple to use the automatic
```
unpacking feature of Python functions in lr.fit(*gen_sindata()). In
```
other words, using the asterisk notation means we don’t have to separately
assign the outputs of gen_sindata before using them for lr.fit.
4.3 Theory of Learning 221
```
In this case, ˆf (x) = ax, where a the expected value of the parameter over all possible
```
training data sets. Using our knowledge of probability, we can write this out explicitly
as the following,
```
a = E
```
```
( x
```
```
1 sin(πx1) + x2 sin(πx2)
```
x21 + x22
```
)
```
```
where x = [x1, x2] and y = [sin(πx1), sin(πx2)] in Eq. 4.3.5.1. However, computing
```
this expectation analytically is hard, but for this specific situation, a ≈ 1.43. To get
this value using simulation, we just loop over the process, collect the outputs, and
the average them as in the following,
```
>>> a_out=[] # output container>>> for i in range(100):
```
```
... _=lr.fit(*gen_sindata(2))... a_out.append(lr.coef_[0,0])
```
```
...>>> np.mean(a_out) # approx 1.43
```
1.3753786877340366
Note that you may have to loop over many more iterations to get close to the purported
value. The var requires the variance of a,
```
var(x) = E((a − a)x)2 = x2E(a − a)2 ≈ 0.71x2
```
The bias is the following,
```
bias(x) = (sin(πx) − ax)2
```
Figure 4.15 shows the bias, var, and mean-squared-error for this problem. Notice
that there is zero bias and zero variance when x = 0. This is because the learning
method cannot help but get that correct because all the hypotheses happen to match
the value of the target function at that point! Likewise, the var is zero because all
possible pairs, which constitute the training data, are fitted through zero because
```
h(x) = ax has no choice but to go through zero. The errors are worse at the end
```
Fig. 4.15 These curves
decompose the mean squared
error into its constituent bias
and variance for this example
222 4 Machine Learning
points. As we discussed in our statistics chapter, those points have the most leverage
against the hypothesized models and result in the worst errors. Notice that reducing
the edge-errors depends on getting exactly those points near the edges as training
data. The sensitivity to a particular data set is reflected in this behavior.
What if we had more than two points in the training data? What would happen to
var and bias? Certainly, the var would decrease because it would be harder and
harder to generate training data sets that would be substantially different from each
other. The bias would also decrease because more points in the training data means
better approximation of the sine function over the interval. What would happen if
we changed the hypothesis set to include more complex polynomials? As we have
already seen with our polynomial regression earlier in this chapter, we would see the
same overall effect as here, but with relatively smaller absolute errors and the same
edge effects we noted earlier. The corresponding Jupyter/IPython Notebook has the
source code to help you can try these ideas and see for yourself.
4.3.6 Learning Noise
We have thus far not considered the effect of noise in our analysis of learning. The
following example should help resolve this. Let’s suppose we have the following
scalar target function,
```
y(x) = wTo x + η
```
```
where η ∼ N (0, σ2) is an additive noise term and w, x ∈ Rd . Furthermore, we have
```
```
n measurements of y. This means the training set consists of {(xi , yi )}ni=1 . Stacking
```
the measurements together into a vector format,
```
y = Xwo + η
```
with y, ∈ Rn , wo ∈ Rd and X contains xi as columns. The hypothesis set consists
of all linear models,
```
h(w, x) = wT x
```
We need to the learn the correct w from the hypothesis set given the training data. So
far, this is the usual setup for the problem, but how does the noise factor play to this?
In our usual situation, the training set consists of randomly chosen elements from a
larger space. In this case, that would be the same as getting random sets of xi vectors.
That still happens in this case, but the problem is that even if the same xi appears
twice, it will not be associated with the same y value due the additive noise coming
from η. To keep this simple, we assume that there is a fixed set of xi vectors and that
we get all of them in the training set. For every specific training set, we know how
to solve for the MMSE from our earlier statistics work,
4.3 Theory of Learning 223
```
w = (XT X)−1XT y
```
Given this setup, what is the in-sample mean-squared-error? Because this is the
MMSE solution, we know from our study of the associated orthogonality of such
systems that we have,
```
Ein = ‖y‖2 − ‖Xw‖2 (4.3.6.1)
```
where our best hypothesis, h = Xw. Now, we want to compute the expectation of
this over the distribution of η. For instance, for the first term, we want to compute,
```
E|y|2 = 1n E(yT y) = 1n Tr E(yyT )
```
```
where Tr is the matrix trace operator (i.e., sum of the diagonal elements). Because
```
each η are independent, we have
```
Tr E(yyT ) = Tr XwowTo XT + σ2 Tr I = Tr XwowTo XT + nσ2 (4.3.6.2)
```
```
where I is the n × n identity matrix. For the second term in Eq. (4.3.6.1), we have
```
```
|Xw|2 = Tr XwwT XT = Tr X(XT X)−1XT yyT X(XT X)−1XT
```
The expectation of this is the following,
```
E|Xw|2 = Tr X(XT X)−1XT E(yyT )X(XT X)−1XT (4.3.6.3)
```
which, after substituting in Eq. 4.3.6.2, yields,
```
E|Xw|2 = Tr XwowTo XT + σ2d (4.3.6.4)
```
Next, assembling Eq. 4.3.6.1 from this and Eq. 4.3.6.2 gives,
```
E(Ein) = 1n Ein = σ2
```
```
(
```
1 − dn
```
)
```
```
(4.3.6.5)
```
which provides an explicit relationship between the noise power, σ2 , the complexity
```
of the method (d) and the number of training samples (n). This is very illustrative
```
because it reveals the ratio d/n, which is a statement of the trade-off between model
complexity and in-sample data size. From our analysis of the VC-dimension, we
already know that there is a complicated bound that represents the penalty for com-
plexity, but this problem is unusual in that we can actually derive an expression for
this without resorting to bounding arguments. Furthermore, this result shows, that
```
with a very large number of training examples (n → ∞), the expected in-sample
```
224 4 Machine Learning
error approaches σ2 . Informally, this means that the learning method cannot general-
ize from noise and thus can only reduce the expected in-sample error by memorizing
```
the data (i.e., d ≈ n).
```
The corresponding analysis for the expected out-of-sample error is similar, but
more complicated because we don’t have the orthogonality condition. Also, the out-
of-sample data has different noise from that used to derive the weights, w. This results
in extra cross-terms,
```
Eout = Tr
```
```
(
```
XwowTo XT + ¸¸T + XwwT XT − XwwTo XT
−XwowT XT
```
)
```
```
(4.3.6.6)
```
where we are using the ¸ notation for the noise in the out-of-sample case, which is
different from that in the in-sample case. Simplifying this leads to the following,
```
E(Eout) = Tr σ2I + σ2X(XT X)−1XT (4.3.6.7)
```
Then, assembling all of this gives,
```
E(Eout) = σ2
```
```
(
```
1 + dn
```
)
```
```
(4.3.6.8)
```
which shows that even in the limit of large n, the expected out-of-sample error also
approaches the noise power limit, σ2 . This shows that memorizing the in-sample data
```
(i.e., d/n ≈ 1) imposes a proportionate penalty on the out-of-sample performance
```
```
(i.e., EEout ≈ 2σ2 when EEin ≈ 0 ).
```
The following code simulates this important example:
```
>>> def est_errors(d=3,n=10,niter=100):... assert n>d
```
```
... wo = np.matrix(arange(d)).T... Ein = list()
```
```
... Eout = list()... # choose any set of vectors
```
```
... X = np.matrix(np.random.rand(n,d))... for ni in xrange(niter):
```
```
... y = X*wo + np.random.randn(X.shape[0],1)... # training weights
```
```
... w = np.linalg.inv(X.T*X)*X.T*y... h = X*w
```
```
... Ein.append(np.linalg.norm(h-y)**2)... # out of sample error
```
```
... yp = X*wo + np.random.randn(X.shape[0],1)... Eout.append(np.linalg.norm(h-yp)**2)
```
```
... return (np.mean(Ein)/n,np.mean(Eout)/n)...
```
4.3 Theory of Learning 225
Fig. 4.16 The dots show the
learning curves estimated
from the simulation and the
solid lines show the
corresponding terms for our
analytical result. The
horizontal line shows the
variance of the additive noise
```
(σ2 = 1 in this case). Both
```
the expected in-sample and
out-of-sample errors
asymptotically approach this
line
Programming Tip
Python has an assert statement to make sure that certain entry conditions for
the variables in the function are satisfied. It is a good practice to use reasonable
assertions at entry and exit to improve the quality of code.
The following runs the simulation for the given value of d.
```
>>> d=10>>> xi = arange(d*2,d*10,d//2)
```
```
>>> ei,eo=np.array([est_errors(d=d,n=n,niter=100) for n in xi]).T
```
which results in Fig. 4.16. This figure shows the estimated expected in-sample and
out-of-sample errors from our simulation compared with our corresponding analyti-
cal result. The heavy horizontal line shows the variance of the additive noise σ2 = 1.
Both these curves approach this asymptote because the noise is the ultimate learning
limit for this problem. For a given dimension d, even with an infinite amount of
training data, the learning method cannot generalize beyond the limit of the noise
```
power. Thus, the expected generalization error is E(Eout) − E(Ein) = 2σ2 dn .
```
4.4 Decision Trees
A decision tree is the easiest classifer to understand, interpret, and explain. A decision
tree is constructed by recursively splitting the data set into a sequence of subsets based
```
on if-then questions. The training set consists of pairs (x, y) where x ∈ Rd where
```
d is the number of features available and where y is the corresponding label. The
learning method splits the training set into groups based on x while attempting to
keep the assignments in each group as uniform as possible. In order to do this, the
learning method must pick a feature and an associated threshold for that feature upon
which to divide the data. This is tricky to explain in words, but easy to see with an
example. First, let’s set up the Scikit-learn classifer,
226 4 Machine Learning
```
>>> from sklearn import tree>>> clf = tree.DecisionTreeClassifier()
```
Let’s also create some example data,
```
>>> import numpy as np>>> M=np.fromfunction(lambda i,j:j>=2,(4,4)).astype(int)
```
>>> print M[ [0 0 1 1]
[0 0 1 1][0 0 1 1]
[0 0 1 1] ]
Programming Tip
The fromfunction creates Numpy arrays using the indicies as inputs to a
```
function whose value is the corresponding array entry.
```
We want to classify the elements of the matrix based on their respective positions in
the matrix. By just looking at the matrix, the classification is pretty simple—classify
as 0 for any positions in the first two columns of the matrix, and classify 1 otherwise.
Let’s walk through this formally and see if this solution emerges from the decision
tree. The values of the array are the labels for the training set and the indicies of
```
those values are the elements of x. Specifically, the training set has X = {(i, j)} and
```
```
Y = {0, 1} Now, let’s extract those elements and construct the training set.
```
```
>>> i,j = np.where(M==0)>>> x=np.vstack([i,j]).T # build nsamp by nfeatures
```
```
>>> y = j.reshape(-1,1)*0 # 0 elements>>> print x
```
[ [0 0][0 1]
[1 0][1 1]
[2 0][2 1]
[3 0][3 1] ]
>>> print y[ [0]
[0][0]
[0][0]
[0][0]
[0] ]
Thus, the elements of x are the two-dimensional indicies of the values of y. For
example, M[x[0,0],x[0,1] ] = y[0,0]. Likewise, to complete the training
set, we just need to stack the rest of the data to cover all the cases,
```
>>> i,j = np.where(M==1)>>> x=np.vstack([np.vstack([i,j]).T,x ]) # build nsamp x nfeatures
```
```
>>> y=np.vstack([j.reshape(-1,1)*0+1,y]) # 1 elements
```
4.4 Decision Trees 227
With all that established, all we have to do is train the classifer,
```
>>> clf.fit(x,y)DecisionTreeClassifier(compute_importances=None, criterion=’gini’,
```
```
max_depth=None, max_features=None, max_leaf_nodes=None,min_density=None, min_samples_leaf=1, min_samples_split=2,
```
```
random_state=None, splitter=’best’)
```
To evaluate how the classifer performed, we can report the score,
```
>>> clf.score(x,y)1.0
```
For this classifer, the score is the accuracy, which is defined as the ratio of the sum of
```
the true-positive (T P) and true-negatives (T N ) divided by the sum of all the terms,
```
including the false terms,
```
accuracy = T P + T NT P + T N + F N + F P
```
In this case, the classifier gets every point correctly, so F N = F P = 0. On a
related note, two other common names from information retrieval theory are recall
```
(a.k.a. sensitivity) and precision (a.k.a. positive predictive value, T P/(T P + F P)).
```
```
We can visualize this tree in Fig. 4.17. The Gini coefficients (a.k.a. categorical vari-
```
```
ance) in the figure are a measure of the purity of each so-determined class. This
```
coefficient is defined as,
```
Ginim =
```
∑
k
```
p m,k (1 − p m,k )
```
where
p m,k = 1N
m
∑
x i ∈R m
```
I (yi = k)
```
```
which is the proportion of observations labeled k in the mth node and I (·) is the
```
usual indicator function. Note that the maximum value of the Gini coefficient is
max Ginim = 1 − 1/m. For our simple example, half of the sixteen samples are in
Fig. 4.17 Example decision
tree. The Gini coefficient in
each branch measures the
purity of the partition in each
node. The samples item in
the box shows the number of
items in the corresponding
node in the decision tree
228 4 Machine Learning
category 0 and the other half are in the 1 category. Using the notation above, the top
box corresponds to the 0th node, so p0,0 = 1/2 = p0,1 . Then, Gini0 = 0.5. The
next layer of nodes in Fig. 4.17 is determined by whether or not the second dimension
of the x data is greater than 1.5. The Gini coefficients for each of these child nodes
is zero because after the prior split, each subsequent category is pure. The value
list in each of the nodes shows the distribution of elements in each category at each
node.
To make this example more interesting, we can contaminate the data slightly,
>>> M[1,0]=1 # put in different class>>> print M # now contaminated
[ [0 0 1 1][1 0 1 1]
[0 0 1 1][0 0 1 1] ]
Now we have a 1 entry in the previously pure first column’s second row.
```
>>> i,j = np.where(M==0)>>> x=np.vstack([i,j]).T
```
```
>>> y = j.reshape(-1,1)*0>>> i,j = np.where(M==1)
```
```
>>> x=np.vstack([np.vstack([i,j]).T,x])>>> y = np.vstack([j.reshape(-1,1)*0+1,y])
```
```
>>> clf.fit(x,y)DecisionTreeClassifier(compute_importances=None, criterion=’gini’,
```
```
max_depth=None, max_features=None, max_leaf_nodes=None,min_density=None, min_samples_leaf=1, min_samples_split=2,
```
```
random_state=None, splitter=’best’)
```
The result is shown in Fig. 4.18. Note the tree has grown significantly due to this one
change! The 0th node has the following parameters, p0,0 = 7/16 and p0,1 = 9/16.
This makes the Gini coefficient for the 0th node equal to 716
```
(
```
1 − 716
```
)
```
- 916 (1 − 916 ) =
0.492. As before, the root node splits on X[1] ≤ 1.5. Let’s see if we can reconstruct
the succeeding layer of nodes manually, as in the following,
```
>>> y[x[:,1]>1.5] # first node on the rightarray([ [1],
```
[1],[1],
[1],[1],
[1],[1],
```
[1] ])
```
This obviously has a zero Gini coefficient. Likewise, the node on the left contains
the following,
```
>>> y[x[:,1]<=1.5] # first node on the leftarray([ [1],
```
[0],[0],
[0],[0],
[0],[0],
```
[0] ])
```
4.4 Decision Trees 229
Fig. 4.18 Decision tree for contaminated data. Note that just one change in the training data caused
the tree to grow five times as large as before!
```
The Gini coefficient in this case is computed as (1/8)*(1-1/8)+(7/8)*
```
```
(1-7/8)=0.21875. This node splits based on X[1] < 0.5. The child node to
```
the right derives from the following equivalent logic,
```
>>> np.logical_and(x[:,1]<=1.5,x[:,1]>0.5)array([False, False, False, False, False, False, False, False, False,
```
```
False, True, True, False, True, False, True], dtype=bool)
```
with corresponding classes,
```
>>> y[np.logical_and(x[:,1]<=1.5,x[:,1]>0.5)]array([ [0],
```
[0],[0],
```
[0] ])
```
Programming Tip
The logical_and in Numpy provides element-wise logical conjuction. It
is not possible to accomplish this with something like 0.5 < x[:, 1] <= 1.5
because of the way Python parses this syntax.
230 4 Machine Learning
Fig. 4.19 The decision tree divides the training set into regions by splitting successively along each
dimension until each region is as pure as possible
Notice that for this example as well as for the previous one, the decision tree was
```
exactly able memorize (overfit) the data with perfect accuracy. From our discussion
```
of machine learning theory, this is an indication potential problems in generalization.
The key step in building the decision tree is to come up with the initial split. There
are the number of algorithms that can build decision trees based on different criteria,
but the general idea is to control the information entropy as the tree is developed.
In practical terms, this means that the algorithms attempt to build trees that are not
excessively deep. It is well-established that this is a very hard problem to solve
completely and there are many approaches to it. This is because the algorithms must
make global decisions at each node of the tree using the local data available up to
that point.
For this example, the decision tree partitions the X space into different regions
corresponding to different Y labels as shown in Fig. 4.19. The root node at the top
of Fig. 4.18 splits the input data based on X[1] ≤ 1.5. This corresponds to the top
```
left panel in Fig. 4.19 (i.e., node 0) where the vertical line divides the training data
```
shown into two regions, corresponding to the two subsequent child nodes. The next
split happens with X[1] ≤ 0.5 as shown in the next panel of Fig. 4.19 titled node
1. This continues until the last panel on the lower right, where the contaminated
element we injected has been isolated into its own sub-region. Thus, the last panel
is a representation of Fig. 4.18, where the horizontal/vertical lines correspond to
successive splits in the decision tree.
4.4 Decision Trees 231
Fig. 4.20 The decision tree
fitted to this triangular matrix
is very complex, as shown by
the number of horizontal and
vertical partitions. Thus,
even though the pattern in the
training data is visually clear,
the decision tree cannot
automatically uncover it
Figure 4.20 shows another example, but now using a simple triangular matrix.
As shown by the number of vertical and horizontal partitioning lines, the decision
tree that corresponds to this figure is tall and complex. Notice that if we apply a
simple rotational transform to the training data, we can obtain Fig. 4.21, which
requires a trivial decision tree to fit. Thus, there may be transformations of the training
data that simplify the decision tree, but these are very difficult to derive in general.
Nonetheless, this highlights a key weakness of decision trees wherein they may be
easy to understand, to train, and to deploy, but may be completely blind to such
time-saving and complexity-saving transformations. Indeed, in higher dimensions,
it may be impossible to even visualize the potential of such latent transformations.
Thus, the advantages of decision trees can be easily outmatched by other methods
that we will study later that do have the ability to uncover useful transformations,
but which will necessarily be harder to train. Another disadvantage is that because
of how decision trees are built, even a single misplaced data point can cause the tree
to grow very differently. This is a symptom of high variance.
In all of our examples, the decision tree was able to memorize the training data
exactly, as we discussed earlier, this is a sign of potential generalization errors. There
are pruning algorithms that strategically remove some of the deepest nodes. but
these are not yet fully implemented in Scikit-learn, as of this writing. Alternatively,
restricting the maximum depth of the decision tree can have a similar effect. The
DecisionTreeClassifier and DecisionTreeRegressor in Scikit-learn
both have keyword arguments that specify maximum depth.
232 4 Machine Learning
Fig. 4.21 Using a simple
rotation on the training data
in Fig. 4.20, the decision tree
can now easily fit the training
data with a single partition
4.4.1 Random Forests
It is possible to combine a set of decision trees into a larger composite tree that has
better performance than its individual components by using ensemble learning. This
is implemented in Scikit-learn as RandomForestClassifier. The composite
tree helps mitigate the primary weakness of decision trees—high variance. Random
forest classifiers help by averaging out the predictions of many constituent trees to
minimize this variance by randomly selecting subsets of the training set to train the
embedded trees. On the other hand, this randomization can increase bias because
there may be a subset of the training set that yields an excellent decision tree, but
the averaging effect over randomized training samples washes this out in the same
averaging that reduces the variance. This is a key trade-off. The following code
implements a simple random forest classifer from our last example.
```
>>> from sklearn.ensemble import RandomForestClassifier>>> rfc = RandomForestClassifier(n_estimators=4,max_depth=2)
```
```
>>> rfc.fit(X_train,y_train.flat)RandomForestClassifier(bootstrap=True, compute_importances=None,
```
```
criterion=’gini’, max_depth=2, max_features=’auto’,max_leaf_nodes=None, min_density=None, min_samples_leaf=1,
```
```
min_samples_split=2, n_estimators=4, n_jobs=1, oob_score=False,random_state=None, verbose=0)
```
Note that we have constrained the maximum depth max_depth=2 to help with
generalization. To keep things simple we have only set up a forest with four individual
classifers. 3 Figure 4.23 shows the individual classifers in the forest that have been
trained above. Even though all the constituent decision trees share the same training
```
data, the random forest algorithm randomly picks feature subsets (with replacement)
```
3 We have also set the random seed to a fixed value to make the figures reproducible in the IPython
Notebook corresponding to this section.
4.4 Decision Trees 233
Fig. 4.22 The constituent decision trees of the random forest and how they partitioned the training
set are shown in these four panels. The random forest classifier uses the individual outputs of each
of the constituent trees to produce a collaborative final estimate
upon which to train individual trees. This helps avoid the tendency of decision trees
to become too deep and lopsided, which hurts both performance and generalization.
At the prediction step, the individual outputs of each of the constituent decision
trees are put to a majority vote for the final classification. To estimate generalization
errors without using cross-validation, the training elements not used for a particular
constituent tree can be used to test that tree and form a collaborative estimate of
generalization errors. This is called the out-of-bag estimate.
The main advantage of random forest classifiers is that they require very
little tuning and provide a way to trade-off bias and variance via averaging and ran-
```
domization. Furthermore, they are fast and easy to train in parallel (see the n_jobs
```
```
keyword argument) and fast to predict. On the downside, they are less interpretable
```
than simple decision trees. There are many other powerful tree methods in Scikit-learn
like ExtraTrees and Gradient Boosted Regression Trees GradientBoosting
Regressor which are discussed in the online documentation.
234 4 Machine Learning
Fig. 4.23 This scatterplot
shows the binary Y variables
and the corresponding x data
for each category
4.5 Logistic Regression
The Bernoulli distribution we studied earlier answers the question of which of two
```
outcomes (Y ∈ {0, 1}) would be selected with probability, p.
```
```
P(Y ) = p Y (1 − p)1−Y
```
We also know how to solve the corresponding likelihood function for the maximum
```
likelihood estimate of p given observations of the output, {Yi }ni=1 . However, now
```
we want to include other factors in our estimate of p. For example, suppose we
observe not just the outcomes, but a corresponding continuous variable, x. That is,
```
the observed data is now {(x i , Yi )}ni=1 How can we incorporate x into our estimation
```
of p?
The most straightforward idea is to model p = ax + b where a, b are parameters
of a fitted line. However, because p is a probability with value bounded between
zero and one, we need to wrap this estimate in another function that can map the
```
entire real line into the [0, 1] interval. The logistic (a.k.a. sigmoid) function has this
```
property,
```
θ(s) = e
```
s
1 + e s
Thus, the new parameterized estimate for p is the following,
```
ˆp = θ(ax + b) = e
```
ax+b
```
1 + e ax+b (4.5.0.1)
```
4.5 Logistic Regression 235
This is usually expressed using the logit function,
```
logit(t) = log t1 − t
```
as,
```
logit( p) = b + ax
```
More continuous variables can be accommodated easily as
```
logit( p) = b +
```
∑
k
a k x k
This can be further extended beyond the binary case to multiple target labels. The
maximum likelihood estimate of this uses numerical optimization methods that are
implemented in Scikit-learn.
Let’s construct some data to see how this works. In the following, we assign class
labels to a set of randomly scattered points in the two-dimensional plane,
>>> import numpy as np>>> from matplotlib.pylab import subplots
>>> v = 0.9>>> @np.vectorize
```
... def gen_y(x):... if x<5: return np.random.choice([0,1],p=[v,1-v])
```
```
... else: return np.random.choice([0,1],p=[1-v,v])...
```
```
>>> xi = np.sort(np.random.rand(500)*10)>>> yi = gen_y(xi)
```
Programming Tip
The np.vectorize decorator used in the code above makes it easy to avoid
looping in code that uses Numpy arrays by embedding the looping semantics
inside of the so-decorated function. Note, however, that this does not neces-
sarily accelerate the wrapped function. It’s mainly for convenience.
Figure 4.23 shows a scatter plot of the data we constructed in the above code,
```
{(x i , Yi )}. As constructed, it is more likely that large values of x correspond to Y = 1.
```
On the other hand, values of x ∈ [4, 6] of either category are heavily overlapped. This
means that x is not a particularly strong indicator of Y in this region. Figure 4.24
shows the fitted logistic regression curve against the same data. The points along
the curve are the probabilities that each point lies in either of the two categories.
For large values of x the curve is near one, meaning that the probability that the
associated Y value is equal to one. On the other extreme, small values of x mean
that this probability is close to zero. Because there are only two possible categories,
this means that the probability of Y = 0 is thereby higher. The region in the middle
corresponding to the middle probabilities reflect the ambiguity between the two
236 4 Machine Learning
catagories because of the overlap in the data for this region. Thus, logistic regression
cannot make a strong case for one category here. The following code fits the logistic
regression model,
```
>>> from sklearn.linear_model import LogisticRegression>>> lr = LogisticRegression()
```
```
>>> lr.fit(np.c_[xi],yi)LogisticRegression(C=1.0, class_weight=None, dual=False, fit_intercept=True,
```
```
intercept_scaling=1, penalty=’l2’, random_state=None, tol=0.0001)
```
For a deeper understanding of logistic regression, we need to alter our notation
slightly and once again use our projection methods. More generally we can rewrite
Eq. 4.5.0.1 as the following,
```
p(x) = 1
```
```
1 + exp(−βT x)
```
```
(4.5.0.2)
```
where β, x ∈ Rn . From our prior work on projection we know that the signed per-
pendicular distance between x and the linear boundary described by β is βT x/‖β‖.
This means that the probability that is assigned to any point in Rn is a function of
how close that point is to the linear boundary described by the following equation,
βT x = 0
But there is something subtle hiding here. Note that for any α ∈ R,
αβT x = 0
describes the same hyperplane. This means that we can multiply β by an arbi-
```
trary scalar and still get the same geometry. However, because of exp(−αβT x) in
```
Eq. 4.5.0.2, this scaling determines the intensity of the probability attributed to x. This
```
is illustrated in Fig. 4.25. The panel on the left shows two categories (squares/circles)
```
Fig. 4.24 This shows the
fitted logistic regression on
the data shown in Fig. 4.22.
The points along the curve
are the probabilities that each
point lies in either of the two
categories
4.5 Logistic Regression 237
split by the dotted line that is determined by βT x = 0. The background colors shows
the probabilities assigned to points in the plane. The right panel shows that by scal-
ing with α, we can increase the probabilities of class membership for the given
points, given the exact same geometry. The points near the boundary have lower
probabilities because they could easily be on the opposite side. However, by scaling
by α, we can raise those probabilities to any desired level at the cost of driving the
points further from the boundary closer to one. Why is this a problem? By driving the
probabilities arbitrarily using α, we can overemphasize the training set at the cost of
out-of-sample data. That is, we may wind up insisting on emphatic class membership
of yet unseen points that are close to the boundary that otherwise would have more
```
equivocal probabilities (say, near 1/2). Once again, this is another manifestation of
```
bias/variance trade-off.
Regularization is a method that controls this effect by penalizing the size of β as
part of its solution. Algorithmically, logistic regression works by iteratively solving
a sequence of weighted least squares problems. Regression adds a ‖β‖/C term to
the least squares error. To see this in action, let’s create some data from a logistic
regression and see if we can recover it using Scikit-learn. Let’s start with a scatter of
points in the two-dimensional plane,
```
>>> x0,x1=np.random.rand(2,20)*6-3>>> X = np.c_[x0,x1,x1*0+1] # stack as columns
```
Note that X has a third column of all ones. This is a trick to allow the corresponding
line to be offset from the origin in the two-dimensional plane. Next, we create a linear
boundary and assign the class probabilities according to proximity to the boundary.
Fig. 4.25 Scaling can arbitrarily increase the probabilities of points near the decision boundary
238 4 Machine Learning
```
>>> beta = np.array([1,-1,1]) # last coordinate for affine offset>>> prd = X.dot(beta)
```
```
>>> probs = 1/(1+np.exp(-prd/np.linalg.norm(beta)))>>> c = (prd>0) # boolean array class labels
```
This establishes the training data. The next block creates the logistic regression object
and fits the data.
```
>>> lr = LogisticRegression()>>> _=lr.fit(X[:,:-1],c)
```
Note that we have to omit the third dimension because of how Scikit-learn inter-
nally breaks down the components of the boundary. The resulting code extracts the
corresponding β from the LogisticRegression object.
>>> betah = np.r_[lr.coef_.flat,lr.intercept_]
Programming Tip
The Numpy np.r_ object provides a quick way to stack Numpy arrays
horizontally instead of using np.hstack.
The resulting boundary is shown in the left panel in Fig. 4.26. The crosses and
triangles represent the two classes we created above, along with the separating gray
line. The logistic regression fit produces the dotted black line. The dark circle is the
point that logistic regression categorizes incorrectly. The regularization parameter is
```
Fig. 4.26 The left panel shows the resulting boundary (dashed line) with C = 1 as the regularization
```
parameter. The right panel is for C = 1000. The gray line is the boundary used to assign the class
membership for the synthetic data. The dark circle is the point that logistic regression categorizes
incorrectly
4.5 Logistic Regression 239
```
C = 1 by default. Next, we can change the strength of the regularization parameter
```
as in the following,
```
>>> lr = LogisticRegression(C=1000)
```
and the re-fit the data to produce the right panel in Fig. 4.26. By increasing the
regularization parameter, we essentially nudged the fitting algorithm to believe the
data more than the general model. That is, by doing this we accepted more variance
in exchange for better bias.
4.5.1 Generalized Linear Models
Logistic regression is one example of a wider class of generalized linear models
that embed non-linear transformations in the fitting process. Let’s back up and break
down logistic regression into smaller parts. As usual, we want to estimate the condi-
```
tional expectation E(Y |X = x). For plain linear regression, we have the following
```
approximation,
```
E(Y |X = x) ≈ βT x
```
```
For notation sake, we call r(x) := E(Y |X = x) the response. For logistic regression,
```
```
because Y ∈ {0, 1}, we have E(Y |X = x) = P(Y |X = x) and the transformation
```
```
makes r(x) linear.
```
```
η(x) = βT x
```
```
= log r(x)1 − r(x)
```
```
= g(r(x))
```
```
where g is defined as the logistic link function. The η(x) function is the linear
```
predictor. Now that we have transformed the original data space using the logistic
```
function to create the setting for the linear predictor, why don’t we just do the same
```
```
thing for the Yi data? That is, for plain linear regression, we usually take data, {X i , Yi }
```
```
and then use it to fit an approximation to E(Y |X = x). If we are transforming the
```
conditional expectation using the logarithm, which we are approximating using Yi ,
then why don’t we correspondingly transform the binary Yi data? The answer is that
```
if we did so then we would get the logarithm of zero (i.e., infinity) or one (i.e., zero),
```
which is not workable. The alternative is to use a linear Taylor approximation, like
```
we did earlier with the delta method, to expand the g function around r(x), as in the
```
following,
240 4 Machine Learning
```
g(Y ) ≈ log r(x)1 − r(x) + Y − r(x)r(x) − r(x)2
```
```
= η(x) + Y − r(x)r(x) − r(x)2
```
```
The interesting part is the Y − r(x) term, because this is where the class label data
```
```
enters the problem. The expectation E(Y − r(x)|X) = 0 so we can think of this
```
```
differential as additive noise that dithers η(x). The variance of g(Y ) is the following,
```
```
V(g(Y )|X) = V(η(x)|X) + 1(r(x)(1 − r(x)))2 V(Y − r(x)|X)
```
```
= 1(r(x)(1 − r(x)))2 V(Y − r(x)|X)
```
```
Note that V(Y |X) = r(x)(1 − r(x)) because Y is a binary variable. Ultimately, this
```
boils down to the following,
```
V(g(Y )|X) = 1r(x)(1 − r(x))
```
Note that the variance is a function of x, which means it is heteroskedastic, meaning
that the iterative minimum-variance-finding algorithm that computes β downplays
```
x where r(x) ≈ 0 and r(x) ≈ 1 because the peak of the variance occurs where
```
```
r(x) ≈ 0.5, which are those equivocal points close to the boundary.
```
For generalized linear models, the above sequence is the same and consists of
```
three primary ingredients: the linear predictor (η(x)), the link function (g(x)), and
```
```
the dispersion scale function, Vds such that V(Y |X) = σ2 Vds (r(x)). For logistic
```
```
regression, we have Vds (r(x)) = r(x)(1 − r(x)) and σ2 = 1. Note that absolute
```
knowledge of σ2 is not important because the iterative algorithm needs only a rel-
ative proportional scale. To sum up, the iterative algorithm takes a linear predic-
```
tion for η(x i ), computes the transformed responses, g(Yi ), calculates the weights
```
```
wi =
```
[
```
(g′(r(x i ))Vds (r(x i )))
```
]−1
```
, and then does a weighted linear regression of g(yi )
```
onto x i with the weights wi to compute the next β. More details can be found in the
following [3–5].
4.6 Regularization
We have referred to regularization in earlier sections, but we want to develop this
important idea more fully. Regularization is the mechanism by which we navigate
the bias/variance trade-off. To get started, let’s consider a classic constrained least
squares problem,
4.6 Regularization 241
minimizex ‖x‖22
subject to: x0 + 2x1 = 1
where ‖x‖2 =
√
x20 + x21 is the L2 norm. Without the constraint, it would be easy to
minimize the objective function—just take x = 0. Otherwise, suppose we somehow
know that ‖x‖2 < c, then the locus of points defined by this inequality is the circle
in Fig. 4.27. The constraint is the line in the same figure. Because every value of c
defines a circle, the constraint is satisfied when the circle touches the line. The circle
can touch the line at many different points, but we are only interested in the smallest
such circle because this is a minimization problem. Intuitively, this means that we
inflate a L2 ball at the origin and stop when it just touches the contraint. The point
of contact is our L2 minimization solution.
We can obtain the same result using the method of Lagrange multipliers. We
can rewrite the entire L2 minimization problem as one objective function using the
Lagrange multiplier, λ,
```
J (x0, x1, λ) = x20 + x21 + λ(1 − x0 − x1)
```
and solve this as an ordinary function using calculus. Let’s do this using Sympy.
```
>>> import sympy as S>>> S.var(’x:2 l’,real=True)
```
```
(x0, x1, l)>>> J=S.Matrix([x0,x1]).norm()**2 + l*(1-x0-2*x1)
```
```
>>> sol=S.solve(map(J.diff,[x0,x1,l]))>>> print sol
```
```
{x0: 1/5, x1: 2/5, l: 2/5}
```
Fig. 4.27 The solution of
the constrained L2
minimization problem is at
the point where the
```
constraint (dark line)
```
```
intersects the L2 ball (gray
```
```
circle) centered at the origin.
```
The point of intersection is
indicated by the dark circle.
The two neighboring squares
indicate points on the line
that are close to the solution
242 4 Machine Learning
Programming Tip
Using the Matrix object is overkill for this problem but it does demon-
strate how Sympy’s matrix machinery works. In this case, we are using the
norm method to compute the L2 norm of the given elements. Using S.var
defines Sympy variables and injects them into the global namespace. It is more
```
Pythonic to do something like x0 = S.symbols(’x0’,real=True)
```
instead but the other way is quicker, especially for variables with many dimen-
sions.
The solution defines the exact point where the line is tangent to the circle in Fig. 4.27.
The Lagrange multiplier has incorporated the constraint into the objective function.
There is something subtle and very important about the nature of the solution,
however. Notice that there are other points very close to the solution on the circle,
indicated by the squares in Fig. 4.27. This closeness could be a good thing, in case
it helps us actually find a solution in the first place, but it may be unhelpful in so far
as it creates ambiguity. Let’s hold that thought and try the same problem using the
L1 norm instead of the L2 norm. Recall that
‖x‖1 =
d∑
```
i=1
```
|x i |
where d is the dimension of the vector x. Thus, we can reformulate the same problem
in the L1 norm as in the following,
minimizex ‖x‖1
subject to: x1 + 2x2 = 1
It turns out that this problem is somewhat harder to solve using Sympy, but we have
convex optimization modules in Python that can help.
```
>>> from cvxpy import Variable, Problem, Minimize, norm1, norm2>>> x=Variable(2,1,name=’x’)
```
```
>>> constr=[np.matrix([ [1,2] ])*x==1]>>> obj=Minimize(norm1(x))
```
```
>>> p= Problem(obj,constr)>>> p.solve()
```
0.49999999996804073>>> print x.value
[ [ 6.20344267e-10][ 5.00000000e-01] ]
4.6 Regularization 243
Programming Tip
The cvxy module provides a unified and accessible interface to the powerful
cvxopt convex optimization package, as well as other open-source solver
packages.
As shown in Fig. 4.28, the constant-norm contour in the L1 norm is shaped like
a diamond instead of a circle. Furthermore, the solutions found in each case are
different. Geometrically, this is because inflating the circular L2 reaches out in all
directions whereas the L1 ball creeps out along the principal axes. This effect is much
more pronounced in higher dimensional spaces where L1 -balls get more spikey.4 Like
the L2 case, there are also neighboring points on the constraint line, but notice that
these are not close to the boundary of the corresponding L1 ball, as they were in the
L2 case. This means that these would be harder to confuse with the optimal solution
because they correspond to a substantially different L1 ball.
To double-check our earlier L2 result, we can also use the cvxpy module to find
the L2 solution as in the following code,
```
>>> constr=[np.matrix([ [1,2] ])*x==1]>>> obj=Minimize(norm2(x)) #L2 norm
```
```
>>> p= Problem(obj,constr)>>> p.solve()
```
0.4472135953578661>>> print x.value
[ [ 0.2][ 0.4] ]
Fig. 4.28 The diamond is
the L1 ball in two
dimensions and the line is
the constraint. The point of
intersection is the solution to
the optimization problem.
Note that for L1
optimization, the two nearby
points on the constraint
```
(squares) do not touch the
```
L1 ball. Compare this with
Fig. 4.27
4 We discussed the geometry of high dimensional space when we covered the curse of dimensionality
in the statistics chapter.
244 4 Machine Learning
The only change to the code is the L2 norm and we get the same solution as before.
Let’s see what happens in higher dimensions for both L2 and L1 as we move from
two dimensions to four dimensions.
```
>>> x=Variable(4,1,name=’x’)>>> constr=[np.matrix([ [1,2,3,4] ])*x==1]
```
```
>>> obj=Minimize(norm1(x))>>> p= Problem(obj,constr)
```
```
>>> p.solve()0.24999999913550727
```
>>> print x.value[ [ 3.88487127e-10]
[ 8.33295433e-10][ 7.97158525e-10]
[ 2.49999999e-01] ]
And also in the L2 case with the following code,
```
>>> constr=[np.matrix([ [1,2,3,4] ])*x==1]>>> obj=Minimize(norm2(x))
```
```
>>> p= Problem(obj,constr)>>> p.solve()
```
0.18257418572129205>>> print x.value
[ [ 0.03333333][ 0.06666667]
[ 0.1 ][ 0.13333333] ]
Note that the L1 solution has selected out only one dimension for the solution, as the
other components are effectively zero. This is not so with the L2 solution, which has
meaningful elements in multiple coordinates. This is because the L1 problem has
many pointy corners in the four dimensional space that poke at the hyperplane that
```
is defined by the constraint. This essentially means the subsets (namely, the points at
```
```
the corners) are found as solutions because these touch the hyperplane. This effect
```
becomes more pronounced in higher dimensions, which is the main benefit of using
the L1 norm as we will see in the next section.
4.6.1 Ridge Regression
Now that we have a sense of the geometry of the situation, let’s revisit our classic
linear regression probem. To recap, we want to solve the following problem,
minβ∈Rp ‖y − Xβ‖
where X =
[
x1, x2, . . . , xp
]
and xi ∈ Rn . Furthermore, we assume that the p column
```
vectors are linearly independent (i.e., rank(X) = p). Linear regression produces
```
the β that minimizes the mean squared error above. In the case where p = n, there
is a unique solution to this problem. However, when p < n, then there are infinitely
many solutions.
4.6 Regularization 245
To make this concrete, let’s work this out using Sympy. First, let’s define an
example X and y matrix,
>>> import sympy as S>>> from sympy import Matrix
```
>>> X = Matrix([ [1,2,3],... [3,4,5] ])
```
```
>>> y = Matrix([ [1,2] ]).T
```
Now, we can define our coefficient vector β using the following code,
```
>>> b0,b1,b2=S.symbols(’b:3’,real=True)>>> beta = Matrix([ [b0,b1,b2] ]).T # transpose
```
Next, we define the objective function we are trying to minimize
```
>>> obj=(X*beta -y).norm(ord=2)**2
```
Programming Tip
The Sympy Matrix class has useful methods like the norm function used
above to define the objective function. The ord=2 means we want to use the
L2 norm. The expression in parenthesis evaluates to a Matrix object.
Note that it is helpful to define real variables using the keyword argument whenever
applicable because it relieves Sympy’s internal machinery of dealing with complex
numbers. Finally, we can use calculus to solve this by setting the derivatives of the
objective function to zero.
```
>>> sol=S.solve([obj.diff(i) for i in beta])>>> beta.subs(sol)
```
```
Matrix([ [ b2],
```
```
[-2*b2 + 1/2],[ b2] ])
```
Notice that the solution does not uniquely specify all the components of the beta
variable. This is a consequence of the p < n nature of this problem where p = 2
and n = 3. While the existence of this ambiguity does not alter the solution,
```
>>> obj.subs(sol)0
```
But it does change the length of the solution vector beta,
```
>>> beta.subs(sol).norm(2)sqrt(2*b2**2 + (-2*b2 + 1/2)**2)
```
If we want to minimize this length we can easily use the same calculus as before,
```
>>> S.solve((beta.subs(sol).norm()**2).diff())[1/6]
```
246 4 Machine Learning
This provides the solution of minimum length in the L2 sense,
```
>>> betaL2=beta.subs(sol).subs(b2,S.Rational(1,6))>>> betaL2
```
```
Matrix([ [1/6],
```
```
[1/6],[1/6] ])
```
But what is so special about solutions of minimum length? For machine learning,
driving the objective function to zero is symptomatic of overfitting the data. Usually,
at the zero bound, the machine learning method has essentially memorized the train-
ing data, which is bad for generalization. Thus, we can effectively stall this problem
by defining a region for the solution that is away from the zero-bound.
minimizeβ ‖y − Xβ‖22
subject to: ‖β‖2 < c
where c is the tuning parameter. Using the same process as before, we can re-write
this as the following,
minβ∈Rp ‖y − Xβ‖22 + α‖β‖22
where α is the tuning parameter. These are the penalized or Lagrange forms of
these problems derived from the constrained versions. The objective function is
penalized by the ‖β‖2 term. For L2 penalization, this is called ridge regression. This
is implemented in Scikit-learn as Ridge. The following code sets this up for our
example,
```
>>> from sklearn.linear_model import Ridge>>> clf = Ridge(alpha=100.0,fit_intercept=False)
```
```
>>> clf.fit(np.array(X).astype(float),np.array(y).astype(float))Ridge(alpha=100.0, copy_X=True, fit_intercept=False, max_iter=None,
```
```
normalize=False, solver=’auto’, tol=0.001)
```
Note that the alpha scales of the penalty for the ‖β‖2 . We set the fit_
```
intercept=False argument to omit the extra offset term from our example.
```
The corresponding solution is the following,
>>> print clf.coef_[ [ 0.0428641 0.06113005 0.07939601] ]
To double-check the solution, we can use some optimization tools from Scipy and
our previous Sympy analysis, as in the following,
```
>>> from scipy.optimize import minimize>>> f = S.lambdify((b0,b1,b2),obj+beta.norm()**2*100.)
```
```
>>> g = lambda x:f(x[0],x[1],x[2])>>> out = minimize(g,[.1,.2,.3]) # initial guess
```
```
>>> out.xarray([ 0.0428641 , 0.06113005, 0.079396 ])
```
4.6 Regularization 247
Programming Tip
We had to define the additional g function from the lambda function we created
from the Sympy expression in f because the minimize function expects a
single object vector as input instead of a three separate arguments.
which produces the same answer as the Ridge object. To better understand the
meaning of this result, we can re-compute the mean squared error solution to this
problem in one step using matrix algebra instead of calculus,
```
>>> betaLS=X.T*(X*X.T).inv()*y>>> betaLS
```
```
Matrix([ [1/6],
```
```
[1/6],[1/6] ])
```
Notice that this solves the posited problem exactly,
```
>>> X*betaLS-yMatrix([
```
```
[0],[0] ])
```
This means that the first term in the objective function goes to zero,
‖y − XβL S ‖ = 0
But, let’s examine the L2 length of this solution versus the ridge regression solution,
```
>>> print betaLS.norm().evalf(), np.linalg.norm(clf.coef_)0.288675134594813 0.108985964126
```
Thus, the ridge regression solution is shorter in the L2 sense, but the first term in the
objective function is not zero for ridge regression,
```
>>> print (y-X*clf.coef_.T).norm()**21.86870864136429
```
```
Ridge regression solution trades fitting error (‖y − Xβ‖2 ) for solution length (‖β‖2 ).
```
Let’s see this in action with a familiar example from Sect. 3.12.4. Consider
Fig. 4.29. For this example, we created our usual chirp signal and attempted to
fit it with a high-dimensional polynomial, as we did in Sect. 4.3.4. The lower panel
is the same except with ridge regression. The shaded gray area is the space between
the true signal and the approximant in both cases. The horizontal hash marks indi-
cate the subset of x i values that each regressor was trained on. Thus, the training set
represents a non-uniform sample of the underlying chirp waveform. The top panel
shows the usual polynomial regression. Note that the regressor fits the given points
extremely well, but fails at the endpoint. The ridge regressor misses many of the
points in the middle, as indicated by the gray area, but does not overshoot at the
ends as much as the plain polynomial regression. This is the basic trade-off for ridge
regression. The Jupyter/IPython notebook has the code for this graph, but the main
steps are shown in the following,
248 4 Machine Learning
Fig. 4.29 The top figure
shows polynomial regression
and the lower panel shows
polynomial ridge regression.
The ridge regression does
not match as well throughout
most of the domain, but it
does not flare as violently at
the ends. This is because the
ridge constraint holds the
coefficient vector down at
the expense of poorer
performance along the
middle of the domain
```
# create chirp signalxi = np.linspace(0,1,100)[:,None]
```
```
# sample chirp randomlyxin= np.sort(np.random.choice(xi.flatten(),20,replace=False))[:,None]
```
```
# create sampled waveformy = cos(2*pi*(xin+xin**2))
```
```
# create full waveform for referenceyi = cos(2*pi*(xi+xi**2))
```
```
# create polynomial featuresqfit = PolynomialFeatures(degree=8) # quadratic
```
```
Xq = qfit.fit_transform(xin)# reformat input as polynomial
```
```
Xiq = qfit.fit_transform(xi)
```
```
lr=LinearRegression() # create linear modellr.fit(Xq,y) # fit linear model
```
```
# create ridge regression model and fitclf = Ridge(alpha=1e-9,fit_intercept=False)
```
```
clf.fit(Xq,y)
```
4.6.2 Lasso
Lasso regression follows the same basic pattern as ridge regression, except with the
L1 norm in the objective function.
minβ∈Rp ‖y − Xβ‖2 + α‖β‖1
4.6 Regularization 249
The interface in Scikit-learn is likewise the same. The following is the same problem
as before using lasso instead of ridge regression,
```
>>> X = np.matrix([ [1,2,3],... [3,4,5] ])
```
```
>>> y = np.matrix([ [1,2] ]).T>>> from sklearn.linear_model import Lasso
```
```
>>> lr = Lasso(alpha=1.0,fit_intercept=False)>>> _=lr.fit(X,y)
```
>>> print lr.coef_[ 0. 0. 0.32352941]
As before, we can use the optimization tools in Scipy to solve this also,
```
>>> from scipy.optimize import fmin>>> obj = 1/4.*(X*beta-y).norm(2)**2 + beta.norm(1)*l
```
```
>>> f = S.lambdify((b0,b1,b2),obj.subs(l,1.0))>>> g = lambda x:f(x[0],x[1],x[2])
```
```
>>> fmin(g,[0.1,0.2,0.3])Optimization terminated successfully.
```
Current function value: 0.360297Iterations: 121
```
Function evaluations: 221array([ 2.27469304e-06, 4.02831864e-06, 3.23134859e-01])
```
Programming Tip
The fmin function from Scipy’s optimization module uses an algorithm that
does not depend upon derivatives. This is useful because, unlike the L2 norm,
the L1 norm has sharp corners that make it harder to estimate derivatives.
This result matches the previous one from the Scikit-learn Lasso object. Solv-
ing it using Scipy is motivating and provides a good sanity check, but specialized
algorithms are required in practice. The following code block re-runs the lasso with
varying α and plots the coefficients in Fig. 4.30. Notice that as α increases, all but one
of the coefficients is driven to zero. Increasing α makes the trade-off between fitting
the data in the L2 sense and wanting to reduce the number of nonzero coefficients
```
(equivalently, the number of features used) in the model. For a given problem, it may
```
```
be more practical to focus on reducing the number of features in the model (i.e., large
```
```
α) than the quality of the data fit in the training data. The lasso provides a clean way
```
to navigate this trade-off.
The following code loops over a set of α values and collects the corresponding
lasso coefficients to be plotted in Fig. 4.30
```
>>> o=[]>>> alphas= np.logspace(-3,0,10)
```
```
>>> for a in alphas:... clf = Lasso(alpha=a,fit_intercept=False)
```
```
... _=clf.fit(X,y)... o.append(clf.coef_)
```
...
250 4 Machine Learning
Fig. 4.30 As α increases,
more of the model
coefficients are driven to
zero for lasso regression
4.7 Support Vector Machines
```
Support Vector Machines (SVM) originated from the statistical learning theory devel-
```
oped by Vapnik-Chervonenkis. As such, it represents a deep application of statistical
theory that incorporates the VC dimension concepts we discussed in the first section.
Let’s start by looking at some pictures. Consider the two-dimensional classification
```
problem shown in Fig. 4.31. Figure 4.31 shows two classes (gray and white circles)
```
that can be separated by any of the lines shown. Specifically, any such separating line
```
can be written as the locus of points (x) in the two-dimensional plane that satisfy the
```
following,
β0 + βT x = 0
To classify an arbitrary x using this line, we just compute the sign of β0 + βT x
and assign one class to the positive sign and the other class to the negative sign.
```
To uniquely specify such a separating line (or, hyperplane in a higher-dimensional
```
```
space) we need additional criteria.
```
Fig. 4.31 In the
two-dimensional plane, the
```
two classes (gray and white
```
```
circles) are easily separated
```
by any one of the lines
shown
4.7 Support Vector Machines 251
Fig. 4.32 The maximal
margin algorithm finds the
separating line that
maximizes the margin
shown. The elements that
touch the margins are the
support elements. The dotted
elements are not relevent to
the solution
Figure 4.32 shows the data with two bordering parallel lines that form a margin
around the central separating line. The maximal margin algorithm finds the widest
margin and the unique separating line. As a consequence, the algorithm uncovers
the elements in the data that touch the margins. These are the support elements. The
other elements away from the border are not relevent to the solution. This reduces
model variance because the solution is insensitive to the removal of elements other
```
than these supporting elements (usually a small minority).
```
To see how this works for linearly separable classes, consider a training set con-
```
sisting of {(x, y)} where y ∈ {−1, 1}. For any point xi , we compute the functional
```
```
margin as ˆγi = yi (β0 + βT xi ). Thus, ˆγi > 0 when xi is correctly classified. The
```
geometrical margin is γ = ˆγ/‖β‖. When xi is correctly classified, the geometrical
margin is equal to the perpendicular distance from xi to the line. Let’s look see how
the maximal margin algorithm works.
Let M be the width of the margin. The maximal margin algorithm is can be for-
mulated as a quadratic programming problem. We want to simultaneously maximize
the margin M while ensuring that all of the data points are correctly classified.
maximizeβ0 ,β,‖β‖=1 M
```
subject to: yi (β0 + βT xi ) ≥ M, i = 1, . . . , N .
```
The first line says we want to generate a maximum value for M by adjusting β0 and
β while keeping ‖β‖ = 1. The functional margins for each ith data element are
the constraints to the problem and must be satisfied for every proposed solution. In
words, the constraints enforce that the elements have to be correctly classified and
outside of the margin around the separating line. With some reformulation, it turns
out that M = 1/‖β‖ and this can be put into the following standard format,
minimizeβ0 ,β ‖β‖
```
subject to: yi (β0 + βT xi ) ≥ 1, i = 1, . . . , N .
```
252 4 Machine Learning
This is a convex optimization problem and can be solved using powerful methods in
that area.
The situation becomes more complex when the two classes are not separable and
we have to allow some unavoidable mixing between the two classes in the solution.
This means that the contraints have to modified as in the following,
```
yi (β0 + βT xi ) ≥ M(1 − ξi )
```
where the ξi are the slack variables and represent the proportional amount that the
prediction is on the wrong side of the margin. Thus, elements are misclassified when
ξi > 1. With these additional variables, we have a more general formulation of the
convex optimization problem,
minimizeβ0 ,β ‖β‖
```
subject to: yi (β0 + βT xi ) ≥ 1 − ξi ,
```
ξi ≥ 0,
∑
ξi ≤ constant, i = 1, . . . , N .
which can be rewritten in the following equivalent form,
minimizeβ0 ,β12 ‖β‖ + C
∑
ξi
```
subject to: yi (β0 + βT xi ) ≥ 1 − ξi , ξi ≥ 0 i = 1, . . . , N .
```
```
(4.7.0.1)
```
```
Because the ξi terms are all positive, the objective is to maximize the margin (i.e.,
```
```
minimize ‖β‖) while minimizing the proportional drift of the predictions to the
```
```
wrong side of the margin (i.e., C ∑ ξi ). Thus, large values of C shunt algorithmic
```
focus towards the correctly classified points near the decision boundary and small
values focus on further data. The value C is a hyperparameter for the SVM.
The good news is that all of these complicated pieces are handled neatly inside of
```
Scikit-learn. The following sets up the linear kernel for the SVM (more on kernels
```
```
soon),
```
>>> from sklearn.datasets import make_blobs>>> from sklearn.svm import SVC
```
>>> sv = SVC(kernel=’linear’)
```
We can create some synthetic data using make_blobs and then fit it to the SVM,
```
>>> X,y=make_blobs(n_samples=200, centers=2, n_features=2,... random_state=0,cluster_std=.5)
```
```
>>> sv.fit(X,y)SVC(C=1.0, cache_size=200, class_weight=None, coef0=0.0, degree=3, gamma=0.0,
```
```
kernel=’linear’, max_iter=-1, probability=False, random_state=None,shrinking=True, tol=0.001, verbose=False)
```
4.7 Support Vector Machines 253
Fig. 4.33 The two class
```
shown (white and gray
```
```
circles) are linearly
```
separable. The maximal
margin solution is shown by
the dark black line in the
middle. The dotted lines
show the extent of the
margin. The large circles
indicate the support vectors
for the maximal margin
solution
After fitting, the SVM now has the estimated support vectors and the coefficients
of the β in the sv.support_vectors_ and sv.coef_ attributes, respectively.
```
Figure 4.33 shows the two sample classes (white and gray circles) and the line
```
separating them that was found by the maximal margin algorithm. The two parallel
dotted lines show the margin. The large circles enclose the support vectors, which
are the data elements that are relevent to the solution. Notice that only these elements
can touch the edges of the margins.
Figure 4.34 shows what happens when the value of C changes. Increasing this
value emphasizes the ξ part of the objective function in Eq. 4.7.0.1. As shown in the
top left panel, a small value for C means that the algorithm is willing to accept many
support vectors at the expense of maximizing the margin. That is, the proportional
amount that predictions are on the wrong side of the margin is more acceptable with
smaller C. As the value of C increases, there are fewer support vectors because the
optimization process prefers to eliminate support vectors that are far away from the
margins and accept fewer of these that encroach into the margin. Note that as the
value of C progresses through this figure, the separating line tilts slightly.
4.7.1 Kernel Tricks
Support Vector Machines provide a powerful method to deal with linear separations,
but they can also apply to non-linear boundaries by exploiting the so-called kernel
trick. The convex optimization formulation of the SVM includes a dual formulation
that leads to a solution that requires only the inner-products of the features. The kernel
trick is to substitute inner-products by nonlinear kernel functions. This can be thought
of as mapping the original features onto a possibly infinite dimensional space of new
254 4 Machine Learning
Fig. 4.34 The maximal margin algorithm finds the separating line that maximizes the margin
shown. The elements that touch the margins are the support elements. The dotted elements are not
relevent to the solution
```
features. That is, if the data are not linearly separable in two-dimensional space (for
```
```
example) maybe they are separable in three-dimensional space (or higher)?
```
To make this concrete, suppose the original input space is Rn and we want to
use a non-linear mapping ψ : x  → F where F is an inner-product space of higher
dimension. The kernel trick is to calculate the inner-product in F using a kernel func-
```
tion, K (xi , x j ) = 〈ψ(xi ), ψ(x j )〉. The long way to compute this is to first compute
```
```
ψ(x) and then do the inner-product. The kernel-trick way to do it is to use the kernel
```
```
function and avoid computing ψ. In other words, the kernel function returns what the
```
inner-product in F would have returned if ψ had been applied. For example, to achieve
```
an nth polynomial mapping of the input space, we can use κ(xi , x j ) = (xTi x j + θ)n .
```
For example, suppose the input space is R2 and F = R4 and we have the following
mapping,
```
ψ(x) : (x0, x1)  → (x20 , x21 , x0 x1, x1 x0)
```
The inner product in F is then,
```
〈ψ(x), ψ(y)〉 = 〈x, y〉2
```
In other words, the kernel is the square of the inner product in input space. The
advantage of using the kernel instead of simply enlarging the feature space is com-
putational because you only need to compute the kernel on all distinct pairs of the
4.7 Support Vector Machines 255
input space. The following example should help make this concrete. First we create
some Sympy variables,
```
>>> import sympy as S>>> x0,x1=S.symbols(’x:2’,real=True)
```
```
>>> y0,y1=S.symbols(’y:2’,real=True)
```
Next, we create the ψ function that maps into R4 and the corresponding kernel
function,
```
>>> psi = lambda x,y: (x**2,y**2,x*y,x*y)>>> kern = lambda x,y: S.Matrix(x).dot(y)**2
```
Notice that the inner product in R4 is equal to the kernel function, which only uses
wthe R2 variables.
```
>>> print S.Matrix(psi(x0,x1)).dot(psi(y0,y1))x0**2*y0**2 + 2*x0*x1*y0*y1 + x1**2*y1**2
```
```
>>> print S.expand(kern((x0,x1),(y0,y1))) # same as abovex0**2*y0**2 + 2*x0*x1*y0*y1 + x1**2*y1**2
```
Polynomial Regression Using Kernels. Recall our favorite linear regression
problem from the regularization chapter,
minβ ‖y − Xβ‖2
where X is a n × m matrix with m > n. As we discussed, there are multiple solutions
to this problem. The least-squares solution is the following:
```
βL S = XT (XXT )-1y
```
Given a new feature vector x, the corresponding estimator for y is the following,
```
ˆy = xT βL S = xT XT (XXT )-1y
```
Using the kernel trick, the solution can be written more generally as the following,
```
ˆy = k(x)T K-1y
```
```
where the n × n kernel matrix K replaces XXT and where k(x) is a n-vector of
```
```
components k(x) = [κ(xi , x)] and where Ki, j = κ(xi , x j ) for the kernel function κ.
```
```
With this more general setup, we can substitute κ(xi , x j ) = (xTi x j +θ)n for nth-order
```
polynomial regression [6]. Note that ridge regression can also be incorporated by
```
inverting (K + αI), which can help stabilize poorly conditioned K matrices with a
```
tunable α hyper-parameter [6].
For some kernels, the enlarged F space is infinite-dimensional. Mercer’s condi-
tions provide technical restrictions on the kernel functions. Powerful, well-studied
kernels have been implemented in Scikit-learn. The advantage of kernel functions
may evaporate for when n → m in which case using the ψ functions instead can be
more practicable.
256 4 Machine Learning
4.8 Dimensionality Reduction
The features from a particular dataset that will ultimately prove important for
machine learning can be difficult to know ahead of time. This is especially true
for problems that do not have a strong physical underpinning. The row-dimension
```
of the input matrix (X) for fitting data in Scikit-learn is the number of samples and
```
the column dimension is the number of features. There may be a large number of
column dimensions in this matrix, and the purpose of dimensionality reduction is
to somehow reduce these to only those columns that are important for the machine
learning task.
Fortunately, Scikit-learn provides some powerful tools to help uncover the most
```
relevant features. Principal Component Analysis (PCA) consists of taking the input
```
```
X matrix and (1) subtracting the mean, (2) computing the covariance matrix, and
```
```
(3) computing the eigenvalue decomposition of the covariance matrix. For example,
```
if X has more columns than is practicable for a particular learning method, then PCA
can reduce the number of columns to a more manageable number. PCA is widely used
in statistics and other areas beyond machine learning, so it is worth examining what
it does in some detail. First, we need the decomposition module from Scikit-learn.
>>> from sklearn import decomposition>>> import numpy as np
```
>>> pca = decomposition.PCA()
```
Let’s create some very simple data and apply PCA.
```
>>> x = np.linspace(-1,1,30)>>> X = np.c_[x,x+1,x+2] # stack as columns
```
```
>>> pca.fit(X)PCA(copy=True, n_components=None, whiten=False)
```
>>> print pca.explained_variance_ratio_[ 1.00000000e+00 4.44023384e-32 6.35796894e-33]
Programming Tip
The np.c_ is a shorcut method for creating stacked column-wise arrays.
In this example, the columns are just constant offsets of the first column. The
explained variance ratio is the percentage of the variance attributable to the trans-
formed columns of X. You can think of this as the information that is relatively
concentrated in each column of the transformed matrix X. Figure 4.35 shows the
graph of this dominant transformed column in the bottom panel.
To make this more interesting, let’s change the slope of each of the columns as in
the following,
```
>>> X = np.c_[x,2*x+1,3*x+2,x] # change slopes of columns>>> pca.fit(X)
```
```
PCA(copy=True, n_components=None, whiten=False)>>> print pca.explained_variance_ratio_
```
[ 1.00000000e+00 8.94906713e-33 1.06089989e-33 9.50578639e-35]
4.8 Dimensionality Reduction 257
Fig. 4.35 The top panel
shows the columns of the
feature matrix and the
bottom panel shows the
dominant component that
PCA has extracted
However, changing the slope did not impact the explained variance ratio. Again,
there is still only one dominant column. This means that PCA is invariant to both
constant offsets and scale changes. This works for functions as well as simple lines,
```
>>> x = np.linspace(-1,1,30)>>> X = np.c_[np.sin(2*np.pi*x),
```
```
... 2*np.sin(2*np.pi*x)+1,... 3*np.sin(2*np.pi*x)+2]
```
```
>>> pca.fit(X)PCA(copy=True, n_components=None, whiten=False)
```
>>> print pca.explained_variance_ratio_[ 1.00000000e+00 3.78264707e-32 4.64963853e-34]
Once again, there is only one dominant column, which is shown in the bottom panel
of Fig. 4.36. The top panel shows the individual columns of the feature matrix.
To sum up, PCA is able to identify and eliminate features that are merely linear
Fig. 4.36 The top panel
shows the columns of the
feature matrix and the
bottom panel shows the
dominant component that
PCA has computed
258 4 Machine Learning
transformations of existing features. This also works when there is additive noise in
the features, although more samples are needed to separate the uncorrelated noise
from between features.
To see how PCA can simplify machine learning tasks, consider Fig. 4.37 wherein
the two classes are separated along the diagonal. After PCA, the transformed data lie
along a single axis where the two classes can be split using a one-dimensional interval,
which greatly simplifies the classification task. The class identities are preserved
under PCA because the principal component is along the same direction that the
classes are separated. On the other hand, if the classes are separated along the direction
orthogonal to the principal component, then the two classes become mixed under
PCA and the classification task becomes much harder. Note that in both cases, the
explained_variance_ratio_ is the same because the explained variance
ratio does not account for class membership.
PCA works by decomposing the covariance matrix of the data using the Singular
```
Value Decomposition (SVD). This decomposition exists for all matrices and returns
```
```
the following factorization for an arbitrary matrix A (Fig. 4.38),
```
```
A = USVT
```
Because of the symmetry of the covariance matrix, U = V. The elements of the
diagonal matrix S are the singular values of A whose squares are the eigenvalues of
AT A. The eigenvector matrix U is orthogonal: UT U = I. The singular values are
in decreasing order so that the first column of U is the axis corresponding to the
Fig. 4.37 The left panel shows the original two-dimensional data space of two easily distinguishable
classes and the right panel shows the reduced the data space transformed using PCA. Because the two
classes are separated along the principal component discovered by PCA, the classes are preserved
under the transformation
4.8 Dimensionality Reduction 259
Fig. 4.38 As compared with Fig. 4.37, the two classes differ along the coordinate direction that is
orthogonal to the principal component. As a result, the two classes are no longer distinguishable
after transformation
largest singular value. This is the first dominant column that PCA identifies. The
```
entries of the covariance matrix are of the form E(x i x j ) where x i and x j are different
```
features. 5 This means that the covariance matrix is filled with entries that attempt
to uncover mutually correlated relationships between all pairs of columns of the
feature matrix. Once these have been tabulated in the covariance matrix, the SVD
finds optimal orthogonal transformations to align the components along the directions
most strongly associated with these correlated relationships. Simultaneously, because
orthogonal matrices have columns of unit-length, the SVD collects the absolute
squared lengths of these components into the S matrix. In our example above in
Fig. 4.37, the two feature vectors were obviously correlated along the diagonal,
meaning that PCA selected that diagonal direction as the principal component.
We have seen that PCA is a powerful dimension reduction method that is invariant
to linear transformations of the original feature space. However, this method performs
poorly with transformations that are nonlinear. In that case, there are a wide range of
extensions to PCA, such as Kernel PCA, that are available in Scikit-learn, which allow
for embedding parameterized non-linearities into the PCA at the risk of overfitting.
5 Note that these entries are constructed from the data using an estimator of the covariance matrix
because we do not have the full probability densities at hand.
260 4 Machine Learning
4.8.1 Independent Component Analysis
```
Independent Component Analysis (ICA) via the FastICA algorithm is also available
```
in Scikit-learn. This method is fundamentally different from PCA in that it is the
small differences between components that are emphasized, not the large principal
components. This method is adopted from signal processing. Consider a matrix of
```
signals (X) where the rows are the samples and the columns are the different signals.
```
For example, these could be EKG signals from multiple leads on a single patient.
The analysis starts with the following model,
```
X = SAT (4.8.1.1)
```
```
In other words, the observed signal matrix is an unknown mixture (A) of some set
```
of conformable, independent random sources S,
```
S = [s1(t), s2(t), . . . , sn (t)]
```
The distribution on the random sources is otherwise unknown, except there can be
at most one Gaussian source, otherwise, the mixing matrix A cannot be identified
because of technical reasons. The problem in ICA is to find A in Eq. 4.8.1.1 and
```
thereby un-mix the si (t) signals, but this cannot be solved without a strategy to
```
reduce the inherent arbitrariness in this formulation.
To make this concrete, let us simulate the situation with the following code,
```
>>> from numpy import matrix, c_, sin, cos, pi>>> t = np.linspace(0,1,250)
```
```
>>> s1 = sin(2*pi*t*6)>>> s2 =np.maximum(cos(2*pi*t*3),0.3)
```
```
>>> s2 = s2 - s2.mean()>>> s3 = np.random.randn(len(t))*.1
```
```
>>> # normalize columns>>> s1=s1/np.linalg.norm(s1)
```
```
>>> s2=s2/np.linalg.norm(s2)>>> s3=s3/np.linalg.norm(s3)
```
>>> S =c_[s1,s2,s3] # stack as columns
```
>>> # mixing matrix>>> A = matrix([ [ 1, 1,1],
```
```
... [0.5, -1,3],... [0.1, -2,8] ])
```
>>> X= S*A.T # do mixing
```
The individual signals (si (t)) and their mixtures (X i (t)) are shown in Fig. 4.39. To
```
recover the individual signals using ICA, we use the FastICA object and fit the
parameters on the X matrix,
```
>>> from sklearn.decomposition import FastICA>>> ica = FastICA()
```
```
>>> # estimate unknown S matrix>>> S_=ica.fit_transform(X)
```
4.8 Dimensionality Reduction 261
Fig. 4.39 The left column shows the original signals and the right column shows the mixed signals.
The object of ICA is to recover the left column from the right
The results of this estimation are shown in Fig. 4.40, showing that ICA is able to
recover the original signals from the observed mixture. Note that ICA is unable
to distinguish the signs of the recovered signals or preserve the order of the input
signals.
To develop some intuition as to how ICA accomplishes this feat, consider the
following two-dimensional situation with two uniformly distributed independent
variables, u x , u y ∼ U[0, 1]. Suppose we apply the following orthogonal rotation
matrix to these variables,
[u′
x
u′y
]
=
```
[cos(φ) − sin(φ)
```
```
sin(φ) cos(φ)
```
] [u
x
u y
]
The so-rotated variables u′x , u′y are no longer independent, as shown in Fig. 4.41.
Thus, one way to think about ICA is as a search through orthogonal matrices so that
the independence is restored. This is where the prohibition against Gaussian distri-
butions arises. The two dimensional Gaussian distribution of independent variables
is proportional the following,
```
f (x) ∝ exp(− 12 xT x)
```
262 4 Machine Learning
Fig. 4.40 The left column shows the original signals and the right column shows the signals that
ICA was able to recover. They match exactly, outside of a possible sign change
Now, if we similarly rotated the x vector as,
```
y = Qx
```
the resulting density for y is obtained by plugging in the following,
```
x = QT y
```
because the inverse of an orthogonal matrix is its transpose, we obtain
```
f (y) ∝ exp(− 12 yT QQT y) = exp(− 12 yT y)
```
In other words, the transformation is lost on the y variable. This means that ICA
cannot search over orthogonal transformations if it is blind to them, which explains
the restriction of Gaussian random variables. Thus, ICA is a method that seeks to
maximize the non-Gaussian-ness of the transformed random variables. There are
many methods to doing this, some of which involve cumulants and others that use
the negentropy,
4.8 Dimensionality Reduction 263
Fig. 4.41 The left panel shows two classes labeled on the u x , u y uniformly independent random
variables. The right panel shows these random variables after a rotation, which removes their mutual
independence and makes it hard to separate the two classes along the coordinate directions
```
J (Y ) = H(Z ) − H(Y )
```
```
where H(Z ) is the information entropy of the Gaussian random variable Z that has
```
the same variance as Y . Further details would take us beyond our scope, but that is
the outline of how the FastICA algorithm works.
The implementation of this method in Scikit-learn includes two different ways of
extracting more than one independent source component. The deflation method iter-
atively extracts one component at a time using a incremental normalization step. The
parallel method also uses the single-component method but carries out normalization
of all the components simultaneously, instead of for just the newly computed com-
ponent. Because ICA extracts independent components, a whitening step is used
beforehand to balance the correlated components from the data matrix. Whereas
PCA returns uncorrelated components along dimensions optimal for Gaussian ran-
dom variables, ICA returns components that are as far from the Gaussian density as
possible.
The left panel on Fig. 4.41 shows the orignal uniform random sources. The white
and black colors distinguish between two classes. The right panel shows the mixture
of these sources, which is what we observe as input features. The top row of Fig. 4.42
```
shows the PCA (left) and ICA (right) transformed data spaces. Notice that ICA is
```
able to un-mix the two random sources whereas PCA transforms along the dominant
diagonal. Because ICA is able to preserve the class membership, the data space can be
reduced to two non-overlapping sections, as shown. However, PCA cannot achieve
a similiar separation because the classes are mixed along the dominant diagonal that
PCA favors as the main component in the decomposition.
For a good principal component analysis treatment, see [7–9], and [10]. Indepen-
dent Component Analysis is discussed in more detail in [11].
264 4 Machine Learning
Fig. 4.42 The panel on the top left shows two classes in a plane after a rotation. The bottom left
panel shows the result of dimensionality reduction using PCA, which causes mixing between the
two classes. The top right panel shows the ICA transformed output and the lower right panel shows
that, because ICA was able to un-rotate the data, the lower dimensional data maintains the separation
between the classes
4.9 Clustering
Clustering is the simplest member of a family of machine learning methods that do
not require supervision to learn from data. Unsupervised methods have training sets
that do not have a target variable. These unsupervised learning methods rely upon a
meaningful metric to group data into clusters. This makes it an excellent exploratory
data analysis method because there are very few assumptions built into the method
itself. In this section, we focus on the popular K-means clustering method that is
available in Scikit-learn.
Let’s manufacture some data to get going with make_blobs from Scikit-learn.
Figure 4.43 shows some example clusters in two dimensions. Clustering methods
work by minimizing the following objective function,
```
J =
```
∑
k
∑
i
‖xi − μk ‖2
4.9 Clustering 265
Fig. 4.43 The four clusters
are pretty easy to see in this
example and we want
clustering methods to
determine the extent and
number of such clusters
automatically
The distortion for the kth cluster is the summand,
‖x i − μk ‖2
Thus, clustering algorithms work to minimize this by adjusting the centers of the
individual clusters, μk . Intuitively, each μk is the center of mass of the points in the
cloud. The Euclidean distance is the typical metric used for this,
‖x‖2 =
∑
x2i
There are many clever algorithms that can solve this problem for the best μk cluster-
centers. The K-means algorithm starts with a user-specified number of K clusters
to optimize over. This is implemented in Scikit-learn with the KMeans object that
follows the usual fitting conventions in Scikit-learn,
```
>>> from sklearn.cluster import KMeans>>> kmeans = KMeans(n_clusters=4)
```
```
>>> kmeans.fit(X)KMeans(copy_x=True, init=’k-means++’, max_iter=300, n_clusters=4, n_init=10,
```
```
n_jobs=1, precompute_distances=True, random_state=None, tol=0.0001,verbose=0)
```
where we have chosen K = 4. How do we choose the value of K ? This is the
eternal question of generalization versus approximation—too many clusters provide
great approximation but bad generalization. One way to approach this problem is to
compute the mean distortion for increasingly larger values of K until it no longer
makes sense. To do this, we want to take every data point and compare it to the
centers of all the clusters. Then, take the smallest value of this across all clusters
and average those. This gives us an idea of the overall mean performance for the K
clusters. The following code computes this explicitly.
266 4 Machine Learning
Programming Tip
The cdist function from Scipy computes all the pairwise differences between
the two input collections according to the specified metric.
>>> from scipy.spatial.distance import cdist>>> m_distortions=[]
```
>>> for k in range(1,7):... kmeans = KMeans(n_clusters=k)
```
```
... _=kmeans.fit(X)... tmp=cdist(X,kmeans.cluster_centers_,’euclidean’)
```
```
... m_distortions.append(sum(np.min(tmp,axis=1))/X.shape[0])...
```
Note that code above uses the cluster_centers_, which are estimated from
K-means algorithm. The resulting Fig. 4.44 shows the point of diminishing returns
for added additional clusters.
Another figure-of-merit is the silhouette coefficient, which measures how compact
and separated the individual clusters are. To compute the silhouette coefficient, we
```
need to compute the mean intra-cluster distance for each sample (ai ) and the mean
```
```
distance to the next nearest cluster (bi ). Then, the silhouette coefficient for the ith
```
sample is
```
sci = bi − aimax(a
```
```
i , bi )
```
The mean silhouette coefficient is just the mean of all these values over all the
samples. The best value is one and the worst is negative one, with values near zero
indicating overlapping clusters and negative values showing that samples have been
incorrectly assigned to the wrong cluster. This figure-of-merit is implemented in
Scikit-learn as in the following,
>>> from sklearn.metrics import silhouette_score
Fig. 4.44 The mean
distortion shows that there is
a diminishing value in using
more clusters
4.9 Clustering 267
Fig. 4.45 The shows how the silhouette coefficient varies as the clusters move closer and become
more compact
Figure 4.46 shows how the silhouette coefficient varies as the clusters become more
dispersed and/or closer together.
K-means is easy to understand and to implement, but can be sensitive to the
initial choice of cluster-centers. The default initialization method in Scikit-learn
uses a very effective and clever randomization to come up with the initial cluster-
centers. Nonetheless, to see why initialization can cause instability with K-means,
consider the following Fig. 4.46. In Fig. 4.46, there are two large clusters on the
left and a very sparse cluster on the far right. The large circles at the centers are the
cluster-centers that K-means found. Given K = 2, how should the cluster-centers
be chosen? Intuitively, the first two clusters should have their own cluster-center
somewhere between them and the sparse cluster on the right should have its own
```
cluster-center. 6 Why isn’t this happening (Fig. 4.45)?
```
The problem is that the objective function for K-means is trading the distance
of the far-off sparse cluster with its small size. If we keep increasing the number
of samples in the sparse cluster on the right, then K-means will move the clus-
ter centers out to meet them, as shown in Fig. 4.46. That is, if one of the initial
cluster-centers was right in the middle of the sparse cluster, the algorithm would
have immediately captured it and then moved the next cluster-center to the mid-
```
dle of the other two clusters (bottom panel of Fig. 4.46). Without some thoughtful
```
initialization, this may not happen and the sparse cluster would have been merged
6 Note that we are using the init=random keyword argument for this example in order to illustrate
this.
268 4 Machine Learning
Fig. 4.46 The large circles
indicate the cluster-centers
found by the K-means
algorithm
```
into the middle cluster (top panel of Fig. 4.46). Furthermore, such problems are
```
hard to visualize with high-dimensional clusters. Nonetheless, K-means is gener-
ally very fast, easy-to-interpret, and easy to understand. It is straightforward to par-
allelize using the n_jobs keyword argument so that many initial cluster-centers
can be easily evaluated. Many extensions of K-means use different metrics beyond
Euclidean and incorporate adaptive weighting of features. This enables the clusters
to have ellipsoidal instead of spherical shapes.
4.10 Ensemble Methods
With the exception of the random forest, we have so far considered machine learn-
ing models as stand-alone entities. Combinations of models that jointly produce a
classification are known as ensembles. There are two main methodologies that create
```
ensembles: bagging and boosting.
```
4.10.1 Bagging
Bagging refers to bootstrap aggregating, where bootstrap here is the same as we
discussed in Sect. 3.10. Basically, we resample the data with replacement and then
train a classifier on the newly sampled data. Then, we combine the outputs of each of
```
the individual classifiers using a majority-voting scheme (for discrete outputs) or a
```
```
weighted average (for continuous outputs). This combination is particularly effective
```
for models that are easily influenced by a single data element. The resampling process
means that these elements cannot appear in every bootstrapped training set so that
some of the models will not suffer these effects. This makes the so-computed com-
bination of outputs less volatile. Thus, bagging helps reduce the collective variance
of individual high-variance models.
4.10 Ensemble Methods 269
Fig. 4.47 Two regions in the
plane are separated by a
nonlinear boundary. The
training data is sampled from
this plane. The objective is to
correctly classify the
so-sampled data
To get a sense of bagging, let’s suppose we have a two-dimensional plane that
is partitioned into two regions with the following boundary: y = −x + x2 . Pairs
```
of (x i , yi ) points above this boundary are labeled one and points below are labeled
```
zero. Figure 4.47 shows the two regions with the nonlinear separating boundary as
the black curved line.
The problem is to take samples from each of these regions and classify them
correctly using a perceptron. A perceptron is the simplest possible linear classifier that
finds a line in the plane to separate two purported categories. Because the separating
boundary is nonlinear, there is no way that the perceptron can completely solve this
problem. The following code sets up the perceptron available in Scikit-learn.
```
>>> from sklearn.linear_model import Perceptron>>> p=Perceptron()
```
```
>>> pPerceptron(alpha=0.0001,class_weight=None,eta0=1.0,fit_intercept=True,
```
```
n_iter=5,n_jobs=1,penalty=None,random_state=0,shuffle=False,verbose=0,warm_start=False)
```
The training data and the resulting perceptron separating boundary are shown in
Fig. 4.48. The circles and crosses are the sampled training data and the gray
separating line is the perceptron’s separating boundary between the two categories.
The black squares are those elements in the training data that the perceptron mis-
classified. Because the perceptron can only produce linear separating boundaries, and
the boundary in this case is non-linear, the perceptron makes mistakes near where
the boundary curves. The next step is to see how bagging can improve upon this by
using multiple perceptrons.
The following code sets up the bagging classifier in Scikit-learn. Here we select
only three perceptrons. Figure 4.49 shows each of the three individual classifiers and
the final bagged classifer in the panel on the bottom right. As before, the black circles
indicate misclassifications in the training data. Joint classifications are determined
by majority voting.
270 4 Machine Learning
Fig. 4.48 The perceptron
finds the best linear boundary
between the two classes
Fig. 4.49 Each panel with the single gray line is one of the perceptrons used for the ensemble
bagging classifier on the lower right
4.10 Ensemble Methods 271
```
>>> from sklearn.ensemble import BaggingClassifier>>> bp = BaggingClassifier(Perceptron(),max_samples=0.50,n_estimators=3)
```
```
>>> bpBaggingClassifier(base_estimator=Perceptron(alpha=0.0001,class_weight=None,eta0=
```
1.0,fit_intercept=True,n_iter=5,n_jobs=1,penalty=None,random_state=0,shuffle=False,
```
verbose=0,warm_start=False),bootstrap=True,bootstrap_features=False,max_features=1.0,
```
```
max_samples=0.5,n_estimators=3,n_jobs=1,oob_score=False,random_state=None,verbose=0)
```
The BaggingClassifier can estimate its own out-of-sample error if passed
the oob_score=True flag upon construction. This keeps track of which samples
were used for training and which were not, and then estimates the out-of-sample error
using those samples that were unused in training. The max_samples keyword
argument specifies the number of items from the training set to use for the base
classifier. The smaller the max_samples used in the bagging classifier, the better
the out-of-sample error estimate, but at the cost of worse in-sample performance. Of
course, this depends on the overall number of samples and the degrees-of-freedom
in each individual classifier. The VC-dimension surfaces again!
4.10.2 Boosting
As we discussed, bagging is particularly effective for individual high-variance classi-
fiers because the final majority-vote tends to smooth out the individual classifiers and
produce a more stable collaborative solution. On the other hand, boosting is particu-
larly effective for high-bias classifiers that are slow to adjust to new data. On the one
```
hand, boosting is similiar to bagging in that it uses a majority-voting (or averaging for
```
```
numeric prediction) process at the end; and it also combines individual classifiers of
```
the same type. On the other hand, boosting is serially iterative, whereas the individual
classifiers in bagging can be trained in parallel. Boosting uses the misclassifications
of prior iterations to influence the training of the next iterative classifier by weighting
those misclassifications more heavily in subsequent steps. This means that, at every
step, boosting focuses more and more on specific misclassifications up to that point,
letting the prior classifications be carried by earlier iterations.
The primary implementation for boosting in Scikit-learn is the Adaptive Boosting
```
(AdaBoost) algorithm, which does classification (AdaBoostClassifier) and
```
```
regression (AdaBoostRegressor). The first step in the basic AdaBoost algorithm
```
```
is to initialize the weights over each of the training set indicies, D0(i) = 1/n where
```
there are n elements in the training set. Note that this creates a discrete uniform
```
distribution over the indicies, not over the training data {(x i , yi )} itself. In other
```
words, if there are repeated elements in the training data, then each gets its own
272 4 Machine Learning
Fig. 4.50 The individual
perceptron classifiers
embedded in the AdaBoost
classifier are shown along
with the mis-classified points
```
(in black). Compare this to
```
the lower right panel of
Fig. 4.49
weight. The next step is to train the base classifer h k and record the classification
error at the kth iteration, k . Two factors can next be calculated using k ,
αk = 12 log 1 − k
k
and the normalization factor,
Z k = 2
√
```
k (1 − k )
```
For the next step, the weights over the training data are updated as in the following,
```
D k+1(i) = 1Z
```
k
```
D k (i) exp (−αk yi h k (x i ))
```
```
The final classification result is assembled using the αk factors, g = sgn(∑k αk h k ).
```
To re-do the problem above using boosting with perceptrons, we set up the
AdaBoost classifier in the following,
```
>>> from sklearn.ensemble import AdaBoostClassifier>>> clf=AdaBoostClassifier(Perceptron(),n_estimators=3,
```
```
... algorithm=’SAMME’,... learning_rate=0.5)
```
```
>>> clfAdaBoostClassifier(algorithm=’SAMME’, base_estimator=Perceptron(alpha=0.0001,cla
```
```
ss_weight=None,eta0=1.0,fit_intercept=True,n_iter=5,n_jobs=1,penalty=None,random_state=0,shuffle=False,
```
```
verbose=0,warm_start=False), learning_rate=0.5,n_estimators=3,random_state=None)
```
The learning_rate above controls how aggressively the weights are updated.
The resulting classification boundaries for the embedded perceptrons are shown in
Fig. 4.50. Compare this to the lower right panel in Fig. 4.49. The performance for
both cases is about the same. The IPython notebook corresponding to this section
has more details and the full listing of code used to produce all these figures.
References 273
References
1. L. Wasserman, All of Statistics: A Concise Course in Statistical Inference (Springer, 2004)
2. V. Vapnik, The Nature of Statistical Learning Theory (Springer, Information Science and Sta-
```
tistics, 2000)
```
3. J. Fox, Applied Regression Analysis and Generalized Linear Models (Sage Publications, 2015)
4. K.J. Lindsey, Applying Generalized Linear Models (Springer, 1997)
5. S.L. Campbell, C.D. Meyer, Generalized Inverses of Linear Transformations, vol. 56 (SIAM,
```
2009)
```
6. C. Bauckhage, Numpy/scipy Recipes for Data Science: Kernel Least Squares Optimization (1)
```
(researchgate.net, March 2015)
```
7. W. Richert, Building Machine Learning Systems With Python (Packt Publishing Ltd, 2013)
8. E. Alpaydin, Introduction to Machine Learning (Wiley Press, 2014)
9. H. Cuesta, Practical Data Analysis (Packt Publishing Ltd, 2013)
10. A.J. Izenman, Modern Multivariate Statistical Techniques, vol. 1 (Springer, 2008)
11. A. Hyvarinen, J. Karhunen, E. Oja, Independent Component Analysis, vol. 46 (John Wiley &
```
Sons, 2004)
```
Index
A
AdaBoost, 271
Almost sure convergence, 105
B
Bagging, 268
Bias/variance trade-off, 219
Boosting, 271
C
Cauchy-Schwarz inequality, 53, 60
Central limit theorem, 111
Chebyshev Inequality, 97
Cluster distortion, 265
Complexity penalty, 212
Conda package manager, 3
Conditional expectation projection, 54
Confidence intervals, 119, 143
Confidence sets, 144
Confusion matrix, 213
Convergence in distribution, 109
Convergence in probability, 107
Cross-validation, 215
Ctypes, 27
Cython, 28
D
Delta method, 123
Dispersion scale function, 240
E
Explained variance ratio, 256
F
False-discovery rate, 140
FastICA, 260
Feature engineering, 214
G
Generalized likelihood ratio test, 135
Generalized linear models, 239
H
Heteroskedastic, 240
Hoeffding Inequality, 98
I
Idempotent property, 54
Independent Component Analysis, 260
Information entropy, 78, 79, 230
Inner product, 54
Inverse CDF method, 88, 90
Ipcluster, 31
IPython Notebook, 18
K
Kernel trick, 253
Kullback-Leibler divergence, 82
L
Lagrange multipliers, 241
Lasso regression, 248
Lesbesgue integration, 36
M
Markov Inequality, 96
© Springer International Publishing Switzerland 2016
J. Unpingco, Python for Probability, Statistics, and Machine Learning,
DOI 10.1007/978-3-319-30717-6
275
276 Index
Maximal margin algorithm, 251
Maximum A-Posteriori Estimation, 158
Measurable function, 37
Measure, 37
Minimax risk, 113
MMSE, 54
Moment generating functions, 83
Monte Carlo sampling methods, 87
Multilinear regression, 199
Multiprocessing, 29
N
Neyman-Pearson test, 133
O
Out-of-sample data, 204
P
Pandas, 21
dataframe, 23
series, 21
Perceptron, 269
Permutation test, 138
Plug-in principle, 118
Polynomial regression, 200
Projection operator, 53
P-values, 132
Pypy, 29
R
Random forests, 232
Receiver operating characteristic, 130
Regression regression, 244
Rejection method, 92
Runsnakerun, 29
S
SAGE, 25
Scipy, 20
Seaborn, 104
Shatter coefficient, 208
Silhouette coefficient, 266
Strong law of large numbers, 110
SWIG, 27
Sympy, 25
lambdify, 115
statistics module, 103
T
Tower property of expectation, 56
U
Unary functions, 5
Uniqueness theorem, 85
V
Vapnik-Chervonenkis dimension, 208
W
Wald test, 139
Weak law of large numbers, 110