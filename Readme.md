﻿# LinkDotNet.Blog
This is a blog software completely written in C# / Blazor. The aim is to have it configurable as possible. 

## How does it work
The basic idea is that the content creator writes his posts in markdown language (like this readme file). 
The markdown will then by translated to HTML and displayed to the client. This gives an easy entry to writing posts with all the flexibility markdown has.

## Setup
Just clone this repository and you are good to go. There are some settings you can tweak. The following chapter will guide you 
through the possibilities.

### appsettings.json
The appsettings.json file has a lot of options to customize the content of the blog. The following table shows which values are used when.

```json
{
  ...
  "BlogName": "linkdotnet",
  "GithubAccountUrl": "",
  "LinkedInAccountUrl": "",
  "Introduction": {
    "Description": "Some nice text about yourself. Markup can be used [Github](https://github.com/someuser/somerepo)",
    "BackgroundUrl": "assets/profile-background.png",
    "ProfilePictureUrl": "assets/profile-picture.jfif"
  },
  "ConnectionString": "",
  "DatabaseName": "",
  "Auth0": {
    "Domain": "",
    "ClientId": "",
    "ClientSecret": ""
  }
}

```

| Property | Type | Description |
|----------|------|-------|
|BlogName|string|Name of your blog. Is used in the navbar and is used as the title of the page.|
|GithubAccountUrl|string|Url to your github account. If not set the navigation link is not shown|
|LinkedInAccountUrl|string|Url to your LinkedIn account. If not set the navigation link is not shown|
|Introduction| |Is used for the introduction part of the blog|
|Description|MarkdownString|Small introduction text for yourself. This is also used for `<meta name="description">` tag. For this the markup will be converted to plain text.|
|BackgroundUrl|string|Url or path to the background image|
|ProfilePictureUrl|string|Url or path to your profile picture|
|ConnectionString|string|Is used for connection to a database. Not used when `InMemoryStorageProvider` is used|
|DatabaseName|string|Name of the database. Only used with `RavenDbStorageProvider`|
|Auth0| |Configuration for setting up Auth0|
|Domain|string|See more details here: https://manage.auth0.com/dashboard/|
|ClientId|string|See more details here: https://manage.auth0.com/dashboard/|
|ClientSecret|string|See more details here: https://manage.auth0.com/dashboard/|

The usage might shift directly into the extension methods, where they are used.

## Storage Provider
Currently there are 4 Storage-Provider:
 * InMemory - Basically a list holding your data (per request)
 * RavenDb - As the name suggests for RavenDb
 * Sqlite - Based on EF Core, so it can be easily adapted for other Sql Dialects
 * SqlServer - Based on EF Core, so it can be easily adapted for other Sql Dialects

### Using
To use one of those just use the extension method in the Startup.cs in `ConfigureServices`:
```csharp
services.UseSqlAsStorageProvider();
```

It is only one storage provider at a time allowed. Registering multiple will result in an exception.

## Authorization
There is only one mechanism enabled via Auth0. For more information go to: https://auth0.com/docs/applications

The main advantage of Auth0 is the easy configurable dashboard on their website. 