# SEP 2 - Upgrade Sirius to PHP 7

## Introduction

Sirius and the other OPG PHP projects are currently running on PHP version 5.5 this is an outdated version which PHP no longer supports with security or bug fix releases. This SEP proposes upgrading our code to the latest released version of PHP, PHP 7.1 and to put in place guidance to ensure we always stay up to date with the latest versions in the future.

A spike was completed to establish how much work this change would be, the findings suggest that the code can be fairly easily brought up to date however we will first need to do work to upgrade the code dependencies eg Zend framework. It also highlighted a need for WebOps to be able to support this change across the full stack including DigiDeps and LPA.

## Proposal

To be able to follow the latest PHP releases, we will need to switch away from the default bundled PHP from the ubuntu repositories and instead follow the third party PPA: https://launchpad.net/~ondrej/+archive/ubuntu/php which is a well maintained repository containing co-installable PHP packages for all currently supported versions. This will minimise the overhead from ops required to support multiple versions of PHP as different projects will be ready to upgrade at different times. It also decouples the upgrade from the ubuntu version so we don't need to upgrade the whole OS to get the latest released version.

The implementation steps for Devops would be 

1) Update docker file for PHP FPM to remove the default ubuntu PHP package.
2) Add the PHP apt repository from above. This allows for co-installable PHP 5.6, 7.0 and 7.1 and most common PHP extensions. Although the apt repository is a third party one, it is considered the recommended way to install alternative PHP versions on ubuntu (https://www.digitalocean.com/community/tutorials/how-to-upgrade-to-php-7-on-ubuntu-14-04)
3) Update PHP fpm run script in docker container to use an environment variable in order to:
a) Choose which PHP fpm to run
b) Update a socket symlink for nginx to find 
c) Run update-alternatives to alias php to the selected version 
If this env variable isn't defined, it should default to 5.6 
4) Projects are free to define the environment variable to select the desired version of PHP and upgrade at their own pace

The advantage of the Env variable method means that we can have different versions on different environments allowing us to slowly progress the upgrade to live; testing thoroughly at each step.

Some build steps in jenkins run a docker container whilst skipping starting of services; we need to consider how best to support this going forward. Options are:
1) specify exact php version required when running script (eg run php5.6 instead of php)
2) Replace php symlink with wrapper script which chooses version based on Env variables (would negate need for 3c above)
3) Fully boot the container before running scripts
4) Reuse a running container to run scripts using docker exec
5) Setup default php version in docker file (this is the least flexible and error prone)

Once this work was completed by devops Sirius and the other projects would then be able to schedule tasks into sprints to upgrade PHP compatibility to PHP 7.1 and switch over in their own time. Much of this work has already been completed for Sirius as part of the spike, so the bulk of the remaining work resides around regression testing.

Related JIRA issues:
* [SDV2-105	- Investigate PHP 7 upgrade for backend](https://opgtransform.atlassian.net/browse/SDV2-105)

