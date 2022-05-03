# Stylify Me

A Style Guide Generator - using [NodeJS](http://nodejs.org/) and [Puppeteer](https://pptr.dev/), an API to control Chrome.
See it live at http://stylifyme.com

This repo only contains the web service.
We host our app on [Heroku](http://heroku.com).

## Running the service locally

1. Make sure you have [NodeJS](http://nodejs.org/) installed and running
2. Install dependencies with npm `npm install`
3. Update the referer url check in `src/validateRefererMiddleware.mjs` with the url of your frontend (local and production):

   ```javaScript
   const isRefererValid = (referer, currentPort) => {
   const validRefs = [
   	"http://stylifyme.com",
   	"http://www.stylifyme.com",
   	"http://stylify.herokuapp.com",
   	"http://localhost:9185",
   	"http://localhost:7210",
   	`http://localhost:${currentPort}`,
   ];
   	...
   	}
   ```

4. Start the nodeJs app with `npm run start` (or `node app.mjs`)
5. Query _http://localhost:5000/query?url=https%3A%2F%2Fgoogle.com_ (assuming you run your app on port `5000`) and you should be able to see a JSON response
   I recommend using [Postman](http://www.getpostman.com) for debugging your api

### Frontend

This repo only contains the web service, you can query it from the front end like this:

```javaScript
var urlToQuery = encodeURIComponent("http://google.com");

$.ajax({
	dataType: "jsonp",
	url: "http://youreServiceUrl.com/query?url="+ urlToQuery,
	success: function(data){
		if(data["error"]){
			alert("Error: " + data["error"]);
			return;
		}
		//PROCESS the result
	},
	timeout : 10000
}).fail(function(){
	alert("Could not query site, the service might be down, please try again later.");
});
```
