## The InterWeb

### Introduction to HTTP

HTTP stands for HyperText Transfer Protocol. It is the usual method of data transfer on the internet. An HTTP interaction consists of two parts: a request, and a response. For example, when you visit a web page in your browser, the browser makes an HTTP request to that site, and the site returns an HTTP response, which the web browser renders for you.

#### Request fields

The request contains many parts. The first is a request line, which tells the server what it is looking for, and what protocol it is using. For example, when I navigate to google.com/calendar, the first line will be `GET /calendar HTTP/1.1`. You don't need to mess with this.

The next request field is the request header. Information can be added to the request header to tell the server many different things, including what type of data you will accept as a response, what your authorization token is, the content type of the request, and the user-agent (what device the user is using). Usually you will may to set `Accept`, `Authorization`, and `Content-Type`. You can find all of the possible fields here: https://en.wikipedia.org/wiki/List_of_HTTP_header_fields#Request_fields.

The next request field is a message body. This is optional. However, in many cases, you will need to pass extra data to the server in order to tell the server what you want. For example, you may have to pass an API key and a search parameter in the message body for a server to return results pertaining to that search query. 

### HTTP Request Types

There are many types of HTTP requests. Remember the first line of the request from above, it said `GET /calendar HTTP/1.1`. GET is actually the request type. This tells the server that you are looking to retrieve a resource from that location. Other common request types you will use are GET, POST, PUT, and DELETE. Each has best-practice guidelines for what they should do; however, it many vary from server to server what each request type does. See all of the request types here: https://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol#Request_methods.

### Introduction to JSON

JSON stands for JavaScript Object Notation. JSON has become the most common way to pass data on the web. JSON is written in plaintext and is human-readable, but formatted into arrays, dictionaries, and other data types. Example JSON is shown below (taken from Spotify Web API response):

``` JSON
{
  "external_urls" : {
    "spotify" : "https://open.spotify.com/artist/0OdUWJ0sBjDrqHygGUXeCF"
  },
  "followers" : {
    "href" : null,
    "total" : 306565
  },
  "genres" : [ "indie folk", "indie pop" ],
  "href" : "https://api.spotify.com/v1/artists/0OdUWJ0sBjDrqHygGUXeCF",
  "id" : "0OdUWJ0sBjDrqHygGUXeCF",
  "images" : [ {
    "height" : 816,
    "url" : "https://i.scdn.co/image/eb266625dab075341e8c4378a177a27370f91903",
    "width" : 1000
  }, {
    "height" : 522,
    "url" : "https://i.scdn.co/image/2f91c3cace3c5a6a48f3d0e2fd21364d4911b332",
    "width" : 640
  }, {
    "height" : 163,
    "url" : "https://i.scdn.co/image/2efc93d7ee88435116093274980f04ebceb7b527",
    "width" : 200
  }, {
    "height" : 52,
    "url" : "https://i.scdn.co/image/4f25297750dfa4051195c36809a9049f6b841a23",
    "width" : 64
  } ],
  "name" : "Band of Horses",
  "popularity" : 59,
  "type" : "artist",
  "uri" : "spotify:artist:0OdUWJ0sBjDrqHygGUXeCF"
}
```

You can see that the JSON object returned is a dictionary (begins and ends with {}). There are nested dictionaries (such as at dictionary["external_urls"]), and nested arrays (such as at dictionary["genres"]), and also values possible include integers, strings, and null.

In Java, JSON dictionaries are represented as JsonObject, and JSON arrays are represented with the JsonArray class. They have methods for creating them and for retrieving data from them. 

### Introduction to Volley

Volley is the standard library for making HTTP requests from Android. Android does have an HttpClient class, but Volley provides wrappers around this for ease of use. 

Volley has (very ugly) documentation here: http://afzaln.com/volley/. Find the class you need to use in the bottom left.

Volley has many request classes, depending which type of data you would like to recieve. For example, suppose we'd like to get a JSON object from the server (the most common use case). We would use JsonObjectRequest. Then you pass the request method you would like to use, the URL, a JSONObject to be used as the body, and two listeners: one for a response and one for errors. You will obtain the request method, the URL, and necessary request body from the documentation for the API you are using. Example code follows:

``` Java
public void searchSpotify(String song) {
        // setup requestqueue here. Usually you should set up one queue for global use
        RequestQueue queue = Volley.newRequestQueue(this);

        // setup the request data
        String URL = "https://api.spotify.com/v1/search"; // search for eye of the tiger
        search = search.replaceAll(" ","+"); // necessary to url encode search
        URL = URL+"?q="+search+"&type=track"; // spotify wants it like this "https://api.spotify.com/v1/search?q=search&type=artist"

        // setup the necessary json body for spotify search
        JSONObject body = new JSONObject();
        try {
            body.put("random", "thing"); // unnecessary, but I wanted to show you how to include body data
        } catch (Exception e) {
            Log.e("JSONException", e.getMessage());
        }

        JsonObjectRequest getRequest = new JsonObjectRequest(
                Request.Method.GET,
                URL,
                body,
                new Response.Listener<JSONObject>() {
                    @Override
                    public void onResponse(JSONObject response) {
                        // do something with response
                        Log.d("Response", response.toString());
                    }
                },
                new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {
                        Log.e("Error", error.getMessage());
                    }
                }
        );

        queue.add(getRequest);
}
```

The information on what request method and body are necessary for this request was found here: https://developer.spotify.com/web-api/search-item/.

### Callbacks in Android

The callbacks are used when the response to something is asynchronous. Asynchronous means that the response or callback is not completed right away. Rather, an asynchronous callback is used whenever the task has finished. Asynchronousity is used so that when the program is running a long-running task (such as an HTTP request), the task can run in the background so that the user can still interact with the main portion of the program. Volley HTTP requests are asynchronous, meaning that you should provide callback functions to do the work when your request has finished. 

Note: You've already experienced asynchronousity with OnClickListeners. You've created functions in OnClickListeners that aren't run right away, but rather when some action has completed (the user pushed your button). This is asynchronous. 

To create a callback in Android, you have to create your own class that contains the callback function (remember that everything in Android is a class). You should implement callbacks as an `interface`, which means that you don't implement the functions in the definition of the class, but rather at a later time. A simple example callback is shown below:

``` Java
public interface SuccessCallback { // creates SuccessCallback class which has a function to be called later
	void callback(boolean success);
}

public class HTTPHandler {

    public RequestQueue queue; // this is where you should usually put the queue

    public HTTPHandler(Context context) {
        queue = Volley.newRequestQueue(context); // queue must be initialized with context, so create initializer which does this
    }

	public void searchWithCallback(SuccessCallback callback) { // other classes call this function with a callback, which will be called when this is done
        String URL = "https://api.spotify.com/v1/search?q=eye+of+the+tiger&type=track"; // search for eye of the tiger

        JsonObjectRequest request = new JsonObjectRequest(
                Request.Method.GET,
                URL,
                new JSONObject(),
                new Response.Listener<JSONObject>() {
                    @Override
                    public void onResponse(JSONObject response) {
                        // we got a response, success!
                        callback.callback(true);
                    }
                },
                new Response.ErrorListener() {
                    @Override
                    public void onErrorResponse(VolleyError error) {
                        // we had an error, failure!
                        callback.callback(false);
                    }
                }
        );

        queue.add(request);
    }
}

public class MainActivity extends AppCompatActivity {
	... // other things

	public void makeRequestWithCallback() {
        HTTPHandler handler = new HTTPHandler(this);
        handler.searchWithCallback(new SuccessCallback() {
            @Override
            public void callback(boolean success) {
                if (success) {
                    Log.d("Success", Boolean.toString(success));
                    // continue
                } else {
                    Log.d("Failure", Boolean.toString(success));
                    // handle failure
                }
            }
        });
	}
}
```