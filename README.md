# HarnessU-CI-CD-Workshop

## Lab 1 - Login to app.harness.io and familiarize yourself with the environment


1. Load up your Chrome web browser and login to https://app.harness.io with the username and password from your lab email. 

2. Click around and explore the GUI. You have full administrator rights to our training Harness implementation. In the "real world" you might not have this level of permissions in Harness.

5. We will be visiting the Setup menu most often. Click in there and explore the different connectors and setting options. 

6. Ask your instructor if you don't understand the use of any configuration or dashboard.

## Lab 2 - Setup the CD side of the equation

In this lab we're going to setup the Continuous Delivery infrastructure which will allow us to deploy the output of the Continuous Integration with Drone we will demo or run for ourselves. 

1. Still in the Harness UI, click on the Setup menu on the left-hand side of the UI.

2. Click on the Add Application button and fill out the information for your new application. Be sure to use your student ID in the name of your application so you can find it easily later.

![Application Setup](/images/newapp.jpg)

3. Click submit and Harness will create your new application. Now we can setup the other parts of the deployment.

4. Click on Services to add our first service to this application, then click on the Add Service button. Give your service a name that includes your student ID (as you did with the application) and set the Deployment Type to Kubernetes.

![Add Service](/images/add_service.jpg)

Click submit. That will take you to the Service Overview.

5. In the Service Overview screen click on Add Artifact Source and select Docker Registry. For Source Server select Harness Docker Hub. This is a sample connection to the public hub.docker.com domain setup automatically for harness.io. In non-training or testing environments, you would most likely delete this connector. For the Docker image name put rlachhman/amazingapp OR your own DockerHub version if you are doing the CI Part by hand. 

![Artifact Source](/images/artifact_source.jpg)

Click submit when done.

6. Click on Services in the popcorn trail on the top part of the Harness UI and select Environments in the dropdown to swith to to setting up the environbment we will be deploying to.

7. Click Add Environment button and give your environment a name that starts with your student ID. Set the environment type to non-production.

![Environment](/images/environment.jpg)

When you click submit that will take you to the Environment Overview screen. 

8. Add an Infrastructure Definition. Give it a name that starts with your student ID. Select Kubernetes Cluster for your Cloud Provider Type, and set the deployment type to Kubernetes. Then you can select the Cloud Provider we have setup for this workshop. It is named "HarnessUFall2020_K8s"

Finally for Namespace please put your Student ID DO NOT leave it as default! 

![Infrastructure Definition](/images/infra_def.jpg)

Click submit when done. 

9. Click back on your popcorn trail as before and select Workflows. Click Add Workflow.

10. Give your workflow a name that starts with your Student ID. Select rolling deployment for your Deployment Type. Then for Environment, Service, and Infrastructure Definition be sure to pick the ones that start with your Student ID.

![Workflow](/images/workflow.jpg)

When you're done. Click submit.

11. Now we have just one last thing to setup on the CD side, a Trigger. Click on Setup -> "Your App Name" -> Triggers +Add Trigger.

12. Give it a name using your studentID. Then click next. 

13. Select On New Artifact for Condition. This will make the Artifact Source dropdown appear. Select rlachhman_amazingapp (or your own source if you are doing the CI portion of this Lab). Set the Build/Tag Filter to .* and tick the RegEx tickbox. (Note that .* is just an anything wildcard in RegEx.)

![Trigger](/images/trigger.jpg)

Click Next. 

14. Set your Actions Execution Type to Workflow and select your workflow from the dropdown. For Build/Version select Last Collected and then select your artifact source from the dropdown. Set the Build / Tag .* and tick the RegEx tickbox as above.

![Trigger](/images/actions.jpg)

Click Next then Submit.

15. Now we can watch Ravi demo the CI portion. When the CI cycle is complete and a new artifact appears in DockerHub your deployment should kick off. Your instructor will share a kubectl command so you can see your namespace appear once your artifact deploys. In the HarnessUI click on Continuous Deployment > Deployments on the left hand side of the screen. 

![Trigger](/images/waitforcd.jpg)





