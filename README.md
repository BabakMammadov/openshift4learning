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

You should now see a page for creating your first project in the web console. Fill in the Name field as myproject.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img3.png)

The rest of the form is optional and up to you to fill in or ignore. Click Create to continue.

After your project is created, your project will appear under My Projects, and you can click on myproject to access your newly created project.

###### Task 2
Notice the menu on the left. You're now currently on the Overview screen. The tools that you'll need for building and deploying your application can also be found here on the left.

Take a quick look around these, clicking on Applications, Builds, and Resources to see more options. There won't be much there for now as we have nothing in our project.

We'll get into those in future sections, but go ahead and explore to see what's possible! Don't spend too much time on these now as you will get to use a lot of these features in the upcoming sections.

### Step 3 - Deploying a Docker Image
In this section, you are going to deploy the front end component of an application called **parksmap**. The web application will display an interactive map, which will be used to display the location of major national parks from all over the world.

###### Exercise: Deploying your first Image
The simplest way to deploy an application in OpenShift is to take an existing Docker-formatted image and run it. We are going to use the OpenShift web console to do this, so ensure you have the OpenShift web console open and that you are in the project called **myproject**.

The OpenShift web console provides various options to deploy an application to a project. For this section, we are going to use the Deploy Image method. As the project is empty at this point, the Overview page should display the following options: *Browse Catalog, Deploy Image, Import YAML/JSON, and Select from Project. Choose the Deploy Image* button.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img4.png)

You could also have selected the Add to Project drop down menu in the top right corner of the project and selected Deploy Image to go directly to the required tab. We'll use the Add to Project option in later sections.

Within the Deploy Image page, choose the Image Name option. This will be used to reference an existing Docker-formatted image hosted on a Docker Hub Registry. For the name of the image, enter the following:

```openshiftroadshow/parksmap-katacoda:1.2.0```

Press enter or click on the magnifying glass icon to the right of the text entry box to be presented with information about the image:

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img5.png)

At this point, OpenShift will pull down and display key information about the image and the pending deployment, as well as populate the Name field with parksmap-katacoda. This name will be what is used for your application and the various components created that relate to it. Leave this as the generated value as steps given in the upcoming sections will use this name.

You are ready to deploy the existing Docker-formatted image. Hit the blue Deploy button at the bottom of the screen, and, in the subsequent page, click the Continue to the project overview link. This should bring you back to the Overview page where summary information about the application you just deployed will be displayed.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img6.png)