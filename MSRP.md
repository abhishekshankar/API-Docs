**Wise Platform API Docs**
----
  API Docs for MSRP Shopping comparison use case.


**POST** [http://api-sandbox.gowise.co/v1/jobs/:id/tasks](http://api-sandbox.gowise.co/v1/jobs/:id/tasks)

**HEADER**: 

* Authorization: Basic APIKEY
* Content-Type: application/json

**BODY**:

```
{
  "data": {
  	"product_id": product_id,
    "image_urls": [
      "link_to_image_1",
      "link_to_image_2"
    ],
    "name": "product_name",
    "brand": "product_brand",
    "description": "description",
    "material": "material",
    "size": "size",
    "color": "color",
    "msrp": msrp_price,
    "discount_price": discount_price,
  },
  "callback_url": "custom_url"
}
```
Note: You may add arbitrary keys and values within the "data" key. Values can be any valid JSON object (number, bool, string, object, array, etc)

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
  "found": true|false,
  "item_url": "link_to_store_selling_item",
  "screenshot_url": "link_to_screenshot_url",
  "msrp": found_msrp_price,
  "comments": "comments"
}  
```
---
**EXAMPLE CALLS**:

**Request:**

*Please replace with your provided APIKEY and POST endpoint before sending the reqeuest.*
*Making a request to the sandbox server will creates a callback with randomized values.*

```bash
curl -X POST -u APIKEY: -H "Content-Type: application/json" -d '{
  "data": {
  	"product_id": 1128127008,
    "image_urls": [
      "http://cdn5.giltcdn.com/images/share/uploads/0000/0005/0405/504058496/420x560.jpg"
    ],
    "name": "Lace Cocktail Dress",
    "brand": "aidan mattox",
    "description": "Lace dress<br>* Crewneck and V-back<br>* Fitted bodice<br>* Even hem<br>* Tonal top stitching and panel seaming <br>* Hidden back zipper closure <br>* Fully lined <br><b>",
    "material": "55% polyester and 45% cotton shell; 96% polyester and 4% elastane combo",
    "size": "medium",
    "color": "black",
    "msrp": 375,
    "discount_price": 375
  },
  "callback_url": "http://mycompany.com"
}' 'http://api-sandbox.gowise.co/v1/jobs/18/tasks'
```

**Response**:

```
{
  "id": "e2a73239-dbc6-495b-b57e-76bfe9b0f9ca",
  "message": "Task Accepted"
}
```

**Callback (If Item Not Found):**

```
{ 
  "id": "e2a73239-dbc6-495b-b57e-76bfe9b0f9ca",
  "found": false
}  
```

**Callback (If Item Found):**

```
{ 
  "id": "e2a73239-dbc6-495b-b57e-76bfe9b0f9ca",
  "found": true,
  "item_url": "http://www.saksfifthavenue.com/main/ProductDetail.jsp?PRODUCT%3C%3Eprd_id=845524446837077",
  "screenshot_url": "http://i.imgur.com/dLui22V.png",
  "msrp": 375
}
```