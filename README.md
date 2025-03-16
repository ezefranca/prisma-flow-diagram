
# prisma-flow-diagram Package [![DOI](https://zenodo.org/badge/919428141.svg)](https://doi.org/10.5281/zenodo.14996713)

## PRISMA Flow Diagram (Overleaf Template)

Easily import this template into Overleaf:

[![Open in Overleaf](https://img.shields.io/badge/Open%20in-Overleaf-brightgreen?style=for-the-badge&logo=overleaf)](https://www.overleaf.com/docs?snip_uri=https://github.com/ezefranca/prisma-flow-diagram/archive/refs/heads/main.zip)


This package provides an abstraction for creating PRISMA 2020 flow diagrams in LaTeX. It simplifies the process of building these diagrams by providing intuitive commands while maintaining full compatibility with TikZ.

![Example](/example.png)

## Installation
1. Copy `prisma-flow-diagram.sty` into the same folder as your `.tex` document.
2. Include the package in your LaTeX document preamble:
   ```latex
   \usepackage{prisma-flow-diagram}
   ```

## Usage
The package provides the following commands:

### Commands
1. **`\prismaflowstart`**  
   Starts the PRISMA flow diagram. Must be called before defining any nodes or labels.

2. **`\prismaflownode{<id>}{<position>}{<text>}{<arrow source>}`**  
   Adds a node to the diagram.  
   - `<id>`: A unique identifier for the node.  
   - `<position>`: Specifies the node's position relative to another node. For example, `below=of tc`.  
   - `<text>`: The text content of the node.  
   - `<arrow source>`: The ID of the source node for an arrow. Leave blank (`{}`) for no arrow.

3. **`\prismalabel{<size>}{<position>}{<text>}`**  
   Adds a vertical label to the left of the diagram.  
   - `<size>`: Size of the label box, typically `1.3*\mh`.  
   - `<position>`: Position relative to a node. For example, `n1a.west`.  
   - `<text>`: Text content of the label.

4. **`\prismaflowarrow{<source>}{<destination>}`**  
   Manually connects two nodes with an arrow.  
   - `<source>`: The ID of the source node.  
   - `<destination>`: The ID of the destination node.

5. **`\prismaflowend`**  
   Ends the PRISMA flow diagram.

### Example
Below is a full example of how to use the package:

```latex
\documentclass{article}
\usepackage{prisma-flow-diagram}

\begin{document}

\begin{figure}[H]
\resizebox{\textwidth}{!}{
\prismaflowstart

% Nodes at the top
\prismaflownode{n1a}{left=of tc}{Records identified through database searching (n = 251)}{};
\prismaflownode{n1b}{right=of tc}{Additional records identified through other sources (n = 0)}{};
\prismaflownode{n2}{below=of tc |- n1a.south}{Records after duplicates removed (n = 41)}{n1a};
\prismaflowarrow{n1b}{n2};

% Screening Phase
\prismaflownode{n3}{below=of n2}{Records screened (n = 210)}{n2};
\prismaflownode{n3r}{right=of n3}{Records excluded (n = 175)}{};
\prismaflowarrow{n3}{n3r};

% Eligibility Phase
\prismaflownode{n4}{below=of n3}{Full-text articles assessed for eligibility (n = 35)}{n3};
\prismaflownode{n4r}{right=of n4}{Full-text articles excluded, with reasons (n = 4) \\ - Not Relevant (n = 3) \\ - Not Open/Available paper (n = 2)}{};
\prismaflowarrow{n4}{n4r};

% Inclusion Phase
\prismaflownode{n5}{below=of n4}{Studies included in qualitative synthesis (n = 30)}{n4};
\prismaflownode{n6}{below=of n5}{Studies included in quantitative synthesis (meta-analysis)}{n5};

% Labels
\prismalabel{1.3*\mh}{n1a.west}{Identification};
\prismalabel{1.3*\mh}{n1a.west |- {$(n2)!0.6!(n3)$}}{Screening};
\prismalabel{1.3*\mh}{n1a.west |- {$(n4)!0.2!(n5)$}}{Eligibility};
\prismalabel{1.3*\mh}{n1a.west |- n6}{Included};

\prismaflowend
}
\caption{PRISMA 2020 Flow Diagram}
\label{fig:prisma}
\end{figure}

\end{document}
```

## License
This package is licensed under the [LPPL 1.3c](https://www.latex-project.org/lppl/).

## Contribution
Contributions are welcome! Feel free to open issues or submit pull requests to improve the package.
