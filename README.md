# Compiler-Design-Project-LL-1-Parsing
The aim of this project is to implement an LL(1) parser using pushdown automata (PDA) and
predictive parsing tables.  
Given an input context-free grammar G = (V, Σ, R, S):
* The code constructs the predictive parsing table for G 
* The code constructs the PDA equivalent to G
* The code implements an LL(1) parser for G which makes use of the table and the PDA to direct its
decisions. Given an input string w, the parser should signal an error if w /∈ L(G) and produce
a derivation of w from S if w ∈ L(G).
• The project is implemented using Java
• Assumptions:  
a) The set V of variables consists of upper-case English symbols.  
b) The start variable is the symbol S.  
c) The set Σ of terminals consists of lower-case English symbols other than “e”.  
d) The letter “e” represents ε.  
• CFG takes an input string encoding a CFG and returns a CFG object. A string encoding
a CFG is a semi-colon-separated sequence of items. Each item represents a largest set
of rules with the same left-hand side and is a comma-separated sequence of strings. The
first string of each item is a member of V , representing the common left-hand side. The
first string of the first item is S.
• For example, consider the CFG ({S, T}, {a, c, i}, R, S), where R is given by the following
productions.  
S −→ i S T| ε    
T −→ c S | a    
This CFG will have the following string encoding.    
**S, iST, e; T, cS, a**
* The function **Table** constructs an object representing the predictive parsing table for a CFG, and
returns a string encoding of the parsing table.  
* A string encoding of a parsing table is a semi-colon-separated sequence of items. Each
item represents a table entry; empty entries are not included. An entry is represented
by a coma-separated sequence of items. The first item is a variable and the second is a
terminal or $. These two items respectively identify a row and a column of the table.
The third and next items represent the rules included in the table entry; each rule
is represented by its right-hand side which is a string of variables and terminals. For
convenience, entries of the same row should appear consecutively. For example, for the
above CFG, the string representation of the corresponding predictive parsing table may
be as follows.  
**S, a, e; S, c, e; S, i, iST; S, $, e; T, a, a; T, c, cS**  
* The function **Parse** takes a string w as input and returns a string encoding a left-most derivation of w
in G; in case w /∈ L(G), this derivation ends with “ERROR.” The method should construct
a PDA equivalent to G and use the PDA together with the table (constructed by Table)
to reach its decision. Note that we will be testing Parse using only LL(1) grammars.
Hence, you do not need to include a search algorithm in your implementation; w either
has no derivation in G or has exactly one.
* A string encoding a derivation is a comma-separated sequence of items. Each item is a
sentential form representing a step in the derivation. The first item is S. If w ∈ L(G)
the last item is w; otherwise, it is ERROR. For example, given the above CFG, on input
string **iiac**, Parse should print the following string.  
**S, iST, iiSTT, iiTT, iiaT, iiacS, iiac**  
On the other hand, on input string **iia**, Parse should print the following.  
**S, iST, iiSTT, iiTT, iiaT, ERROR**
