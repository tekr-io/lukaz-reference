# Introduction

Welcome to the lukaz API! You can use our API to access lukaz API endpoints.

We have a client available in JavaScript. You can view code examples in the dark area to the right, and you can switch the programming language of the examples with the tabs in the top right.

# Authentication

> To authorize, use this code:

```bash
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from 'lukaz'

const client = await await lukaz.authorize('<LUKAZ_API_KEY>')
```

> Make sure to replace `<LUKAZ_API_KEY>` with your API key.

lukaz uses API keys to allow access to the API. You can create a new lukaz API key at [settings](https://lukaz.ai/settings) page under security options.

lukaz expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: <LUKAZ_API_KEY>`

# Workspaces



## Get All Workspaces

```bash
curl "https://luk.az/workspaces"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const workspaces = await client.workspaces()
```

> The above endpoint returns JSON structured like this:

```json
[
  {
    "id": "<WORKSPACE_ID>",
    "createdAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
    "description": "This a workspace on lukaz!",
    "documents": [
      {
        "createdAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
        "extension": "pdf",
        "name": "File_Name.pdf",
        "processed": true,
        "updatedAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
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
    "processedAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
    "roles": {
      "owner@example.com": 5,
      "user@example.com": 4
    },
    "stats": {
      "answers": 5,
      "docs": 2,
      "questions": 7
    },
    "updatedAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
    "userEmails": ["owner@example.com", "user@example.com"]
  }
]
```

This endpoint retrieves all workspaces.

### HTTP Request

`GET https://luk.az/workspaces`

### Query Parameters

There are no query params available at the moment.




## Get a Specific Workspace

```bash
curl "https://luk.az/workspace/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.workspace('<WORKSPACE_ID>')
```

> The above endpoint returns JSON structured like this:

```json
{
  "id": "<WORKSPACE_ID>",
  "createdAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
  "description": "This is my first workspace on lukaz!",
  "documents": [
    {
      "createdAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
      "extension": "pdf",
      "name": "File_Name.pdf",
      "processed": true,
      "updatedAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
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
  "processedAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
  "roles": {
    "owner@example.com": 5,
    "user@example.com": 4
  },
  "stats": {
    "answers": 5,
    "docs": 2,
    "questions": 7
  },
  "updatedAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
  "userEmails": ["owner@example.com", "user@example.com"]
}
```

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to retrieve

This endpoint retrieves a specific workspace.

### HTTP Request (with ID)

`GET https://luk.az/workspace/<WORKSPACE_ID>`




## Create New Workspace

```bash
curl "https://luk.az/createWorkspace/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.workspace('<WORKSPACE_ID>')
```

> The above endpoint returns JSON structured like this:

```json
null
```

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to retrieve

This endpoint retrieves a specific workspace.

### HTTP Request (with ID)

`POST https://luk.az/workspace/<WORKSPACE_ID>`

## Update Existing Workspace

```bash
curl "https://luk.az/updateWorkspace/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.updateWorkspace('<WORKSPACE_ID>', {
    
})
```

> The above endpoint returns JSON structured like this:

```json
null
```

### HTTP Request (with ID)

`POST https://luk.az/workspace/<WORKSPACE_ID>`

This endpoint retrieves a specific workspace.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to retrieve

### HTTP Request Body

Property    | Description
---------   | -----------
description | (string) The descripton of the workspace
notify      | (boolean) Notify new users
options     | (object) Workspace options
roles       | (object) User roles





## Delete Existing Workspace

```bash
curl "https://luk.az/deleteWorkspace/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.deleteWorkspace('<WORKSPACE_ID>')
```

> The above endpoint returns JSON structured like this:

```json
null
```

### HTTP Request (with ID)

`DELETE https://luk.az/deleteWorkspace/<WORKSPACE_ID>`

This endpoint deletes a specific workspace.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to retrieve

This endpoint retrieves a specific workspace.





## Upload File onto Workspace

```bash
curl "https://luk.az/upload/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.upload('<WORKSPACE_ID>', {
    file: File,
})
```

> The above endpoint returns JSON structured like this:

```json
null
```

### HTTP Request (with ID)

`POST https://luk.az/upload/<WORKSPACE_ID>`


### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to upload the file

This endpoint uploads a file onto a specific workspace.

## Delete File from Workspace

```bash
curl "https://luk.az/deleteFile/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.deleteFile('<WORKSPACE_ID>', {
    fileName: 'Test_File.pdf',
})
```

> The above endpoint returns JSON structured like this:

```json
null
```

### HTTP Request (with ID)

`DELETE https://luk.az/deleteFile/<WORKSPACE_ID>`

This endpoint deletes a file from a specific workspace.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to delete the file from

### HTTP Request Body

Property    | Description
---------   | -----------
fileName    | (string) The name of the file to be deleted



# Questions



## Get Question Transcript

```bash
curl "https://luk.az/getTranscript/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.deleteFile('<WORKSPACE_ID>', {
    audioUrl: 'https://example.com/Audio_File.wav',
})
```

> The above endpoint returns JSON structured like this:

```json
"This is the text from the audio file."
```

### HTTP Request (with ID)

`POST https://luk.az/getTranscript/<WORKSPACE_ID>`

This endpoint transcripts the text from an audio file.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to ask a questionn

### HTTP Request Body

Property    | Description
---------   | -----------
audioUrl    | (string) The URL of an .wav audio file

### HTTP Response Body

Property    | Description
---------   | -----------
            | (string) The text extracted from the audio file





## Ask Question to Workspace

```bash
curl "https://luk.az/ask/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const answer = await client.ask('<WORKSPACE_ID>', {
    question: 'What is this workspace about?',
    translateAnswer: false
})
```

> The above endpoint returns JSON structured like this:

```json
{
  "answer": "This workspace is about the history of AI.",
  "question": "What is this workspace about?",
  "questionId": "01I83mudzoQWVrKMoFbx0T8XQZS2",
  "sensitive": false
}
```

### HTTP Request (with ID)

`POST https://luk.az/getTranscript/<WORKSPACE_ID>`

This endpoint asks a question to a specific workspace.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the workspace to ask a questionn

### HTTP Request Body

Property         | Description
---------        | -----------
question         | (string) The natural question to ask
translateAnswer  | (boolean) Answer language should be same as question

### HTTP Response Body

Property    | Description
---------   | -----------
answer      | (string) The answer generate for the question asked
question    | (string) The question asked to the workspace
questionId  | (string) The unique id of the question asked
sensitive   | (boolean) If question context is sensitive or not





## Get Answer Audio

```bash
curl "https://luk.az/getAudio/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const audioUrl = await client.getAudio('<QUESTION_ID>')
```

> The above endpoint returns JSON structured like this:

```json
"https://example.com/Answer_Audio_File.mp3"
```

### HTTP Request (with ID)

`POST https://luk.az/getAudio/<QUESTION_ID>`

This endpoint generates an audio file from the answer.

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to generate the audio

### HTTP Request Body

The request body must be empty.

### HTTP Response Body

Property    | Description
---------   | -----------
            | (string) The file URL of the generated audio




## Get All Questions

```bash
curl "https://luk.az/questions"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const questions = await client.getQuestions()
```

> The above endpoint returns JSON structured like this:

```json
[
  {
    "answer": "This is workspace is about the history of AI.",
    "audioUrl": "https://example.com/Answer_Audio_File.mp3",
    "createdAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
    "feedback": 0,
    "id": "<QUESTION_ID>",
    "question": "What is this workspace about?",
    "sensitive": false,
    "updatedAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
    "visible": true,
    "workspaceId": "my-workspace"
  }
]
```

This endpoint retrieves all user questions of a specific workspace.

### HTTP Request

`GET https://luk.az/workspaces`

### Query Parameters

There are no query params available at the moment.




## Get a Specific Question

```bash
curl "https://luk.az/getQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const question = await client.getQuestion('<QUESTION_ID>')
```

> The above endpoint returns JSON structured like this:

```json
{
  "answer": "This is workspace is about the history of AI.",
  "audioUrl": "https://example.com/Answer_Audio_File.mp3",
  "createdAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
  "feedback": 0,
  "id": "<QUESTION_ID>",
  "question": "What is this workspace about?",
  "sensitive": false,
  "updatedAt": {"_seconds": 1680559078, "_nanoseconds": 928000000},
  "visible": true,
  "workspaceId": "my-workspace"
}
```

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to retrieve

This endpoint retrieves a specific question.

### HTTP Request (with ID)

`GET https://luk.az/getQuestion/<QUESTION_ID>`





## Make Question Visible

```bash
curl "https://luk.az/showQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
await client.showQuestion('<QUESTION_ID>')
```

> The above endpoint returns JSON structured like this:

```json
true
```

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to make visible

This endpoint makes a specific question visible on its workspace.

### HTTP Request (with ID)

`PUT https://luk.az/showQuestion/<QUESTION_ID>`





## Make Question Invisible

```bash
curl "https://luk.az/hideQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
await client.showQuestion('<QUESTION_ID>')
```

> The above endpoint returns JSON structured like this:

```json
true
```

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to make invisible

This endpoint makes a specific question invisible on its workspace.

### HTTP Request (with ID)

`PUT https://luk.az/hideQuestion/<QUESTION_ID>`



## Save Question to Favourites

```bash
curl "https://luk.az/saveQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
await client.saveQuestion('<QUESTION_ID>')
```

> The above endpoint returns JSON structured like this:

```json
true
```

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to save in favourites list

This endpoint saves a specific question as favourite.

### HTTP Request (with ID)

`PUT https://luk.az/saveQuestion/<QUESTION_ID>`





## Remove Question from Favourites

```bash
curl "https://luk.az/removeQuestion/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
await client.removeQuestion('<QUESTION_ID>')
```

> The above endpoint returns JSON structured like this:

```json
true
```

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to remove from favourites list

This endpoint removes a specific question from favourites.

### HTTP Request (with ID)

`PUT https://luk.az/removeQuestion/<QUESTION_ID>`





## Rate Question Answer

```bash
curl "https://luk.az/rateAnswer/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
await client.rateAnswer('<QUESTION_ID>')
```

> The above endpoint returns JSON structured like this:

```json
true
```

### URL Parameters

Parameter | Description
--------- | -----------
ID        | The ID of the question to rate

This endpoint rates the answer of a specific question.

### HTTP Request (with ID)

`PUT https://luk.az/rateAnswer/<QUESTION_ID>`





## Get Authenticated User

```bash
curl "https://luk.az/getUser/<QUESTION_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = await lukaz.auth('<LUKAZ_API_KEY>')
const user = await client.getUser()
```

> The above endpoint returns JSON structured like this:

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

### HTTP Request (with ID)

`GET https://luk.az/getUser`

