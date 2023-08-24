# Project Name
SCoRe Lab - Scan8

## Student Info

- Name: Shelly Suthar

- Email: shellysuthar@gmail.com

- GitHub: [Shelly011s](https://github.com/Shelly011s)

- Linkedin: [Shelly Suthar](https://www.linkedin.com/in/shelly-suthar-a46920216/)

# Project Abstract
Scan8 is a distributed scanning system for detecting trojans, viruses, malware, and other malicious threats embedded in files. The system will allow one to submit a list of URLs or files and get the scan results in return.
This project's user interface is out-of-date and does not handle real-time data changes from the database at the moment. By the integration of websockets and an updated, user-friendly user interface, this project seeks to address the issue of real-time data orchestration.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2023/projects/KK8mBdNH)

## [GSoC Project Proposal](https://docs.google.com/document/d/1F5bvEHx6sN1VgrFFUKMoqdQV10FLDswfVM7eKjF82sM/edit?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/Scan8)

## [GitHub Personal Repo](https://github.com/Shelly011s/Scan8)

## [Commits during GSoC 2023](https://github.com/c2siorg/Scan8/pulls?q=is%3Apr+author%3AShelly011s+)

## [Project Demo Video](https://drive.google.com/file/d/1pRM5R7qGz_1vuvCmu0ebMO8z7YNhdGsW/view?usp=sharing)

## [GSoC Blog](https://medium.com/@shellysuthar/gsoc23-journey-so-far-with-score-labs-984d3d52d116)

# Work Summary

PR [#113](https://github.com/c2siorg/Scan8/pull/113)

- Redis pub/sub queue is initialized to allow multiple dashboard.py clients to subscribe to a Redis channel and receive updates from the scan.py process.
- The useless imports were removed to improve the performance of the application.
- The SocketIO import was added to enable real-time communication between the frontend and the backend.

PR [#117](https://github.com/c2siorg/Scan8/pull/117)

- Initialized frontend using reactJS
- Added a navbar and modal to upload files or folder
- Added a reusable scan component for various scan progress states.
- Initialized a websocket connection on the frontend to realize the objective of real time data orchestration.

PR [#121](https://github.com/c2siorg/Scan8/pull/121)
- Fixed minor issues related to sockets to make frontend and backend real time compliant.

# What Covered
- Refactored the current frontend using ReactJS
- Integrated websockets with flask server to implement real time data orchestration
- Updated current Dashboard UI
- Modified current new scan page 

# What left
- Using docker to containerize the application for easy setup of the development enviroment.
