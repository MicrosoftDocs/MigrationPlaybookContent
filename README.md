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
All the files are organized in a structure that must be adhered to. It's not overly complicated and within the structure there is some freedom. With the exception of step files, everything is in JSON format. There is a section covering some [basic rules of JSON](#json). Step files take up the bulk of the actual content and are in Markdown format. We've created a [cheat sheet](#markdown) to help you. The rationale for making all these discrete files in their own folders is to make them reusable for different scenarios.

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

An explanation of each of the properties and their expected values are as follows:

  * id
    * A meaningful name that is unique from all other questions
    * Must NOT contain spaces, numbers, or special characters (i.e. !@#$%^&\*()-\_\[]{};:'",.<>/?\|\`~)
  * text
    * The text of the question as displayed to the user.
  * options
    * The list of options of the question as displayed to the user.
  * required
    * If the user is required to answer this question or not (if not then it is considered to optional or advanced).
    * Accepts "true" or "false".
    * Currently, only the two questions marked as required, `source` and `target` are ever displayed. Optional questions are
      placeholders for future features.

### 2. caseStudies
This section contains case studies of how other companies have benefited from migrating to Microsoft SQL technologies. Each item in this section has a single property `filelocation` whose value references a file within the `caseStudies` folder. The value is in relation to the `caseStudies` folder so it should ***not*** include any part of the path from the root of the repository to the `caseStudies` folder.
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

### 3. scenarioMap
This section ties the selection of a source and a target to an actual scenario file. The format of each line is as follows:

`"source[option index]_target[option index]" : "[scenario file name]"`

So the following entry:

`"source0_target0" : "sql-to-sqlserver2016"`

Breaks down like this (using the current `siteConfig`): If a user selected the first option for source (since Javascript has zero-based indexes this maps to 0) and the first option for target then they would be directed (mapped) to the file called "sql-to-sqlserver2016".


## Scenarios
This file contains all the metadata necessary to displaying a single scenario and everything associated with it. The content of a scenario is displayed in two sections: Business and Technical. Each of these sections is further broken down into "steps" that the user would go through either in justifying the migration (Business) or carrying it out (Technical). Each "step" is a file in the `steps` folder containing displayable content in Markdown format.

An explanation of each of the properties and their expected values are as follows:

  * displayname
    * The title of the scenario as displayed to the user. It is displayed as the title of the browser tab, as a heading to the scenario, the heading and file name when choosing to print (or save to PDF), and the email subject line when choosing to email the scenario to someone.
  * emailmessage
    * Used as the message body when emailing the scenario.
  * description
    * Used in the scenario page's <meta content=""> tag, useful for Search Engine Optimization.
  * businesssection
    * A collection of `items` or "steps" explaining the business justification for migrating to Microsoft SQL technologies. The `item` [format is explained below](#items).
    * In addition to `items`, the business section contains a section for related Case Studies and another section for Partners. These are explained in their own [section below](#partners--case-studies).
  * technicalsection
    * A collection of `items` or "steps" explaining the physical process of migrating.
  * footer
    * This section is not in use but acting as a placeholder for a future feature.

### Items
Items are subsections in the Business and Technical sections. Items essentially refer to a file containing a "step" in the process of migrating. Each `item` can optionally contain one or more `actions` which are either links to an onlince resource or downloadable tools or documents.

An explanation of each of the properties and their expected values are as follows:

  * filelocation
    * The location of this file in relation to the `steps` folder. Do ***not*** include `steps` or any folder above it in this path.
  * actions
    * This is a collection of resources the user can use to further help them with migration.
    * This can be empty. But be sure to include `[ ]` to explicity indicate an empty array.
    * Each action has the following two properties:
      * actiontype
        * Accepts either "forwardlink" or "download"
        * "forwardlink" means the user is directed to an online resource in a new browser tab.
        * "download" means the user will be asked to download either a document or tool.
      * filelocation
        * The location of the action file in relation to the `actions` folder. As with all times when you see "filelocation", do ***not*** include `actions` or any yfolder above it in the path you enter here.


## Steps
Steps are the meat in the Migration Playbook stew. Or, if you're a vegetarian, it's the legumes. Either way, this is where all the protein is. Steps are files containing [Markdown](http://commonmark.org/). These are split out 


## Actions
Some text


## Partners & Case Studies
Some text


## JSON
Some text


## Markdown
Some text
