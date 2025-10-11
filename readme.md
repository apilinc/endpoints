**Create Project Using this URL**
```
https://api.codestrail.com/
```
# 🧩 API Data Endpoint Documentation

**Base URL:**  
```
https://api.codestrail.com/project/{projectId}
```

This endpoint allows you to manage your project’s API data — including creating, reading, updating, and deleting records.

---

## 🔒 Authentication
You must include your **API Key** in the request header:

```
x-api-key: YOUR_API_KEY
Content-Type: application/json
```

---

## 📘 Endpoints Overview

| Method | Endpoint | Description |
|--------|-----------|-------------|
| **GET** | `/` | Get all API data records |
| **GET** | `/{id}` | Get a single record by ID |
| **GET** | `/search?field=value&orderby=field+asc&limit=10&page=2` | Filter, sort, and paginate results |
| **POST** | `/` | Create a new record |
| **POST** | `/{id}/uploadfile` | Upload a file associated with a record |
| **PUT** | `/{id}` | Fully update a record |
| **PATCH** | `/{id}` | Partially update specific fields |
| **DELETE** | `/{id}` | Delete a record |

---

## 🟢 1. Get All Records

**Endpoint:**  
```http
GET /{resourceName}
```

**Response:**
```json
{
  "status": true,
  "statusCode": 200,
  "data": [
    {
      "name": "Testing1",
      "email": "testing1@gmail.com",
      "password": "hhhh",
      "role": 1,
      "id": 1,
      "_created_at": "2025-10-09 05:55:29",
      "_updated_at": "2025-10-09 05:55:29"
    },
    {
      "name": "Testing2",
      "email": "testing2@gmail.com",
      "password": "jjjj",
      "role": 0,
      "id": 2,
      "_created_at": "2025-10-09 05:56:14",
      "_updated_at": "2025-10-09 05:56:14"
    }
  ]
}
```

**JavaScript Example:**
```js
fetch('https://api.codestrail.com/project/{projectId}/{resourceName}', {
  method: 'GET',
  headers: { "x-api-key": 'YOUR_API_KEY' }
})
.then(res => res.json())
.then(console.log);
```

---

## 🟢 2. Get Single Record

```http
GET /{resourceName}/{id}
```

**Response:**
```json
{
  "status": true,
  "statusCode": 200,
  "data": {
    "name": "Abdul Qadir",
    "email": "aqadir@gmail.com",
    "password": "hhhh",
    "role": 1,
    "id": 1,
    "_created_at": "2025-10-09 05:55:29",
    "_updated_at": "2025-10-09 05:55:29"
  }
}
```

**Example:**
```js
fetch('https://api.codestrail.com/project/{projectId}/{resourceName}/{id}', {
  method: 'GET',
  headers: { "x-api-key": 'YOUR_API_KEY' }
})
.then(res => res.json())
.then(console.log);
```

---

## 🟢 3. Search & Filter

**Query Parameters:**
| Parameter | Type | Description |
|------------|------|-------------|
| `field name` (e.g., `name`) | any | search record by field name you can use single or multiple |
| `limit` | integer | Limit number of records per page |
| `page` | integer | Specify page number |
| `orderby` | string | Sort by field (e.g., `orderby=name asc`) |


**Supported Operators**

Your API supports a range of filtering operators that make it easy to query and manipulate data efficiently.

| Operator | Full Form / Meaning | Description / Example |
|---------------|--------------------------|-----------------------------|
| **eq** | Equal | Matches values that are **equal** to the specified value.<br>**Example:** `status=eq:active` → returns all records where `status` is `"active"`. |
| **ne** | Not Equal | Matches values that are **not equal** to the specified value.<br>**Example:** `status=ne:active` → excludes records with `status = "active"`. |
| **gt** | Greater Than | Matches values that are **greater than** the given value.<br>**Example:** `age=gt:30` → returns records where `age` > 30. |
| **gte** | Greater Than or Equal | Matches values that are **greater than or equal to** the given value.<br>**Example:** `price=gte:100` → returns records with `price` ≥ 100. |
| **lt** | Less Than | Matches values that are **less than** the given value.<br>**Example:** `age=lt:18` → returns records where `age` < 18. |
| **lte** | Less Than or Equal | Matches values that are **less than or equal to** the given value.<br>**Example:** `price=lte:500` → returns records with `price` ≤ 500. |
| **in** | In List | Matches values that are **present in a given list** of values.<br>**Example:** `status=in:active,pending` → returns records where `status` is either `"active"` or `"pending"`. |
| **contains** | Contains / Substring Match | Matches text fields that **contain** the given substring.<br>**Example:** `name=contains:john` → returns records where `"john"` appears in the `name` field. |

---

### 🔍 Example Usage

You can combine multiple filters in a single API request:

```http
GET /users/search?age=gte:18&status=in:active,pending&name=contains:john

```

**Response:**
```json
{
  "status": true,
  "statusCode": 200,
  "page": 1,
  "limit": 5,
  "total": 30,
  "data": [{ "id": 20, "name": "Order 020", "status": "Pending" }]
}
```

**Example:**
```js
fetch('https://api.codestrail.com/project/{projectId}/{resourceName}/search?status=Pending&orderby=id desc&limit=5&page=1', {
  method: 'GET',
  headers: { "x-api-key": 'YOUR_API_KEY' }
})
.then(res => res.json())
.then(console.log);
```

---

## 🟢 4. Create Record

```http
POST /{resourceName}
```

**Request:**
```json
{
    "name": "Testing3",
    "email": "testing3@gmail.com",
    "password": "hhhh",
    "role": 1
}
```

**Response:**
```json
 {
  "status": true,
  "statusCode": 200,
  "data": {
    "name": "Testing3",
    "email": "testing3@gmail.com",
    "password": "hhhh",
    "role": 1,
    "id": 3
  }
}
```

**JS Example:**
```js
fetch('https://api.codestrail.com/project/{projectId}/{resourceName}', {
  method: 'POST',
  headers: { 'x-api-key': 'YOUR_API_KEY', 'Content-Type': 'application/json' },
  body: JSON.stringify({
    "name": "Testing3",
    "email": "testing3@gmail.com",
    "password": "hhhh",
    "role": 1
})
})
.then(res => res.json())
.then(console.log);
```

---

## 🟢 5. Upload File

```http
POST /{resourceName}/{id}/uploadfile
```

**Form Data:**  
| Field | Type | Description |
|--------|------|-------------|
| `file` | file | The file to upload |

**Response:**
```json
{
  "status": true,
  "statusCode": 200,
  "message": "Uploaded",
  "file": {
    "id": "1",
    "url": "/uploads/68e74ce68b2fa/users/1/1759994380_3.png",
    "type": "image/png",
    "size": 239465
  }
}
```

**Example:**
```js
const formData = new FormData();
formData.append('file', document.querySelector('#fileInput').files[0]);

fetch('https://api.codestrail.com/project/{projectId}/{resourceName}/{id}/uploadfile', {
  method: 'POST',
  headers: { 'x-api-key': 'YOUR_API_KEY' },
  body: formData
})
.then(res => res.json())
.then(console.log);
```

---

## 🟢 6. Update Record

```http
PUT /{resourceName}/{id}
```

**Request:**
```json
{
    "name": "Test3",
    "email": "test3@gmail.com",
    "password": "hhtttthh",
    "role": 0
}
```

**Response:**
```json
 {
  "status": true,
  "statusCode": 200,
  "message": "Updated",
  "data": {
    "name": "Test3",
    "email": "test3@gmail.com",
    "password": "hhtttthh",
    "role": 0,
    "id": 1
  }
}
```

**JS Example:**
```js
fetch('https://api.codestrail.com/project/{projectId}/{resourceName}/{id}', {
  method: 'PUT',
  headers: { 'x-api-key': 'YOUR_API_KEY', 'Content-Type': 'application/json' },
  body: JSON.stringify({
    "name": "Test3",
    "email": "test3@gmail.com",
    "password": "hhtttthh",
    "role": 0
})
})
.then(res => res.json())
.then(console.log);
```

---

## 🟢 7. Partial Update

```http
PATCH /{resourceName}/{id}
```

**Request:**
```json
{
    "password": "hashkjs"
}
```

**Response:**
```json
{
  "status": true,
  "statusCode": 200,
  "message": "Updated",
  "data": {
    "name": "Test3",
    "email": "test3@gmail.com",
    "password": "hashkjs",
    "role": 0,
    "id": 1
  }
}
```

**JS Example:**
```js
fetch('https://api.codestrail.com/project/{projectId}/{resourceName}/{id}', {
  method: 'PATCH',
  headers: { 'x-api-key': 'YOUR_API_KEY', 'Content-Type': 'application/json' },
  body: JSON.stringify({
    "password": "hashkjs"
  })
})
.then(res => res.json())
.then(console.log);
```

---

## 🟢 8. Delete Record

```http
DELETE /{resourceName}/{id}
```

**Response:**
```json
{
  "status": true,
  "statusCode": 200,
  "message": "Deleted"
}
```
**Response:**
```js
fetch('https://api.codestrail.com/project/{projectId}/{resourceName}/{id}', {
  method: 'DELETE',
  headers: { "x-api-key": 'YOUR_API_KEY' }
})
.then(res => res.json())
.then(console.log);
```
---

## ⚙️ HTTP Status Codes

| Code | Meaning |
|------|----------|
| **200** | OK — Successful request |
| **201** | Created — New record created |
| **400** | Bad Request — Invalid data |
| **401** | Unauthorized — Invalid or missing API key |
| **404** | Not Found — Record not found |
| **409** | Conflict — Duplicate resource |
| **500** | Server Error — Something went wrong |

---

## 🧪 Example Headers
```json
{
  "x-api-key": "0d72a35eadd778bd7c5354981dbdb3e1",
  "Content-Type": "application/json"
}
```

---

## 🧾 License
This API Database service is open for testing and educational use.  
Developed by [CodesTrail APIs](https://api.codestrail.com/).  
All rights reserved © 2025.
