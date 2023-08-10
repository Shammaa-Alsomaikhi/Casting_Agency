### API Reference

### Getting Started
- Base URL: At present this app can only be run locally and is not hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:5000/`, which is set as a proxy in the frontend configuration. 
- Authentication: This version of the application does not require authentication or API keys. 

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```
The API will return three error types when requests fail:
- 400: Bad Request
- 404: Resource Not Found
- 422: Unprocessable 
- 405: Method not allowed
- 500: Internal Server Error

### Endpoints 
#### GET /movies
- General:
    - Returns a list of movies that contains id, release date, title  
    - Success value
- Sample: `curl -H "Authorization: Bearer <Token>" http://127.0.0.1:5000/movies`

``` {
"movies": [
    {
      "id": 5,
      "release_date": "Wed, 12 Jan 2022 00:00:00 GMT",
      "title": "Gintama"
    },
    {
      "id": 7,
      "release_date": "Sat, 07 Mar 2020 00:00:00 GMT",
      "title": "Gintama the movie"
    }
  ],
  "success": true
}
```
#### GET /actors
- General:
    - Returns a list of actors that contains id, age, gender, movie_id, name 
    - Success value
- Sample: `curl -H "Authorization: Bearer <Token>" http://127.0.0.1:5000/actors`

``` {
    "acorts": [
    {
      "age": 25,
      "gender": "male",
      "id": 4,
      "movie_id": 5,
      "name": "tom holland"
    },
    {
      "age": 58,
      "gender": "male",
      "id": 5,
      "movie_id": 5,
      "name": "Robert doney .jr"
    }
  ],
  "success": true
}
```
#### DELETE /movies/{movie_id}
- General:
    - Deletes the movie of the given ID if it exists. Returns the id of the deleted movie, success value, a confirmation message. 
- `curl -X DELETE http://127.0.0.1:5000/movies/5 -H "Authorization: Bearer <Token>"`
```
{
  "deleted": 5,
  "message": "Movie (Gintama) was successfully deleted",
  "success": true
}
```
#### DELETE /actors/{actor_id}
- General:
    - Deletes the actor of the given ID if it exists. Returns the id of the deleted actor, success value, a confirmation message. 
- `curl -X DELETE http://127.0.0.1:5000/actors/6 -H "Authorization: Bearer <Token>"`
```
{
  "deleted": 6,
  "message": "Actor (Robert doney .jr) was successfully deleted",
  "success": true
}
```
#### POST /movies
- General:
    - Creates a new movie using the submitted title, release date. Returns the id of the created movie, success value, total movies.
- `curl -X POST http://127.0.0.1:5000/movies -H "Content-Type: application/json" -H "Authorization: Bearer <Token>" -d '{"title" : "the batman", "release_date" : "04/03/2022"}'`
```
{
  "created": 9,
  "success": true,
  "total_movies": 3
}
```
#### POST /actors
- General:
    - Creates a new actor using the submitted name, age, gender, movie_id. Returns the id of the created actor, success value, total actors.
- `curl -X POST http://127.0.0.1:5000/actors -H "Content-Type: application/json" -H "Authorization: Bearer <Token>" -d '{"name" : "Robert Pattinson", "age" : "37", "gender":"male", "movie_id":"9"}'`
```
{
  "created": 7,
  "success": true,
  "total_actors": 1
}
```
#### PATCH /movies/{movie_id}
- General:
    - Update the movie of the given ID using the submitted title, release date. Returns the id, relase date, title, success value.
- `curl -X PATCH http://127.0.0.1:5000/movies/7 -H "Content-Type: application/json" -H "Authorization: Bearer <Token>" -d '{"title" : "the batman", "release_date" : "04/03/2022"}'`
```
{
  "movie": [
    {
      "id": 7,
      "release_date": "Sun, 03 Apr 2022 00:00:00 GMT",
      "title": "the batman"
    }
  ],
  "success": true
}
```
#### PATCH /actors/{avtor_id}
- General:
    - Update the actor of the given ID using the submitted name, age, gender, movie_id. Returns the id, relase date, title, success value.
- `curl -X PATCH http://127.0.0.1:5000/actors/7 -H "Content-Type: application/json" -H "Authorization: Bearer <Token>" -d '{"name" : "Robert", "age" : "", "gender" : "", "movie_id": ""}'`
```
{
  "movie": [
    {
      "age": 37,
      "gender": "male",
      "id": 7,
      "movie_id": 9,
      "name": "Robert"
    }
  ],
  "success": true
}
```
