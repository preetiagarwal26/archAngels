# Personalization component

## Current Goal 
Increase conversion of transactional customers to engaged customers. 

## Assumptions 

- Transactional customers interact with Farmacy Food in 2 ways : 
  1. Mobile App : Contact information is either obtained during check out or the email linked with the credit card is obtained. 
  2. Smart Fridges : Email linked with credit card is obtained.
- It’s not clear as to how the Point of sale / smart fridge interfaces interact with the Farmacy Food backend. Is it a synchronous or an asynchronous update? 
Is it event source based or an API call to Farmacy Food backend. 
  
  Note : Irrespective of how this works, it seems like a good recommendation for Farmacy Food to maintain a data store (maybe DynamoDB) of transactional customers 
  along with their emails / preferred contact information. If the smart fridges interact with Farmacy backend systems using events, those events can then be used 
  to update a database (like DynamoDB). This data store can then even be used at a later time for other periodic (monthly) marketing of special discounts or events. 
- The definition of an engaged customer, is a customer who registers / signs up on the Mobile app and engages in the app using communities, views resources available and consumes those resources.

## Requirement 
Asynchronous system that sends targeted emails to transactions customers to incentivize them into engagement. 

## Input 
- Email address for customer to target. 
- Targeting information to send to the customer. May be static or personalized for the customer. 

## Output / Action
Send email with engagement opportunities and Farmacy Family benefits to targeted customers. 

## Architectural Characteristics 
- Cost : This system is not critical to the main business operations of Farmacy Food and hence the priority is low cost setup with low maintenance. 
- Reliability : This system is fairly important to send marketing emails and attract more engaged users for Farmacy Family and hence the system should be fairly reliable. 
- Scalability : Like most systems it should be easy to scale this system to incorporate more input events from transactional customers. 

## Architecture Decision Record 

### Title : Architecture for targeting transactional customers 

### Context 
We need an asynchronous system to send emails to transactional customers. Since this is an internal system which means we have some flexibility over how we want to model the input data.

### Alternatives  
The input to this system is a transaction customer/customers with some contact information like email. There are a few alternatives to implement this system : 
1. Cron job like scheduling to send emails to a batch of transactional customers. 
  - The targeting system would operate like a periodic cron job, let’s say hourly, that takes a batch of transactional customers added in the last hour (configurable parameter) and sends targeting emails to them. 
  - Input preparation would then require some work: 
    1. One option is to query the transactional customers in the past hour if this information is stored in a data store like DynamoDB. 
    2. The second option is to set up something like Kinesis Firehose to collect one hour worth of transactional events (in a Kinesis stream) and then dump them to S3. The S3 dump would trigger the targeting system to send out emails. 
  - This option suffers from 2 main disadvantages : 
    1. It requires the input to be in very specific formats which may not necessarily be very useful for other future components. Input preparation option (i) requires the data to be stored efficiently enough to support a query to return past hour customers. Input preparation option (ii) seems to produce an output that may not be useful for any future use cases. We may also have to setup systems to clean up past data from S3 buckets to reduce cost. 
    2. Results in delayed communication. Based on how often this system runs hourly vs daily or another parameter, it may not be very fruitful to send targeting emails a significant period after a customer has made a transaction. We can further look into this point and back this claim by data that might suggest an appropriate period of time window to send customers targeting emails. 

2. Event triggered upon a successful transaction from a customer. 
- A transactional event generated upon successful transaction by a customer can be directly consumed by this targeting system. Though, as mentioned above, we recommend that such an event be first used to update the DynamoDB table of transactional customers and then a successful DynamoDB update can be consumed using DynamoDB stream to trigger an email. 

### Decision  
The second option is simple and involves less components to maintain. It also makes a recommendation to maintain a DynamoDB table of transactional customers which is more future proof than the recommendations made in option 1. 

### Consequences  
- Low cost. We only need to consume kinesis/ dynamodb stream events which can trigger the targeting system using AWS Lambda that sends the targeting email. 
- AWS Kinesis and AWS Lambda are very reliable and scalable components and require very low maintenance. 
- This event based model may lead to multiple emails to the same customer over a short period of time if the same customer makes multiple different transactions. Before designing a solution for this, it will be worthwhile to look into some data points about how often this happens.

## Working system 
- When a transactional customer successfully interacts with Farmacy Food, it generates an event. 
- The event is consumed and triggers the targeting system (AWS Lambda) either directly or via the DynamoDB table update. 
- AWS Lambda queries the Analytics component to retrieve a personalized targeting email content or uses some static email content. 
- The lambda then uses the notification subsystem to send the email to the customer. 
