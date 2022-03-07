# Cloud Services

### Google Cloud Platform

[Google Cloud Platform](https://cloud.google.com/) (GCP) is Google's one-stop-shop-clearing-house-AWS-look-alike-do-it-all service.  And it is just that.  We use GCP to host our web products, and all of the homegrown services, infrastructure, and databases that make those web products go.  Every project in GCP:

- has three instances: `prod`, `integration`, and `dev`.  [[Deployment workflows for those environments|Deployment Workflows]]

- infrastructure defined in [terraform](https://www.terraform.io/)

- has docker containers to be used on build/deploy

### Netlify

[Netlify](https://www.netlify.com/) is a static site hosting platform with next.js and gatsby projects in mind.  It offers a bunch of wonderful tools for managing and deploying projects, as well as config files to assert even greater control over builds and such.  It has a very generous free tier and, before we set up GCP for similar types of development, it was absolutely indispensable.  This is close to a legacy service as we now have the capability to host these kinds of client apps in GCP app engine.  However, this is still where all of the current iterations of the Formal Education Investigations live and most of them will likely stay here throughout the rest of the pilot testing cycles of FY21 - FY23 and beyond.  Starting in FY22 we may begin the process of porting Investigations from the Gatsby to next.js.  As this work unfolds we will tackle hosting on GCP in tandem.

### Canto

[Canto](https://www.canto.com/) is a Digital Assets Management system (DAM) that our team uses to house an archive of all of the assets (photos, videos, 3D renderings, etc.) the Rubin project produces, and also as a distribution source for all of the media assets we include in our web products.  It has miriad tools for managing, editing, transforming, and sharing assets in the browser.  It features a number of [integrations](https://www.canto.com/integrations/) as well as [a robust API](https://api.canto.com/) and all of the assets are served over a cdn.

### User Analytics

TBD

## Legacy

These are services we still rely upon but are in the process of shifting away from, or in the process of deprecating those web products that rely upon them.

### DigitalOcean

We use [DigitalOcean](https://www.digitalocean.com/) to host traditional sorts of projects that require a web server and database and the like.  We intend to migrate all of the products hosted on DigitalOcean  to the Google Cloud Platform by the end of FY22.

### AWS

We used [AWS](https://www.google.com/aclk?sa=l&ai=DChcSEwjr6JqJw6X0AhUaYoYKHU4nBpEYABABGgJ2dQ&ae=2&sig=AOD64_3F94tAu-usimY111nEO2HKDgw0KA&q&adurl&ved=2ahUKEwiAxpCJw6X0AhWvRDABHUVSA8EQ0Qx6BAgCEAE)) for website hosting prior to adopting DigitalOcean.  We still use an AWS bucket as an interim media server assets storage solution.  We intend to migrate all of the media assets hosted on AWS to Canto by the end of FY22.

### Namecheap

[Namecheap](https://www.namecheap.com/) handles domain purchases, DNS records, and some name servers stuff.  Mostly we've already shifted away from this service.  The only site in production that still relies upon it is Data2Dome.  We intend to migrate any remaining domains to GCP by the end of 2021.
