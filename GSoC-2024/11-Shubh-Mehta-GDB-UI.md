# GDB-UI

## Project Abstract
---
The issue at hand is to address the usability and accessibility limitations of GDB by developing a user interface (UI) using React. This UI leverages the GDB Python API to create a graphical dashboard that simplifies and streamlines the debugging process. The goal is to provide a more intuitive and visually interactive interface, enhancing the overall debugging experience for developers.

This improved UI makes it easier to execute commands, examine program state, and control operations within GDB. It includes features such as starting and stopping program execution, inspecting variables, registers, and memory, and offering a log or console view for command output and error messages. These enhancements aim to make the debugging process more efficient and user-friendly.

---

### [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2024/projects/WrwfJdvR)

### [GSoC Project Proposal](https://drive.google.com/file/d/16OimPeZDhqaTgr31DqeQesuijAhKWdHp/view)

### [GitHub Organization Repo](https://github.com/c2siorg/GDB-UI)

### [GitHub Personal Repo](https://github.com/shubh942/GDB-UI)

### [Commits during GSoC 2024](https://github.com/c2siorg/GDB-UI/commits/main/?author=Shubh942)

### [Project Demo Video]()

### [Project Wiki](https://github.com/c2siorg/GDB-UI/blob/main/README.md)

### [GSoC Blog](https://medium.com/@shubhmehta942)

## Work Summary

---

| **Description** | **PR** | **Merged** |  
|-----------------------------------|----|---------|
| Created the Flask App and Test File | [#4](https://github.com/c2siorg/GDB-UI/pull/4) | ✅ |
| Added More GDB APIs and GitHub Templates | [#7](https://github.com/c2siorg/GDB-UI/pull/7) | ✅ |
| Initialized the Frontend and Added Some Components | [#9](https://github.com/c2siorg/GDB-UI/pull/9) | ✅ |
| Added GDB Components with Functionality of Uploading File to Server | [#12](https://github.com/c2siorg/GDB-UI/pull/12) | ✅ |
| Dockerized the Project | [#15](https://github.com/c2siorg/GDB-UI/pull/15) | ✅ |
| Added More Components in Frontend | [#17](https://github.com/c2siorg/GDB-UI/pull/17) | ✅ |
| Added .yml File for Webapp to Run Tests on PR | [#19](https://github.com/c2siorg/GDB-UI/pull/19) | ✅ |
| Added Feature of Toggling Dark and Light Mode | [#21](https://github.com/c2siorg/GDB-UI/pull/21) | ✅ |
| Added Context API in Webapp for State Management | [#23](https://github.com/c2siorg/GDB-UI/pull/23) | ✅ |
| Connected Adding Breakpoints with Server and Added Toast Feature to Inform User | [#26](https://github.com/c2siorg/GDB-UI/pull/26) | ✅ |
| Enhanced Terminal and Added Monaco Editor to Mainscreen | [#30](https://github.com/c2siorg/GDB-UI/pull/30) | ✅ |
| Modified Readme.md File and Connected Access Button with Server | [#33](https://github.com/c2siorg/GDB-UI/pull/33) | ✅ |

---

## What Covered

---

The GDB-UI project has undergone substantial development, focusing on improving its functionality, usability, and deployment from scratch. Here's a summary of the key implementations:

1. **Project Initialization**: The project began with the creation of a Flask backend and initial setup of the frontend, including the development of basic components and integration of GDB functionalities.

2. **API Development**: Multiple GDB APIs were implemented, allowing for key debugging operations like starting/stopping programs, inspecting variables, and handling breakpoints.

3. **Frontend Development**: The frontend was progressively enhanced with additional components, integrating features like file upload to the server, breakpoint management, and a robust UI for interacting with GDB.

4. **State Management and User Experience**: The Context API was integrated to manage state across the application, along with features like toggling between dark and light modes to improve user experience.

5. **Project Containerization**: The project was dockerized, enabling consistent development environments and simplifying deployment with Docker and Docker Compose.

6. **CI/CD Integration**: A `.yml` file was added to automate testing on every pull request, ensuring code quality and smooth integration of new features.

7. **Terminal and Editor Enhancements**: The terminal was enhanced and the Monaco editor was integrated into the mainscreen, providing a more interactive and user-friendly interface for developers.

---

# What left

---

- **User Authentication**: Implement and integrate robust user login and signup functionality to ensure secure and seamless access to the platform.

- **Code Storage for Debugging**: Store user-submitted code in the file system. This will facilitate debugging, especially when dealing with large and complex codebases, enabling easier tracking and reproduction of issues.


---
