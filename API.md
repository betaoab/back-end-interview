# Back-End Exercise - API


## Requirements

For this exercise, we will be building a social link aggregator. At its core, it will be a place where users can submit internet links (URLs), 
and upvote/downvote ("Thumb up"/"Thumb down") each other's Links. The difference between **Upvotes** and **Downvotes**, for each **Link**, is their **Score**. 

A Link is an URL associated with scoring data (upvotes, downvotes, score) and some metadata (created, id). A proposal has been made to represent a Link:

### The Link Object
```json
{
  "id": 1,
  "created": "2022-05-19T13:15:06Z",
  "url": "https://www.google.com/",
  "upvotes": 5,
  "downvotes": 2,
  "score": 3
}
```

Our API will allow clients:
- to **create** new Links by sending a `POST` request with the following data to the `/api/links` endpoint:
  ```json
  {
    "url": "https://www.yahoo.com/"
  }
  ```
  The link should be validated as being a valid URL.
- to **retrieve** all Links submitted, sorted by their Score, by sending a `GET` request to the `/api/links` endpoint.
- to perform **actions** on each Link:
  - **Upvote**, by sending a `POST` request to the `/api/links/{linkId}/upvote` endpoint. This should add 1 to the "upvotes" property for that Link.
  - **Downvote**, by sending a `POST` request to the `/api/links/{linkId}/downvote` endpoint. This should add 1 to the "downvotes" property for that Link.


## Goals
- Bootstrap a new Django 5.x application using the django-admin CLI tool and the [startproject](https://docs.djangoproject.com/en/5.0/ref/django-admin/#startproject) command. Keep the default database set up by django-admin, SQLite.
- Create all the necessary models to support the above requirements
- Write the necessary API endpoints, serializers and routes to support the above requirements, using Django Rest Framework
- Bonus: Write some API tests to check if your endpoints are behaving properly

## Scope
- The submission will run on the latest Python version (3.11 at the moment of writing)
- No authentication or user management is necessary.
- No frontend is necessary.
- No python libraries besides Django and Django Rest Framework are necessary.
- If you are not familiar with Django, any web framework (or none) of your choice will be admitted.
