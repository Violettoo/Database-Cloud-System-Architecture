# Database-Exercise-3
Exercise 3: Packet Inspection Analysis. 

Observation of HTTP HeadersIn this step, I utilized Wireshark to capture a POST request sent from Postman to Node-RED. As seen in my captured screenshot <img width="1024" height="576" alt="image" src="https://github.com/user-attachments/assets/1cb15996-8f21-4692-89cf-4bc77142abed" />
 the Hypertext Transfer Protocol section reveals critical metadata:

Endpoint: POST /api/secure-data HTTP/1.1 

Content-Type: application/json 

Authorization: Bearer super_secret_iot_token_123 
