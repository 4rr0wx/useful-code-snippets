# LaTeX Basics

LaTeX is a typesetting system commonly used for academic and technical documents. It uses markup language to format documents.

## Basic Mathematical Formulas

Mathematical formulas in LaTeX are enclosed in dollar signs:

- Inline equation: $E=mc^2$
- Display equation: 

$$
F = G \frac{{m_1 \cdot m_2}}{{r^2}}
$$

## Basic Commands

### Document Structure

```latex
\documentclass{article}
\begin{document}
    % Your content here
\end{document}
```

### Sections and Subsections

```latex
\section{Introduction}
This is the introduction.

\subsection{Background}
This is the subsection.
```

### Lists

#### Unordered List

```latex
\begin{itemize}
    \item Item 1
    \item Item 2
    \item Item 3
\end{itemize}
```

#### Ordered List

```latex
\begin{enumerate}
    \item First item
    \item Second item
    \item Third item
\end{enumerate}
```

### Figures and Tables

#### Figure

```latex
\begin{figure}[h]
    \centering
    \includegraphics[width=0.5\textwidth]{image.png}
    \caption{Caption for the figure}
    \label{fig:my_label}
\end{figure}
```

#### Table

```latex
\begin{table}[h]
    \centering
    \begin{tabular}{|c|c|}
        \hline
        Item 1 & Item 2 \\
        \hline
        Value 1 & Value 2 \\
        \hline
    \end{tabular}
    \caption{Caption for the table}
    \label{tab:my_table}
\end{table}
```



This is a basic introduction to LaTeX. There are many more advanced features and packages available for various purposes.
