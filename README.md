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
  "id": "image_identifier" (optional),
  "data": {
    "image_url": "link_to_image",
    "gender": "male"|"female",
    "left": integer,
    "top": integer,
    "width": integer,
    "height": integer
  },
  "meta": "Any valid JSON object containing metadata",
  "callback_url": "custom_url"
}
```
**RESPONSE**:

```
{
  "id": "image_identifier or generated uuid",
  "message": "Task Accepted"
}
```

**RESPONSE (Duplicate ID)**:

If passing an id that is the same as the id of a previous task

```
{
  "id": "image_identifier",
  "decision": "approve"|"decline"|"escalate",
  "reason": "string" (optional)
}
```

**CALLBACK PAYLOAD**:

POST request made to the callback_url once the task is completed

```
{ 
  "id": "image_identifier or generated uuid",
  "decision": "approve"|"decline"|"escalate",
  "reason": "string" (optional)
}  
```
if decision is decline, reason will be one of the following values:

* sunglass
* no_people
* multiple_people
* nudity 
* unclear_face
* underage

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
