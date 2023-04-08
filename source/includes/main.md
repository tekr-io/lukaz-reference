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
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from 'lukaz'

const lukaz = new client('<API_KEY>')
```

> Make sure to replace `<API_KEY>` with your API key.


<aside>
lukaz uses API keys to allow access to the API. You can create a new API key on the <a href="https://lukaz.ai/settings" target="_blank">settings</a> page under security options.
</aside>

lukaz expects for the API key to be included in all API requests to the server in a header that looks like the following:

`x-api-key: <API_KEY>`




## Get Authenticated User

```bash
curl "https://luk.az/getUser"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const user = await lukaz.getUser()
```

> HTTP Response Body:

```json
{
  "displayName": "Example User",
  "email": "user@example.com",
  "photoURL": "https://example.com/Photo.jpg",
  "quota": {
    "questions": 1000,
    "workspaces": 10
  },
  "savedQuestions": ["<ID>", "<ID>"],
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
  -H "x-api-key: <API_KEY>"
  
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const workspaces = await lukaz.getWorkspaces()
```

> HTTP Response Body:

```json
[
  {
    "id": "<ID>",
    "createdAt": "2023-01-01T18:10:54.376Z",
    "description": "This my AI workspace on lukaz.",
    "documents": [
      {
        "createdAt": "2023-01-01T18:10:54.376Z",
        "extension": "pdf",
        "name": "File_Name.pdf",
        "processed": true
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
    "roles": {
      "owner@example.com": 5,
      "user@example.com": 4
    },
    "stats": {
      "answers": 5,
      "docs": 2,
      "questions": 7
    },
    "updatedAt": "2023-01-01T18:10:54.376Z"
  }
]
```

This endpoint retrieves all workspaces that the authenticated user owns or has access to.

### HTTP Request

`GET https://luk.az/getWorkspaces`




## Get a Specific Workspace

```bash
curl "https://luk.az/workspace/<ID>"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const workspace = await lukaz.getWorkspace('<ID>')
```

> HTTP Response Body:

```json
{
  "id": "<ID>",
  "createdAt": "2023-01-01T18:10:54.376Z",
  "description": "This is my AI workspace on lukaz.",
  "documents": [
    {
      "createdAt": "2023-01-01T18:10:54.376Z",
      "extension": "pdf",
      "name": "File_Name.pdf",
      "processed": true
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
  "roles": {
    "owner@example.com": 5,
    "user@example.com": 4
  },
  "stats": {
    "answers": 5,
    "docs": 2,
    "questions": 7
  },
  "updatedAt": "2023-01-01T18:10:54.376Z"
}
```

This endpoint retrieves a specific workspace.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to retrieve

### HTTP Request

`GET https://luk.az/getWorkspace/<ID>`




## Create New Workspace

```bash
curl "https://luk.az/createWorkspace/<ID>"
  -H "x-api-key: <API_KEY>"
  -d '{"description": "Nice workspace description"}'
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
await lukaz.workspace('<ID>')
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

`POST https://luk.az/createWorkspace/<ID>`




## Update Workspace

```bash
curl "https://luk.az/updateWorkspace/<ID>"
  -H "x-api-key: <API_KEY>"
  -d '{"options": {"ask": false, "upload": false}'
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
await lukaz.updateWorkspace('<ID>', {
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

`PUT https://luk.az/updateWorkspace/<ID>`

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
curl "https://luk.az/deleteWorkspace/<ID>"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
await lukaz.deleteWorkspace('<ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint deletes a specific workspace.

### HTTP Request

`DELETE https://luk.az/deleteWorkspace/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to delete





## Upload File onto Workspace

```bash
curl "https://luk.az/upload/<ID>"
  -H "x-api-key: <API_KEY>"
  -d '{"file": "<FILE_BLOB>"}'
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const workspace = await lukaz.upload('<ID>', {
    file: File,
})
```

> HTTP Response Body:

```json
true
```

This endpoint uploads a file onto a workspace.

### HTTP Request

`POST https://luk.az/upload/<ID>`


### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to upload the file





## Delete File from Workspace

```bash
curl "https://luk.az/deleteFile/<ID>"
  -H "x-api-key: <API_KEY>"
  -d '{"fileName": "<FILE_NAME>"}'
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const workspace = await lukaz.deleteFile('<ID>', {
    fileName: '<FILE_NAME>',
})
```

> HTTP Response Body:

```json
true
```

This endpoint deletes a file from a workspace.

### HTTP Request

`PUT https://luk.az/deleteFile/<ID>`

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
curl "https://luk.az/getTranscript/<ID>"
  -H "x-api-key: <API_KEY>"
  -d '{"audioUrl": "https://example.com/Audio.wav"}'
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const workspace = await lukaz.getTranscript('<ID>', {
    audioUrl: 'https://example.com/Audio.wav',
})
```

> HTTP Response Body:

```json
{
  "transcript": "This is the text from the audio file."
}
```
This endpoint transcripts the text from an audio file.

### HTTP Request

`POST https://luk.az/getTranscript/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to ask a questionn

### HTTP Request Body

Property    | Description
---------   | -----------
audioUrl    | The URL of a .wav audio file

### HTTP Response Body

Property    | Description
---------   | -----------
transcript  | The text extracted from the audio file





## Ask Question to Workspace

```bash
curl "https://luk.az/ask/<ID>"
  -H "x-api-key: <API_KEY>"
  -d '{"question": "What is this workspace about?"}'
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const answer = await lukaz.ask('<ID>', {
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

This endpoint asks a question to a workspace.

### HTTP Request

`POST https://luk.az/ask/<ID>`

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
questionId  | The unique ID of the question asked
sensitive   | If question context is sensitive or not





## Get Answer Audio

```bash
curl "https://luk.az/getAudio/<ID>"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const audioUrl = await lukaz.getAudio('<ID>')
```

> HTTP Response Body:

```json
{
  "audioUrl": "https://example.com/Audio.mp3"
}
```

This endpoint generates an audio file from the answer.

### HTTP Request

`POST https://luk.az/getAudio/<ID>`

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
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const questions = await lukaz.getQuestions()
```

> HTTP Response Body:

```json
[
  {
    "answer": "This is workspace is about AI.",
    "audioUrl": "https://example.com/Audio.mp3",
    "createdAt": "2023-01-01T18:10:54.376Z",
    "feedback": 0,
    "id": "<ID>",
    "question": "What is this workspace about?",
    "sensitive": false,
    "updatedAt": "2023-01-01T18:10:54.376Z",
    "visible": true,
    "workspaceId": "<WORKSPACE_ID>"
  }
]
```

This endpoint retrieves all user questions of a specific workspace.

### HTTP Request

`GET https://luk.az/getQuestions`




## Get a Specific Question

```bash
curl "https://luk.az/getQuestion/<ID>"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
const question = await lukaz.getQuestion('<ID>')
```

> HTTP Response Body:

```json
{
  "answer": "This is workspace is about AI.",
  "audioUrl": "https://example.com/Audio.mp3",
  "createdAt": "2023-01-01T18:10:54.376Z",
  "feedback": 0,
  "id": "<ID>",
  "question": "What is this workspace about?",
  "sensitive": false,
  "updatedAt": "2023-01-01T18:10:54.376Z",
  "visible": true,
  "workspaceId": "<WORKSPACE_ID>"
}
```

This endpoint retrieves a specific question.

### HTTP Request

`GET https://luk.az/getQuestion/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to retrieve




## Make Question Visible

```bash
curl "https://luk.az/showQuestion/<ID>"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
await lukaz.showQuestion('<ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint makes a question visible on its workspace.

### HTTP Request

`PUT https://luk.az/showQuestion/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to make visible




## Make Question Invisible

```bash
curl "https://luk.az/hideQuestion/<ID>"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
await lukaz.showQuestion('<ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint makes a question invisible on its workspace.

### HTTP Request

`PUT https://luk.az/hideQuestion/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to make invisible





## Save Question to Favourites

```bash
curl "https://luk.az/saveQuestion/<ID>"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
await lukaz.saveQuestion('<ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint saves a question on user's favourites.

### HTTP Request

`PUT https://luk.az/saveQuestion/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to save





## Remove Question from Favourites

```bash
curl "https://luk.az/removeQuestion/<ID>"
  -H "x-api-key: <API_KEY>"
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
await lukaz.removeQuestion('<ID>')
```

> HTTP Response Body:

```json
true
```

This endpoint removes a question from user's favourites.

### HTTP Request

`PUT https://luk.az/removeQuestion/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to remove






## Rate Answer

```bash
curl "https://luk.az/rateAnswer/<ID>"
  -H "x-api-key: <API_KEY>"
  -d '{"feedback": 1}'
```

```javascript
import {lukaz as client} from '@lukaz/client'

const lukaz = new client('<API_KEY>')
await lukaz.rateAnswer('<ID>', {
    feedback: 1
})
```

> HTTP Response Body:

```json
true
```

This endpoint rates the answer of a specific question.

### HTTP Request

`PUT https://luk.az/rateAnswer/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to rate
