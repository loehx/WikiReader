#WikiReader

WikiReader is a simple client based web application. On server side, it was written in NodeJS and uses the [microtemplates](https://github.com/paulmillr/microtemplates/) plugin to render out the views. The client side is based on AngularJS.

##Functionality

To put it simply, the main functionalities are:

* Search for articles from Wikipedia
* and read the specific article.

###Features

- **Live search.** There is no need to klick on 'find' or press enter when the user wants to search for articles. It now happens automatically while the user presses the keys.

- **Multi language support.** Just a simple multi language feature.


##Server side
###index

The *index.js* is the entrance point for the application. It does the following things:

* Use the wiki module.
* Allow access to the public folder. 
* Detect the browser language and redirect the user.
* Sends the start page in the specified language to the client.
* And of course, starts the server.

###lib / lang

This module manages the multi language support. It does the following things:

* Defines the default language, which will be used as fallback. (Default: 'en')
* Gets a language object for the specific language and fill the missing fields with the default language.

###lib / wiki

This module Works as a proxy for the Wiki API. The request of the client will be sent to the Wiki API using GET parameters. The client then receives the chunks that we receive.

##Client side
###Controllers

- **SearchController** manages the search. It uses the *core/Wikipedia* module to search.
- **ArticleController** gets and handles the data of an article using the *core/Wikipedia* module.

###Views

- **/view/search** is the model for the *SearchController*. It consists of an search field for user input and a result view that lists all the articles.
- **/view/article** is the model for the *ArticleController*.

Because of the fact that there are just two views and they are not very complex, the views are included to the *index.htm* and not in a seperate folder.

###Core

- **Wikipedia** is the client side module for accessing Wikipedia.org. It communicates with the server side **/lib/wiki** module and is all about getting data from Wikipedia. It uses a Ajax/JSON communication, as well as Ajax/HTML for the *Improved article forwarding* feature. It is seperate from the controllers and could be used in other projects.

##Folder Structure

**index.js** starts the server. It handles the following requests:

- "**/**" redirects to the master language 'en'.
- **/en/** loads the english page, starting with the article search.
- **/public/...** allows access to the public folder.

**lang** contains all language files, which are written in JSON and contain several translations, which can be used in the *index.htm* using the [microtemplates](https://github.com/paulmillr/microtemplates/) plugin.

**lib** contains the JavaScript/NodeJS files, which are used by the *index.js* in the root folder.

**node_modules** contains the NodeJS plugins.

**public** contains the client side files, such as the view or the resources. Everything not in the *public* folder relates to the server and cannot be reached by the user directly.

- **controller** contains all AngularJS controller. 
- **core** contains modules with a deeper logic.
- **resrc** contains all assets.

README from January 10, 2015