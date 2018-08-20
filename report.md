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
Travis CI has a proven record of reliable service, and the enterprise license includes support. If Travis CI were to experience an outage, they would be responsible. However, communications issues due to a support contact's unfamiliarity with our systems and lack of access to our data centers could result in longer than necessary downtimes.

### Skynet
The reliability of Skynet will be heavily dependant upon project management. If initial development is well managed, and sufficient resources are allocated for program maintenance, Skynet is expected to have reliability similar to Travis CI. However, when issues do emerge no outside support will be available; the company will be entirely responsible for bringing the program back online. This could prove to be an asset, however, since support staff will be thoroughly familiar with the software and our configuration, and will already have security clearance.

## Extensibility
### Travis CI
While Travis CI ships as a complete solution, it does have an API to allow for the development of extensions and external tools. This API is limited, though, and doesn't offer nearly the customization potential of Skynet.

### Skynet
As custom software, Travis CI is nearly infinitely extensible. This is a significant advantage when undertaking projects as diverse and unusual as those pursued by Aperature Science. However, this advantage is not without risk. Every extension and modification increases maintenance requirements, and to a greater degree the more unusual the modification. "Infinitely extensible" is better stated "As extensible as you can afford." 

## Workflow Integration
### Travis CI
Travis CI integrates with GitHub, in our case integrating with our local GitHub Enterprise instance. Repositories can easily be added to Travis CI, and automated builds will occur once a .travis.yml configuration file has been added to the repository. Options for when to perform builds can be easily changed, and default to building any time a branch or pull request is pushed. Builds can also be performed on a monthly, weekly, or daily basis. Builds will only occur for branches which contain a .travis.yml file.

The .travis.yml file contains all the information needed to perform the build. The most basic configuration file states the language used, though many more options are available. The most common are used to set the os and os version, set required permissions, specify the build script to run, install dependancies, and modify Git's behavior. One popular feature of .travis.yml configuration is the build matrix, which allows you to specificy several paramaters and will automatically perform builds for every combination of parameters, with some additional customization options.

### Skynet
Skynet obtains build configuration from a skynet.lua configuration file. Unlike Travis CI, this file applies to the whole repository and cannot differ between branches. Only the skynet.lua file in the `build` branch will be considerd when peforming builds for the repository, and it is reccomended to remove all other files in the `build` branch. Repositories will only be considered after being added to the repos.lua file in the applcommon.skynet repository.

The skynet.lua and .travis.yml files contain similar info, but differ in key ways. Because the skynet.lua files applies to the whole repository, it can contain configuration for when builds are performed. Like Travis CI, builds can be triggered by a push, a pull request, or a cron job. Unlike Travis CI, the builds performed by each of these events are independant and can have different configurations. For each event, multiple builds can be configured. Each build specifies the tools to be used, and the script to be run. Other parameters are available, though not as many as Travis CI. Of course, if a new feature is required it can be added, and there is no reason to support features our organization is not using.

It should also be noted that Skynet is not strictly confined to GitHub, as the underlying Jenkins software is compatable with a variety of version control systems and hosts. 

## Conclusion
Because security and customization are of critical importance, a self-hosted, internally developed and maintained solution is attractive. Due to the scale of software development undertaken by the company, support costs can be spread over a large number of teams and projects, lessening the financial burden of custom software. For these reasons, Skynet is recommened for use.