# TextToSpeechServerless

**General Notes**

An simple serverless web application made using HTML, CSS and javascript that converts text into speech using the AWS Polly service. AWS polly is an machine learning service which converts text into lifelike speech, allowing you to create applications that talk, and build entirely new categories of speech-enabled products.

- I'm now building this application on AWS cloud. Currently this app doesn't works as there is no storage service connected to it and no backend services 
to store and retrieve the posts or text.

**The application architecture would be**:

![Pollly](https://user-images.githubusercontent.com/93663329/194707147-614f16d5-3e03-46ff-9311-3e54577d8940.png)

**For now building this app , I'm going to**:
1. Create two s3 buckets, one to host the application and other to store the speech mp3 files recieved from polly.
2. Create an dynamoDB table called posts which stores the text messages and also the status of those text messages that got converted into mp3. This has only one partition key as id.
3. Create appropiate IAM policies for providing access to the lambda functions that are going to acces this s3 buckets and dynamodb, and attach these policies with roles.
4. Create an Simple Notification Service(SNS) topic call "new_posts".
5. Create these necessary lambda functions:
    - First lambda function to create and save the new text to dynamoDB table.
    - Second lambda function to convert the text into audio using polly service. In triggers,  add the SNS topic you created previously.
    - Third lambda function to get all the post messages from dynamoDB table.
6. Create an API gateway with tow methods:
    - GET: to retireve all the text messages
    -POST: to save or create text messages.
7. Deploy the api and then paste the invoke url into the script.js file to use this api endpoint in your application.

