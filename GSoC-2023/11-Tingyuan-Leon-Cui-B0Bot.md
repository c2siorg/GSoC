# B0Bot - Cybersecurity News API

# Student Info

- Name: Tingyuan Cui
- Email: cty.works@gmail.com
- Github: [CoToYo](https://github.com/CoToYo)
- LinkedIn: [Tingyuan(Leon) Cui](https://www.linkedin.com/in/tingyuan-cui-b02155204/)
- Medium: [@Tingyuan(Leon) Cui](https://medium.com/@cty.works)

# Project Abstract

In this project, our objective is to develop a Cybersecurity News API tailored for automated bots on social media platforms.

It is a cutting-edge Flask-based API that grants seamless access to the latest cybersecurity and hacker news. Users can effortlessly retrieve news articles either through specific keywords or without, streamlining the information acquisition process.

Once a user requests our API, it retrieves news data from our knowledge base and feeds it to ChatGPT. After ChatGPT processes the data, the API obtains the response and returns it in JSON format.

#### High-level Architecture:

Our API lives inside a Flask API and is powered by LangChain and OpenAI API.

In addition, to keep the knowledge base of news up to date, a scheduled script will be executed on a regular interval to retrieve the most recent cybersecurity news by scraping a list of target news websites and store them into the MongoDB Atlas Database. Everytime a user requests the API, news in the database will be read into LangChain's memory and fed to the LLM of OpenAI. Then, answers will be generated based on both OpenAI model and our knowledge base.

![image](https://user-images.githubusercontent.com/56789038/251870854-218fdf2b-be27-4222-9119-81c3dc5c4e02.png)

![image](https://user-images.githubusercontent.com/56789038/251878034-4e5fe460-a210-46e9-b490-caa02e34c3af.png)

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2023/projects/qdMmh9Hb)

## [GSoC Project Proposal](https://drive.google.com/file/d/1g9Tfl5HteSslEOV81mRaWjorZZ3ZS-Mi/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/b0bot)

## [GitHub Personal Repo](https://github.com/CoToYo/b0bot)

## [Commits during GSoC 2023](https://github.com/c2siorg/b0bot/commits?author=CoToYo)

## [Project Demo Video](https://youtu.be/6ArNHn4Qd3U)

## [GSoC Blog](https://medium.com/@cty.works)

# Work Summary

During the Google Summer of Code 2023 program, I developed a Flask API for auto bots on social medias to obtain recent cybersecurity and hacker news. 

At the very begining, I am expected to build a Twitter (now called X) bot for helping its followers to know about recent cybersecurity and hacker related news and knowledge. But subject to the changes of the price of Twitter APIs, mentors and I decided to rethink the project proposal, which leading us to build a cybersecurity nes API based on LangChain and OpenAI LLM (ChatGPT 3.5).

The API I built is under the Flask framework, which is deployed on cloud platform Render. All interactions between the API and ChatGPT is implemented using [LangChain](https://python.langchain.com/docs/get_started/introduction.html). Since the newest data studied by ChatGPT are from a few years ago,  web scraping technic is integrated into our API to fetch the up-to-date news data. Also, to improve the efficiency, all news data fetched are stored in a separate knowledge base using MongoDB Atlas. The knowledge base will be updated periodically by a scheduled web scraping script.

# What Covered

#### [PR 1](https://github.com/c2siorg/b0bot/pull/12)

- Set up Flask development environment.
- Set up OpenAI developer account.
- Implemented basic Flask API functionality by integrating LangChain.
- Processed the API response in JSON format
- Performed testing using unit tests and Postman.

#### [PR 2](https://github.com/c2siorg/b0bot/pull/13)

- Refactored the code structure for better extendibility.
- Updated readme file, adding new diagram of knowledge base design and rewriting the project description.
- Performed testing using Postman.

#### [PR 3](https://github.com/c2siorg/b0bot/pull/14)

- Set up the MongoDB Atlas database for cyber news storage.
- Implemented database update script.
- Performed testing using Postman.

#### [PR 4](https://github.com/c2siorg/b0bot/pull/15)

- Refined the API by connecting MongoDB knowledge base and ChatGPT.
  - Retrieve news data from knowledge base
  - Feed retrieved news data to ChatGPT.
- Performed testing using Postman.
- Updated readme file.



# What left

1. Reduce response time of the API
2. Get the latest news data from more channels

# Refernce

1. [What is LangChain?](https://www.youtube.com/watch?v=_v_fgW2SkkQ&list=PLqZXAkvF1bPNQER9mLmDbntNfSpzdDIU5)
2. [LangChain Doc](https://python.langchain.com/docs/get_started/introduction.html)
3. [LangChain Tutorials](https://github.com/gkamradt/langchain-tutorials/blob/main/LangChain%20Cookbook%20Part%201%20-%20Fundamentals.ipynb)
4. [OpenAI API Doc](https://platform.openai.com/docs/introduction)
5. [ChatGPT (Medium)](https://medium.com/tag/chatgpt)
6. [A Complete Guide to the ChatGPT API](https://www.makeuseof.com/chatgpt-api-complete-guide/)
7. [Python package: cybernews](https://github.com/hitesh22rana/cybernews)
8. [Llama Hub](https://llamahub.ai/)
9. [MongoDB Atlas](https://www.mongodb.com/atlas)