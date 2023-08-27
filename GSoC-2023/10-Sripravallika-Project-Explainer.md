# Project Explainer

## Student Info

### Name         

Sripravallika Bandarupalli

### Email

sripravallikab@gmail.com

### GitHub       

[sripravallikab](https://github.com/sripravallikab)

### LinkedIn    

[Sripravallika](https://www.linkedin.com/in/sripravallika-bandarupalli)


## Project Abstract

![](https://raw.githubusercontent.com/c2siorg/Project-Explainer/main/static/logos/logo.svg)

Large Language Models are picking pace very quickly and they are turning out to be extremely good in multiple tasks. With the help of zero-shot, few-shot, and fine tuning techniques we could effectively specialize a language model for the use case. Summarization is one such use case that has been widely researched for a couple of years now. Broadly there are techniques such as Abstractive and Extractive approaches. The motive of this project proposal is to handle the summarization task (mostly Abstractive + Extractive hybrid approach) through the language model’s (foundation model) lens. This project aims to cover everything from data collection, EDA, experimenting with different language models to developing production-scale system that can take GitHub repo as reference and provide summary. One of the challenges that is novel is to use smaller sized models to achieve great performance in summarization. SCoRe Lab has been into developing solutions in the space of making user life easier with products such as D4D, Bassa, Track Pal, and others. This project will add to that portfolio and would be a great reference for AI practitioners and system developers which aims to work right from data to production-grade end product using AI and Systems. This repository will hold, data/data references, experiments, and a system that takes GitHub Link as input and provides a summary for the repository.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2023/projects/eJoLPhgw)

## [GSoC Project Proposal](https://drive.google.com/file/d/1pIDpls9glIbTbjknwboksxa8irMt88Vt/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/Project-Explainer)

## [GitHub Personal Repo](https://github.com/sripravallikab/Project-Explainer)

## [Commits during GSoC 2023](https://github.com/c2siorg/Project-Explainer/pulls?q=is%3Apr+author%3Asripravallikab+)

## [Demo](https://huggingface.co/spaces/SriPravallikaB/projectexplainer)

## Work Summary
Work involved creating multiple components for Project Explainer, running through some experiments on base nlp models, creating an [intial demo deployment](https://huggingface.co/spaces/SriPravallikaB/projectexplainer) and providing docs for module based usage for other projects.

## What Covered
All the PRs made during the work are available [here](https://github.com/c2siorg/Project-Explainer/pulls?q=is:pr+author:sripravallikab+)

1. Experiments done during the tenure can be found [here](https://github.com/c2siorg/Project-Explainer/tree/main/experiments). Contributed PRs - [2](https://github.com/c2siorg/Project-Explainer/pull/2), [7](https://github.com/c2siorg/Project-Explainer/pull/7), [12](https://github.com/c2siorg/Project-Explainer/pull/12).

2. Complete project processor module has been written which extracts useful pieces of information from markdown files that could contribute for better summarization. Contributed PRs - [5](https://github.com/c2siorg/Project-Explainer/pull/5), [8](https://github.com/c2siorg/Project-Explainer/pull/8), [13](https://github.com/c2siorg/Project-Explainer/pull/13), [14](https://github.com/c2siorg/Project-Explainer/pull/14)

3. Complete project explainer module has been written which acts as a wrapper over project processor module  to prepare information and handle sending that as input to any hugggingface complaint nlp model and returns the output. Contributed PRs - [8](https://github.com/c2siorg/Project-Explainer/pull/8), [13](https://github.com/c2siorg/Project-Explainer/pull/13), [9](https://github.com/c2siorg/Project-Explainer/pull/9)

4. Wrote a simple gradio based UI to consume the initial version of project explainer. The UI is hosted [here](https://huggingface.co/spaces/SriPravallikaB/projectexplainer). Contributed PRs - [13](https://github.com/c2siorg/Project-Explainer/pull/13), [14](https://github.com/c2siorg/Project-Explainer/pull/14)

5. Wrote complete documentation covering the installation of dependencies and usage. Contributed PRs - [16](https://github.com/c2siorg/Project-Explainer/pull/16), [15](https://github.com/c2siorg/Project-Explainer/pull/15), [1](https://github.com/c2siorg/Project-Explainer/pull/1)

## What left
1. Add more coverage to extract better pieces of information from GitHub repositories
2. Perform more experiments and train models for summarization (need GPUs support here).
