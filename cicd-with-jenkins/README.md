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
  * Helps to main a stable and functional software build 

# What is CD? Benefits?
**CD Stands for either Continuous Delivery or Deployment** 

* about:
  * ==continuous delivery== (manual sign off/approval )
  * Or ==Continuous Deployment== ( automatically deploys code to production)

### **continuous delivery:**
* ensures software is always in a deployable state, read/can be push production line any time. 
  * often involves producing a artifact
  * requires a manual decision 👨‍💼👨
* Benefits:
* always have a deployable artifact ready to deploy to end users
  
### **continuous deployment**
* extends continuous delivery by automating the final step of automating to production
  * no manual intervention required 🤖
  * benefit which is also a disadvantage: 
    * removes all human approval, relies entirely on automated processes.

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

* Cost Effective - automating repetitive processes.
* Faster time to market
* reduced risk -  
* 