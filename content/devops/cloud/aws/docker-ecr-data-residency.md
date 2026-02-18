---
title: Docker, ECR, and Data Residency
---

Note: Every word of this article is written by a human and there is no AI involved in this process.

I have been working with Docker and Elastic Container Registry (ECR) of AWS from a very long time and I missed one of the limitations of ECR until now. I tried to make a lambda function in one region to pull a docker image from ECR in another region. How dumb was I? Let me explain what lead me to this dumb mistake.

Every company goes through several stage in it's lifecycle. Some die as a startup, some survive to become big companies. Testlify (where I work) is in that transition phase from a startup to a big company. As we are growing, we are seeing customers from across the globe. And, one of the main challenges of having customers so wide spread is strict data residency. Especially, for SaaS B2B products like Testlify.

When we decided that we support data residency with multiple regions, we had to implement it for some key regions so fast that we had to make some compromises. One of those compromises was to not utilize Infrastructure as Code (IaC). It was those days when Claude Opus 4.5 was not released yet, so can't completely blame the decision given the speed at which we had to move. We manually setup servers for multiple micro-services in multiple regions.