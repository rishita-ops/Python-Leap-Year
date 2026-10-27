# Python — Leap Year Checker

A command-line program that tells whether a given year is a leap year using the Gregorian calendar rules.

---

## Problem Statement

A year is a **leap year** if:

- it is divisible by **4**, **and**
- it is **not** divisible by **100**, **unless**
- it is also divisible by **400**.

Read a year and print whether it is a leap year.

**Example**

```
Enter a year: 2024
2024 is a leap year
```

---

## Solution

```python
year=int(input("Enter a year: "))

if year%4==0 and year%100!=0 or year%400==0:
    print(year,"is a leap year")
else:
    print(year,"is not a leap year")
```

---

## The Critical Idea

The rule has an exception to an exception, which fits in one boolean expression:

```
(divisible by 4 AND not divisible by 100)  OR  divisible by 400
```

Python evaluates `and` before `or`, so the original line already groups this way. Adding parentheses makes that grouping visible.

---

## How the Condition Works

| Part              | Meaning                          | Example |
| ----------------- | -------------------------------- | ------- |
| `year % 4 == 0`   | Candidate leap year              | 2024    |
| `year % 100 != 0` | Not a century year               | 2024    |
| `year % 400 == 0` | Century year that is a leap year | 2000    |

A century year such as 1900 fails the first group (divisible by 100) and the second (not divisible by 400), so it is not a leap year.

---

## Pseudocode

```
read year
if (year % 4 == 0 and year % 100 != 0) or (year % 400 == 0):
    print leap year
else:
    print not a leap year
```

---

## Dry Run

| Year | %4==0 | %100!=0 | %400==0 | Result          |
| ---- | ----- | ------- | ------- | --------------- |
| 2024 | True  | True    | False   | Leap year       |
| 2023 | False | True    | False   | Not a leap year |
| 1900 | True  | False   | False   | Not a leap year |
| 2000 | True  | False   | True    | Leap year       |
| 2100 | True  | False   | False   | Not a leap year |

---

## Complexity

- **Time:** O(1)
- **Space:** O(1)

---

## Edge Cases

| Case                                        | Behaviour                                                                 |
| ------------------------------------------- | ------------------------------------------------------------------------- |
| Century years (1900, 2100)                  | Not leap years                                                            |
| Century years divisible by 400 (2000, 2400) | Leap years                                                                |
| Year `0`                                    | Reported as a leap year (`0 % 400 == 0`)                                  |
| Negative years                              | Follow the same arithmetic, but the Gregorian calendar did not exist then |
| Non-numeric input                           | `ValueError` crash                                                        |

---

## Code-Quality Notes

- Add parentheses: `(year % 4 == 0 and year % 100 != 0) or (year % 400 == 0)`. The behaviour is the same, but the intent is clear.
- Wrap the input in `try/except ValueError`.
- Put the logic in a function `is_leap(year)` that returns a boolean, which makes it easy to test.
- The standard library offers `calendar.isleap(year)` for comparison.

---

## Natural Extension

- Check a **range of years** and list all leap years.
- Count leap years between two years.
- Return **days in a given month**, accounting for February.
- Write unit tests for the five dry-run years.

---

## Repository Structure

```
python-practice/
├── leap_year.py
└── README.md
```

---

## How to Run

```bash
python leap_year.py
```

---

## Key Concepts

- Modulo operator (`%`)
- Logical operators `and` / `or`
- Operator precedence
- `if / else`
- Type casting with `int()`

---

## Why This Problem Matters

This looks simple, but it shows how **operator precedence** and **layered rules** can break a condition. The same careful reasoning is needed in date handling, billing cycles and scheduling logic.

---

## Contributing

Suggestions and improvements are welcome. Fork the repo, make your change and open a pull request.

---

## License

This project is open source and available under the MIT License.
