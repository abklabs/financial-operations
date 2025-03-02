# Abklabs Financial Operations

[![Crates.io](https://img.shields.io/crates/v/abklabs-financial-operations)](https://crates.io/crates/abklabs-financial-operations)
[![Docs.rs](https://docs.rs/abklabs-financial-operations/badge.svg)](https://docs.rs/abklabs-financial-operations)
[![License](https://img.shields.io/crates/l/abklabs-financial-operations)]()

This crate provides a set of operations for working with financial data, more specifically, avoiding
the usage of floating point types.

## Usage

```rust
use abklabs_financial_operations::CheckedDecimalOperations;

fn test_add_decimals() {
    let a: u64 = 1_0000;
    let a_decimals = 4;
    let b: u64 = 2_00;
    let b_decimals = 2;

    let (result, decimals) = a.add_decimals_checked(b, a_decimals, b_decimals)?;
    assert_eq!(result, 3_0000);
    assert_eq!(decimals, 4);

    let a: u32 = 123_45;
    let a_decimals = 2;
    let b: u32 = 0_45;
    let b_decimals = 2;

    let (result, decimals) = a.add_decimals_checked(b, a_decimals, b_decimals)?;
    assert_eq!(result, 123_90);
    assert_eq!(decimals, 2);
}
```

Very useful when dealing with money or blockchain transactions.

## Supported operations

### Checked

This set of operations will return an `Result` with the result and the number of decimals,
if the operation is successful. If the operation is not successful, it will return a `DecimalOperationError`.

```rust
use abklabs_financial_operations::CheckedDecimalOperations;
```

- `add_decimals_checked`
- `sub_decimals_checked`
- `mul_decimals_checked`
- `div_decimals_checked`
- `rem_decimals_checked`

### Unchecked

This set of operations will return the result and the number of decimals, without any checks,
carrying the underlying operation way of handling overflows and underflows.

```rust
use abklabs_financial_operations::DecimalOperations;
```

- `add_decimals`
- `sub_decimals`
- `mul_decimals`
- `div_decimals`
- `rem_decimals`
