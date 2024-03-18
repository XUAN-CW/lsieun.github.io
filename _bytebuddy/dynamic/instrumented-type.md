---
title: "InstrumentedType"
sequence: "104"
---

```text
                    ┌─── hierarchy ───┼─── withInterfaces(TypeList.Generic interfaceTypes)
                    │
                    │                 ┌─── modifier ──────┼─── withModifiers(int modifiers)
                    │                 │
                    ├─── class ───────┤                   ┌─── withInitializer(LoadedTypeInitializer loadedTypeInitializer)
                    │                 │                   │
                    │                 │                   ├─── withInitializer(ByteCodeAppender byteCodeAppender)
                    │                 └─── initializer ───┤
                    │                                     ├─── getLoadedTypeInitializer()
                    │                                     │
                    │                                     └─── getTypeInitializer()
                    │
                    │                 ┌─── withField(FieldDescription.Token token)
                    ├─── field ───────┤
                    │                 └─── withAuxiliaryField(FieldDescription.Token token, Object value)
                    │
                    ├─── method ──────┼─── withMethod(MethodDescription.Token token)
                    │
                    │                 ┌─── annotation ───┼─── withAnnotations(List<? extends AnnotationDescription> annotationDescriptions)
                    │                 │
                    │                 ├─── generic ──────┼─── withTypeVariable(TypeVariableToken typeVariable)
                    │                 │
InstrumentedType ───┤                 │                  ┌─── withNestHost(TypeDescription nestHost)
                    │                 ├─── nested ───────┤
                    │                 │                  └─── withNestMembers(TypeList nestMembers)
                    │                 │
                    │                 │                  ┌─── withEnclosingType(TypeDescription enclosingType)
                    │                 │                  │
                    │                 │                  ├─── withEnclosingMethod(MethodDescription.InDefinedShape enclosingMethod)
                    ├─── feature ─────┼─── enclose ──────┤
                    │                 │                  ├─── withDeclaringType(@MaybeNull TypeDescription declaringType)
                    │                 │                  │
                    │                 │                  └─── withDeclaredTypes(TypeList declaredTypes)
                    │                 │
                    │                 ├─── anonymous ────┼─── withAnonymousClass(boolean anonymousClass)
                    │                 │
                    │                 ├─── local ────────┼─── withLocalClass(boolean localClass)
                    │                 │
                    │                 ├─── sealed ───────┼─── withPermittedSubclasses(@MaybeNull TypeList permittedSubclasses)
                    │                 │
                    │                 │                  ┌─── withRecordComponent(RecordComponentDescription.Token token)
                    │                 └─── record ───────┤
                    │                                    └─── withRecord(boolean record)
                    │
                    └─── validate ────┼─── validated()
```

