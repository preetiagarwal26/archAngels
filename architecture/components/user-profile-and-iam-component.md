<h1>User Profile and Access Control Subsystem</h1>

<h2>Current Goal</h2>
Enable the right <strong>Farmacy Family</strong> user's to access the right resources at the right times for the right reasons.

Assumptions
An engaged user is a customer who registers / signs up on Farmacy Family and engages using communities, views resources available and consumes those resources.

<h2>Requirement</h2>
Engaged users can view all the information for all wellness providers and dieticians.
Wellness providers and dieticians can view basic information of the customer they are engaged with. They may be allowed to view additional information like medical reports if a user grants them access.

<h2>Solution</h2>
We propose building services that use API to add users, upload reports, retrieve current access controls, etc. We will create a service that interacts with existing DynamoDB that stores user profile information.
We will leverage AWS's Cognito for identity and access management. Access Management basically helps us allow/disallow access to engaged user's information.
 
<h3>Data privacy</h3>
Security and privacy is also a matter of law, regulation, and contracts during data storage, transit and display. Data protection standards like HIPPA and the Sarbanes-Oxley Act in the U.S. enforce strict standards for data security. State regulations like the California Consumer Privacy Act (CCPA) also needs to be taken into account.
Amazon Cognito User Pools is a standards-based Identity Provider and supports identity and access management standards, such as OAuth 2.0, SAML 2.0, and OpenID Connect.
It also supports multi-factor authentication and encryption of data-at-rest and in-transit. Amazon Cognito is HIPAA eligible and PCI DSS, SOC, ISO/IEC 27001, ISO/IEC 27017, ISO/IEC 27018, and ISO 9001 compliant.
