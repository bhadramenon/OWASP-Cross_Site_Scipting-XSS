## Reflected XSS Challenge

### Goal
Understand how reflected XSS works in the order tracking page of OWASP Juice Shop.

## Tools Used: 
Web browser: To navigate the web application and test different XSS payloads. 
Developer Tools: Inspect the Javascript code and understand the HTML content present on the web application. 
Burpsuite: Helps to intercept, analyze, modify, and test HTTP/HTTPS traffic to identify vulnerabilities.


### What I did
1. Add few products into the basket
   
   
<img width="873" height="570" alt="Screenshot 2026-07-18 at 11 34 44 AM" src="https://github.com/user-attachments/assets/ec7d8cbe-30ac-45b1-83bc-8e9fc4e00ace" />


2. Add new address to order the products.
   

<img width="437" height="492" alt="Screenshot 2026-07-18 at 11 33 54 AM" src="https://github.com/user-attachments/assets/e6aae74a-99c7-4db3-a15d-e125f858db9a" />


3. Choose the delivery mode.


<img width="872" height="584" alt="Screenshot 2026-07-18 at 11 50 03 AM" src="https://github.com/user-attachments/assets/d519991f-1610-4966-ac57-868d9bc6ac7b" />


4. Tracking id is obtained for the ordered products.

<img width="876" height="454" alt="Screenshot 2026-07-18 at 2 40 32 PM" src="https://github.com/user-attachments/assets/646fa9fc-946e-4502-9ad1-31eb8c431aea" />



5. I opened the order tracking feature and used the track ID from my order.


<img width="1008" height="45" alt="Screenshot 2026-07-18 at 12 01 12 PM" src="https://github.com/user-attachments/assets/9f1e77e7-c9ab-447d-a401-40354994ac14" />


Then I replaced the track ID in the URL with an iframe-based XSS payload.


I also watched the request flow in Burp Suite to understand how the input was being passed.

### What I saw
After loading the page, the browser showed a popup with `xss`.

That told me the input was being reflected back and executed in the browser.

The page did not safely handle the value coming from the URL parameter.

### What I learned
This is a reflected XSS issue because the payload is sent in the URL and then reflected in the page response.

The browser runs the injected content because the application does not encode or sanitize the input properly.

Burp Suite helped me see the request clearly and understand where the value was going.

### Why it matters
Reflected XSS can be dangerous because a user may click a crafted link and unknowingly run attacker-controlled JavaScript in their browser.

This can affect user data, page behavior, and trust in the application.

### Prevention
- Validate and sanitize user input.
- Encode output before rendering it in the page.
- Avoid reflecting raw URL parameters in HTML.
- Use safe output handling on the server and client side.

