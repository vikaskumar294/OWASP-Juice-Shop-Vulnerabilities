# Reflected XSS

**Solution:**

1. Go to the OWASP Juice Shop Home page and order some products. Fill in the details like name, address, zipcode, card name, and payment.  
2. Now click on the **Track Order** option.  
3. In the URL, you'll see something like `id=5267-806e6938843b7096`. This parameter is vulnerable.  
4. Go to the challenge page, copy the payload below, and replace the `id` value in the URL with it.  
   Then press **Enter** and reload the page — the challenge will be solved.

```html
<iframe src="javascript:alert(`xss`)">
