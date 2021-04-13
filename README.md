# NFA_to_DFA
####This assignment deals with the implementation of some utilities for finite automata. It restricts only to DFA and
####NFA, and does not deal with ε-NFA. In short, you are asked to carry out the following tasks.
####• Read the data for an NFA N = (QN,Σ,∆,S,FN) from a file.
####• Use the subset-construction procedure to convert the input NFA to an equivalent DFA D = (Q,Σ,δ,s,F).
####• Use a graph-traversal algorithm to find out all reachable (or accessible) states in D.
####• Remove all unreachable states from D to get a DFA D = (Q',Σ,δ',s',F').
####• Find all groups of equivalent states in D′.
####• Collapse each group of equivalent states in D′to a single state, and generate the resulting minimized DFA 
####D′′ = (Q′′,Σ,δ′′,s′′,F′′).
