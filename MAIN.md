# Roadmap

The analysis phase can be divided into two stages -
- commiting ast to the db
- running analysis on the db

## Commiting ast

The full ast should be dumped in the db under a `:codeq/ast`
node. See [AST.md][1] for proposed schema modifications.

## Analysis

Preliminary analysis may include detection of standard
macro invocations like defn, let and defmacro. Since we
are primarily harvesting ast, we have to resort to
matching an ast pattern for making sense of a macro.

I propose an umbrella node (say `:codeq/infer`) to contain
all of analysis results. This can be furthur divided into
nodes like `:infer/core`, `:infer/type` etc to contain info
mined by various plugins, with core for things like macro
analysis and more.

This stage heavily depends on our final expectations of the
suite. Hence I have been approaching the problem from both
ends, looking into publications on static analysis and
versioned program analysis.

## Furthur reading

- [Olin Shivers - Control-Flow Analysis of Higher-Order
  Languages][3]
- [Static analysis for Ruby in the presence of gradual typing][4]
- [Identifying the Semantic and Textual Differences Between
  Two Versions of a Program][5]
- [Program element matching for multi-version program
  analyses][6]
- [Understanding Source Code Evolution Using Abstract Syntax
  Tree Matching][7]
- [Analyzing and Inferring the Structure of Code Changes][8]

[1]: https://github.com/Navgeet/gsocq/blob/master/AST.md
[2]: https://github.com/Navgeet/gsocq/blob/master/ANALYSIS.md
[3]: http://citeseer.ist.psu.edu/viewdoc/summary?doi=10.1.1.202.3797
[4]: http://www.cs.dartmouth.edu/reports/abstracts/TR2011-686/
[5]: http://dl.acm.org/citation.cfm?id=93574
[6]: http://dl.acm.org/citation.cfm?id=1137999
[7]: http://dl.acm.org/citation.cfm?id=1083143
[8]: http://dl.acm.org/citation.cfm?id=1627249
