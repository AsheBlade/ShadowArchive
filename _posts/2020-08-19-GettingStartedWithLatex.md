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

## Latex Sample Template

Some very useful latex sample template I downloaded from Internet: [here](https://drive.google.com/drive/folders/1yoXO_5o08kadeHUEZfI4Fb7vhDJD_Q_Q?usp=sharing)

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

## 插入代码

**header插入**

其中language=Java, 可以根据具体程序语言更改, 其他字号和颜色都是可以按喜好自有更改. 

```latex
\usepackage{listings}
\usepackage{color}

\definecolor{dkgreen}{rgb}{0,0.6,0}
\definecolor{gray}{rgb}{0.5,0.5,0.5}
\definecolor{mauve}{rgb}{0.58,0,0.82}

\lstset{frame=tb,
  language=Java,
  aboveskip=3mm,
  belowskip=3mm,
  showstringspaces=false,
  columns=flexible,
  basicstyle={\small\ttfamily},
  numbers=none,
  numberstyle=\tiny\color{gray},
  keywordstyle=\color{blue},
  commentstyle=\color{dkgreen},
  stringstyle=\color{mauve},
  breaklines=true,
  breakatwhitespace=true,
  tabsize=3
}
```

**Code block**

```latex
\begin{lstlisting}
// Hello.java
import javax.swing.JApplet;
import java.awt.Graphics;

public class Hello extends JApplet {
    public void paintComponent(Graphics g) {
        g.drawString("Hello, world!", 65, 95);
    }    
}
\end{lstlisting}
```

**效果**

![](https://i.stack.imgur.com/wKKMy.png)

**来源**

[stackoverflow](https://stackoverflow.com/questions/3175105/inserting-code-in-this-latex-document-with-indentation)

## Pseudocode

**Header**

```latex
\usepackage{algorithm}
\usepackage{algorithmic}
```
**example**

```latex
\begin{algorithm}
\caption{Calculate $y = x^n$}
\begin{algorithmic}
\REQUIRE $n \geq 0 \vee x \neq 0$
\ENSURE $y = x^n$
\STATE $y \leftarrow 1$
\IF{$n < 0$}
\STATE $X \leftarrow 1 / x$
\STATE $N \leftarrow -n$
\ELSE
\STATE $X \leftarrow x$
\STATE $N \leftarrow n$
\ENDIF
\WHILE{$N \neq 0$}
\IF{$N$ is even}
\STATE $X \leftarrow X \times X$
\STATE $N \leftarrow N / 2$
\ELSE[$N$ is odd]
\STATE $y \leftarrow y \times X$
\STATE $N \leftarrow N - 1$
\ENDIF
\ENDWHILE
\end{algorithmic}
\end{algorithm}
```

**Reference**

[Math-Linux.com](https://www.math-linux.com/latex-26/faq/latex-faq/article/how-to-write-algorithm-and-pseudocode-in-latex-usepackage-algorithm-usepackage-algorithmic)

