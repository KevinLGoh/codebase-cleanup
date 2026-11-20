# Code smells

Tags for findings in step 3, and fixes to consider in step 5.

Use Refactoring.Guru names and link to `https://refactoring.guru/smells/<slug>` (for example `middle-man`). A finding can have several smells or none. Skip class-based smells (Refused Bequest, Parallel Inheritance Hierarchies) in functional or React code. The Comments smell covers only comments that make up for unclear code, and commented-out code.

| Group | Smells | Usual categories |
|---|---|---|
| Dispensables | Dead Code, Duplicate Code, Lazy Class, Speculative Generality, Data Class, Comments | 1, 2, 4, 7 |
| Bloaters | Long Method, Large Class, Long Parameter List, Primitive Obsession, Data Clumps | 4 |
| Couplers | Middle Man, Message Chains, Feature Envy, Inappropriate Intimacy, Incomplete Library Class | 4, 8 |
| OO Abusers | Switch Statements, Temporary Field, Refused Bequest, Alternative Classes with Different Interfaces | 2, 4 |
| Change Preventers | Shotgun Surgery, Divergent Change, Parallel Inheritance Hierarchies | 8 |

Dispensables are not automatically quick wins: removing a Lazy Class or Data Class can touch many callers.

| Smell | Try first | Catalogue refactoring, if justified |
|---|---|---|
| Middle Man | Call the underlying code directly | Remove Middle Man |
| Lazy Class | Inline it into its only user | Inline Class, Collapse Hierarchy |
| Speculative Generality | Delete unused parameters, hooks and layers | Remove Parameter, Collapse Hierarchy |
| Long Method | Remove dead branches, use early returns | Extract Function |
| Long Parameter List, Data Clumps | Drop unused parameters | Introduce Parameter Object |
| Switch Statements | Keep a small, single switch | Replace Conditional with Polymorphism, only if the switch repeats and keeps growing |
| Message Chains | Accept if shallow and stable | Hide Delegate |
| Feature Envy | Move the logic next to its data | Move Function |
