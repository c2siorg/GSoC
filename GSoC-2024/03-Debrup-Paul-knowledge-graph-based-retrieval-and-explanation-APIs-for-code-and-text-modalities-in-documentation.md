# knowledge graph based retrieval and explanation modules for code and text modalities in documentation
## Student Info
  * Name - Debrup Paul
  * Email - f20212946@goa.bits-pilani.ac.in / debrup.dpsrpk@gmail.com
  * University - Birla Institue of Technology and Science,Pilani
  * [GitHub profile](https://github.com/debrupf2946)
  * [LinkedIn profile]( https://www.linkedin.com/in/debrup-paul-599158227/)

# Project Abstract
graph-rag is project under Project Explainer containg 3 modules,for building Knowledge Graph from code and text modalities from documentation.
- Knowledge graph builder
- Knowledge graph retriever
- Knowledge graph evaluation

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2024/projects/jf5D7VwU)

## [GSoC Project Proposal](http://LinikToYourGSoCProjectProposal)

## [GitHub Organization Repo](https://github.com/c2siorg/Project-Explainer)

## [GitHub Personal Repo](https://github.com/c2siorg/Project-Explainer/tree/main)

## [Commits during GSoC 2024](https://github.com/c2siorg/Project-Explainer/pulls?q=is%3Apr+author%3Adebrupf2946+)

## [Project Demo Video]()
- [Knowledge Graph Evaluation](https://github.com/c2siorg/Project-Explainer/blob/main/graph_rag/evaluation/README.MD)
- [Knowledge Graph Builder](https://github.com/c2siorg/Project-Explainer/blob/main/graph_rag/graph_builder/README.MD)
- [Knowledge Graph Retriever](https://github.com/c2siorg/Project-Explainer/blob/main/graph_rag/graph_retrieval/README.MD)

## [Project Wiki](https://github.com/c2siorg/Project-Explainer/blob/main/README.md)

## [GSoC Blog](https://medium.com/@QuantiPhy/road-to-graph-rag-f729c85e7807)

### Work Summary

1. **Knowledge Graph Builder:**
   - Developed a tool to build a Knowledge Graph from unstructured data (e.g., .md and .py files).
   - Implemented functionality to load, chunk, and index documents using llama-index.
   - Set up a local LLM (Llama3) with Ollama for building and querying the Knowledge Graph.
   - Provided methods to visualize and save the graph as an HTML file.
   - Experimented Llama-index Property Graph with Relik,built with llama 3.1

2. **Experiments with Models and Embeddings:**
   - Experimented with various models, embeddings, and libraries to optimize Knowledge Graph construction.
   - Used models like Salesforce/codegen2-7B_P, Salesforce/codet5p-110m-embedding, and several others, often quantizing them to 4 bits for efficiency.
   - Focused on open-source models compatible with free Colab environments.

3. **Graph Index Retriever:**
   - Created a module to load and query a graph index using a Llama-Index query engine.
   - Integrated advanced training techniques, including QLoRA and P-Tuning, for fine-tuning LLMs to improve retrieval and response quality.

4. **Knowledge Graph Evaluation:**
   - Developed tools to evaluate the performance of the Knowledge Graph using Llama-Index and Ragas evaluation packs.
   - Implemented QA generation and critique functionalities, focusing on metrics like groundedness, relevance, and standalone quality.
   - Provided scripts to create custom test datasets and benchmark GraphRag performance.

This summary encapsulates the core contributions and developments you made during the GSoC period at C2SI.

### What Was Covered
I focused on foundational research, experimentation, and the creation of modules related to Knowledge Graph creation, retrieval, and evaluation.
- #### [PR1](https://github.com/c2siorg/Project-Explainer/pull/34)
    The GraphRag folder contains Modules allows users to construct a Knowledge Graph from unstructured data (e.g., .md, .py files).
    -  Transforms unstructured documents into a structured Knowledge Graph by identifying key entities and relationships.
    - Utilizes the locally-run llama3 model for advanced content processing.
    - Outputs an interactive HTML file to explore and view the Knowledge Graph.
    -  Built to easily support additional data formats and models in the future.

- #### [PR2](https://github.com/c2siorg/Project-Explainer/pull/35)
    Graph Index Retriever Module, which includes methods for:
    - Loading a graph index from a pickle file.
    - Setting up a llama_index query engine.
    - Querying the graph index.

    These functionalities enable efficient querying of Knowledge Graphs using LLMs.

- #### [PR3](https://github.com/c2siorg/Project-Explainer/pull/36)
    Contains all artifacts and experiments data for this project
   - Experiments markdown file
    - Contains all the experiments that are being performed for building KG

- #### [PR4](https://github.com/c2siorg/Project-Explainer/pull/37)
    Modules and experiments with regard to graph-rag evaluation
    -  GraphRag data set generator
    - Evaluation with Llama-Index
    - Evaluation with Ragas


- #### [PR5](https://github.com/c2siorg/Project-Explainer/pull/39)
    Modules and experiments with regard to Knowledge Graph retrieval
    - p-tuning retriever on custom data, used for retrieval of KG
    - QLora trained retriever on custom data, used for retrieval of KG
    - Knowledge Graph using llama-index property graphs and relik,stored in neo4j aura-db


### What Is Left

From my side, all planned work is complete. However, this project has great future potential, and additional work can be pursued.

---