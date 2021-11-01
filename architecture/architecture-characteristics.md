<h2>Top Architecture Characteristics</h2>

S.No.|Characteristic|Why
-----|--------------|---
1|Cost| - Farmacy Foods is a startup firm with limited resources. We propose to reduce cost by using open source libraries and reusing services provided by AWS. 
2|Agility| - Solution should be delivered quickly. Time to market could a constraint here. Suggest to have less in-house build components 
3|Security| - Farmacy Family plan to store customer's PII (Personal Identifiable Information), EMR (Electronic Medical Record). Data compliance, governance should be taken into consideration. <br/>- We offer storing data in <strong>Amazon S3 layer</strong>, and accessed via <strong>AWS HIPPA eligible services</strong>. 
4|Feasibility & Simplicity| - Prefer pay-as-you-go instead of owning infrastructure and licenses.
5|Extensibility|Farmacy Foods is in the growth phase and is likely to constantly add products and features.
6|Scalability|Farmacy Foods had ambitious growth plans and the architecture should scale with growing business and community.


<h2>Architecture Styles</h2>

Considering above -ilities, we narrowed down architecture style to following:-
  * Microkernel
  * Service-based

<h3>Microkernal</h3>
  A style consisting of two types of components <strong>core</strong> , <strong>plugin</strong>. <br/> In future if we were to add more third parties such as Gym, Therapist etc. They could potentially be added as plugin to existing system. <br/> However, one could argue they could be managed as separate identity in identity management system.<br/> This style may be more suitable for insurance, claims system.

<h3>Service-based</h3>

<h3>Hybrid</h3>
 We propose an style that is a mix of monolith, service-based, event driven.
 
 <h2>Third party/Open-source libraries</h2>
 
 <h3>Chat System</h3>
 
 We evaluated following open-source Chat and Messaging development SDK:-
  * Rocket.chat (https://rocket.chat/)
    <p>It's an open-source self-hosted messaging platform, which can be installed anywhere. <br/> Additionally it can be deployed on AWS (https://docs.rocket.chat/quick-start/installing-and-updating/paas-deployments/aws) </p>
  * Amazon Connect
    <p> An easy-to-use omnichannel cloud contact center with chat capabilities.<br/> Available for free, for 12 months, as part of the AWS Free Tier program. Provides pay-as-you-go pricing model.</p>

<h3>Forum</h3>

Following open-source forum system can be plugged in to existing system:-
 * MyBB (https://mybb.com/)
   <p>Free and open-source forum software. It can be easily integerated with AWS (https://aws.amazon.com/marketplace/pp/prodview-khsff4s7snq32)</p>
 * phpBB (https://www.phpbb.com/
   <p>Free open-source bulletin board software. Here is a link to integerate with AWS (https://aws.amazon.com/marketplace/pp/prodview-we55cxypcapls)</p>
   
<h2>References</h2>
https://aws.amazon.com/blogs/architecture/store-protect-optimize-your-healthcare-data-with-aws/ <br/> https://aws.amazon.com/compliance/hipaa-eligible-services-reference/ <br/>
https://learning.oreilly.com/videos/software-architecture-fundamentals/9781491998991/9781491998991-video317000/
