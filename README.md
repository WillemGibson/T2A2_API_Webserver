# T2A2 - Anime Management API - Willem Gibson

[Project Github Repository](https://github.com/WillemGibson/API_Webserver_Animanage) [Has installation, hardware requirements, etc.]

[Trello Board](https://trello.com/b/xFlzBtlj/t2a2trello)

## Problem Identification

> Identification of the problem you are trying to solve by building this particular app

The problem? simple. Currently, there are no great anime management web applications out there, this API is here is fix that. The current market just consists of 'My Anime List' and 'AniList' which are terrible for any customization or personalization of reviews. I found this when trying to use them. So I decided to make my own which is custom to how I like to review the anime I consume.

## Problem Significance

> Why is it a problem that needs solving?

The importance of this project is significant to me as I consume a decent amount of anime and, just like I book the books I read, I like to review them to later look back on or to easily have an accessible opinion on one if needed. For me, I wanted a solution custom to my tastes and procedure of reviewing anime and felt that building one was the only option. I will continue to use this project in my daily life.

## Database System Selection

> Why have you chosen this database system? What are the drawbacks compared to others?

PostgreSQL was my choice of database system. The platform, Although one of the oldest, is one of the most advanced systems to date, allowing users to how full control over their data. The beauty of PostgreSQL lies in its devoted community. This community is responsible for not only the expansion of the product but also the maintenance of it. A big reason for my choice was the ability to use PostgreSQL on either Windows, Linux, or Mac, allowing the choice of swapping from my different devices at ease.

Now, just because I chose this platform, doesn't necessarily mean it is perfect, it has its disadvantages. Such as it only works for relational databases, and PostgreSQL doesn't support the use of other forms of DBs. Also, it is reported to be significantly slower in performance, in certain circumstances. And, for better or worse as I mentioned, it is open source. This means the code has been slapped together by thousands of different devs which can once again affect performance especially. This is compared to company-backed alternatives with centralized and specialized code.

## ORM Functionalities & Benefits

> Identify and discuss the key functionalities and benefits of an ORM

Object Relational Mapping or ORM for short is a model used to "bridge" object-oriented code into a relational database, in this instance, python to PostgreSQL. The ORM acts as a layer between your coding language and database, helping them communicate with each other. In this specific project I used Marshmellow, an ORM framework specifically designed with Python in mind.

ORMs such as Marshmellow, Django, Apache, etc. help programmers speed up development time exceptionally and help make the transition between front-end development and back-end development seamless. It is also a lifesaver in the security department, the tools are built to eliminate the possibility of SQL injection attacks. And, of course, it allows the developer to require less code in interacting with the database, instead of lines and lines of SQL code that you'll most likely have to repeat over and over, and ORM allows seamless DRY (Don't Repeat Yourself) code in the form of models.

## Endpoints

> Document all endpoints for your API

### User Endpoints

#### **`/auth/register (Method = POST)`**

> Creating a new account

This endpoint is used to create and inject a new user into the 'users' table of the database.

Required Attributes:

- `username` = (`str`) chosen username to identify a user
- `password` = (`str` HASHED using bcrypt) used to secure account
- `is_admin` = (`boolean`) determines if a user is an admin or not

*JSON Injection:*

```json
    {
        "username": "user1",
        "pasword": "password",
        "is_admin": False
    }
```

#### **`/auth/login (Method = POST)`**

> Log into an account

This endpoint is used to authenticate and access a user in the 'users' table of the database.

Required Attributes:

- `username` = (`str`) chosen username to identify a user
- `password` = (`str` HASHED using bcrypt) used to secure account

*JSON Injection:*

```json 
    {
        "username": "user1",
        "pasword": "password"
    }
```

### Review Endpoints

#### **`/reviews (Method = POST)`**

> Creating a review

This endpoint is used to create and inject a new review into the 'reviews' table of the database.

Required Attributes:

- `title` = (`str`) title of the anime the user is reviewing
- `status_id` = (`int`) links to the 'status' table to supply the current status of the anime
- `type_id` = (`int`) links to the 'type' table to supply the current type of the anime
- `rating_id` = (`int`) links to the 'rating' table to supply the rating status of the anime
- `eps_watched` = (`int`) input of the number of episodes watched of the anime by the user
- `eps_total` = (`int`) input of the number of episodes in total of the anime by the user
- `date_started` = (`date`) input of the date in which the user started the anime
- `date_finished` = (`date`) input of the date on which the user completed the anime
- `recom` = (`Boolean`) whether or not the user was recommended the anime
- `fav` = (`Boolean`) whether or not the anime is a favorite of the user
= `com` = (`str`) any comments about the anime by the user

*JSON Injection:*

```json
    {
        "title": "Anime 1",
        "status_id": 3,
        "type_id": 1,
        "rating_id": 4,
        "eps_watched": 12,
        "eps_total": 24,
        "date_started": "2020-03-13",
        "date_finished": "2020-05-10",
        "recom": false,
        "fav": true,
        "com": null
    }
```

#### **`/reviews/<int:review_id> (Method = UPDATE)`**

> Editing/changing a review

This endpoint is used to edit or change a review in the 'reviews' table of the database.

Changeable Attributes:

- `title` = (`str`) title of the anime the user is reviewing
- `status_id` = (`int`) links to the 'status' table to supply the current status of the anime
- `type_id` = (`int`) links to the 'type' table to supply the current type of the anime
- `rating_id` = (`int`) links to the 'rating' table to supply the rating status of the anime
- `eps_watched` = (`int`) input of the number of episodes watched of the anime by the user
- `eps_total` = (`int`) input of the number of episodes in total of the anime by the user
- `date_started` = (`date`) input of the date in which the user started the anime
- `date_finished` = (`date`) input of the date on which the user completed the anime
- `recom` = (`Boolean`) whether or not the user was recommended the anime
- `fav` = (`Boolean`) whether or not the anime is a favorite of the user
= `com` = (`str`) any comments about the anime by the user

*JSON Injection:*

```json
    {
        "status_id": 4,
        "eps_total": 22,
        "date_started": "2020-04-07",
        "recom": true,
        "com": "new comment"
    }
```

#### **`/reviews/<int:review_id> (Method = DELETE)`**

> Removing a review

This endpoint is used to remove a review in the 'reviews' table of the database.

*JSON Injection:*

```json
   No JSON Needed
```

#### **`/reviews/<int:review_id> Method = GET`**

> View one review

***This endpoint is protected by a JSON Web Token (JWT).***

This endpoint is used to view one review from the 'reviews' table of the database.

*JSON Output:*

```json
    {
        "id": "1",
        "user": {
            "username": "user1"
        },
        "title": "Anime 1",
        "status": {
            "status": "Completed"
        },
        "type": {
            "type": "Series"
        },
        "rating": {
            "rating": "5 Star"
        },
        "genres": [
            {
                "id": 12,
                "genre": "Thriller"
            }
        ],
        "eps_watched" 12,
        "eps_total" 12,
        "date_started": "2023-11-23",
        "date_finished": "2023-12-30",
        "recom": false,
        "fav": true,
        "com": "It was pretty good"
    }
```

#### **`/reviews Method = GET`**

> View all reviews

***This endpoint is protected by a JSON Web Token (JWT).***

This endpoint is used to view all reviews from the 'reviews' table of the database.

*JSON Output:*

```json
    [
        {
            "id": "1",
            "user": {
                "username": "user1"
            },
            "title": "Anime 1",
            "status": {
                "status": "Completed"
            },
            "type": {
                "type": "Series"
            },
            "rating": {
                "rating": "5 Star"
            },
            "genres": [
                {
                    "id": 12,
                    "genre": "Thriller"
                }
            ],
            "eps_watched" 12,
            "eps_total" 12,
            "date_started": "2023-11-23",
            "date_finished": "2023-12-30",
            "recom": false,
            "fav": true,
            "com": "It was pretty good"
        },
        {
            "id": "2",
            "user": {
                "username": "user2"
            },
            "title": "Anime 2",
            "status": {
                "status": "Watching"
            },
            "type": {
                "type": "Series"
            },
            "rating": {
                "rating": null
            },
            "genres": [
                {
                    "id": 12,
                    "genre": "Thriller"
                },
                {
                    "id": 3,
                    "genre": "Horror"
                }
            ],
            "eps_watched" 2,
            "eps_total" 24,
            "date_started": "2023-07-03",
            "date_finished": null,
            "recom": true,
            "fav": true,
            "com": null
        },
        {
            "id": "3",
            "user": {
                "username": "user1"
            },
            "title": "Anime 3",
            "status": {
                "status": "Completed"
            },
            "type": {
                "type": "Movie"
            },
            "rating": {
                "rating": "2 Star"
            },
            "genres": [
                {
                    "id": 12,
                    "genre": "Psychological"
                },
                {
                    "id": 1,
                    "genre": "Action"
                },
                {
                    "id": 2,
                    "genre": "Adventure"
                }
            ],
            "eps_watched" 1,
            "eps_total" 1,
            "date_started": "2022-03-27",
            "date_finished": "2022-03-27",
            "recom": true,
            "fav": false,
            "com": "It was alright"
        }
    ]

```

### Genre Linking Endpoints

#### **`/reviews/<int:review_id>/genres/<int:genre_id> (Method = POST)`**

> Link a genre to a review

This endpoint is used to link a genre review in both the 'reviews' table and the 'genres' table with a 'reviews_genre' joining table.

Required Attributes:

- `review_id` = (`int`) chosen review by the user to be linked to the chosen genre by the user
- `genre_id` = (`int`) chosen genre by user to be linked to chosen review by user

*JSON Injection:*

```json
    {
        "review_id": 1,
        "genre_id": 3
    }
```

#### **`/reviews/<int:review_id>/genres/<int:genre_id> (Method = DELETE)`**

> Remove a linked genre from a review

This endpoint is used to remove a linked genre from a review in both the 'reviews' table and the 'genres' table with a 'reviews_genre' joining table.

Required Attributes:

- `review_id` = (`int`) chosen review by the user to be linked to the chosen genre by the user 
- `genre_id` = (`int`) chosen genre by user to be linked to chosen review by user 

*JSON Injection:*

```json
    {
        "review_id": 1,
        "genre_id": 3
    }
```

## Entity Relationship Diagram (ERD)

> An ERD for your app

![Entity Relationship Diagram (ERD)](/Resources/ERD%20Diagram/ERD.png)

## Thrid-Party Services

> Detail any third-party services that your app will use

| Service | Description |
| :--- | ---: |
| Bcrypt | Modern password hashing for your software and your servers |
| Blinker | Fast, simple object-to-object and broadcast signaling |
| Click | Composable command line interface toolkit |
| Flask | A simple framework for building complex web applications. |
| Flask-bcrpyt | Brcrypt hashing for Flask. |
| Flask-JWT-Extended | Extended JWT integration with Flask |
| Flask-marshmallow | Flask + marshmallow for beautiful APIs |
| Flask-SQLAlchemy | Add SQLAlchemy support to your Flask application. |
| itsdangerous | Safely pass data to untrusted environments and back. |
| Jinja2 | A very fast and expressive template engine. |
| MarkupSafe | Safely add untrusted strings to HTML/XML markup. |
| Marshmellow | A lightweight library for converting complex datatypes to and from native Python datatypes. |
| Marshmellow-sqlachemy | SQLAlchemy integration with the marshmallow (de)serialization library |
| Packaging | Core utilities for Python packages |
| Psycopg2-binary | psycopg2 - Python-PostgreSQL Database Adapter |
| PyJWT | JSON Web Token implementation in Python |
| Python-dotenv | Read key-value pairs from a .env file and set them as environment variables |
| SQLAlchemy | Database Abstraction Library |
| Typing_extentions | Backported and Experimental Type Hints for Python 3.8+ |
| Werkzeug | The comprehensive WSGI web application library. |

## Model Relationships

> Describe your project models in terms of the relationships they have with each other

### User Model

- The User model is used to represent a user in the API.
- The user has a one-to-many relationship with reviews, meaning a user can have as many reviews as possible, but reviews can only have one user.
- The user has a cascading function, meaning if a user is deleted so are all their reviews.
- The user model has nested fields for their reviews.

### Review Model

- The review model is used to represent a review in the API.
- A review has many one-to-many relationships with users, status, type, and rating. And also has a many-to-many relationship with genres with a join table with the name of reviews_genres
- A review does not have a cascading function, as we don't want any of the following to be deleted if a review is deleted: users, status, type, rating, and genre.
- A review has nested fields for users, status, type, and rating. With a nested field within a nested list for the genres for the join table.

### Status Model

- The status model is used to represent the status of a review in the API.
- A status has a one-to-many relationship with a review as a review can have only one status, but a status can have as many reviews as possible.
- Status should never be deleted.
- There are no nest fields.

### Type Model

- The type model is used to represent a type of review in the API.
- A type has a one-to-many relationship with a review as a review can have only one type, but a type can have as many reviews as possible.
- Types should never be deleted.
- There are no nest fields.

### Rating Model

- The rating model is used to represent a rating of a review in the API.
- A rating has a one-to-many relationship with a review as a review can have only one rating, but a rating can have as many reviews as possible.
- Ratings should never be deleted.
- There are no nest fields.

### Genre Model

- The genre model is used to represent a genre of a review in the API.
- A genre has a one-to-many relationship with the review_genres entity
- genres should never be deleted.
- There is no nested field within a nested list for the reviews for the join table

### Reviews > Genre

- The Reviews > Genre model is used to represent a joining table between the many-to-many relationship of genres to reviews in the API.
- The Reviews > Genre has a one-to-many relationship with a review and genres to join them together.
- Entity will be deleted once and only once an 'unlink genre' request has been made.
- There are nest fields for both reviews and genres.

## Database Relationships

> Discuss the database relations to be implemented in your application

**The user has a one-to-many relationship with reviews**

- Meaning a user can have as many reviews as possible, but reviews can only have one user.

**A review has many one-to-many relationships with users, status, type, and rating. And a many-to-many relationship with genres utilizing a join table called reviews_genres**

- This means a user can fully review an anime. with all the information needed regardless of the relationship between entities.

**A type has a one-to-many relationship with a review**

- Meaning a review can have only one type, but a type can have as many reviews as possible.

**A rating has a one-to-many relationship with a review** 

- This means a review can have only one rating, but a rating can have as many reviews as possible.

**A genre has a many-to-many relationship with a review**

- Meaning a review can have as many genres as possible and a genre can have as many reviews as possible. This is possible due to the reviews_genres joining table

## Task Allocation

> Describe the way tasks are allocated and tracked in your project

Throughout this project, I leveraged the platform [Trello](https://www.trello.com/) to help my task allocation and time management. Trello is an industry-recognised platform for software development, which one, means it is certainly a great tool to use for the job, and two, will be a good tool to learn as I go into the career. 

Using the Kanban style, I was able to keep this super simple, using carded user stories with checklist due dates for each. This allowed me to easily see everything that was required for each user story and see when it was due with just a glance but also was able to expand the card to see more details if needed. 

Using simple 'To Do', 'Doing', and 'Done' lists, I was able to simply move the tasks to their respective status.

![Entity Relationship Diagram (ERD)](resources/Images/trello_screenshot.png)


## Reference

- Dhruv, S. (2019). Pros and Cons of using PostgreSQL for Application Development. [online] Aalpha. Available at: https://www.aalpha.net/blog/pros-and-cons-of-using-postgresql-for-application-development/.
- freeCodeCamp.org. (2024). freeCodeCamp.org. [online] Available at: https://www.freecodecamp.org/news/ [Accessed 23 Mar. 2024].
- Abba, I.V. (2022). What is an ORM – The Meaning of Object Relational Mapping Database Tools. [online] freeCodeCamp.org. Available at: https://www.freecodecamp.org/news/what-is-an-orm-the-meaning-of-object-relational-mapping-database-tools/.
- marshmallow.readthedocs.io. (n.d.). marshmallow: simplified object serialization — marshmallow 3.17.1 documentation. [online] Available at: https://marshmallow.readthedocs.io/en/stable/.
- developers, T.P.C.A. (n.d.). bcrypt: Modern password hashing for your software and your servers. [online] PyPI. Available at: https://pypi.org/project/bcrypt/.
- Kirtland, J. (n.d.). blinker: Fast, simple object-to-object and broadcast signaling. [online] PyPI. Available at: https://pypi.org/project/blinker/ [Accessed 23 Mar. 2024].
- PyPI. (n.d.). click: Composable command line interface toolkit. [online] Available at: https://pypi.org/project/click/ [Accessed 23 Mar. 2024].
- Ronacher, A. (n.d.). Flask: A simple framework for building complex web applications. [online] PyPI. Available at: https://pypi.org/project/Flask/.
- Countryman, M. (n.d.). Flask-Bcrypt: Brcrypt hashing for Flask. [online] PyPI. Available at: https://pypi.org/project/Flask-Bcrypt/.
- Gilbert, L.A. (n.d.). Flask-JWT-Extended: Extended JWT integration with Flask. [online] PyPI. Available at: https://pypi.org/project/Flask-JWT-Extended/.
- PyPI. (n.d.). flask-marshmallow: Flask + marshmallow for beautiful APIs. [online] Available at: https://pypi.org/project/flask-marshmallow/ [Accessed 23 Mar. 2024].
- Ronacher, A. (n.d.). Flask-SQLAlchemy: Adds SQLAlchemy support to your Flask application. [online] PyPI. Available at: https://pypi.org/project/Flask-SQLAlchemy/.
- Ronacher, A. (n.d.). itsdangerous: Safely pass data to untrusted environments and back. [online] PyPI. Available at: https://pypi.org/project/itsdangerous/ [Accessed 23 Mar. 2024].
- Ronacher, A. (n.d.). Jinja2: A very fast and expressive template engine. [online] PyPI. Available at: https://pypi.org/project/Jinja2/.
- Ronacher, A. (n.d.). MarkupSafe: Safely add untrusted strings to HTML/XML markup. [online] PyPI. Available at: https://pypi.org/project/MarkupSafe/.
- Loria, S. (n.d.). marshmallow: A lightweight library for converting complex datatypes to and from native Python datatypes. [online] PyPI. Available at: https://pypi.org/project/marshmallow/ [Accessed 23 Mar. 2024].
- PyPI. (n.d.). marshmallow-sqlalchemy: SQLAlchemy integration with the marshmallow (de)serialization library. [online] Available at: https://pypi.org/project/marshmallow-sqlalchemy/ [Accessed 23 Mar. 2024].
- Stufft, D. (n.d.). packaging: Core utilities for Python packages. [online] PyPI. Available at: https://pypi.org/project/packaging/ [Accessed 23 Mar. 2024].
- Gregorio, F.D. (n.d.). psycopg2-binary: psycopg2 - Python-PostgreSQL Database Adapter. [online] PyPI. Available at: https://pypi.org/project/psycopg2-binary/.
- Padilla, J. (n.d.). PyJWT: JSON Web Token implementation in Python. [online] PyPI. Available at: https://pypi.org/project/PyJWT/.
- Kumar, S. (n.d.). python-dotenv: Add .env support to your django/flask apps in development and deployments. [online] PyPI. Available at: https://pypi.org/project/python-dotenv/.
- Bayer, M. (n.d.). SQLAlchemy: Database Abstraction Library. [online] PyPI. Available at: https://pypi.org/project/SQLAlchemy/.
- Lee, G. van R., Jukka Lehtosalo, Łukasz Langa, Michael (n.d.). typing-extensions: Backported and Experimental Type Hints for Python 3.8+. [online] PyPI. Available at: https://pypi.org/project/typing-extensions/.
- Ronacher, A. (n.d.). Werkzeug: The comprehensive WSGI web application library. [online] PyPI. Available at: https://pypi.org/project/Werkzeug/