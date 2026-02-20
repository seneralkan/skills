# SQS/SNS Producer/Consumer (Go)

## Producer
- Use SNS for fan-out, SQS for buffering and decoupling.
- Prefer FIFO queues when strict ordering/dedup is required.
- Set message group id and deduplication id for FIFO flows.

## Consumer
- Set visibility timeout larger than max processing time.
- Extend visibility for long-running handlers.
- Use long polling to reduce empty receives.
- Delete message only after successful processing.

## Failure handling
- Configure redrive policy to DLQ with max receive count.
- Include attempt count and last error in message attributes when republishing.
- Build replay worker to move verified DLQ messages back safely.
