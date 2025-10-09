## Product Tampering


## Solution

Open the Product Tampering challenge or the product listing in your local Juice Shop instance.

Perform a search that returns OWASP SSL Advanced Forensic Tool (O-Saft).

With the proxy enabled, intercept the request that looks like:
GET /rest/products/search?q=OWASP%20SSL%20Advanced%20Forensic%20Tool%20(O-Saft)

Send the intercepted search request to Burp Suite → Repeater and click Send to view the JSON response.

Note the product id (for example 9) and confirm the response contains price, image, and description.

Retrieve the single product resource with:
GET /api/products/<id>
Send this to Repeater and view the full JSON body.

Change the request method from GET to PUT to update the resource.

Add the header: Content-Type: application/json.

Copy the JSON response body from the GET into the PUT request body, locate the description field, and modify its value.

## Example replacement:
"description": "<a href=\"https://owasp.slack.com\">join our slack</a> O-Saft is an easy to use tool"

Send the PUT /api/products/<id> request. Confirm the server responds with 200 OK and returns the updated JSON.

Refresh the product page or re-run the search in the browser to verify the description has changed and the challenge is solved.

## What’s the Vulnerability?

This is a Broken Access Control issue — specifically Missing Authorization on Object Modification (a form of IDOR).

Missing Authorization
The API accepts update requests for product resources without verifying whether the requester is allowed to modify that resource.

## Impact
An attacker can alter product metadata (description, links, etc.), inject malicious links or misleading content, and manipulate what users see.