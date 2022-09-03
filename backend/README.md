# Backend - Trivia API

## Setting up the Backend

### Install Dependencies

1. **Python 3.8** - Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

2. **Virtual Environment** - We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

3. **PIP Dependencies** - Once your virtual environment is setup and running, install the required dependencies by navigating to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

#### Key Pip Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) is the Python SQL toolkit and ORM we'll use to handle the lightweight SQL database. You'll primarily work in `app.py`and can reference `models.py`.

- [Flask-CORS](https://flask-cors.readthedocs.io/en/latest/#) is the extension we'll use to handle cross-origin requests from our frontend server.

### Set up the Database

With Postgres running, create a `trivia` database:

```bash
createdb trivia
```

Populate the database using the `trivia.psql` file provided. From the `backend` folder in terminal run:

```bash
psql trivia < trivia.psql
```

### Run the Server

From within the `./src` directory first ensure you are working using your created virtual environment.

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

## Tasks

One note before you delve into your tasks: for each endpoint you are expected to define the endpoint and response data. The frontend will be a plentiful resource because it is set up to expect certain endpoints and response data formats already. You should feel free to specify endpoints in your own way; if you do so, make sure to update the frontend or you will get some unexpected behavior. 

1. Use Flask-CORS to enable cross-domain requests and set response headers. 
2. Create an endpoint to handle GET requests for questions, including pagination (every 10 questions). This endpoint should return a list of questions, number of total questions, current category, categories. 
3. Create an endpoint to handle GET requests for all available categories. 
4. Create an endpoint to DELETE question using a question ID. 
5. Create an endpoint to POST a new question, which will require the question and answer text, category, and difficulty score. 
6. Create a POST endpoint to get questions based on category. 
7. Create a POST endpoint to get questions based on a search term. It should return any questions for whom the search term is a substring of the question. 
8. Create a POST endpoint to get questions to play the quiz. This endpoint should take category and previous question parameters and return a random questions within the given category, if provided, and that is not one of the previous questions. 
9. Create error handlers for all expected errors including 400, 404, 422 and 500. 

## Endpoints

### GET `/categories`
- Fetches a dictionary of categories in which the keys are the ids and the value is the corresponding string of the category.
- Request arguments: None.
- Returns:  An object with these keys:
  - `success`: The success flag
  - `categories`: Contains a object of `id:category_string` and `key:value pairs`.

```json
{
  "success": true,
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  }
}
```

### GET `/questions`
- Fetches:
  - A list of questions (paginated by 10 items)
  - A dictionary of categories
  - The total of questions
  - The current category
- Request arguments:
  - `page` (integer) - The current page
- Returns: An object with these keys:
  - `success`: The success flag
  - `questions`: A list of questions (paginated by 10 items)
  - `categories`: A dictionary of categories
  - `total_questions`: The total of questions
  - `current_category`: The current category

```json
{
  "success": true,
  "questions": [
    {
      "answer": "Apollo 13",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What movie earned Tom Hanks his third straight Oscar nomination, in 1996?"
    },
    {
      "answer": "Tom Cruise",
      "category": 5,
      "difficulty": 4,
      "id": 4,
      "question": "What actor did author Anne Rice first denounce, then praise in the role of her beloved Lestat?"
    },
  ],
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "total_questions": 10,
  "current_category": null,
}
```

### DELETE `/questions/:question_id/`
- Delete question using a question ID
- Request arguments:
  - `question_id` (integer): The question id
- Returns: An object with theses keys:
  - `success` that contains a `boolean`.
  - `deleted` that contains the ID of the question created.

```json
{
  "success": true,
  "deleted": 1,
}
```

### POST `/questions`
- Create a new question.
- Request arguments:
  - `question` (string) - The question
  - `answer` (string) - The answer
  - `difficulty` (string) - The question difficulty
  - `category` (string) - The question category
- Returns: An object with theses keys:
  - `success` that contains a `boolean`.
  - `created` that contains the ID of the question created.

```json
{
  "success": true,
  "created": 1,
}
```

### POST `/search`
- Search a question.
- Request arguments:
  - `search` (string) - The term to search
- Returns: An object with these keys:
  - `success`: The success flag
  - `questions`: A list of questions
  - `total_questions`: The total of questions
  - `current_category`: The current category

```json
{
  "success": true,
  "questions": [
    {
      "answer": "M. Sall",
      "category": 2,
      "difficulty": 3,
      "id": 2,
      "question": "Who is the actual president of Senegal?"
    },
    {
      "answer": "Eminem",
      "category": 4,
      "difficulty": 3,
      "id": 4,
      "question": "Who is the best rapper for ever?"
    },
  ],
  "total_questions": 10,
  "current_category": null,
}
```


### GET `/categories/:category_id/questions`
- Fetches a list of questions based on category.
- Request arguments:
  - `category_id` (integer): The category id
- Returns: An object with these keys:
  - `success`: The success flag
  - `questions`: A list of questions (paginated by 10 items)
  - `total_questions`: The total of questions
  - `current_category`: The current category

```json
{
  "success": true,
  "questions": [
    {
      "answer": "Lake Victoria",
      "category": 5,
      "difficulty": 4,
      "id": 2,
      "question": "What is the largest lake in Africa?"
    },
    {
      "answer": "Eminem",
      "category": 3,
      "difficulty": 4,
      "id": 4,
      "question": "Who is the best rapper for ever?"
    },
  ],
  "total_questions": 10,
  "current_category": 1,
}
```

### POST `/quizzes`
- Fetches a question to play the quiz.
- Request arguments:
  - `quiz_category` (dictionary): The quiz category with the `type` and the `id`.
  - `previous_ids` (list of strings): The previous questions ids
- Returns: An object with these keys:
  - `success`: The success flag
  - `question`: The question to play

```json
{
  "success": true,
  "question":{
    "answer": "Uruguay",
    "category": 5,
    "difficulty": 4,
    "id": 2,
    "question": "Which country won the first ever soccer World Cup in 1930?"
  }
}
```

## Errors

### Error 400
- Returns an object with these keys: `success`, `error` and `message`.

```json
{
  "success": false,
  "error": 400,
  "message": "bad request"
}
```

### Error 404
- Returns an object with these keys: `success`, `error` and `message`.

```json
{
  "success": false,
  "error": 404,
  "message": "resource not found"
}
```

### Error 422
- Returns an object with these keys: `success`, `error` and `message`.

```json
{
  "success": false,
  "error": 422,
  "message": "unprocessable"
}
```

### Error 500
- Returns an object with these keys: `success`, `error` and `message`.

```json
{
  "success": false,
  "error": 500,
  "message": "internal server error"
}
```

## Testing
To run the tests, run the script `test_flaskr.py`:

```bash
# Commande line after cd /backend

python3 test_flaskr.py
```