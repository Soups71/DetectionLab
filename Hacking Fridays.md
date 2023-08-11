## Detection Labs Showcase

### Introduction:
Creating a home lab for exploitation and detection practice can be hard. I will demonstrate how to create a home lab using the [Detection Labs](https://detectionlab.network/introduction/) Project. This project has a lot of good things built in, but sometimes it doesn't like to play nice.

The project is no longer being maintained, so I created a fork of the project in attempt to fix bugs I ran into along the way. Hopefully the changes work for others as well.

Link to fork: https://github.com/Soups71/DetectionLab


### Plan:
* What is Detection Labs
* What is it used for
* How does it work
* How to build the network
* "I've built the lab, now what?"

### What is Detection Labs?

[Link to the original project](https://detectionlab.network/introduction/)

"DetectionLab is a repository containing a variety of Packer, Vagrant, Powershell, Ansible, and Terraform scripts that allow you to automate the process of bringing an ActiveDirectory environment online complete with logging and security tooling using a variety of different platforms."

What does this mean in normal people language?

It ultimately build us our own personal AD environment. It also has some sick tools preloaded within the network.  I do have to admit that it's not perfect and has it's challenges.

![[Pasted image 20230810204335.png]]

### What is it used for?

When we are able to quickly build and destroy our network, it is a lot less daunting to explore running attacks within an AD network.

In addition, the built-in detection tools allow us to see what artifacts our attacks leave behind after they are executed. This is great as it allows for us to begin the long journey of being able to correlate what we might see as defenders to the real world attacks.

### How does it work?

This project uses a lot of automation to build the network. The project can be deployed on a number of different resources. For today, I am only going to be focusing on deploying the lab on VirtualBox. 

In order to deploy the 4 machines within the network, the project utilizes vagrant to build and configure the boxes.

What is vagrant?

"Vagrant is an open-source software product for building and maintaining portable virtual software development environments; e.g., for VirtualBox, KVM, Hyper-V, Docker containers, VMware, Parallels, and AWS" (Google)

Basically, this just means that it can deploy the boxes using a configuration file and minimizes the work needed to be conducted by us.

### How to build the network

There are installation instructions that can be found on the github repo or on the detection lab web page. However, I have provided the boiled down commands below:

```bash
sudo apt install vagrant
vagrant plugin install vagrant-vmware-desktop
git clone https://github.com/Soups71/DetectionLab.git
cd DetectionLab/Vagrant
./prepare.sh

vagrant up --provider=virtualbox
```

This will take a while to build. If it happens to fail in the middle of building a box you can use the following command to build the boxes individually.

```bash
vagrant up --provision logger
vagrant up --provision dc
vagrant up --provision wef
vagrant up --provision win10

```

### "I've built the lab, now what?"

As I've mentioned throughout this write-up, there are a lot of use cases for this network.

List of things you can do on the network:
* Practice your windows automation and deployment of tools using powershell across the domain.
* Practice the cool Windows attacks you learn from attending Hacking Fridays each week
* See what artifacts are left behind by certain tools that you might be using.


### Conclusion

This has been a lot of fun learning about this project and getting antiquated with it. I do have to give a huge shout out to the team who built the tool and maintained it for about 6 years. The original link to the project can be found [here](https://github.com/clong/DetectionLab). 

With the fact that the project is no longer being actively maintained, I am going to do my best to continue working on maintaining a working version of the tool as best as I can with the hope that others will get benefit of having the ability to quickly build and destroy their own personal AD.