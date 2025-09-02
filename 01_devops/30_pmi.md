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
  
This helped make the build process more stable and predictable, improving traceability and maintainability. The ability to use this tool as a standalone tool in a local environment allowed developers to detect errors early in development, which resulted in a reduction in the load on the SI server.  
  
This experience taught me the importance of proactive problem-solving, data-driven decision-making, and perseverance.  

## 4. Tell me about a successful project and your role in it <a name="question4"></a>

Hiring managers ask this behavioural question to evaluate your interpersonal skills, leadership skills and how you work with a team. Showcase your role with your previous employer, the project, and how you assisted your co-workers. Provide examples of communication, collaboration, teamwork and problem-solving.  
  
**Answer:**  
On my previous project we worked together with team A most of the time. Due to my proactive position and direct involvement in improving the build processes affecting Team C, I was able to establish good communication with the members of this team.  
  
This has led to a gradual expansion of the scope of our tasks and, consequently, an increase in the qualifications and , later, a size our team. This also led to improved interaction with Team A and the customer in general, as well as increased customer trust in our team.  
  
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

## 8. Share an example of a time when you demonstrated leadership skills <a name="question8"></a>

Answering the behavioural job interview question about demonstrating leadership skills and driving positive change within a team or organisation is crucial. It showcases your ability to lead, collaborate, and make a meaningful impact – a key aspect employers look for.  
  
**Answer:**  

## 9. How did you motivate your team, set goals, and achieve success <a name="question9"></a>

Answering the job interview question about taking the lead on a project or initiative is important for showcasing your leadership abilities. It demonstrates your capacity to inspire a team, establish objectives, and attain success – qualities highly sought after by employers.  
  
**Answer:**  

## 10.  <a name="question10"></a>


  
**Answer:**  