# NodeCloud- Oracle and Linode Cloud Providers


# Student Info

- Name - Partik Singh
- Email - partikbumrah13508@gmail.com
- University - Indian Institute of Technology, Varanasi
- GitHub Profile - https://github.com/partik03
- LinkedIn profile - https://www.linkedin.com/in/partik-singh-945a87227/
- Medium - https://medium.com/@partikbumrah13508
- Project Link: [https://summerofcode.withgoogle.com/programs/2023/projects/62Zo1VXJ](https://summerofcode.withgoogle.com/programs/2023/projects/62Zo1VXJ)


# Project Abstract

<p align="center">
  <img src="https://raw.githubusercontent.com/leopardslab/nodecloud/master/assets/logo.png" >
</p>

NodeCloud is a standard library to get a single API on the open cloud with multiple providers.It is an API allowing developers to interact with multiple cloud providersusing a unified interface. This abstraction layer helps to hide the implementation details of different cloud providers, making it easier for developers to use cloud services without having to deal with the specifics of each provider.

## [GSoC Project Page](https://summerofcode.withgoogle.com/programs/2023/projects/62Zo1VXJ)

## [GSoC Project Proposal](https://drive.google.com/file/d/1g8KJ30l9h8_yVSKgdRPQdU16gGp6kn80/view?usp=sharing)

## [GitHub Organization Repo](https://github.com/leopardslab/nodecloud)

## [GitHub Personal Repo](https://github.com/partik03/nodecloud)

## [Commits during GSoC 2023](https://github.com/leopardslab/nodecloud/commits?author=partik03)

## [Project Demo Video](https://www.youtube.com/watch?v=hDJWL7q4k98)

## [Project Tracker During GSoC](https://www.notion.so/GSoC-23-Progress-Report-aba8972a06b94641aec7c4524dfd89ee)

## GSoC Blog
- Week 0 & 1 Blog : [https://medium.com/@partikbumrah13508/the-community-bonding-period-and-week-1-google-summer-of-code23-score-lab-a068ed615109](https://medium.com/@partikbumrah13508/the-community-bonding-period-and-week-1-google-summer-of-code23-score-lab-a068ed615109)
- Week 2 & 3 Blog : [https://medium.com/@partikbumrah13508/coding-week-2-and-3-gsoc-23-with-score-lab-99dd9d123c48](https://medium.com/@partikbumrah13508/coding-week-2-and-3-gsoc-23-with-score-lab-99dd9d123c48)
- Week 4 & 5 Blog : [https://medium.com/@partikbumrah13508/coding-week-4-and-5-gsoc-23-with-score-lab-74e6f2d2d203](https://medium.com/@partikbumrah13508/coding-week-4-and-5-gsoc-23-with-score-lab-74e6f2d2d203)
- Week 6 & 7 Blog : [https://medium.com/@partikbumrah13508/coding-week-6and-7-gsoc-23-with-score-lab-3fd543d49c64](https://medium.com/@partikbumrah13508/coding-week-6and-7-gsoc-23-with-score-lab-3fd543d49c64)
- Week 8 & 9 Blog : [https://medium.com/@partikbumrah13508/coding-week-8-and-9-gsoc-23-with-score-lab-a2b4ede6aa32](https://medium.com/@partikbumrah13508/coding-week-8-and-9-gsoc-23-with-score-lab-a2b4ede6aa32)
- Week 10 Blog: [https://medium.com/@partikbumrah13508/coding-week-10-gsoc-23-with-score-lab-82e9f321ca03](https://medium.com/@partikbumrah13508/coding-week-10-gsoc-23-with-score-lab-82e9f321ca03)

# Work Summary

The current implementation of NodeCloud is a core library that supports AWS, Azure, GCP and DigitalOcean cloud services as extensible plugins. I worked on extending this plugin functionality built into NodeCloud to include other cloud providers like Oracle and Linode.The project included the implementation of a code generation module to consume the SDK and auto-generate service implementations that can be assembled as the "oracle-plugin" and "linod-plugin" for NodeCloud integration. This is achieved by writing out parsers, generators and transformers specifically made for the SDKs of both cloud providers.

# What Covered

- Added function for saving generated class files to their specific folders
- Created a Parser for the Linode code generation module
- Created a Parser for the Oracle code generation module
- Created a Generator for the Linode code generation module
- Created a Generator for the Oracle code generation module
- Created a transformer for the Linode code generation module
- Created a transformer for the Oracle code generation module
- Performed unit testing for the code generation modules
- Updated the generator config file with sutaible Oracle and Linode Services
- Finalized the plugin for the Linode and Oracle Provider
- Improved documentation explaining the Directory Structure, flow of tool and details of Oracle and Linode
- Wrote Examples for implemented Linode and Oracle Services for Nodecloud

### Issues Created
- Add Dummy Classes for Linode  (#**[162](https://github.com/leopardslab/nodecloud/issues/162)**)
- Add dummy classes for Oracle (#[163](https://github.com/leopardslab/nodecloud/issues/163)) 
- Implement SDK Parser for Oracle (#[164](https://github.com/leopardslab/nodecloud/issues/164))
- Implement SDK Parser for Linode (#[165](https://github.com/leopardslab/nodecloud/issues/165))
- Implement Data Extractor functions for Oracle (#[166](https://github.com/leopardslab/nodecloud/issues/166))
- Implement the Data Extractor functions for Linode (#[167](https://github.com/leopardslab/nodecloud/issues/167))
- Implement Transformer for Oracle cloud provider (#[168](https://github.com/leopardslab/nodecloud/issues/168))
- Implement Transformer for Linode (#[169](https://github.com/leopardslab/nodecloud/issues/169))
- Add unit tests for Oracle (#[179](https://github.com/leopardslab/nodecloud/issues/179))
- Add unit tests for Linode (#[178](https://github.com/leopardslab/nodecloud/issues/178))

### Pull Requests 


|Title                      |Linked Issue                                       |Link                                             |
|---------------------------|---------------------------------------------------|-------------------------------------------------|
|Oracle dummy class         |https://github.com/leopardslab/nodecloud/issues/163|https://github.com/leopardslab/nodecloud/pull/170|
|Linode Dummy Class         |https://github.com/leopardslab/nodecloud/issues/162|https://github.com/leopardslab/nodecloud/pull/171|
|Linode SDK parser          |https://github.com/leopardslab/nodecloud/issues/165|https://github.com/leopardslab/nodecloud/pull/172|
|Linode Data Extractor      |https://github.com/leopardslab/nodecloud/issues/167|https://github.com/leopardslab/nodecloud/pull/175|
|Oracle Parser              |https://github.com/leopardslab/nodecloud/issues/164|https://github.com/leopardslab/nodecloud/pull/173|
|Oracle Data Extractor      |https://github.com/leopardslab/nodecloud/issues/166|https://github.com/leopardslab/nodecloud/pull/174|
|Oracle Transformer         |https://github.com/leopardslab/nodecloud/issues/168|https://github.com/leopardslab/nodecloud/pull/176|
|Linode Transformer         |https://github.com/leopardslab/nodecloud/issues/169|https://github.com/leopardslab/nodecloud/pull/177|
|Oracle unit tests          |https://github.com/leopardslab/nodecloud/issues/179|https://github.com/leopardslab/nodecloud/pull/181|
|Linode unit tests          |https://github.com/leopardslab/nodecloud/issues/178|https://github.com/leopardslab/nodecloud/pull/180|
|Linode Package             |                    -                              |https://github.com/leopardslab/nodecloud/pull/182|
|Oracle Package             |                    -                              |https://github.com/leopardslab/nodecloud/pull/183|
|Final Changes and Docs     |                    -                              |https://github.com/leopardslab/nodecloud/pull/189|

# What left

# References

- [https://github.com/oracle/oci-typescript-sdk/tree/master/lib](https://github.com/oracle/oci-typescript-sdk/tree/master/lib)
- [https://docs.oracle.com/en-us/iaas/Content/services.html](https://docs.oracle.com/en-us/iaas/Content/services.html)
- [https://docs.oracle.com/en-us/iaas/api/#/](https://docs.oracle.com/en-us/iaas/api/#/)
- [https://www.linode.com/docs/api/](https://www.linode.com/docs/api/)
- [https://github.com/linode/manager/tree/develop/packages/api-v4](https://github.com/linode/manager/tree/develop/packages/api-v4)
- [https://developers.linode.com/libraries-tools/](https://developers.linode.com/libraries-tools/)