!!! note
	This is for fetching plain text only. See [utils.DownloadFileAsync](../namespaces/utils.md#utilsdownloadfileasyncwindow_id-url-path-verify_image) for downloading binary files or [utils.DownloadImageAsync](../namespaces/utils.md#utilsdownloadimageasyncwindow_id-url) for downloading images in memory.

See also: [utils.HTTPRequestAsync](../namespaces/utils.md#utilshttprequestasyncwindow_id-type-url-user_agent_or_headers-post_data) and
[on_http_request_done](../callbacks/component.md#on_http_request_donetask_id-success-response_text-status-response_headers).

## GET requests

These examples look at making the request first. Handling the response is detailed [below](#handling-the-response).

The simplest request can be done like this:

```js
var url = ...
var GET = 0;

// because we're omitting a user agent or headers, a
// default based on the component name/version will be used.
var id = utils.HTTPRequestAsync(window.ID, GET, url);
```

If you want to supply your own user agent, it can be a simple string like this:

```js
var url = ...
var GET = 0;
var user_agent = "my_app/0.1";
var id = utils.HTTPRequestAsync(window.ID, GET, url, user_agent);
```

If you want to supply custom headers, you can supply a stringified object like this:

```js
var headers = JSON.stringify({
	"User-Agent" : "my_app/0.1",
	"Some other header" : "blah",
});

var url = ...
var GET = 0;
var id = utils.HTTPRequestAsync(window.ID, GET, url, headers);
```

When scraping HTML from a website, you might need to set a `Referer` based on
the website you're accessing and a `User-Agent` based on a browser like this:

```js
var headers = JSON.stringify({
	'User-Agent' : 'Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/114.0',
	'Referer' : 'https://www.last.fm',
});

var url = ...
var GET = 0;
var id = utils.HTTPRequestAsync(window.ID, GET, url, headers);
```

## POST requests

Here's a simple `POST` example.

```js
var headers = JSON.stringify({
	"Content-Type" : "application/json",
});

var url = ...
var POST = 1;
var obj = ...
var post_data = JSON.stringify(obj);
var id = utils.HTTPRequestAsync(window.ID, POST, url, headers, post_data);
```

## Handling the response

When a web request is completed, the `on_http_request_done` callback is called.

Most included samples don't care about the type of failure and report the `response_text` to the `Console`
like this:

```js
// the task_id is the return value from the utils.HTTPRequestAsync call
function on_http_request_done(task_id, success, response_text, status, headers) {
	if (!success) {
		console.log(window.Name, ": ", response_text);
		return;
	}

	// if we get here, do something useful with the response_text
}
```

If `success` is `true`, it only means the server responded. You may have enccountered
a server error and this can be checked with the `status`. It will be `200` for complete
success and I'm sure everyone is familiar with `404` for page not found.

If `success` is `false`, the `status` should always be `0` and the `response_text` should
describe the error.

Lastly, the `response headers` can be inspected but only when `success` is `true`.

```js
if (success) {
	var obj = JSON.parse(response_headers);
	// do something
}
```

## Examples

This first example is designed to fail on purpose by using a url to an image. Only
plain text responses are supported:

```js
var GET = 0;
var url = "https://lastfm.freetls.fastly.net/i/u/770x0/59f6ae4009bc475baf4f5581dd0afe28.jpg";
var id = utils.HTTPRequestAsync(window.ID, GET, url);

// the task_id is the return value from the utils.HTTPRequestAsync call
function on_http_request_done(task_id, success, response_text, status, headers) {
	utils.ShowPopupMessage(response_text);
}
```

The following text should be displayed:

```
Unsupported content type: image/jpeg
```

This should succeed:

```js
var GET = 0;
var url = "https://www.last.fm/";
var id = utils.HTTPRequestAsync(window.ID, GET, url);

// the task_id is the return value from the utils.HTTPRequestAsync call
function on_http_request_done(task_id, success, response_text, status, headers) {
	utils.ShowPopupMessage(response_text);
}
```