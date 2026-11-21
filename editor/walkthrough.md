## Backtest a demand forecast

Choose an initial training history, a positive horizon and a nonnegative gap. A zero training window expands the history. A positive window caps its length. The final incomplete test horizon is omitted.

1. Open an empty file named `backtest-demo.blyx`.
2. Type `blyx-backtest-demo` and select **Backtest — runnable example**. You can also use **Snippets: Fill File with Snippet**.
3. Choose **Blyx: Run File** from the command palette. Change an argument near the end of `fn main()` to try another input.

Expected output

```text
4
25
30
5
```

[Work through the example in the browser](https://www.blyx-lang.space/play?example=package-backtest)
