+++
title = "Parsing Takeaways"
date = 2022-04-03
[taxonomies]
tags = ["Compilers", "Parsing"]
categories = ["Courses"]
+++

## CFG

A CFG is a 4-tuple $(V, \Sigma, S,\rightarrow)$

* $V$ is set of nonterminals
* $\Sigma$ is set of terminals
* $S\in V$ is the start symbol
* $\rightarrow\subset V\times (V\cup \Sigma)^*$ is relation, called the products

**Derivation** is a sequence of replacement from left handside to **RHS** of grammar rules.

**Notation** $\Rightarrow^*$ means any steps of derivation.

<!-- more -->

### Ambiguity Removal

**Nonassociative** requires no more than one operators in a expression, making a expression fully parenthesized.

**Precedence** 

$$
exp\rightarrow exp\,addop\,exp | term\\\\
addop\rightarrow +|-\\\\
term \rightarrow term\,mulop\,term|factor\\\\
mulop\rightarrow *\\\\
factor\rightarrow (exp) | number
$$

**Associativity** left-recursive makes left-associative, right-recuisive makes right-associative.

**Dangling else** this requires if a statement have else, then both the two statement inside the statement to have else statement. And for both of matched and unmatched statement, the statement between if and else must be matched.

**Inessential Ambiguity** the associated semantices do not depend on disambiguating rule used.

In **EBNF**, {} stands for repetition and [] is for optionality.

## LL(1)

This method comprises two actions:

- Generate, for a generative rule $A\rightarrow\alpha$, the nonterminal at the top of the stack can be replaced by $\alpha$.
- Match, remove the token at the top, if it is the same as the next input token.

### First & Follow

* ${\rm First}(X)$ is the terminals that X can start with. And if $X\rightarrow \epsilon$, then $\epsilon\in {\rm First}(X)$.

* ${\rm Follow}(X)$ is only for non-terminals, it can be calculated in these steps:

  1. adding $\$$ to ${\rm Follow}(S)$.
  2. if $A\rightarrow \alpha B \beta$, adding ${\rm First}(\beta) - \epsilon$ to ${\rm Follow}(B)$
  3. if $A\rightarrow \alpha B$ or $A\rightarrow \alpha B\beta, \epsilon \in {\rm First}(\beta)$, then add ${\rm Follow}(A)$ to ${\rm Follow}(B)$.

### Parsing table $M[N, T]$

Here M for moves.

- If $A\rightarrow \alpha$ is a production rule, and there is a derivation $\alpha \Rightarrow^*a\beta$, where $a$ is a token, then add $A\rightarrow \alpha$ to $M[A, a]$.
- If $A\rightarrow \alpha$ is a production rule, and there is a derivation $\alpha \Rightarrow^\ast\epsilon$, and $S\Rightarrow^\ast\beta Aa \gamma$
 where $a$ is a token, then add $A\rightarrow \alpha$ to $M[A, a]$. (Making $A$ disappear directly).

### Left Factoring

$$
A\rightarrow A\alpha_1 | A\alpha_2 | \ldots | A\alpha_n | \beta_1|\beta_2|\ldots|\beta_m
$$

$$
A\rightarrow \beta_1A'|\beta_2A'|\ldots|\beta_mA'\\ A'\rightarrow \alpha_1A' | \alpha_2A' | \ldots | \alpha_nA'|\epsilon
$$

If  there is no **cycle** and no $\epsilon$-production, then the non-terminals should be sorted in some order, and resolved in non-decreasing order. 

## LR(0)

**Item** is yielded by production. For example, $A\rightarrow XYZ$, yields 

$$
A\rightarrow .XYZ \\\\
A\rightarrow X.YZ \\\\
A\rightarrow XY.Z \\\\
A\rightarrow XYZ.
$$

### Closure

**Closure** of item **sets** is constructed using two rules:

- All items I is in Closure(I).
- If $A\rightarrow \alpha .B\beta \in$ Closure(I), and $B\rightarrow \gamma$, then add $B\rightarrow .\gamma$.

this indicates at some stage of parsing process, elements inside a closure can be derived from another one in the closure.

- *Kernel items* ends with a ..
- *Nonkernel items* doesn???t.

The elements added to the set can never be a kernel item.

### Goto

## SLR(1)

## LR(1)

## LALR(1)