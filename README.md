# Blyx Backtest

A walk-forward evaluation framework for single-series forecasts, written in Blyx. Plan chronological training and test windows, leave a gap for delayed labels, and compare your forecasts with last-value and training-mean baselines on identical observations.

## Try it

Install Blyx 0.2.1, Rust 1.85 or later and a host linker. From this repository, run:

```sh
blyxc native-run example.blyx
blyxc native-run tests.blyx
```

For demand `[10, 20, 30, 40, 50, 60, 70, 80]`, start with three observations, leave a one-observation gap and evaluate the following two. Advance two observations for the next fold. With a rolling training window of two, the four scored observations give last-value MAE of **25**, training-mean MAE of **30**, and MAE of **5** for the supplied model forecasts.

## Use it in a project

From the directory containing your entry file:

```sh
git clone --depth 1 --branch v0.1.0 https://github.com/Rahulchaube1/blyx-backtest.git vendor/backtest
```

```blyx
use vendor::backtest::backtest;

fn main() {
    let y = [10, 20, 30, 40, 50, 60, 70, 80];
    let scores = bt_baselines(y, 3, 2, 1, 2);
    println!(at(scores, 1));
}
```

Save this as `main.blyx` and run `blyxc native-run main.blyx`. The result is `25`.

## Fold and scoring contracts

| Function | Result |
| --- | --- |
| `bt_fold_count(n, initial, horizon, gap)` | Number of complete test folds. Returns 0 if the history is too short and -1 for invalid parameters. |
| `bt_fold(n, initial, horizon, gap, window, fold)` | `[train_start, train_end, test_start, test_end]` for the zero-based fold. Ends are exclusive. |
| `bt_baselines(series, initial, horizon, gap, window)` | `[scored_rows, last_value_MAE, training_mean_MAE]`. Each baseline makes its entire horizon forecast using only that fold’s training window. |
| `bt_score(series, forecasts, initial, horizon, gap)` | `[scored_rows, MAE, mean_signed_error]` for your forecasts, packed in test-fold order. A positive signed error means overprediction. |

`initial` and `horizon` must be positive. A nonnegative `gap` counts observations between the end of training and the first test point. Set `window` to zero for expanding training, or a positive value to cap it at that many observations. A trailing partial test horizon is excluded. Test folds are contiguous and disjoint. Vector results are empty for invalid inputs, nonfinite values or arithmetic overflow, and when there are no complete folds to score.

For the example, the first fold trains on positions 1 and 2, skips position 3 and scores positions 4 and 5. The next fold trains on 3 and 4, skips 5 and scores 6 and 7. Earlier observations may enter a later training window when they become available. The baseline runner updates its training sum as the window moves and uses a single chronological pass after validating the series.

The caller orders the series by time and chooses a gap that reflects actual data availability. For custom models, fit feature transformations and train on each fold’s training data before predicting the test horizon. The scorer can align submitted predictions and measure their errors. Only the model pipeline can establish what data went into those predictions.

[Blyx ecosystem](https://www.blyx-lang.space/packages) · [Blyx compiler](https://github.com/Rahulchaube1/blyxxxx/releases/tag/v0.2.1)
