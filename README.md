# Full Stack Project Casting Agency

## Project Description
This is the udacity final project "Casting Agency". There are three different roles in the agency: an assistant, a producer and a director. (Access Token can be find below)

## Project Result
Heroku: https://udacity-final-project.onrender.com/

Localhost: http://127.0.0.1:5000/

## Tech Stack
* **PostgreSQL** as our database of choice
* **Python3** and **Flask** as our server language and server framework
* **Auth0** for authentication management
* **Render** for deployment

## Getting Started

1. Initialize and activate a virtualenv:
  ```
  $ cd YOUR_PROJECT_DIRECTORY_PATH/
  $ python -m venv venv
  $ venv\Scripts\activate.bat
  ```

2. Install the dependencies:
  ```
  $ pip install -r requirements.txt
  ```
  This will install all of the required packages satated in the `requirements.txt` file.

3. Database Setup

  ```
  flask db init
  ```

4. Run the development server:
  ```
  $ export FLASK_APP=app.py
  $ export FLASK_ENV=development # enables debug mode
  flask run
  ```

## Testing
To run the tests, run 
```
dropdb casting_test
createdb casting_test
psql casting_test < casting.pgsql
python -m unittest test_app.py
```

## API Reference

### Endpoints

#### GET '/movies'
- General:
    - Return all movies in the database
    - Role Authorized: Assistant, Director, Producer
- Example: ```curl -H "Authorization: Bearer <Token>" http://127.0.0.1:5000/movies```
```
{
    "movies": [
        {
            "id": 2,
            "release_date": "Fri, 07 Feb 2020 00:00:00 GMT",
            "title": "Birds of Prey"
        },
    ],
    "success": true
}
```
#### GET '/actors'
- General:
    - Return all actors in the database
    - Role Authorized: Assistant, Director, Producer
- Example: ```curl -H "Authorization: Bearer <Token>" http://127.0.0.1:5000/actors```
```
{
    "actors": [
        {
            "age": 30,
            "gender": "F",
            "id": 2,
            "movie_id": 2,
            "name": "Margot Robbie"
        },
    ],
    "success": true
}
```

#### POST '/movies'
- General:
    - Add a new movie. The new movie must have all required information. 
    - Role Authorized: Producer
- Example: ```curl -X POST - H '{"Content-Type: application/json", "Authorization: Bearer <TOKEN>}' -d '{"title": "Movie 1", "release_date": "2017-10-20"}' http://127.0.0.1:5000/movies```
```
{
    "movie": {
        "id": 1,
        "release_date": "Fri, 20 Oct 2017 00:00:00 GMT",
        "title": "Movie 1"
    },
    "success": true
}
```

#### POST '/actors'
- General:
    - Add a new actor. The new movie must have all four information. 
    - Role Authorized: Director, Producer
- Example: ```curl -X POST - H '{"Content-Type: application/json", "Authorization: Bearer <TOKEN>}' -d '{"name": "John Doe", "age": 24, "gender": "M", "movie_id": 1}' http://127.0.0.1:5000/actors```

```
{
    "actor": {
        "age": 24,
        "gender": "M",
        "id": 11,
        "movie_id": 1,
        "name": "John Doe"
    },
    "success": true
}
```

#### PATCH '/movies/<int:id>'
- General:
    - Update some information of a movie based on a payload.
    - Roles authorized : Director, Producer.
- Example: ```curl http://127.0.0.1:5000/movies/3 -X PATCH -H '{"Content-Type: application/json", "Authorization: Bearer <TOKEN>}' -d '{ "title": "", "release_date": "2020-11-01" }'```
```
{
  "movie": {
    "id": 3,
    "release_date": "Sun, 01 NOV 2020 00:00:00 GMT",
    "title": "The Great Gatsby"
  },
  "success": true
}
```

#### PATCH '/actors/<int:id>'
- General:
    - Update some information of an actor based on a payload.
    - Roles authorized : Director, Producer.
- Example: ```curl -X PATCH - H '{"Content-Type: application/json", "Authorization: Bearer <TOKEN>}' -d '{"name": "", "age": 88, "": "M", "movie_id": }' http://127.0.0.1:5000/actors/3```
```
{
  "actor": {"age": 88,
    "gender": "M",
    "id": 3,
    "movie_id": 3,
    "name": "Leonardo DiCaprio"
  }, 
  "success": true
}
```

#### DELETE '/movis/<int:id>'
- General:
    - Deletes a movie by id form the url parameter.
    - Roles authorized : Executive Producer.
- Example: ```curl -H '{"Content-Type: application/json", "Authorization: Bearer <TOKEN>}' -X DELETE http://127.0.0.1:5000/movies/2```
```
{
  "success": true, 
  "delete": 2
}
```

#### DELETE '/actors/<int:id>'
- General:
    - Deletes a movie by id form the url parameter.
    - Roles authorized : Casting Director, Executive Producer.
- Example: ```curl -H '{"Content-Type: application/json", "Authorization: Bearer <TOKEN>}' -X DELETE http://127.0.0.1:5000/actors/2```
```
{
    "success": "True",
    "deleted": 2
}
```

### Error Handling
Errors are returned in the following json format:
```
{
    'success': False,
    'error': 404,
    'message': 'Resource not found. Input out of range.'
}
```
The API returns 6 types of errors:
- 400: bad request
- 404: not found
- 403: forbidden
- 422: unprocessable
- 500: internal server error
- AuthError: which mainly results in 401 (unauthorized)

## Deployed Project Tokens

Assistant:
```
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6InlVYnJBUUdVZzNwVnBsbHJUeURZUyJ9.eyJpc3MiOiJodHRwczovL2Rldi0xOHBnaHo1cjBwbWZuMXBmLnVzLmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw2NTA4OTM5OTZlYTgyNWVmNGY1ZDhiNzgiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNjk2MDAyMDgwLCJleHAiOjE2OTYwODg0ODAsImF6cCI6IlBHOUh1cTd6UFBOemNHN1pqUm9KTVY4OW5GVERBaEoyIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJnZXQ6YWN0b3JzIiwiZ2V0Om1vdmllcyJdfQ.m4IAOD6bVbWswFpNvm9f3FAmyJT78PUUKZxNEESKCNYI4xoCAM9wngffdrrEFR1lhXy4B1q_AJc_8rYWvxVXp6xqDwJA_7QOTXQ3XvflOcXOqxbBIGYz-tf1eVh6JSuXSAtFdVUDDHcN3RhDII1tcy1iHFVjQn5iNSwYCHd6H9tGx_Io1tJtHySoAMnfYgGcKp53koQIxPXqi_UkxvEDAmw9OpJ_nQD6CnLAOhhjCgIGXDm71jbNM1ZxoTQ_-3cs5SoZpKDmJ8WwTWuochnjNm1q-xtGljSpHN4FEPnbQqUJf4PCve3J91mBDku0tSUhgVBaZYUiTshi2_rk6i_UjA
```

Producer:
```
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6InlVYnJBUUdVZzNwVnBsbHJUeURZUyJ9.eyJpc3MiOiJodHRwczovL2Rldi0xOHBnaHo1cjBwbWZuMXBmLnVzLmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw2NTAwMmE4N2M3MDJhZTBmNDkzYmVlNDgiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNjk2MDAyMDQyLCJleHAiOjE2OTYwODg0NDIsImF6cCI6IlBHOUh1cTd6UFBOemNHN1pqUm9KTVY4OW5GVERBaEoyIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6YWN0b3JzIiwiZ2V0OmFjdG9ycyIsImdldDptb3ZpZXMiLCJwYXRjaDphY3RvcnMiLCJwYXRjaDptb3ZpZXMiLCJwb3N0OmFjdG9ycyJdfQ.Nw1gsB_A6BU2reWKjlrwcUHDecTYQQzc6G2X4fOkXbfO8o-xTGAfZg4b1TPYKhV2kg8QJIjM-qB3zMRvdPv2RAk3ErP9snAyn_CnrfuG1_JtHzxwhafk-3UcBYkAvazb0HITb-dIlDC9WZ-s8oADE4hfD-DNjJm7qHsLM-g7vGdSXmtwvfF5rNAgnOvUl_SRbuWTAqA1Rj1DNLY3hM0VfgEtA8gEWpIy27y1qz2YnmTMVAfnq_qzy37K63mGTcDj2WlM2JkAYwoPZL2D_HLihL7fkXJ37ezB4DHQvCjl63dBQfNyeICctsEDt-AsCU9fKnuzQcQoZUBkQDWBkIangA
```

Director:
```
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6InlVYnJBUUdVZzNwVnBsbHJUeURZUyJ9.eyJpc3MiOiJodHRwczovL2Rldi0xOHBnaHo1cjBwbWZuMXBmLnVzLmF1dGgwLmNvbS8iLCJzdWIiOiJhdXRoMHw2NTE1N2VkMTk3NDVkOWM2M2MyNjI2NGEiLCJhdWQiOiJjYXN0aW5nIiwiaWF0IjoxNjk1OTk5Mzk1LCJleHAiOjE2OTYwODU3OTUsImF6cCI6IlBHOUh1cTd6UFBOemNHN1pqUm9KTVY4OW5GVERBaEoyIiwic2NvcGUiOiIiLCJwZXJtaXNzaW9ucyI6WyJkZWxldGU6YWN0b3JzIiwiZGVsZXRlOm1vdmllcyIsImdldDphY3RvcnMiLCJnZXQ6bW92aWVzIiwicGF0Y2g6YWN0b3JzIiwicGF0Y2g6bW92aWVzIiwicG9zdDphY3RvcnMiLCJwb3N0Om1vdmllcyJdfQ.oWgxeZNMB3DQvuZQ3Njogi0r7gFlRFU0xh93x1HPd-LMHogXhKVqNrCo3sbmrRjwkO8vF7dlkq-ZjYoSoc5-9_JU0nkPW-5JfHPGAr9BW9So65ODiIW-ZOG0RQYuVx0zyHguc0DjddbE9zaY3OHaq-AyIBWJnFcXA1TNVFgNx1ei91jmHRc4e0FfOlpU5q2xX1zWwoWyrlJJaJlNQYoMljZCABTVA802KyHCHy8jzu-56gqjEnmGS0gl2D_uNXyyPF_YGhXZW4MvF_b6igZ3je-Z5yQvYWuNVCoKZI5WQsQXzZC6uR63k2IFnuQWYUj3PTKX1SrKmDPIEk6SOLEXzQ
```