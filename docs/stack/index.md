# The Stack

For content driven projects we use [Craft 3 as a headless CMS](https://craftcms.com/docs/3.x/#tech-specs) on the backend and [next.js](https://nextjs.org/docs/getting-started) on the frontend.

## Craft 3

### Why Craft?

Craft is a real Swiss Army Knife of CMSs.  Written in PHP, on top of the popular Yii Framework, it is highly flexible, extremely developer and content creator friendly, has a rich [marketplace of plugins](https://plugins.craftcms.com), and a [vibrant dev community](https://craftcms.com/community).  While it is not an open source project, they certainly adopt a similar ethos in their releases, their communication to users, and their dependency on a sprawling international dev community.  And it's pretty darn cheap.  The CMS dashboard is totally responsive, very mobile-friendly, and very intuitive for admins and content creators.  It has a clean-slate approach to content modeling and [front-end development](https://craftcms.com/docs/3.x/dev/) that doesn’t make any assumptions about your content or how it should be consumed.  It has a robust framework for [module and plugin development](https://craftcms.com/docs/3.x/extend/).  It has a thoughtful approach to [localization/multi-site management](https://craftcms.com/docs/3.x/sites.html).

Additionally, Craft has an option to run as a headless CMS.  When this option is enabled  queries to the CMS are handled over GraphQL.  Using Craft as a headless CMS allows for a very generous separation of concerns between the backend and the frontend, and therefore much more flexibility in terms of what technologies or strategies we leverage on the backend vs the frontend.

### Modeling content in Craft

The GUI in the Craft Admin Dashboard makes declaring and editing new Entry Types and Fields quick and easy.  All changes are recorded in the project config files as migrations (of sorts).  Project configs are applied when the project is instantiated making your work very portable across environments.  Asserting such fine control over such complex things all in a GUI in the dashboard also means devs can get going in Craft quite quickly, not getting bogged down by code/syntactic idiosyncracies.

### Creating content in Craft

Craft is a fairly unopinionated CMS which lends itself well to both traditional text-heavy web content like pages and posts, as well as defining very customized structured data.  

For the former, as much as possible, we take the composable "Content Block" approach, rather than a "Page Template" approach.  The distinction being that where a "Page Template" approach requires a new kinda "set in stone" page template for every type of page on your site, the composable "Content Block" approach supplies the content creator with a set of building blocks they can select and arrange to "compose" pages.  Still approach not only allows for more variance across pages, but also means a block of content can easily be abstracted out of a Page Entry, and into its own Entry, at which point that block of content can be reused across any pages.  For instance, if you have a Callout Content Block, any Callout the content creator creates can just be a one-off for whatever page they're working on, but also every Callout that is created is saved as its own Entry, independent of whatever page it is on, and therefore identical instances of that Callout can then be reused across any page.

For less-pagey content a Content Block approach usually isn't appropriate, but the wide array of off the shelf fields, and the ability to define highly complex custom fields, means you have a lot of tools at your disposal to create Entries, and create relationships between Entries, such that nearly any shape of data is achievable in the CMS.

## next.js

React is a fairly freewheeling javascript framework.  [next.js](https://nextjs.org/docs) provides enough structure/framework to keep your repo/project well organized and also dead simple configurations for your builds.  It is a framework optimized for SSR and/or Static content, and/or Dynamic content.  This versatility means it's never a stretch to use next.js in a project.  Because it's never one way or the other, but as many ways as you'd like, different aspects of a project can be optimized for different use cases.

## graphQL

[graphQL](https://graphql.org/) is a query language that thrusts more than the usual amount of ""API data-fetching" onus to the frontend.  It's not the most flexible way to compose queries, and that's sorta the point.  Each query is sorta a little schema validating what you want, against what you get, against what is available.