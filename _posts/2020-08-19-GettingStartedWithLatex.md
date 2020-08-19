---
layout: post
title: Getting Started With Latex
date: 2020-08-19
author: Shadow Walker
tags: [Latex]
comments: true
toc: true
---

## Overview

This tutorial helps people to quickly getting started with Latex.  Most of the content from this article is from [here](https://www.latex-tutorial.com/tutorials/first-document/) .

## Hello World

### Very Basic

This will give a very basic Hello World page. 

```latex
\documentclass{article}
\begin{document}
  Hello World!
\end{document}
```

### Add a title page

This add a title page to the previous one. 

```latex
\documentclass{article}

\title{My first document}
\date{2013-09-01}
\author{John Doe}

\begin{document}
  \maketitle
  \newpage

  Hello World!
\end{document}
```

### Add page number

This add page numbers to the previous one. 

```latex
\documentclass{article}

\title{My first document}
\date{2013-09-01}
\author{John Doe}

\begin{document}
  \pagenumbering{gobble}
  \maketitle
  \newpage
  \pagenumbering{arabic}

  Hello World!
\end{document}
```

## Syntax

Latex is like python. Spaces do matter.  
This shows what is valid and what is not. 

```latex
% Valid:

\begin{document}
  \begin{environment1}
    \begin{environment2}
    \end{environment2}
  \end{environment1}
\end{document}

%Invalid:

\begin{document}
  \begin{environment1}
    \begin{environment2}
  \end{environment1}
    \end{environment2}
\end{document}

% Invalid:

\begin{document}
  \begin{environment1}
\end{document}
  \end{environment1}

% Also invalid:

\begin{environment}
  \begin{document}
  \end{document}
\end{environment}
```

