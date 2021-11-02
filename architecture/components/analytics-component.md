# Analytics Component

## Current Goal 
Analytics component that builds, trains and deploys machine learning models on data gathered from within the Farmacy Food backend as well as third party integrations like data from clinics, data from smart fridge endpoints. 

## Assumptions 
- In general, recommendation systems, personalization systems, trends reporting systems, etc. receive their input as huge batches of data (usually on HDFS) that may be generated periodically (hourly, daily, weekly, etc.). So here we are assuming that periodic batches of raw input data from various sources is available. For internal systems, Farmacy Foods backend systems will be responsible for taking backups or snapshots. AWS provides [AWS Backup](https://aws.amazon.com/blogs/database/set-up-scheduled-backups-for-amazon-dynamodb-using-aws-backup/) that can be used for this purpose. 

## Requirements
- System must process huge batches of data
- System must santize, aggregate and process raw input data 
- System must build, train and deploy machine learning models 
- System must derive, store and serve inferred data 
- Inferred data can be queried using SQL like query language
- API support to query certain derived data for example "Targeting content for user X".

## Inputs 
- Geographical trend analytics data 
  - Smart fridge Data (like food wasted, food ordered, food in popular demand, etc.) from different geographical locations backed up to S3 which is a global service. 
  - Other third party data sources may exist like geographical data from clinics or other health and wellness institutes (like changes in diets, new super food in town, cultural shift in eating habits, etc.). 
- Anonymized medical results history for Farmacy customers 

## Outputs 
- Tables capturing important attributes derived from geo data. Important attributes may include scores on popular food items, optimum quantity of food item needed based on population and popularity, etc. Table may answer questions like : 
  - What’s the probability x food item will be wasted in a particular geo location? 
  - What’s the optimum quantity of x food item that should be ordered?
- Aggregated tables based on the medical history of customers. Answering questions like : 
  - Precentage improvement in blood sugar for patients with diabetic history. 
  - Percentage improvement in metric x for people who belong in community y. 
  - Number of new Farmacy Family customers added

## Use Cases 
- The output tables above can be used to query and generate reports that can help formulate strategies to reduce waste, reports for presenting to investors, etc. 
- The output tables can be queried to view data for different periods of time i.e it can feed the existing Reporting subsystem. 

## Architecture characteristics 
- Security : To produce marketing data or data for investors we want to see users’ improvement which involves analyzing personal medical data. All data that is being used should be anonymized. The recommendation is to not use data that can personally identify a user. This would mean using a pseudonomous identifier in this system which should not be mapped to the user identifier used in identity management systems. This also means processing data like changing birthdates to age groups, etc. 
  - In fact, given the mission statement of Farmacy Food and how they want to use medical information to provide meals to people, an important future recommendation would be to invest a few resources in the latest research on [differential privacy](https://towardsdatascience.com/understanding-differential-privacy-85ce191e198a) and [privacy preserving machine learning](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.678.8298&rep=rep1&type=pdf).
- Extensibility : Should be easy to support more use cases i.e. derive more trends or support answering some other specific questions. 

## Architecture Decision Record 

#### Title : Build, train and deploy machine learning models 

#### Context 
While it is easy to get the input and dump it in S3, we still need a solution to effectively build and deploy different machine learning models based on different use cases. 

#### Alternatives 
- [AWS Personalize](https://aws.amazon.com/machine-learning/ml-use-cases/personalization/) : This is a no-prior experience required machine learning based personalization system. The main advantage of using this would be to quickly deploy a personalization solution without spending much time training the developer team. This solution would be a good fit to get recommendations to send targeting emails to Farmacy Food customers (models can be trained using Farmacy Food customers' previous purchases along with data from current Farmacy Family customers who have similar habits.). 
- [AWS SageMaker](https://aws.amazon.com/sagemaker/) : Using this requires some experience but provides greater flexibility to deploy different types of models that can support different use cases. 

#### Decision 
The recommendation is to use AWS SageMaker from the beginning. The reasoning is that AWS Personalize may end up supporting a very limited use case that may not even be a very useful use case to support initially. For example, Farmacy food customers can be targeted initially with some static content about the benefits of Farmacy Family. At a later stage we can mature our targeting and provide more personalized course and community recommendations. 

Learning from data is a key business driver and hence it's better to train the developers to user AWS SageMaker from the very start. 

#### Consequences
- Time to market may be a little higher for some types of queries. 
- Future proof recommendation as the investment in time right now would be very fruitful in quickly deriving interesting trends and reports. 

## Process 
1. Batches of data can be captured in S3. (Do cost analysis.)
2. S3 batch generation triggers Amazon Data Pipeline that can run hadoop jobs to process the data on AWS EMR (Elastic Map Reduce) cluster. 
3. The Map reduce job can sanitize, process, aggregate inputs. 
4. AWS Personalize or AWS Sage Maker can be used to build, train and deploy machine learning models. 
5. The output tables that are mainly to be queried for reports or used for manual queries to get data for investors can be dumped in S3 and Athena can be used to query that data on demand. 
6. Inferred data that needs to be queried by APIs and may have lower latency requirements can be put in DynamoDB. 

