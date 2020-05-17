# Integrate Slack and Salesforce in 20 mins! 💬🌩️🌐
### Presented at VirtualDreamin'20
![Recording-_331](https://user-images.githubusercontent.com/16715515/82121440-af546680-97aa-11ea-864d-da0d06ebdcfe.gif)

## 📺 Walkthrough
1. Slide Deck - https://docs.google.com/presentation/d/1Qsz_CFvs-1qHIRwkMjlp_7vP8ynY7blh/edit#slide=id.p1
2. Video Walkthrough - Coming Soon!
3. Q & A - Coming Soon!

## 🛠️ How is this done (5 simple steps!)?

This is achieved using the new **Workflow Builder** feature in Slack and **External Services** in Salesforce. Here are the steps in brief:

1.  Using the **Slack Workflow Builder**, create and publish a Workflow that post messages into a _Slack Channel_ and is triggered by a **Webhook**. Read for more info: [https://slack.com/intl/en-in/help/articles/360035692513-Guide-to-Workflow-Builder](https://slack.com/intl/en-in/help/articles/360035692513-Guide-to-Workflow-Builder).

2.  Construct a **Swagger Schema** for the Webhook provided by Slack (_in Step 1_). Use the **Template** given below to get started.

3.  Created a **Named Credential** in Salesforce with URL - [https://hooks.slack.com](https://hooks.slack.com). (_No Auth_)

4.  Import the Swagger Schema constructed in Step 2 using **External Services**.

5.  Create a **Flow** as shown below:
![image](https://user-images.githubusercontent.com/16715515/82121553-9f895200-97ab-11ea-82d3-6e6aaa94f5d4.png)

## 📋 Template Swagger Schema
```json
{
  "swagger": "2.0",
  "info": {
    "title": "Slack + Salesforce",
    "description": "Instantly Send Messages to Slack from Salesforce",
    "version": "1.0.0"
  },
  "host": "hooks.slack.com",
  "schemes": [ "https" ],
  "paths": {
    "[REPLACE THIS WITH YOUR WEBHOOK]": {
      "post": {
        "consumes": [ "application/json" ],
        "parameters": [
          {
            "in": "body",
            "name": "slackMessageRequest",
            "type": "object",
            "required": true,
            "schema" : {
              "$ref" : "#/definitions/SlackMessageRequest"
            }
          }
        ],
        "responses": {
          "200": {
            "description": "Successful Operation"
          }
        }
      }
    }
  },
  "definitions": {
    "SlackMessageRequest": {
      "type": "object",
      "properties": {
        "message": {
          "type": "string"
        }
      }
    }
  }
}
```
> ⚠️ Note: To **validate** a Swagger Schema (_written by yourself_), visit - [http://editor.swagger.io/](http://editor.swagger.io/).

> ⚠️ Note: Please DO NOT forget to replace `[REPLACE THIS WITH YOUR WEBHOOK]` in the above _Template Swagger Schema_ with the Webhook of your Slack Workflow.

## 🔗 Resources
1. Trailhead [https://trailhead.salesforce.com/en/content/learn/modules/external-services](https://trailhead.salesforce.com/en/content/learn/modules/external-services)
2. Blogs [https://shrutisridharan.wordpress.com/tag/external-services/](https://shrutisridharan.wordpress.com/tag/external-services/)
