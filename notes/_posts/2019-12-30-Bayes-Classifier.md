---
image:
  teaser: 1920px-Python_logo_and_wordmark.svg.png

layout: article
title: Bayes Classifier
date: 2019-12-30
categories: notes
author: chunyi_hsiao
tags: [Statistics, Probability Models]
share: true

---

<!-- <script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=default"></script> -->


In order to derive the concept of Bayes classifier step by step and learn it. Here keeps a note.

Based on the Prof. Chou, who describes the principle of Bayes decesion theory for multiple-classification concerning of probability and loss.\\
依照周志華教授的思路，他從機率與損失來解釋貝葉斯決策理論在多分類任務上之原理。

Given a dataset $$X=\{x_1, x_2, ..., x_M\}$$ where exists M samples and labelset $$Y=\{c_1, c_2, ..., c_N\}$$ where exists N classes. We can have a conditional risk formula:\\
首先，假設我們有一資料集\\(D\\)存有\\(M\\)筆樣本與標籤集\\(Y\\)具有\\(N\\)類標籤，基於前段所提到的機率與損失，可構成期望損失（亦為條件風險）：


\begin{equation}
R(c_i|x) = \sum_{j=1}^{N}{\lambda_{ij}P(c_j|x)}
\label{eq:first}
\tag{1}
\end{equation}


Here we know:\\
\\(R(c_i\|x)\\) is the expected loss from miscatogorizing sample \\(x\\) to class \\(c_i\\). \\
\\(\lambda_{ij}\\) is the loss from miscatogorizing a sampole \\(c_i\\) to \\(c_j\\). \\
\\(P(c_j|x)\\) is the postrior probability.

Above formula is to calculate the risk from the loss from miscatogorizing one sampole \\(c_i\\) to \\(c_j\\). We want to obtain the over risk by assuming \\(h:X\mapsto Y\\) (\\(h\\) means a rule which input space \\(X\\) reflects to output space \\(Y\\)).

Hence we can get:


\begin{equation}
R(h) = \mathop{\mathbb{E}}[R(h(x)|x)]
\label{eq:second}
\tag{2}
\end{equation}


In order to reduce the over risk \\(R(h)\\), we can make it by minimizing the \\(R(h(x)\|x)\\):

$$ h^{\ast}(x) = \mathop{\arg\min}_{c \in Y}[R(h(x)|x)] \longrightarrow \mathop{\arg\min}_{c \in Y}[R(c|x)] $$

\\(h^{\ast}\\) helps us to find the minimun overall risk \\(R(c\|x)\\),in other words giving the best performance.

If we reckon conditional risk with loss \\(c_i\\) and \\(c_j\\) with:

$$\lambda_{ij}=
\begin{cases}
0& \text{if } i=j;\\
1& \text{otherwise,}
\end{cases}$$

Then we derive the conditional risk \\(R(c_i\|x)\\) when \\(i\neq j\\):

\begin{equation}
R(c_i\|x) = \sum_{j\neq i}^{N} \lambda_{ij}P(c_j\|x) \\
= \sum_{j\neq i}^{N} P(c_j\|x) \\ 
= 1 - P(c_i\|x)
\label{eq:third}
\tag{3}
\end{equation}
	
Therefore, we can simplify and get the over risk:

\begin{equation}
R(c\|x) = 1 - P(c\|x)
\label{eq:forth}
\tag{4}
\end{equation}

Thus, to minimize \\(R(c\|x)\\) is equivelent to maximize posterior probability \\(P(c\|x)\\).

Bayes theroem says:

\begin{equation}
P(c\|x) = \frac{P(c)P(x\|c)}{P(x)}
\label{eq:fifth}
\tag{5}
\end{equation}


Here we know:\\
\\(P(c)\\) is prior probability. \\
\\(P(x\|c)\\) is class-conditional probability or likelihood. \\
\\(P(x)\\) is evidence.

Due to prior probability \\(P(c)\\) is how frequent the class occurred and Likelihood \\(P(x\|c)\\) involves with joint probability of all samples \\(x\\). We usually use MLE(Maximum Likelihood Extimation) to estimate 

 thus, the goal of bayes classifier is to maximize likelihood \\(P(x\|c)\\).

***Reference***\\
机器学习-周志华\\
[Chapter 4 Bayesian Decision Theory](https://www.byclb.com/TR/Tutorials/neural_networks/ch4_1.htm)\\
[How to Develop a Naive Bayes Classifier from Scratch in Python](https://machinelearningmastery.com/classification-as-conditional-probability-and-the-naive-bayes-algorithm/)

 
<!-- $$x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$ -->


<!-- \\(x=\frac{-b\pm\sqrt{b^2-4ac}}{2a}\\) -->

---
