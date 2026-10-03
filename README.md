# Front-End and Back-End Separation Calculator - Back End

## 1. Project Introduction

This repository contains the back-end part of a front-end and back-end separation calculator project.

The back end receives mathematical expressions from the front end through HTTP requests, safely evaluates supported expressions, returns calculation results, and manages calculation history in a database.

The calculation is performed by the back end. Python `eval()` and `exec()` are not used.

## 2. Main Features

- REST API based on FastAPI
- Addition
- Subtraction
- Multiplication
- Division
- Operator precedence
- Parentheses
- Decimal numbers
- Unary positive and negative signs
- Safe expression parsing
- Division-by-zero handling
- Invalid-expression handling
- Calculation history storage
- History query
- Delete a specified history record
- Cross-origin request support

## 3. Technology Stack

- Python
- FastAPI
- Uvicorn
- SQLite for local development
- Python AST for safe expression parsing

## 4. Project Structure

```text
calculator_backend/
├── main.py
├── calculator.py
├── requirements.txt
├── README.md
└── codestyle.md
File Description
main.py: FastAPI application, API routes, and database operations.
calculator.py: Safe mathematical expression parsing and evaluation.
requirements.txt: Python package dependencies.
README.md: Project documentation and running instructions.
codestyle.md: Back-end coding conventions.
5. Running Environment

Recommended environment:

Python 3.9 or later

A Python virtual environment is recommended.

6. Installation

Clone or download this repository.

Create a virtual environment:

Windows
python -m venv venv

Activate it:

venv\Scripts\activate

Install the dependencies:

pip install -r requirements.txt

The main dependencies are:

fastapi
uvicorn
7. Starting the Back End

Run:

uvicorn main:app --reload

The local server will normally be available at:

http://127.0.0.1:8000

The FastAPI interactive API documentation is available at:

http://127.0.0.1:8000/docs
8. API Design
8.1 Server Status
GET /

Example response:

{
  "message": "Calculator backend is running"
}
8.2 Calculate an Expression
POST /api/calculate

Example request:

{
  "expression": "1+2*3"
}

Example response:

{
  "success": true,
  "expression": "1+2*3",
  "result": 7
}
8.3 Get Calculation History
GET /api/history

Returns calculation history stored in the database.

8.4 Delete a History Record
DELETE /api/history/{history_id}

Deletes the history record with the specified ID.

9. Expression Evaluation

The project does not use:

eval()
exec()

Instead, mathematical expressions are parsed using Python's Abstract Syntax Tree (AST).

Only supported nodes and operators are evaluated.

Supported binary operators:

+
-
*
/

The calculator also supports:

Parentheses
Decimal numbers
Unary positive signs
Unary negative signs

Examples:

1+2*3      -> 7
(1+2)*3    -> 9
-5+8       -> 3
3*-2       -> -6
1.5+2.5    -> 4.0
10. Error Handling

Examples of handled errors include:

Empty expression
Invalid expression syntax
Unsupported operators
Division by zero
Invalid expression content
History record not found

For example:

10/0

returns an error indicating that the divisor cannot be zero.

11. Database

SQLite is used for local development.

When the back-end application starts, the database table is created automatically if it does not already exist.

The history table contains:

id
expression
result
created_at

Successful calculations are stored in the database.

Failed calculations are not stored as successful history records.

12. Front-End Connection

For local development, the front end connects to:

http://127.0.0.1:8000

The back end provides CORS support so that the front-end application can send HTTP requests to the API.

The communication process is:

Front End
    ↓
HTTP / JSON
    ↓
FastAPI
    ↓
Expression Evaluator
    ↓
Database
13. Deployment

For production deployment, the application can be started with a command such as:

uvicorn main:app --host 0.0.0.0 --port $PORT

The public API address will be added after deployment is completed.

A persistent production database should be used if the hosting platform does not provide persistent storage for local SQLite files.
