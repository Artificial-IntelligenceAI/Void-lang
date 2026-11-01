# Void — Design decisions (formerly Graft)

Running log. Each entry gives the date, the decision, who proposed it and who chose it, quoting the owner where they
spoke. Nothing is final until the owner says so. Open questions are at the bottom.

## Decided

### 2026-11-01 — The language is called Graft (owner)

The owner: "Let's make/design Graft (coding language)." The design choices are the owner's. Claude may suggest.

### 2026-11-01 — Licences: Apache-2.0 WITH LLVM-exception for code, CC BY 4.0 for writing (owner)

The owner: "legal: Apache 2.0 with LLVM exception, CC BY 4.0". This follows CyborgPL: [`LICENSE`](LICENSE) covers the
code and everything else, and [`LICENSE-CC-BY-4.0`](LICENSE-CC-BY-4.0) covers this repo's Markdown and future logos.

### 2026-11-01 — The repo is `Artificial-IntelligenceAI/Graft-lang`, with commits in CyborgPL's style (owner)

The owner: "GH repo location: <myacc, not Soclets>/Graft-lang" and "GH commit style: Soclets/CyborgPL (don't over
read, though)". Commits are written `kind.area.topic: what is now true`, with `(owner: "…")` when the owner chose it.
The kinds are `decision`, `design`, `feature`, `fix` and `test`. The author identity is the one CyborgPL uses (a
`.invalid` address), so no personal email lands in the history. Claude created the repo **private**. Whether it
becomes public is open (pitch, decision 9).

### 2026-11-01 — Questions are asked one at a time (owner: "One question a time")

Claude had listed nine decisions at once. From now on, Claude asks one question per message, in chat, never as a
popup.

### 2026-11-01 — Graft is C syntax with a garbage collector (owner: "It's just C syntax with a GC, basically")

Asked about the core idea, the owner chose none of the pitch's three directions (foreign roots, checked grafts, live
grafting). Graft is C's syntax, with memory managed by a garbage collector instead of `malloc`/`free`. This answers
pitch decisions 1 (core idea), 4 (memory: garbage collected) and 7 (syntax: C's). "Basically" leaves open how close
to C it stays. That is the next question.

### 2026-11-01 — Graft looks like C but is its own language, as in the owner's first sample (owner: "Kinda like that")

Asked how close to C Graft stays (superset, C cleaned up, minimal change, or something else), the owner answered
with a program, kept in [`design/samples.md`](design/samples.md):

```c
void main[void] {
string str = "World!";
concat_print("Hello, " concat str concat \n);
return void;
}
```

`main[void]` and `concat` are not C, so Graft is not a superset of C. It is C-like with its own rules. The eight
things the sample shows are listed in `design/samples.md`, and each is asked separately.

### 2026-11-01 — `for (i=0;i<n;i++)` is not Graft (owner: "I do not wanna see this shit in my lang")

While choosing brackets (question 3), Claude passed on Radium's rule that a comparison needs a space on each side.
The owner: "Who in tarnation even writes `a<b`?" Claude answered that packed C loops like `for (i=0;i<n;i++)` do. The
owner said the line above. What exactly is refused (the packing, C's three-part `for`, or both) is asked next.
Question 3 (brackets for parameters and calls) is still open.

Radium's design session was consulted on `[]` vs `<>` vs `()`, at the owner's request. It reported Radium's rule:
`( )` runs, `[ ]` holds values (parameters, indexing), `< >` fills in types only, and a comparison must be spaced.

### 2026-11-01 — Operators are spaced; packed code is refused; C's three-part `for` stays (owner: "Add some fucking spaces")

Answering question 4, the owner chose (a). A binary operator (`=`, `<`, `+` and so on) has a space on each side, so
`i=0` and `i<n` are errors, and the loop is written `for (i = 0; i < n; i++)`. A unary operator like `i++` stays
attached. The exact operator list is settled when operators are designed.

### 2026-11-01 — The language is Void, renamed from Graft (owner: "Rename it to Void now, there's 3 voids in Hello World. And yes, I'm serious")

Asked question 3 again (brackets for parameters and calls, now with Radium's rule as an option), the owner said:
"You know what? Since it's gonna get abandoned anyways, it depends on my vibe. Rename it to Void now, there's 3 voids
in Hello World. And yes, I'm serious". The three are `void main[void]` and `return void;` in the hello sample.
Decisions are made by the owner's vibe. The GitHub repo is renamed `Artificial-IntelligenceAI/Void-lang` to follow
the earlier `Graft-lang`. The entries above keep the name Graft, as it was when they were made.

### 2026-11-01 — `[ ]` around a definition's parameters, `( )` around a call's arguments (owner: "(a)")

As in the hello sample: `void main[void] { … }` defines, and `concat_print(…)` calls. Twice, (a) was offered with
`[ ]` also used for indexing. `< >` is not taken for now (Radium's rule was option (b)).

### 2026-11-01 — `""` is illegal; Void uses `void` (owner: "Forget `""`, that's illegal. We use `void`, of course")

Said with the answer above. Whether this covers only the empty string (`string s = void;`) or quotes altogether is
asked next.

### 2026-11-01 — Anything empty is written `void` (owner: "anything empty uses `void`")

Answering question 5 (whether `void` replaces only the empty string or quotes altogether): neither exactly. Non-empty
strings keep their quotes (`"World!"`), and `void` is how Void writes emptiness of any kind. That covers the hello
sample's three voids: `void main` (returns nothing), `main[void]` (takes nothing) and `return void;` (gives back
nothing). It also covers the empty string, `string s = void;`, in place of the illegal `""`. Whether it reaches empty
calls (`f(void)`) and empty blocks is asked next.

### 2026-11-01 — A call with nothing to pass is written `(void)` (owner: the program below, "legal")

Asked whether "anything empty" reaches calls and blocks, the owner answered with a program, kept in
[`design/samples.md`](design/samples.md) as sample 2:

```c
void main[void] {
string str = void;
concat_print(void);
return void;
}
```

So `concat_print(void);` is how a call with nothing to pass is written, and `concat_print()` is not Void. The sample
has no empty block, so `{ void }` vs `{}` is still open.

### 2026-11-01 — An empty block is `{ void }`; `{}` is not Void (owner: "`void` is `void`, bro. You know")

Answering question 7, the owner chose (a). `void` means empty everywhere, without exception: no parameters
`[void]`, no arguments `(void)`, returning nothing `return void;`, the empty string `= void`, and the empty block
`{ void }`.

### 2026-11-01 — Escapes live only outside quotes; inside quotes a backslash is just a backslash (owner: "(a)")

`\n`, `\t` and the other escapes are values of their own, joined with `concat`:
`concat_print("Line one" concat \n concat "Line two");`. A string in quotes holds exactly what you see. Because of
that, the way to put a `"` inside a string (a bare `\"` would follow the rule) is still open.

### 2026-11-01 — No hidden conversions; `concat` joins strings only (owner: "No hidden conversions.")

Answering question 9 (what `concat` can join), the owner chose (a) and said it as a rule: Void never converts a value
behind your back. `"Age: " concat age` is an error while `age` is a number, so the number has to be turned into text
first. This reaches past `concat`: C's implicit conversions (int to float, char to int, narrowing on assignment and so
on) are not Void. How a conversion is written (`to_string(age)` was only a placeholder) is still open.

### 2026-11-01 — `concat_print` is Void's one print, built into the language; Void has no standard library (owner: "(a). Btw, there's no stdlib, this is the in the lang")

`concat_print` takes one string and prints it exactly, with no newline added. It is part of the language, not a
library function. Void has no stdlib: what it can do is built in.

### 2026-11-01 — A value is turned into a string with the built-in `string_convertor(…)` (owner: the line below)

Asked how a conversion is written, the owner answered with a line, kept as sample 3:
`concat_print("Age: " concat string_convertor(age) concat \n);`. It is a built-in written like a call, and the
spelling is "convertor".

### 2026-11-01 — Every conversion is a built-in `<type>_convertor(…)` (owner: "(a)")

For example `int_convertor("42")` and `float_convertor(age)`, alongside `string_convertor(age)`.

### 2026-11-01 — A `void` where a `;` belongs counts as nothing, so the error is the missing `;` (owner)

The owner: "Oh, btw, funnily. If you put `void` instead of `;`, the error msg would act like there's no `;`, instead
of mentioning `void` there". `void` is empty even to the compiler's errors. In `string str = "x" void`, the error says
a `;` is missing after `"x"` and never mentions `void`.

### 2026-11-01 — A failed conversion stops the program unless handled with `otherwise`; `otherwise void` is undefined behaviour (owner)

The owner: "default to stop, and you can handle with `otherwise`. And of course, if you say `otherwise void`, it's
instead UB 💀". So `int_convertor("abc")` alone stops the program with an error, while
`int n = int_convertor(s) otherwise 0;` gives `0` instead. `otherwise void` handles it with nothing, and that is
undefined behaviour: the program has promised the conversion can't fail, so the check can be skipped. What may follow
`otherwise` besides a value is asked next.

### 2026-11-01 — `otherwise` takes a value or a block (owner: "(b)")

`int n = int_convertor(s) otherwise 0;` or `int n = int_convertor(s) otherwise { … };`. What a block that doesn't
`return` gives back is asked next.

### 2026-11-01 — An `otherwise` block gives its value with `give`; `give void` makes it void, not UB (owner: "(b), and of course, if you `give void`, it would just make it void, not UB this time")

```c
int n = int_convertor(s) otherwise {
concat_print("Using 0" concat \n);
give 0;
};
```

`give` was Claude's placeholder, and the owner used it, so `give` is the word. `give void` leaves `n` void and is
well defined, unlike `otherwise void`. So an `int` can be void. What a void `int` is (a real nothing, or `0` as the
empty `int`, the way a void `string` is the empty string) is asked next.

### 2026-11-01 — A void `int` holds nothing, and using it doesn't stop: nothing + 1 is 1 (owner: "(a). Using it won't stop, it holds nothing, so it would add 1 to nothing. Which means 1")

Every type can hold void, a real "nothing", and it isn't the type's zero. Using a void value is not an error. With
`n` void, `n + 1` is `1`. What void does under other operators (`n * 3`) is asked next.

### 2026-11-01 — Multiplying by void gives void: three of nothing is nothing (owner: "Right, so it's 3 of nothing, which is nothing")

With `n` void, `n * 3` is void. Addition lets void drop out (`n + 1` is `1`), but multiplication keeps it. Claude
reads subtraction like addition (`n - 5` is `-5`, `5 - n` is `5`) and `n / 3` like multiplication (a third of nothing
is void), unless the owner says otherwise. Dividing by void (`3 / n`) is asked next.

### 2026-11-01 — Dividing by void gives void (owner: "(a)")

With `n` void, `3 / n` is void: splitting 3 into nothing parts leaves nothing. So far, `+` and `-` let void drop out,
and `*` and `/` give void whichever side it is on.

### 2026-11-01 — Void is abandoned (owner: "Say that Void is abandoned, commit & push")

The owner had said early on: "Since it's gonna get abandoned anyways, it depends on my vibe." Void stops here, the
same day it began as Graft. The last thing written was the most void program
([`design/most-void.md`](design/most-void.md)).

## Open (left unasked)

Void was abandoned with these still open: how to check for void (question 19, `n == void`, `is_void(n)` or not at
all), comparisons with void, `string`, a `"` inside a string, the readings in `design/most-void.md`, the first
program, typing, how it runs, the implementation language, the file extension and visibility.
