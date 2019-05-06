
# Content Library Application

> A single database stores the entire library of content for all HTML topics in the content tool of the LMS. Each HTML page that uses this application must define a variable array to call one or more items of content from the database.

This is a free-of-charge application. It is NOT open-source.

By using this application you agree to the following terms. It must only be used for generating HTML topics within the content tool of the Brightspace LMS. Unauthorized modification of this applciation is strictly prohibited. Unauthorized sale of this applciation is strictly prohibited. By using this application you do so at your own risk. The author is not responsible for any loss or damage resulting from the use or misuse of this application.

Written by [Ricky Haror](https://www.linkedin.com/in/rickyharor)

Copyright (C) Ricky Haror

Contact: [https://coursedevtools.rickyharor.com/Home/Contact](https://coursedevtools.rickyharor.com/Home/Contact)

## Table of Contents
* [Prerequisites](#prerequisites)
  * [Self-host](#self-host)
  * [Direct link](#direct-link)
* [Running the application](#running-the-application)
  * [Database](#database)
  * [GitHub Pages](#github-pages)
  * [.js Files](#js-files)
  * [JavaScript Variables](#javaScript-variables)
  * [HTML](#html)
* [Example configuration](#example-configuration)
  * [HTML Content Topic page](#html-content-topic-page)
  * [index.js](#indexjs)

##  Prerequisites

There are two options for hosting this application, **Self-host** or the recommended method, **Link Directly** to this repo. 

### Self-host
If you choose to self-host your application, you will need to be manually update it when there are fixes or changes made to the application.

Clone this repo to your local machine using  `https://github.com/RickyHaror/content-library-app.git`

 
### Direct link

Linking directly to the files in this repo is the recommended method to setup this application. This ensures that you are always using the latest version.

If you choose to link directly to this repo there are no hosting steps required for you to complete.

## Running the application
The following sections provide information on configuring the items required to get your application running.

### Database
The content library items must be stored in a single **database.json** file. Create a new GitHub repo to host this file or push it to an existing repo.

This file must contain an array of objects. Each object is an individual piece of content with the following properties:

    {
      "id": int,
      "name": string,
      "markup": string
    }

#### Notes
The **id** property must be unique for each object. The application uses this value to get content objects to display.
The **name** property does not currently get displayed when running this application. It's for organizational purposes and may, in the future, be used to create an index page.
The **markup** string cannot include line breaks and quotes need to be escaped.

### GitHub Pages
Enable GitHub Pages for a no jekyll site.
There is a delay in processing updates to the GitHub Pages website that you create. It could take a few minutes to hours for updates to be applied.

### .js Files
Currently there are three compiled JavaScript files that are required to run this application.

 1. runtime.js
 2. polyfills.js
 3. main.js

These files need to be referenced just before the end of the `<body>` section of your content topic HTML page in the order listed above.

### JavaScript Variables
The following JavaScript variables must be set in the global scope:

 1. `sections` - The array of database Id values or string values. You can use strings to pass markup that is not listed in the database. This is useful in cases where you need to add content between items from the database that is specific to the course but not useful for other courses. The values in the array are displayed in the order you provide.
 2. `databaseHost` - Name of the GitHub repo host.
 3. `databaseRepoPath` - Name of the repo in the above host along with the specific path.

### HTML
The following markup must appear in the body section of the HTML topic page before the .js files are called.
```html
<div id="content-library">
  <app-root></app-root>
</div>
```

## Example configuration
The following example is setup with low maintenance in mind. I don't want to update each HTML content page when there is a change to content or to the content-library-app code. This the recommended approach, but it's not the only way.

You can find the sample app repo on GitHub: [content-library-app-sample](https://github.com/RickyHaror/content-library-app-sample)
Note: This repo has been setup with GitHub Pages.
