# Project Name
Bug-Connector Proposal 
# Project Abstract
This project provides a system that maps Common Vulnerabilities and Exposures (CVE) data from public sources (like MITRE and NIST) to historical commit data from the Apache repository. The system uses natural language processing (NLP) models, specifically SentenceTransformers, to generate semantic embeddings of text and computes cosine similarity to identify the most relevant commits for each CVE. This allows developers and security researchers to link vulnerabilities to specific code changes, making it easier to track the resolution of security issues in open-source software.

The project is designed as a command-line interface (CLI) tool for ease of use, allowing users to query specific CVEs, view relevant commit messages, and output the results to a file. The system also supports processing large datasets from MITRE and NIST to maintain up-to-date vulnerability mappings.
## [GSoC Project Page](http://LinikToYourGSoCProjectPage)https://summerofcode.withgoogle.com/myprojects
## [GSoC Project Proposal](http://LinikToYourGSoCProjectProposal)
https://summerofcode.withgoogle.com/myprojects/details/rmFUzLkp
## [GitHub Organization Repo](http://github.com/repo)
https://github.com/c2siorg/bug-connector
## [GitHub Personal Repo](http://github.com/repo)
https://github.com/dilishwaggins/bug-connector
## [Commits during GSoC 2017](http://github.com/commits)

## [Project Demo Video](http://LinkToDemoVideo)

## [Project Wiki](http://github.com)
https://github.com/dilishwaggins/bug-connector/blob/main/README.md
## [GSoC Blog](http://GSoCBlog)

# Work Summary
Phase 1: Historical Data Compilation

Weeks 1-2 (10 hours): Project Setup
Set up the project, including environment setup and dependency installation.
Installed key libraries like pandas, sentence-transformers, and scikit-learn.
Cloned and organized the GitHub repository.

Weeks 3-5 (40 hours): Data Collection
Developed scripts to gather CVE data from MITRE and NIST via APIs and static files.
Created web scraping scripts to fetch Apache commit history and processed it into a structured format.
Ensured data integrity and completeness while working with multiple sources of vulnerability and commit information.

Weeks 6-8 (60 hours): Data Pre-processing
Preprocessed CVE data and commit messages to normalize the format, handle missing values, and clean the text.
Applied tokenization and text pre-processing techniques like stopword removal, stemming, and lowercasing for uniformity.

Weeks 9-12 (40 hours): CVE-Commit Matching Algorithms
Developed matching algorithms based on:
Cosine similarity: Using semantic similarity to match CVE descriptions to commit messages.
Evaluated the efficiency of the algorithm and implemented fallback mechanisms for edge cases where timing data was insufficient.

Weeks 13-14 (40 hours): Exploring Feasibility of LLMs
Explored the use of large language models (LLMs) for improved CVE-to-commit matching.
Evaluated the SentenceTransformer model and implemented it for computing cosine similarity between CVE descriptions and commit messages.

Phase 2: Real-Time Integration

Weeks 15-16 (20 hours): Designing System Architecture
Designed a modular system architecture for real-time CVE monitoring, focusing on scalability and flexibility.
Defined clear boundaries between components like data loading, data processing, and model application.

Weeks 17-18 (40 hours): Real-Time Pipeline Implementation
Implemented a real-time pipeline to integrate the historical model with live updates from MITRE and NIST CVE databases.
Integrated the real-time CVE updates with the Apache commit data to maintain a constantly updated mapping.

Weeks 19-20 (20 hours):Documentation
Created comprehensive system documentation, including guides on architecture, operation, and contribution.

Weeks 21-22(20 hours): Final Report
Prepared the final report summarizing system performance, limitations, and recommendations for future improvements.

# What Covered
-Data Collection and Preprocessing: Comprehensive scripts were developed to collect CVE and commit data from MITRE, NIST, and Apache repositories.

-CLI Development: A command-line interface was implemented to allow users to input a CVE ID and receive relevant commit mappings.

-Cosine Similarity: Semantic embeddings were computed using SentenceTransformer to match CVEs to relevant commits with a user-defined similarity threshold.

-Real-Time Integration: The system architecture was designed for real-time updates of CVE-commit mappings.

-System Documentation: Detailed user guides and developer documentation were written for easy onboarding and usage.

# What left
-Advanced Real-Time Monitoring: Further work is required to continuously monitor new CVEs and update the mappings in real-time.

-Evaluation Metrics Enhancement: The current system uses basic evaluation metrics like precision and recall, but more sophisticated metrics could be introduced for nuanced evaluation.

