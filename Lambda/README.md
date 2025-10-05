
# ☁️ AWS Lambda

- AWS Lambda is a serverless computing service provided by Amazon Web Services (AWS).

- It lets you run your code without managing any servers.

- You just write your function, upload it, and AWS takes care of:

- provisioning servers

- scaling automatically

- running the code only when needed

- You only pay for the time your code runs, not for idle time.


#### Normally, when you run code on a server (like EC2), you need to:

- Start the server

- Install software

- Keep it running all the time

- With Lambda, you don’t do any of that.

#### Instead:

- You just upload your code (as a function).

- AWS runs it automatically when something happens — like:

- A file is uploaded to S3

- An API request is made

- A database changes

-  schedule triggers it (like a cron job)

- Then AWS stops it when done — no server is running continuously.

## ⚙️ How Lambda Works 

- You write a function (in Python, Node.js, Java, etc.).

- You set a trigger (an event that tells Lambda when to run).

- When the trigger happens — AWS automatically:
Starts a temporary container

- Runs your function code

- Returns the result

- Shuts down the container

- Everything is managed by AWS — you never see or manage the server.

## 💰 Billing

You pay only for:

Number of requests

Execution time (in milliseconds)

## ✅ Free Tier:

- 1 million requests per month free

- 400,000 GB-seconds of compute time free

## ⚠️ Limitations of AWS Lambda

Even though AWS Lambda is powerful, it has certain limitations and drawbacks to be aware of:

| Limitation | Description |
|------------|-------------|
| Execution Time Limit | Each Lambda function can run for a maximum of 15 minutes. Not suitable for long-running tasks. |
| Cold Start Delay | If a function hasn’t been used for some time, startup can take longer (cold start). |
| Memory and Storage Limit | Max memory: 10 GB, Temp storage (`/tmp`): 512 MB only. |
| Stateless Nature | Lambda doesn’t store data between runs; you need S3 or DynamoDB for state persistence. |
| No GPU Support | Not suitable for deep learning training or GPU-heavy workloads. |

## 🧠 When to Use AWS Lambda

### Ideal For:

- Event-driven short tasks

- Lightweight automation

- API backends

- File processing (e.g., S3 uploads)

### Avoid For:

- Long-running background jobs

- Heavy computation (ML model training)

- GPU or high-memory workloads