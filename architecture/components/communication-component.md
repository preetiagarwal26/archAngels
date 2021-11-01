<h1>Communication Subsystem</h1>

<h2>Current Goal</h2>
Provide <strong>Farmacy Family</strong> user's ability to interact with other users and providers such as dietitian, gym etc. via chat, forums.

Assumptions
Both chat, forum components will be deployed on AWS.

<h2>Requirement</h2>
* Provision a chat system
* Build community forum

<h2>Solution</h2>
We propose using third party open-source library, rather than building in-house system. Thus reducing cost.

<h3>Chat System</h3>
 
 Use following open-source Chat and Messaging development SDK:-
  * Rocket.chat (https://rocket.chat/)
    <p>It's an open-source self-hosted messaging platform, which can be installed anywhere. <br/> Additionally it can be deployed on AWS (https://docs.rocket.chat/quick-start/installing-and-updating/paas-deployments/aws) </p>
  
<h3>Forum</h3>

 Following open-source forum system can be plugged in to existing system:-
 * MyBB (https://mybb.com/)
   <p>Free and open-source forum software. It can be easily integerated with AWS (https://aws.amazon.com/marketplace/pp/prodview-khsff4s7snq32)</p>
 * phpBB (https://www.phpbb.com/
   <p>Free open-source bulletin board software. Here is a link to integerate with AWS (https://aws.amazon.com/marketplace/pp/prodview-we55cxypcapls)</p>