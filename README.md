# MP4-to-MP3 Converter

A Python-based event-driven microservice architecture demo that allows clients to convert their MP4 file into MP3 file. Tech stack used for this project is Python, Kubernetes, Docker, AWS, RabbitMQ, MongoDB.

## Steps

1. Client sends a HTTP request containing the MP4 video to be converted into MP3 to AWS API Gateway.
2. API Gateway stores the MP4 file in a MongoDB database.
3. API Gateway creates and places a message in RabbitMQ queue, allowing downstream services to realize the MP4 file to be processed.
4. MP3-converter services consume the message from RabbitMQ, get ID from message, pull the MP4 file from MongoDB, convert into MP3 file.
5. The MP3 files are then stored back onto MongoDB, and a new message is created in the queue.
6. Notification service consumes the conversion confirmation message and relays an email back to the client.
7. Client use the ID of the email message with personal JWTs to make an authenticated HTTP request to download the MP3 file from MongoDB.
