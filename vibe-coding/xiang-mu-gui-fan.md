---
description: xulin
icon: standard-definition
---

# 项目规范

来源:[https://github.com/KentBeck/BPlusTree3/blob/main/rust/docs/CLAUDE.md](https://github.com/KentBeck/BPlusTree3/blob/main/rust/docs/CLAUDE.md)

## Development Guidelines <a href="#oaic-1756124649563" id="oaic-1756124649563"></a>

### Philosophy <a href="#disv-1756124649565" id="disv-1756124649565"></a>

#### Core Beliefs <a href="#id-2cc3-1756124649567" id="id-2cc3-1756124649567"></a>

* Incremental progress over big bangs - Small changes that compile and pass tests
* Learning from existing code - Study and plan before implementing
* Pragmatic over dogmatic - Adapt to project reality
* Clear intent over clever code - Be boring and obvious

#### Simplicity Means、 <a href="#zagx-1756124649578" id="zagx-1756124649578"></a>

* Single responsibility per function/class
* Avoid premature abstractions
* No clever tricks - choose the boring solution
* If you need to explain it, it's too complex

### Process <a href="#ptbj-1756124649588" id="ptbj-1756124649588"></a>

#### 1. Planning & Staging <a href="#nwpj-1756124649590" id="nwpj-1756124649590"></a>

Break complex work into 3-5 stages. Document in IMPLEMENTATION\_PLAN.md:## Stage N: \[Name] \*\*Goal\*\*: \[Specific deliverable] \*\*Success Criteria\*\*: \[Testable outcomes] \*\*Tests\*\*: \[Specific test cases] \*\*Status\*\*: \[Not Started|In Progress|Complete]

* Update status as you progress
* Remove file when all stages are done

#### 2. Implementation Flow <a href="#zsgw-1756124649611" id="zsgw-1756124649611"></a>

1. Understand - Study existing patterns in codebase
2. Test - Write test first (red)
3. Implement - Minimal code to pass (green)
4. Refactor - Clean up with tests passing
5. Commit - With clear message linking to plan

#### 3. When Stuck (After 3 Attempts) <a href="#ffsd-1756124649623" id="ffsd-1756124649623"></a>

CRITICAL: Maximum 3 attempts per issue, then STOP.

1. Document what failed:

* What you tried
* Specific error messages
* Why you think it failed

2. Research alternatives:

* Find 2-3 similar implementations
* Note different approaches used

3. Question fundamentals:

* Is this the right abstraction level?
* Can this be split into smaller problems?
* Is there a simpler approach entirely?

4. Try different angle:

* Different library/framework feature?
* Different architectural pattern?
* Remove abstraction instead of adding?

### Technical Standards <a href="#yvff-1756124649658" id="yvff-1756124649658"></a>

#### Architecture Principles <a href="#tdjn-1756124649660" id="tdjn-1756124649660"></a>

* Composition over inheritance - Use dependency injection
* Interfaces over singletons - Enable testing and flexibility
* Explicit over implicit - Clear data flow and dependencies
* Test-driven when possible - Never disable tests, fix them

#### Code Quality <a href="#dr7u-1756124649670" id="dr7u-1756124649670"></a>

* Every commit must:
* Compile successfully
* Pass all existing tests
* Include tests for new functionality
* Follow project formatting/linting
* Before committing:
* Run formatters/linters
* Self-review changes
* Ensure commit message explains "why"

#### Error Handling <a href="#hf86-1756124649690" id="hf86-1756124649690"></a>

* Fail fast with descriptive messages
* Include context for debugging
* Handle errors at appropriate level
* Never silently swallow exceptions

### Decision Framework <a href="#sh2f-1756124649700" id="sh2f-1756124649700"></a>

When multiple valid approaches exist, choose based on:

1. Testability - Can I easily test this?
2. Readability - Will someone understand this in 6 months?
3. Consistency - Does this match project patterns?
4. Simplicity - Is this the simplest solution that works?
5. Reversibility - How hard to change later?

### Project Integration <a href="#jcdz-1756124649714" id="jcdz-1756124649714"></a>

#### Learning the Codebase <a href="#asgo-1756124649716" id="asgo-1756124649716"></a>

* Find 3 similar features/components
* Identify common patterns and conventions
* Use same libraries/utilities when possible
* Follow existing test patterns

#### Tooling <a href="#sxbg-1756124649726" id="sxbg-1756124649726"></a>

* Use project's existing build system
* Use project's test framework
* Use project's formatter/linter settings
* Don't introduce new tools without strong justification

### Quality Gates <a href="#jhrv-1756124649737" id="jhrv-1756124649737"></a>

#### Definition of Done <a href="#n09e-1756124649739" id="n09e-1756124649739"></a>

Tests written and passingCode follows project conventionsNo linter/formatter warningsCommit messages are clearImplementation matches planNo TODOs without issue numbers

#### Test Guidelines <a href="#vmyi-1756124649753" id="vmyi-1756124649753"></a>

* Test behavior, not implementation
* One assertion per test when possible
* Clear test names describing scenario
* Use existing test utilities/helpers
* Tests should be deterministic

### Important Reminders <a href="#xwuh-1756124649765" id="xwuh-1756124649765"></a>

NEVER:

* Use --no-verify to bypass commit hooks
* Disable tests instead of fixing them
* Commit code that doesn't compile
* Make assumptions - verify with existing code

ALWAYS:

* Commit working code incrementally
* Update plan documentation as you go
* Learn from existing implementations
* Stop after 3 failed attempts and reassess
