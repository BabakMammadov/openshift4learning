# openshift4learning
Taken notes during learning OpenShift on https://learn.openshift.com
- [Foundations of OpenShift](#foundations-of-openShift)
    - [Getting Started with OpenShift for Developers](#getting-started-with-openshift-for-developers)
    - [Logging in to an OpenShift Cluster](#logging-in-to-an-openshift-cluster)
    - [Deploying Applications From Images](#deploying-applications-from-images)
    - [Deploying Applications From Source](#deploying-applications-from-source)
    - [Using the CLI to Manage Resource Objects](#using-the-cli-to-manage-resource-objects)
    - [Connecting to a Database Using Port Forwarding](#connecting-to-a-database-using-port-forwarding)
    - [Transferring Files in and out of Containers](#transferring-files-in-and-out-of-containers)

## Foundations of OpenShift
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

These are all the steps you need to run to get a "vanilla" Docker-formatted image deployed on OpenShift. This should work with any Docker-formatted image that follows best practices, such as defining the port any service is exposed on, not needing to run specifically as the root user or other dedicated user, and which embeds a default command for running the application.

### Step 4 - Scaling Your Application
Let's scale our application up to 2 instances of the pods. You can do this by clicking the "up" arrow next to the Pod in the OpenShift web console on the overview page.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img7.png)

To verify that we changed the number of replicas, click the pods number in the circle next to the arrows. You should see a list with your pods similar to the following by scrolling to the bottom of the web console:

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img8.png)

You can see that we now have 2 replicas.

Overall, that's how simple it is to scale an application (Pods in a Service). Application scaling can happen extremely quickly because OpenShift is just launching new instances of an existing image, especially if that image is already cached on the node.

###### Application "Self Healing"
Because OpenShift's DeploymentConfigs are constantly monitoring to see that the desired number of Pods is actually running, you might also expect that OpenShift will fix the situation if it is ever not right. You would be correct!

Since we have two Pods running right now, let's see what happens if we "accidentally" kill one.

On the same page where you viewed the list of pods after scaling to 2 replicas, open one of the pods by clicking its name in the list.

In the top right corner of the page, there is an Actions tab. When opened, there is the Delete action.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img9.png)

Click Delete and confirm the dialog. You will be taken back to the page listing pods, however, this time, there are three pods.

The pod that we deleted is terminating (i.e., it is being cleaned up). A new pod was created because OpenShift will always make sure that, if one pod dies, there is going to be new pod created to fill its place.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img10.png)

###### Exercise: Scale Down
Before we continue, go ahead and scale your application down to a single instance. It's as simple as clicking the down arrow on the Overview page.

### Step 5 - Routing HTTP Requests
Services provide internal abstraction and load balancing within an OpenShift environment, but sometimes clients (users, systems, devices, etc.) outside of OpenShift need to access an application. The way that external clients are able to access applications running in OpenShift is through the OpenShift routing layer. The data object behind that layer is a Route.

The default OpenShift router (HAProxy) uses the HTTP header of the incoming request to determine where to proxy the connection. You can optionally define security, such as TLS, for the Route. If you want your Services, and, by extension, your Pods, to be accessible to the outside world, you need to create a Route.

###### Task: Creating a Route
Fortunately, creating a Route is a pretty straight-forward process. You just click the Create Route link displayed against the application on the Overview page.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img11.png)

By default, OpenShift is configured to create the Route based on the Service name being exposed and the Project where the application lives, adding a common subdomain configured at the platform level. In our scenario, we have:

**https://2886795272-8443-simba07.environments.katacoda.com/**

This means that there is no need to change the default settings in the Route creation form.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img12.png)

Once you click Create, the Route will be created and displayed in the Overview page.

We can also get the list of all the existing Routes by clicking the Applications->Routes menu:

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img13.png)

Currently the list of Routes will only display the one we just created.

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img14.png)

In this list, we will be able to see the details associated with the route, such as the hostname, the service, the port the route is exposing, and details on the TLS security for the route, if any.

You can always click on the Route name in this list to modify an existing Route.

Now that we know how to create a Route, let's verify that the application is really available at the URL shown in the web console. Click the link and you will see:

![img](https://github.com/Bes0n/openshift4learning/blob/master/images/img15.png)


## Logging in to an OpenShift Cluster

In this course you learnt about how to log into an OpenShift cluster, as well as how you can add other users as collaborators to you project.

You can find a summary of the key commands covered below, along with some related commands. To see more information on each oc command, run it with the --help option.

- ```oc login``` - Log in to your OpenShift cluster and save the session token for subsequent use. You will be prompted for the user name and password or directed to a web console page where you can obtain a token you must then use to use to login from the command line. The web page will require you to first login in to the web console if you are not already logged in.

- ```oc login <server>``` - Log in to a specific OpenShift cluster. You will need to specify the name of the server as argument the first time you are using it, or if switching back to it after having used a different cluster.

- ```oc login --username <user>``` - Log in to your OpenShift cluster as a specific user.

- ```oc login --username <username> --password <password>``` - Log in to your OpenShift cluster as a specific user and supply the password on the command line. Note that this is not recommended for real systems as your password may be logged or retained in command history.

- ```oc login --token <token>``` - Log in to your server using a token for an existing session.

- ```oc logout``` - Log out of the active session by clearing the session token.

- ```oc whoami``` - Show the name of the user for the current login session.

- ```oc whoami --token``` - Show the token for the current login session.

- ```oc whoami --show-server``` - Show which OpenShift cluster you are logged into.

- ```oc whoami --show-context``` - Shows the context for the current session. This will include details about the project, server and name of user, in that order.

- ```oc config get-clusters``` - Show a list of all OpenShift clusters ever logged in to.

- ```oc config get-contexts``` - Show a list of contexts for all sessions ever created. For each context listed, this will include details about the project, server and name of user, in that order.

- ```oc adm policy add-role-to-user edit <username> -n <project>``` - Add another user to a project so that they can work within the project, including creating new deployments or deleting applications.

- ```oc adm policy add-role-to-user view <username> -n <project>``` -  Add another user to a project but such that they can only view what is in the project.

- ```oc adm policy add-role-to-user admin <username> -n <project>``` - Add another user to a project such that they are effectively a joint owner of the project and have administration rights over it, including the ability to delete the project.


## Deploying Applications From Images

In this course you learnt about deploying an existing Docker-formatted container image to OpenShift. You first deployed an image direct from an external image registry. This was followed by importing an image into the OpenShift internal registry, and then deploying the image from the internal registry.

You can find a summary of the key commands covered below. To see more information on each oc command, run it with the --help option.

- ```oc new-app <docker-image> --name <name>``` - Deploy an application from a Docker-formatted image found on an external image registry. If there is any ambiguity as to the source of the image, use the --docker-image option.

- ```oc new-app <image-stream> --name <name>``` - Deploy an application from a Docker-formatted image found in the internal image registry. If there is any ambiguity as to the source of the image, use the --image-stream option.

- ```oc import-image <docker-image> --confirm``` - Import a Docker-formatted image found on an external image registry, causing it to be pulled into the internal image registry.


## Deploying Applications From Source

In this course you learnt about deploying an application from source code using a Source-to-Image (S2I) builder. You first deployed the application from the web console, following that up with using the command line. You also learnt about using binary input source builds to run builds using source code from a local directory on your own computer.

The web application you deployed was implemented using the Python programming language. OpenShift provides S2I builders for a number of different programming languages/frameworks in addition to Python. These include Java, NodeJS, Perl, PHP and Ruby.

You can find a summary of the key commands covered below. To see more information on each oc command, run it with the --help option.

- ```oc new-app <image:tag>~<source-code> --name <name>``` - Deploy an application from source code hosted on a Git repository using the specified S2I builder image.

- ```oc start-build <name>``` - Trigger a new build and deployment of the application where source code is taken from the hosted Git repository specified to oc new-app when the build configuration was created.

- ```oc start-build <name> --from-dir=.``` - Trigger a new build and deployment of the application where source code is taken from the current working directory of the local machine where the oc command is being run.

- ```oc cancel-build <build>``` - Cancel a running build.

- ```oc logs bc/<name> --follow``` - Monitor the log output from the current build for the application.

- ```oc get builds``` - Display a list of all builds, completed, cancelled and running.

- ```oc get builds --watch``` - Monitor the progress of any active builds.

- ```oc get pods --watch``` - Monitor any activity related to pods in the project. This will include pods run to handle building and deployment of an application.

## Using the CLI to Manage Resource Objects

In this course you learnt about oc commands you would use for querying and updating the resource objects that OpenShift uses to track the state of the cluster.

You can find a summary of the key commands covered below. To see more information on each oc command, run it with the --help option.

- ```oc types```: Shows an introduction to core OpenShift concepts and types.

- ```oc explain <setting-path>```: Shows a description of the purpose of a specific resource object type setting.

- ```oc get```: Shows a list of all the resource object types you can make queries about.

- ```oc get <type>```: Shows summary details of all resource objects of a specific type.

- ```oc get <type> --selector app=<name>```: Shows summary details of all resource objects of a type with the specified label.

- ```oc get <type/name>```: Show summary details of a resource object.

- ```oc get <type/name> -o <json|yaml>```: Shows raw details of a resource object type as JSON or YAML.

- ```oc get all```: Shows summary details of the key resource objects in a project. The list of resource object types matched by all includes buildconfigs, builds, imagestreams, deploymentconfigs, replicationcontrollers, routes, services and pods.

- ```oc get all --selector app=<name>```: Shows summary details of the key resource objects in a project with the specified label.

- ```oc describe <type/name>```: Shows human readable long form description of a resource object.

- ```oc edit <type/name> -o <json|yaml>```: Edit the raw details of a resource object type as JSON or YAML.

- ```oc export <type/name> -o <json|yaml>```: Shows raw details of a resource object type as JSON or YAML where any settings not required when creating a resource object have been removed.

- ```oc create -f <definition.json>```: Create a resource object from a definition stored in a file. The format of the definition must be JSON or YAML. The metadata.name field of the definition must not correspond to an existing resource object.

- ```oc replace -f <definition.json>```: Replace the definition of a resource object with that stored in a file. The format of the definition must be JSON or YAML. The metadata.name field of the definition must correspond to an existing resource object.

- ```oc apply -f <definition.json>```: Replace the definition of a resource object if it exists with that stored in a file. The format of the definition must be JSON or YAML. The metadata.name field of the definition must correspond to an existing resource object. If the resource object does not already exist, it will be created.

- ```oc patch <type/name> --patch <patch>```: Update a resource object using a patch specification.

- ```oc label <type/name> <name=value>```: Add a label to a resource object.

- ```oc label <type/name> <name->```: Remove a label from a resource object.

- ```oc delete <type/name>```: Delete a resource object.

- ```oc delete <type> --selector app=<name>```: Delete all resource objects of a type with the specified label.

- ```oc delete <type> --all```: Delete all resource objects of a specific type.

- ```oc delete all --all```: Delete all key resource objects in a project. The list of resource object types matched by all includes buildconfigs, builds, imagestreams, deploymentconfigs, replicationcontrollers, routes, services and pods.

- ```oc delete all --selector app=<name>```: Delete all key resource objects in a project with the specified label.

## Connecting to a Database Using Port Forwarding

In this course you learnt about oc commands you would use for setting up a temporary connection between your local machine and a service running inside of OpenShift.

You can find a summary of the key commands covered below. To see more information on each oc command, run it with the --help option.

- ```oc rsh <pod-name>```: Start an interactive shell in the specified pod.

- ```oc port-forward <pod-name> <local-port>:<remote-port>```: Forward connections between your local machine and an application running in OpenShift. The remote port is the port the application running in OpenShift accepts connections. The local port is the port on your local machine you wish to make it available as, and to which any client application running on your local machine would connect to.

- ```oc port-forward <pod-name> :<remote-port>```: Forward connections between your local machine and an application running in OpenShift. The remote port is the port the application running in OpenShift accepts connections. As a local port to use is not specified, a random local port is used, with the port number being displayed. Any client application running on your local machine would connect to the randomly assigned port.

## Transferring Files in and out of Containers

In this course you learnt about oc commands you can use to transfer files to and from a running container, as well as how to set up live synchronization so changes are automatically copied from a local machine into a running container.

You can find a summary of the key commands covered below. To see more information on each oc command, run it with the --help option.

- ```oc rsync <pod-name>:/remote/dir/filename ./local/dir```: Copy a single file from the pod to the local directory.

- ```oc rsync <pod-name>:/remote/dir ./local/dir```: Copy the directory from the pod to the local directory.

- ```oc rsync <pod-name>:/remote/dir/. ./local/dir```: Copy the contents of the directory from the pod to the local directory.

- ```oc rsync <pod-name>:/remote/dir ./local/dir --delete```: Copy the contents of the directory from the pod to the local directory. The --delete option ensures that the resulting directories will match exactly, with directories/files in the local directory which are not found in the pod being deleted.

- ```oc rsync ./local/dir <pod-name>:/remote/dir --no-perms```: Copy the directory to the remote directory in the pod. The --no-perms option ensures that no attempt is made to transfer permissions, which can fail if remote directories are not owned by user container runs as.

- ```oc rsync ./local/dir <pod-name>:/remote/dir --exclude=* --include=<filename> --no-perms```: Copy the single file to the remote directory in the pod. The --no-perms option ensures that no attempt is made to transfer permissions, which can fail if remote directories are not owned by user container runs as.

- ```oc rsync ./local/dir <pod-name>:/remote/dir --no-perms --watch```: Copy the directory to the remote directory in the pod and then keep the remote directory syncrhonized with the local directory, with any changed files automatically being copied to the pod. The --no-perms option ensures that no attempt is made to transfer permissions, which can fail if remote directories are not owned by user container runs as. The --watch option is what enables the synchronization mechanism.

- ```oc run dummy --image centos/httpd-24-centos7```: Run a dummy application pod which can be used to mount persistent volumes to facilitate copying files to a persistent volume.

- ```oc set volume dc/dummy --add --name=tmp-mount --claim-name=<claim-name> --type pvc --claim-size=1G --mount-path /mnt```: Claim a persistent volume and mount it against a dummy application pod at the directory /mnt so files can be copied into the persistent volume using oc rsync.

- ```oc set volume dc/dummy --add --name=tmp-mount --claim-name=<claim-name> --mount-path /mnt```: Mount an existing persistent volume against a dummy application pod at the directory /mnt so files can be copied into the persistent volume using oc rsync.

- ```oc rsync ./local/dir <pod-name>:/remote/dir --strategy=tar```: Copy the directory to the remote directory in the pod. The --strategy=tar option indicates to use tar to copy the files rather than rsync.
