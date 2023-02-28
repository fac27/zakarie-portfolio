## 1. Write code that executes asynchronously

```javascript
const handleSubmit = (e) => {
  e.preventDefault();
  const postcode = e.target.children[1].value;

  validatePostcode(postcode).then((result) => {
    if (result) {
      getBasicInfo(postcode).then((data) => displayBasicInfo(data));
      getNearestBuses(postcode).then((data) => displayTransportInfo(data));
    }
  });
};
```

This <code>handleSubmit</code> function is triggered when the user submits a form. Then, the <code>validatePostcode</code> function is called with the <br />
postcode value provided by the user. This function returns a *Promise* which resolves with a boolean value indicating <br />
whether the postcode is valid or not.<br />

The **.then** method is used to handle the resolved value of the Promise returned by validatePostcode. If the postcode is <br />
valid (result is true), then two API calls (<code>getBasicInfo</code> and <code>getNearestBuses</code>) are made to retrieve data about the postcode.<br />

Each of these API calls also returns a Promise, and the .then method is used again to handle the resolved value of each Promise. <br />
If the Promise is resolved successfully, the data is passed to a corresponding display function (<code>displayBasicInfo</code> or <code>displayTransportInfo</code>).<br />

Since these API calls are asynchronous and return Promises, the JavaScript code does not block the main thread and <br />
can execute other tasks while waiting for the API responses.

## 2. Use callbacks to access values that aren’t available synchronously

```javascript
getLongAndLat(postcode).then((result) => {
  const { longitude, latitude } = result;
});
```

In this code snippet, the <code>getLongAndLat</code> function is called with the **postcode** parameter. This function returns <br />
a promise that will eventually resolve with an object containing the ***longitude*** and ***latitude*** values.<br />

The <code>.then</code> method is used to define a callback function that will be executed when the promise is resolved. <br />
The callback function takes the resolved result as its parameter, which is the object containing ***longitude*** and ***latitude***.

By using the <code>.then</code> method and the callback function, we can access the ***longitude*** and ***latitude*** values asynchronously, <br />
once they become available, instead of trying to access them synchronously before the promise has been resolved.


## 3. Use promises to access values that aren’t available synchronously

```javascript
await Promise.all(
  allQueryStrings.map((qs) =>
    fetch(qs)
      .then((response) => {
        if (response.ok) {
          progressBar.value = Math.floor(
            (++fetchNumber / totalFetches) * 100
          );
          progressBar.textContent = `${progressBar.value}%`;
          p.textContent = `Fetching crime data (${progressBar.value}%)`;
          return response.json();
        }
      }).catch((error) => {
        console.error("OH NO! This happened when fetching crime data:\n" + error);
        userInfoContainer.style.display = 'none';
      })
  )
)
```

This code uses the <code>Promise.all()</code> method to make multiple API requests at once and waits for all of them to *resolve* <br />
before proceeding to the next step in the code. This help us to access values that aren't available synchronously because the code doesn't <br />
have to wait for each request to finish before moving on to the next one. 

Instead, it can continue executing the code and handle the data returned from each request once it's available.

## 4. Use the fetch method to make HTTP requests and receive responses

```javascript
export const getBasicInfo = (postcode) => {
  return fetch(`https://api.postcodes.io/postcodes/${postcode}`)
    .then((response) => {
      if (response.ok) {
        return response.json().then((data) => data.result);
      } else {
        throw new Error(response.status);
      }
    })
    .catch((error) => console.log(error));
};
```

The <code>fetch</code> method is used to make a request to the specified URL and returns a *Promise* that resolves to a *Response* object. <br />
The <code>.then</code> method is then used to handle the response object, where it checks if the response is okay using the <code>response.ok</code>property. <br />
If it is okay, it returns the *JSON* data from the response using the <code>response.json()</code> method and resolves it to the <code>data.result</code>.

If the response is not okay, the *throw* statement is executed with the response status as the argument. Finally, the <code>catch</code> method is <br />
used to handle any errors that may occur during the fetch operation.

## 5. Configure the options argument of the fetch method to make GET and POST requests

```javascript
fetch('https://echo.oliverjam.workers.dev/json', {
  method: 'POST',
  headers: {
    'content-type': 'application/json',
  },
  body: JSON.stringify({
    name: 'Zakarie',
    cohort: 'fac27',
  }),
})
  .then((response) => {
    if (response.ok) {
      response.json().then((data) => console.log(data));
    } else {
      throw new Error(response.status);
    }
  })
  .catch((error) => console.log(error));
```

The code snippet is an example of configuring the *options* argument of the <code>fetch</code> method to make a **POST** request. <br />
The second argument of the fetch function is an object that includes several properties that configure the request. In this case, the <code>method</code> <br /> property is set to **"POST"**, indicating that the request is a **POST** request, and the <code>headers</code> property is an object that <br />
specifies the content-type of the request as **"application/json"**. 

Finally, the <code>body</code> property is set to a **JSON** string that includes the data that will be sent as the body of the request.

## 6. Use the map array method to create a new array containing new values

```javascript
const sanitizedPostcode = postcode
  .split('')
  .filter((char) => char !== ' ')
  .map((char) => char.toLowerCase())
  .join('');
```

There is a part in our codebase that requires a specific type of postcode to return the required result. So, we used the <code>map</code> method to create <br />
a new array of transformed values. The <code>split</code> method is called on the postcode string to break it into an array of characters, <br />
then the <code>filter</code> method is called on this array to remove any spaces. 

The <code>map</code> method is then called on this filtered array to convert each character to lowercase. Finally, the <code>join</code> method <br />
is called to join the lowercase characters back into a string.

## 7. Use the filter array method to create a new array with certain values removed

See above point. #6

## 8. Access DOM nodes using a variety of selectors

```javascript
const basicInfoOutput = document.querySelector('#output__info');
```

We are using the <code>querySelector</code> method to select the first element that matches the CSS selector **#output__info**, which <br />
is an element with the id attribute of **output__info**. We attach that element the basic info of the specified postcode.

This method can be used to select elements based on their ID, class, tag name, or other attributes. Once the element is selected, <br />
it can be manipulated or used in other ways, such as adding content or event listeners.

## 9. Add and remove DOM nodes to change the content on the page

```javascript
const basicInfoDiv = document.createElement('div');
---
document.querySelector('.postcodes__container').innerHTML = '';
```

The first line of the code creates a new <code>div</code> element called **basicInfoDiv**.

The second line of the code selects an element on the page with a class of **postcodes__container** using the <code>document.querySelector()</code> <br />
method, and sets its **innerHTML** property to an empty string. This effectively removes any child elements previously contained <br />
within the **postcodes__container** element.

Together, these two lines of code allow for the creation of a new element and the removal of any existing elements within a specified <br />
container element, effectively changing the content on the page.

## 10. Toggle the classes applied to DOM nodes to change their CSS properties

By toggling a class on an element, we can separate the presentation logic from the JavaScript logic. This makes our code more modular <br />
and easier to maintain. We can define CSS rules for the class in a separate stylesheet or in the same file, and they will apply to the element <br />
whenever the class is added to or removed from it.

Toggling classes provides a more flexible, modular, and maintainable way to change the appearance of elements on a web page.

## 11. Use consistent layout and spacing

Using consistent layout and spacing in your code makes it more readable and easier to understand for both yourself and others who may <br />
be working  on the project. When code is consistently formatted, it's easier to quickly scan and identify key parts of the code, making it faster <br />
to debug and maintain. 

Additionally, consistent spacing can make it easier to identify nested blocks of code, which can be especially helpful in languages <br />
that rely heavily on brackets, such as Javascript.

## 12. Follow a spacing guideline to give our app a consistent feel

Following a spacing guideline is important because it ensures that all elements on the page are laid out in a visually pleasing <br />
and organized manner. Consistent spacing helps to create a clear visual hierarchy and makes it easier for users to scan and understand the content.

Inconsistent spacing can make an app look disorganized and chaotic, which can be confusing and frustrating for users.

## 13. Debug client side JS in our web browser

Debugging client-side JavaScript in a web browser is an essential skill for web developers.

Modern web browsers come with a set of developer tools that include a JavaScript console. The console allows you to execute JavaScript <br />
code and view the output or any errors that may occur. You can also set breakpoints in the JavaScript code using the debugger statement. <br />
When the code reaches the breakpoint, it pauses execution, allowing you to inspect the values of variables and step through the code one line at a time.

## 14. Use console.log() to help us debug our code

When we encounter a problem with our code, we can use <code>console.log()</code> to output messages to the browser console to help us <br />
understand what is happening in our code and identify potential issues. By examining the output generated by <br />
<code>console.log()</code>, we can often see the values of variables, the order in which functions are being called, and other important <br />
information that can help us track down and fix problems in our code. 
