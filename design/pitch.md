# Graft — the pitch

> Status: **not taken.** On 2026-11-01 the owner chose "C syntax with a GC, basically" instead of any of these
> directions (see [`DECISIONS.md`](../DECISIONS.md)). This page is kept for the record.

In grafting, a cutting (the **scion**) is joined onto a rooted plant (the **stock**). They grow together at the
**union**, and the result is one plant. The name suggests three different languages. Each is a real direction, and
each is described below with a small program.

---

## Direction A — Graft onto other ecosystems (the stock is someone else's code)

Graft is a compiled language that grows on top of existing libraries. You don't write bindings: you name a C header,
a Rust crate or a Python module as a **root**, and its functions and types are usable straight away, typed. Graft
code is the scion.

```graft
root c "stdio.h"
root c "sqlite3.h" link "sqlite3"

fn main() {
    let db = c.sqlite3_open("notes.db")?
    c.printf("opened %s\n", "notes.db")
}
```

- **Like:** Zig's `@cImport`, Nim, Kotlin on the JVM, Swift's C interop.
- **Strength:** useful on day one, because there's a huge library on day one.
- **Weakness:** the most crowded space. Your foreign roots are only as safe as the code they come from.

## Direction B — Open types with checked grafts (the stock is any type)

Every type is a **stock** that anyone can **graft** onto: methods, interface implementations and even fields, from
any module, without editing the original. The compiler checks every **union**: wherever two grafts meet (two
modules adding `to_json` to `Point`, say), it refuses the program and asks you to choose. You never get a silent
winner.

```graft
// geometry.graft
stock Point { x: f64, y: f64 }

// render.graft — never touches geometry.graft
graft Point {
    fn len(self) -> f64 = sqrt(self.x * self.x + self.y * self.y)
}

// json.graft
graft Point as Json {
    fn to_json(self) -> Str = "{\"x\": {self.x}, \"y\": {self.y}}"
}

// cache.graft: a grafted field, stored beside the value without changing Point's layout
graft Point {
    field seen: u32 = 0
}
```

- **Like:** Rust traits without the orphan rule, Swift extensions, Clojure protocols, C# extension methods, plus
  something none of them has: grafted fields, and checked conflicts as a language rule.
- **Strength:** a single idea that the whole language can be built around, and it fits the name exactly. Direction
  A also fits in: a C library is just another stock.
- **Weakness:** coherence (which grafts are visible where) is the hard design problem. Grafted fields need
  whole-program compilation or side tables.

## Direction C — Live grafting (the stock is a running program)

A Graft program can be changed while it runs. You graft a new version of a function, type or module into the live
process, and the language guarantees the union holds: types still line up, and state is migrated by code you wrote.

```graft
// server.graft — running
fn handle(req: Req) -> Resp { ... }

// patch.graft — applied to the running process
graft handle = fn(req: Req) -> Resp { ... the fix ... }

graft Session from v1 {          // state migration, checked by the compiler
    field locale: Str = "en"
}
```

- **Like:** Erlang/BEAM hot code loading, Smalltalk images, Lisp's live environments, Unison.
- **Strength:** rare among typed languages, and very good for servers, games and live coding.
- **Weakness:** needs a runtime/VM, which makes systems-level targets harder.

---

## Suggestion

**B, with A as part of it.** "Everything is a stock, and you graft onto it" is one rule, and it also covers foreign
code: `root c "sqlite3.h"` just becomes a stock you can graft onto. Live grafting (C) can come later on top of B
without redesign, because a live patch is just a graft applied at run time.

---

## Decisions for the owner

Answer in any form, e.g. `1b 2: games 3a …`. Each one goes into [`DECISIONS.md`](../DECISIONS.md) with your words.
Where I have a suggestion it is marked ★.

1. **Core idea:** (a) A, foreign roots · (b) B, open types with checked grafts ★ · (c) C, live grafting · (d) a mix
   (say which) · (e) something else.
2. **What is the first real program written in Graft?** For example a CLI tool, a game, a server, a compiler, data
   scripts. This decides most of what follows, so it is worth answering even roughly.
3. **Typing:** (a) static with inference ★ · (b) gradual (types optional) · (c) dynamic.
4. **Memory:** (a) garbage collected · (b) ownership and borrowing (Rust-style) · (c) reference counting (Swift-style)
   · (d) regions/arenas. ★ depends on 2: (a) for scripting/servers, (c) for games/apps, (b) for systems.
5. **How it runs:** (a) native via LLVM · (b) its own VM/bytecode · (c) compiles to C · (d) an interpreter first as
   the reference, a compiler later ★.
6. **What the compiler is written in:** (a) Rust ★ · (b) Zig · (c) C++ · (d) Graft itself later, starting in (a)–(c).
7. **Syntax family:** (a) braces, Rust/Swift-like (as above) · (b) indentation, Python-like · (c) its own look ·
   (d) decide later, after semantics ★.
8. **File extension:** (a) `.graft` ★ · (b) `.gft` · (c) `.gr`.
9. **Repo visibility:** `Graft-lang` was created **private**. (a) keep it private for now · (b) make it public.
