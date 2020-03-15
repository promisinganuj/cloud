### What is AWS Well-Architected Framework?
* It is a framework helps you understand the pros and cons of decisions you make while building systems on AWS.
* It's a set of best practices and core strategies for architecting systems in the cloud.
* It documents a set of foundational questions that allow you to understand if a specific architecture aligns well with cloud best
practices.

### What are the five pillars of Well Architected Framework?
1. Operational Excellence - The ability to run and monitor systems to deliver business value and to continually improve supporting
processes and procedures.
2. Security - The ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies.
3. Reliability - The ability of a system to recover from infrastructure or service disruptions, dynamically acquire computing resources to meet demand, and mitigate disruptions
such as misconfigurations or transient network issues.
4. Performance Efficiency - The ability to use computing resources efficiently to meet system requirements, and to maintain that
efficiency as demand changes and technologies evolve.
5. Cost Optimization - The ability to run systems to deliver business value at the lowest price point.

### Different terms used in AWS Well-Architected Framework
* Component - Code, configuration and AWS Resources that together deliver against a requirement.
* Workload - Set of components that together deliver business value. 
* Milestones - Changes in your architecture as it evolves throughout the product lifecycle (design, testing, go live, and in production).
* Architecture - How components work together in a workload.
* Technology Portfolio - Collection of workloads that are required for the business to operate.

### How does these pillars help in designing a Well-Architected Framework?
* It's all about making trade-off between those pillars based on business priorities and requirements. For Ex:
  * Development Environment - We might optimize to reduce cost at the expense of reliability.
  * Mission-critical solutions - We might optimize reliability with increased costs
  * E-commerce solutions - Peformance is the priority
* Security and operational excellence are generally not traded-off against the other pillars.
