# attendance-management-system

🎓 RGUKT Attendance Management System (AWS-Serverless)
A secure, location-based attendance management system for RGUKT students built using AWS services, fully serverless, with Google Sign-In (restricted to @rguktsklm.ac.in), selfie-based verification using AWS Rekognition, and geolocation restriction.

🚀 Features

✅ Login with Google (@rguktsklm.ac.in only)

✅ Face Liveness + Face Match via AWS Rekognition

✅ Location-based attendance validation

✅ Student Registration with Selfie Upload

✅ Attendance submission via webcam selfie

✅ Serverless Architecture using AWS Lambda, S3, DynamoDB, Rekognition

✅ No Amplify | Pure AWS SDK + Hosted UI

📂 Project Structure

/project-root

│

├── login.html         ← Redirects to Cognito Hosted UI (Google Sign-In)

├── register.html      ← Registration form for new users (with selfie & details)

├── attendance.html    ← Attendance capture page (location + face match)

├── denied.html        ← If user is not from @rguktsklm.ac.in

├── success.html       ← Attendance submission confirmation

└── /assets            ← CSS/JS files if needed


🧠 How It Works

User Authentication

User lands on login.html which redirects to Amazon Cognito Hosted UI.
Google Sign-In is enabled and restricted to @rguktsklm.ac.in.
Unauthorized users are redirected to denied.html.

Registration

New users are redirected to register.html.
They fill details like Name, Student ID, Branch, Year, Section.
Upload a selfie with Rekognition Liveness Detection.

On form submit:

Selfie is uploaded to Amazon S3
All form data + S3 image URL is stored in Amazon DynamoDB
Rekognition Face Collection is updated with the user’s face
Redirected to attendance.html.

Attendance

Users upload a new selfie via webcam (with liveness check).
User's current location is verified (only allowed from college coordinates).
AWS Rekognition compares the new selfie with the registered image.
If match → attendance recorded → redirect to success.html.



Lambda & Backend

All backend logic is handled by AWS Lambda functions:
Form submission
S3 uploads
DynamoDB writes
Rekognition comparison
Location check
Communication is through API Gateway endpoints (no Amplify).

📦 AWS Services Used

Amazon Cognito	Authentication via Google OAuth (@rguktsklm.ac.in only)

Amazon S3	Store selfies uploaded during registration & attendance

Amazon DynamoDB	Store user registration data + S3 image URLs

AWS Lambda	Backend functions for processing registration & attendance

Amazon Rekognition	Liveness check & face comparison

API Gateway	Public endpoints for Lambda triggers

IAM Roles & Policies	Secure access between services

