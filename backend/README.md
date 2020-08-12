# Full Stack Trivia API Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Enviornment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organaized. Instructions for setting up a virual enviornment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/)  is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use handle the lightweight sqlite database. You'll primarily work in app.py and can reference models.py. 

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross origin requests from our frontend server. 

## Database Setup
With Postgres running, restore a database using the trivia.psql file provided. From the backend folder in terminal run:
```bash
psql trivia < trivia.psql
```

## Running the server

From within the `backend` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
export FLASK_APP=flaskr
export FLASK_ENV=development
flask run
```

Setting the `FLASK_ENV` variable to `development` will detect file changes and restart the server automatically.

Setting the `FLASK_APP` variable to `flaskr` directs flask to use the `flaskr` directory and the `__init__.py` file to find the application. 

## API
### Base URL
This project isn't currently deployed anywhere and can be run as localhost on port 5000 with URL: http://127.0.0.1:5000
### Endpoints
- GET /questions
- DELETE /questions/{question_id}
- POST /questions
- GET /categories
- GET /categories/{category_id}/questions
- POST /quizzes

### GET /questions
Accepts a 'page' argument and returns 10 questions corresponding to the given page and defaults to page 1.
#### Example Request
curl localhost:5000/questions?page=2
#### Example Response
```json
{
  "questions": [
    {
      "answer": "Escher",
      "category": 2,
      "difficulty": 1,
      "id": 16,
      "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
    },
    {
      "answer": "Mona Lisa",
      "category": 2,
      "difficulty": 3,
      "id": 17,
      "question": "La Giaconda is better known as what?"
    },
    {
      "answer": "One",
      "category": 2,
      "difficulty": 4,
      "id": 18,
      "question": "How many paintings did Van Gogh sell in his lifetime?"
    },
    {
      "answer": "Jackson Pollock",
      "category": 2,
      "difficulty": 2,
      "id": 19,
      "question": "Which American artist was a pioneer of Abstract Expressionism, and a leading exponent of action painting?"
    },
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {
      "answer": "Alexander Fleming",
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": "Who discovered penicillin?"
    },
    {
      "answer": "Blood",
      "category": 1,
      "difficulty": 4,
      "id": 22,
      "question": "Hematology is a branch of medicine involving the study of what?"
    },
    {
      "answer": "Scarab",
      "category": 4,
      "difficulty": 4,
      "id": 23,
      "question": "Which dung beetle was worshipped by the ancient Egyptians?"
    }
  ],
  "success": true,
  "total_questions": 18
}
```
### DELETE /questions/{question_id}
Deletes the question of the given id.
#### Example Request
curl -X DELETE localhost:5000/questions/4
#### Example Response
```json
{
  "question_id": 4,
  "success": true
}
```
### POST /questions
There are two ways to use this endpoint: 
 - If a 'searchTerm' is sent in the body then the request is treated as a searching request and the returned response will contain questions that has the search term as a substring in them.
 #### Example Request
  curl -X POST localhost:5000/questions -H 'Content-type:application/json' -d '{"searchTerm":"was"}'
 #### Example Response
 ```json
  {
    "current_category": null,
    "questions": [
      {
        "answer": "Edward Scissorhands",
        "category": 5,
        "difficulty": 3,
        "id": 6,
        "question": "What was the title of the 1990 fantasy directed by Tim Burton about a young man with multi-bladed appendages?"
      },
      {
        "answer": "Escher",
        "category": 2,
        "difficulty": 1,
        "id": 16,
        "question": "Which Dutch graphic artist\u2013initials M C was a creator of optical illusions?"
      },
      {
        "answer": "Jackson Pollock",
        "category": 2,
        "difficulty": 2,
        "id": 19,
        "question": "Which American artist was a pioneer of Abstract Expressionism, and a leading exponent of action painting?"
      },
      {
        "answer": "Scarab",
        "category": 4,
        "difficulty": 4,
        "id": 23,
        "question": "Which dung beetle was worshipped by the ancient Egyptians?"
      }
    ],
    "success": true,
    "total_questions": 4
  }
 ```
 - Otherwise the request is treated as a create request to insert a new question in the database and expects a 'questions', an 'answer', a 'difficulty', and a 'category' in the json body.
 #### Example Request
  curl -X POST localhost:5000/questions -H 'Content-type:application/json' -d '{"question":"Some Question?", "answer":"Some answer", "difficulty":2, "category":3}'
 #### Example Response
 ```json
  {
    "question_id": 25,
    "success": true
  }
```
### GET /categories
Returns all the categories in the database.
#### Example Request
curl localhost:5000/categories
#### Example Response
```json
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "success": true
}
```
### GET /categories/{category_id}/questions
Returns all the questions in the category of the given id.
#### Example Request
curl localhost:5000/categories/1/questions
#### Example Response
```json
{
  "current_category": 1,
  "questions": [
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {
      "answer": "Alexander Fleming",
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": "Who discovered penicillin?"
    },
    {
      "answer": "Blood",
      "category": 1,
      "difficulty": 4,
      "id": 22,
      "question": "Hematology is a branch of medicine involving the study of what?"
    }
  ],
  "success": true,
  "total_questions": 3
}
```
### POST /quizzes
Expects a 'quiz_category' and a 'previous_questions' list in the json body, and returns a random question from the given category that is not one of the given 'previous_questions', if no questions are left in the categories returns a null question.
#### Example Request
curl -X POST localhost:5000/quizzes -H 'Content-type:application/json' -d '{"quiz_category":1, "previous_questions":[20, 21]}'
#### Example Response
```json
{
  "question": {
    "answer": "Blood",
    "category": 1,
    "difficulty": 4,
    "id": 22,
    "question": "Hematology is a branch of medicine involving the study of what?"
  },
  "success": true
}
```
### Error Codes
- Failure of providing any required parameter will result in 400 status code with this response:
```json
  {
    "error": 400,
    "message": "Bad request",
    "success": false
  }
```
- Trying to access a question or a category or any resource that doesn't exist wiill result in a 404 status code with this response:
```json
  {
    "error": 404,
    "message": "Resource not found",
    "success": false
  }
```

## Testing
To run the tests, run
```
dropdb trivia_test
createdb trivia_test
psql trivia_test < trivia.psql
python test_flaskr.py
```
