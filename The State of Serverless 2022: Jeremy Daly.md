The State of Serverless 2022: Jeremy Daly

- https://www.youtube.com/watch?v=RDfqrf1B2cM

## What we're going to talk about
- How serverless has evolved over the last 7 years
- How our workflows and responsibilities have chaged
- The tools, servces, and patterns we've adopted
- The groundwork being laid for the future of modern applications

## I still get annoyed by every piece of AWS that is not serverless! ~ Wener Vogels

## Pre-Serverless Era (2006-2014)

- S3, SQS, CloudWatch, SNS, CloudFront, Route53, CloudFormation, DynamoDB, Kinesis

## The WonderYears (2015~2016)

- API Gateway, Serverless Framework, Jamestack, VPC Support for Lambda, Azure Functions, Athena, AWS SAM, Step Functions, Serverless Application Lens 

## Expansion of Use Cases (2017)

- Google Cloud Functions, GaunaDB Serverless Cloud, Architect Framework, Google Firestore(beta), AWS Amplify, AWS Fargate, AppSync, Aurora Serverless, Serverless Application Repository

## Integration and Controls (2018) 
- SQS as an event trigger, Google Cloud Run, Numbella, Lambda 15 minute timeouts, Websockets in API Gateway, Lambda Layers and Runtime API, Application Load Balancer support

## The Missing Links (2019)
- Data API, Amazon EventBridge, AWS CDK, Lambda Destinations, HTTP Apis for API gateway, RDS Proxy

## Typical serverless developer experience

## Remove the Contraints (2020)
- CockroachDB Serverless, Lambda EFS integration, Lambda Extensions, Lambda Container Image Support with 10GB container size, Lambda with 10GB of memory, Aurora Server less v2

## Know your primitives
### Serverless framework
- functions = Lambda
- events map directly to primitives
- resources define CloudFormation

### Architect
- @http = Lambda
- @queues = SQS
- @tables = DynamoDB
- @events = SNS
- @ws = API Gateway

### Cloud Develop Kit
- resouces explicitly define & configure primitives
- constructs help simplify use cases & minimize config

### Pulumi
- custom resources explicitly define & configure primitives
- component resources logically groups resource to create higher-level-abstractions

#### The develop still needs to understand and be responsible for the infrastructure configuration

## Only Three Things are infinte:
- The Universe, Human Stupidity and serverless possiblities

## Serverless develop responsibilities
- Business Logic
- Infrastructure & Cloud Architecture
- Build & Deployment Pipelines
- Monitoring & Observability
- Security & Compliance

## Configuration OVER Code
- Error handling and retry failures
- Managing failover and redundancy
- transporting (and sometimes transforming) data
- Orchestrating workflows
- Code is a liability even if it's laC

## Serverless Microservice Patterns for AWS
- The Simple Web Service
- The Strangler Pattern
- Fan-out/Fan-in Pattern

## CDKPatterns.com

## ServerlessLand.com/patterns

## Creating and Enforcing Standards

"Serverless Enablement Team"
- Codify serverless patterns and enable "day 2" pattern usage from new team members

"Platform Squad"
- Introduce and maintain standards around compliance, shared code, observability

## Combine the Primitives (2021)
- AWS App Runner, StepFunction integration with AWS SDK, Amplify Studio, Partial batch responses, Event filtering for SQS, DynamoDB and kinesis, S3 event notifications with EventBridge, SageMaker Serverless Inference, Serverless RedShift, OnDemand Kinesis, EMR Serverless, MSK Serverless, Lambda Function URLs, Lambda 10GB of Ephemeral Storage

## Post Serverless Era (2022 and beyond)

## Modern Applications

## Preconfigured infrastucture platforms

AWS App Runner
- Uses your source code or container image to automatically build and deploy your web application and load balance traffic

Nimbella (bought by Digital Ocean)
- Deploy "just code" or code packaged as containers, platform manages abstractions and provides underlying infrastructure

IBM Cloud Code Engine
- Run your container, application code or batch job on a fully managed container runtime

## Edge computing platforms
- Low-latency compute
- Globally distributed
- K/V capabilities
- Limited execution time
- Lightweight workloads(redirects, header manipulation, authentication, etc.)

- Cloudflare Workers, fastly, amazon cloudfront functions

## Jamstack meets serverless meets Edge
- SSR, SSG, ISR, etc.
- Framework detection
- Deployment management
- Serverless & Edge functions
- Integrated backends
- Extensibility

- Vercel, netlify, Cloudflare Pages, AWS Amplify

## Advancements in two fields - programming languages and cloud infrastructure - will converge in a single paradigm: where all resources required by a program will be automatically provisioned, and optimized, by the environment that runs it. - Shawn @SWYX Wang

## Self-provisioning runtimes & languages
- dark, lambdragon, cloudcompiler.run, encore, wasp-lang, serverless-cloud, nitric

## Infrastructure from Code
- ONLY write application code
- No YAML or configuration files
- Focus on USE CASES and OUTCOMES versus primitives
- Use familiar patterns to define business logic
- Automatically deploys/manages infrastructure to support the app
- Provide simple workflows for development, testing, & deployments
- Infrastructure is optizied over time based on usage

## "Modern" Architectural Patterns
- Event-driven Applications
- Orchestration/Stateful Apps
- Jamstack (evolving)
- Self-provisioning Runtimes
- Functional Web Apps

## The State of Serverless...
- Serverless has evolved tremendously over the last 7 years
- The vast majority of objections have been addressed
- There is most likely a primitive/managed service for you to use
- Configuration over code - let the cloud do the heaby lifting
- Event-driven applications(EDAs) are back with a vengeance
- Growing complexity is still a concern
