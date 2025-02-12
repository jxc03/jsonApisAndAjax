<h1 align="center">
  JSON APIs And AJAX
</h1>

<p>
  This teached me the basics about working with APIs and different AJAX technologies in the browser.
</p>

## Steps
**S1 - Handle Click Events with JavaScript using the onclick property**<br>
You want your code to execute only once your page has finished loading. For that purpose, you can attach a JavaScript event to the document called `DOMContentLoaded`. Here's the code that does this:<br>
`document.addEventListener('DOMContentLoaded', function() {`<br>
`});`<br>

You can implement event handlers that go inside of the `DOMContentLoaded` function. You can implement an `onclick` event handler which triggers when the user clicks on the `#getMessage` element, by adding the following code:<br>
`document.getElementById('getMessage').onclick = function(){};`<br>

Add a click event handler inside of the `DOMContentLoaded` function for the element with id of `getMessage`.

```js
<script>
  document.addEventListener('DOMContentLoaded', function(){
    // Add your code below this line
    document.getElementById('getMessage').onclick = function(){};
    // Add your code above this line
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

**S2 - Change Text with click Events**<br>
When the click event happens, you can use JavaScript to update an HTML element.<br>
For example, when a user clicks the `Get Message` button, it changes the text of the element with the class `message` to say `Here is the message`.<br>

This works by adding the following code within the click event:<br>
`document.getElementsByClassName('message')[0].textContent="Here is the message";`<br>

Add code inside the `onclick` event handler to change the text inside the `message` element to say `Here is the message`.

```js
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      // Add your code below this line
      document.getElementsByClassName('message')[0].textContent="Here is the message";
      // Add your code above this line
    }
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

**S3 - Get JSON with the JavaScript XMLHttpRequest Method**<br>
You can also request data from an external source. This is where APIs come into play.<br>
Remember that APIs - or Application Programming Interfaces - are tools that computers use to communicate with one another. You'll learn how to update HTML with the data we get from APIs using a technology called AJAX.<br>
Most web APIs transfer data in a format called JSON. JSON stands for JavaScript Object Notation.<br>

JSON syntax looks very similar to JavaScript object literal notation. JSON has object properties and their current values, sandwiched between a `{` and a `}`.<br>
These properties and their values are often referred to as "key-value pairs".<br>
However, JSON transmitted by APIs are sent as `bytes`, and your application receives it as a `string`. These can be converted into JavaScript objects, but they are not JavaScript objects by default. The `JSON.parse` method parses the string and constructs the JavaScript object described by it.<br>
You can request the JSON from freeCodeCamp's Cat Photo API. Here's the code you can put in your click event to do this:<br>
`const req = new XMLHttpRequest();`<br>
`req.open("GET",'/json/cats.json',true);`<br>
`req.send();`<br>
`req.onload = function(){`<br>
  `const json = JSON.parse(req.responseText);`<br>
  `document.getElementsByClassName('message')[0].innerHTML = JSON.stringify(json);`<br>
`};`<br>
Here's a review of what each piece is doing. The JavaScript `XMLHttpRequest` object has a number of properties and methods that are used to transfer data. First, an instance of the `XMLHttpRequest` object is created and saved in the `req` variable. Next, the `open` method initializes a request - this example is requesting data from an API, therefore is a `GET` request. The second argument for `open` is the URL of the API you are requesting data from. The third argument is a Boolean value where `true` makes it an asynchronous request. The `send` method sends the request. Finally, the `onload` event handler parses the returned data and applies the `JSON.stringify` method to convert the JavaScript object into a string. This string is then inserted as the message text.<br>

Update the code to create and send a `GET` request to the freeCodeCamp Cat Photo API. Then click the `Get Message` button. Your AJAX function will replace the `The message will go here` text with the raw JSON output from the API.

```js
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      // Add your code below this line
      const req = new XMLHttpRequest();
      req.open("GET",'/json/cats.json',true);
      req.send();
      req.onload = function(){
        const json = JSON.parse(req.responseText);
        document.getElementsByClassName('message')[0].innerHTML = JSON.stringify(json);
      };
      // Add your code above this line
    };
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

**S4 - Get JSON with the JavaScript fetch method**<br>
Another way to request external data is to use the JavaScript `fetch()` method. It is equivalent to `XMLHttpRequest`, but the syntax is considered easier to understand.<br>
Here is the code for making a GET request to `/json/cats.json`<br>
`fetch('/json/cats.json')`<br>
  `.then(response => response.json())`<br>
  `.then(data => {`<br>
    `document.getElementById('message').innerHTML = JSON.stringify(data);`<br>
  `})`<br>
Take a look at each piece of this code.<br>

The first line is the one that makes the request. So, `fetch(URL)` makes a `GET` request to the URL specified. The method returns a Promise.<br>
After a Promise is returned, if the request was successful, the `then` method is executed, which takes the response and converts it to JSON format.<br>
The `then` method also returns a Promise, which is handled by the next `then` method. The argument in the second `then` is the JSON object you are looking for!<br>
Now, it selects the element that will receive the data by using `document.getElementById()`. Then it modifies the HTML code of the element by inserting a string created from the JSON object returned from the request.<br>

Update the code to create and send a `GET` request to the freeCodeCamp Cat Photo API. But this time, using the `fetch` method instead of `XMLHttpRequest`.

```js
<script>
  document.addEventListener('DOMContentLoaded',function(){
    document.getElementById('getMessage').onclick= () => {
      // Add your code below this line
      fetch('/json/cats.json')
      .then(response => response.json())
      .then(data => {
        document.getElementById('message').innerHTML = JSON.stringify(data);
      })
      // Add your code above this line
    };
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p id="message" class="box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

**S5 - Access the JSON Data from an API**<br>
In the previous challenge, you saw how to get JSON data from the freeCodeCamp Cat Photo API.<br>
Now you'll take a closer look at the returned data to better understand the JSON format. Recall some notation in JavaScript:<br>
`[ ] -> Square brackets represent an array.`<br>
`{ } -> Curly brackets represent an object.`<br>
`" " -> Double quotes represent a string. They are also used for key names in JSON.`<br>
Understanding the structure of the data that an API returns is important because it influences how you retrieve the values you need.<br>

On the right, click the `Get Message` button to load the freeCodeCamp Cat Photo API JSON into the HTML.<br>
The first and last character you see in the JSON data are square brackets `[ ]`. This means that the returned data is an array. The second character in the JSON data is a curly `{` bracket, which starts an object. Looking closely, you can see that there are three separate objects. The JSON data is an array of three objects, where each object contains information about a cat photo.<br>

You learned earlier that objects contain "key-value pairs" that are separated by commas. In the Cat Photo example, the first object has `"id":0` where `id` is a key and `0` is its corresponding value. Similarly, there are keys for `imageLink`, `altText`, and `codeNames`. Each cat photo object has these same keys, but with different values.<br>

Another interesting "key-value pair" in the first object is `"codeNames":["Juggernaut","Mrs. Wallace","ButterCup"]`. Here `codeNames` is the key and its value is an array of three strings. It's possible to have arrays of objects as well as a key with an array as a value.<br>

Remember how to access data in arrays and objects. Arrays use bracket notation to access a specific index of an item. Objects use either bracket or dot notation to access the value of a given property. Here's an example that prints the `altText` property of the first cat photo - note that the parsed JSON data in the editor is saved in a variable called `json`:<br>
`console.log(json[0].altText);`<br>
The console would display the string `A white cat wearing a green helmet shaped melon on its head.`.<br>

For the cat with the `id` of 2, print to the console the second value in the `codeNames` array. You should use bracket and dot notation on the object (which is saved in the variable `json`) to access the value.

```js
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      const req = new XMLHttpRequest();
      req.open("GET",'/json/cats.json', true);
      req.send();
      req.onload=function(){
        const json = JSON.parse(req.responseText);
        document.getElementsByClassName('message')[0].innerHTML = JSON.stringify(json);
        // Add your code below this line
        console.log(json[2].codeNames[1]);
        // Add your code above this line
      };
    };
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

**S6 - Convert JSON Data to HTML**<br>
Now that you're getting data from a JSON API, you can display it in the HTML.<br>

You can use a `forEach` method to loop through the data since the cat photo objects are held in an array. As you get to each item, you can modify the HTML elements.<br>

First, declare an html variable with `let html = "";` .<br>
Then, loop through the JSON, adding HTML to the variable that wraps the key names in `strong` tags, followed by the value. When the loop is finished, you render it.<br>
Here's the code that does this:<br>
`let html = "";`<br>
`json.forEach(function(val) {`<br>
  `const keys = Object.keys(val);`<br>
  `html += "<div class = 'cat'>";`<br>
  `keys.forEach(function(key) {`<br>
    `html += "<strong>" + key + "</strong>: " + val[key] + "<br>";`<br>
  `});`<br>
  `html += "</div><br>";`<br>
`});`<br>
<b>Note</b>: For this challenge, you need to add new HTML elements to the page, so you cannot rely on `textContent`. Instead, you need to use `innerHTML`, which can make a site vulnerable to cross-site scripting attacks.

Add a `forEach` method to loop over the JSON data and create the HTML elements to display it.<br>
Here is some example JSON:<br>
`[`<br>
  `{`<br>
    `"id":0,`<br>
      `"imageLink":"https://cdn.freecodecamp.org/curriculum/legacy-json-apis-ajax/funny-cat.jpg",`<br>
      `"altText":"A white cat wearing a green helmet shaped melon on its head. ",`<br>
      `"codeNames":[ "Juggernaut", "Mrs. Wallace", "Buttercup"`<br>
    `]`<br>
  `}`<br>
`]`

```js
```

**S7 - Render Images from Data Sources**<br>
The last few challenges showed that each object in the JSON array contains an `imageLink` key with a value that is the URL of a cat's image.<br>
When you're looping through these objects, you can use this `imageLink` property to display this image in an `img` element.<br>
Here's the code that does this:<br>
`html += "<img src = '" + val.imageLink + "' " + "alt='" + val.altText + "'>";`<br>

Add code to use the imageLink and altText properties in an img tag.

```js
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      const req=new XMLHttpRequest();
      req.open("GET",'/json/cats.json',true);
      req.send();
      req.onload = function(){
        const json = JSON.parse(req.responseText);
        let html = "";
        json.forEach(function(val) {
          html += "<div class = 'cat'>";
          // Add your code below this line
          html += "<img src = '" + val.imageLink + "' " + "alt='" + val.altText + "'>";
          // Add your code above this line
          html += "</div><br>";
        });
        document.getElementsByClassName('message')[0].innerHTML=html;
      };
     };
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

**S8 - Pre-filter JSON to Get the Data You Need**<br>
If you don't want to render every cat photo you get from the freeCodeCamp Cat Photo API, you can pre-filter the JSON before looping through it.

Given that the JSON data is stored in an array, you can use the `filter` method to filter out the cat whose `id` key has a value of `1`.<br>
Here's the code to do this:<br>
`json = json.filter(function(val) {,`<br>
  `return (val.id !== 1);`<br>
`});`<br>

Add code to `filter` the json data to remove the cat with the `id` value of `1`.

```js
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('getMessage').onclick = function(){
      const req = new XMLHttpRequest();
      req.open("GET",'/json/cats.json', true);
      req.send();
      req.onload=function(){
        let json = JSON.parse(req.responseText);
        let html = "";
        // Add your code below this line
        json = json.filter(function(val) {
          return (val.id !== 1);
        });

        // Add your code above this line
         json.forEach(function(val) {
           html += "<div class = 'cat'>"

           html += "<img src = '" + val.imageLink + "' " + "alt='" + val.altText + "'>"

           html += "</div>"
         });
         document.getElementsByClassName('message')[0].innerHTML = html;
       };
     };
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>
<h1>Cat Photo Finder</h1>
<p class="message box">
  The message will go here
</p>
<p>
  <button id="getMessage">
    Get Message
  </button>
</p>
```

**S9 - Get Geolocation Data to Find A User's GPS Coordinates**<br>
Another cool thing you can do is access your user's current location. Every browser has a built in navigator that can give you this information.<br>

The navigator will get the user's current longitude and latitude.<br>
You will see a prompt to allow or block this site from knowing your current location. The challenge can be completed either way, as long as the code is correct.<br>
By selecting allow, you will see the text on the output phone change to your latitude and longitude.<br>
Here's code that does this:<br>
`if (navigator.geolocation){`<br>
  `navigator.geolocation.getCurrentPosition(function(position) {`<br>
    `document.getElementById('data').innerHTML="latitude: " + position.coords.latitude + "<br>longitude: " + position.coords.longitude;`<br>
  `});`<br>
`}`<br>
First, it checks if the `navigator.geolocation` object exists. If it does, the `getCurrentPosition` method on that object is called, which initiates an asynchronous request for the user's position. If the request is successful, the callback function in the method runs. This function accesses the `position` object's values for latitude and longitude using dot notation and updates the HTML.<br>

Add the example code inside the `script` tags to check a user's current location and insert it into the HTML.

```js
<script>
  // Add your code below this line
  if (navigator.geolocation){
    navigator.geolocation.getCurrentPosition(function(position) {
      document.getElementById('data').innerHTML="latitude: " + position.coords.latitude + "<br>longitude: " + position.coords.longitude;
    });
}
  // Add your code above this line
</script>
<h4>You are here:</h4>
<div id="data">
</div>
```

**S10 - Post Data with the JavaScript XMLHttpRequest Method**<br>
In the previous examples, you received data from an external resource. You can also send data to an external resource, as long as that resource supports AJAX requests and you know the URL.

JavaScript's `XMLHttpRequest` method is also used to post data to a server. Here's an example:<br>
`const xhr = new XMLHttpRequest();`<br>
`xhr.open('POST', url, true);`<br>
`xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');`<br>
`xhr.onreadystatechange = function () {`<br>
  `if (xhr.readyState === 4 && xhr.status === 201){`<br>
    `const serverResponse = JSON.parse(xhr.response);`<br>
    `document.getElementsByClassName('message')[0].textContent = serverResponse.userName + serverResponse.suffix;`<br>
  `}`<br>
`};`<br>
`const body = JSON.stringify({ userName: userName, suffix: ' loves cats!' });`<br>
`xhr.send(body);`<br>

You've seen several of these methods before. Here the `open` method initializes the request as a `POST` to the given URL of the external resource, and passes true as the third parameter - indicating to perform the operation asynchronously.<br>
The `setRequestHeader` method sets the value of an HTTP request header, which contains information about the sender and the request. It must be called after the `open` method, but before the `send` method. The two parameters are the name of the header and the value to set as the body of that header.<br>
Next, the `onreadystatechange` event listener handles a change in the state of the request. A `readyState` of `4` means the operation is complete, and a `status` of `201` means it was a successful request. Therefore, the document's HTML can be updated.<br>
Finally, the `send` method sends the request with the `body` value. The `body` consists of a `userName` and a `suffix` key.

Update the code so it makes a `POST` request to the API endpoint. Then type your name in the input field and click `Send Message`. Your AJAX function should replace `Reply from Server will be here.` with data from the server. Format the response to display your name appended with the text `loves cats`.

```js
<script>
  document.addEventListener('DOMContentLoaded', function(){
    document.getElementById('sendMessage').onclick = function(){

      const userName = document.getElementById('name').value;
      const url = 'https://jsonplaceholder.typicode.com/posts';
      // Add your code below this line
      const xhr = new XMLHttpRequest();
      xhr.open('POST', url, true);
      xhr.setRequestHeader('Content-Type', 'application/json; charset=UTF-8');
      xhr.onreadystatechange = function () {
        if (xhr.readyState === 4 && xhr.status === 201){
          const serverResponse = JSON.parse(xhr.response);
          document.getElementsByClassName('message')[0].textContent = serverResponse.userName + serverResponse.suffix;
        }
      };
      const body = JSON.stringify({ userName: userName, suffix: ' loves cats!' });
xhr.send(body);
      // Add your code above this line
    };
  });
</script>
<style>
  body {
    text-align: center;
    font-family: "Helvetica", sans-serif;
  }
  h1 {
    font-size: 2em;
    font-weight: bold;
  }
  .box {
    border-radius: 5px;
    background-color: #eee;
    padding: 20px 5px;
  }
  button {
    color: white;
    background-color: #4791d0;
    border-radius: 5px;
    border: 1px solid #4791d0;
    padding: 5px 10px 8px 10px;
  }
  button:hover {
    background-color: #0F5897;
    border: 1px solid #0F5897;
  }
</style>

<h1>Cat Friends</h1>
<p class="message box">
  Reply from Server will be here
</p>
<p>
  <label for="name">Your name:
    <input type="text" id="name"/>
  </label>
  <button id="sendMessage">
    Send Message
  </button>
</p>
```


```js
```
