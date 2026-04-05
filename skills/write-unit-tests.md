# Skill: Write Unit Tests

## Purpose

Generate comprehensive unit tests for a given piece of code.

## Instructions

When asked to write unit tests, follow this process:

1. **Understand the unit under test** – Identify all public functions/methods, their inputs, outputs, and side effects.
2. **Identify test cases** – Cover:
   - Happy path (valid inputs producing expected outputs)
   - Edge cases (empty collections, zero values, boundary values)
   - Error cases (invalid inputs, missing required data, exception paths)
3. **Structure each test**:
   - Use the Arrange / Act / Assert pattern.
   - Give each test a descriptive name: `test_<function>_<scenario>_<expected_result>`.
   - Keep each test focused on a single behaviour.
4. **Mock external dependencies** – Replace database calls, HTTP requests, and filesystem access with mocks/stubs.
5. **Assert specifically** – Check the exact return value, raised exception type, or side-effect; avoid overly broad assertions.

## Example

```python
# Unit under test
def divide(a: float, b: float) -> float:
    if b == 0:
        raise ValueError("Cannot divide by zero")
    return a / b

# Generated tests
def test_divide_positive_numbers_returns_quotient():
    assert divide(10, 2) == 5.0

def test_divide_by_zero_raises_value_error():
    with pytest.raises(ValueError, match="Cannot divide by zero"):
        divide(10, 0)

def test_divide_negative_dividend_returns_negative_quotient():
    assert divide(-10, 2) == -5.0
```
