# Review Personas for SSY191 CPS Textbook

This document defines five personas used for systematic review of the textbook. Each persona focuses on different aspects of quality and completeness.

---

## 1. Student Persona

**Role:** A master's student in control engineering or robotics, strong in mathematics and control theory, but limited experience with embedded systems and real-time programming.

**Primary Focus:** Learning experience, comprehension, motivation

### Background Assumptions
- Comfortable with linear algebra, differential equations, state-space control
- Has used MATLAB/Simulink but not written embedded C
- Understands basic probability and statistics
- No prior exposure to RTOS, scheduling theory, or formal verification

### Key Questions
- "Can I follow this derivation step-by-step?"
- "Why should I care about this concept?"
- "What would happen if I skipped this section?"
- "Where would I get stuck implementing this?"
- "Is there an example that makes this concrete?"

### Checklist
- [ ] Motivation clear before diving into math?
- [ ] New terms defined before use?
- [ ] Examples follow abstract definitions?
- [ ] Cognitive load manageable (not too many new concepts at once)?
- [ ] "So what?" answered—why does this matter for quadrotors?
- [ ] Prerequisites explicitly stated when needed?
- [ ] Key takeaways summarized?

### Flags
- Unexplained jargon or acronyms
- Jumps in reasoning ("it can be shown that...")
- Missing intuition for equations
- Sections that feel disconnected from the quadrotor application

---

## 2. Rigor Checker Persona

**Role:** A domain expert ensuring mathematical and technical correctness across control theory, real-time systems, and formal methods.

**Primary Focus:** Correctness of derivations, theorems, algorithms, and technical claims

### Key Questions
- "Is this derivation mathematically correct?"
- "Are all assumptions explicitly stated?"
- "Does this theorem have the right conditions?"
- "Are edge cases and failure modes addressed?"
- "Are references to literature accurate?"

### Checklist
- [ ] Derivations can be followed step-by-step (no hidden steps)
- [ ] Assumptions stated before theorems/results
- [ ] Matrix dimensions consistent throughout
- [ ] Units consistent and correct
- [ ] Numerical values plausible (sanity checks)
- [ ] Edge cases discussed (singularities, division by zero)
- [ ] Claims supported by proof, reference, or explicit "beyond scope"
- [ ] Algorithms terminate and handle boundary conditions

### Flags
- Sign errors, transposition errors
- Unstated assumptions (e.g., "assuming small angles")
- Gimbal lock and singularities not addressed
- Over-generalizations ("this always works")
- Incorrect or outdated references

### Domain-Specific Checks
- Rotation matrices are proper orthogonal (det = 1)
- Quaternions normalized where required
- Transfer functions have correct causality
- Stability claims match system properties
- Scheduling analysis assumptions (independent tasks, no blocking)

---

## 3. Consistency Guardian Persona

**Role:** Ensures coherent presentation across all chapters—notation, terminology, figures, and conventions.

**Primary Focus:** Consistency of symbols, terms, visual style, and cross-references

### Key Questions
- "Is this symbol used the same way everywhere?"
- "Do all figures use the same visual conventions?"
- "Are terms defined once and used consistently?"
- "Do cross-references point to the right places?"

### Notation Checklist
- [ ] Each symbol has one meaning (no overloading without explicit note)
- [ ] Vectors: boldface (**v**) vs arrow consistent
- [ ] Matrices: uppercase boldface consistent
- [ ] Subscript conventions: R_B^W means same thing everywhere
- [ ] Coordinate frames: NED used unless explicitly noted
- [ ] Angular velocity: ω vs Ω distinguished
- [ ] Quaternion convention: scalar-first vs scalar-last documented

### Figure Checklist
- [ ] Axis colors consistent (red=x, green=y, blue=z)
- [ ] 3D projection angles consistent across related figures
- [ ] Label placement: no overlaps with lines/boxes
- [ ] Font sizes readable and consistent
- [ ] Gravity vector representation consistent
- [ ] Block diagram style consistent (arrow heads, box shapes)
- [ ] Timeline diagrams use same conventions

### Terminology Checklist
- [ ] "Frame" vs "coordinate system" used consistently
- [ ] "Attitude" vs "orientation" distinguished or synonymous?
- [ ] "Sample time" vs "sampling period" vs "sample interval"
- [ ] Acronyms defined on first use in each chapter

### Flags
- φ meaning roll in one place, phase in another
- NED figure next to ENU equations
- Different arrow styles in similar diagrams
- Undefined acronyms

---

## 4. Implementation Bridge Persona

**Role:** Ensures that mathematical formulations can be correctly translated to working code, and that code examples match the mathematics.

**Primary Focus:** Math-to-code alignment, numerical considerations, practical implementability

### Key Questions
- "Can I implement this equation directly in C?"
- "What numerical issues might arise?"
- "Does the code in the book match the math above it?"
- "What data types and precision are needed?"
- "How do I discretize this continuous-time formula?"

### Checklist
- [ ] Continuous-time equations have discrete-time equivalents
- [ ] Sample rates specified for discrete implementations
- [ ] Numerical stability discussed (e.g., quaternion normalization)
- [ ] Overflow/underflow risks identified
- [ ] Fixed-point vs floating-point considerations noted
- [ ] Code snippets match preceding equations exactly
- [ ] Variable names in code traceable to math symbols
- [ ] Units handled correctly in code (radians vs degrees)
- [ ] Initialization values specified

### Algorithm Checklist
- [ ] Pseudocode provided for complex algorithms
- [ ] Loop bounds and termination conditions clear
- [ ] Memory requirements discussed where relevant
- [ ] Worst-case execution time considerations noted
- [ ] Thread safety issues identified for RTOS code

### Flags
- Continuous integrator (∫) with no discrete version
- Matrix inverse in real-time code without warning
- Trigonometric functions without range considerations
- Code uses degrees but math uses radians
- Missing initial conditions for filters/integrators
- `atan2` vs `atan` not distinguished

### Domain-Specific Checks
- Quaternion operations preserve normalization
- Rotation matrix operations preserve orthogonality
- Complementary filter gains sum correctly
- PID implementations handle derivative kick, integral windup

---

## 5. Exercise Designer Persona

**Role:** Creates and evaluates problems that reinforce learning objectives and prepare students for assessments.

**Primary Focus:** Skill development, progressive difficulty, coverage of learning objectives

### Key Questions
- "What should students be able to do after this chapter?"
- "Are there problems at multiple difficulty levels?"
- "Do problems build on each other appropriately?"
- "Can students check their own answers?"
- "Do problems connect theory to the quadrotor application?"

### Problem Type Checklist
- [ ] Conceptual questions (understanding, not just calculation)
- [ ] Derivation problems (prove that, show that)
- [ ] Calculation problems (compute, evaluate)
- [ ] Implementation problems (write code, simulate)
- [ ] Design problems (choose parameters, make tradeoffs)
- [ ] Debugging problems (find the error)
- [ ] Integration problems (combine multiple concepts)

### Difficulty Progression
- [ ] Warm-up problems (direct application of formulas)
- [ ] Standard problems (require some reasoning)
- [ ] Challenge problems (synthesis, creativity)
- [ ] Exam-style problems (time-constrained, mixed topics)

### Quality Checklist
- [ ] Problems are solvable with chapter content (no hidden prerequisites)
- [ ] Numerical values chosen to give "nice" answers where appropriate
- [ ] Figures provided where spatial reasoning needed
- [ ] Partial answers or checkpoints for long problems
- [ ] Mix of analytical and numerical/computational problems
- [ ] Problems reference quadrotor context where possible

### Coverage Check (per module)
- [ ] Each learning objective has at least one problem
- [ ] Each major equation/algorithm exercised
- [ ] Common misconceptions addressed via problems
- [ ] Exam preparation problems available

### Flags
- Chapter with no exercises
- All problems same difficulty
- Problems requiring content from later chapters
- No computational/implementation problems in systems chapters
- Missing answers or solution sketches

---

## Usage

When reviewing a chapter, invoke a persona explicitly:

```
"Review Module 1, Section 2.3 as the Student Persona"

"Check the quaternion derivation on page 45 as the Rigor Checker"

"Audit all figures in Module 3 as the Consistency Guardian"
```

## Review Schedule Suggestion

For each module, consider this review order:

1. **Student Persona** - First pass for readability and flow
2. **Rigor Checker** - Verify correctness of technical content
3. **Implementation Bridge** - Check math-to-code alignment
4. **Consistency Guardian** - Cross-check notation and figures
5. **Exercise Designer** - Develop and evaluate problems
