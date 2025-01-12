# Introduction

Welcome to the lukaz API, a generative AI for your documents!
You can use our API to develop an application based on lukaz.
In this reference, you can find some code examples in `JavaScript` and in `bash`.

## Installation

You can install lukaz with the following command:

`npm i @lukaz/client`

Or just use our HTTP endpoints described in this reference. 

## Base URLs

### Production Environment

`europe-west1-lukaz-api.cloudfunctions.net`

### Development Environment

`europe-west1-lukaz-dev.cloudfunctions.net`

Create an account on the dev UI: <a href="https://lukaz.dev/sign-up?user=true" target="_blank">lukaz.dev</a>

Set the dev environment on the JS client by passing `dev` in the second parameter.




# Authentication

lukaz uses API keys to allow access to the API.
You can create a new API key on the <a href="https://lukaz.ai/settings" target="_blank">settings</a> page under security options.

The API key should be included in all requests to the server in a header that looks like the following:

`x-api-key: <API_KEY>`

> Send a valid API key in the header for every request:

```javascript
import client from 'lukaz'
const lukaz = new client('<API_KEY>')

const workspaces = await lukaz.getWorkspaces()
```

```bash
curl "https://<BASE_URL>/<ENDPOINT>" \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> Make sure to replace `<API_KEY>` with your API key.




## Get Authenticated User

This endpoint retrieves the user data related to the API key in use.
Currently only available on the dev environment.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

const user = await lukaz.getUser()
```

```bash
curl "https://<BASE_URL>/getUser" \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
{
  "displayName": "Example User",
  "email": "user@example.com",
  "photoURL": "https://example.com/Photo_File.jpg",
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

### HTTP Request

`POST https://<BASE_URL>/getUser`

### HTTP Response Body

Property        | Description
---------       | -----------
createdAt       | Timestamp of the creation
displayName     | User's display name
email           | Email address
photoURL        | URL of the profile photo
quota           | Quota related to the subscription plan
savedQuestions  | Array of IDs of user's favorite questions
usage           | Usage of the current billing period

### User Quota

Property          | Description
---------         | -----------
questions         | Number of questions / month allowed
workspaces        | Number of workspaces allowed

### Plan Usage

Property          | Description
---------         | -----------
questions         | Current number of questions asked
workspaces        | Number of workspaces created





# Workspaces

## Create New Workspace

This endpoint creates a new workspace.
A workspace is basically a collection of documents with questions and answers.
It can be shared with other users or made publicly available.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.createWorkspace('<WORKSPACE_ID>', {
    description: 'My custom AI workspace.',
    options: {
        ask: true,
        docs: false,
        free: false,
        public: false,
        upload: true
    }
})
```

```bash
curl "https://<BASE_URL>/createWorkspace/<WORKSPACE_ID>" \
  -d '
  {
    "description": "My custom AI workspace.",
    "options": {
      "ask": true,
      "docs": true,
      "free": false,
      "public": false,
      "upload": true
    }
  }' \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`POST https://<BASE_URL>/createWorkspace/<WORKSPACE_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to create

### HTTP Request Body

Property    | Description
---------   | -----------
description | Descripton of the workspace
options     | Options of the workspace

### Workspace Options

Property    | Description
---------   | -----------
ask         | Asking questions enabled/disabled
docs        | Documents shown/hidden on workspace
free        | Asking questions free/paid
public      | Workspace access public/private
upload      | File upload enabled/disabled





## Get Workspace

This endpoint retrieves a workspace.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

const workspace = await lukaz.getWorkspace('<WORKSPACE_ID>')
```

```bash
curl "https://<BASE_URL>/getWorkspace/<WORKSPACE_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
{
  "createdAt": "2023-01-31T18:10:54.376Z",
  "description": "My custom AI workspace.",
  "documents": [
    {
      "createdAt": "2023-01-31T18:10:54.376Z",
      "extension": "pdf",
      "name": "Text_File.pdf",
      "processed": true,
      "url": "https://example.com/Text_File.pdf"
    }
  ],
  "id": "<WORKSPACE_ID>",
  "ownerEmail": "owner@example.com",
  "options": {
    "ask": true,
    "docs": false,
    "free": false,
    "public": false,
    "upload": true
  },
  "roles": {
    "owner@example.com": 5,
    "user@example.com": 4
  },
  "stats": {
    "answers": 5,
    "docs": 2,
    "questions": 7
  },
  "updatedAt": "2023-01-31T18:10:54.376Z"
}
```

### URL Parameters

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to retrieve

### HTTP Request

`POST https://<BASE_URL>/getWorkspace/<WORKSPACE_ID>`

### HTTP Response Body

Property     | Description
---------    | -----------
createdAt    | Timestamp of the creation
description  | Description of the workspace
documents    | Documents uploaded to the workspace
id           | The ID of the workspace
ownerEmail   | Email address of the workspace's owner
options      | Options of the workspace
roles        | Users emails with their roles
stats        | Statistics of the workspace
updatedAt    | Timestamp of the last update

### Documents

Property    | Description
---------   | -----------
createdAt   | Timestamp of the updload
extension   | File extension
name        | File name
processed   | Processing status
url         | File URL on lukaz

### Workspace Options

Property    | Description
---------   | -----------
ask         | Asking questions enabled/disabled
docs        | Documents shown/hidden on workspace
free        | Asking questions free/paid
public      | Workspace access public/private
upload      | File upload enabled/disabled

### User Roles

Property        | Description
---------       | -----------
EMAIL_ADDRESS   | Email address or session ID

### User Roles Values

Value           | Label    | Description
---------       |----------| -----------
0               | disabled | No access to the workspace
1               | viewer   | Access to visible questions
2               | asker    | View and ask questions
3               | editor   | Show/hide questions
4               | admin    | Upload new documents
5               | owner    | Delete documents
6               | creator  | Delete workspace

### Workspace Statistics

Property    | Description
---------   | -----------
answers     | Number of questions visible on workspace
docs        | Number of documents processed
questions   | Total number of questions asked (by all users)





## Get All Workspaces

This endpoint retrieves all workspaces that the authenticated user owns or has access to.
See `getWorkspaces` for a detailed description of a workspace structure.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

const workspaces = await lukaz.getWorkspaces()
```

```bash
curl "https://<BASE_URL>/getWorkspaces"
  -H "x-api-key: <API_KEY>" \ 
  -X POST
```

> HTTP Response Body:

```json
[
  {
    "createdAt": "2023-01-31T18:10:54.376Z",
    "description": "My custom AI workspace.",
    "documents": [
      {
        "createdAt": "2023-01-31T18:10:54.376Z",
        "extension": "pdf",
        "name": "Text_File.pdf",
        "processed": true,
        "url": "https://example.com/Text_File.pdf"
      }
    ],
    "id": "<WORKSPACE_ID>",
    "ownerEmail": "owner@example.com",
    "options": {
      "ask": true,
      "docs": false,
      "free": false,
      "public": false,
      "upload": true
    },
    "roles": {
      "owner@example.com": 5,
      "user@example.com": 4
    },
    "stats": {
      "answers": 5,
      "docs": 2,
      "questions": 7
    },
    "updatedAt": "2023-01-31T18:10:54.376Z"
  }
]
```

### HTTP Request

`POST https://<BASE_URL>/getWorkspaces`

### HTTP Response Body

Property     | Description
---------    | -----------
Workspace[]  | The array of retrieved workspaces





## Update Workspace

This endpoint updates a workspace.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.updateWorkspace('<WORKSPACE_ID>', {
    description: 'My custom AI workspace.',
    notify: true,
    options: {
        ask: true,
        docs: true,
        free: false,
        public: false,
        upload: true
    },
    roles: {
        'user@example.com': 2
    }
})
```

```bash
curl "https://<BASE_URL>/updateWorkspace/<WORKSPACE_ID>" \
  -d '
  {
    "description": "My custom AI workspace.",
    "notify": true,
    "options": {
      "ask": true,
      "docs": true,
      "free": false,
      "public": false,
      "upload": true
    },
    "roles": {
      "user@example.com": 2
    }
  }' \
  -H "x-api-key: <API_KEY>" \
  -X PUT
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`PUT https://<BASE_URL>/updateWorkspace/<WORKSPACE_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to update

### HTTP Request Body

Property    | Description
---------   | -----------
description | Descripton of the workspace
notify      | Send invite email for new users
options     | Options of the workspace
roles       | Email addresses with their roles

### Workspace Options

Property    | Description
---------   | -----------
ask         | Asking questions enabled/disabled
docs        | Documents shown/hidden on workspace
free        | Asking questions free/paid
public      | Workspace access public/private
upload      | File upload enabled/disabled

### User Roles

Property        | Description
---------       | -----------
EMAIL_ADDRESS   | Email address or session ID

### User Roles Values

Value           | Label    | Description
---------       |----------| -----------
0               | disabled | No access to the workspace
1               | viewer   | Access to visible questions
2               | asker    | View and ask questions
3               | editor   | Show/hide questions
4               | admin    | Upload new documents
5               | owner    | Delete documents
6               | creator  | Delete workspace




## Delete Workspace

This endpoint deletes a workspace.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.deleteWorkspace('<WORKSPACE_ID>')
```

```bash
curl "https://<BASE_URL>/deleteWorkspace/<WORKSPACE_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`POST https://<BASE_URL>/deleteWorkspace/<WORKSPACE_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to delete





## Upload File onto Workspace

This endpoint uploads a file onto a workspace.

Supported formats: `pdf, doc, docx, jpg, png, txt, md` 

Max file size: `50MB`

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.upload('<WORKSPACE_ID>', {
    filePath: '<FILE_PATH>',
})
```

```bash
curl "https://<BASE_URL>/upload/<WORKSPACE_ID>" \
  -F filePath=@Text_File.pdf \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`POST https://<BASE_URL>/upload/<WORKSPACE_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to upload the file

### HTTP Request Body

Property    | Description
---------   | -----------
filePath    | Path of a local text file to upload






## Delete File from Workspace

This endpoint deletes a file from a workspace.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.deleteFile('<WORKSPACE_ID>', {
    fileName: '<FILE_NAME>',
})
```

```bash
curl "https://<BASE_URL>/deleteFile/<WORKSPACE_ID>" \
  -d '{"fileName": "<FILE_NAME>"}' \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`POST https://<BASE_URL>/deleteFile/<WORKSPACE_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to delete the file from

### HTTP Request Body

Property    | Description
---------   | -----------
fileName    | The name of the file to be deleted





# Questions

## Get Question Transcript

This endpoint transcripts the text from an audio file hosted on the web or locally.

Supported formats: `mp3, mp4, mpeg, mpga, m4a, wav, webm`

Max file size: `5MB`

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

const {transcript} = await lukaz.getTranscript('<WORKSPACE_ID>', {
    audioUrl: 'https://example.com/Audio_File.mp3',
    filePath: '<FILE_PATH>'
})
```

```bash
curl "https://<BASE_URL>/getTranscript/<WORKSPACE_ID>" \
  -d '{"audioUrl": "https://example.com/Audio_File.mp3"}' \
  -F filePath=@Audio_File.mp3 \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
{
  "transcript": "This is the text from the audio file."
}
```

### HTTP Request

`POST https://<BASE_URL>/getTranscript/<WORKSPACE_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to ask a question

### HTTP Request Body

Just one of the properties is required.

Property    | Description
---------   | -----------
audioUrl    | URL of a hosted audio file
filePath    | Path of a local audio file

### HTTP Response Body

Property    | Description
---------   | -----------
transcript  | The text extracted from the audio





## Ask Question to Workspace

This endpoint asks a question to a workspace.
On the dev environment, it will return just a test answer.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

const answer = await lukaz.ask('<WORKSPACE_ID>', {
    question: 'What is this workspace about?',
    translateAnswer: false
})
```

```bash
curl "https://<BASE_URL>/ask/<WORKSPACE_ID>" \
  -d '{"question": "What is this workspace about?", "translateAnswer": false}' \
  -H "x-api-key: <API_KEY>" \
  -X POST
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

### HTTP Request

`POST https://<BASE_URL>/ask/<WORKSPACE_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to ask a questionn

### HTTP Request Body

Property         | Description
---------        | -----------
question         | The natural question to ask
translateAnswer  | Answer language same as question's

### HTTP Response Body

Property    | Description
---------   | -----------
answer      | Answer generated for the question asked
question    | Question asked to the workspace
questionId  | Unique ID of the question asked
sensitive   | Sensitiveness of the question's context





## Get Answer Audio

This endpoint generates an audio file from the answer.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

const {audioUrl} = await lukaz.getAudio('<QUESTION_ID>')
```

```bash
curl "https://<BASE_URL>/getAudio/<QUESTION_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
{
  "audioUrl": "https://example.com/Audio_File.mp3"
}
```

### HTTP Request

`POST https://<BASE_URL>/getAudio/<QUESTION_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
QUESTION_ID         | The ID of the question to generate the audio

### HTTP Response Body

Property    | Description
---------   | -----------
audioUrl    | The file URL of the generated audio




## Get Question

This endpoint retrieves a question.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

const question = await lukaz.getQuestion('<QUESTION_ID>')
```

```bash
curl "https://<BASE_URL>/getQuestion/<QUESTION_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
{
  "answer": "This workspace is about AI.",
  "audioUrl": "https://example.com/Audio_File.mp3",
  "createdAt": "2023-01-31T18:10:54.376Z",
  "feedback": 0,
  "id": "<QUESTION_ID>",
  "question": "What is this workspace about?",
  "sensitive": false,
  "updatedAt": "2023-01-31T18:10:54.376Z",
  "visible": true,
  "workspaceId": "<WORKSPACE_ID>"
}
```

### HTTP Request

`POST https://<BASE_URL>/getQuestion/<QUESTION_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
QUESTION_ID         | The ID of the question to retrieve

### HTTP Response Body

Property     | Description
---------    | -----------
answer       | Answer generated for the question
audioUrl     | File URL of the answer's audio
createdAt    | Timestamp of the creation
feedback     | Feedback from the asker
id           | Unique ID of the question
question     | Question text that was asked
sensitive    | Sensitiveness of the question
updatedAt    | Ttimestamp of the last update
visible      | Status of the question on workspace
workspaceId  | ID of the question's workspace




## Get All Questions

This endpoint retrieves all questions of a workspace or made by the user.
See `getQuestion` for a detailed description of a question structure.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

const questions = await lukaz.getQuestions('<WORKSPACE_ID>')
```

```bash
curl "https://<BASE_URL>/getQuestions/<WORKSPACE_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X POST
```

> HTTP Response Body:

```json
[
  {
    "answer": "This workspace is about AI.",
    "audioUrl": "https://example.com/Audio_File.mp3",
    "createdAt": "2023-01-31T18:10:54.376Z",
    "feedback": 0,
    "id": "<QUESTION_ID>",
    "question": "What is this workspace about?",
    "sensitive": false,
    "updatedAt": "2023-01-31T18:10:54.376Z",
    "visible": true,
    "workspaceId": "<WORKSPACE_ID>"
  }
]
```

### HTTP Request

`POST https://<BASE_URL>/getQuestions/<WORKSPACE_ID>`

### URL Parameters

If `<WORKSPACE_ID>` is not provided, then the questions made by the user are retrieved.

Parameter           | Description
---------           | -----------
WORKSPACE_ID        | The ID of the workspace to retrieve the questions

### HTTP Response Body

Property     | Description
---------    | -----------
Question[]   | The array of retrieved questions





## Show Question on Workspace

This endpoint makes a question visible on its workspace.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.showQuestion('<QUESTION_ID>')
```

```bash
curl "https://<BASE_URL>/showQuestion/<QUESTION_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X PUT
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`PUT https://<BASE_URL>/showQuestion/<QUESTION_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
QUESTION_ID         | The ID of the question to make visible





## Hide Question from Workspace

This endpoint makes a question invisible on its workspace.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.showQuestion('<QUESTION_ID>')
```

```bash
curl "https://<BASE_URL>/hideQuestion/<QUESTION_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X PUT
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`PUT https://<BASE_URL>/hideQuestion/<QUESTION_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
QUESTION_ID         | The ID of the question to make invisible





## Save Question to Favourites

This endpoint saves a question on user's favourites.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.saveQuestion('<QUESTION_ID>')
```

```bash
curl "https://<BASE_URL>/saveQuestion/<QUESTION_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X PUT
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`PUT https://<BASE_URL>/saveQuestion/<QUESTION_ID>`

### URL Parameters

Parameter          | Description
---------          | -----------
QUESTION_ID        | The ID of the question to save





## Remove Question from Favourites

This endpoint removes a question from user's favourites.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.removeQuestion('<QUESTION_ID>')
```

```bash
curl "https://<BASE_URL>/removeQuestion/<QUESTION_ID>" \
  -H "x-api-key: <API_KEY>" \
  -X PUT
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`PUT https://<BASE_URL>/removeQuestion/<QUESTION_ID>`

### URL Parameters

Parameter           | Description
---------           | -----------
QUESTION_ID         | The ID of the question to remove






## Rate Answer

This endpoint rates the answer of the question.

```javascript
import client from '@lukaz/client'
const lukaz = new client('<API_KEY>')

await lukaz.rateAnswer('<QUESTION_ID>', {
    feedback: 1
})
```

```bash
curl "https://<BASE_URL>/rateAnswer/<QUESTION_ID>" \
  -d '{"feedback": 1}' \
  -H "x-api-key: <API_KEY>" \
  -X PUT
```

> HTTP Response Body:

```json
true
```

### HTTP Request

`PUT https://<BASE_URL>/rateAnswer/<QUESTION_ID>`

### URL Parameters

Parameter          | Description
---------          | -----------
QUESTION_ID        | The ID of the question to rate

### HTTP Request Body

Property     | Description
---------    | -----------
feedback     | 0 (bad) or 1 (good)





# HTML Widget

You can embed lukaz on any website with almost no code!
Just copy the widget code from your workspace options and follow the comments.

For customization, read the documentation on <a href="https://www.npmjs.com/package/@lukaz/widget" target="_blank">npm</a>.
