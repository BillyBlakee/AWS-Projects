This was a small AWS project which I did for fun.

I created an application that used AWS Amplify, DynamoDB, Lambda, IAM and API Gateway.
The application was a simple math application that had the used input a base number and an exponenet. Then the program would output the answer (8^2 = 64)

The first step in creating the application was creating a small index.html file that would have the front end html and css for the web page. This was quite simple with a couple of input fields, some text and a calculate button. This file had to be zipped
so I could later drop it into AWS amplify for easy deployment.

The next step was to open the AWS Amplify service in my AWS console. I created an app and deployed it without a git provider, then drag and dropped my zip file and manually deployed it.

After I had to use AWS labmda so I could run my code serverlessly. I created a function that was authored from scratch. I then updated my labda code with some simple python that would handle the math calculations on my deployed amplify page. I saved the 
code, deployed it, and then created a test event to ensure that my python code was running correctly. After I created the test event I could actually run the test. Once the test was successful I could move on to the next step.

Then I went to the API gateway service. I used rest api for this next step. I created a new API with the default settings. After I created a POST method which integrated my lambda function, this gave API gateway permissions to invoke my function. I also had to enable CORS
to allow my web application to access different domains. After CORS was enabled I deployed my API and saved the invoke URL so I could paste it where needed later.

Then I wanted to incorporate a database so I could save the reults that were output by my program (there was no practical use for this I just wanted to do it so I could learn). I used DynamoDB for this. I first just created a table with the default settings and 
made sure to save the arn as I would need it for later. Then I had to give lambda permission to write to the table that I created. In the lambda configuration tab I clicked 'role name' which navigated me to IAM. From IAM I allowed the lambda function to update my
DynamoDB table. This is also where I pasted the arn that I saved earlier. I also had to update my python in mt lambda function so that it would write to my table in DynamoDB

dynamodb = boto3.resource('dynamodb)
table = dynamodb.Table('MyTable')
now = strftime("%a, %d %b %Y %H:%H:%$ +0000", gntime())

These three lines of code allowed my lambda function to properly store information to my DynamoDB table.

The final thing that I did was have to update my html code with the API gateway link that I copied down earlier.

Below are some images of my application:
![aws1](https://github.com/BillyBlakee/AWS-Projects/assets/151226564/fdd5da9f-fa51-49e7-b5aa-5b85e14d5ed6)
![aws2](https://github.com/BillyBlakee/AWS-Projects/assets/151226564/8b1fe134-c41d-41a8-8ac3-fc025d0010c3)


