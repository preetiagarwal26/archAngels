<h1>User Profile and Access Control Subsystem</h1>

<h2>Current Goal</h2>
Enable the right <strong>Farmacy Family</strong> users to access the right resources at the right times for the right reasons.

<h2>Assumption</h2>
An engaged user is a customer who registers / signs up on Farmacy Family and engages using communities, views resources available and consumes those resources.

<h2>Requirement</h2>
Engaged users can view all the information for all wellness providers and dieticians. They can choose wellness provider’s classes and dieticians to engage with.<br />
Wellness providers and dieticians can view basic information of the user they are engaged with. They may be allowed to view additional information like medical reports if a user grants them access.

<h2>Solution</h2>
We propose building services that use API to add users, upload reports, retrieve current access controls, etc. We will create a service that interacts with existing DynamoDB that stores user profile information.
We will leverage AWS's Cognito for identity and access management. Access Management basically helps us allow/disallow access to engaged user's information.
 
<h3>Data privacy</h3>
Security and privacy is also a matter of law, regulation, and contracts during data storage, transit and display. Data protection standards like HIPPA and the Sarbanes-Oxley Act in the U.S. enforce strict standards for data security. State regulations like the California Consumer Privacy Act (CCPA) also needs to be taken into account.
Amazon Cognito User Pools is a standards-based Identity Provider and supports identity and access management standards, such as OAuth 2.0, SAML 2.0, and OpenID Connect.
It also supports multi-factor authentication and encryption of data-at-rest and in-transit. Amazon Cognito is HIPAA eligible and PCI DSS, SOC, ISO/IEC 27001, ISO/IEC 27017, ISO/IEC 27018, and ISO 9001 compliant.

## Architecture Decision Record 

#### Title : Build an Identity and Access Management (IAM) system 

#### Context 
We need a solution to quickly integrate identity management and access control to be able to use Farmacy Family securely

#### Alternatives 
- Build our own IAM : We can build our own IAM sub-system that gives us the flexibility to add features and functionality when needed.
- [AWS Cognito](https://aws.amazon.com/cognito/) : AWS offers a service called Cognito which we use here to handle Farmacy Family’s authentication needs. Styling can be applied to brand all screens. It allows for other authentication providers to be hooked up. A practical example of this is giving the user the option to log in to Farmacy Family using their Google, Facebook, or other email and social media site login. The use of federation will generate trust in the system with a large portion of potential users.<br />
It supports non-federated authentication too. So, in the future, if Farmacy Family would like their own login and database, it would be easy to set that up. Cognito has all the necessary forms built-in to use on the login, logout, profile, etc. screens.

#### Decision 
The recommendation is to use AWS Congnito from the beginning. The reasoning is that cloud-based IAM is more secure, flexible, and oftentimes more cost-effective. A cloud IAM solution is more progressive, supporting a wide range of operating systems, platforms, and providers through one central console.<br />
At a later stage, when we are more confident and have the resources, we could develop our own IAM system and integrate it with Cognito without disrupting operations. 

#### Consequences
- Time to push the component live will reduce drastically if we do not have to design our own
- Cognito is generally up to date with compliance laws and regulations for data storage and transfer
- Password handling and management will not be our responsibility
- Engaged users do not have to remember an extra set of credentials, thus, providing ease of use
