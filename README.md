# Sameness charts in LaTeX

A LaTeX package that typesets **sameness charts**
in the style of *The Little Typer* (Friedman & Christiansen).
It provides a left‑ruled, numbered sequence of expressions with
automatic indentation, used for presenting sameness derivations.

## Installation

Download `sameness.sty` and place it either
- in your project folder, or
- somewhere in your `TEXMF` tree (e.g., `~/texmf/tex/latex/sameness/`).

Requires **LuaLaTeX** or **XeLaTeX** (because of `fontspec`).

## Quick start

```latex
\documentclass{article}
\usepackage{libertine}
\usepackage{lmodern}
\newcommand{\schoolbookfont}{\fontencoding{T1}\fontfamily{fnc}\selectfont}

\usepackage[
  unicodesup, % use Unicode superscripts for step numbers
  exprfont={Linux Libertine O}, % font for expressions
  commentfontcmd=schoolbookfont, % font for comments
  stepskip=1ex % vertical step between adjacent steps
]{sameness}

\begin{document}
\newcommand{\num}[1]{{\texttt{##1}\/}}  % uses the environment’s current font
\newcommand{\add}[1]{\constructor{add}\hspace*{-1pt}\texttt{1}}
\newcommand{\zero}{\constructor{zero}}
\newcommand{\iterNat}{\func{iter-Nat}}
\newcommand{\step}[1]{\func{step-##1}}
\newcommand{\constructor}[1]{{\textsf{##1}}}
\newcommand{\func}[1]{{\textbf{##1}} }
\newcommand{\nodef}[1]{{\textbf{\textit{##1}}}}
\newcommand{\type}[1]{{\textsf{##1}}}
\newcommand{\var}[1]{{\textsf{\textit{##1}}}}

\begin{sameness}
    \same (+ \num2 \num4)
    \same (\iterNat \num2 \num4 \step{+}) \comment{expand definition of +}
    \same (\iterNat (\add1 \add1 \zero) \num4 \step{+}) \comment{expand normal form of 2}
    \same[4] (\step{+} \\
        \indentmore (\iterNat (\add1 \zero) \num4 \step{+}))
        \comment{apply 2nd Commandment of iter-Nat}
    \same (\add1 \\
        \indentmore (\iterNat (\add1 \zero) \num4 \step{+}))
        \comment{apply definition of step-+ and arg to $\lambda$-expression}
    \same[6] (\add1 \\
        \indentmore (\step{+} \\
            \indentmore (\iterNat {\zero} \num4 \step{+})))
        \comment{apply 2nd Commandment of iter-Nat}
    \same (\add1 \\
        \indentmore (\add1 \\
            \indentmore (\iterNat \zero \num4 \step{+})))
        \comment{apply definition of step-+ and arg to $\lambda$-expression}
    \same[8] (\add1 \\
        \indentmore (\add1 \\
            \indentmore \num4 ))
        \comment{apply 1st Commandment of iter-Nat}
    \same[9] \num6
        \comment{common human-readable representation of \add1...\add1 (6 times) zero}
    \same[1234] \num6
        \comment{4-digit line numbers (1234) also work}
\end{sameness}
\end{document}
```

## Documentation

A complete list of supported options is provided in the final section of *sameness.sty*.
