# {u}scripted Harness University Hands-On Labs

## Hour 1 Labs

## Lab 1 - Login to app.harness.io and familiarize yourself with the environment


1. You should receive an invite to https://app.harness.io in the email you used to register for this session. Follow the links in that email to setup your login and proceed to the Harness UI.

2. Click around and explore the UI. Please note depending on the user role you have in your own organization's Harness implementation you may not have access to the menus and settings you see here in our training setup. 

3. We will be visiting the Setup menu most often. Click in there and explore the different connectors and options. 

4. Ask your instructor if you don't understand the use of any configuration or dashboard.

## Lab 2 - Setup a basic Nginx deployment on our training cluster

1. Click on the Setup menu on the left hand side of the Harness UI.

2. Click on the Add Application button and fill out the information for your new application. Be sure to use your name and at least first initial of your last name (or the name of your pet or really anything rated G that you'll remember! Note that hereinafter we will just refer to this as your name.) in the Name field of your application so you can find it easily later among all the other students. 

![Application Setup](/images/appapp.jpg)

3. Click submit and Harness will create your new application. Now we can setup the other parts of the deployment.

4. Click on Services to add our first service to this application, then click on the Add Service button. Give your service a name that includes your name (as you did with the application) and set the Deployment Type to Kubernetes.

![Add Service](/images/addservserv.jpg)

Click submit. That will take you to the Service Overview.

5. Since we specififed Kubernetes in the Service setup, Harness went ahead and created a Go Template for our workload. All we need do really to test this is specify which container image we'd like to run. To do this, in the Service Overview screen click on Add Artifact Source and select Docker Registry. For Source Server select Harness Docker Hub. This is a connection to the public hub.docker.com domain. For the Docker image name put library/nginx . That will allow us to pick our nginx version from among the many when we deploy.

![Artifact Source](/images/artisrcsrc.jpg)

Click submit when done. We won't be changing any of the preconfigured yaml at this time. We're just doing a simple first deployment. 

6. Near the top of the screen you should see the popcorn trail for your Application. Click on the drop down triangle next to Services to see all the other parts of your Application. Click on Environments to setup the next key piece of our deployment. 

![Popcorn Trail](/images/poppop.jpg)

7. Click the  Add Environment button and give your Environment your name. Set the environment type to non-production.

![Environment](/images/envenv.jpg)

When you click submit that will take you to the Environment Overview screen. 

8. It's helpful to think of an Environment as the overall category e.g., "staging" or "QA", whereas an Infrastructure Definition points to something more specific like a Kubernetes cluster or Kubernetes Namespace. Click Add Infrastructure Definition and give it your name. Select Kubernetes Cluster for your Cloud Provider Type, and set the deployment type to Kubernetes. Then you can select the Cloud Provider we have setup for this workshop called "unscripted-harnessu-k8s-cluster". Finally for Namespace please put your name. 

![Infrastructure Definition](/images/infradefdef.jpg)

Click submit when done. 

9. Click back on in the popcorn trail and switch to Workflows. Click Add Workflow.

10. Give your workflow your name and select rolling deployment for your Deployment Type. Then for Environment, Service, and Infrastructure Definition pick the ones you just created with your name.

![Workflow](/images/wkfloflo.jpg)

When you're done. Click submit.

11. Harness will crate a workflow framework, that currently just includes deploying nginx. But there's lots of room for further steps along the way. Well make a much more interesting workflow in Lab 3, we promise. 

That said, now we are ready to do the actual deploy! Click on the Deploy button in the upper right corner of the screen. That will bring up the Start New Deployment dialog box. 

12. Since we specified "library/nginx" as our artifact source we now have to pick which version of Nginx we wish to deploy. Select whichever tag you like. This is just a test after all. 

![Start New Deployment](/images/newnew.jpg)

It's a good idea for test and training deployments to select Send Notification to Me Only to avoid spamming your coworkers with test deployments. Click Submit to kick off the deployment.

13. Harness will switch to the deployment screen. Click on each box as it appears to see what information Harness provides. Click on the Rollout Deployment box to see the results from the command line on the delegate.

![Live Deployment View](/images/viewdepdep.jpg)

## Lab 3 - Cleanup the cluster

1. Now we can run a deployment to delete our previous deployment and leave our training cluster neat and tidy! I know, I know, we just installed this workload . . . but we've got cooler stuff to do ahead! Go back to Setup screen in the Harness UI and select your application. We're going to create a new Workflow to delete our namespace and the pod inside it. 

2. Click on Workflows and Add Workflow. Give this workflow a different name, but be sure to include your name. Otherwise same settings as the previous Workflow.

![Cleanup Workflow](/images/cleanclean.jpg)

Click submit.

3. By default Harness put a Rollout Deployment step in for us, but we don't actually need that. Hover your mouse over the Rollout Deployment stage and click the X that appears next to that step to delete it. 

![Remove Step](/images/norollroll.jpg)

4. Once that step is gone click on Add Step. This takes you to the Workflow step creation dialog. Click on Kubernetes and then the Delete action. 

![Delete Step](/images/deldel.jpg)

Click next.

5. Tell Harness what you want the Kubernetes delete command to delete. We will hardcode our namespace, but you could also use a variable here to Delete whatever namesapce was associated with the deployment. 

![Configure Delete](/images/confdeldel.jpg)

Click Submit.

6. Now we can run our delete deployment. Click Deploy in the upper right hand corner. You don't have to choose an image this time, because this workflow came not to deploy, but to destroy! (Sorry couldn't resist.) Once the Deploy starts click on the Delete task to watch the command line. 

![Final Delete](/images/finaldeldel.jpg)

7. Pat yourself on the back! First series of labs complete.

## Hour Two Labs

## Lab 1 - Watch Ravi Update a Test Container With Drone CI

1. Watch as our illustrious instructor Ravi shows off his container dev skills for us! We will be using the versions he creates to deploy in our lab.

## Lab 2 - Setup the CD side of the equation

In this lab we're going to setup the Continuous Delivery infrastructure which will allow us to deploy the output of the Continuous Integration with Drone we will demo or run for ourselves. 

1. Go back into the Application we made in the first hour lab, and click on Services to add our first service to this application, then click on the Add Service button. Give your service a name that includes your name (as you did with the application) and set the Deployment Type to Kubernetes.

![Add Service](/images/add_service.jpg)

Click submit. That will take you to the Service Overview.

5. In the Service Overview screen click on Add Artifact Source and select Docker Registry. For Source Server select Harness Docker Hub. This is a sample connection to the public hub.docker.com domain setup automatically for harness.io. In non-training or testing environments, you would most likely delete this connector. For the Docker image name put rlachhman/amazingapp OR your own DockerHub version if you are doing the CI Part by hand. 

![Artifact Source](/images/artifact_source.jpg)

Click submit when done.

6. Click on Services in the popcorn trail on the top part of the Harness UI and select Environments in the dropdown to swith to to setting up the Environment we will be deploying to.

7. Click Add Environment button and give your environment a name that starts with your name. Set the environment type to non-production.

![Environment](/images/environment.jpg)

When you click submit that will take you to the Environment Overview screen. 

8. Add an Infrastructure Definition. Give it a name that starts with your name. Select Kubernetes Cluster for your Cloud Provider Type, and set the deployment type to Kubernetes. Then you can select the Cloud Provider we have setup for this workshop. It is named "HarnessUFall2020_K8s"

Finally for Namespace please put your name DO NOT leave it as default! 

![Infrastructure Definition](/images/infra_def.jpg)

Click submit when done. 

9. Click back on your popcorn trail as before and select Workflows. Click Add Workflow.

10. Give your workflow a name that starts with your name. Select rolling deployment for your Deployment Type. Then for Environment, Service, and Infrastructure Definition be sure to pick the ones that start with your name.

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

## Hour 3 Labs

## Lab 1 - Setup a Harness Application for our canary deployment

1. Click on the Setup menu and go back into your Application.

2. Click on Services then click on the Add Service button. Give your service a name that includes your name and set the Deployment Type to Kubernetes. Click submit. That will take you to the Service Overview.

3. In the Service Overview screen click on Add Artifact Source and select Docker Registry. For Source Server select Harness Docker Hub. For the Docker image name put harness/cv-demo . That is pointing to the Docker image we made for this lab.

![Artifact Source](/images/demosrcsrc.png)

Click submit when done.

4. Now we need to hook our service up to a directory in Github which contains the yamls to install our demo application. To do this click on the three little dots in the upper right hand corner of the Manifests sections and select Link Remote Manifests

![remote manifests](/images/lnkremrem.jpg)

5. Provide Harness with the information to find the remote manifests on Gitbut. We are using normal K8s Resource YAMLs in a Go Template format - the same as we use in the Harness UI. We've already setup a Connector to the our Github account for you. Fill out the form like this:

Set the Manifest Format to ```Kubernetes Resource Specs in YAML format```

Set the Source Repository to ```CVProm (https://github.com/harness-training-dept/cvprom)```

Set the Branch to ```master```

Set the File/Folder path to ```workload```

![edit deployment.yaml](/images/remmanman.jpg)

Click Submit when done.

It should look like this:

![after link](/images/aftlnklnk.jpg)

6. Now that we've updated the service definition we can move on to setting up the Environment we're going to deploy to. Click on your application name in the popcorn trail on the upper left of the Harness UI to return to your Application main screen. Then click on Environments to setup an environment to deploy to. 

7. Now that we've setup a Service we can just the Environment we setup in the very first labs. Our next step is to build the canary deployment.

8. Using the popcorn trail switch to Workflows in your application. Click on the Add Workflow buttom. Give your new workflow a name that includes your name. Select Canary Deployment for your Workflow Type, and finally select the Environment you setup previously.

![workflow](/images/wfcancan.jpg)

Click submit when done. Now we are in our Workflow builder. Harness has setup an empty Canary template for us. Now let's fill it out.

9. First we're going to add a Deployment Phase. Under Deployment Phases click on + Add Phase

![add phase](/images/addphapha.jpg)

In the Phase definition select the CV Canary Service you setup just before this and the Infrastructure Definition you setup in hour 1. 

![phase setup](/images/cphasetset.jpg)

Click submit when done. Now your Workflow screen should look like this:

![deployment screen](/images/depscrcancan.jpg)

10. Ok! Now we have the Deployment framework setup. First off we're going to configure the Canary Phase of the Workflow with a verification and rollback step. First up we're going to need to add a verification phase to our canary. (This is the step where we will consult metrics from Prometheus about our Canary. (TL;DR Prometheus is an open source metrics gathering agent and search engine for distributed systems.) To set this up we'll need to add a Verification step to our Canary Phase. In the Verify section of the Canary Phase click on Add Step. Your screen should look something like this:

![add step](/images/adcandeldel.jpg)

If you don't see the Prometheus step listed just type "prom" in the search box and that should bring it up. Once it's there select it and click Next.

14. Next we are going to configure the verification by specifying what metrics we're interested in. First specify the Prometheus server we setup called Prometheus CV. Next we're going to specify our first metric to monitor. 

For the Metric Name specify "error_call"

For the Metric Type pick "Error" in the dropdown

For Group Name specify "custom" 

And for Query specify this:
```io_harness_custom_metric_error_call{kubernetes_pod_name="$hostName"}```

Click on the +Add button to add an additional metric

For the 2nd Metric:

Metric Name specify "normal_call"

For the Metric Type pick "Throughput" in the dropdown

For Group Name specify "custom" 

And for Query specify this:
```io_harness_custom_metric_normal_call{kubernetes_pod_name="$hostName"}```

When you're done it should look like this:

![two metrics](/images/metricscancan.jpg)

15. Set your analysis time to 5 mins and your algorhytim to "very sensitive". 

Should look like this:

![analysis time](/images/analysiscancan.jpg)

Hit Submit when done. Your Canary Phase should now look like this: 

![verifyfinal](/images/verifinalfinal.jpg)

16. Now we need to specify a Roll Back Setp to delete the Canary if the deployment fails. Under Rollback Steps select "Add Step" under "1. Deploy" Search for the "Delete" step by typing del into the search box. Select the Delete command and click Next.

![delsearch](/images/delsrchcancan.jpg)

17. Give your Delete step a name and then specify ```${k8s.canaryWorkload}``` for Resources. That's a variable that specifies the Canary workload during the deployment.

![candel](/images/aurevoircancan.jpg)

Click Submit when done. Now your Workflow should look like this:

![canwf](/images/wfmoremore.jpg)

18. Go back out of the Canary Phase of your Workflow and into the main part of your workflow. Your screen should look like this:

![nophase](/images/nophase.jpg)

19. Now we're going to add the main deployment phase that will happen after a successful canary. To do that click on + Add Phase under Deployment Phases. You will need to select the same Service and Infrastructure as you did for the Canary Phase. 

![phasephase](/images/phasephase.jpg)

Click Submit when done. Now you have a Rolling Deployment phase all setup that runs after a sucessful Canary.

20. Go back out to the main part of your Workflow to add two Workflow Variables to our workflow. Click on edit icon next to Workflow Variables.

![wfvedit](/images/workflowvar1.jpg)

Then click on the + Add button and add the following two variables:

Variable Name: verify_canary

Default Value: yes

All else leave as is. 

Variable Name: metric_verification

Default Value: Prometheus

All else leave as it. 

Should look exactly like this before you hit Save. 

![wfvar](/images/wfvar2.jpg)

Now you're back out with a completed Canary Workflow! Well done!

![wfalldone](/images/wfalldone.jpg)

21. Now! we are ready to start deploying. But remember a Canary is designed to be compared to an already running microservice. So first we have to Deploy once to setup a baseline to compare our Canary to. To do this we'll run our Deployment but skip the verification stage. Scroll up to the top of the Workflow Overview screen and Click on the big blue Deploy button:

![deploybang](/images/deploybang.jpg)

22. That brings up our Start New Deployment screen. Change the verify_canary variable to no - this tells Harness to skip/automatically pass the Verify step. Leave metric_verification the default. Select the Tag# stable artifact.

![firstgood](/images/firstgood.jpg)

Hit submit when done. 

![alldonefirst](/images/alldone1st.jpg)

Now we have one good deployment to compare our canaries to! Take a moment to inspect the Prometheus step in your Canary Phase. You may need to scroll to left to get back over to it. 

![firstprom](/images/1stprom.jpg)

23. Take a 5 minute coffee / tea / beer / soda break to let our stable version build up some nice stable data in Prometheus. 

24. Ok welcome back. Now we can rerun our Deployment. But this time we're going to enable verification and we're going to deploy a less stable version. Go back into the Setup screen and select your application. Then go to your Workflow and hit Deploy. Leave both variables at their defaults but this time select the Tag# unstable version of the container. Hit Deploy when done. 

![badcanary](/images/badcanary.jpg)

25. While your canary deployment is running. Click on the Prometheus step to watch the verification process run. This can take a bit of time so feel free to freshen up the beverage from step 27. 

![promrunnin](/images/promrunnin.jpg)

26. Once the Prometheus step has completed and we realize that the artifact tagged unstable turned out to be unstable! The Canary gets marked failed and the Canary Phase Rollback step we created was run to delete the suspect Canary. 

![arcan](/images/arcan.jpg)




