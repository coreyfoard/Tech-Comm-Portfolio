#### Base URL for all API requests is:

<!-- Could probably trim this to "Base URL:" ... also, try to use the level headings in MD so as to clearly indicate a hierarchy of information. So: Resource (l1), Endpoint (l2), Sample Request (l3), Sample Response (l3), Parameters (l2) -->

```javascript
https://api.zotero.org
```

<!-- Search as a resource type? -->

## Getting all item types
Retrieves all requested item types. An item type will distinguish whether the item is a "book," "note," "report," or any of the other broad categories used to help cite items.

<!-- ItemTypes refer to ... -->

<!-- summary table of the end points for the item search resource? -->
```javascript
GET /itemTypes
```

#### Parameters

| Parameter   | Value       | Description |
| ----------- | ----------- | ----------- |
| format      |“atom”, “bib”, “keys”, “versions”,       |Will retrun request in the assigned format. |
|key         | string      |If a valid API key is provided, the request will be processed with the identity of the key's owner and the authority granted to the key.
| newer       | integer     |Return only objects modified after the specified library verson.          |
| locale| query| Will request names in other languages.|

<!-- Descriptions on parameters are usually noun phrases. Careful of spelling errors, Atom will not catch these unless you install a spellcheck package. Also, include a column for data type and required/optional? -->

#### <summary>Sample Request</summary>

```javascript
curl --location --request GET 'https://api.zotero.org/itemTypes'
```

#### <summary>Sample Response</summary>

<div style="height:300px;width:px;border:1px solid #ccc;font:16px/26px Georgia, Garamond, Serif;overflow:auto;">

```javascript
[
    {
        "itemType": "artwork",
        "localized": "Artwork"
    },
    {
        "itemType": "audioRecording",
        "localized": "Audio Recording"
    },
    {
        "itemType": "bill",
        "localized": "Bill"
    },
    {
        "itemType": "blogPost",
        "localized": "Blog Post"
    },
    {
        "itemType": "book",
        "localized": "Book"
    },
    {
        "itemType": "bookSection",
        "localized": "Book Section"
    },
    {
        "itemType": "case",
        "localized": "Case"
    },
    {
        "itemType": "computerProgram",
        "localized": "Computer Program"
    },
    {
        "itemType": "conferencePaper",
        "localized": "Conference Paper"
    },
    {
        "itemType": "dictionaryEntry",
        "localized": "Dictionary Entry"
    },
    {
        "itemType": "document",
        "localized": "Document"
    },
    {
        "itemType": "email",
        "localized": "E-mail"
    },
    {
        "itemType": "encyclopediaArticle",
        "localized": "Encyclopedia Article"
    },
    {
        "itemType": "film",
        "localized": "Film"
    },
    {
        "itemType": "forumPost",
        "localized": "Forum Post"
    },
    {
        "itemType": "hearing",
        "localized": "Hearing"
    },
    {
        "itemType": "instantMessage",
        "localized": "Instant Message"
    },
    {
        "itemType": "interview",
        "localized": "Interview"
    },
    {
        "itemType": "journalArticle",
        "localized": "Journal Article"
    },
    {
        "itemType": "letter",
        "localized": "Letter"
    },
    {
        "itemType": "magazineArticle",
        "localized": "Magazine Article"
    },
    {
        "itemType": "manuscript",
        "localized": "Manuscript"
    },
    {
        "itemType": "map",
        "localized": "Map"
    },
    {
        "itemType": "newspaperArticle",
        "localized": "Newspaper Article"
    },
    {
        "itemType": "note",
        "localized": "Note"
    },
    {
        "itemType": "patent",
        "localized": "Patent"
    },
    {
        "itemType": "podcast",
        "localized": "Podcast"
    },
    {
        "itemType": "presentation",
        "localized": "Presentation"
    },
    {
        "itemType": "radioBroadcast",
        "localized": "Radio Broadcast"
    },
    {
        "itemType": "report",
        "localized": "Report"
    },
    {
        "itemType": "statute",
        "localized": "Statute"
    },
    {
        "itemType": "tvBroadcast",
        "localized": "TV Broadcast"
    },
    {
        "itemType": "thesis",
        "localized": "Thesis"
    },
    {
        "itemType": "videoRecording",
        "localized": "Video Recording"
    },
    {
        "itemType": "webpage",
        "localized": "Web Page"
    }
]
```

</div>

## Get updated group metadata
Group metadata includes group titles and descriptions as well as member/role/permissions information. It is separate from group library data.

<!-- I think that this statement is intended as an endpoint description. If so, you will want it to  be expressed as verb phrase, which will emphasize the user action that is supported. -->

<!-- Note about what a group is?  Also need to talk about {group ID} as a path parameter -->

```javascript
GET /users/<userID>/groups?format=versions
```

#### Parameters

| Parameter   | Value       | Description |
| ----------- | ----------- | ----------- |
| Last-Modified-Version      |header       |Indicates the current version of either a library (for multi-object requests) or an individual object (for single-object requests). If changes are made to a library in a write request, the library's version number will be increased, any objects modified in the same request will be set to the new version number, and the new version number will be returned in the ```Last-Modified-Version``` header. Since modified objects always receive the newly increased library version, the returned ```Last-Modified-Version``` will be the same whether an item is modified as part of a multi-object or single-object request. |
| If-Modified-Since-Version       | header     |Checks for new data. If ```If-Modified-Since-Version: <libraryVersion>``` is passed with a multi-object read request and data has not changed in the library since the specified version, the API will return ```304 Not Modified```. If ```If-Modified-Since-Version: <objectVersion>``` is passed with a single-object read request, a ```304 Not Modified``` will be returned if the individual object has not changed.       |
| If-Unmodified-Since-Version     | header      |Used to ensure that existing data won't be overwritten by a client with out-of-date data. All write requests that modify existing objects must include either the ```If-Unmodified-Since-Version: <version>``` header or a JSON version property for each object. If both are omitted, the API will return a ```428 Precondition Required.```
| newer       | integer     |Return only objects modified after the specified library verson.          |
format      |“atom”, “bib”, “keys”, “versions”,       |Will retrun request in the assigned format. |

#### Sample Request


```javascript
curl --location --request GET 'https://api.zotero.org//users/<userid>/groups?format=versions'
```
<!-- In parameter table above: again check on the spelling. Also include a column for data type and required/optional. Try to make the parameter descriptions into noun phrases and keep the responses out for further elaboration in the Sample Response -->

#### Sample Response

```javascript
{
  "<groupID>": "<version>",
  "<groupID>": "<version>",
  "<groupID>": "<version>"
}
```
<!-- Given that different parameters will generate different success and failure messages you probably need to have a table summarizing the possible responses and the parameters associated with those responses -->

<!-- Nice work on making sense of this fairly complicated set of endpoints and parameters.  I thought that your document had a nice layout in the way that you set off endpoints and code samples to be visually distinct and grouped together, along with parameters. Check on the traditional ways of describing endpoints with verb phrases, parameters with noun phrases, and for describing a general resource statement. All of the minor details are important for meeting developer expectations and enabling them to make a more rapid decision about whether an endpoint is appropriate for them. See my comments about organization vis a vis the use of headings in MD. Grade: 134/150 -->
