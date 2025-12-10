---
title: "Prerequiste"
date: "2025-12-09"
weight: 2
chapter: false
pre: " <b> 5.2. </b> "
---

#### Prepare and create the build file (.jar)

Before deploying to AWS, the Spring Boot application needs to be packaged into an executable `.jar` file.

In the project’s root directory, run the command:

```bash
mvn clean package -DskipTests
```

After the process completes, the built file will appear in the directory:

```bash
/target/<application-name>.jar
```

![](/images/2-Proposal/target.jpg)
