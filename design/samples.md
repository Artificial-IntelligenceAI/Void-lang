# Graft samples from the owner

Programs the owner wrote to show what Graft looks like, kept exactly as given. What each one shows is listed below
it. A reading becomes a rule only once the owner confirms it in [`DECISIONS.md`](../DECISIONS.md).

## 1. Hello (2026-11-01, "Kinda like that")

```c
void main[void] {
string str = "World!";
concat_print("Hello, " concat str concat \n);
return void;
}
```

What it shows (to be confirmed, one question at a time):

1. A function's parameter list is in square brackets, `main[void]`, but the call `concat_print(…)` uses parentheses.
2. `string` is a built-in type.
3. `concat` is an infix operator that joins strings.
4. `\n` is written bare, outside quotes, as a value.
5. `concat_print` is the printing function.
6. A `void` function ends with `return void;`.
7. `main` returns `void` and takes `void`.
8. Declarations (`string str = …;`) and statements ending in `;` are C's.
