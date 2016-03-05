# ose-binary-builds

Demonstrates the usage of [binary build](https://docs.openshift.com/enterprise/3.1/dev_guide/builds.html#binary-source) types in OpenShift

## Templates

Each of the examples described below can be deployed to OpenShift through the use of [templates](https://docs.openshift.com/enterprise/3.1/architecture/core_concepts/templates.html) found in the [templates](templates) folder

## Examples

The following examples are available to demonstrate the the usage of Binary builds. It is expected that a [project](https://docs.openshift.com/enterprise/3.1/dev_guide/projects.html) be available or a new project created for each of the examples.

### CakePHP Source Code

The [cakephp-binary-build-with-src](cakephp-binary-build-with-src) folder contains the source code for a complete [CakePHP](http://cakephp.org/) application

Instantiate the template by navigating to the templates folder and running the following command:

    oc process -f cakephp-binary-build.json | oc create -f -
    
Cancel the initial build that is automatically started

    oc cancel-build cakephp-binary-app-1
    
Navigating back the root of the repository, execute the following command to upload the *cakephp-binary-build-with-src* folder as the source for the build

    oc start-build cakephp-binary-app --from-dir=cakephp-binary-build-with-src
    
Once the build completes, the application can be accessed through the route created as part of the template instantiation. To determine the URL of the route, run *oc get routes*

### JBoss EAP Artifact

Compiled artifacts, such as Java Web Archives can be easily deployed to OpenShift through the use of Binary builds. When used in conjunction with the [Source to Image](https://docs.openshift.com/enterprise/3.1/architecture/core_concepts/builds_and_image_streams.html#source-build), artifacts can be deployed to the platform within the image automatically. 

The [jboss-binary-build-with-artifact](jboss-binary-build-with-artifact) folder contains the folder structure necessary to deploy pre-built artifacts to the JBoss platform during a source to image build. The *deployments* folder contains a sample web archive based application named *ROOT.war* which will result in the application being accessible at the root context when the image is used within a running container.

Instantiate the template by navigating to the templates folder and running the following command:

    oc process -f jboss-eap64-binary-build.json | oc create -f -
    
Cancel the initial build that is automatically started

    oc cancel-build eap-binary-app-1
    
Navigating back the root of the repository, execute the following command to upload the *jboss-binary-build-with-artifact* folder as the source for the build

    oc start-build eap-binary-app --from-dir=jboss-binary-build-with-artifact
    
Once the build completes, the application can be accessed through the route created as part of the template instantiation. To determine the URL of the route, run *oc get routes*