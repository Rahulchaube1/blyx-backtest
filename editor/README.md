# Blyx Backtest

Evaluate forecasts in time order with a gap for delayed observations and disjoint test windows.

This extension includes the Blyx Backtest 0.1.1 source, a runnable example and completions for its public functions. It uses the Blyx Language extension for syntax highlighting and execution.

## Run in the editor

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

## Use Backtest in a project

Extract the starter into a new folder. It contains `main.blyx`, the licensed framework source in `vendor/backtest`, and a VS Code task. With the Blyx 0.2.1 compiler and host toolchain installed, run `blyxc native-run main.blyx` from that folder. Type `blyx-backtest-` in a Blyx file to see the framework completions. [Download the starter ZIP](https://github.com/Rahulchaube1/blyxxxx/releases/download/framework-editors-v0.1.0/blyx-backtest-starter-0.1.0.zip)

[API and input requirements](https://www.blyx-lang.space/packages/backtest) · [Framework source](https://github.com/Rahulchaube1/blyx-backtest/tree/2371260a23c140652d58fcec38a81a6e756a3282) · [Report an issue](https://github.com/Rahulchaube1/blyx-backtest/issues)

[GitHub Sponsors](https://github.com/sponsors/Rahulchaube1) · [Buy Me a Coffee](https://buymeacoffee.com/rahulchaube)
