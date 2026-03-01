# Serverlesspresso Workshop — AWS Event-Driven Serverless Architecture

Completed as part of the official [AWS Serverlesspresso Workshop](https://catalog.workshops.aws/serverlesspresso) on February 28, 2026.

---

## What I Built

A fully serverless, event-driven coffee ordering application — deployed independently on a live AWS account. Customers order from a mobile web app, the order flows through independent microservices, and the barista receives real-time notifications. No servers managed.

The deployment comprises **95 AWS resources across 14 service types**, all defined as Infrastructure as Code in the included CloudFormation template.

---

## Architecture

Three microservices communicate exclusively through **Amazon EventBridge** — no service calls another directly.

| Service | Role |
|---|---|
| Order Manager | REST API → Step Functions → DynamoDB |
| QR Validator | Validates customer session before allowing an order |
| Publisher | Pushes real-time WebSocket updates via AWS AppSync Events |

![Completed Architecture](assets/arquitectura-completa.png)

---

## AWS Services Used

`EventBridge` `Step Functions` `Lambda` `API Gateway` `DynamoDB` `AppSync` `Cognito` `SAM/CloudFormation` `SSM Parameter Store` `CloudWatch`

---

## Key Patterns Implemented

- **Event-driven architecture** — 9 active EventBridge rules routing events across all services
- **Wait-for-callback (task token)** — Step Functions pauses execution until the barista confirms the order via `SendTaskSuccess`
- **Workflow orchestration** — Two state machines managing the full order lifecycle
- **Infrastructure as Code** — 95 resources deployed from a single SAM template

---
---

## References

- [AWS Serverlesspresso Workshop](https://catalog.workshops.aws/serverlesspresso)
- [Source Repository — aws-samples/serverless-coffee-workshop](https://github.com/aws-samples/serverless-coffee-workshop)
