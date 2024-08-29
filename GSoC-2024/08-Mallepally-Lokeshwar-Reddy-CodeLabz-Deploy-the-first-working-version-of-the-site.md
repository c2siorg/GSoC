# CodeLabz - Deploy the First Working Version of the Site.

# Project Abstract
CodeLabz is a platform for users to engage with online tutorials and for organizations to create and manage them. Developed with ReactJS, Node.js, Redux, and Firebase, it features user authentication, tutorial creation, recommendations, and dynamic in-app notifications. Key functionalities include a recommender system, a search bar for tutorials, a "Who to Follow" sidebar, a verification system during signup, and a like/dislike feature for tutorials and comments. The project also includes a CI/CD pipeline for deployment.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2024/projects/DqAwlznt)

## [GSoC Project Proposal](https://drive.google.com/file/d/1nRWXxOil-ZMngFau8mCEKF1-3jMjC3op/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/c2siorg/Codelabz)

## [GitHub Personal Repo](https://github.com/lokeshwar777/Codelabz)

## [Commits during GSoC 2024](https://github.com/lokeshwar777/Codelabz/commits/master-gsoc-24/)

<!-- ## [Project Demo Video](http://LinkToDemoVideo) -->

## [Project Wiki](https://github.com/scorelab/Codelabz/wiki)

## [GSoC Blog](https://bit.ly/codelabz-gsoc-24)
This Notion page documents the research conducted during the GSoC period.

# Work Summary
|**Task**|**Description**|**PR Link**|
|-|-|-|
|CI/CD Pipeline and Deployment  |Rebuilt the CI/CD pipeline and deployed the first working version of the site.|[#138](https://github.com/c2siorg/Codelabz/pull/138)|
|Upgrade Cypress Workflow|Optimized Cypress setup for faster and more reliable test execution.|[#140](https://github.com/c2siorg/Codelabz/pull/140)|
|GitHub Actions Workflow Improvement|Improved existing GitHub Actions workflows for a better developer experience.|[#142](https://github.com/c2siorg/Codelabz/pull/142)|
|Like/Dislike Feature|Added functionality for liking and disliking tutorials and comments.|[#144](https://github.com/c2siorg/Codelabz/pull/144)|
|Fix Comment Display Issue|Fixed issues related to comment display and improved comment submission handling.|[#146](https://github.com/c2siorg/Codelabz/pull/146)|
|Dynamic In-App Notification System|Replaced static notification system with a dynamic one and added notification badge.|[#148](https://github.com/c2siorg/Codelabz/pull/148)|
|Search Bar for Tutorials|Implemented a search bar on the home page to enable users to search for tutorials.|[#150](https://github.com/c2siorg/Codelabz/pull/150)|
|Verification System on Signup|Added verification during signup and redirection to the login page after successful signup.|[#152](https://github.com/c2siorg/Codelabz/pull/152)|
|Recommender System|Developed a system to recommend tutorials on the home page based on specific criteria.|[#154](https://github.com/c2siorg/Codelabz/pull/154)|
|Tutorial Page Completion|Fixed bugs related to author data and comment display.|[#156](https://github.com/c2siorg/Codelabz/pull/156)|
|Dynamic Sidebar Data|Rendered dynamic data on the sidebar, including "Who to Follow" section.|[#158](https://github.com/c2siorg/Codelabz/pull/158)|


# What Covered
- Implemented Like/Dislike feature for tutorials and comments.
- Completed the Tutorial Page with bug fixes, author data, and comments display, and added tutorial recommendations.
- Replaced the static notification system with a dynamic in-app notification system, including a notification badge.
- Developed a recommender system for the home page that filters tutorials based on specific criteria.
- Rebuilt the CI/CD pipeline and deployed the first working version of the site.
- Added a search bar on the home page for tutorial search functionality.
- Implemented dynamic data rendering on the sidebar ("Who to Follow").
- Added a verification system during signup with redirection to the login page.
- Improved GitHub Actions workflows for a better developer experience.

# What left
- Managing Org-Setting Including Roles and Permissions for the Users.
- Tutorials Creation By Individual Users.
- Updating Minor dependencies and migration to Typescript for better code quality.