# Back-End Code Style

## 1. Overview

This document defines the coding conventions used in the back-end of the calculator project.

The back-end is implemented with Python, FastAPI, and a database. The goal of these conventions is to keep the source code readable, consistent, safe, and easy to maintain.

## 2. Python Style

### 2.1 Indentation

Use 4 spaces for each indentation level.

Example:

```python
def calculate(expression):
    if not expression:
        raise ValueError("Expression cannot be empty")

    return expression
2.2 Variable and Function Naming

Use snake_case for variables and functions.

Examples:

created_at = "2026-10-03"
history_id = 1

def get_database():
    pass

def calculate_expression(expression):
    pass
2.3 Constant Naming

Use uppercase letters with underscores for constants.

Examples:

DATABASE_NAME = "calculator.db"
BINARY_OPERATORS = {}
UNARY_OPERATORS = {}
2.4 Class Naming

Use PascalCase for class names.

Example:

class CalculationRequest:
    pass
3. Import Style

Place imports at the beginning of the Python file.

Separate standard-library imports from third-party imports and local project imports.

Example:

import sqlite3
from datetime import datetime

from fastapi import FastAPI, HTTPException
from pydantic import BaseModel

from calculator import calculate_expression
4. Function Design

Functions should have one clear responsibility whenever possible.

Examples:

get_database()
create_database()
calculate_expression()
evaluate_node()
get_history()
delete_history()

Avoid creating unnecessarily large functions that perform unrelated tasks.

5. API Style

Use clear REST-style endpoint names.

Examples:

POST   /api/calculate
GET    /api/history
DELETE /api/history/{history_id}

Use appropriate HTTP status codes for errors.

Examples:

200 - successful request
400 - invalid expression
404 - history record not found

API responses should use JSON.

6. Expression Evaluation and Security

Do not use Python eval() or exec() to evaluate expressions.

Only supported mathematical operations should be accepted:

+
-
*
/

The calculator may also support:

parentheses
decimal numbers
unary positive signs
unary negative signs

Unsupported AST nodes or operators must be rejected.

Example:

if operator_type not in BINARY_OPERATORS:
    raise ValueError("Unsupported operator")

Division by zero must be handled explicitly.

7. Database Style

Database operations should use parameterized SQL statements instead of building SQL commands by concatenating user input.

Example:

cursor.execute(
    """
    DELETE FROM history
    WHERE id = ?
    """,
    (history_id,)
)

The history table should contain the fields required by the project, including:

id
expression
result
created_at

Database connections should be closed after operations are complete.

8. Error Handling

Expected user errors should be handled and converted into clear API responses.

Examples include:

empty expressions
invalid expression syntax
unsupported operators
division by zero
nonexistent history records

Example:

raise HTTPException(
    status_code=400,
    detail="表达式不能为空"
)
9. Comments and Documentation

Use comments or docstrings when they help explain non-obvious logic.

Example:

def calculate_expression(expression: str):
    """
    Safely calculate a mathematical expression.
    """

Avoid comments that merely repeat the code.

10. File Organization

The main back-end files are organized as follows:

calculator_backend/
├── main.py
├── calculator.py
├── requirements.txt
├── README.md
├── codestyle.md
└── .gitignore

File responsibilities:

main.py: FastAPI routes, database operations, and API responses
calculator.py: safe expression parsing and calculation
requirements.txt: Python dependencies
README.md: project documentation
codestyle.md: coding conventions
.gitignore: files that should not be committed
11. General Principles
Follow consistent Python formatting.
Use meaningful names.
Keep functions focused.
Validate user input.
Do not use eval() or exec().
Use parameterized SQL statements.
Return clear API errors.
Keep calculation logic separate from API routing when practical.
