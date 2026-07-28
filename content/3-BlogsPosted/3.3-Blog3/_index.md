---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# BUILDING A SERVERLESS AI ASSISTANT AT PELAGO: FROM CONCEPT TO CARE IN JUST TWO WEEKS

In the digital healthcare industry, the biggest challenge when scaling is how to maintain deep, personalized patient interactions without overwhelming the healthcare care team or reducing service quality. Pelago – a digital clinic specializing in the treatment and support of substance use disorders – solved this challenge by building an event-driven AI assistant on AWS in just two weeks.

However, in the healthcare sector, implementing Generative AI is not simply about calling an API of a Large Language Model (LLM). The engineering team must deal with strict challenges related to Protected Health Information (PHI) security, Human-in-the-loop requirements, and response latency when processing conversation histories spanning many weeks or even months.

To overcome these barriers, Pelago leveraged AWS Serverless and AI services such as Amazon Bedrock, AWS Lambda, Amazon DynamoDB, and Amazon SNS/SQS to create a secure, cost-efficient AI assistant system that could be deployed at record speed.

## 1. KEY HIGHLIGHTS:

**Event-Driven Architecture & Asynchronous Processing:** Instead of making coaches wait for AI-generated responses in real time when opening a conversation, the system listens for new messages from patients and triggers an asynchronous background processing workflow. As soon as the coach opens the chat, contextual response suggestions are already available.

**Human-In-The-Loop:** The system never automatically sends messages directly to patients. AI only acts as an "Assistant", generating suggestions and contextual considerations. The healthcare care team reads, evaluates, and adjusts the content before sending it to the patient, ensuring the highest level of clinical safety.

**Sensitive Healthcare Data Security (PHI Compliance) within a VPC:** All patient data and AI processing workflows operate entirely within Pelago's Amazon VPC infrastructure. Integration with Amazon Bedrock is performed securely, eliminating the risk of data leakage to the public Internet and strictly meeting healthcare data security requirements.

**Flexible Scaling & Cost Optimization with Serverless:** The entire solution uses a fully Serverless architecture (AWS Lambda, DynamoDB, SQS). The system automatically scales when message volume spikes and incurs no infrastructure maintenance costs when there is no traffic (pay-per-use).

**Shortening Time-to-Market:** By leveraging AWS fully managed services, Pelago was able to take the system from the concept stage to a production environment serving patients (care) in just 14 days.

## 2. REAL-WORLD SCENARIO:

A coach at Pelago has to simultaneously manage and communicate with dozens of patients undergoing treatment. Every message sent requires the coach to recall the entire conversation history, psychological developments, and health status from many weeks earlier. Manually compiling all this information is extremely time-consuming.

The standard Serverless & AI Assistant deployment architecture at Pelago is as follows:

*User Message Event → Amazon SNS / SQS → AWS Lambda (Context Orchestrator) → Amazon DynamoDB (Fetch History) → Amazon Bedrock (Generate Suggestions) → DynamoDB / Cache Store → Care Team Dashboard*
![Hình minh họa](/images/3-BlogsPosted/3.3-Blog3/blog3.png)


In this architecture:

* **User Message Event & Queuing (SNS/SQS):** When a patient sends a message, the event is immediately pushed into the queueing workflow to ensure high availability and prevent data loss.

* **AWS Lambda:** Acts as the central orchestrator. Lambda retrieves the conversation history from Amazon DynamoDB, builds a prompt containing the full long-term context, and sends the request to Amazon Bedrock.

* **Amazon Bedrock:** Receives the prompt and uses powerful foundation models (such as Anthropic Claude) to analyze the patient's intent and condition and provide the most optimal response suggestions.

* **Care Team Dashboard:** When the coach opens the application, the AI-generated suggestions have already been stored in DynamoDB and are displayed instantly on the interface, reducing the time required to compose messages from several minutes to just a few seconds.

### 3. CONCLUSION:

What I find impressive about Pelago's solution is how effectively they combined Serverless and Generative AI to solve a complex business problem in an extremely short time. Instead of spending months setting up servers, managing clusters, or self-hosting complex LLMs, they focused entirely on business logic and user experience.

Designing the system around an Event-driven architecture combined with Human-in-the-loop not only effectively addresses the latency challenges of LLMs but also ensures the highest level of safety – a critical factor in the healthcare industry.

In my opinion, this is a highly valuable real-world lesson for both Startups and large Enterprises: To successfully deploy AI, it is not necessary to invest in overly complex infrastructure. Making the most of Serverless services combined with Amazon Bedrock can help businesses turn innovative AI solutions into reality within just a few weeks, while ensuring security and optimizing operational costs.

## 4. Original Document Link:

https://aws.amazon.com/vi/blogs/architecture/building-a-serverless-ai-assistant-at-pelago-concept-to-care-in-two-weeks/
