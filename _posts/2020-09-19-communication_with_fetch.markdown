---
layout: post
title:      "Communication with fetch "
date:       2020-09-19 23:30:09 +0000
permalink:  communication_with_fetch
---


Wrapping up the javascript module, one of the key sections that I found was AJAX, and more specifically fetch. AJAX stands for asynchronous JavaScript and XML AJAX is used to make requests to the server, without reloading the web page. Which we can then can manipulate the data that is returned from the server. One of the methods we use to execute AJAX is by using fetch.

Two of the basic definitions that fetch uses are, request and response. However there can be other objects that are used within a fetch function. To see a little more about this, here is a snippet of a basic fetch function: 

```
fetch("string representing a URL to a data source")
  .then(response => {
    if (!response.ok) {
      throw new Error('Network response was not ok');
    }
    return response.json();
  })
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error('There has been a problem with your fetch operation:', error);
  });
```

Beginning at the top, with declaring fetch, you will pass in a URL as a string. And this will be used to connect to the server you want to get your data from. From here we then call the .then() function with returns the response from the fetch. As long as we can an response that is okay, we can then move onto the next .then(). With our finally .then(), we get our data we initially wanted in the form of json, in this case. With our data in a json format, we can use that data to start calling other functions. Two ways we can catch some errors while we are using fetch are, writing an if statement within our response callback, and also throwing a catch error at the end of our fetch. Each one will either indicate if our response status fails or the last catch error will print out an error message.

For my project I built a project on reviewing wine. My initial fetch to GET my wines looked very similar to the example above.
```
fetch(`${baseUrl}/wines`)
    .then (resp => {
        if (resp.status !== 200) {
            throw new Error(resp.statusText);
        }
        return resp.json()
    })
    .then (data => {
        Wine.createWines(data);
        Wine.displayWines();
    })
    .catch(errors => console.log(errors))
```

I first used string interpolation with a baseURL that was a variable to my local host, and then the wines endpoint. As I moved along with a successful response, I moved to the data callback. This is where I called in two functions from my Wine class. One was to create the wine from the json data. After creating the wines, I called a displayWine(), to display the wines to the web page. If I were to hit any errors throughout the call, I threw a catch error to my conslole with the errors messages. This is an example of utilizing fetch to GET data. However we can also use a fetch for full CRUD routes. Moving to creating a new wine from a form, 
```
fetch(`${baseUrl}/wines.json`, {
			method: "POST",
			headers: {
				"Accept": "application/json",
				"Content-Type": "application/json"
			},
			body: JSON.stringify(strongParams)
	})
	.then(resp => resp.json())
	.then(data => {
			let wine = Wine.create(data.id, data.label, data.varietal, data.region, data.price);
			wine.renderWine();
			resetInputs();
	})
	.catch(errors => console.log(errors));
```

In this example, we have a similar layout to the GET method we have above. A little more added information we have is putting a method we need, and some metadata about the data. Lastly we through in a body key to use for our params to create the wine. In this instance, because we are creating a new wine, we use a POST method. However if we wanted to update a object, you can change the method to PATCH, as well as DELETE to delete an object. The headers has two keys in our example, Accept which tells the server what kind of data to accept, and Content-Type which indicates the format of the data we are requesting. 

Through learning more about using fetch in this project, I was a new outlook on what we can do to speed up our applications. I didn't have to reload to a whole new page or anything to get new data that wasn't currently present on the page. I can call a fetch to get the data back, and just alter the page alittle to show the data that I need. Continuing to use fetch in the future will be interesting as data continues to grow in projects, and seeing how it changes our load times on web pages and applications. 
