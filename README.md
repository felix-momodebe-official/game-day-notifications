# NBA Game Day Notifications / Sports Alerts System

## **Project Overview**
This project is an alert system that sends real-time NBA game day score notifications to subscribed users via SMS/Email. It leverages **Amazon SNS**, **AWS Lambda and Python**, **Amazon EvenBridge** and **NBA APIs** to provide sports fans with up-to-date game information. The project demonstrates cloud computing principles and efficient notification mechanisms.

---

## **Features**
- Fetches live NBA game scores using an external API.
- Sends formatted score updates to subscribers via SMS/Email using Amazon SNS.
- Scheduled automation for regular updates using Amazon EventBridge.
- Designed with security in mind, following the principle of least privilege for IAM roles.

---

## **Technical Architecture**
- **Cloud Provider**: AWS
- **Core Services**: SNS, Lambda, EventBridge
- **External API**: NBA Game API (e.g., SportsData.io, BallDontLie, or RapidAPI)
- **Programming Language**: Python 3.x
- **Dependencies**:
  - `boto3`: AWS SDK for Python
  - `requests`: HTTP requests for NBA API
- **IAM Security**:
  - Least privilege policies for Lambda, SNS, and EventBridge.

---

## **Project Structure**
```bash
game-day-notifications/
├── src/
│   ├── lambda_function.py               # Main Lambda function code
├── policies/
│   ├── sns_publish_policy.json          # SNS publishing permissions
│   ├── eventbridge_invoke_policy.json   # EventBridge to Lambda permissions
│   └── lambda_execution_policy.json     # Lambda execution role permissions
├── .gitignore
├── requirements.txt                     # Python dependencies
└── README.md                            # Project documentation
```

## **Setup Instructions**

### **Clone the Repository**
```bash
git clone https://github.com/YourGitHubUsername/nba-game-alerts.git
cd nba-game-alerts
```

### **Install Dependencies**
```bash
pip install -r requirements.txt
```


### **Create an SNS Topic**
1. Open the AWS Management Console.
2. Navigate to the SNS service.
3. Click Create Topic and select Standard as the topic type.
4. Name the topic (e.g., game_day_not_topic) and note the ARN.
5. Click Create Topic.


### **reate an IAM Role for Lambda**
1. Open the IAM service in the AWS Management Console.
2. Click Roles → Create Role.
3. Select AWS Service and choose Lambda.
4. Attach the following policies:
  - SNS Publish Policy (sns_publish_policy.json)
  - EventBridge Invoke Policy (eventbridge_invoke_policy.json)
  - Lambda Execution Policy (lambda_execution_policy.json)SNS Publish Policy, EventBridge Invoke Policy, Lambda Execution Policy
5. Name the role (e.g., game_day_not_role) and create it.
6. Copy and Save the ARN of the role.


### **Deploy the Lambda Function**
1. Open the AWS Management Console and navigate to the Lambda service.
2. Click Create Function.
3. Select Author from Scratch.
4. Enter a function name (e.g., game_day_notifier).
5. Choose Python 3.x as the runtime.
6. Assign the IAM role created earlier (game_day_not_role) to the function.
7. Under the Function Code section:
- Copy the content of the src/game_day_notifier.py file from the repository.
- Paste it into the inline code editor.
8. Under the Environment Variables section, add the following:
- NBA_API_KEY: your NBA API key.
- SNS_TOPIC_ARN: the ARN of the SNS topic created earlier.
9. Click Create Function.


### **Set Up Automation with Eventbridge**
1. Navigate to the CloudWatch service in the AWS Management Console.
2. Go to Rules → Create Rule.
3. Select Event Source: Schedule.
4. Set the cron schedule for when you want updates (e.g., hourly).
5. Under Targets, select the Lambda function (game_day_notifier) and save the rule.


### **Test the System**
1. Open the Lambda function in the AWS Management Console.
2. Create a test event to simulate execution.
3. Run the function and check CloudWatch Logs for errors.
4. Verify that SMS notifications are sent to the subscribed users.


### **What We Learned**
1. Designing a notification system with AWS SNS and Lambda.
2. Securing AWS services with least privilege IAM policies.
3. Automating workflows using EventBridge.
4. Integrating external APIs into cloud-based workflows.


### **Future Enhancements**
1. Add NFL score alerts for extended functionality.
2. Store user preferences (teams, game types) in DynamoDB for personalized alerts.
3. Implement a web UI
