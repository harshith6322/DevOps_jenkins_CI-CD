---

## 📊 CI/CD Workflow

![CI/CD Pipeline Diagram](https://github.com/user-attachments/assets/1ebd1164-e26e-4f89-9656-e8cea971c736)

---
````markdown
# 🚀 DevOps Jenkins CI/CD Pipeline

This repository demonstrates a **Jenkins CI/CD pipeline** for building, uploading, and deploying a Java/Maven application with multiple environments and a branching strategy.


## 📌 Pipeline Overview

The pipeline is defined in the `Jenkinsfile` and contains the following stages:

1. **Git Checkout**  
   - Pulls code from GitHub (`main`, `dev`, `qa`, or `feature/*` branches).

2. **Maven Build**  
   - Builds the project with `mvn install`.  
   - Generates a `.war` artifact.

3. **Upload Artifacts to Nexus**  
   - Publishes the `.war` file to **Nexus Repository Manager**.  
   - Uses the `nexusArtifactUploader` plugin.  
   - Parameters such as `GroupId`, `ArtifactId`, `Version`, and `Repository` are passed from the Jenkins job.

4. **Deploy to Tomcat**  
   - Deploys the generated `.war` file into **Apache Tomcat 9** server.  
   - Uses Jenkins `Deploy to Container` plugin.

---

## 📂 Branching Strategy

The project follows a **Git branching model**:

- **`main`** → Production-ready branch. Only stable and tested code gets merged here.  
- **`dev`** → Development branch. All new features are integrated and tested here before QA.  
- **`qa`** → QA/testing branch. Code from `dev` is tested here before release.  
- **`feature/*`** → Feature branches for individual tasks/bug fixes. Merged into `dev` after completion.

---

## ⚙️ Tools & Plugins Used

- **Jenkins** – CI/CD automation  
- **Maven** – Build and dependency management  
- **Nexus Repository Manager** – Artifact storage  
- **Apache Tomcat 9** – Deployment target  
- **Plugins**:  
  - `Pipeline`  
  - `Maven Integration`  
  - `Nexus Artifact Uploader`  
  - `Deploy to Container`

---

## 🔑 Jenkins Parameters

The pipeline expects the following **parameters** to be configured in Jenkins:

- `Branch` → Git branch to checkout  
- `GroupId` → Maven group ID  
- `ArtifactId` → Maven artifact ID  
- `Version` → Artifact version  
- `Repository` → Nexus repository name  
- `WarFile` → Path to generated WAR file (e.g., `target/myapp.war`)  
- `Type` → Artifact type (e.g., `war`)  
- `Nexus_URL` → Nexus server URL (e.g., `54.210.178.49:8081`)  
- `Nexus_Version` → Nexus version (`nexus2` or `nexus3`)  
- `Protocol` → `http` or `https`

---

## 🚀 How to Run the Pipeline

1. Clone this repository in Jenkins:
   ```bash
   git clone https://github.com/harshith6322/DevOps_jenkins_CI-CD.git
````

2. Configure Jenkins with:

   * `maven_build` tool
   * `nexus_cred` credentials for Nexus
   * `tomcat_cred` credentials for Tomcat

3. Run the pipeline with required parameters.

4. Verify:

   * WAR file uploaded in Nexus
   * Application deployed on Tomcat at:

     ```
     http://<Tomcat_Server_IP>:8080/ecom
     ```

---

## 📜 Example Nexus Upload Step

```groovy
nexusArtifactUploader artifacts: [[
  artifactId: 'junit',
  classifier: '',
  file: 'target/myweb-8.6.9.war',
  type: 'war'
]], 
credentialsId: 'nexus_cred',
groupId: 'in.javahome',
nexusUrl: '54.210.178.49:8081',
nexusVersion: 'nexus2',
protocol: 'http',
repository: 'maven_artifact',
version: '8.6.9.9'
```

---

## ✅ Expected Outcome

* Every commit to a branch triggers a Jenkins build.
* Artifacts are uploaded to Nexus.
* WAR is deployed to Tomcat automatically.

---

## 🧑‍💻 Author

**Harshith Reddy**
DevOps Engineer & React Developer

---





