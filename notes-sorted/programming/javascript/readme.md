# JavaScript

## Async Await

For parallel requests:

When You have an multiple endpoints you need to make requests to from an API and the order of execution does not matter, you can use async await as follows:

1. Create an array of these endpoints

   ```js
   const apiEndpoints = ["posts", "users", "todos"];
   ```

2. Use `Array.map()` to execute the async/await logic for each request. This creates an Array of Promises.

   ```js
   const DataPromises = apiEndpoints.map(async endpoint => {
     const { data } = await axios.get(endpoint);
     apiData[endpoint] = data;
   });
   ```

3. Await the complete response by using `Promise.all()`

   ```js
   await Promise.all(DataPromises);
   ```

4. All of this functionality needs to be wrapped within an `async` function

   ```js
   async function getEndpoints() {
     const DataPromises = apiEndpoints.map(async endpoint => {
       const { data } = await axios.get(endpoint);
       apiData[endpoint] = data;
     });

     await Promise.all(DataPromises);
   }
   ```

**Here's an example using axios**

```js
import axios from "axios";

axios.defaults.baseURL = "https://jsonplaceholder.typicode.com";

const apiData = {};
const apiEndpoints = ["posts", "users", "todos"];

async function getEndpoints() {
  const DataPromises = apiEndpoints.map(async endpoint => {
    const { data } = await axios.get(endpoint);
    apiData[endpoint] = data;
  });

  await Promise.all(DataPromises);
}

getEndpoints();
```

## Axios

### Creating An Instance

```js
import axios from "axios";

const api = axios.create({
  baseURL: `https://jamstack-api.firebaseio.com/`
});

api.interceptors.request.use(config => {
  config.url = `${config.baseURL}/${config.url}.json`;
  return config;
});

export default api;
```

## Interesting

The first alert will actually fire before the calendar's view gets changes and the view will only change after closing the alert.

The second alert, inside the `timeout`, will fire at what seems the exact same time
as the changing view even though it has 0 seconds for the `timeout`.

I think this has to do with the way JavaScript works like what you've read when learning about Promises & Async/Await.

```js
setTimeout(() => {
  calendar.changeView("listWeek");
  alert("Alert1 -> Line After changeView!");

  setTimeout(() => {
    alert("Alert2 -> In another timeout!");
  }, 0);
}, 1500);
```
