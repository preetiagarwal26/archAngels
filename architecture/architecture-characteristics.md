<h2>Top Architecture Characteristics</h2>

S.No.|Characteristic|Why
-----|--------------|---
1|Cost| - Farmacy Foods is a startup firm with limited resources. We propose to reduce cost by using open source libraries and reusing services provided by AWS. 
2|Adaptablity| - Farmacy Family is an extension to Farmacy Foods. New components should be adaptable to existing system and should provide seamless integeration. 
3|Agility| - Solution should be delivered quickly. Time to market could a constraint here. Suggest to have less in-house build components 
4|Security| - Farmacy Family plan to store customer's PII (Personal Identifiable Information), EMR (Electronic Medical Record). Data compliance, governance should be taken into consideration. <br/>- We offer storing data in <strong>Amazon S3 layer</strong>, and accessed via <strong>AWS HIPPA eligible services</strong>. 
5|Feasibility & Simplicity| - Prefer pay-as-you-go instead of owning infrastructure and licenses.
6|Extensibility|Farmacy Foods is in the growth phase and is likely to constantly add products and features.
7|Scalability|Farmacy Foods had ambitious growth plans and the architecture should scale with growing business and community.


<h2>Architecture Styles</h2>

Considering above -ilities, we narrowed down architecture style to following:-
  * Microkernel
  * Event-driven only
  * Microservices only

<h3>Microkernel</h3>
  A style consisting of two types of components <strong>core</strong> , <strong>plugin</strong>. <br/> In future if we were to add more third parties such as Gym, Therapist etc. They could potentially be added as plugin to existing system. <br/> However, one could argue they could be managed as separate identity in identity management system.<br/> This style may be more suitable for insurance, claims system.

<h3>Event-driven only</h3>
  Components like <strong>Personalization</strong>, <strong>notification</strong> are asynchronous by nature, hence more suitable for event-driven style.

<h3>Micorservices only</h3>
   Farmacy Family has components like <strong>User Profile and Access Control</strong>. This component needs to validate identity and respond back synchronously to proceed further. Only event-driven style would not serve stated purpose.
  
<h3>Hybrid</h3>
 Finally, we propose an style that is a mix of monolith, event driven, microservices. Component level style can be found in <strong>Solution</strong> section
   
<h2>References</h2>
https://learning.oreilly.com/videos/software-architecture-fundamentals/9781491998991/ <br/> https://aws.amazon.com/blogs/architecture/store-protect-optimize-your-healthcare-data-with-aws/ <br/> https://aws.amazon.com/compliance/hipaa-eligible-services-reference/ 
