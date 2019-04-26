## 2.（a）

| Stack                       | Buffer                             | New dependency               | Transition            |
| --------------------------- | ---------------------------------- | ---------------------------- | --------------------- |
| [ROOT]                      | [I,parsed,this,sentence,correctly] |                              | Initial Configuration |
| [ROOT,I]                    | [parsed,this,sentence,correctly]   |                              | SHIFT                 |
| [ROOT,I,parsed]             | [this,sentence,correctly]          |                              | SHIFT                 |
| [ROOT,parsed]               | [this,sentence,correctly]          | parsed$\rightarrow$I         | LEFT-ARC              |
| [ROOT,parsed,this]          | [sentence,correctly]               |                              | SHIFT                 |
| [ROOT,parsed,this,sentence] | [correctly]                        |                              | SHIFT                 |
| [ROOT,parsed,sentence]      | [correctly]                        | sentence$ \rightarrow$ this  | LEFT-ARC              |
| [ROOT,parsed]               | [correctly]                        | parsed$\rightarrow$sentence  | RIGHT-ARC             |
| [ROOT,parsed,correctly]     | []                                 |                              | SHIFT                 |
| [ROOT,parsed]               | []                                 | parsed$\rightarrow$correctly | RIGHT-ARC             |
| [ROOT]                      | []                                 | ROOT$\rightarrow$parsed      | RIGHT-ARC             |



## （f）

### i)

Error type: Verb  Phrase  Attachment  Error

Incorrect dependency: wedding$\rightarrow$fearing

Correct dependency: I $\rightarrow$fearing

### ii)

Error type: Coordination Attachment Error

Incorrect dependency: rescue$\rightarrow$and

Correct dependency: rescue $\rightarrow$rush

### iii)

Error type: Prepositional Phrase Attachment Error

Incorrect dependency: named$\rightarrow$Midland

Correct dependency: guy $\rightarrow$Midland

### iv)

Error type: Modifier Attachment Error

Incorrect dependency: elements$\rightarrow$most

Correct dependency: crucial $\rightarrow$most







