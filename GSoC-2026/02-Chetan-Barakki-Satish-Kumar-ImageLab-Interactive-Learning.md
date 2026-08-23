# ImageLab: Building Interactive Learning with GSoC 2026
**Contributor:** [Chetan Barakki Satish Kumar](https://github.com/chetanbarakki)

**Mentor:** [Oshan Mudannayake](https://github.com/ivantha)

# Project Abstract
ImageLab is a block-based image processing environment built using Blockly and OpenCV. During GSoC 2026, I worked on extending ImageLab from a pipeline execution tool into a more interactive environment for learning, experimentation, and reusable image-processing workflows.

The project focused on five major areas: interactive step-by-step pipeline inspection, image analysis, pipeline persistence and sharing, batch processing, and reusable custom macros. Together, these features allow users to understand intermediate processing results, save and reuse their work, process multiple images, and build more reusable workflows.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2026/projects/yPbEIkbf)

## [GSoC Project Proposal](https://drive.google.com/file/d/10UbhycGH0M6fE1jbhzTERbGA9pesoX49/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/imagelab/)

## [GitHub Personal Repo](https://github.com/chetanbarakki/imagelab/)

## [Commits during GSoC 2026](https://github.com/c2siorg/imagelab/commits/main/?author=chetanbarakki)

## [Project Demo Video](https://drive.google.com/file/d/1KlXSH8s_HEJl9qoJbzS4raUCsOxfOOJU/view?usp=sharing)

## [Project Wiki](https://github.com/c2siorg/imagelab/blob/main/README.md)

## [GSoC Blog](https://medium.com/@chetanbarakki24/building-interactive-learning-in-imagelab-with-gsoc-2026-b0577ce0e577)

# Work Summary
During GSoC 2026, I extended ImageLab across five major areas:

1. **Interactive Pipeline Execution**
   - Added visibility into intermediate pipeline results.
   - Allowed individual pipeline steps to be selected and inspected.
2. **Image Analysis**
   - Added image metadata and histogram-based analysis for pipeline results.
   - Allowed users to inspect quantitative properties of intermediate images.
3. **Pipeline Persistence**
   - Added saving and loading of pipelines.
   - Added pipeline versioning, restoration, sharing, and cloning.
4. **Batch Processing**
   - Added batch execution for processing multiple images using a pipeline.
   - Added background processing, progress tracking, failure handling, and downloadable results.
5. **Custom Macros**
   - Added reusable custom macros for groups of Blockly operations.
   - Added graph-based validation and macro expansion during execution.
   
The major implementation work was completed across the ImageLab frontend and backend, with the corresponding changes submitted through the project's GitHub pull requests.

# What Covered

## 1. Interactive Pipeline Execution
Extended ImageLab's pipeline execution flow to expose intermediate results instead of showing only the final processed image. Users can now inspect individual pipeline steps and view the corresponding intermediate outputs, making it easier to understand how each operation transforms an image.
<img width="1268" height="594" alt="image" src="https://github.com/user-attachments/assets/404755a1-eab6-42bb-a61a-1d020be19e0f" />

## 2. Image Analysis

Added an image analysis workflow for intermediate pipeline results. Users can inspect image metadata and histogram information for the selected step, making it possible to understand changes in the image both visually and quantitatively.
<img width="1280" height="593" alt="image" src="https://github.com/user-attachments/assets/d2e32cbe-a4be-4370-9aa2-6d5b1352e00c" />

## 3. Pipeline Persistence

Implemented persistent pipeline storage so that pipelines can be saved and loaded instead of existing only as temporary workspace state. Added pipeline versioning and restoration, allowing users to maintain previous versions while experimenting with their workflows. Pipeline sharing and cloning were also added to make pipelines easier to reuse and collaborate on.
<img width="550" height="418" alt="image" src="https://github.com/user-attachments/assets/68ac93e6-e995-4c0d-a05b-6a469babca2a" />


## 4. Batch Processing

Implemented a batch processing engine that allows a pipeline to be executed on multiple images as a background job. The system tracks job progress, handles individual image failures without stopping the entire batch, and provides downloadable processing results along with summary and error information.

The batch execution engine also uses bounded concurrency so that multiple images can be processed without allowing an uncontrolled number of workers to consume backend resources.
<img width="650" height="514" alt="image" src="https://github.com/user-attachments/assets/17c02605-a728-4db0-9874-3883b19b86eb" />


## 5. Custom Macros

Implemented custom macros that allow users to save a connected group of Blockly operations as a reusable block. Macros are persisted and can be reused in other pipelines, reducing repetition when building workflows.

The macro system represents macro dependencies as a directed graph. DFS-based cycle detection is used to prevent circular dependencies, while Kahn's topological sorting algorithm is used to determine a valid execution order. During execution, macros are expanded into their underlying operations and processed through the existing pipeline execution flow.
<img width="1280" height="511" alt="image" src="https://github.com/user-attachments/assets/e779f082-8740-4e03-a28e-dcdb9e700e69" />


# What left

The current implementation provides the foundation for further improvements to ImageLab. Some possible directions for future development are:

## 1. Parallel DAG Execution

The current pipeline engine executes DAG nodes sequentially after macro expansion. A future improvement would be to extend Kahn's topological processing to identify independent execution levels and execute independent nodes concurrently. This could improve performance for pipelines containing multiple independent branches.

## 2. More Expressive Control Flow

The current conditional workflow can be extended to support richer expressions and more complex conditions. Future work could include multiple variables, logical operators such as `AND` and `OR`, and additional image properties such as standard deviation, aspect ratio, and channel statistics.

## 3. Expanding Reusable Workflow Patterns

The custom macro system can be extended with additional reusable workflow patterns for more complex and iterative image-processing tasks. This could provide users with greater flexibility while keeping the main ImageLab pipeline interface simple and approachable.
