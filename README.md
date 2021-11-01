# Posts-API

### API documentation:

- You can check the detailed documentation using Postman [here](https://www.getpostman.com/collections/2f30e34c1308da19d822)

### List all posts
```
GET https://vast-chamber-06347.herokuapp.com/api/posts
```
- return an object containing the following fields:
  * current_page
  * total_number_of_posts
  * number_of_pages
  * posts
  
- posts field is an array of posts, where each post contains a post object and a user object.

  * the post object contains the following fields:
    * id: the post id
    * title : post title
    * body: content of the post
    * image: url of the post
    * created_at: date of creation of the post
    * updated_at: date of last update of the post
    * user_id: id of the user who created it

  * the user object contains the following fields:
    * id: the id of the user
    * username: the username of the user

- response sample:

```json
{
    "current_page": 1,
    "total_number_of_posts": 3,
    "number_of_pages": 1,
    "posts": [
        {
            "post": {
                "id": 5,
                "title": "New Post !!!!!",
                "body": "i love sleep, very very very very very very much !!",
                "image": "https://www.thepoke.co.uk/wp-content/uploads/2014/08/q8DUn04.png",
                "created_at": "2021-01-06T11:25:09.673Z",
                "updated_at": "2021-01-06T11:25:09.673Z",
                "user_id": 2
            },
            "user": {
                "id": 2,
                "username": "Adnen"
            }
        },
        {
            "post": {
                "id": 2,
                "title": "Serious Post 7777",
                "body": "i love fish, very very very very very very much !!",
                "image": "https://www.thepoke.co.uk/wp-content/uploads/2014/08/q8DUn04.png",
                "created_at": "2021-01-05T19:59:37.548Z",
                "updated_at": "2021-01-06T14:10:44.395Z",
                "user_id": 1
            },
            "user": {
                "id": 1,
                "username": null
            }
        }
    ]
}
```

---

### Create a post
```
POST https://vast-chamber-06347.herokuapp.com/api/posts
```
returns the created post with status 201 on success,

- you should include these fields in the body of the request:

  * title : post title
  * body: content of the post
  * image: url of the post
  
- you should provide the authorization token inside the headers:

```
Authorization: "Bearer xxxx.xxx.xxx"
```

- response sample:
```json
{
    "id": 69,
    "title": "3d modeling",
    "body": " character in blender",
    "image": "https://e6r6h4f7.stackpathcdn.com/wp-content/uploads/2019/08/3D-Modeling-1-1024x683.jpg",
    "created_at": "2020-12-22T20:47:56.900Z",
    "updated_at": "2020-12-22T20:47:56.900Z",
    "user_id": 22
}
```

---

### Get one post by id
```
GET https://vast-chamber-06347.herokuapp.com/api/posts/<post_id>
```
returns one post object containing:
- the field "post" in which is:
  * id: the post id
  * title : post title
  * body: content of the post
  * image: url of the post
  * created_at: date of creation of the post
  * updated_at: date of last update of the post
  * user_id: id of the user who created it (it's your id)
  * comments: an array of comments published by the user related to that post
  
- a comment contains:
  
  * id: the comment id
  * post_id : post id of the comment
  * name: title of the comment
  * text: content of the comment
  * created_at: date of creation of the post
  * updated_at: date of last update of the post
  
```json
{
    "post": {
        "id": 69,
        "title": "3d modeling",
        "body": " character in blender",
        "image": "https://e6r6h4f7.stackpathcdn.com/wp-content/uploads/2019/08/3D-Modeling-1-1024x683.jpg",
        "created_at": "2020-12-22T20:47:56.900Z",
        "updated_at": "2020-12-22T20:47:56.900Z",
        "user_id": 22
    },
    "comments": [
        {
          "id": 1,
          "post_id": 414,
          "name": "comment 1",
          "text": "comment body!!!",
          "created_at": "2020-12-23T20:07:45.066Z",
          "updated_at": "2020-12-23T20:07:45.066Z"
        }
     ]
}
```

---

### Register

```
POST https://vast-chamber-06347.herokuapp.com/api/signup
```

- you should include these fields in the body of the request:

an object having a user object inside it,
inside which you have:
  * email: the user's new email
  * password: the password of the user
  * username: the user's displayed name
  * image: the user's avatar
  
- request example:
```json
{
	"user": {
		"email": "adnba3@adnba3.com",
		"password": "abcdefg",
		"username": "Adnen 3",
		"image": "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSIltE7CNXgJ95jKIkczNnzcVEbiox9t0c-sg&usqp=CAU"
	}
}
```

- response sample:
```json
{
  "id": 1,
  "post_id": 414,
  "name": "comment 1",
  "text": "comment body!!!",
  "created_at": "2020-12-23T20:07:45.066Z",
  "updated_at": "2020-12-23T20:07:45.066Z"
}
```

- it will return the created user as an object in the response but you should care about the header instead
in which you will find your token

- in the Authorization header of your response

---

### Login

```
POST https://vast-chamber-06347.herokuapp.com/api/login
```

- you should include these fields in the body of the request:

an object having a user object inside it,
inside which you have:
  * email: the user's new email
  * password: the password of the user
  
- request example:
```json
{
	"user": {
		"email": "adnba3@adnba3.com",
		"password": "abcdefg"
	}
}
```

- response sample:
```json
{
  "id": 1,
  "post_id": 414,
  "name": "comment 1",
  "text": "comment body!!!",
  "created_at": "2020-12-23T20:07:45.066Z",
  "updated_at": "2020-12-23T20:07:45.066Z"
}
```

- it will return the user logged in as an object in the response but you should care about the header instead
in which you will find your token

- in the Authorization header of your response

---

### Profile page
```
GET https://vast-chamber-06347.herokuapp.com/api/profile
```

- posts field is an array of posts, where each post contains a post object and a user object.
returns one object containing a Posts array and a User object:
- the Posts array contains objects where each one is an object with the following fields:
  * id: the post id
  * title : post title
  * body: content of the post
  * image: url of the post
  * created_at: date of creation of the post
  * updated_at: date of last update of the post
  * user_id: id of the user who created it (it's your id)
  * comments: an array of comments published by the user related to that post

- the User object contains the following fields:
  * id: the id of the user
  * username: the user's displayed name
  * email: the user's new email
  * created_at: date of creation of the user
  * updated_at: date of last update of the user
  * image: the user's avatar

```json
{
    "User": {
        "id": 1,
        "username": null,
        "created_at": "2021-01-05T18:21:26.376Z",
        "updated_at": "2021-01-05T18:21:26.376Z",
        "email": "adnba@adnba.com",
        "jti": "73144588-0417-448a-b5b0-1c4dd24f880b",
        "image": "https://i.stack.imgur.com/l60Hf.png"
    },
    "Posts": [
        {
            "id": 2,
            "title": "Serious Post 7777",
            "body": "i love fish, very very very very very very much !!",
            "image": "https://www.thepoke.co.uk/wp-content/uploads/2014/08/q8DUn04.png",
            "created_at": "2021-01-05T19:59:37.548Z",
            "updated_at": "2021-01-06T14:10:44.395Z",
            "user_id": 1
        },
        {
            "id": 1,
            "title": "Serious Post",
            "body": "i love fish, very very very very very very much !!",
            "image": "https://www.thepoke.co.uk/wp-content/uploads/2014/08/q8DUn04.png",
            "created_at": "2021-01-05T18:34:24.576Z",
            "updated_at": "2021-01-05T18:34:24.576Z",
            "user_id": 1
        }
    ]
}
```

---

### Modify a post
```
PUT https://vast-chamber-06347.herokuapp.com/api/posts/<post-id>
```
returns the updated post with status 200 on success,

- you should include _one of_ these fields in the body of the request:

  * title : post title
  * body: content of the post
  * image: url of the post
  
- you should add the authorization token in the headers

- response sample:
```json
{
    "id": 69,
    "title": "3d modeling",
    "body": " character in blender",
    "image": "https://e6r6h4f7.stackpathcdn.com/wp-content/uploads/2019/08/3D-Modeling-1-1024x683.jpg",
    "created_at": "2020-12-22T20:47:56.900Z",
    "updated_at": "2020-12-22T20:47:56.900Z",
    "user_id": 22
}
```

---

### Delete a post
```
DELETE https://vast-chamber-06347.herokuapp.com/api/posts/<post-id>
```
returns an empty response with status 204 on success

- you should add the authorization token in the headers

---

## Comments

### List comments of a post:

#### Option 1: by getting a post by id
- by getting a post by ID you get the comments array in the fields

```
GET https://vast-chamber-06347.herokuapp.com/api/posts/{post_id}
```

#### Option 2: by getting the comments only

- but you can use this endpoint if you want the comments array only

```
 GET https://vast-chamber-06347.herokuapp.com/api/posts/{post_id}/comments
 ```
 
 - response sample:
 
 ```json
[
   {
     "id": 1,
     "post_id": 414,
     "name": "comment 1",
     "text": "comment body!!!",
     "created_at": "2020-12-23T20:07:45.066Z",
     "updated_at": "2020-12-23T20:07:45.066Z"
   }
]
 ```
 
 ---

### Create a comment

```
POST https://vast-chamber-06347.herokuapp.com/api/posts/{post_id}/comments
```

- you should include these fields in the body of the request:

  * name: title of the comment
  * text: content of the comment
  
- you should add the authorization token in the headers

- response sample:
```json
{
  "id": 1,
  "post_id": 414,
  "name": "comment 1",
  "text": "comment body!!!",
  "created_at": "2020-12-23T20:07:45.066Z",
  "updated_at": "2020-12-23T20:07:45.066Z"
}
```

---

### Update a comment

- modify a comment related to a post

```
PUT https://vast-chamber-06347.herokuapp.com/api/posts/{post_id}/comments/{comment_id}
```

- you should include _one of_ these fields in the body of the request:

  * name: title of the comment
  * text: content of the comment

- you should add the authorization token in the headers

---

### Delete a comment

- delete a comment related to a post

```
DELETE https://vast-chamber-06347.herokuapp.com/api/posts/{post_id}/comments/{comment_id}
```

- you should add the authorization token in the headers

---

### Search a post

```
GET https://vast-chamber-06347.herokuapp.com/api/posts/search/{search}
```

- returns an array of posts fitting the criteria either in title or in body:

- response sample:

```json
{
