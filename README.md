# Image-enroll
Repository for readme and postman collection for running custom JT4 job

---
To succesfully upload the images, three input fields are required: `photo`, `user_id`, and `user_created_at`. To make requests on the Smile's APIs, 3 authentication parameters are also required: `partner_id`, `signature`, and `timestamp`. [See the docs here](https://docs.smileidentity.com/rest-api/signing-your-api-request/generate-signature) for more details on making requests.



Request Details 
---

##### Test API (sandbox)

```
POST https://testapi.smileidentity.com/v1/backfill_users
```

##### Production API
```
POST https://api.smileidentity.com/v1/backfill_users
```


This is a custom job type 4. A sample body request looks like this:
```json
{
    "partner_id": "172",
    "timestamp": "{time.now}",
    "signature": "{calculated_signature}",
    "user_id": "unique_user_id_012",
    "user_created_at": "2021-08-12",
    "photo": "/9j/base64"
}
```
 ---


##### photo
This is the photo of a user. Photos are to be transferred using Base64 binary encoding format.
> The image Upload limit is set to `5 MB`. The permitted file types to encode are `.jpg` and `.png`. Do not add data URIs to the request (eg. data:image/jpeg;base64)

`"photo":"/9j/4AAQSkZJRgABA..."`  


##### user_id
This a unique identifier that you create to track your user on Smile's Platform. Once used, the same ID cannot be used for another user. It can be in alphanumeric form.

##### user_created_at
This is the date string that indicates when the user uploaded the image or when the account was created.
The date format should be in ISO date format.

`"user_created_at":"yyyy-mm-dd hh:mm:ss-xxxx"`  

This field is designed to enable advanced fraud detection and protection for all images.


##### partner_id 
The partner ID of your organisation. This can be found on the Smile [Partner Portal](https://portal.smileidentity.com).
 `"partner_id": "172"`  

##### timestamp
This is the timestamp for the request in an ISO 8601 date format. 
`"timestamp":"yyyy-mm-dd hh:mm:ss-xxxx"`  

##### signature

To communicate with our systems we require a signature on each request to ensure that both parties are who they say they are. To calculate your signature, you will need your `partner ID` and `API Key` to calculate the `signature`, both of which are available on the Smile [portal](https://portal.smileidentity.com/api-key). Also refer to the [docs](https://docs.smileidentity.com/rest-api/signing-your-api-request/generate-signature) on generating signature.

`"signature": "6s.....tE="`

>NOTE: API Keys should be generated for their specific environments. Test API request should use the sandbox api keys and Production request should use production API Keys

Response Details
---
A success `200`, a sample response would look like this:
```json
{
    "Actions": {
        "Register_Selfie": "Approved",
        "Selfie_Check": "Passed",
        "Selfie_Provided": "Passed",
        "Human_Review_Compare": "Not Applicable",
        "Human_Review_Liveness_Check": "Not Applicable",
        "Human_Review_Selfie_Check": "Not Applicable",
        "Human_Review_Update_Selfie": "Not Applicable",
        "Liveness_Check": "Not Applicable",
        "Return_Personal_Info": "Not Applicable",
        "Selfie_To_ID_Authority_Compare": "Not Applicable",
        "Selfie_To_ID_Card_Compare": "Not Applicable",
        "Selfie_To_Registered_Selfie_Compare": "Not Applicable",
        "Update_Registered_Selfie_On_File": "Not Applicable",
        "Verify_ID_Number": "Not Applicable"
    },
    "ConfidenceValue": "99",
    "PartnerParams": {
        "job_type": 4,
        "user_id": <user_id provided as input>,
        "job_id": "d9821b53-ada3-411c-8c5c-d6ea2a95915c",
        "user_created_at": <user_created_at provided as input>
    },
    "ResultCode": "0840",
    "ResultText": "Enroll User",
    "Source": "Rest API",
    "SmileJobID": "0000021007",
    "signature": "3w4Ar1rv/nFazj4DRlDFvCcwnaf9SL3f8coYAdX+FlY=",
    "timestamp": "2023-02-14T00:07:49.924Z"
}
```





-----



## Postman Collection

How to use the attached postman collection.
Update the following:

### 1. Edit and save `environment variables`
* Check Partner ID to ensure its the same as yours. 
* generate an api_key 
* Access this by clicking the `KUDA Test`  folder and navigate to `variables`. Save once done.


### 2. Check out the `pre-request script` on the post-request
* Your timestamp and signature are already calculated here for convenience. No need to edit this.
* Access this by clicking the `testapi` request folder and navigate to `Pre-request Script` . Save once done.

### 3. Edit the `Request Body`
* This is the `raw json body`
* Edit the `user_id`, `user_created_at` and `photo` with your own request parameters.
* Access this by clicking the `testapi` request folder and navigate to `Body > raw > JSON`. 
