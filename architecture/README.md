# Solution 

Existing system : https://github.com/ldynia/archcolider 

## Overview 

The following component diagram shows the new components added to [archcollider's system](https://github.com/ldynia/archcolider/blob/4a71575e64fb4e28a284f3bc063169ce7082668c/img/FF_system_approach.png).
The main purpose of extending archcollider's original component diagram is to ease understanding and give an overall picture of how our new components fit 
into the existing solution. We believe that this diagram is extremely important to ensure our solution can be easily adapted and integrated into the existing 
architecture. 

![alt text](https://github.com/preetiagarwal26/archAngels/blob/main/architecture/component-diagram.jpg "Component composition and communication")

### Components 

- **Catalog and Fulfillment** :  From an architectural point of view, the design, architecture, flow of information remain the same as the original archcollider's 
Meal Catalog and Meal Pickup. We can generalize these components into Catalog and Fulfillment respectively. The main idea behind this is that whether a user chooses 
a meal from the Meal Catalog, a class from the Education Catalog or a community to join from the Community Catalog, architecturally these are all identical actions. 

  The only place where these actions differ is the way in which these actions are fulfilled. So while we use Meal Pickup to fulfill a meal purchase, we use Resource Delivery to fulfill the purchase of other resources. Just like some meal purchases may be scheduled and/or ordered (using the Order Processing subsystem), classes, articles, wellness information, etc. can also be scheduled and/or ordered. Just like meal purchases can be prepaid or paid in real time, education resources "can" also be prepaid or paid for in real time as per the business requirements. 

  So the overall recommendation for this component is simply to use the reactive monolith as it is present today. We simply define an overall interface for Catalog and that can be extended by Meal Catalog, Education Catalog, Community Catalog, and any other catalog in future. Similarly Fulfillment defines a common interface that is extended by Meal Pickup and Resource Delivery and each of the different types of catalogs refer to their specific fulfillment implementation. 
  
- **Community forum & chat** : This sub-component can be viewed as a second way to communicate with the customers. The notifications sub-component can be viewed as a “push model” for community engagement while the Community forum and chat is an implementation of the “pull model”.  We view this sub-component as the medium for fulfilling orders of the type Education Catalog and Community Catalog as mentioned above. Given the complexity of owning such a system, our initial recommendation is to use an open source library deployed in the existing network (AWS). <TODO : Add technology recommendations. See if AWS has something already.>
- **User Profile** : 
- **Access Control** : 
- **Analytics** : The component is responsible for running machine learning algorithms on batches of data to derive models that can be used to infer behaviors, trends, recommendations, etc. This component has the ability to receive its inputs from several systems which may be internal like the End-user offerings subsystem, Order processing subsystem and external systems like Smart Fridge, Ghost kitchens, etc. More data from different systems can enable this component to make smarter and more personalized recommendations. This component can then feed the Personalization component discussed below, or can even be used by the existing Reporting subsystem to prepare reports and dashboards that can be used to see various trends like users added, health improvement over a period of time, food wastage improved over a period of time, etc. 
- **Personalization** : The Personalization component leverages the intelligence derived from the Analytics component to personalize user experience. For now, based on the current requirements, it’s simply used to target the transactional customers to encourage them to become engaged customers. In future, this component can be extended to send periodic personalized recommendations to all users, to personalize user experiences in the front-end app, etc. 

