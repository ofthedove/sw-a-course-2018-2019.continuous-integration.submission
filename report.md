# Comparison of Travis CI and Skynet

## Introduction
In light of recent research into software development process improvement, Aperature Science has decided to mandate the use of continuous integration in software development programs. To this end, build and test automation software must be aquired. Preliminary research has narrowed the available options to two: Travis CI and Skynet. The purpose of this report is to compare these tools and reccomend a specific tool based on a variety of critera.

## Problem Definition
Aperature science has dozens of teams of software developers working across hundreds of repositories. To enable CI for all of these projects and teams, the software must be scalable and support a variety of languages and configurations.

Any developer should be able to create a repository, add build and test configuration, and add the repository to the CI system. While specific workflows may vary, the system should the perform automated builds at designated times.

## Implementation Overview
### Travis CI
Travis CI is a third party tool that integrates with github and performs automated builds, either scheduled or event triggered, for any repository containing an appropriate configuration file. Travis CI is available either as a service, or self hosted, and is free for open source projects. The ability to quickly evaluate Travis CI without aquiring and configuring physical servers is a definite advantage, though for security reasons a production system would be locally hosted. 

### Skynet
Skynet is custom software built on Jenkins, another popular third party tool. Skynet has many of the same features as Travis CI, while still retaining some of the advantages of Jenkins. Skynet benefits from Jenkins' support of more build platforms than Travis CI. However, unline Travis CI, Skynet is a strictly self-hosted application, requiring dedicated servers for use.

As custom software, Skynet has several advantages and disadvantages. Because both the servers and the code for Skynet would be interally owned, there is greater ability to adapt it to suit our needs. In contrast, Travis CI is less flexible, but benefits from third party support. 

## Security
### Travis CI
For most projects, Travis CI is sold as a service. However, Enterprise liscensing is available and allows Travis CI to be run on local servers, or in the cloud environment of our choosing. Travis CI Enterprise also supports GitHub Enterprise, meaning it can be used without exposing any of our code or data to the world outside our network. However, Travis CI may not offer full source code with Enterprise liscensing, which could lead to auditing issues and the potential for vulnerabilities.

### Skynet
As custom software, Skynet requires internally managed servers, simplifying data security. Also, because Skynet is internally developed and based on the open-source Jenkins software, it's code can be fully audited to provide an additional layer of security.

## Cost
### Travis CI
Costs associated with Travis CI include hosting and licensing. Assuming 100 users, annual liscensing fees will be $40,000. This figure includes unlimited concurrent builds, updates, and support. While the resources required to perform a build and the number of builds per day will vary widely between projects, it is estimated that adding the required build servers to existing data centers will cost $75,000 per year. Because dedicated servers will be used, these costs will be static.

### Skynet
Because Skynet is based on Open Source tools, there will be no liscensing fees. (Excepting OS or complier liscensing to actually run the builds, which should be negligable since most development is on Linux or GLaDOS.) Hosting fees for Skynet should be comperable to Travis CI, since the underlying builds are the same. However, there may be a slight reduction in resource usage versus Travis CI since Skynet reuses build environments. The greatest cost associated with Skynet is development and maintenance. Basing Skynet on Jenkins helps, but significant development work will be needed to bring the system online.  Estimated first year development costs are $150,000 with an estimated $30,000 in maintenance required thereafter. These costs are only estimates, and with custom and open-source software the company is ultimately responsible for costs related to critical bugs and vulnerabilities. 

## Reliability
### Travis CI
Good, not our problem

### Skynet
Depends on how well we build it, our problem if it breaks

## Extensibility
### Travis CI
Read docs on plugins

### Skynet
Totally extensible, we (mostly) built it ourselves!

## Workflow Integration
### Travis CI
Easy if you're already using GitHub

### Skynet
Maybe?

## Conclusion
Because we require the security and scale of a self-hosted solution, and because we can spread the support costs over a large number of teams and projects, Skynet is recommened for use. While Travis CI may be an excellent choice for small and open source projects, at scale it cannot compete with the improved compatability and adaptability of Skynet.
