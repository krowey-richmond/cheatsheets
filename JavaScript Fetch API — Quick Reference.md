# JavaScript Fetch API — Quick Reference

## 1. What is `fetch()`?

`fetch()` is JavaScript's built-in way of making HTTP requests to APIs and servers.

Basic syntax:

```js
fetch("API_URL");
```

By default, `fetch()` makes a **GET request**.

Example:

```js
fetch("https://api.adviceslip.com/advice");
```

---

# 2. The Basic Fetch Pattern

The most common pattern when working with an API is:

```js
async function getData() {
    const response = await fetch("API_URL");

    const data = await response.json();

    console.log(data);
}

getData();
```

Think of the process as:

```text
fetch(URL)
    ↓
HTTP Response
    ↓
response.json()
    ↓
JavaScript object
    ↓
console.log(data)
```

---

# 3. `response` vs `data`

This is one of the most important things to understand.

If you do:

```js
const response = await fetch(url);

console.log(response);
```

You are **NOT logging the actual API data**.

You are logging the HTTP `Response` object.

It contains information such as:

```text
Response
├── status
├── ok
├── headers
├── url
├── body
└── ...
```

For example:

```js
console.log(response.status);
```

might give:

```text
200
```

And:

```js
console.log(response.ok);
```

might give:

```text
true
```

---

# 4. Getting the Actual API Data

The actual data is inside the response body.

For JSON APIs, use:

```js
const data = await response.json();
```

Then:

```js
console.log(data);
```

Example:

```js
async function getAdvice() {
    const response = await fetch(
        "https://api.adviceslip.com/advice"
    );

    const data = await response.json();

    console.log(data);
}

getAdvice();
```

The console will show something similar to:

```js
{
    slip: {
        id: 42,
        advice: "Some piece of advice..."
    }
}
```

The exact values will change because the API returns different advice.

---

# 5. How to Discover an API's Data Structure

You do NOT always need to memorize or guess the response structure.

When using an unfamiliar API:

### Step 1 — Find the endpoint

Example:

```text
https://api.adviceslip.com/advice
```

### Step 2 — Fetch it

```js
const response = await fetch(url);
```

### Step 3 — Convert the response to JSON

```js
const data = await response.json();
```

### Step 4 — Log the data

```js
console.log(data);
```

### Step 5 — Open DevTools

Go to:

```text
Browser
→ DevTools
→ Console
```

Expand the object and inspect its properties.

For the Advice API, you may discover:

```text
data
└── slip
    ├── id
    └── advice
```

Therefore:

```js
data.slip.id
```

gets the advice ID.

And:

```js
data.slip.advice
```

gets the actual advice text.

---

# 6. The Most Important API Skill

Do NOT rely entirely on memorizing response structures.

Different APIs return completely different structures.

For example:

```js
data.user.name
```

Another API might return:

```js
data.results[0].title
```

Another:

```js
data.products[0].price
```

Another:

```js
data.slip.advice
```

The professional approach is:

```text
Receive the data
      ↓
Inspect the object
      ↓
Understand its structure
      ↓
Access the properties you need
```

---

# 7. Checking the HTTP Response

You can inspect the response before converting it to JSON.

```js
const response = await fetch(url);

console.log(response);
```

### Check the status code

```js
console.log(response.status);
```

Common status codes:

```text
200 → Success
201 → Created
400 → Bad Request
401 → Unauthorized
403 → Forbidden
404 → Not Found
500 → Server Error
```

### Check whether the request succeeded

```js
console.log(response.ok);
```

Usually:

```text
true → HTTP status is successful
false → HTTP status indicates an error
```

### Check the URL

```js
console.log(response.url);
```

### Check headers

```js
console.log(response.headers);
```

---

# 8. GET Requests

`fetch()` uses GET by default.

This:

```js
fetch(url);
```

is essentially:

```js
fetch(url, {
    method: "GET"
});
```

For a simple GET request, you normally don't need to specify the method.

Example:

```js
const response = await fetch(
    "https://api.adviceslip.com/advice"
);
```

---

# 9. Other HTTP Methods

The main HTTP methods you will encounter are:

```text
GET
POST
PUT
PATCH
DELETE
```

### GET

Retrieve data.

```js
fetch(url);
```

### POST

Send/create data.

```js
fetch(url, {
    method: "POST"
});
```

### PUT

Replace/update data.

```js
fetch(url, {
    method: "PUT"
});
```

### PATCH

Partially update data.

```js
fetch(url, {
    method: "PATCH"
});
```

### DELETE

Delete data.

```js
fetch(url, {
    method: "DELETE"
});
```

The exact requirements depend on the API documentation.

---

# 10. Error Handling

A real application should handle failed requests.

Use `try...catch`:

```js
async function getData() {
    try {
        const response = await fetch("API_URL");

        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error(error);
    }
}

getData();
```

However, remember an important detail:

`fetch()` does not automatically throw an error for HTTP errors such as `404` or `500`.

You can explicitly check:

```js
if (!response.ok) {
    throw new Error("Failed to fetch data");
}
```

So a more complete pattern is:

```js
async function getData() {
    try {
        const response = await fetch("API_URL");

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        const data = await response.json();

        console.log(data);
    } catch (error) {
        console.error(error);
    }
}

getData();
```

---

# 11. The `async/await` Pattern to Remember

For most basic API projects, remember this structure:

```js
async function getData() {
    try {
        const response = await fetch("API_URL");

        if (!response.ok) {
            throw new Error(`HTTP error: ${response.status}`);
        }

        const data = await response.json();

        console.log(data);

    } catch (error) {
        console.error(error);
    }
}

getData();
```

You don't have to memorize every line immediately.

Understand what each stage does:

```text
async
 ↓
Allows await

fetch()
 ↓
Makes the request

await
 ↓
Wait for the response

response
 ↓
HTTP response object

response.json()
 ↓
Convert JSON response into JavaScript data

data
 ↓
The actual information from the API

console.log(data)
 ↓
Inspect what the API returned

try/catch
 ↓
Handle failures
```

---

# 12. API Investigation Workflow

When starting a new project with an unfamiliar API:

```text
1. Find the API endpoint
        ↓
2. Make a simple fetch request
        ↓
3. Log the response
        ↓
4. Check response.status
        ↓
5. Convert response using .json()
        ↓
6. console.log(data)
        ↓
7. Expand the object in DevTools
        ↓
8. Identify the properties you need
        ↓
9. Access those properties in JavaScript
        ↓
10. Put the data into the DOM
```

Example:

```js
const data = await response.json();

console.log(data);
```

Then inspect:

```text
data
├── ...
├── ...
└── ...
```

Only after understanding the structure should you write something like:

```js
data.slip.advice
```

---

# 13. Quick Debugging Checklist

If your API isn't working, check:

- Is the URL correct?
- Is the endpoint accessible?
- Did I use `await fetch()`?
- Did I call `response.json()`?
- Did I `console.log(data)`?
- What does `response.status` say?
- Is `response.ok` true?
- What does the actual object look like in DevTools?
- Am I accessing the correct property?
- Did I put the request inside `try/catch`?
- Is the API requiring an API key?
- Is the API blocked by CORS?

---

# 14. Advice Slip API Example

Endpoint:

```text
https://api.adviceslip.com/advice
```

Basic investigation:

```js
async function getAdvice() {
    const response = await fetch(
        "https://api.adviceslip.com/advice"
    );

    console.log(response);

    const data = await response.json();

    console.log(data);
}

getAdvice();
```

After inspecting the returned object, you can access:

```js
data.slip.id
```

and:

```js
data.slip.advice
```

The important lesson isn't memorizing `data.slip.advice`.

The important lesson is knowing how to **discover it yourself**.

---

# 15. Golden Rule

When you don't know what an API returns:

> **Don't guess. Fetch it, convert it, log it, inspect it.**

```js
const response = await fetch(url);

const data = await response.json();

console.log(data);
```

Then let the actual response tell you how to access the data.

---

## Quick Cheat Sheet

```js
// GET request
const response = await fetch(url);

// Check HTTP response
console.log(response.status);
console.log(response.ok);

// Convert JSON
const data = await response.json();

// Inspect API data
console.log(data);

// Access properties after inspecting the object
console.log(data.property);

// Error handling
try {
    const response = await fetch(url);

    if (!response.ok) {
        throw new Error(`HTTP error: ${response.status}`);
    }

    const data = await response.json();

    console.log(data);
} catch (error) {
    console.error(error);
}
```

### Remember

**`fetch()` → Response → `.json()` → Data → Inspect → Use**