## **AUTO NBA SPORTS ALERT SYSTEM**

**The Project Overview**
This very  project is a smart alert system built to deliver all specified  real-time NBA game day scores notifications to subscribed users to either their SMS and email(which ever is preferable by the user). It leverages AWS services such as the  SNS, Lambda, and EventBridge working  with the NBA API, made to  provide sports fans with all  up-to-date game information. This project emphazises on  cloud computing principles and as well  efficient notification mechanisms.

## *The Project architecture **
![NBA NOTIFICATION ARCH](https://github.com/user-attachments/assets/0e31b93d-d6f9-4565-82c3-d455eba958d9)


## **Project Features**
-It Fetches live NBA game scores using the NBA Game API.
-Sends formatted score updates to subscribers via SMS and email through Amazon SNS.
-Automates regular updates using Amazon EventBridge schedules.
-Implements  the principle of least privilege for IAM roles for security reasons.


## **Technologies used**
-AWS (SNS,EVENT BRIDGE,LAMBDA)

-NBA GAME API FROM [sportsdata.io](https://sportsdata.io/)

-PYTHON 3X.

-IAM for securing the AWS SERVICES.

## **Project file Structure**
```
DAY 2/
├── src/
│   ├── gd_notifications.py          # Main Lambda function code in pyhton
├── policies/
│   ├── gd_sns_policy.json           # SNS publishing permissions
│   ├── gd_eventbridge_policy.json   # EventBridge to Lambda permissions
│   └── gd_lambda_policy.json        # Lambda execution role permissions
├── .gitignore
└── README.md                        # Project documentation falls here

```

## **Setup guide made to assit you**


### **Clone the Repository**
```

git clone https://github.com/Maurice-Makafui/notification-for-NBA-game-day.git

```

### **Creating an SNS Topic**

1. Log into your  AWS Management Console.
2.  Search  the SNS service.
3. Click Create Topic and select Standard as the topic type.
4. Name the topic (e.g., Maurice_NBA_Topic) and note down the ARN generated.
5. Click Create Topic.


### **Adding your  Subscriptions to the SNS Topic**

1. After creating the topic, click on the topic name from the list.
2. Navigate to the Subscriptions tab and click Create subscription.
3. Select your  preferred Protocol:

- For Email:
  - Choose Email.
  - Enter a valid email address.



- For SMS (phone number):
  - Choose SMS.
  - Enter a valid phone number in international format (e.g., +23327711534).



4. Click Create Subscription.


5. If you added an Email subscription:

- Check the inbox of the provided email address.
- Confirm the subscription by clicking the confirmation link in the email.

6. For SMS, the subscription will be immediately active after creation.


### **Creating  the SNS Publish Policy with AWS IAM**

1. Navigate to  the IAM service in the AWS Management Console via the search button.
2. Navigate to Policies and click on Create Policy.
3. Click JSON and paste the JSON policy from maurice_sns_policy.json file
4. Replace the REGION and ACCOUNT_ID with your AWS region and account ID.
5. Click Next: Tags (optional though).
6. Click Next: Review.
7. Enter a name for the policy (e.g., maurice_sns_policy).
8. Review and click Create Policy.


### **Create an IAM Role for Lambda**

1. Open the IAM service in the AWS Management Console.
2. Click Roles and  Create Role.
3. Select AWS Service and choose Lambda.

4. Attach the following policies:
- SNS Publish Policy (maurice_sns_policy) (check the previous step).
- Lambda Basic Execution Role (AWSLambdaBasicExecutionRole) (an AWS managed policy).

5. Click Next: Tags (optional to).
6. Click Next to  Review.
7. Enter a name for the role (e.g., maurice_role).
8. Review and click Create Role.
9. Copy and save the ARN of the role for use in the Lambda function.



### **Deployment of  the Lambda Function**

1. Open the AWS Management Console and navigate to the Lambda service.
2. Click Create Function.
3. Select Author from Scratch.
4. Enter a function name (e.g., maurice_notifications).

5. Choose Python 3.x as the runtime.
6. Assign the IAM role created earlier (maurice_role) to the function.
7. Under the Function Code section:



- Copy the content of the src/maurice_nba_notifications.py file from the repository.



- Paste it into the inline code editor.
8. Under the Environment Variables section, add the following:
- NBA_API_KEY: your NBA API key.
- SNS_TOPIC_ARN: the ARN of the SNS topic created earlier.
(This practice is to secure your info and env)

9. Click Create Function.



### **Setting  Up the  Automation  AWS  Eventbridge**

1. Navigate to the Eventbridge service in the AWS Management Console.


2. Go to Rules → Create Rule.
3. Select Event Source: Schedule.
4. Set the cron schedule for when you want updates (e.g., Daily).


5. Under Targets, select the Lambda function (maurice_notifications) and save the rule.


### **Ensure you test the System**

1. Open the Lambda function in the AWS Management Console.
2. Create a test event to simulate execution.
3. Run the function and check CloudWatch Logs for errors.
4. Verify that SMS notifications are sent to the subscribed users


### **What I Learnt**
1. Designing a notification system with AWS SNS and Lambda.
2. Securing AWS services with least privilege IAM policies.
3. Automating workflows using EventBridge.
4. Integrating external APIs into cloud-based workflows.



### **Future Enhancements**

1. Support for Multiple Sports:
 -Extend the system to include notifications for other sports like soccer, baseball, tennis, or hockey.

2. Enhanced Personalization:
 -Allow users to set preferences for:
 -Favorite teams or players.
 -Types of updates (e.g., live scores, game summaries, injury reports, trade updates).
 -Frequency of notifications.

3. Advanced Analytics Dashboard: 
 -Create a web-based dashboard to provide:
 -Real-time game analytics.
 -Historical performance trends for teams and players.