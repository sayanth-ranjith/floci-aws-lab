# floci-aws-lab

Hands-on AWS practice for backend devs, with no AWS account needed. A Spring Boot order service (Java 17, Spring Boot 4, AWS SDK v2) runs against [Floci](https://github.com/floci-io/floci), an open-source local AWS emulator.

## Quick start

```bash
docker compose up -d
aws configure   # any dummy values: test / test / us-east-1
aws --endpoint-url http://localhost:4566 s3 mb s3://invoices
aws --endpoint-url http://localhost:4566 s3 ls
```

All services are served at `http://localhost:4566`.

## Roadmap

| # | Feature | What it covers | Status |
|---|---------|----------------|--------|
| 1 | Setup | Floci via Docker Compose, AWS CLI, SDK clients behind a `local` profile | ⏳ |
| 2 | S3 | Upload/download invoices, list by prefix, presigned URLs | ⬜ |
| 3 | DynamoDB | `Orders` table, partition/sort keys, GSI, conditional writes | ⬜ |
| 4 | SNS + SQS | Order-placed fan-out, DLQ, idempotent consumers | ⬜ |
| 5 | Lambda | S3 upload triggers a Java Lambda | ⬜ |
| 6 | Secrets Manager / SSM / KMS | Config and credentials out of `application.yml` | ⬜ |
| 7 | Step Functions / EventBridge | Order workflow as a state machine (compare with Temporal) | ⬜ |
| 8 | Tests + IaC | Testcontainers with Floci, Terraform or CloudFormation | ⬜ |
| 9 | Real AWS (free tier) | IAM roles, VPC, one deploy to ECS/EC2, billing alarm | ⬜ |

## Notes

- Use `forcePathStyle(true)` on `S3Client` when pointing at Floci.
- Data persists in `./data` (default `hybrid` storage mode).
- Floci doesn't replace real AWS for IAM enforcement, networking, costs or the console. Step 9 covers those.
