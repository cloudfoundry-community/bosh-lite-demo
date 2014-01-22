# Learn BOSH with a bosh-lite demo

This project includes an easy-to-run command that does everything to build [bosh-lite](https://github.com/cloudfoundry/bosh-lite) on your local machine, and deploy an example system. The "killer app" system for BOSH to deploy [Cloud Foundry](http://www.cloudfoundry.com/).

Sections:

  * [FAQ](#faq)
* [Quick Start](#quick-start)
* [Requirements](#requirements)
* [Concepts](#concepts), while you wait
* [Quick Shutdown](#quick-shutdown)

## FAQ

**What is BOSH?** An open-source platform for deploying and managing systems on your favorite infrastructures: vSphere, OpenStack and AWS.

**Can I try it out on my laptop without AWS/OpenStack/vSphere?** Yes. For dev/test/demo of BOSH, we have [bosh-lite](https://github.com/cloudfoundry/bosh-lite) - a version of BOSH that runs on your local machine that manages Linux Containers, rather than virtual machines on your favorite infrastructure.

**Can I use bosh-lite on my Mac?** Yes, bosh-lite is run within a Linux virtual machine via Vagrant/Virtualbox; and not directly run within your OS X machine.

**Can I use bosh-lite on my Windows machine?** Ah, no, not afaik. Even though Vagrant/Virtualbox can run on Windows; it is the current BOSH CLI that may not work on a Windows machine.

**What is this project?** The purpose of this project is to give you a Quick Start to running bosh-lite on your local machine, and then introducing you to the concepts of BOSH. Everything you can do on bosh-lite, every BOSH release you can deploy, can then be used on your favourite infrastructure.

**Explain it again. What is BOSH and what is bosh-lite?** bosh-lite runs within Vagrant and when it provisions "vms" (aka virtual machines/servers/machines) it is actually provisioning Linux containers (via the Warden project, similar to the Docker project). BOSH is the production version and is configured to provision "vms" on a single target infrastructure.

Each VM is bound to the infrastructure's networking. Each VM can have an optional "persistent disk" attached (for example, an EBS volume on AWS). Each VM then runs one or more processes. All the processes across all the VMs compose together as a "system". Systems are used to run your company.

BOSH deploys these systems (called "deployments"), and can upgrade them, scale them, and heal them.

bosh-lite performs all the same functions except entirely within your laptop, and without the concept of "persistent disks".

**What infrastructures are currently supported by BOSH?** BOSH can currently control AWS (EC2 and VPC networking), OpenStack (Nova & Neutron networking), and vSphere. There are also variations of BOSH for: vCloud, Google Compute, Cloud Stack and Tier 3/Century Link. There is major work going on in the BOSH project to make it much easier to describe support for different infrastructures.

**Who is using BOSH?** Currently, BOSH is primarily being used to deploy and run small, medium and large private Cloud Foundry deployments; as well as to run Pivotal's public Cloud Foundry: [run.pivotal.io](https://run.pivotal.io).

**What can I deploy with BOSH?** You can deploy any system, assuming your system is a collection processes to be run on virtual machines. Either you write new BOSH releases for your own software/systems; or you use pre-existing BOSH releases from the community. Try Googling for "boshrelease" or visit [https://github.com/cloudfoundry-community](https://github.com/cloudfoundry-community)

There are a number of open source BOSH release projects for running open source systems ([redis](https://github.com/cloudfoundry-community/redis-boshrelease), [etcd](https://github.com/cloudfoundry-community/etcd-boshrelease), [jenkins](https://github.com/cloudfoundry-community/jenkins-boshrelease), [gitlab](https://github.com/drnic/gitlab-boshrelease))

## Quick Start

During this script, approximately 2G of content is downloaded (Vagrant box, Cloud Foundry source & dependencies, Warden image/stemcell). Also, the first time you run the installer (it can be re-run over and over to upgrade and rebuild), it will compile the source packages of Cloud Foundry one time. If you re-run the script below, these assets will not be downloaded again.

```
curl https://raw2.github.com/cloudfoundry-community/bosh-lite-demo/master/binscripts/bosh-lite-cloudfoundry-demo | bash
```

You may you want to [read through this script](https://github.com/cloudfoundry-community/bosh-lite-demo/blob/master/binscripts/bosh-lite-cloudfoundry-demo) first.

If the script ever fails, re-run it and it will skip over any steps that were already successfully.

## Requirements

* Ruby 1.9.3
* Vagrant/Virtualbox 1.4+
* wget
* spiff
* gcf

The installer script will test for the existence of these requirements.

## Concepts

The Quick Start will take a while. Or a long time if you have slow internet, downloading the 2G of bits and bobs.


## Quick Shutdown & Cleanup

```
cd ~/bosh-lite-tutorial/bosh-lite
vagrant destroy
```

If you want to boot bosh-lite back up, and re-deploy Cloud Foundry, then run the `curl | bash` script above.

If you never want to boot bosh-lite ever again, then delete the root folder of the tutorial:

```
rm -rf ~/bosh-lite-tutorial
```
