# Void samples from the owner

Programs the owner wrote to show what Void looks like, kept exactly as given. What each one shows is listed below
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

## 2. Nothing (2026-11-01, "legal")

The `←` notes are the owner's annotations, not Void comments.

```c
void main[void] {          ← takes nothing, gives nothing
string str = void;         ← a string holding… nothing
concat_print(void);        ← prints nothing
return void;               ← returns nothing
}
```

What it shows: `string str = void;` is the empty string, and a call with nothing to pass is written `(void)`, so
`concat_print()` is not Void. This was the owner's answer to question 6, which still leaves empty blocks open.

## 3. Conversion (2026-11-01)

```c
concat_print("Age: " concat string_convertor(age) concat \n);
```

What it shows: a conversion is a built-in written like a call, `string_convertor(…)` (spelt "convertor"), and it
turns a value into a string. Whether other types follow the same `<type>_convertor` pattern is asked next.
