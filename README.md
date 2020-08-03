## Introduction

Most of the time as a front end developer, development of a prototype can be stalled due to lack of an actual API. This could be because the back end team maybe taking too much time to develop the endpoint your application is to consume. In this guide, you will learn how to create your own mock endpoints using a local JSON file and how to consume it using your application.
This guide assumes that you have a basic understanding of APIs and at least _beginner_ proficiency in working with JSON files. You should also be familiar with testing APIs with either CURL or Postman.

Suppose you are a budding front end developer at a dev house in your local tech community. 
You need to develop a proof of concept(PoC) of a Payroll System for a potential client. 
The client has only requested to see a page with a list of Employee, fetched from some API. 
To accelerate the development, you decide to develop a mock API.

The mock API endpoint could be `/employees` and the properties for each of the employee will consist of:
1. `id` - number that uniquely identifies the employee
2. `first_name` - the first name of the employee
3. `last_name` - the last name of the employee
4. `email` - the email address of the employee
4. `gender` - the gender of the employee
4. `status` - the status of the employee

## Setup

To create the mock API, you are going to use a tool called JSON server. The tool is designed to help developers spin up REST APIs with CRUD functionalities very quickly.

You can start off by setting up your Node Js project. Create a directory called `json-mock-api`

```bash
mkdir json-mock-api
```

Navigate to your project's root directory. 

```bash
cd json-mock-api
```

Create a `package.json` file. The file is used to define the project's metadata; from name of the project to the dependencies to commands to run tests and start the project. Below is a sample of its contents and paste it into your `package.json` file:

```json
{
  "name": "json-mock-api",
  "version": "1.0.0",
  "description": "A simple JSON mock API",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```

You can then proceed to add the dependency needed to create the mock API, **json-server**. This can be done by running the following command on the project's root directory.

```bash
npm install json-server --save
```

## Creating the mock API

Your mock API will need a source for its data. You can go ahead and create an `src` folder. In the `src` folder, you can then create a `db.json` file. Your file structure should look something like this.

```
json-mock-api/    
    node_modules/
    src/   
    	db.json
    package.json
```

The db.json file will act like your data source. There you will define what data you would want to retrieve from your mock API. Here is where you define the sample employees, and their various details as discussed earlier.
The first property `employees` on the JSON file is used to define the name of the endpoint
. 
```json
{
  "employees": [
    {
      "id": 1,
      "first_name": "John",
      "last_name": "Doe",
      "email": "johndoe@abc.com",
      "gender": "Male",
      "status": "Terminated"
    },
    {
      "id": 2,
      "first_name": "Jane",
      "last_name": "Doe",
      "email": "janedoe@abc.com",
      "gender": "Female",
      "status": "New"
    },
    {
      "id": 3,
      "first_name": "Alice",
      "last_name": "Doe",
      "email": "alicedoe@abc.com",
      "gender": "Female",
      "status": "Leaving"
    },
    {
      "id": 4,
      "first_name": "Bob",
      "last_name": "Doe",
      "email": "bobdoe@abc.com",
       "gender": "Male",
      "status": "Active"
    }
  ]
}
```

To start up your API, run the command below:

```bash
json-server --watch src/db.json
```

You should see be able to see your API running with an endpoint, `http:/localhost:3000/employees`

## Testing the mock API

You can go ahead and test your newly created endpoint on any API testing tool like Postman or CURL. 

To make a GET request for all the employees, run the command below.

```bash
curl http://localhost:3000/employees
```

The response should be as below. Note that it is an array with all the employees.

```json
[
  {
    "id": 1,
    "first_name": "John",
    "last_name": "Doe",
    "email": "johndoe@abc.com",
    "gender": "Male",
    "status": "Terminated"
  },
  {
    "id": 2,
    "first_name": "Jane",
    "last_name": "Doe",
    "email": "janedoe@abc.com",
    "gender": "Female",
    "status": "New"
  },
  {
    "id": 3,
    "first_name": "Alice",
    "last_name": "Doe",
    "email": "alicedoe@abc.com",
    "gender": "Female",
    "status": "Leaving"
  },
  {
    "id": 4,
    "first_name": "Bob",
    "last_name": "Doe",
    "email": "bobdoe@abc.com",
     "gender": "Male",
    "status": "Active"
  }
]
```

To make a GET request for a specific employee, you append the `id` of the employee to the endpoint; `/employees/4`. You can then run the command as below.

```bash
curl http://localhost:3000/employees/4
```

The response should be as below. Note that it is an object with the specific employee details of the employee whose `id` is 4.

```json
{
  "id": 4,
  "first_name": "Bob",
  "last_name": "Doe",
  "email": "bobdoe@abc.com",
  "gender": "Male",
  "status": "Active"
}
```

## Conclusion

Well, there you have it a simple mock API to help accelerate development. In this guide, you only managed to do GET requests. You can also use `json-server` to develop endpoints with other methods like POST, PATCH, DELETE. In addition, you can also add filtering and pagination to your endpoints. Just have a look at the [Json Server Documentation](https://github.com/typicode/json-server)


