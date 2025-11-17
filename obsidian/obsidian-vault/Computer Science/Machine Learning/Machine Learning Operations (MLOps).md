
Machine learning operations (MLOps) are a set of practices that automate and simplify machine learning (ML) workflows and deployments. Is an **ML culture** and practice that unifies ML application development (Dev) with ML system deployment and operations (Ops).

MLOps is a paradigm that aims to **deploy and maintain** machine learning models in production reliably and efficiently. It bridges the gap between machine learning **development and production operations**, ensuring that models are **robust, scalable, and aligned with business goals**. 

Machine learning models are tested and developed in isolated experimental systems. When an algorithm is **ready to be launched**, MLOps is practiced between Data Scientists, DevOps, and Machine Learning engineers to transition the algorithm to production systems.

![[Pasted image 20250523105456.png]]

### MLOps Principles

#### Version control
This process involves **tracking changes** in the machine learning assets so you can **reproduce results and roll back to previous versions if necessary**. Every ML training code or model specification goes through a **code review phase**. Each is versioned to make the training of ML models reproducible and auditable.

*Reproducibility* in an ML workflow is important at every phase, from data processing to ML model deployment. It means that each phase should produce identical results given the same input.

#### Automation
Automate various stages in the machine learning pipeline to ensure **repeatability, consistency, and scalability**. This includes stages from *data ingestion*, *preprocessing*, *model training*, and *validation* to deployment.

These are some factors that can trigger automated model training and deployment:

* **Messaging**
* **Monitoring or calendar events**
* **Data changes**
* **Model training code changes**
* **Application code changes.**

Automated testing **helps to discover problems early for fast error fixes and learnings**. Automation is more efficient with **infrastructure as code (IaC)**. You can use tools to define and manage infrastructure. This helps ensure it's *reproducible* and can be consistently deployed across **various environments**.

#### Continuous X
Through automation, you can continuously run tests and deploy code across your ML pipeline.

In MLOps, continuous refers to **four activities that happen continuously if any change is made anywhere in the system**:

* **Continuous integration extends the validation and testing of code to data and models in the pipeline**
* **Continuous delivery automatically deploys the newly trained model or model prediction service**
* **Continuous training automatically retrains ML models for redeployment**
* **Continuous monitoring concerns data monitoring and model monitoring using metrics related to business**

#### Model governance
**Governance involves managing all aspects of ML systems for efficiency.**

* **Foster close collaboration between data scientists, engineers, and business stakeholders**
* **Use clear documentation and effective communication channels to ensure everyone is aligned**
* **Establish mechanisms to collect feedback about model predictions and retrain models further**
* **Ensure that sensitive data is protected, access to models and infrastructure is secure, and compliance requirements are met**

It’s also essential to have a **structured process to review, validate, and approve models before they go live**. This can involve checking for *fairness, bias, and ethical considerations*.

## **Further Reading**

* [MLOps (Wiki)](https://en.wikipedia.org/wiki/MLOps)
* [What is MLOps?](https://aws.amazon.com/what-is/mlops/#:~:text=Machine%20learning%20operations%20(MLOps)%20are,deliver%20value%20to%20your%20customers.)