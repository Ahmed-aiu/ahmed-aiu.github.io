# Ahmed AIU GitHub Pages

This repository hosts a static web application. The key file is [`static/index.html`](static/index.html), which submits user files to an n8n webhook for processing.

## How it works

1. Users select one or more files in the "RFQ Distribution" form.
2. When the form is submitted, JavaScript gathers the files into a `FormData` object.
3. The files are **POSTed** to the n8n webhook via `XMLHttpRequest`. The URL for this request appears around line 134 of `static/index.html` and should be replaced with **your own** n8n webhook endpoint.
4. The webhook should process the uploaded files and respond with JSON that includes a field named `result_html`. The code also accepts `html` or `data` for backward compatibility.
5. The value of that field must contain HTML wrapping a `<div id='content-container'>...</div>` element. The script extracts the contents of this div and updates the page with the returned HTML.

An example JSON response looks like this:

```json
{
  "result_html": "<div id='content-container'>Processed results here</div>"
}
```

Ensure your webhook responds with the correct structure so the interface updates properly.
