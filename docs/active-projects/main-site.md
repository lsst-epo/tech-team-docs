# Main Site

## Rubin Observatory Operations Site (the Main Site)

This project has two associated repos, `rubin-obs-api` and `rubin-obs-client`, where the former is a headless Craft 3 CMS instance running in a Docker container, and the latter is a next.js app with a mix of static and dynamic pages.  What follows is not a comprehensive description of those technologies (that's covered in [[CMS Backend + React Frontend Stack | The Stack]]) or information about how to get the project up and running on your local (that's covered in the readmes for the [api](https://github.com/lsst-epo/rubin-obs-api/blob/master/README.md) and  [client](https://github.com/lsst-epo/rubin-obs-client/blob/master/README.md) and repos), but instead a summary of the repo structure, and any a note on Craft Localization quirks.

### Client architecture

- `/lib` — backend API fetching methods and GraphQL queries
- `/pages` — a single component that uses [`getStaticProps`](https://nextjs.org/docs/basic-features/data-fetching#getstaticprops-static-generation) and [`getStaticPaths`](https://nextjs.org/docs/basic-features/data-fetching#getstaticpaths-static-generation) to dynamically generate static pages for all routes.
- `/components` — all React components for generating portions of static pages. These are further organized by type: "content-blocks", "dynamic", "factories", "global", "layout", "primitives", and "templates".
- `/components/content-blocks` — content blocks are the building 
- `/components/dynamic` — components that make run-time API requests and are rendered client-side.
- `/theme` — SCSS partials defining the frontend theme. Component styles are defined in the same directory as their components but are imported at `/theme/styles/components/_index.scss` so that they are compiled in a single global stylesheet.
- `/shapes` — reusuable prop-type shapes for recurring data structures like pages, images, locales, etc.
- `/public` — static assets like favicons that are passed directly to the output directory without hashing.

Module aliases are defined in `/jsconfig.json`.

### Localization

There are some nuances to be aware of when dealing with localization data from Craft in Next.js:

- Entries must be fetched separately for each locale (`site` param in the GraphQL API). If you want to generate pages for all routes, each set of entries must be concatenated into one array first.
- Similarly, an API request for a single entry must include the locale (`site` param) even if the `uri` includes the subdirectory for the locale (e.g. `/es/gallery`).
- There isn't a `site` property that exists on an entry but there is a `language` property. There is also a `localized` property which will return an array of instances of that entry in all other locales.
  - The `LanguageSelect` component makes use of these properties to handle client-side routing between localized instances of a page. This approach avoids having to test for the presence of a localized subdirectory in the current route.
