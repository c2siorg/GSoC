# WebFL

# Project Abstract
Federated Learning (FL) is a machine learning (ML) approach that allows models to be trained collaboratively and distributedly without sharing individual data points. WebGPU, a modern web standard and API, provides low-level, high-performance access to a device's GPU through web browsers. It aims to enable developers to create complex graphical applications and experiences on the web by utilizing modern GPU hardware for efficient graphics rendering. Due to their extensive usage and customized optimizations, current Federated Learning (FL) systems frequently concentrate on certain device types, such as smartphones or Internet of Things (IoT) devices. Nevertheless, FL's adaptability to other device kinds may be limited by this device-centric optimization, necessitating substantial coding and redesign work to modify FL systems for diverse device types. Because developers wind up building different and fragmented codebases for each device, this method violates software engineering principles of code reusability, making maintenance more difficult and impeding the effective deployment of FL. In this proposal, a novel WebGPU based federated learning network for heterogeneous device network is proposed. The proposal aims to deliver a working federated learning system supported by web browsers along with additional features. 

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2024/projects/l7SskZNS)

## [GSoC Project Proposal](https://docs.google.com/document/d/1YijAVhZs_IZ7GLnTNfDuYwmucM9mC0d6WaQ6qXi7lDI/edit?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/WebFL)

## [GitHub Personal Repo](https://github.com/sonodew/WebFL)

## [Commits during GSoC 2017](https://github.com/sonodew/WebFL/commits/main/?author=sonodew)

## [Project Wiki](https://github.com/sonodew/WebFL/blob/main/README.md)

## [GSoC Blog](https://medium.com/@sonos69)

# Work Summary

WebFL is a browser based (WebGPU) federated learning framework for training machine learning models. Since this is the beginning of the project, the focus was to implement the basic functionality of the cllient and the server. The WebFl Client is focused on training the model on the browser by using the data available and the WebFL server is working on the network management and the global model generation process. During the GSoC time period, The main functionality of each componet is implemented.

| Features          | PR Link               |
| ----------------- |:----------------------- |
| Initializes the client project      | [PR 1](https://github.com/c2siorg/WebFL/pull/3)   |
| Initialize the server project | [PR 2](https://github.com/c2siorg/WebFL/pull/4)     |
| Update server project     | [PR 3](https://github.com/c2siorg/WebFL/pull/5)     |
| Add basic server implementation       | [PR 4](https://github.com/c2siorg/WebFL/pull/7)    | 
| Update client project with CRA and tfjs   | [PR 5](https://github.com/c2siorg/WebFL/pull/9) |
| Add runtime utilities for server runtime   | [PR 6](https://github.com/c2siorg/WebFL/pull/10) |
| Finalize the implementation   | [PR 7](https://github.com/c2siorg/WebFL/pull/11) |
| Documentation   | [PR 8](https://github.com/c2siorg/WebFL/pull/12) |

# What Covered

1. Initilization of the global model in the server and broadcast it into the client after the client is connected to the server. The global model is converted to onnx format for the model training process prior to send the model to the client
2. Once the client is connected, client can communicate with the global model and start the training process on the browser. Note that in this phase, an assumtion was made s.t the client has the data inside the local storage of the browser prior to the model training begins.
3. In each federation round, after the client finishes the training of the model, the weights are transfered to the server and server waits for all the clients to send its updates prior to the global model generation.
4. Once the global model is generated, the server send back the aggregated model weight to the client network for the further training.
5. A conditional loop has added to stop the training when the desired federation round is met.
6. Server is implemented using python Flask where the client is implemented using react and onnx runtime.

# What left
1. Current UI of the project is very primitive and needs to improve.
2. More features, s.t. Differential Privacy techniques, Client Selection, Hierarchical Federated Learning approach should be added into the process.