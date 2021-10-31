<h2>Top Architecture Characteristics</h2>

S.No.|Characteristic|Why
-----|--------------|---
1|Cost| - Farmacy Foods is a startup firm with limited resources. We propose to reduce cost by using open source libraries and reusing services provided by AWS. 
2|Agility| - Solution should be delivered quickly. Time to market could a constraint here. Suggest to have less in-house build components 
3|Security| - Farmacy Family plan to store customer's PII (Personal Identifiable Information), EMR (Electronic Medical Record). Data compliance, governance should be taken into consideration. <br/>- We offer storing data in Amazon S3 layer, and accessed via AWS HIPPA eligible services. 
4|Feasibility & Simplicity| - Prefer pay-as-you-go instead of owning infrastructure and licenses.
5|Extensibility|Farmacy Foods is in the growth phase and is likely to constantly add products and features.
6|Scalability|Farmacy Foods had ambitious growth plans and the architecture should scale with growing business and community.


<h2>Architecture Styles</h2>

Considering above -ilities, we narrowed down architecture style to following:-
  * Microkernel
  * Service-based

<h3>Microkernal</h3>
  A style consisting of two types of components <strong>core</strong> , <strong>plugin</strong>
  In future if we were to add more third parties such as Gym, Therapist etc. They could potentially be added as plugin to existing system. <br/> However, one could argue they could be managed as separate identity in identity management system.<br/> This style may be more suitable for insurance, claims system.

<h3>Service-based</h3>

<h3>Hybrid</h3>
 We propose an style that is a mix of monolith, service-based, event driven.

<h2>References</h2>
https://aws.amazon.com/blogs/architecture/store-protect-optimize-your-healthcare-data-with-aws/ <br/> https://aws.amazon.com/compliance/hipaa-eligible-services-reference/ <br/>
https://learning.oreilly.com/videos/software-architecture-fundamentals/9781491998991/9781491998991-video317000/
