# RayZed

## Student Info

- Name: Kushal Shah

- Email: shahkushal0602@gmail.com

- GitHub: [Kushal-Ajay-Shah](https://github.com/Kushal-Ajay-Shah)

- Linkedin: [Kushal Shah](https://www.linkedin.com/in/kushalajayshah/)

- Medium: [@KushalAjayShah](https://medium.com/@KushalAjayShah)

## Project Abstract

Finding out web vulnerabilities for specific targets(URLs) is a critical task. For this OWASP ZAP-ZED helps by using its various scan functionalities like active, passive and spider scan. These scans scrutinize the target URL for different standard vulnerabilities and thus is an extensive process. The target(URLs) could be distributed among Ray cluster nodes deployed on the cloud-native platform where ZAP is running as a daemon. This architecture scales the process of finding vulnerabilities for targets. The purpose of this project is to create a parallelized tool that could fetch vulnerabilities of different websites in an efficient way such that the process could be scaled and automated for cybersecurity research. This project has the setup for ZAP, Ray and Terraform as infrastructure as code for GCP ready and tasks for setup automated using Ansible.
Project Architecture RayZed tool would have the following main components:

1. Terraform
2. Cloud-native platforms(GCP)
3. VMs of cloud-native platforms configured for ssh, firewall and local execution(ZAP).
4. Ray manages the parallelized architecture of the head and workers.

   Distributed Architecture
   ![Architecture](https://miro.medium.com/v2/resize:fit:1380/1*wP1pLLsvVq8oQv63XFFo7g.png)

## GSoC Project Page

- [GSoC 2023 with SCoRe Lab](https://summerofcode.withgoogle.com/programs/2023/projects/1IN7Sna1)

## GSoC Project Proposal

- [RayZed project proposal](https://docs.google.com/document/d/1EC05X-8w_JWoWQ0d4bOkT5O1VrrQjj_AvPEd9R9hLZg/edit?usp=sharing)

## GitHub Organization Repo

- [https://github.com/c2siorg/RayZed](https://github.com/c2siorg/RayZed)

## GitHub Personal Repo

- [https://github.com/Kushal-Ajay-Shah/RayZed/](https://github.com/Kushal-Ajay-Shah/RayZed/)

## Commits during GSoC 2023

- [https://github.com/c2siorg/RayZed/commits/main](https://github.com/c2siorg/RayZed/commits/main)

## Project Demo Video

- [Demo Video & Explanation](https://drive.google.com/file/d/1qeda8B_KDyGGTONeVsP30S2zMWHyZ6JP/view?usp=drive_link)

## Project Wiki

- [RayZed README](https://github.com/c2siorg/RayZed#readme)

## GSoC Blog(s)

- [Medium Page @KushalAjayShah](https://medium.com/@KushalAjayShah)

## Work Summary

I majorly focused on the optimizations that can be done such that huge sites’ spider and active scans could be done in the least amount of time using Zap-Zed (application level) optimizations as well as distributed parallel ray optimizations. Handled the distributed computing on GCP using Ray actors. Smoothened the process of transfer of session files in order to optimize the time required for web vulnerabiltity scanning. Implemented the novel approach of having multiple Zap daemons (application level) as well as VMs (Ray level) optimized distributed parallel computing. Documented all the techniques of optimization.

## What Covered

1. [PR1](https://github.com/c2siorg/RayZed/pull/2)

- Added documentation for the project setup.

- Handled blockers and explained solutions for setup

2. [PR2](https://github.com/c2siorg/RayZed/pull/5)

- Tested different architecture to optimize the Zed

- Specifically focused on application level Zap optimization

- Properly documentated all the techniques of application level optimization

3. [PR3](https://github.com/c2siorg/RayZed/pull/6)

- Integrated the Ray and Zap code.

- Focused on distributing the session files among the VMs

- Finalized the code architecture of distributed computing having tiers of optimization(Application(Daemon directory level) and VM level)

- Handled the distributed computing using Ray (By help of Ray actors)

4. [PR4](https://github.com/c2siorg/RayZed/pull/7)

- Fine tuned SCP (i.e. transfer of session files between VMs)

- Handled small bugs while copying of session files.

- Final enhancemennts

## What left

- Adding Burp suite compatibility
