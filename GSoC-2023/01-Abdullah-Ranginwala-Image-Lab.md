# ImageLab

# Project Abstract
ImageLab is a standalone tool which supports anyone to get started with image processing related concepts and techniques in an interactive and intuitive manner. The users can build image processing pipelines with the help of blocks and apply the operators to different images.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2023/projects/0BLb9KSk)

## [GSoC Project Proposal](https://drive.google.com/file/d/1OJZck1izX3LJoyBM0o3zetZ3rNkxekGj/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/scorelab/imagelab)

## [GitHub Personal Repo](https://github.com/abdullahranginwala/imagelab)

## [Commits during GSoC 2023](https://github.com/scorelab/imagelab/commits?author=abdullahranginwala)

## [Project Demo Video](https://drive.google.com/file/d/17MxMb4F14qH8NXsbzIE6TxCVYVAGdDXE/view?usp=sharing)

## [Project Wiki](https://github.com/scorelab/imagelab/blob/master/README.md)

## [GSoC Blog](https://medium.com/@abdullahranginwala28/week-1-gsoc-2023-imagelab-project-updates-cf4f527b5f28)

# Work Summary
I undertook a comprehensive project aimed at modernizing and enhancing the Imagelab application. This included a complete overhaul of the user interface, migrating the backend to the node.js process, establishment of a robust testing framework, and documentation enhancement. My work began with crafting a design mockup that set the stage for the project's design language. Subsequently, I transitioned the front-end to an Electron-React architecture, introducing features like workspace saving/loading and an improved image viewer. Additionally, I meticulously integrated the backend into the Electron main process using IPC, ensuring efficient communication and processing. Rigorous unit testing, powered by thorough mock implementations for OpenCV.js functions, validated the image processing operators' functionality. To further enhance usability, I expanded the documentation, making it more comprehensive and accessible. Overall, my contributions aimed to create a more efficient, user-friendly, and reliable usage experience for ImageLab.

# What Covered
## Front-End Migration and Enhancement
- **UI/UX Design Mockup**: I initiated the project by creating a meticulous design mockup that laid the foundation for the improved user experience. This design evolved over the course of the project but served as a backbone for the UI/UX overhaul 

<img width="839" alt="Screenshot 2023-08-19 at 12 18 48 PM" src="https://github.com/c2siorg/GSoC/assets/19731056/558ad79a-9648-47a2-b880-f0b35438d942">

- **Electron-React Architecture**: The front-end migration involved transitioning the application to an Electron-based React architecture. This transition enhanced the application's efficiency and responsiveness.

- **Integration of React Components**: I successfully integrated new and enhanced features into the application:
  - React-blocky: Using react-blockly, a wrapper for the Blockly visual editor, I created a UI to build the image processing pipelines.
  - Save and Load Workspace: Implemented a seamless mechanism for users to save and load their workspaces, providing convenience and flexibility.
  - Image Viewer Improvement: Overhauled the image viewer with new pinch and pan capabilities, optimizing the user's interaction with images.
  - Dual Image Viewers: Introduced an intuitive user interface with two image viewers—one for the original image and another for the processed image. This real-time visual feedback enhances the editing experience.
    
<img width="1438" alt="Screenshot 2023-08-19 at 1 09 25 PM" src="https://github.com/c2siorg/GSoC/assets/19731056/af7bd24b-e6eb-4474-864c-cf081f552c9d">

### PRs
- [#151](https://github.com/scorelab/imagelab/pull/151)
- [#153](https://github.com/scorelab/imagelab/pull/153)
- [#155](https://github.com/scorelab/imagelab/pull/155)
- [#156](https://github.com/scorelab/imagelab/pull/156)
- [#159](https://github.com/scorelab/imagelab/pull/159)

## Backend Migration and Integration
- **Node.js Process Integration**: I migrated the backend processing to the Electron main (Node.js) process, enabling efficient utilization of system resources.
- **IPC (Inter-Process Communication)**: To address the absence of direct access to DOM elements in the Node.js process, I meticulously developed logic to convert images to base64 format. This facilitated seamless communication between the React (renderer) and Node.js (main) processes.

### PRs
- [#154](https://github.com/scorelab/imagelab/pull/154)

## Unit Testing & Documentation
- **Unit Testing Suite Setup**: I established a robust unit testing framework that enabled rigorous testing of the application's functionalities.
- **OpenCV.js Function Mocks**: I created comprehensive mock implementations for OpenCV.js functions, ensuring accurate and reliable testing without external dependencies.
- **Operator-Specific Unit Tests**: I designed and executed unit tests for each image processing operator, validating their functionalities and ensuring consistent performance. Thus, also contributing to a better development and contributing experience.

### PRs
- [#160](https://github.com/scorelab/imagelab/pull/160)
- [#161](https://github.com/scorelab/imagelab/pull/161)
- [#162](https://github.com/scorelab/imagelab/pull/162)
- [#163](https://github.com/scorelab/imagelab/pull/163)
- [#165](https://github.com/scorelab/imagelab/pull/165)
- [#166](https://github.com/scorelab/imagelab/pull/166)
- [#167](https://github.com/scorelab/imagelab/pull/167)
- [#168](https://github.com/scorelab/imagelab/pull/168)

# What left
- Over the course of the project, more image processing operators were added to the Electron project. The new image operators have to be migrated to the React project
- Add dark mode to the React project
  
# References
- [React.js documentation](https://reactjs.org/docs/getting-started.html)
- [react-blockly documentation](https://www.npmjs.com/package/react-blockly?activeTab=readme)
- [OpenCV.js documentation](https://docs.opencv.org/3.4/d5/d10/tutorial_js_root.html)
- [Jest documentation](https://jestjs.io/docs/mock-functions)
- [Electron documentation](https://www.electronjs.org/docs/latest/tutorial/process-model)
