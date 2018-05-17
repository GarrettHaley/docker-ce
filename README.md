# Docker CE - With CentOS Developer User Tutorial

This repository hosts open source components of Docker CE products. The
`master` branch serves to unify the upstream components on a regular
basis. Long-lived release branches host the code that goes into a product
version for the lifetime of the product.

This repository is solely maintained by Docker, Inc.

## Issues

There are separate issue-tracking repos for the end user Docker CE
products specialized for a platform. Find your issue or file a new issue
for the platform you are using:

* https://github.com/docker/for-linux
* https://github.com/docker/for-mac
* https://github.com/docker/for-win
* https://github.com/docker/for-aws
* https://github.com/docker/for-azure

## Unifying upstream sources

The `master` branch is a combination of components adapted from
different upstream git repos into a unified directory structure using the
[moby-components](https://github.com/shykes/moby-extras/blob/master/cmd/moby-components)
tool.

You can view the upstream git repos in the
[components.conf](components.conf) file. Each component is isolated into
its own directory under the [components](components) directory.

The tool will import each component git history within the appropriate path.

For example, this shows a commit
is imported into the component `engine` from
[moby/moby@a27b4b8](https://github.com/moby/moby/commit/a27b4b8cb8e838d03a99b6d2b30f76bdaf2f9e5d)
into the `components/engine` directory.

```
commit 5c70746915d4589a692cbe50a43cf619ed0b7152
Author: Andrea Luzzardi <aluzzardi@gmail.com>
Date:   Sat Jan 19 00:13:39 2013

    Initial commit
    Upstream-commit: a27b4b8cb8e838d03a99b6d2b30f76bdaf2f9e5d
    Component: engine

 components/engine/container.go       | 203 ++++++++++++++++++++++++++++...
 components/engine/container_test.go  | 186 ++++++++++++++++++++++++++++...
 components/engine/docker.go          | 112 ++++++++++++++++++++++++++++...
 components/engine/docker_test.go     | 175 ++++++++++++++++++++++++++++...
 components/engine/filesystem.go      |  52 ++++++++++++++++++++++++++++...
 components/engine/filesystem_test.go |  35 +++++++++++++++++++++++++++
 components/engine/lxc_template.go    |  94 ++++++++++++++++++++++++++++...
 components/engine/state.go           |  48 ++++++++++++++++++++++++++++...
 components/engine/utils.go           | 115 ++++++++++++++++++++++++++++...
 components/engine/utils_test.go      | 126 ++++++++++++++++++++++++++++...
 10 files changed, 1146 insertions(+)
```

## Updates to `master` branch

Main development of new features should be directed towards the upstream
git repos. The `master` branch of this repo will periodically pull in new
changes from upstream to provide a point for integration.

## Branching for release

When a release is started for Docker CE, a new branch will be created
from `master`. Branch names will be `YY.MM` to represent the time-based
release version of the product, e.g. `17.06`.

## Adding fixes to release branch

Note: every commit of a fix should affect files only within one component
directory.

### Fix available upstream

A PR cherry-picking the necessary commits should be created against
the release branch. If the the cherry-pick cannot be applied cleanly,
the logic of the fix should be ported manually.

### No fix yet

First create the PR with the fix for the release branch. Once the fix has
been merged, be sure to port the fix to the respective upstream git repo.

## Release tags

There will be a git tag for each release candidate (RC) and general
availablilty (GA) release. The tag will only point to commits on release
branches.

# Getting Started with Docker and CentOS

There exist a number of tutorials for Linux, Max OSX, and Windows but the documentation for CentOS specifically is lacking. The following tutorial will help you get aquainted with DockerHub, networks, and the client/server relationship between two containers.

### Create a DockerHub Account
Head over to https://hub.docker.com and register an account. For the purposes of this tutorial the account I created is called "centostutorial" and wherever that string is used, replace it with the appropriate username.

Once you've got an account setup, create a public repository called "tutorial", which is the name we'll use for this guide.

### Configure Docker on your CentOS CLI
Once you've got a Docker account registered lets head over to your CentOS box and get docker installed. On the command line interface you'll need to run the following commands:

This command will install the yum-utils, device-mapper-persistent-data, and lvm2 packages. The `-y` flag indicates that we want `yum` to agree to and install any packages which ask the user `yes` or `no`.<br />
`sudo yum install -y yum-utils device-mapper-persistent-data lvm2`

Next, using the `yum-config-manager` we're going to add the docker community edition repo from Docker's website:<br />
`sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`

After adding the repo we want to install the docker community edition package:<br />
`sudo yum install -y docker-ce`

Then, using the system control service start the docker process:<br />
`sudo systemctl start docker`

And enable docker to run by default<br />
`sudo systemctl enable docker`

And finally, add your username to the docker group <br />
`sudo usermod -aG docker <your centos username>`

Reboot your machine and test that docker has successfully installed with the following:<br />
`docker run hello-world`

### Get Familiar with Alpine

### Create the Server (Using Dockerfiles!)

### Create the Client (Using Dockerfiles!)

### Clear your Workspace

### Configure the network

### Run your containers
