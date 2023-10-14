## Install Ansible

During the weekly meeting, the Nautilus DevOps team discussed about the automation and configuration management solutions that they want to implement. While considering several options, the team has decided to go with Ansible for now due to its simple setup and minimal pre-requisites. The team wanted to start testing using Ansible, so they have decided to use jump host as an Ansible controller to test different kind of tasks on rest of the servers.



Install <span style='color:cyan'>**ansible**</span> version <span style='color:cyan'>**4.9.0**</span> on <span style='color:cyan'>**Jump**</span> host using <span style='color:cyan'>**pip3**</span> only. Make sure Ansible binary is available <span style='color:cyan'>**globally**</span> on this system, i.e <span style='color:cyan'>**all users**</span> on this system are able to run Ansible commands.

### Solution

1. Run 
```
sudo pip3 install "ansible==4.9.0"
```
