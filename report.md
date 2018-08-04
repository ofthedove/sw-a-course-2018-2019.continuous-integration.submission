# Comparison of Travis CI and Skynet

The purpose of this report is to evaluate continuous integration tools for use by Aperture Science, and reccomend a specific tool based on a variety of critera.

## Overview

The software being evaluated will be expected enable continous integration by performing automated builds. Both tools under evaluation are able to perform automated builds based on configuration files stored in the repository with the code being built. Both tools provide some level of configuration, but have different abilities and advantages.

## Travis CI

Travis CI is a third party tool that integrates with github and performs automated builds, either scheduled or event triggered, for any repository containing an appropriate configuration file. Travis CI is available either as a service, or self hosted, and is free for open source projects. The ability to quickly evaluate Travis CI without aquiring and configuring physical servers is a definite advantage, though for security reasons a production system would be locally hosted. 

## Skynet

Skynet is custom software built on Jenkins, another popular third party tool. Skynet has many of the same features as Travis CI, while still retaining some of the advantages of Jenkins. For example, Skynet is configured by a configuration file stored alongside code in a repository, similary to Travis CI. Skynet also benefits from Jenkins' support of more build platforms than Travis CI. However, unline Travis CI, Skynet is a strictly self-hosted application, requiring dedicated servers for use.

As custom software, Skynet has several advantages and disadvantages. Because we own both the servers and the code for Skynet, we have the ability to adapt it to suit our needs. In contrast, Travis CI is less flexible, but benefits from third party support. 

## Conclusion

Because we require the security and scale of a self-hosted solution, and because we can spread the support costs over a large number of teams and projects, Skynet is recommened for use. While Travis CI may be an excellent choice for small and open source projects, at scale it cannot compete with the improved compatability and adaptability of Skynet.