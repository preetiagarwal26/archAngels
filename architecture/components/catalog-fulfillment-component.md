# Catalog & Fulfillment component

## Architectural Characteristics 
1. Adaptability : This system should be easy to plug into the existing architecture. This characteristic is super important to expedite delivery of this component and reduce time to market. 
2. Reliability 
3. Scalability

## Architecture Decision Record 
#### Title : Architecture for catalog and fulfillment of wellness and educational resources. 

#### Context
We need a system to maintain and view available resources like classes, courses, articles, videos and we need a system to process the ordering of these resources and finally the fulfillment or delivery of the resources.  

As mentioned earlier, we view this system as architecturally identical to the Meal Catalog and Meal Pickup systems. In fact the overall proposal is to generalize and abstract the Catalog component which can then be extended by existing Meal Catalog and new Education Catalog. Similarly we can introduce a fulfillment component that can be extended by the existing Meal Pickup and new Resource Delivery. 

#### Alternatives 
We already know that all the components in our existing architecture are modular monoliths. The decision lies in whether we want to use the existing event source based communication style or whether we want to move to a microservice based architecture. 

#### Decision 
Given that our top most architectural characteristic for this component is adaptability, we recommend using the existing event-source based style. This feature of engaging customers using educational resources is new and hence it makes sense to release and launch the feature with minimal developer effort and time to market. 

#### Consequences 
- Extremely adaptable as we simply use the existing frameworks with some refactoring to handle different types of orders : meal orders, educational resource orders. 
- Low time to market. 
- Reusing existing developer experience. 

## Catalog component

### Goal 
Content management for a catalog of educational and wellness resources like articles, in-person or virtual classes and other training resources. 

### Assumptions 
- Farmacy Food customers can still view the education catalog but can only order a resource if they are signed up as a Farmacy Family customer.
- The existing ordering subsystem including scheduling and ordering components as per archcollider’s solution are serving current business requirements and meeting SLAs. 
- The existing event source based architecture for Meal catalog is scaling to business requirements and meeting SLAs.  
- Currently the assumption is that none of the resources offered require payments but this can easily be lifted by again using the existing payment subsystem. 

### Requirement 
Enhance Catalog system to view educational and training resources, sign up / order / purchase resources. 

### Input 
- Customer token to authenticate and authorize. 
- Customer command to view current resources. 
- Customer command to select / sign up for a resource. 

### Output / Action 
- Based on different resources the action may be different like reserving a seat in a class. 
- Send order confirmation. 

### Working System 
1. User views and selects a wellness course to enroll in. 
2. Selection of the course generates an event that contains the customer token that can be used to verify the role of the customer. The customer is allowed to process only if they belong to the Farmacy Family role. 
3. User confirmation of course order will generate an event that is consumed by the Ordering subsystem or the scheduling subsystem depending on the type of course. (The Scheduling subsystem may be used to fulfill a course order at a later time.)
4. The Ordering subsystem reserves the seat for the customer and generates an event consumed by the catalog to update the remaining seats (if applicable). 
5. A record of the order is also maintained in the existing Event Store and can be viewed by the customer under purchased orders. 

## Fulfillment component 

### Goal 
Ability to fulfill the orders i.e. deliver the resource that was ordered / purchased by the customer. 

### Assumptions 
- It was not clear how a training resource is delivered to an engaged customer. While the mobile app itself can be enhanced to make it a platform to view articles and videos, as the first step we would recommend a simpler approach to resource delivery like using emails. 
- Existing notifications subsystem meets the current requirements and is scalable to satisfy additional push use cases like delivery of education resources. 

### Requirement 
Support different implementations to fulfill different order types. 

### Input 
- Order successfully purchased event. (Here the term order is used as a general term which applies to both order types : meals and educational resources. Similarly the term purchase is used to indicate meal payments, course sign ups, content viewing request)

### Output / Action
- Different fulfillment implementations based on order type. 
  - Meal purchase event is fulfilled using Meal pickup. 
  - Course sign ups and content viewing requests can be initially fulfilled by sending links to the hosting platforms as emails.

### Working system 
1. System receives an Order successfully purchased event. For example : “Course Seat Reserved”.
2. Based on the type of order system triggers the respective fulfillment subsystem : Meal Pickup or Resource Delivery. In the example above, the Resource Delivery subsystem is triggered.
3. Fulfillment subsystem fulfills the order. Resource Delivery subsystem uses the existing Notifications subsystem to deliver the details (like zoom link) of the course the user registered for. 
