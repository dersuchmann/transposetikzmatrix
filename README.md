# LaTeX Package: `transposetikzmatrix`

This package allows to transpose TikZ matrices using the `xparse` command `\TransposeTikzMatrix #1`.

The package is fully written in `expl3` and `xparse` syntax.

## Package Options

Using this package requires that you define the `ampersand replacement` property of your TikZ matrix. By default, this package assumes you have set `ampersand replacement=\&`. This requires you to use `\&` instead of  `&` to separate entries within a matrix row. 

You can choose to use a different control structure as ampersand replacement. For instance, if you prefer to use `\x`, you can provide the name of the control structure (without `\`) as the `ampersand` package option:

```latex
\usepackage[ampersand=x]{transposetikzmatrix}
```

## Sample Use

This example can also be found in the `sample-use.tex` and `sample-use.pdf` files.

```latex
\documentclass[border=0.5cm]{standalone}

\usepackage{xparse}
\usepackage{expl3}
\usepackage{tikz}
\usetikzlibrary{matrix}

\usepackage{transposetikzmatrix}


\begin{document}
    
    \tikzset{
        sample matrix/.style={
            matrix of nodes, 
            ampersand replacement=\&,
            draw, 
            font=\Large
        }
    }

    \begin{tikzpicture}
        \def\samplematrix{
            a \& d \& g \& j \\
            b \& e \& h \& k \\
            c \& f \& {
                        \tikz[baseline=0.1cm]
                        \node
                            (complex-example-node) 
                            [
                                draw, 
                                minimum width=3cm
                            ] 
                            {$
                                e^
                                {
                                    \tikz[baseline=(char.base)]
                                    \node
                                        (char) 
                                        [
                                            draw, 
                                            shape=circle, 
                                            minimum width=1pt, 
                                            inner sep=1pt
                                        ] 
                                        {i}
                                    ;
                                    \pi
                                }
                                =-1
                            $}; 
                      } \& l \\
        }
        
        \matrix (original) at (0, 0) [sample matrix] {
            \samplematrix
        };
        \matrix (transposed) at (7cm, 0) [sample matrix] {
            \TransposeTikzMatrix\samplematrix
        };
        
        \draw[->, shorten <=0.2cm, shorten >=0.2cm] 
            (original) 
            -- node[above] {\textit{transpose}} (transposed)
        ;
    \end{tikzpicture}
    
\end{document}
```
