# Data Migration Playbook Contributor Guide
This is the content repository for Microsoft's Data Migration Playbook which is hosted at https://datamigration.microsoft.com. This page serves as a guide to help future contributors get up to speed on files, their structure, and how to edit them and create new ones.

1. [Folder Structure](#folder-structure-overview)
2. [SiteConfig](#siteconfig)
3. [Scenarios](#scenarios)
4. [Steps](#steps)
4. [Actions](#actions)
5. [Partners & Case Studies](#partners--case-studies)
6. [JSON](#json)
7. [Markdown](#markdown)


## Folder Structure Overview
All the files are organized in a structure that must be adhered to. It's not overly complicated and within the structure there is some freedom. With the exception of step files, everything is in JSON format. There is a section covering some [basic rules of JSON](#json). Step files take up the bulk of the actual content and are in Markdown format. We've created a [cheat sheet](#markdown) to help you.

### en-US
At the top level is the folder for the default language which is United States English. All content files should be placed in their respective subfolders under this folder. We will explore this further below. Other languages might be brought on later but any translations should be based on the files here in the `en-US` folder. So, if and when multiple languages become available, if you want content available in all languages it should first be made here and translated after.

### Other Folders and Files
The only other folder currently here is a folder called `test` and this is strictly used for nightly unit and availability tests so this folder and its contents should be left alone.

The other files here are:

`.gitignore` - This should be obvious and should also, obviously, be left alone.

`README.md` - The file you are currently reading.

`scenarioTemplate` - A general example for the structure of a scenario file.

`siteConfigTemplate` - An example for the structure of the siteConfig file.

`sitemap.xml` - The only other file worth mentioning here. This is file that search engine robots look at to know the important discoverable URLs of the [Data Migration Playbook](https://datamigration.microsoft.com). If you create a new scenario, you will definitely want to update this file. Simply create a new `<url>` tag and place a new `<loc>` tag within. This contains the direct url to the new scenario. For example:
```HTML
  ...
  <url>
    <loc>https://datamigration.microsoft.com/scenario/scenario-file-name</loc>
  </url>
</urlset>
```


## SiteConfig
Directly under `en-US` is the `siteConfig` file. This JSON file has three main sections:

### 1. questions
This section holds the questions presented to users along with the possible answers. Currently, the only two questions shown are `source` and `target`. The selection of a source and a target maps to a specific `scenario`. Generally, the most you will edit in this section is adding an option to `source`. Simply add a data source enclosed in double quotes to the `options` list, making sure that each option is followed by a comma exception the last one. For example:
```
...
"options":[
    "SQL Server",
    "Oracle",
    "DB2",
    "MySQL",
    "Sybase",
    "Access",  // a comma was added here since it was the old last item
    "Teradata"  // no comma should be here since it is the new last item in a list
],
...
```

The meaning of the fields and their expected values are as follows:
  • id
    ○ A meaningful name that is unique from all other questions
    ○ Must NOT contain spaces, numbers, or special characters (i.e. !@#$%^&\*()-\_\[]{};:'",.<>/?\|\`~)
  • text
    ○ The text of the question as displayed to the user.
  • options
    ○ The list of options of the question displayed to the user. Same rules for text (above) apply here.
  • required
    ○ If the user is required to answer this question or not (if not then it is considered to optional or advanced).
    ○ Accepts "true" or "false".
    ○ Currently, only the two questions marked as required, `source` and `target` are ever displayed. Optional questions are
      placeholders for future features.

### 2. caseStudies
This section contains case studies of how other companies have benefited from migrating to Microsoft SQL technologies. Each item in this section has a single property `filelocation` whose value references a file within the `caseStudies` folder. The value is in relation to the `caseStudies` folder so it should *_NOT_* include any part of the path from the root of the repository to the `caseStudies` folder.
```
...
  {
    "filelocation": "MigrationPlaybookContent/en-US/caseStudies/Floatel" // WRONG!
  },
  {
    "filelocation": "caseStudies/Infosys" // ALSO WRONG!
  },
  {
    "filelocation": "HollandAmerica" // CORRECT!
  }
  ...
```


## Scenarios
Some text


## Steps
Some text


## Actions
Some text


## Partners & Case Studies
Some text


## JSON
Some text


## Markdown
Some text
