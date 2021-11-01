<h1>Community Event Scheduling Subsystem</h1>

<h2>Current Goal</h2>
Provide <strong>Farmacy Family</strong> user's ability to list join virtual in-person classes.

Assumptions
None

<h2>Requirement</h2>

* User should be able to :-
	* List currently registered, upcoming classes based on geographic location
	* Register/unregister/attend classes

<h2>Solution</h2>
We propose using third party open-source library, rather than building in-house system. Thus reducing cost.

Extend following open-source for scheduling:-
  * Optaplanner (https://www.optaplanner.org/?r=pmp-osess&dpm=8933)
    <p>It's an AI scheduling platform, written in Java, Springboot, Drools. Scheduler can be invoked using AWS Lambda.</p>
  
