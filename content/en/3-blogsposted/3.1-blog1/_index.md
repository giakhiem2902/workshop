---
title: "Blog 1"
weight: 1
pre: "<b>3.1. </b>"
---

## Bringing AIOps to Practice: Building an AI Assistant That Automatically Analyzes AWS Health with Amazon Bedrock

![Blog 1](/images/blog/blog1.png)

The article introduces a breakthrough architecture that combines Amazon Bedrock Agents with AWS Health to create a self-service infrastructure health analytics system. This solution turns dry event logs into concrete remediation actions, solving the "alert fatigue" problem for good.

**Key takeaways:**

- The system automatically collects events from AWS Health via EventBridge and stores them centrally in a Data Lake (S3 & Athena).
- A Knowledge Base (vectorized through OpenSearch) is used to look up the company's incident runbooks/playbooks.
- Amazon Bedrock Agents act as the orchestrator, taking natural-language questions and turning them into SQL queries through Action Groups.
- RAG (Retrieval-Augmented Generation) is applied to produce accurate answers with detailed remediation steps.
- Data stays fully secure inside the AWS account and is never used to train public foundation models.

This architecture is especially useful for DevOps/SRE teams looking to shorten incident resolution time (MTTR) and democratize infrastructure-data querying for every project member.

Link: https://aws.amazon.com/vi/blogs/machine-learning/build-self-service-aws-health-analytics-to-find-actionable-health-insights-with-ai-agents-powered-by-amazon-bedrock/

**Detailed implementation guide:**

1. **Set up the ingestion pipeline**: create an Amazon EventBridge rule to automatically capture AWS Health events. Use AWS Lambda to parse the raw data and store it in Amazon S3.
2. **Configure querying**: set up Amazon Athena to query the log data stored on S3 directly.
3. **Create a Knowledge Base**: in the Amazon Bedrock console, create a Knowledge Base and point it to the S3 folder containing the internal Runbook/Playbook documents. Use Amazon OpenSearch Serverless as the vector store.
4. **Configure the Bedrock Agent**: create an Agent and define the Action Groups. Link these Action Groups to a Lambda function responsible for executing SQL queries on Athena.
5. **Integrate the frontend**: use the AWS SDK to call the Bedrock Agent Runtime API, connecting it to a web interface (e.g., an admin UI built with ReactJS) so engineers can chat directly with the system.
