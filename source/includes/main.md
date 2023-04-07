# Introduction

Welcome to the lukaz API! You can use our API to access lukaz endpoints.

We have a client available in JavaScript. You can view code examples in the right side.

You can install lukaz with the following command:

`npm i @lukaz/client`



# Authentication


## Authenticate User

> Send a valid API key in the Authorization header for every request:

```bash
curl "https://luk.az/getUser"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from 'lukaz'

const lukaz = new client('<LUKAZ_API_KEY>')
```

> Make sure to replace `<LUKAZ_API_KEY>` with your API key.

lukaz uses API keys to allow access to the API. You can create a new API key on the [settings](https://lukaz.ai/settings) page under security options.

lukaz expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: <LUKAZ_API_KEY>`




## Get Authenticated User

```bash
curl "https://luk.az/getUser"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const user = await lukaz.getUser()
```

> HTTP Response Body:

```json
{
  "displayName": "Example User",
  "email": "user@example.com",
  "photoURL": "https://example.com/User_Photo.jpg",
  "quota": {
    "questions": 1000,
    "workspaces": 10
  },
  "savedQuestions": ["questionId", "anotherQuestionId"],
  "usage": {
    "questions": 834,
    "workspaces": 7
  }
}
```

This endpoint reads the user data related to the API key in use.

### HTTP Request

`GET https://luk.az/getUser`




# Workspaces


## Get All Workspaces

```bash
curl "https://luk.az/getWorkspaces"
  -H "Authorization: <LUKAZ_API_KEY>"
  
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const workspaces = await lukaz.getWorkspaces()
```

> HTTP Response Body:

```json
[
  {
    "id": "<WORKSPACE_ID>",
    "createdAt": "Timestamp",
    "description": "This my AI workspace on lukaz.",
    "documents": [
      {
        "createdAt": "Timestamp",
        "extension": "pdf",
        "name": "File_Name.pdf",
        "processed": true,
        "updatedAt": "Timestamp",
        "workspaceId": "<WORKSPACE_ID>"
      }
    ],
    "email": "owner@example.com",
    "options": {
      "ask": true,
      "free": false,
      "public": false,
      "upload": true
    },
    "processing": false,
    "processedAt": "Timestamp",
    "roles": {
      "owner@example.com": 5,
      "user@example.com": 4
    },
    "stats": {
      "answers": 5,
      "docs": 2,
      "questions": 7
    },
    "updatedAt": "Timestamp"
  }
]
```

This endpoint retrieves all workspaces that the authenticated user owns or has access to.

### HTTP Request

`GET https://luk.az/getWorkspaces`




## Get a Specific Workspace

```bash
curl "https://luk.az/workspace/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const workspace = await lukaz.getWorkspace('<WORKSPACE_ID>')
```

> HTTP Response Body:

```json
{
  "id": "<WORKSPACE_ID>",
  "createdAt": "Timestamp",
  "description": "This is my AI workspace on lukaz.",
  "documents": [
    {
      "createdAt": "Timestamp",
      "extension": "pdf",
      "name": "File_Name.pdf",
      "processed": true,
      "updatedAt": "Timestamp",
      "workspaceId": "<WORKSPACE_ID>"
    }
  ],
  "email": "owner@example.com",
  "options": {
    "ask": true,
    "free": false,
    "public": false,
    "upload": true
  },
  "processing": false,
  "processedAt": "Timestamp",
  "roles": {
    "owner@example.com": 5,
    "user@example.com": 4
  },
  "stats": {
    "answers": 5,
    "docs": 2,
    "questions": 7
  },
  "updatedAt": "Timestamp"
}
```

This endpoint retrieves a specific workspace.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to retrieve

### HTTP Request

`GET https://luk.az/getWorkspace/<WORKSPACE_ID>`




## Create New Workspace

```bash
curl "https://luk.az/createWorkspace/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
  -d '{"description": "Nice workspace description"}'
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
await lukaz.workspace('<WORKSPACE_ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint creates a new workspace.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to create

### HTTP Request

`POST https://luk.az/createWorkspace/<WORKSPACE_ID>`




## Update Workspace

```bash
curl "https://luk.az/updateWorkspace/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
  -d '{"options": {"ask": false, "upload": false}
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
await lukaz.updateWorkspace('<WORKSPACE_ID>', {
    description: 'New description of my AI workspace.',
    options: {
        ask: true,
        free: false,
        public: false,
        upload: true
    },
    roles: {
        'owner@example.com': 5,
        'user@example.com': 4
    }
})
```

> HTTP Response Body:

```json
true
```

This endpoint updates a specific workspace.

### HTTP Request

`PUT https://luk.az/updateWorkspace/<WORKSPACE_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to update

### HTTP Request Body

Property    | Description
---------   | -----------
description | The descripton of the workspace
notify      | Send invite email for new user roles
options     | Workspace options
roles       | User roles





## Delete Workspace

```bash
curl "https://luk.az/deleteWorkspace/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
await lukaz.deleteWorkspace('<WORKSPACE_ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint deletes a specific workspace.

### HTTP Request

`DELETE https://luk.az/deleteWorkspace/<WORKSPACE_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to delete





## Upload File onto Workspace

```bash
curl "https://luk.az/upload/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
  -d "{'fileName': fileName}"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const workspace = await lukaz.upload('<WORKSPACE_ID>', {
    file: File,
})
```

> HTTP Response Body:

```json
true
```

This endpoint uploads a file onto a specific workspace.

### HTTP Request

`POST https://luk.az/upload/<WORKSPACE_ID>`


### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to upload the file





## Delete File from Workspace

```bash
curl "https://luk.az/deleteFile/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const workspace = await lukaz.deleteFile('<WORKSPACE_ID>', {
    fileName: 'Test_File.pdf',
})
```

> HTTP Response Body:

```json
true
```

This endpoint deletes a file from a specific workspace.

### HTTP Request

`PUT https://luk.az/deleteFile/<WORKSPACE_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to delete the file from

### HTTP Request Body

Property    | Description
---------   | -----------
fileName    | The name of the file to be deleted





# Questions



## Get Question Transcript

```bash
curl "https://luk.az/getTranscript/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const workspace = await lukaz.deleteFile('<WORKSPACE_ID>', {
    audioUrl: 'https://example.com/Audio_File.wav',
})
```

> HTTP Response Body:

```json
"This is the text from the audio file."
```
This endpoint transcripts the text from an audio file.

### HTTP Request

`POST https://luk.az/getTranscript/<WORKSPACE_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to ask a questionn

### HTTP Request Body

Property    | Description
---------   | -----------
audioUrl    | The URL of an .wav audio file

### HTTP Response Body

Property    | Description
---------   | -----------
transcript  | The text extracted from the audio file





## Ask Question to Workspace

```bash
curl "https://luk.az/ask/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const answer = await lukaz.ask('<WORKSPACE_ID>', {
    question: 'What is this workspace about?',
    translateAnswer: false
})
```

> HTTP Response Body:

```json
{
  "answer": "This workspace is about AI.",
  "question": "What is this workspace about?",
  "questionId": "<QUESTION_ID>",
  "sensitive": false
}
```

This endpoint asks a question to a specific workspace.

### HTTP Request

`POST https://luk.az/ask/<WORKSPACE_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to ask a questionn

### HTTP Request Body

Property         | Description
---------        | -----------
question         | The natural question to ask
translateAnswer  | Answer language should be same as question

### HTTP Response Body

Property    | Description
---------   | -----------
answer      | The answer generate for the question asked
question    | The question asked to the workspace
questionId  | The unique id of the question asked
sensitive   | If question context is sensitive or not





## Get Answer Audio

```bash
curl "https://luk.az/getAudio/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const audioUrl = await lukaz.getAudio('<QUESTION_ID>')
```

> HTTP Response Body:

```json
"https://example.com/Answer_Audio.mp3"
```

This endpoint generates an audio file from the answer.

### HTTP Request

`POST https://luk.az/getAudio/<QUESTION_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to generate the audio

### HTTP Request Body

The request body must be empty.

### HTTP Response Body

Property    | Description
---------   | -----------
audioUrl    | The file URL of the generated audio




## Get All Questions

```bash
curl "https://luk.az/questions"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const questions = await lukaz.getQuestions()
```

> HTTP Response Body:

```json
[
  {
    "answer": "This is workspace is about AI.",
    "audioUrl": "https://example.com/Answer_Audio.mp3",
    "createdAt": "Timestamp",
    "feedback": 0,
    "id": "<QUESTION_ID>",
    "question": "What is this workspace about?",
    "sensitive": false,
    "updatedAt": "Timestamp",
    "visible": true,
    "workspaceId": "<WORKSPACE_ID>"
  }
]
```

This endpoint retrieves all user questions of a specific workspace.

### HTTP Request

`GET https://luk.az/getQuestions`

### Query Parameters

There are no query params available at the moment.




## Get a Specific Question

```bash
curl "https://luk.az/getQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
const question = await lukaz.getQuestion('<QUESTION_ID>')
```

> HTTP Response Body:

```json
{
  "answer": "This is workspace is about AI.",
  "audioUrl": "https://example.com/Answer_Audio.mp3",
  "createdAt": "Timestamp",
  "feedback": 0,
  "id": "<QUESTION_ID>",
  "question": "What is this workspace about?",
  "sensitive": false,
  "updatedAt": "Timestamp",
  "visible": true,
  "workspaceId": "<WORKSPACE_ID>"
}
```

This endpoint retrieves a specific question.

### HTTP Request

`GET https://luk.az/getQuestion/<QUESTION_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to retrieve




## Make Question Visible

```bash
curl "https://luk.az/showQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
await lukaz.showQuestion('<QUESTION_ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint makes a specific question visible on its workspace.

### HTTP Request

`PUT https://luk.az/showQuestion/<QUESTION_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to make visible




## Make Question Invisible

```bash
curl "https://luk.az/hideQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
await lukaz.showQuestion('<QUESTION_ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint makes a specific question invisible on its workspace.

### HTTP Request

`PUT https://luk.az/hideQuestion/<QUESTION_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to make invisible





## Save Question to Favourites

```bash
curl "https://luk.az/saveQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
await lukaz.saveQuestion('<QUESTION_ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint saves a specific question as favourite.

### HTTP Request

`PUT https://luk.az/saveQuestion/<QUESTION_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to save in favourites list





## Remove Question from Favourites

```bash
curl "https://luk.az/removeQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
await lukaz.removeQuestion('<QUESTION_ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint removes a specific question from favourites.

### HTTP Request

`PUT https://luk.az/removeQuestion/<QUESTION_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to remove from favourites list






## Rate Question Answer

```bash
curl "https://luk.az/rateAnswer/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<LUKAZ_API_KEY>')
await lukaz.rateAnswer('<QUESTION_ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint rates the answer of a specific question.

### HTTP Request

`PUT https://luk.az/rateAnswer/<QUESTION_ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to rate
