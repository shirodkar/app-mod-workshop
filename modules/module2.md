# Module 2: Upgrading to EAP 8

Because the application relies on an unsupported, outdated technology stack and has security vulnerabilities that require attention, your organization has chosen to initially upgrade the stack without making significant structural changes to the application.

Consequently, your initial objective is upgrading the system to **Jakarta EE 10** and deploying the application on a **JBoss EAP 8** server.

## Why Jakarta EE 10?

Jakarta EE 10 introduced a lot of changes when compared to Java EE 8. Luckily, the **Migration Toolkit for Applications (MTA)** tool from Red Hat has built-in rules that help you identify areas in the code that need modification in order to comply with the Jakarta EE 10 specification. Not only that, the latest version of MTA, called **Developer Lightspeed for MTA**, provides AI capabilities to help you implement these code changes.

MTA provides a Visual Studio Code Extension that has already been installed in your Dev Spaces instance and has also been configured to connect to an LLM.

## MTA Analysis

Follow these instructions to analyze the code:

> **TASK:** Click on the MTA Extension icon in the left menu.

> **TASK:** Click on the **Open Analysis Panel** button on the left.

> **TASK:** Make sure that the **'EAP7 to EAP8'** profile is selected in the dropdown.

> **TASK:** Make sure that **'Agent Mode'** is selected.

> **TASK:** Click on the **'Start'** button.

> **TASK:** Click on the **'Run Analysis'** button.

After a few seconds, under the Analysis Results panel, you should see a few issues listed.

Review the analysis results to understand what changes are to be made.

## AI Solutions

MTA has the capability to implement solutions using AI. Against every issue there is an **"AI"** button which triggers a call to an LLM. The LLM helps implement all the code changes that are needed to address that issue.

For a complete EAP7 to EAP8 upgrade activity, all of the issues need to be addressed, but due to time constraints, we will address only issues associated with one file, in this lab.

Here are the steps to do that:

> **TASK:** In the Analysis Results section, change the **"Group by"** dropdown from Issues to Files.

> **TASK:** Look for the file **MammothResource.java** and click the AI button against it. This will launch the Resolution Panel. MTA will send the issue description along with the code to the LLM, and the LLM will respond with the required code changes.

> **TASK:** Read through the recommended code changes and then click on the blue **Accept** button for each recommendation. (You may even click on **'Review in Editor'** and Accept changes within the file before clicking on the blue Accept button). You will see that the changes have been applied and are ready to be committed.

Typically you would go over each issue and apply the resolutions in a similar fashion.

We have done that for you already and the changes are available in the branch named **'eap8'**.

> **Note:** The devfile was modified manually to provision JBoss EAP 8.

## Viewing the Upgraded Application

You can view the source code for the upgraded application [here](https://github.com/shirodkar/mammoth-ear/tree/eap8).

To view the code in an IDE, click on the contributor badge, or [this link](https://devspaces.apps.${OCP_BASE_URL}/#https://github.com/shirodkar/mammoth-ear/tree/eap8).

You can follow the same steps as in [Module 1](module1.md) to test and run the application, only that now it will run on **JBoss EAP 8**.
