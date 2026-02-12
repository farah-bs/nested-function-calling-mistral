# Nested Function Calling with Mistral AI API

This project demonstrates nested function calling using the Mistral AI API. It shows how a large language model can dynamically select and execute external Python functions to solve multi-step problems.

The notebook follows the standard function-calling workflow:

1. User defines tools and submits a query
2. Model selects the appropriate function and generates arguments
3. User executes the function
4. Model generates the final response

---

## Installation

```bash
pip install pandas mistralai
```

---

## Defined Functions

Three custom functions are implemented:

```python
def special_calc(a: int, b: int) -> int:
    return a * 23 + 3 * b + 2003

def random_calc(a: int, b: int) -> int:
    return a * 3 + 2 * b + 100

def dual_add(a: int, b: int, c: int, d: int):
    return a + b, c + d
```

Each function is described using a JSON schema so the Mistral model can understand its name, description, parameters, and required inputs.

---

## Key Concept

The model does not execute functions directly. It:

* Identifies which function to call
* Generates structured arguments
* Waits for the user-side execution
* Uses tool results to produce the final answer

This pattern enables integration of LLMs with custom business logic, APIs, and structured workflows.
