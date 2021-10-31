<h2>Top Architecture Characteristics</h2>

S.No.|Characteristic|Why
-----|--------------|---
1|Cost| - Farmacy Foods is a startup firm with limited resources. We propose to reduce cost by using open source libraries and reusing services provided by AWS. 
2|Agility| - Solution should be delivered quickly. Time to market could a constraint here. Suggest to have less in-house build components 
3|Security| - Farmacy Family plan to store customer's PII (Personal Identifiable Information), EMR (Electronic Medical Record). <br/> - Data compliance, governce should be taken into consideration. <br/>- Data will be stored in Amazon S3 layer, and accessed via AWS HIPPA eligible services. 
4|Feasibility & Simplicity| - Prefer pay-as-you-go instead of owning infrastructure and licenses.
5|Extensibility|Farmacy Foods is in the growth phase and is likely to constantly add products and features.
6|Scalability|Farmacy Foods had ambitious growth plans and the architecture should scale with growing business and community.


<h2>Architecture Styles</h2>

Considering above -ilities, we narrowed down architecture style to following:-
  * Microkernel
  * Service-based

<h3>Microkernal</h3>
