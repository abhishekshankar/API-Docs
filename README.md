**Wise Platform API Docs**
----
  API Docs for image moderation use case.


**POST** [http://api.gowise.co/v1/jobs/:id/tasks](http://api.gowise.co/v1/jobs/:id/tasks)

**HEADER**: 

* Authorization: Basic APIKEY
* Content-Type: application/json

**BODY**:

```
{
  "data": {
    "image_url": "link_to_image",
    "gender": "male"|"female"
  },
  "meta": "Any valid JSON object containing metadata",
  "callback_url": "custom_url"
}
```
**RESPONSE**:

```
{
  "id": "uuid",
  "message": "Task Accepted"
}
```

**CALLBACK PAYLOAD**:

POST request made to the callback_url once the task is completed

```
{ 
  "id": "uuid",
  "decision": "approve"|"decline"|"escalate"
}  
```
---
**EXAMPLE CALLS**:

**Basic:**

```bash
curl -X POST -u APIKEY: -H "Content-Type: application/json" -d '{
  "data": {
    "image_url": "url"
  },
  "callback_url": "http://mycompany.com"
}' 'http://api-sandbox.gowise.co/v1/jobs/2/tasks'
```

**With Metadata:**

Any valid JSON metadata can be passed to train our machine learning models that help aid human workers

```bash
curl -X POST -u APIKEY: -H "Content-Type: application/json" -d '{
  "data": {
    "image_url": "url"
  },
  "meta": {
    "follower_count": 10,
    "following_count": 50,
    "karma": 15
  },
  "callback_url": "http://mycompany.com"
}' 'http://api-sandbox.gowise.co/v1/jobs/2/tasks'
```
