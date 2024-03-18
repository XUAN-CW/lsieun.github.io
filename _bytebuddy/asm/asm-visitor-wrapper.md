---
title: "AsmVisitorWrapper"
sequence: "101"
---

## AsmVisitorWrapper

```text
                     ┌─── NoOp
                     │
AsmVisitorWrapper ───┤
                     │                    ┌─── ForDeclaredFields ────┼─── FieldVisitorWrapper
                     └─── AbstractBase ───┤
                                          └─── ForDeclaredMethods ───┼─── MethodVisitorWrapper
```

