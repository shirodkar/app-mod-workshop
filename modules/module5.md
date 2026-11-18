# Module 5: Refactoring to Microservices

In this module, we will refactor each component of the application using the **Strangler Fig** approach.

We will start with the **backend-api** module and convert it to a **Quarkus** microservice.

The frontend module can still continue to run inside of EAP 8 as a Jakarta EE application, but instead of calling APIs locally, it will invoke APIs provided by the backend-api Quarkus microservice.

## Mammoth Backend

To use the Strangler Fig approach, the backend component has already been pulled out into a separate project called **mammoth-backend**.

> **TASK:** Access the source code for this application [here](https://github.com/shirodkar/mammoth-backend).

### Exploring the Application in Dev Spaces

> **TASK:** Click on the contributor badge in the README section, or click on [this link](https://devspaces.apps.${OCP_BASE_URL}/#https://github.com/shirodkar/mammoth-backend).

> **TASK:** If prompted, click on the **"Login with OpenShift"** button.

> **TASK:** Provide your OpenShift credentials:
> - **Username:** `${USERNAME}`
> - **Password:** `${PASSWORD}`

> **Note:** It may take a few seconds for the workspace to be set up.

## MTA Analysis

Follow these instructions to analyze the code:

> **TASK:** Click on the MTA Extension icon in the left menu.

> **TASK:** Click on the **Open Analysis Panel** button on the left.

> **TASK:** Make sure that the **'Quarkus'** profile is selected in the dropdown.

> **TASK:** Make sure that **'Agent Mode'** is selected.

> **TASK:** Click on the **'Start'** button.

> **TASK:** Click on the **'Run Analysis'** button.

After a few seconds, under the Analysis Results panel, you should see a few issues listed.

Review the analysis results to understand what changes are to be made.

## AI Solutions

MTA has the capability to implement solutions using AI. Against every issue there is an **"AI"** button which triggers a call to an LLM. The LLM helps implement all the code changes that are needed to address that issue.

For a complete Refactoring activity, all of the issues need to be addressed, but due to time constraints, we will address only issues associated with one file, in this lab.

Here are the steps to do that:

> **TASK:** In the Analysis Results section, change the **"Group by"** dropdown from Issues to Files.

> **TASK:** Look for the file **pom.xml** and click the AI button against it. This will launch the Resolution Panel. MTA will send the issue description along with the code to the LLM, and the LLM will respond with the required code changes.

> **TASK:** Go through the recommended code changes and then click on the blue **Accept** button for each recommendation. (You may even click on **'Review in Editor'** and Accept changes within the file before clicking on the blue Accept button). You will see that the changes have been applied and are ready to be committed.

Typically you would go over each issue and apply the resolutions in a similar fashion.

We have done that for you already and the changes are available in the branch named **'refactor'**.

> **Note:** The devfile was modified manually to run Quarkus. Also, the database script was modified to add additional information.

## Viewing the Refactored Application

You can view the source code for the refactored application [here](https://github.com/shirodkar/mammoth-backend/tree/refactor).

To view the code in Dev Spaces, click on the contributor badge, or [this link](https://devspaces.apps.${OCP_BASE_URL}/#https://github.com/shirodkar/mammoth-backend/tree/refactor).

### Testing the Application

> **TASK:** In Dev Spaces, click on the search bar on top → **Run task** → **devfile**.

> **TASK:** Execute the **"Start Quarkus dev mode"** task. You should see the following output:

```
Listening for transport dt_socket at address: 5005
__  ____  __  _____   ___  __ ____  ______
 --/ __ \/ / / / _ | / _ \/ //_/ / / / __/
 -/ /_/ / /_/ / __ |/ , _/ ,< / /_/ /\ \
--\___\_\____/_/ |_/_/|_/_/|_|\____/___/
INFO  [io.quarkus] (Quarkus Main Thread) mammoth-backend 1.0.0-SNAPSHOT on JVM
INFO  [io.quarkus] (Quarkus Main Thread) Installed features: [...]
```

## Build

> **TASK:** In the OpenShift console, select **Build → BuildConfigs**.

> **TASK:** Select the **'cicd'** project.

> **TASK:** Start the **'refactor-mammoth-backend'** build. Once the build is complete a new image for the backend microservice will be created.

### Connecting the Frontend to the Backend Microservice

To point the Replatformed Mammoth EAR application (from the previous module) to the Quarkus backend, edit the **WildFlyServer** instance and add the following under `spec`:

```yaml
env:
  - name: MAMMOTH_API_URL
    value: 'http://mammoth-backend.refactor.svc.cluster.local:8080/mammoths'
```

This will instruct the Mammoth EAR application running under the **'replatform'** namespace to point to the Mammoth Backend Microservice running under the **'refactor'** namespace.

## Deploy

The code from this branch has already been deployed to OpenShift under the **'refactor'** project. To roll out the new image:

> **TASK:** In the OpenShift console, select **Workloads → Deployments**.

> **TASK:** Select the **'refactor'** project.

> **TASK:** Roll out the **'mammoth-backend'** deployment, by clicking the 3 dots on the right and select **'Restart rollout'**.

## Testing the Deployed Application

To test, just like we did earlier, access the application using the URL provided by the `mammoth-route` OpenShift Route under the **replatform** project.

Instead of accessing the local backend component, it is now using the Quarkus backend microservice.

You should be able to see a new category called **'Elephants'** now.
