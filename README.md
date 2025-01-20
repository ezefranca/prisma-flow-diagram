
# prisma-flow-diagram Package

This package simplifies the creation of PRISMA flow diagrams using TikZ in LaTeX.

## Installation
1. Copy `prisma-flow-diagram.sty` into the same folder as your `.tex` document.
2. Include the package in your document with:
   ```latex
   \usepackage{prisma-flow-diagram}
   ```

## Usage
Use the provided commands to create PRISMA diagrams:
- `\prismaflowstart`: Begin the diagram.
- `\prismaflownode{<id>}{<position>}{<text>}`: Add a node.
- `\prismaflowarrow{<source>}{<destination>}`: Draw an arrow.
- `\prismaflowend`: End the diagram.

### Example
```latex
\documentclass{article}
\usepackage{prisma-flow-diagram}

\begin{document}

\begin{figure}[H]
\resizebox{0.9\textwidth}{!}{
\prismaflowstart
\prismaflownode{n1a}{left=of start}{Records identified through database searching (n = 251)}
\prismaflownode{n1b}{right=of start}{Additional records identified through other sources (n = 0)}
\prismaflownode{n2}{below=of n1a}{Records after duplicates removed (n = 41)}
\prismaflowarrow{n1a}{n2}
\prismaflowarrow{n1b}{n2}
\prismaflowend
}
\caption{PRISMA Flow Diagram}
\label{fig:prisma}
\end{figure}

\end{document}
```

## License
This package is licensed under the [LPPL 1.3c](https://www.latex-project.org/lppl/).

## Contribution
Contributions are welcome. Feel free to open issues or submit pull requests.