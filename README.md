# Data Migration Playbook Contributor Guide
This is the content repository for Microsoft's Data Migration Playbook which is hosted at https://datamigration.microsoft.com. This page serves as a guide to help future contributors get up to speed on files, their structure, and how to edit them and create new ones.

1. [Folder Structure](#folder-structure-overview)
2. [SiteConfig](#siteconfig)
3. [Scenarios](#scenarios)
4. [Steps](#steps)
4. [Actions](#actions)
5. [Partners & Case Studies](#partners--case-studies)
6. [Markdown](#markdown)

## Folder Structure Overview
All the files are organized in a structure that must be adhered to. It's not overly complicated and within the structure there is some freedom.

### en-US
At the top level is the folder for the default language which is United States English. All content files should be placed in their respective subfolders under this folder. We will explore this further below. Other languages might be brought on later but any translations should be based on the files here in the `en-US` folder. So, if and when multiple languages become available, if you want content available in all languages it should first be made here and translated after.

### Other Folders and Files
The only other folder currently here is a folder called `test` and this is strictly used for nightly unit and availability tests so this folder and its contents should be left alone.

The other files here are:

`.gitignore` - This should be obvious and should also, obviously, be left alone.

`README.md` - The file you are currently reading.

`scenarioTemplate` - A general example file for the structure of a scenario file.

`siteConfigTemplate` - An example file for the structure of the siteConfig file.

`sitemap.xml` - The only other file worth mentioning here. This is file that search engine robots look at to know the important discoverable URLs of the [Data Migration Playbook](https://datamigration.microsoft.com). If you create a new scenario, you will definitely want to update this file. Simply create a new `<url>` tag and place a new `<loc>` tag within. This contains the direct url to the new scenario. For example:
```HTML
  ...
  <url>
    <loc>https://datamigration.microsoft.com/scenario/scenario-file-name</loc>
  </url>
</urlset>
```

## SiteConfig
Some text

## Scenarios
Some text

## Steps
Some text

## Actions
Some text

## Partners & Case Studies
Some text

## Markdown
Some text
