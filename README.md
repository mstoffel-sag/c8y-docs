# Cumulocity Guides website

<https://cumulocity.com/guides>

**Built with [Hugo](https://gohugo.io/)**

## Development environment

- Clone the repository
- [Install Hugo](https://gohugo.io/getting-started/installing/)
- Open a terminal window on project directory and type `hugo server`

## Structure

The Cumulocity Guides website architecture has the following structure:

- Section (e.g. *<http://cumulocity.com/guides/user-guide>*)
  - Subsection - renders as a single page (e.g. *<http://cumulocity.com/guides/user-guide/overview>*)
    - Anchor section - anchor tag in the subsection page (e.g. *<http://cumulocity.com/guides/user-guide/overview#user-settings>*)

The architecture is built with a mix of front matter and directory structure

## Adding content

### 1. Add a new section

Before adding a new section, check if the content fit in any of the available sections:

- Release notes
- Concepts guide
- User guide
- User guide (german version)
- Device guides
- Cumulocity-IoT Edge
- Microservice SDK guide
- Device SDK guide
- Web SDK guide
- Analytics guide
- Reference guide

A new section is defined by a markdown file with the following front matter:

```yaml
---
title: My new section # add the section title
bundle: new-section # add the directory holding the section pages
icon: "c8y-icon c8y-icon-tools" # use either fontawesome or c8y-icons
type: root # don't change
layout: root # don't change
weight: 90 # order the section in the section dropdown in ascending order
---
```

Grab the icon classes in the [styleguide](http://styleguide.cumulocity.com/icons/)

### 2. Add the section root directory

All guides are stored in the ```content``` directory. To add a new section, create a directory here and name it with the `bundle` value set in the front matter.

### 3. Add a subsection

Inside the newly created directory create a markdown file with the name you wish to use as a url — e.g. `introduction.md` with the following front matter:

```yaml
---
title: Introduction to Cumulocity # the page title
layout: bundle # don't change
weight: 10 # set the position of the page within the section in ascending order
aliases: # if needed, add the redirects here, otherwise remove this
  - /concepts-guide/introduction-to-cumulocity/
  - /concepts-guide/introduction-to-cumulocity.html
---
# add optional content as markdown
Cumulocity gives you very fast visibility and control over your remote assets, be these houses, cars, machines or any other assets that you need to manage.
```

If you're looking to have a short page without anchors, you're good to go, but if you want to add multiple subsections with anchors then proceed to the next step.

When adding multiple subsections, the content provided in this file will be rendered as a lead (text slightly larger) in the top of the page.

### 4. Add blocks of content with anchors to a page

To display multiple blocks of content and provide anchor links to display in the navigator, you'll have to follow these steps:

1. add a directory with the exact same name as the markdown file adding the suffix `-bundle`, e.g. `introduction-bundle`.

&nbsp;

2. Add a `index.html` file into the new directory with the following front matter:

```yaml
---
title: Introduction # not important as we won't use it, but we need the title
headless: true # states that all content inside this directory is just a resource to be used in another page
---
```

&nbsp;
3. Add a mardown file for each block of content with the folloing front matter:

```yaml
---
title: Overview # will be used as anchor, i.e. guides/users-guide/introduction/#overview
weight: 10 # to set the position in the page
---

## Add content as markdown or HTML

* Certified hardware kits and software libraries you can use to bring your remote assets into the cloud.
* Device management, data visualization and remote control functionality through the web.
* Rapid customization of the above through [real-time processing](/guides/concepts/realtime) and [Cumulocity applications](/guides/concepts/applications).
* APIs for extending the existing functionality or interfacing Cumulocity with your other IT services such as ERP or CRM systems. Cumulocity can also host your HTML5 applications.
[…]
```

### 5. Add media

Media should be added to `/static/images/`. Add a new directory if none of the available suits your needs.

Keep all file names url friendly (lowercase, no special characters, and no empty spaces).

To use the images in your pages, just add the relative path e.g `![image title](/images/<directory name>/<file name>)`.

### 6. Add devices into device guides

Device guides include a overview page with thumbnails of the devices and a filtering field.

When adding a new device, make sure to include an image sized 350 x 350px and provide the path to it on the front matter:

```yaml
---
title: Adeunis LoRaWAN Demonstrator # device name
layout: bundle # don't change
image: '/guides/images/devices/device-list/adeunis_rf-lorawan.jpg' #must include the full url
brand: Adeunis RF # brand or manufacturer
---
```

## Redirects

Redirects must be processed through aliases. To add them, go to the target page and add the following in front matter:

```yaml
---
title: Introduction to Cumulocity
layout: bundle
weight: 10
# add all the redirects to this page in a array
aliases:
  - /concepts-guide/introduction-to-cumulocity/
  - /concepts-guide/introduction-to-cumulocity.html
---
```

---
&copy; Cumulocity GmbH  2019 + All rights reserved.