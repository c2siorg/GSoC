# SkamShield

# Project Abstract
Users often encounter calls, SMS messages, and links across various mobile platforms, including browsers, social media, and messaging apps. However, when doubts arise regarding the legitimacy of these communications, such as suspicions of phishing attacks or the presence of malicious links, users currently lack a dedicated platform for submitting and reviewing such content. This absence of a centralized platform leaves users vulnerable to potential threats, as they lack a reliable mechanism to report and verify suspicious communications. Consequently, there is a pressing need for the development of a dedicated platform where users can submit calls, SMS messages, and links for review by trusted authorities or community members. Such a platform would empower users to proactively address security concerns, enhance collective awareness of potential threats, and contribute to the creation of a safer digital environment for all mobile users. To address this pressing issue, we propose the development of a comprehensive mobile application equipped with automatic detection capabilities tailored to identify and mitigate spam and scams. In addition to its automated features, the application empowers users to manually contribute instances of suspicious content encountered on diverse platforms, fostering a community-driven approach to combating online fraud. Complementing the mobile app, a dedicated web application will cater to administrative users, providing them with the tools and resources needed to conduct thorough reviews of reported instances. Through a systematic review process, pertinent information about identified spams and scams will be meticulously documented and stored in a secure database, facilitating further analysis and informing future detection strategies.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2024/projects/9gHu616G)

## [GSoC Project Proposal](https://github.com/user-attachments/files/16729515/skam_shield_project_proposal.pdf)

## [GitHub Organization Repo](https://github.com/c2siorg/SkamSheild)

## [GitHub Personal Repo](https://github.com/hachchi/SkamSheild)

## [Commits during GSoC 2017](https://github.com/c2siorg/SkamSheild/commits/main/?author=hachchi)

## [Project Demo Video](https://github.com/user-attachments/assets/fe78f84c-1fc6-4661-8a56-38ab82d1ac03)

## [Project Wiki](https://github.com/c2siorg/SkamSheild/blob/main/README.md)

## [GSoC Blog](https://medium.com/@don.akikk)

# Work Summary
We developed *Skam Shield*, a comprehensive cybersecurity project designed to protect users from online scams and malicious content. The project includes several components: a mobile client for real-time threat detection and user reporting, a web client for administrators to manage and review reports, a browser extension to flag dangerous URLs in search results, and a honeypot system for deploying and monitoring traps across cloud platforms. Each component integrates with Firebase for data management and utilizes modern tools like React Native, Docker, and Terraform, offering a robust defense against online threats.

| Features          | PR Link               |
| ----------------- |:----------------------- |
| Implement UI for web-client      | [PR 1](https://github.com/c2siorg/SkamSheild/pull/2)   |
| Implement UI for the IOS/ Android Mobile Client | [PR 2](https://github.com/c2siorg/SkamSheild/pull/5)     |
| Implement AI assistance Chatbot UI for IOS/ Android Mobile Clients     | [PR 3](https://github.com/c2siorg/SkamSheild/pull/10)     |
| Integrate firebase with react context for mobile clients       | [PR 4](https://github.com/c2siorg/SkamSheild/pull/11)    | 
| Implement Spam/ Scam aware browser extension   | [PR 5](https://github.com/c2siorg/SkamSheild/pull/12) |
| Implement honeypot data collector on cloud vendors   | [PR 6](https://github.com/c2siorg/SkamSheild/pull/13) |
| Fix UI issues  | [PR 7](https://github.com/c2siorg/SkamSheild/pull/14) |
| Documentation   | [PR 8](https://github.com/c2siorg/SkamSheild/pull/15) |

# What Covered
- **Mobile Client Development**:
  - Built using React Native.
  - Features include user authentication, search for suspicious content and malicious content reporting.
  - Integration with Firebase for data storage and management.

- **Web Admin Client**:
  - Developed with React.js for administrators.
  - Allows for review and management of user-reported suspicious content.
  - Includes search, filter, and status management functionalities.

- **Browser Extension**:
  - Developed a Chrome extension to detect and flag suspicious URLs in Google search results.
  - Automatically checks URLs against a Firestore database and highlights dangerous ones.

- **Partial Firebase Integration**:
  - Unified backend using Firebase for all components, ensuring seamless data handling and synchronization.

- **Project Documentation**:
  - Detailed `README.md` files for each component, including setup instructions, key features, and usage guidelines.
  - Visual documentation with screenshots and demos for better understanding.

- **Contributions and Licensing**:
  - Open for contributions with clear guidelines.
  - Licensed under the MIT License.


# What left
- **Full Firebase Integration for Mobile Client**:
  - Complete the integration of Firebase services for the mobile client, including real-time database, authentication, and storage.

- **Search, Filter, and Status Management in Web Client**:
  - Implement search, filter, and status management functionalities in the web admin client for efficient handling of user reports.

- **Complete Honeypot Project**:
  - Finalize the deployment and monitoring of honeypots across cloud platforms. Ensure data collection and analysis are fully operational.

- **Fix Issues in Browser Extension**:
  - Address and resolve any remaining bugs or performance issues in the Scam URL Checker browser extension.
