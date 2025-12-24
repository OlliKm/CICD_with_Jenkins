#### Advise to start here

# Intro To CICD & Jenkins 


**Table of content**
- [Intro To CICD \& Jenkins](#intro-to-cicd--jenkins)
- [What is CI? Benefits?](#what-is-ci-benefits)
- [What is CD? Benefits?](#what-is-cd-benefits)
    - [**continuous delivery:**](#continuous-delivery)
    - [**continuous deployment**](#continuous-deployment)
- [What is Jenkins?](#what-is-jenkins)
- [Why use Jenkins? Benefits of using Jenkins? Disadvantages?](#why-use-jenkins-benefits-of-using-jenkins-disadvantages)
- [Stages of Jenkins](#stages-of-jenkins)
- [What alternatives are there for Jenkins](#what-alternatives-are-there-for-jenkins)
- [Why build a pipeline? Business value?](#why-build-a-pipeline-business-value)
- [CICD Diagrams](#cicd-diagrams)
    - [Pipelines](#pipelines)
  - [CICD Jobs and how they work with Jenkins and GitHub](#cicd-jobs-and-how-they-work-with-jenkins-and-github)
      - [Now you have learned the basics its best to learn how to impliment it](#now-you-have-learned-the-basics-its-best-to-learn-how-to-impliment-it)

# What is CI? Benefits?
**CI Stands for Continuous Integration**

* About
  * ==continuous integration==.
  * merging code
  * Triggered by: Developers frequently pushing the code changes to shared repo
  * tests are run **automatically** on the code before its integrated into the main code.
  
  **Benefits:**
  * Helps you identify and resolve bugs.
    * Reduces Cost 💰
  * Helps to main a stable and functional software build 🏗️

# What is CD? Benefits?
**CD Stands for either Continuous Delivery or Deployment** 

* about:
  * ==continuous delivery== (manual sign off/approval )
  * Or ==Continuous Deployment== ( automatically deploys code to production)

### **continuous delivery:**
* ensures software is always in a deployable state, read/can be push production line any time. 
  * often involves producing a artifact
  * **requires a manual decision** 👨‍💼
* Benefits:
* always have a deployable artifact ready to deploy to end users 🟢
  
### **continuous deployment**
* extends continuous delivery by automating the final step of automating to production
  * no manual intervention required 🤖
  * benefit which is also a disadvantage: 
    * **removes all human approval**, relies entirely on automated processes.

# What is Jenkins?
* **==automation Server==** 
* open source
* Primary Used for CICD, but can automate much more

# Why use Jenkins? Benefits of using Jenkins? Disadvantages?
* Benefits: ✅
  * Automation
  * Extensibility: Jenkins has over 1800 Plugins
  * Scalability: Jenkins server can scale easily by adding/using worker nodes/agents to run jobs
  * Community Support
  * Cross-platform: works across Windows, Linux, MacOs
<br> 
* Disadvantages: ❌
  * can be complex for beginners
  * Maintenance overhead:
  * Resource Intensive when running multiple jobs
  * User Interface: outdated 

# Stages of Jenkins
A typical Jenkins CICD pipeline involves the following stages:

1. ==Stage== Code Management(SCM)
2. ==Build==: Compile the code, Build into executable artifact. 
3. ==Test==: Automated Tests ( Unit, integration, etc)
4. ==Package==: package into deployable artifact
5. ==release==: If using **Cont Deploy**, the package is deployed into the target environment e.g. test, production
6. ==Monitor==: Monitoring tools may be deployed/configured to observe performance log issues etc after deployment 

# What alternatives are there for Jenkins
```
* GitLab CI
* GitHub Actions
* Travis CI
* Bamboo
* Team City
* GOCD
* Azure Pipelines
```

# Why build a pipeline? Business value?

* Cost Effective - due to it automating repetitive processes. 
* Faster time to market 
* reduces risk 
  
# CICD Diagrams 
### Pipelines
> CICD Pipelines progress
* ![alt text](/images/cicdPipelin.png)
> CICD Pipelines progress
1. Once a git push has been processed the code then gets **tested** to check if theres anything wrong with it.
--
1.  Once it passes testing it will then be **merged** from dev branch to main branch
--
1. When the merge is completed be sure to use the **Code that was tested and merged** when **deploying** rather that the lastest version to avoid any conflicts of others pushing code that doesn't work with yours

  ## CICD Jobs and how they work with Jenkins and GitHub

  > CICD Jobs and how they work
    * ![alt text](</images/cicd jobs.png>)
  > CICD Jobs and how they work
   * typically when working with CICD, Jenkins automated servers are typically used to help push code.
   1. when the git push is initialised from the dev branch to the GitHub Repo 
2. we then assign webhooks [Automated messages that get sent when specific events occur]()
3. We then use Jenkins which is made up of the Master node(built in node) which uses Agent Nodes to run jobs
4. in order to do so ==Jenkins needs the private Github key== so it can merge and update repo.  as well as ==Jenkins needing the EC2 private key== to SSH into the EC2 
<br>

**How Jobs work:**
  * Job 1. is the test code (Dev Branch)
   **If Successful**
  * Job 2. Merges code from dev branch to main branch
   **If Successful**
  * The Code gets Deployed to the EC2

#### Now you have learned the basics its best to learn how to impliment it
[Link to Jenkins setup guide](/cicd-with-jenkins/Jenkins-setup.md)