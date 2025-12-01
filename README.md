
# AWS Documentation
Covered: AWS Setup, IAM, Lambda, Glue, Vector Database, OpenSearch & Bedrock  


---

# 1. INTRODUCTION

This document explains how to create and use a complete cloud setup using Amazon Web Services (AWS).

It is written for beginners, with simple steps and explanations, so that even a non-programmer can follow it.

This project shows how to:
- Create an AWS account
- Secure access using IAM
- Run code with AWS Lambda
- Process data with Spark using AWS Glue
- Store and search data using a vector database
- Use AI services via AWS Bedrock

---

# 2. AWS ACCOUNT CREATION

---

## 2.1 What You Need

Before you start:

- Email address  
- Mobile phone  
- Debit/credit card or UPI  
- Internet connection  
- Chrome or Edge browser  

---

## 2.2 Steps to Create Account

### Step 1: Open AWS website

Go to:
https://aws.amazon.com

Click:
Create an AWS Account

---

### Step 2: Enter Email and Account Name

Fill:
Root Email: your email  
AWS Account Name: shivanshi-aws (example)

Click:
Verify Email Address

Check your inbox for the code and confirm.

---

### Step 3: Create Password

Set and confirm your password.

Click:
Continue

---

### Step 4: Choose Account Type

Select:
Personal Account

Fill address and phone details.

Click:
Continue

---

### Step 5: Billing Setup

Choose:
UPI or Debit/Credit card

Enter details.

AWS may test with a small amount which is usually refunded.

Click:
Verify and Continue

---

### Step 6: Phone Verification

Enter OTP.

---

### Step 7: Support Plan

Choose:
Basic (Free)

---

### Step 8: Login Console

Open:
https://console.aws.amazon.com

Login with email and password.

---

# 3. ACCOUNT ACTIVATION NOTES

If you see:
"Complete your registration"

It means AWS is confirming your identity.

Solution:
- Wait 15–30 minutes
- Check email
- Refresh console

---

If you see:
"You are not eligible for free plan"

This means:
You are on Pay-As-You-Go

Only running services cost money.

---

# 4. IAM (IDENTITY AND ACCESS MANAGEMENT)

IAM controls who can access AWS.

Do NOT use root daily.

Create:

- Admin user (you)
- Viewer user (read only)

---

## 4.1 Create Admin User

Search:
IAM

Click:
Users → Create user

Name:
shivanshi-admin

Select:
Attach policies directly

Choose:
AdministratorAccess

Create User.

Enable console login.

Logout root → Login as admin.

---

## 4.2 Create Viewer User

Create user:
aparnesh.gaurav

Attach:
ReadOnlyAccess

This user can view but cannot modify.

---

# 5. AWS LAMBDA

Lambda lets you run code without servers.

You upload code and AWS runs it.

---

## 5.1 Create Lambda

Search:
Lambda

Click:
Create function

Name:
hello-lambda

Runtime:
Python 3.x

Create.

---

## 5.2 Code

Replace with:

def lambda_handler(event, context):
    return {
        'statusCode': 200,
        'body': 'Hello from AWS Lambda'
    }

Click:
Deploy

Test:
Run → Output should show Hello.

---

# 6. PYTHON DATA PROCESSING (PANDAS)

Install pandas locally:

pip install pandas

Example:

import pandas as pd
df = pd.read_csv("file.csv")
print(df.head())

---

# 7. AWS GLUE (APACHE SPARK)

Glue runs big data jobs with Spark.

No setup needed.

---

## Practical Glue Example

1. Upload CSV to S3 bucket
2. Create Glue Job
3. Paste:

from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("Demo").getOrCreate()
df = spark.read.csv("s3://your-bucket/data.csv", header=True)
df.show()
spark.stop()

4. Run job
5. View output
6. Delete job

---

# 8. VECTOR DATABASE

A vector database stores MEANING, not words.

Text → Numbers → Similarity search

Example:
"Google builds AI"
becomes
[0.8,0.7,0.4]

Search:
"AI company"

Returns:
"Google builds AI"

---

# 9. OPENSEARCH (VECTOR DATABASE)

OpenSearch stores vectors.

---

## Steps:

1. Create OpenSearch domain (smallest)
2. Open Dev Tools and create index:

PUT vectors-demo
{
  "mappings": {
    "properties": {
      "text": { "type": "text" },
      "vector": { "type": "knn_vector", "dimension": 3 }
    }
  }
}

3. Insert data:

POST vectors-demo/_doc
{
  "text": "Google builds AI",
  "vector": [0.8, 0.7, 0.4]
}

4. Search:

POST vectors-demo/_search
{
  "query": {
    "knn": {
      "vector": {
        "vector": [0.75, 0.7, 0.3],
        "k": 1
      }
    }
  }
}

5. Delete domain after test.

---

# 10. AWS BEDROCK

AWS Bedrock is a cloud service that lets you use **AI models** without building or training them.

In simple words:

You write a question → Bedrock sends it to an AI model → you get an answer.

You do **not** have to:

- Set up servers  
- Train models  
- Manage GPUs  
- Handle scaling  

AWS does all that in the background.

---

## 1.1 Why is Bedrock useful?

Because it lets you add AI to your applications **quickly and safely**.

You can:

- Build chatbots  
- Summarize long documents  
- Generate text  
- Classify text  
- Create embeddings (vectors)  
- Power semantic search  

All using AWS infrastructure.

---

# 2. WHAT CAN YOU DO WITH BEDROCK?

Here are some simple use cases:

- **Chatbot** – Answer user questions  
- **Summarization** – Reduce large text  
- **Rewrite** – Make text simpler or professional  
- **Translation** – Change language  
- **Text generation** – Blogs, emails, descriptions  
- **Embeddings** – Convert text to numbers for AI search  

---

# 3. HOW BEDROCK WORKS (CONCEPT)

Basic flow:

1. You send text input  
2. Bedrock sends it to an AI model  
3. AI generates a response  
4. You get output via Console or Code  

You do NOT touch model internals.

---

# 4. BEFORE USING BEDROCK

You must have:

- AWS account  
- IAM user with permissions  
- AWS console access  

For coding:

- AWS CLI installed  
- `aws configure` done  
- Python installed  
- boto3 library installed  

---

# 5. ENABLE AWS BEDROCK

## Step 5.1 Open Console

Search:

Bedrock

Click:

Amazon Bedrock

---

## Step 5.2 Request Model Access

1. Go to **Model access**
2. Click **Request access**
3. Select:
   - Text models
   - Embedding models
4. Submit request

---

## Step 5.3 Confirm Access

You will see:

✅ Enabled  
⏳ Pending  

Use any enabled model.

---

# 6. USING BEDROCK WITHOUT CODE (PLAYGROUND)

## Step 6.1 Open Playground

Go to:

Playgrounds → Chat / Text

---

## Step 6.2 First Prompt

Enter:

Explain cloud computing in simple words.

Click **Run**

---

## Step 6.3 Test More

Try:

- Summarize this paragraph  
- Rewrite in easy English  
- Write an email  
- Explain AI to a child  

---

# 7. USING BEDROCK WITH PYTHON

## 7.1 Install Library

``bash
pip install boto3

# 7.2 Configure AWS

Run:

aws configure

Enter:

- Access Key  
- Secret Key  
- Region (example: ap-south-1)  
- Output format: json  

---

# 7.3 Python Example (Text Generation)

``python
import boto3
import json

client = boto3.client("bedrock-runtime")

prompt = "Explain artificial intelligence simply."

response = client.invoke_model(
    modelId="YOUR_MODEL_ID",
    body=json.dumps({
        "inputText": prompt
    }),
    contentType="application/json"
)

print(response)

# 8. WHAT IS AN EMBEDDING?

An embedding is a numeric version of text.

### Example

"I love learning AI"

Becomes:

[0.23, 0.89, 0.11, 0.43]

---

# 8.1 Why embeddings matter?

They allow:

- Meaning-based search  
- Recommendations  
- AI recall  
- Smart chat  
- Vector databases  

# 9. CREATING EMBEDDINGS WITH BEDROCK

## Python Example

``python
import boto3
import json

client = boto3.client("bedrock-runtime")

text = "Cloud computing uses internet servers."

response = client.invoke_model(
    modelId="EMBEDDING_MODEL_ID",
    body=json.dumps({
        "inputText": text
    }),
    contentType="application/json"
)

print(response)

# 10. REAL SYSTEM FLOW

User
↓
Frontend
↓
Backend API
↓
AWS Bedrock
↓
Vector DB (OpenSearch)
↓
Response

yaml
Copy code

---

# 11. IAM PERMISSIONS

Bedrock needs:

- bedrock:InvokeModel  
- bedrock:ListFoundationModels  

---

## Example IAM Policy

``json
{
  "Effect": "Allow",
  "Action": [
    "bedrock:InvokeModel",
    "bedrock:ListFoundationModels"
  ],
  "Resource": "*"
}


# 12. COST AWARENESS

Charges occur for:

- Requests  
- Output size  
- Token usage  
- Embedding generation  

## Safety Rules

- Avoid loops  
- Test once  
- Monitor billing  
- Set budget alerts  

---

# 13. COMMON MISTAKES

Avoid:

- Not enabling models  
- Wrong model ID  
- Missing permissions  
- Infinite loops  
- Ignoring bills  

---

# 14. WHAT YOU NOW UNDERSTAND

You now know:

- What Bedrock is  
- How to enable it  
- How to use Playground  
- How to call via Python  
- What embeddings are  
- AI + Vector DB workflow  
- IAM permissions  
- Cost awareness  

---

# 15. FINAL STATEMENT

AWS Bedrock allows you to use AI without building AI.

Just input → AI output.

No infrastructure.  
No training.  
Only intelligence.


