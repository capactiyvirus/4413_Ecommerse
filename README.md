# 4413_Ecommerse

[Project Website](https://bbc-client.netlify.app/)

[Git For Project](https://github.com/chenc118/4413_groupProject)

![](bigbook.png)



[How to create REST API in Java using DynamoDB](https://www.serverless.com/blog/how-to-create-a-rest-api-in-java-using-dynamodb-and-serverless)

[Building an App with Spring boot](https://spring.io/guides/gs/spring-boot/)


# Implementation

# Decisions and Trade-Offs
    Our frontend is composed of React and Redux. To handle authentication we used AWS Cognito. We deployed our backend through serverless.yml, which constructs a cloudformation stack consisting of AWS API gateway acting as our API endpoints. We used Lambda to handle all API actions and used DynamoDB for datastore and CloudWatch for logging. For development we designed our API in SwaggerHub and used smoke tests via Postman. For general backend and frontend development we deployed GitHub Repositories. 

    The tradeoff for using Java on AWS Lambda is load times. Since we use AWS API gateway with Lambda for the backend because it allows for each API endpoint to be scaled according to load. This also allows for requests to be processed async without any unique handling, since DynamoDB handles concurrent read/writes. However, Java is relatively slow and as such a six second cold start time on Lambda (after initial cold start, warm execution drops to an order of milliseconds) is required and will be apparent during testing. 

# Limitations
    To handle credit-card checkout we used Stripe’s API, however this comes with a huge limitation on what we can do for testing it. If the credit-card entered is not one from the Stripe’s testing site the card will automatically be declined due to it being attached to Stripe’s API.




















# Security
    For most security related issues we implemented 3rd-party solutions to ensure the element was handled properly and efficiently. We then tested our implementation to see if it was working as expected.
    
    Authentication: To ensure authentication our group used AWS Cognito which handles all security related issues in regards to sign-in/sign-up. We then later tested for this by trying to access the admin page through a user account and it was blocked.

    Injections: As stated before our group decided to use DynamoDB for our datastore. As such, no SQL is present in our program therefore SQL injections are not possible.

    Cross-Site-Scripting: To ensure harmful scripts cannot be injected into our website we escape all user data into non-harmful html entities. We then tested this by attempting a XSS attack on a book review.
