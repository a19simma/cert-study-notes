# [Message-Based Solutions](https://learn.microsoft.com/en-us/training/paths/az-204-develop-message-based-solutions/) 

# [Message Queues](https://learn.microsoft.com/en-us/training/modules/discover-azure-message-queue/)
Service Bus has two core messaging capabilities:
- Queues, provide FIFO guarantees to one or more competing consumers. Receiving messages can have two modes:
  - Receive and delete, upon a consumer request, Service bus marks the message as deleted and returns it. This can leave
  a message unprocessed if the client crashes before completing the job.
  - Peek Lock, request the next message and locks it. Upon a completion confirmation, Service Bus marks it as consumed.

- Topics and Subscriptions, are a one to many form of messaging where multiple consumers subscribe to a topic and all
consumers receive a copy of each message. 

Create Namespace:
```bash
az servicebus namespace create \
    --resource-group az204-svcbus-rg \
    --name $myNameSpaceName \
    --location $myLocation
```

Create Queue:
```bash
az servicebus queue create --resource-group az204-svcbus-rg \
    --namespace-name $myNameSpaceName \
    --name az204-queue
```

Queue Storage is for storing large number of messages for a longer time. Up to the limit of a storage account.
