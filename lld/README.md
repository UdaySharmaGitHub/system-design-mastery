# Low-Level Design

This folder contains all Low-Level Design (LLD) content — class diagrams, OOP design principles, design patterns, and working code implementations.

## Sub-folders

| Folder | What goes here |
|---|---|
| `fundamentals/` | OOP principles, SOLID, class-diagram conventions — language-agnostic explanations |
| `patterns/` | GoF and other design patterns, each with implementations in multiple languages |
| `case-studies/` | LLD deep-dives for classic systems, with code organised by language |

## Multi-Language Structure

Every topic that includes code follows this layout:

```
lld/patterns/<pattern-name>/
├── README.md          ← explanation, class diagram, trade-offs, interview angle
├── java/
│   └── <ClassName>.java
├── python/
│   └── <module_name>.py
├── go/
│   └── <package_name>.go
├── typescript/
│   └── <moduleName>.ts
└── cpp/               ← add only if contributed
    └── <FileName>.cpp
```

You do not need to implement all languages. Start with the one you know best — other contributors can add more languages to the same pattern folder.
