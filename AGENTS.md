This project is a combination of tutorial guide, software specs, and implementations.

The overall goal is to create a website that serves as a guide for writing an asteroids game that enables various machine learning experiments.

# Project Structure

```
asteroids-ml/
│
├── book/                   # Human mental model'
│   ├── index.md            # Site home
│   └── ...
│
├── projects/                               # Projects used by the asteroids ml tutorial book
│   ├── asteroids-ml-harness/                   # The asteroids CLI app for playing and training
│   │   ├── book/                                   # Human oriented book explaining the cli app, implementation NOT tutorial focused
│   │   ├── roadmap/                                # PRDs and issues to guide a concrete implementation
│   │   ├── tests/                                  # Generic harness to evaluate any implementation
│   │   └── reference-implementation/               # Reference implementation
│   └── ...
│
├── spec/                 # Normative system contract
│
├── roadmap/              # Intended evolution
│
├── conformance/          # Black-box tests
│
├── plans/                # Historical implementation increments
│   ├── 001-core-simulation/
│   ├── 002-serialization/
│   └── 003-rendering/
│
└── implementations/
    ├── rust/
    └── ...
```

All of the sub-projects in the `projects/` folder should be built using book-first development. There is a skill in this repo provided to help you understand it.