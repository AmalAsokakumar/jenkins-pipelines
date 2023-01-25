Configuring SonarQube to Perform Quality Gate Analysis with Webhooks

Prerequisites

SonarQube installed and running
A project that has been analyzed with SonarQube
An external service that can receive webhooks (e.g. Jenkins, GitHub)
Step 1: Enable webhooks in SonarQube

Log in to the SonarQube web interface as an administrator.
Go to the Administration > Configuration > General Settings page.
Scroll down to the Webhooks section.
Check the Enable Webhooks box.
Click the Save button.
Step 2: Create a webhook in SonarQube

Go to the Administration > Configuration > Webhooks page.
Click the Generate button to generate a secret token.
Enter the URL of the external service that will receive the webhook in the URL field.
Select the Project Analysis event in the Events field.
Enter a name for the webhook in the Name field.
Click the Save button.
Step 3: Configure the external service to receive the webhook

Consult the documentation for the external service that you are using to learn how to configure it to receive webhooks. You will need to provide the URL of the SonarQube webhook and the secret token that you generated in Step 2.

Step 4: Run a SonarQube analysis and trigger the webhook

Run a SonarQube analysis for the project that you want to trigger the webhook for.
If the analysis passes the quality gate, the webhook will be triggered and the external service will receive it.
Step 5: Configure the external service to perform an action based on the webhook

Consult the documentation for the external service that you are using to learn how to configure it to perform an action based on the webhook. You may want to configure it to perform an action (e.g. run a build, deploy code) if the webhook indicates that the quality gate was passed, and perform a different action (e.g. send an alert, roll back code) if the quality gate was not passed.