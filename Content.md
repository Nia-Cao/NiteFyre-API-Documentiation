# Content

This document outlines the NiteFyre API content endpoints.

The NiteFyre content API is a flexible storage system that allows custom applications to store hierarchical content within a single social content API.
Basic content is a JSON object which can have children and be a child of parent content. Any application using the NiteFyre API can access users content.
This allows for cross-experience content posting. Content follows a standard format with a data field. The data field can be a plain text message, or a large JSON object containing binary data.

## Overview

Below is an example of a parent post in the content API.
```
{
  "uuid":"niamh",
  "cuuid":"3cdb9372-39fa-4c24-814c-d58cebaf70cf",
  "content":"hii",
  "childOf":"home",
  "parentOf":["848d194c-1be2-4793-8b84-c2351048429a","39a27958-18af-4bb2-9896-7d8ab11fd779","b7305d5f-306e-44f6-92f4-bacbdaf78c93"],
  "created":"09/07/2022 08:38:05",
  "user":null
}
```
uuid" is the id of the user that posted the content.

"cuuid" is the UUID of the content.

"content" is a string which can be a serialised JSON object. This can contain anything an application developer wishes to store, however all content is available to be viewed. Future plans include additional application specific documents.

"childOf" is the cuuid of parent content.

"parentOf" is an array of all child content to this parent.

"created" is a content creation timestamp.

"user" is currently unused.

Below is an example of child content where the above example is the parent.

```
{
  "uuid":"niamh",
  "cuuid":"39a27958-18af-4bb2-9896-7d8ab11fd779",
  "content":"derp",
  "childOf":"3cdb9372-39fa-4c24-814c-d58cebaf70cf",
  "parentOf":[],
  "created":"09/10/2022 21:32:08",
  "user":null
}
```

When fetching content, the API can be given a cuuid and either return that single object, or it can return all child content.
As the parent/child concept allows infinite depth, only the first level is returned. To return all children of a first level child, the first level child must be requested.
Children of second level child content must also be requested seperately, and so on.

All content generally will have a parent, however the option to leave this field null means that it can only be accessed by requesting by cuuid.
In the above examples, "home" refers to the NiteFyre default user home page. Content with any other parent will not be displayed in user home.

