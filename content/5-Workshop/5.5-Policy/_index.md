---
title: "Access the application and test"
date: "2025-12-09"
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

## Access the application and test the API using Postman

After the deployment succeeds, Elastic Beanstalk provides a URL in the format:

```bash
http://<environment-id>.<region>.elasticbeanstalk.com
```

![Example](/images/2-Proposal/domain.jpg)

Use this URL to send requests from Postman to the Spring Boot API.

Example:

```bash
GET http://<env>.elasticbeanstalk.com/api/hello
```

![Example](/images/2-Proposal/postman.jpg)

If the API responds with the expected data, the deployment is considered successful.
