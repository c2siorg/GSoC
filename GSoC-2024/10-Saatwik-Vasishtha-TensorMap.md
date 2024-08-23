# Project Name
<div style="text-align: center;">
<img src="https://github.com/user-attachments/assets/64cec3f6-2428-41e8-942b-563d62dcc6c2" width=500 height=100 alt="TensorMap Logo">
</div>  


Tensormap - [Saatwik Vasishtha](https://github.com/Teak-Rosewood)

## Project Abstract
TensorMap will be a web application that will allow the users to create machine learning algorithms visually. TensorMap will support reverse engineering of the visual layout to a Tensorflow implementation in preferred languages.

This year's goal aims to enhance the TensorMap web application by addressing technical challenges and introducing functionalities to improve usability and efficiency. Key issues, such as dependency management and server-side complexity, will be tackled by Dockerizing the backend for easier deployment. 
### [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2024/projects/rKXxuFox)

### [GSoC Project Proposal](https://drive.google.com/file/d/1GKbFU1xzVIGEWuGLg5_1l-QqGG6t3nHM/view?usp=sharing)

### [Organization Repository](https://github.com/c2siorg/tensormap)

### [Personal Fork](https://github.com/Teak-Rosewood/tensormap)

### [Commits during GSoC 2024](https://github.com/c2siorg/tensormap/commits/master/?author=Teak-Rosewood&since=2024-05-01&until=2024-09-01)

### [Project Demo Video](https://www.youtube.com/watch?v=3_kukRYsz2U&t=2s)

### [Project Wiki](https://github.com/scorelab/TensorMap/wiki)

### [GSoC Blog](https://medium.com/@saatwik.vasishtha)

# Work Summary

| **Description** | **Issue** | **PR** | **Merged** |  
|------------ |-------|----|---------|
| Dockerization | [#17](https://github.com/c2siorg/tensormap/issues/17) | [#19](https://github.com/c2siorg/tensormap/pull/19) | ✅ |
| Client-end Compilation and Dependency Issues | [#6](https://github.com/c2siorg/tensormap/issues/6) [#18](https://github.com/c2siorg/tensormap/issues/18) | [#21](https://github.com/c2siorg/tensormap/pull/21) | ✅ |
| Progress Bar & Linear Regression Model Integration | [#24](https://github.com/c2siorg/tensormap/issues/24) [#25](https://github.com/c2siorg/tensormap/issues/25) [#26](https://github.com/c2siorg/tensormap/issues/26) [#28](https://github.com/c2siorg/tensormap/issues/28) | [#27](https://github.com/c2siorg/tensormap/pull/27) | ✅ |
| Dataset Preprocessing | [#29](https://github.com/c2siorg/tensormap/issues/29) | [#30](https://github.com/c2siorg/tensormap/pull/30) | ✅ |
| Delete Datasets Feature | [#36](https://github.com/c2siorg/tensormap/issues/36) | [#37](https://github.com/c2siorg/tensormap/pull/37) | ✅ |
| Dynamic Inputs and Conv Layer | [#38](https://github.com/c2siorg/tensormap/issues/38) [#39](https://github.com/c2siorg/tensormap/issues/39) | [#40](https://github.com/c2siorg/tensormap/pull/40) | ✅ |
| Prettier Linting | [#11](https://github.com/c2siorg/tensormap/issues/11) | [#42](https://github.com/c2siorg/tensormap/pull/42) | ✅ |
| Vite Testing & NavBar Change | [#49](https://github.com/c2siorg/tensormap/issues/49) [#51](https://github.com/c2siorg/tensormap/issues/51) | [#54](https://github.com/c2siorg/tensormap/pull/54) | ✅ |
| Prettier and Husky Integration | [#55](https://github.com/c2siorg/tensormap/issues/55) | [#56](https://github.com/c2siorg/tensormap/pull/56) | ✅ |
| Cleaning up server | [#57](https://github.com/c2siorg/tensormap/issues/57) | [#58](https://github.com/c2siorg/tensormap/pull/58) | ✅ |
| PostgreSQL Migration | [#59](https://github.com/c2siorg/tensormap/issues/59) | [#60](https://github.com/c2siorg/tensormap/pull/60) | ✅ |
| Poetry Integration | [#61](https://github.com/c2siorg/tensormap/issues/61) | [#62](https://github.com/c2siorg/tensormap/pull/62) | ✅ |
| Documentation Update | [#63](https://github.com/c2siorg/tensormap/issues/63) | [#64](https://github.com/c2siorg/tensormap/pull/64) | ✅ |
| Image Dataset Integration | [#65](https://github.com/c2siorg/tensormap/issues/65) | [#70](https://github.com/c2siorg/tensormap/pull/70) | ✅ |
| Preprocessing Image Data | [#71](https://github.com/c2siorg/tensormap/issues/71) | [#72](https://github.com/c2siorg/tensormap/pull/72) | ✅ |
| Minor bug fixes in preprocessing | [#73](https://github.com/c2siorg/tensormap/issues/73) | [#74](https://github.com/c2siorg/tensormap/pull/74) | ✅ |
| Introducing simple CNN training | [#75](https://github.com/c2siorg/tensormap/issues/75) | [#76](https://github.com/c2siorg/tensormap/pull/76) | ✅ |

## What Was Covered
The TensorMap project has undergone significant development, focusing on enhancing its functionality, usability, and deployment process. Here's a summary of the key implementations:

1. **Dockerization:** The backend of TensorMap has been dockerized, allowing for easier deployment and environment consistency. This includes creating a Dockerfile and using Docker Compose for setup.

2. **Client-side Improvements:** Various client-side enhancements were made, including fixing dependency issues, transitioning components from class-based to functional, and integrating Prettier for code formatting. The project also shifted to using Vite for faster builds and better performance.

3. **Dataset Handling:** New features were added for dataset management, such as viewing, preprocessing, and deleting datasets. This also includes handling image datasets and introducing preprocessing techniques for both numerical and string data.

4. **Modeling Capabilities:** The project expanded its machine learning capabilities by adding support for linear regression and convolutional neural networks (CNNs), including Conv2D. These models can now handle both numerical and image data, with a focus on usability for beginners.

5. **Server-side Enhancements:** Alongside the Dockerization, the server was cleaned up, and several middleware functions were added to support the new functionalities, such as handling multiple inputs for models.

6. **User Interface and Experience:** The navigation and sidebar were improved, and a progress bar was introduced that dynamically updates during model training. Alerts and modals were also fixed for better user feedback.

7. **Documentation and Testing:** Documentation was updated to reflect the new changes, and extensive testing was implemented across both the client and server sides to ensure stability and reliability.

## What is Left

All deliverables for the project have been met.
