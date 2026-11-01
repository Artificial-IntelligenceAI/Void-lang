# The most void Void program

Written by Claude at the owner's request ("Create the most voids void program", 2026-11-01). It uses only what
[`DECISIONS.md`](../DECISIONS.md) has settled, plus a few readings that are marked below. It has 25 `void`s, and it
does nothing: it takes nothing, prints nothing and returns nothing.

```c
void nothing[void] {
void;
{ void }
return void;
}

void main[void] {
void;
string str = void;
string more = void concat void concat str;
string said = string_convertor(void);
int n = void;
int m = n * void / void;
int k = int_convertor(void) otherwise {
nothing(void);
give void;
};
concat_print(void);
concat_print(str concat more concat said);
nothing(void);
{ void }
for (void; void; void) {
return void;
}
}
```

## What each part does

- `void nothing[void]` takes nothing and returns nothing. Its body is an empty statement, an empty block and
  `return void;`.
- `str`, `more` and `said` are all the empty string. Joining nothing to nothing is nothing, and converting nothing
  to text is nothing.
- `n` is a void `int`. `m` is `n * void / void`, and since `*` and `/` keep void, `m` is void.
- `int_convertor(void)` has nothing to convert, so it fails. The `otherwise` block calls `nothing` and does
  `give void`, which is well defined (it isn't `otherwise void`, which would be UB 💀). So `k` is void.
- `concat_print(void)` prints nothing. Then `concat_print(str concat more concat said)` prints nothing three times.
- `for (void; void; void)` has no start, no condition and no step, so it loops forever, as C's `for (;;)` does. Its
  body returns at once, so the program ends there.

## Readings used here, not yet decided

1. `void;` is the empty statement (C's lone `;`). This follows "anything empty uses `void`".
2. `int n = void;` sets a void `int` directly, not only through `give void`.
3. `for (void; void; void)`: each empty part of a `for` is `void`, and an empty condition loops forever.
4. `void concat void` is void, and `string_convertor(void)` is void.
5. `int_convertor(void)` fails, because there is nothing to convert.
6. `n == void` was left out on purpose: how to check for void is question 19, still open.
