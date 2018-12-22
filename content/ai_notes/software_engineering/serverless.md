---
title: Serverless
menu: 
    ai_notes:
        parent: Software Engineering
draft: True
---
You only pay for the compute time you uses. That's the fun part. 

You have these self-contained code pieces (in AWS, this would be your Lambdas),
and these can be run in parallel. Serverless backends. Data processing. 

Function (the Lambda container), like a Storm bolt, requires a name.

You have to define the memory in a Lambda, and the timeout. 

## Lambda

You can createa a role for your Lambda function that allows you to set policies
for the function itself. Perhaps it can only read from your S3, etc. By default
all the Lambdas share a single role, and this role can create and write
CloudWatch logs, but you can also create custom roles.





