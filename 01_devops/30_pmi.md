# PMI

## Table of contents
1. [Describe a time when you had to overcome a difficult situation at work and how you managed it](#question1)
2. [How do you respond to high-pressure situations?](#question2)
3. [What has been your greatest achievement to date](#question3)
4. [Tell me about a successful project and your role in it](#question4)
5. [How do you handle disagreements with your colleagues or your manager](#question5)
6. [Tell me about a situation where you had to handle a dissatisfied customer or client.](#question6)
7. [Describe a time when you had to multitask and manage multiple projects or tasks simultaneously](#question7)
8. [Share an example of a time when you demonstrated leadership skills](#question8)
9. [How did you motivate your team, set goals, and achieve success](#question9)
10. [Some](#question10)

## 1. Describe a time when you had to overcome a difficult situation at work and how you managed it <a name="question1"></a>

This interview question gauges your definition of a challenging situation and your problem-solving skills. Choose an instance not caused by you, detailing your actions to resolve it. Emphasise the positive outcome, lessons learned, and how your solutions improved overall performance.  
  
**Answer:**  
In my previous project I was involved in implementation of some services specific for 2 ECU types. Let's say I've been working together with team A on ECU A implementation and there was a team B which was working on ECU B. Both ECUs use service S. For ECU B it has been already deployed, and the goal was to deploy similar service S2 with a bit extended functionality.  
  
Service S1 was deployed in k8s cluster, and we decided to deploy our service S2 next to S1, but in a different k8s namespace to provide a resource isolation. Unfortunately, colleagues from team B declined our request without any argumentation or explanation. So I had to come up with another solution in a quite short time.  
  
The customer already had an extensive infrastructure, but there was no documentation that would list all the available platforms and solutions. So, I splitted task to 3 subtasks: platform research (to find all available platforms),  platform overview (to summarize the platform's capabilities and costs), service requirements (to identify critical service parameters and their compliance with the capabilities of available platforms). As a team lead, I distributed these tasks among the team, and as a result of our joint efforts, we provided a comparative table of available solutions within the specified deadline.  
  
Having discussed all the pros and cons together with the customer, we chose the optimal solution and I proceeded to the next stage. This situation taught me the importance of identifying problems early in the design process, adaptability, and clear communication during unexpected challenges.  

## 2. How do you respond to high-pressure situations? <a name="question2"></a>

This behavioural question is designed to understand how you stay focused in different, difficult and stressful situations. It is a chance to highlight how you solve problems and your ability to work well under pressure.  
  
**Answer:**  
In high-pressure situations, I prioritise and break down tasks into manageable steps. For example, in my previous role, we faced an unexpected logistics issue right before a release.  
  
I provided a short analysis (define a build step which is broken), implemented a quick fix (use a default logistics), which unblocked upcoming release. After that i made a detailed analysis and provide a long-term fix in collaboration with other colleagues to prevent such issues in future.  
  
By focusing on the solution, maintaining a calm demeanour, and fostering team collaboration, we resolved the issue in time for the release. These experiences have reinforced that staying organised and maintaining a positive attitude are essential in managing pressure effectively.  

## 3. What has been your greatest achievement to date <a name="question3"></a>

Here, the interviewer is looking to see if you are a high performer and where you have excelled in your previous roles.  
  
In this case, select a few recent accomplishments that are directly related to the job position, role and responsibilities wherever possible. Be precise, and quantify the action, the steps taken and the benefits you provided.  
  
**Answer:**  
On my previous project, I was involved to maintenance of the one of critical periodic job. I noticed that one of the build stages is unstable (there is a sporadic bug, and build time varies from a few minutes to half an hour).  
  
I insisted on the need for improvements and initiated a refactoring process that involved replacing a third party build tool based on bad written bash scripts and critically dependent on the naming and location of some configs with a highly configurable python-based tool written by myself with detailed logging, config templating and user-defined paths.  
  
This helped to make the build process more stable and predictable, improving traceability and maintainability. The ability to use this tool as a standalone tool in a local environment allowed developers to detect errors earlier during the development, that resulted in a reduction of the load on the CI server.  
  
This experience taught me the importance of proactive problem-solving, data-driven decision-making, and perseverance.  

## 4. Tell me about a successful project and your role in it <a name="question4"></a>

Hiring managers ask this behavioural question to evaluate your interpersonal skills, leadership skills and how you work with a team. Showcase your role with your previous employer, the project, and how you assisted your co-workers. Provide examples of communication, collaboration, teamwork and problem-solving.  
  
**Answer:**  
On my previous project we worked together with team A most of the time. Due to my proactive position and direct involvement in improving the build processes affecting Team C, I was able to establish good communication with the members of this team.  
  
This led to a gradual growth of the scope of our tasks and, consequently, extended our expertise and, as follows, a size of our team. This improved our reputation as a problem solver within internal customer's teams.  
  
This project taught me the importance of proactive planning, flexibility in the face of unforeseen challenges, and the value of maintaining strong professional relationships.  

## 5. How do you handle disagreements with your colleagues or your manager <a name="question5"></a>

This interview question probes your conflict resolution and communication skills at work. It’s essential to demonstrate diplomacy and tact, as teams thrive when members can address disagreements and reach a consensus.  
  
Reflect on a situation where you and a colleague or manager resolved differing views through effective communication, leading to a collaborative solution.  
  
**Answer:**  
When I encounter disagreements with colleagues or managers, I prioritise open communication. First, I actively listen to their viewpoint to understand their concerns fully.  
  
By doing so, I often find areas of common ground. I then share my perspective, ensuring I present it as an alternative viewpoint rather than a contradiction. If needed, I seek feedback from other team members or suggest collaborative problem-solving sessions.  
  
This approach ensures that the final decision is well-informed and beneficial for the project or organisation. Importantly, I always maintain respect for everyone involved, understanding that diverse opinions often lead to the best solutions.  

## 6. Tell me about a situation where you had to handle a dissatisfied customer or client. How did you address their concerns and ensure their satisfaction? <a name="question6"></a>

When responding to this behavioural question, focus on demonstrating your ability to empathise, communicate effectively, and find constructive solutions to resolve customer issues. Your response should highlight your commitment to delivering excellent customer service and problem-solving skills.  
  
**Answer:**  
On my previous project, I encountered a dissatisfied customer who was frustrated by the need for extensive knowledge sharing sessions. The reason was not related to our team, but to a general lack of documentation of key aspects of the development process on the client's side. To address their concerns and ensure their satisfaction, I initiated a proactive approach.  
  
It involved documentation research or contacting responsible persons on the Client's side, issue investigation, providing a table of possible approaches and, finally, providing detailed breakdown for each Story. With this approach we were able to reduce and gradually eliminate the need for knowledge-sharing sessions from customer's side and were able to establish contact with key developers.  
  
Throughout the process, I maintained open communication with the customer, providing regular updates on the progress for each ongoing issue. This transparency helped rebuild trust.  
  
This experience taught me the importance of empathy, swift problem-solving, and effective communication in handling dissatisfied customers.  

## 7. Describe a time when you had to multitask and manage multiple projects or tasks simultaneously. How did you stay organised and meet all your deadlines? <a name="question7"></a>

For this question, you should emphasise your time management, organisational skills, and ability to prioritise effectively. Hiring managers want to assess your capability to handle a demanding workload efficiently.  
  
**Answer:**  
  
On my previous project I often had to work on different topics at the same time. To stay organised and meet all deadlines, I implemented a systematic approach. I started from creating a detailed task list, prioritising tasks by deadlines dates and importance.  
  
Then I allocated specific time blocks for each task, ensuring I had uninterrupted periods for focused work. That means I allocated 1-2h timeslot at midday for sync-ups, morning hours were used for highly important topics and tasks with long-running tests, and hours after lunch were used for getting approvals and merging PRs (due to specific Zuul reconfiguration hours).  
  
Regular sync-ups helped maintain alignment and address any blockers. By maintaining a disciplined schedule, staying adaptable, and leveraging technology, I successfully managed multiple topics, meeting all deadlines effectively.  

## 8. Share an example of a time when you demonstrated leadership skills <a name="question8"></a>

Answering the behavioural job interview question about demonstrating leadership skills and driving positive change within a team or organisation is crucial. It showcases your ability to lead, collaborate, and make a meaningful impact – a key aspect employers look for.  
  
**Answer:**  
  
I was consistently taking an active role in refinement sessions, not only by refining items by myself but also by supporting other developers in the process. I have essentially acted as the Tech Lead for Landau team, ensuring that refinement sessions are productive and well-structured.  
  
Also, I provided valuable guidance and support to my colleagues, enabling them to gain a deeper technical understanding and work independently on these areas. These structured mentoring and knowledge-sharing efforts significantly strengthened the team's technical capabilities.  
  
By taking ownership of technical discussions and supporting the team’s development, I demonstrated leadership and technical expertise, making a lasting impact on the team’s growth.  
  
This experience highlighted my ability to lead, inspire change, and foster teamwork, ultimately contributing to positive outcomes.  

## 9. How did you motivate your team, set goals, and achieve success <a name="question9"></a>

Answering the job interview question about taking the lead on a project or initiative is important for showcasing your leadership abilities. It demonstrates your capacity to inspire a team, establish objectives, and attain success – qualities highly sought after by employers.  
  
**Answer:**  
  
On my last project one of my colleagues didn't have a lot of experience with tolls and technologies used on Client's side. So he was struggling with focus and communication, which made it challenging to track progress effectively.  
  
So, I stepped in to provide guidance, structure, and hands-on support. I leveraged in-person collaboration to align on tasks, address blockers, and ensure progress was made. It definetly helped to improve my colleague's engagement and communication while fostering a more structured way of working.  
  
This experience further strengthened my mentoring and leadership skills, making a positive impact on both the individual and the team. It demonstrats my ability to support colleagues while maintaining a productive and collaborative team environment.  

## 10.  <a name="question10"></a>


  
**Answer:**  
