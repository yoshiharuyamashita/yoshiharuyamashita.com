+++
date = "2016-01-31T17:42:03Z"
description = ""
draft = false
tags = ["hugo", "wercker"]
title = "Automated Deployments using Wercker"
topics = ["Techy Stuff"]

+++

## Hugo + GitHub + Wercker

This website is hosted from my GitHub repository. Every time I commit changes to that repository, the website is built and deployed automatically with [Wercker](//wercker.com/). This is great as it means I can concentrate on writing!

If you want to achieve the same workflow, you should follow this excellent [tutorial](//gohugo.io/tutorials/automated-deployments/) from the official Hugo site.

## But Something Went Wrong

Everything was working as expected for a few weeks until one day I recevied a deploy error from Wercker. After that all my commits ended up with the same error, which meant that I couldn't update my website.

The error was as follows: 

```
export WERCKER_STEP_ROOT="/pipeline/install-packages-57eed074-cb0b-4e08-97a0-32cf7ef1f7d3"
export WERCKER_STEP_ID="install-packages-57eed074-cb0b-4e08-97a0-32cf7ef1f7d3"
export WERCKER_STEP_OWNER="wercker"
export WERCKER_STEP_NAME="install-packages"
export WERCKER_REPORT_NUMBERS_FILE="/report/install-packages-57eed074-cb0b-4e08-97a0-32cf7ef1f7d3/numbers.ini"
export WERCKER_REPORT_MESSAGE_FILE="/report/install-packages-57eed074-cb0b-4e08-97a0-32cf7ef1f7d3/message.txt"
export WERCKER_REPORT_ARTIFACTS_DIR="/report/install-packages-57eed074-cb0b-4e08-97a0-32cf7ef1f7d3/artifacts"
export WERCKER_INSTALL_PACKAGES_PACKAGES="git ssh-client"
source "/pipeline/install-packages-57eed074-cb0b-4e08-97a0-32cf7ef1f7d3/run.sh" < /dev/null
Reading package lists...
Building dependency tree...
Some packages could not be installed. This may mean that you have
requested an impossible situation or if you are using the unstable
distribution that some required packages have not yet been created
or been moved out of Incoming.
The following information may help to resolve the situation:

The following packages have unmet dependencies:
 git : Depends: liberror-perl but it is not going to be installed
E: Unable to correct problems, you have held broken packages.
```

My wercker.yml settings:

```
box: debian
build:
  steps:
    - arjen/hugo-build:
        version: "0.15"
        theme: blackburn
        flags: --buildDrafts=true
deploy:
  steps:
    - install-packages:
        packages: git ssh-client
    - lukevivier/gh-pages@0.2.1:
        token: $GIT_TOKEN
        domain: yoshiharuyamashita.com
        basedir: public
```

Googling for a solution, I found out the error was something to do with bad package dependencies but being a Wercker newbie I was still unsure how to fix it.

## Solution
 
 I was able to fix this problem by clearing **$WERCKER_CACHE_DIR**. In Wercker it's under **Application Settings** -> **Options** as shown below:
 
{{% fluid_img "/img/post/wercker-clear-cache.png" %}}

I hope this helps!