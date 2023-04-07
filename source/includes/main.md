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

const client = await lukaz.authorize('<LUKAZ_API_KEY>')
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

const client = lukaz.auth('<LUKAZ_API_KEY>')
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

const client = lukaz.auth('<LUKAZ_API_KEY>')
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

const client = lukaz.auth('<LUKAZ_API_KEY>')
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

const client = lukaz.auth('<LUKAZ_API_KEY>')
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

const client = lukaz.auth('<LUKAZ_API_KEY>')
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

const client = lukaz.auth('<LUKAZ_API_KEY>')
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

const client = lukaz.auth('<LUKAZ_API_KEY>')
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

## Get Question Transcript

```bash
curl "https://luk.az/getTranscript/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.deleteFile('<WORKSPACE_ID>', {
    audioUrl: 'https://example.com/Audio_File.wav',
})
```

> The above endpoint returns JSON structured like this:

```json
{
  "transcript": "This is the text from the audio file."
}
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
transcript  | (string) The text extracted from the audio file


## Get Question Transcript

```bash
curl "https://luk.az/getTranscript/<WORKSPACE_ID>"
  -H "Authorization: <LUKAZ_API_KEY>"
```

```javascript
import { lukaz } from '@lukaz/client'

const client = lukaz.auth('<LUKAZ_API_KEY>')
const workspace = await client.deleteFile('<WORKSPACE_ID>', {
    audioUrl: 'https://example.com/Audio_File.wav',
})
```

> The above endpoint returns JSON structured like this:

```json
{
  "transcript": "This is the text from the audio file."
}
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
transcript  | (string) The text extracted from the audio file

