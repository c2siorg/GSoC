# Survey6
## Student Info
* Name: Dhruvi Doshi
* Email: drdoshi29@gmail.com
* GitHub: [dhruvi29](https://github.com/dhruvi29)
* Linkedin: [Dhruvi Doshi](https://www.linkedin.com/in/dhruvi-doshi-5007801a0/)
* Medium: [@dhruvidoshi](https://medium.com/@dhruvidoshi)
## Project Abstract
Ipv6 is the internet's future, and it necessitated a more scalable survey tool to comprehend how routing and DNS function. The purpose of this project is to create an IPv6 listener that will passively collect IPv6 traffic data as a passive data collection tool for cyber security research.
Survey6 is a geo-distributed grid application with C&C Server as its center and the probes as the packet collection application for intercepting IPv6 traffic on linux.
![](https://github-production-user-asset-6210df.s3.amazonaws.com/61967013/263470237-21e180e0-0bb3-4248-a7a4-9af0ad1895cb.png)


## GSoC Project Page
* [GSoC 2023 with SCoRe Lab](https://summerofcode.withgoogle.com/programs/2023/projects/LdlUOWJd)

## GSoC Project Proposal
* [Survey6 project proposal](https://docs.google.com/document/d/1etx4P6Io8ECbHZ4X_rXQtVguH3KFq3HxedVkyK83kEI/edit?usp=sharing)


## GitHub Organization Repo
* [c2siorg/survey6](https://github.com/c2siorg/survey6)

## GitHub Personal Repo
* [dhruvi29/survey6](https://github.com/dhruvi29/survey6)

## Commits during GSoC 2023
* [c2siorg/survey6/commits/main?author=dhruvi29](https://github.com/c2siorg/survey6/commits/main?author=dhruvi29)

## Project Demo Video
* [Application Demo](https://drive.google.com/file/d/1h5fSkFO_X-V7j1uW4reVOjq3vejkE89J/view?usp=sharing)

## Project Wiki
* [Survey6 README](https://github.com/c2siorg/survey6#readme)

## GSoC Blog(s)
* [Survey6 — Sprint2 @ GSOC’23](https://medium.com/@dhruvidoshi/survey6-sprint2-gsoc23-b5f5ef188a1d)

## Work Summary
In the second sprint of the development of the survey6, we have implemented a lot of features for the probe and some for the data aggregator. Probe is ready to be a debian package now. All the three components of the survey6 are in a MVP stage and can be used in integration to one another. 

## What Covered
[All PRs here](https://github.com/c2siorg/survey6/pulls?q=is%3Apr+author%3Adhruvi29+is%3Aclosed)
Some of the major PRs are as follows: 
1. [PR#31 - continuous data collection and rsync transfer ](https://github.com/c2siorg/survey6/pull/31)
    - a `clientName/capture` folder is created in the server where the captured files will be copied
    - Rsync is used to transfer the files
    - The client needs to copy its keys in the server before starting the script
    - `/capture` is copied into `/clientName/capture` folder
2. [PR#31 - Connection Disconnection](https://github.com/c2siorg/survey6/pull/33)
    - The uid received upon connection is stored in `uid.id`. This uid is used while sending disconnection request. 
    - The grpc server ip should be editable and hence made a part of the environment variables with this PR 
3. [PR#38 - Heartbeats Sending and Receiving](https://github.com/c2siorg/survey6/pull/38)
    - HeartbeatRequest protobuf definition to include uid as a means to identify the probe, hence, the updating of python gRPC client and server interface codes
    - Sending Heartbeat every 3s by the client with the current timestamp
    - Implementing Heartbeat end point of the grpc 
    - Updating corresponding last active time of the client in the database of the server
4. [PR#41 - Probe CLI](https://github.com/c2siorg/survey6/pull/41)
    Probe works as a unit. Only a bash file will do it all for us.
    > Commands:
    `probe start`
    - Sends a connection request
    - Starts capturing script
    - Starts Rsync transfer script
    - Starting heartbeat mechanism
    > `probe stop`
    - Killing the running scripts
    - Sending disconnection request
5. [PR#43 - Packaging of the probe](https://github.com/c2siorg/survey6/pull/43)
6. [PR#46 - Archiving files in data aggregator](https://github.com/c2siorg/survey6/pull/46)
    - Changing the backup folder structure at the probe to include the host to have a different directory for itself.
    - Upon data transfer from probe to server, delete files from probe. This is done to ensure that these files aren't backed up again. Since the data aggregator would process the data files into pcap archives, files will be deleted from the main backup folder that is open to the client. hence to prevent re-sending we delete it from the probe, this frees memory at the probe to.
    - Scripts for hourly and month archive
    - Cron job for archiving

7. [PR#48 - Heartbeat eventlog](https://github.com/c2siorg/survey6/pull/48)
    - Created a new Table in the C&C Server called `EventLog` to store all the heartbeat events of all the probe.
    - Schema of `EventLog` is (hostId, hostName, heartbeatTime)
8. [PR#50 - Probe Metadata](https://github.com/c2siorg/survey6/pull/50)
    - Generate only one metadata file with name `**uid.json**`
    - Includes UID, sysname, number_of_packets_captured_per_pcap, total_memory, cpu_count, among others


## What left
1. Sending password pf the data aggregator from server to the probe on regisration
2. Configurable parameters

