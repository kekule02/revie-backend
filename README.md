# Project Overview

This project consists of three schemas: **User**, **Review**, and **Apartment**. Below are the details of each schema and the API endpoints for the project.

## Schemas

### User Schema

- `name`: `String`, required, trimmed
- `email`: `String`, required, unique, trimmed, lowercase, validated
- `password`: `String`, required, minimum length: 6 characters
- `timestamps`: auto-generated

### Review Schema

- `apartmentId`: `ObjectId`, references "Apartment"
- `userId`: `ObjectId`, references "User"
- `landlordReviewRating`: `Number`, required, range: 0-5
- `landlordReviewNote`: `String`
- `environmentReviewRating`: `Number`, range: 0-5
- `environmentReviewNote`: `String`
- `amenitiesReviewRating`: `Number`, range: 0-5
- `amenitiesReviewNote`: `String`
- `reviewHelpfulCount`: `Number`, default: 0
- `timestamps`: auto-generated

### Apartment Schema

- `name`: `String`, required
- `address`: `String`, required
- `owner`: `String`, optional

## API Endpoints

### User Endpoints

#### User Sign-Up

- **Endpoint**: `/api/user/sign-up`
- **Method**: `POST`
- **Description**: Registers a new user.
- **Body**:
  ```json
  {
    "name": "John Doe",
    "email": "johndoe@gmail.com",
    "password": "johndoe123!"
  }
  ```
- **Response**:
  ```json
  {
    "user": {
      "name": "John Doe",
      "email": "johndoe@gmail.com",
      "password": "$2b$10$vdjKaZbYq3YXlujckpEutevUEAQ70K1Lag17bDnoFvTbUuz0y1q5m",
      "_id": "66c74d27108a8955abdbe75c",
      "createdAt": "2024-08-22T14:37:27.082Z",
      "updatedAt": "2024-08-22T14:37:27.082Z",
      "__v": 0
    },
    "message": "Sign-up successfully complete!"
  }
  ```

#### User Login

- **Endpoint**: `/api/user/login`
- **Method**: `POST`
- **Description**: Logs in a user with the correct details after it has been authenticated.
- **Body**:
  ```json
  {
    "email": "johndoe@gmail.com",
    "password": "johndoe123!"
  }
  ```
- **Response**:
  ```json
  {
    "message": "Login Successful!",
    "user": {
      "_id": "66c74d27108a8955abdbe75c",
      "name": "Azeez Ajibola",
      "email": "azeezlawal2002@gmail.com",
      "password": "$2b$10$vdjKaZbYq3YXlujckpEutevUEAQ70K1Lag17bDnoFvTbUuz0y1q5m",
      "createdAt": "2024-08-22T14:37:27.082Z",
      "updatedAt": "2024-08-22T14:37:27.082Z",
      "__v": 0
    },
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJfaWQiOiI2NmM3NGQyNzEwOGE4OTU1YWJkYmU3NWMiLCJpYXQiOjE3MjQzMzc0NzUsImV4cCI6MTcyNDM0MTA3NX0.tLhJnpq8A9FClp2z5F6RhtWytwgVMRguYaTrT587Moo"
  }
  ```

### Apartment Endpoints

#### Create Apartment

- **Endpoint**: `/api/apartment/create`
- **Method**: `POST`
- **Description**: Creates a new apartment listing in the system. Requires user authentication.
- **Body**:
  ```json
  {
    "name": "The Ben Street Main House",
    "address": "5, Sokoya Street, Obalende, Lagos State"
  }
  ```
- **Response**:
  ```json
  {
    "name": "The Ben Street Main House",
    "address": "5, Sokoya Street, Obalende, Lagos State",
    "_id": "66c74914549fa93126ad0d7a",
    "__v": 0
  }
  ```

#### Get All Apartments

- **Endpoint**: `/api/apartment/`
- **Method**: `GET`
- **Description**: Retrieves a list of all apartments. Requires user authentication.
- **Response**:
  ```json
  [
    {
      "_id": "66c6506440e80297a69126ca",
      "name": "The John Street Main House",
      "address": "5, Johnson Street, Iwaya, Lagos State",
      "owner": "Segun Basit",
      "__v": 0
    },
    {
      "_id": "66c6509740e80297a69126cd",
      "name": "The Ben Street Main House",
      "address": "5, Sokoya Street, Obalende, Lagos State",
      "__v": 0
    }
  ]
  ```

### Review Endpoints

#### Create Review

- **Endpoint**: `/api/reviews/:id`
- **Method**: `POST`
- **Description**: Creates a new review for a specific apartment. Requires user authentication.
- **Body**:
  ```json
  {
    "landlordReviewRating": 4.5,
    "environmentReviewNote": "Very Good area!"
  }
  ```
- **Response**:
  ```json
  {
    "message": "Review upload complete!",
    "review": {
      "apartmentId": "66c6506440e80297a69126ca",
      "userId": "66c74d27108a8955abdbe75c",
      "landlordReviewRating": 4.5,
      "environmentReviewNote": "Very Good area!",
      "reviewHelpfulCount": 0,
      "_id": "66c74d62108a8955abdbe761",
      "createdAt": "2024-08-22T14:38:26.846Z",
      "updatedAt": "2024-08-22T14:38:26.846Z",
      "__v": 0
    }
  }
  ```

#### Update Review

- **Endpoint**: `/api/reviews/:id`
- **Method**: `PATCH`
- **Description**: Updates an existing review by ID. Requires user authentication.
- **Body**:
  ```json
  {
    "amenitiesReviewRating": 4.5,
    "amenitiesReviewNote": "24/7 electricity. Perfect!!"
  }
  ```
- **Response**: After sending the "amenitiesReviewRating" and "amenitiesReviewNote" fields as the request body, below is the updated review response:
  ```json
  {
    "_id": "66c74d62108a8955abdbe761",
    "apartmentId": "66c6506440e80297a69126ca",
    "userId": "66c74d27108a8955abdbe75c",
    "landlordReviewRating": 4.5,
    "environmentReviewNote": "Very Good area!",
    "reviewHelpfulCount": 0,
    "createdAt": "2024-08-22T14:38:26.846Z",
    "updatedAt": "2024-08-22T14:39:35.450Z",
    "__v": 0,
    "amenitiesReviewNote": "24/7 electricity. Perfect!!",
    "amenitiesReviewRating": 4.5
  }
  ```

#### Increase Most Helpful Count

- **Endpoint**: `PATCH /:id/upvote`
- **Method**: `PATCH`
- **Description**: Increases the "Most Helpful" count for a review. Requires user authentication.
- **Response**:
  ```json
  {
    "message": "Done!"
  }
  ```

#### Get All Reviews for a Specific Apartment

- **Endpoint**: `/api/reviews/:id`
- **Method**: `GET`
- **Description**: Retrieves all the reviews for a specific apartment and sorts them by the recently created by default. Passing the qeury param below sorts by "reviewHelpfulCount" value in descending order. Requires user authentication.
- **Query**: `sortBy = "mostHelpful"`
- **Response**:
  ```json
  [
    {
      "_id": "66c74d62108a8955abdbe761",
      "apartmentId": "66c6506440e80297a69126ca",
      "userId": "66c74d27108a8955abdbe75c",
      "landlordReviewRating": 4.5,
      "environmentReviewNote": "Very Good area!",
      "reviewHelpfulCount": 15,
      "createdAt": "2024-08-22T14:38:26.846Z",
      "updatedAt": "2024-08-22T14:41:43.588Z",
      "__v": 0,
      "amenitiesReviewNote": "24/7 electricity. Perfect!!",
      "amenitiesReviewRating": 4.5
    },
    {
      "_id": "66c68c32b62b0031c3cf5f32",
      "apartmentId": "66c6506440e80297a69126ca",
      "userId": "66c6451864915ae175641ee6",
      "landlordReviewRating": 4.5,
      "environmentReviewNote": "After moving in did I find out that the area is a bit noisy. If you're okay with all the noise, then I think it is fine if you want to move in",
      "reviewHelpfulCount": 4,
      "createdAt": "2024-08-22T00:54:10.240Z",
      "updatedAt": "2024-08-22T09:18:25.869Z",
      "__v": 0,
      "amenitiesReviewNote": "Electricity in the area is not the best",
      "amenitiesReviewRating": 3.5
    }
  ]
  ```
