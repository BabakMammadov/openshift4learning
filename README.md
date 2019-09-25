# openshift4learning
Taken notes during learning OpenShift on https://learn.openshift.com

- [Getting Started with OpenShift for Developers](#getting-started-with-openshift-for-developers)

## Getting Started with OpenShift for Developers
### Step 1 - Exploring The Command Line
The OpenShift CLI is accessed using the command oc. From here, you can administrate the entire OpenShift cluster and deploy new applications.
  
The CLI exposes the underlying Kubernetes orchestration system with the enhancements made by OpenShift. Users familiar with Kubernetes will be able to adapt to OpenShift quickly. The CLI is ideal in situations where you are:
  
1) Working directly with project source code
2) Scripting OpenShift operations
3) Restricted by bandwidth resources and cannot use the web console
  
For this section, our task is going to be creating our first project.

###### What is a project? Why does it matter?
The goal of this section is to get a project created and running, which you'll be doing with the web console in the next section.
  
OpenShift is often referred to as a container application platform in that it is a platform designed for the development and deployment of containers.
  
To contain your application, we use projects. The reason for having a project to contain your application is to allow for controlled access and quotas for developers or teams.
  
More technically, it's a visualization of the Kubernetes namespace based on the developer access controls.

###### Command Line Interface (CLI)
In this course, we're not focusing on the OpenShift CLI, but we want you to be aware of it in case using the command line is your thing. You can check out our other courses that go into the use of the CLI in more depth. Now, we're just going to practice logging in so you can get some experience with how the CLI works.
  
###### Task
Let's get started by logging in. Your task is to enter the following into the console:
``` oc login ``` - login on CLI. Write down your **username** and **password** once prompted.
``` whoami ``` - check your login details
  
That's it!
  
In the next step, we'll get started with creating your first project using the web console.

### Step 2 - Exploring The Web Console
While the command line tool is awesome, for this course we are going to focus on the web console, which is equally awesome.

###### Task 1
To begin, click on the Dashboard tab on your screen. This will open the web console on your browser.

You should see an OKD window with Username and Password forms as shown below:

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img1.png)

For this scenario, log in by entering the following:
  
Username: **developer**
  
Password: **developer**
  
After logging in to the web console, you'll see a blue button labeled Create Project in the top right corner of your screen that is shown below. Click this button to get started.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img2.png)

