# jenkins-based-rpm-builder
A multi branch pipeline based RPM build utility

# Introduction
For IT operations teams, especially middleware teams, periodically maintaining custom RPM packages is a laborious and thankless job. It is important for the security and integrity of IT systems that all RPM packages are updated periodically to more stable releases. This tool is a small initiative to make this task easier for IT administrators. This is limited to packages for RedHat and CentOS distributions onlu

# Custom RPM packages
RHEL administrators are no strangers to RPM files. While it is true that Redhat releases periodic updates and fully supports Apache distributions like Tomcat, APR and HTTPD, it is also true that these releases substantially lag compared to stable releases from Apache. From both security and performance standpoint, it is important to update these packages regularly.

# Manual Process
Following are the overall steps involved in custom RPM package generation.

- Download the necessary source code and host it in standard location in build server
- Edit relevant SPEC file to include required changes 
- Generate the RPM in the build server
- Deploy the packages to YUM repository

# Drawbacks of present approach
- Each step is manual and prone to error
- The process is time consuming
- The unnecessary complexity of the process delays updates to software components
- Version control of both source code and artifacts are done manually
- Rollback process is equally cumbersome and time consuming

# Proposed Approach

![Architecture](https://github.com/senthilmnathan/jenkins-based-rpm-builder/blob/master/architecture.png)

# Build Components
## Source Code Repository
In this GitHub repository, all the necessary build components are present. Any new updates can be made here and jenkins pipeline will take care of the build process

## Jenkins Pipeline
A dedicated Jenkins pipeline will build the RPMs and Source RPMs (SRPM) files from the new source code in GitHub repository. It fetches the source code, runs the build script on top of it and generates the RPM artifacts.

# Build Process
Once the code is commited in GitHub, it will trigger the Jenkins pipeline and the RPMs are generated automatically. 

# Setting Up the Jenkins Pipeline
A multi branch jenkins pipeline must be created targetting this GitHub repository which hosts the jenkins file. Once this job is created, the build process is automatically done

# Dependencies
The jenkins instance where the job is created is expected to contain the location, **/var/jenkins_home**. There are no other dependencies.

# Enhancements
This tool can be further expanded to include
(1) Stage to automatically update YUM repository used by Linux servers
(2) Stash the generated RPM files to Artifactory or some other Git based repository for source control
(3) While  this pipeline is limited to few middleware packages, the logic can be expanded to other RPMs too.




