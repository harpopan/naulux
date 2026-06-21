INTERVIEWER:
“Your frontend is running on localhost:3000 and your backend is on localhost:8000. When you try to fetch data, you get a CORS error. Why does this happen, and how do you fix it?” 🤔🌐
🧠 BEGINNER EXPLANATION
Imagine you live in a Strict Apartment Building (The Browser). 🏢
• You (The Frontend at :3000) want to borrow sugar from a neighbor in a Different Building (The Backend at :8000).
• The security guard (The Browser) stops you and says: “Wait! I don’t know if that neighbor trusts you. I won’t let you take anything unless they explicitly tell me you are allowed to.”
This “Security Guard” is the Same-Origin Policy. It prevents malicious websites from stealing data from other sites.
⚙️ TECHNICAL BREAKDOWN
CORS (Cross-Origin Resource Sharing):
It is a security feature implemented by browsers. An “Origin” is defined by Protocol + Domain + Port. Since your ports are different (:3000 vs :8000), the browser considers them “Cross-Origin.”
The Flow:
1. Preflight Request (OPTIONS): Before the actual request, the browser sends an “OPTIONS” call to the backend to ask: “Hey, is it okay if :3000 talks to you?”
2. The Response: If the backend doesn’t send back the correct header (Access-Control-Allow-Origin), the browser blocks the request and throws the CORS error.
How to fix it:
You must configure your backend (Node.js, Spring Boot, Python, etc.) to allow requests from your frontend port.
• Example (Express.js):
app.use(cors({ origin: ‘http://localhost:3000’ }));
🎯 INTERVIEW FLEX
“CORS is not a ‘bug’; it’s a browser-side security mechanism based on the Same-Origin Policy. To resolve it, we must configure the backend to include the Access-Control-Allow-Origin header in its response. In production, we should never use origin: ‘*’ as it opens security vulnerabilities; we should always whitelist only the specific domains that need access to our API.” 🛡️🚀