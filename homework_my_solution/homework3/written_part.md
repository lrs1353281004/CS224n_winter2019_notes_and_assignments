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



