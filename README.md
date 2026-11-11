# Awesome Serverless Test Automation Execution

> A curated list of top Serverless Test Automation Execution platforms — both SaaS/Hosted commercial solutions and open-source alternatives for testing serverless functions, edge runtimes, and event-driven architectures.
> 🌟 Star this repo if you find it useful! 🌟

---

## 📋 Table of Contents

- [SaaS / Hosted Platforms](#-saas--hosted-platforms)
  - [Datadog Serverless Monitoring](#datadog-serverless-monitoring)
  - [BrowserStack Test Companion Cloud](#browserstack-test-companion-cloud)
  - [Lumigo](#lumigo)
  - [Thundra](#thundra)
  - [Dashbird](#dashbird)
- [Open-Source Software](#-open-source-software)
  - [Cloudflare Workers Vitest Integration](#cloudflare-workers-vitest-integration)
  - [Cloudflare createTestHarness](#cloudflare-createtestharness)
  - [aws-testing-framework](#aws-testing-framework)
  - [samstack](#samstack)
  - [LocalStack](#localstack)
- [Comparison at a Glance](#-comparison-at-a-glance)
- [Contributing](#-contributing)

---

## 🟦 SaaS / Hosted Platforms

Commercial, cloud-hosted Serverless Test Automation Execution platforms. These are not open-source but are included as reference points for feature comparison (sorted by company valuation / market cap descending).

### Datadog Serverless Monitoring
**Company Valuation / Scale:** ~$63B–$68B Market Cap (~$4B+ ARR) | **Type:** Serverless observability with AWS Lambda and Step Functions
Datadog Serverless Monitoring collects real-time metrics, logs, and traces from AWS Lambda, Azure App Service, Azure Container Apps, and Google Cloud Run [citation:7]. For AWS Lambda, enhanced metrics (`aws.lambda.enhanced`) provide second-level granularity for cold starts, estimated costs, timeouts, out-of-memory errors, and memory usage. Distributed tracing connects serverless traces to metrics, and deployment tracking correlates code changes with performance impact [citation:7]. Step Functions integration provides execution tracing with state machine paths, step inputs/outputs, and execution durations [citation:7]. **Note:** This is monitoring rather than test execution—it helps diagnose failures in deployed serverless functions, not run tests against them.

### BrowserStack Test Companion Cloud
**Company Valuation / Scale:** ~$4B Valuation (~$225M ARR) | **Type:** Cloud-hosted AI test execution for large jobs
BrowserStack Test Companion Cloud runs test automation tasks on a machine in the BrowserStack cloud rather than inside the developer's IDE. A cloud machine clones your GitHub repository, installs required tools, opens its own browser, and executes the task—splitting large jobs into parallel subtasks where possible. Results arrive as a pull request on your repository [citation:2]. **Important limitations:** It is in beta and available on request; works only in Visual Studio Code; requires a repository on github.com; and tests run on Chrome only [citation:2]. This is not a serverless-specific testing tool—it is a cloud execution environment for test automation that can be used for serverless-adjacent workflows.

### Lumigo
**Company Valuation / Scale:** ~$100M–$250M Valuation (Acquired by Dash0, $37M raised) | **Type:** Serverless observability with AI-powered troubleshooting
Lumigo provides full visibility into serverless stacks—traces, logs, metrics, and payloads—with auto-instrumentation for Lambda across Node.js, Python, Java, Go, and .NET [citation:8]. Key features include end-to-end distributed tracing, payload inspection, cold start tracking, asynchronous workflow tracing (SQS, SNS, Step Functions), and AI-powered troubleshooting via Lumigo Copilot [citation:8]. Deployment uses a CloudFormation template to provision permissions. **Note:** Like Datadog, this is observability rather than test execution, but it is commonly used to validate serverless behavior post-deployment.

### Thundra
**Company Valuation / Scale:** ~$15M–$30M Est. Valuation / Acquisition by Catchpoint ($4M+ raised) | **Type:** Serverless observability with LocalStack integration
Thundra (acquired by Catchpoint) provides monitoring and debugging for AWS Lambda functions, with support for Node.js, Python, and Java runtimes [citation:9]. A notable integration is with **LocalStack**, allowing developers to monitor and debug Lambda functions locally before deploying to AWS. You obtain a Thundra API key and add it to the Lambda function's environment variables (`THUNDRA_APIKEY`), then inspect invocations and traces in the Thundra Console [citation:9]. This LocalStack integration is particularly relevant for serverless test automation workflows where local testing is desired.

### Dashbird
**Company Valuation / Scale:** ~$5M–$15M Est. Valuation ($2.9M raised) | **Type:** Agentless serverless observability
Dashbird provides agentless serverless observability and monitoring for AWS environments, with error detection, incident management, and cost optimization insights without code-level instrumentation [citation:10]. It is designed to help DevOps teams identify issues and maintain availability for distributed serverless applications.

---

## 🟩 Open-Source Software

Self-hosted, community-driven Serverless Test Automation Execution tools. The open-source ecosystem spans **runtime-native testing frameworks** for edge/serverless platforms and **local emulation tools** for AWS serverless services.

### Cloudflare Workers Vitest Integration
**Stack:** TypeScript / Vitest | **License:** Open Source (Cloudflare Workers SDK)
Cloudflare provides a **Workers Vitest integration** for unit testing Workers functions, running tests inside the actual Workers runtime (`workerd`) so test code can access bindings and runtime APIs directly [citation:4]. It supports assertions against binding state (KV, R2, D1, Durable Objects) and direct calls to Durable Objects. This is the recommended path for fast feedback when testing individual Workers functions [citation:4]. **Important:** Miniflare, the local emulator underlying this, is not a hardened sandbox and should not be used to run untrusted code [citation:4].

### Cloudflare createTestHarness
**Stack:** TypeScript / Wrangler | **License:** Open Source (Cloudflare Workers SDK)
The **`createTestHarness()`** API provides integration testing for Cloudflare Workers, running production build output from Wrangler or the Cloudflare Vite plugin. It dispatches requests and events to one or more Workers, provides access to bindings and local storage, and captures logs and diagnostic output [citation:14]. It is compatible with any Node.js test runner and integrates with Playwright and MSW [citation:14]. This is the recommended path for integration tests that exercise Workers as a whole.

### aws-testing-framework
**Stack:** TypeScript / Node.js / AWS SDK | **License:** MIT
aws-testing-framework is an open-source BDD-style testing framework for AWS serverless applications, with a focus on **verifying actual Lambda execution** via CloudWatch logs rather than just checking deployment [citation:1]. It provides pre-built step definitions for S3, SQS, Lambda, and Step Functions, with examples like "the Lambda function should be invoked 3 times within 5 minutes" and "the Step Function execution should succeed" [citation:1]. It supports configurable timeouts, retry attempts, and environment-specific configuration (`createForDevelopment`, `createForProduction`). **Differentiator:** Real execution verification, not just resource existence checks [citation:1]. **Trade-off:** Focused on AWS serverless services; requires AWS credentials and resources to test against.

### samstack
**Stack:** Python / Docker / LocalStack | **License:** Open Source (PyPI)
samstack is a Python testing utility for local AWS serverless development, combining **SAM CLI** and **LocalStack** in Docker containers to run integration tests against S3, DynamoDB, SQS, SNS, and Lambda [citation:3]. It provides Python fixtures that wrap these services with a simple API (`bucket.delete()`, `table.put_item()`, `queue.send()`) and automatically starts LocalStack and SAM local endpoints. Configuration is via `pyproject.toml` with options for ports, images, and pre-warming Lambda functions [citation:3]. **Trade-off:** Python-centric; requires Docker; focused on local testing rather than cloud execution.

### LocalStack
**Stack:** Python / Docker | **License:** Apache-2.0 (Community)
LocalStack is a cloud service emulator that runs AWS services locally in a single Docker container, enabling offline development and testing of serverless applications without connecting to AWS [citation:9]. It supports Lambda, S3, DynamoDB, SQS, SNS, Step Functions, and many other services. It is commonly used with frameworks like samstack and integrates with Thundra for local observability [citation:9]. **Trade-off:** It is an emulator, not a test runner—you still need a testing framework (pytest, Vitest, etc.) to write and execute tests against the emulated services.

---

## 📊 Comparison at a Glance

| Software | License | Company Scale (Valuation / Revenue) | Stack | Runtime Target | Execution vs Observability | Self-Hosted | Best For |
|----------|---------|-------------------------------------|-------|----------------|---------------------------|-------------|----------|
| **Datadog Serverless** | Proprietary | ~$63B–$68B Market Cap (~$4B+ ARR) | Cloud | AWS Lambda, Azure, GCP | Observability | ❌ | Post-deployment diagnostics |
| **BrowserStack Test Companion** | Proprietary | ~$4B Valuation (~$225M ARR) | VS Code / Cloud | General test automation | Execution (cloud) | ❌ | Large AI-assisted test jobs |
| **Lumigo** | Proprietary | ~$100M–$250M Valuation ($37M raised) | Cloud | AWS Lambda | Observability | ❌ | Serverless troubleshooting + AI |
| **Thundra** | Proprietary | ~$15M–$30M Est. Valuation ($4M raised) | Cloud | AWS Lambda (LocalStack) | Observability | ❌ | Local Lambda debugging |
| **Dashbird** | Proprietary | ~$5M–$15M Est. Valuation ($2.9M raised) | Cloud | AWS serverless | Observability | ❌ | Agentless monitoring |
| **Workers Vitest** | Open Source | N/A (Cloudflare backing) | TypeScript | Cloudflare Workers | Execution (unit) | ✅ | Fast unit tests in Workers runtime |
| **createTestHarness** | Open Source | N/A (Cloudflare backing) | TypeScript | Cloudflare Workers | Execution (integration) | ✅ | Integration tests across Workers |
| **aws-testing-framework** | MIT | N/A (Open Source) | TypeScript | AWS serverless | Execution (BDD) | ✅ | Real Lambda execution verification |
| **samstack** | Open Source | N/A (Open Source) | Python | AWS (local via SAM) | Execution (local) | ✅ | Python local serverless testing |
| **LocalStack** | Apache-2.0 | ~$25M Series A ($30M+ raised) | Python/Docker | AWS emulation | Emulation | ✅ | Offline AWS service testing |

---

## 🤝 Contributing

Contributions are welcome! If you know of an open-source Serverless Test Automation Execution tool that should be listed here, please open a pull request with:

- Project name and URL
- Brief description (1–2 sentences)
- Stack and license
- Why it stands out

Please ensure the project is actively maintained (releases within the last 12 months) and genuinely open-source. Note that the open-source ecosystem **splits** between **runtime-native testing frameworks** (Cloudflare Workers Vitest, createTestHarness) that execute tests inside the serverless runtime, **AWS-specific test harnesses** (aws-testing-framework, samstack) that verify execution against real or emulated services, and **local emulators** (LocalStack) that provide the foundation for offline testing. Commercial platforms (Datadog, Lumigo, Thundra, Dashbird) are primarily **observability** tools rather than test execution engines—they help diagnose failures in deployed serverless functions but do not run tests. BrowserStack Test Companion Cloud is an execution environment for general test automation, not a serverless-specific tool [citation:2].

---

## 📄 License

This list is released under CC0 1.0 Universal (Public Domain). The software projects listed retain their respective licenses.

---

⭐ **If this list helped you discover a useful tool, please star the repo!** ⭐
