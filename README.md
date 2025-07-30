# Email Service

[![Java](https://img.shields.io/badge/Java-21-blue.svg?logo=java)](https://www.oracle.com/java/technologies/javase/jdk21-archive-downloads.html)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.5.4-brightgreen.svg?logo=spring-boot)](https://spring.io/projects/spring-boot)
[![License](https://img.shields.io/badge/license-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

A backend email service developed as a solution for [Uber's Backend Coding Challenge](https://github.com/uber-archive/coding-challenge-tools/blob/master/coding_challenge.md).

This project leverages Java 21 and Spring Boot, integrating with Amazon SES for reliable email delivery.

---

## Table of Contents

- [Requirements](#requirements)
- [Setup](#setup)
- [Amazon SES Configuration](#amazon-ses-configuration)
- [Testing the API](#testing-the-api)

---

## Requirements

- Java 21
- Maven
- AWS Account with SES enabled and a verified email address

---

## Setup

1. **Clone the repository:**
   ```sh
   git clone https://github.com/RafaelTomazGraciano/Email_Service.git
   cd Email_Service/email-service
   ```

2. **Configure AWS Credentials:**

   Edit the file [`src/main/resources/application.properties`](email-service/src/main/resources/application.properties):

   ```properties
   spring.application.name=email-service

   aws.accessKeyId=YOUR_AWS_ACCESS_KEY_ID
   aws.secretKey=YOUR_AWS_SECRET_KEY
   aws.region=YOUR_AWS_REGION
   ```

   Replace `YOUR_AWS_ACCESS_KEY_ID`, `YOUR_AWS_SECRET_KEY`, and `YOUR_AWS_REGION` with your actual AWS credentials and region (e.g., `us-east-1`).

---

## Amazon SES Configuration

You must use a verified sender email address in Amazon SES.

Update the source email in [`SesEmailSender.java`](email-service/src/main/java/com/email_service/infra/SesEmailSender.java):

```java
// ...existing code...
.withSource("your_verified_email@domain.com")
// ...existing code...
```

Replace `"your_verified_email@domain.com"` with the email address you have verified in your Amazon SES account.

---

## Testing the API

The application will start on `http://localhost:8080`.

You can test the email sending endpoint by making an HTTP POST request as shown below.

- **Endpoint:** `POST http://localhost:8080/api/email`
- **Request Body Example:**

```json
{
  "to": "recipient@example.com",
  "subject": "Test Email",
  "body": "This is a test email sent via the Email Service."
}
```

Replace `"recipient@example.com"` with the actual recipient's email address.
