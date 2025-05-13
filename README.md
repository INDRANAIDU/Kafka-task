# Kafka-task
# 📨 Kafka Real-Time Notification System

## ⚙️ Kafka Task – Step-by-Step Setup

### 🔍 Visualizing Kafka’s Event Streaming Architecture

Start all required services using Docker:

```bash
docker-compose up -d

🚀 Let's Test the Real-Time Notification System 👨‍🔬🖥️👩‍🔬
1️⃣ Start the Producer
Open a terminal and run:
go run cmd/producer/producer.go

2️⃣ Start the Consumer
In a second terminal:
go run cmd/consumer/consumer.go

3️⃣ Sending Notifications
🟢 Method 1: Using Postman
Set Method: POST

URL: http://localhost:8080/send

Body: Choose x-www-form-urlencoded

Add the following one at a time as key-value pairs:

fromID	toID	message
2	1	Bruno started following you.
1	2	Emma mentioned you in a comment: 'Great seeing you yesterday, @Bruno!'
4	1	Lena liked your post: 'My weekend getaway!'
3	4	Hello Lena
4	3	Hello from Rick!

👉 Make sure to click Send after each entry. Each request must be sent separately.

🟠 Method 2: Using cURL

# Bruno to Emma
curl -X POST http://localhost:8080/send \
-d "fromID=2&toID=1&message=Bruno started following you."

# Emma to Bruno
curl -X POST http://localhost:8080/send \
-d "fromID=1&toID=2&message=Emma mentioned you in a comment: 'Great seeing you yesterday, @Bruno!'"

# Lena to Emma
curl -X POST http://localhost:8080/send \
-d "fromID=4&toID=1&message=Lena liked your post: 'My weekend getaway!'"

# Rick to Lena
curl -X POST http://localhost:8080/send \
-d "fromID=3&toID=4&message=Hello Lena"

# Lena to Rick
curl -X POST http://localhost:8080/send \
-d "fromID=4&toID=3&message=Hello from Rick!"


4️⃣ Retrieving Notifications
You can fetch notifications by User ID.

🟢 Postman Method
Set Method: GET

URL: http://localhost:8081/notifications/{userID}

Example: http://localhost:8081/notifications/1

🟠 cURL Method
curl http://localhost:8081/notifications/1

Example Output:

json

{
  "notifications": [
    {
      "from": { "id": 2, "name": "Bruno" },
      "to": { "id": 1, "name": "Emma" },
      "message": "Bruno started following you."
    },
    {
      "from": { "id": 4, "name": "Lena" },
      "to": { "id": 1, "name": "Emma" },
      "message": "Lena liked your post: 'My weekend getaway!'"
    }
  ]
}
