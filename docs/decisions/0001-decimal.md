# 0001: Use shopspring/decimal for money

**Problem:** prices and amounts need exact arithmetic. float64 cannot represent 2012.30 exactly, and errors accumulate across lots.
**Alternatives:** float64 (inexact); int64 paise (exact, but per-unit costs and averages need more than 2 decimals).
**Decision:** `github.com/shopspring/decimal` for all prices and amounts.
**Cost:** one external dependency, slower than ints, and values must be compared with `Equal`, not `==`.
**Revisit if:** profiling shows decimal is a bottleneck (unlikely for a CLI).