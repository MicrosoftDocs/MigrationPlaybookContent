# Migration Guide - Contributor Guide
The content repository for Microsoft's Migration Guide is hosted at https://datamigration.microsoft.com. This document serves as a guide for future contributors to help them better understand files, their structure, how to edit them, and how to create new ones.

1. [Folder Structure](#folder-structure-overview)
2. [SiteConfig](#siteconfig)
3. [Scenarios](#scenarios)
4. [Steps](#steps)
4. [Actions](#actions)
5. [Partners and Case Studies](#partners--case-studies)
6. [JSON](#json)
7. [Markdown](#markdown)
8. [Microsoft Open Source Code of Conduct](#microsoft-open-source-code-of-conduct)

**Note:** When you are ready to make changes, be sure you are working against the "Dev" branch. Any changes made directly to either the "PreProd" or "Prod" branches will not be recognized.

## Structural overview of the GitHub repository
The files and folders within the GitHub repository are organized in a specific structure, which must be maintained. The structure is not overly complicated and allows for a degree of flexibility. In general, files are separated into discrete folders, which makes them resuable for different scenarios.

All files except those associated with "steps" are in JSON format. Step files, which make up the bulk of the actual content of the Migration Guide, are in Markdown format. Additional information about basic rules of [JSON](#json), [step files](#steps), and Markdown format (see this [cheat sheet](#markdown)) are provided later in this document.

### Top-level folders and files
The top level of the repository contains an `en-US` folder, which includes files for the default language (United States English). All content is first being delivered in English, and any future translations will be based on the content in the `en-US` folder.

There is also a `test` folder, which is used strictly for nightly unit and availability tests. Please do not make any changes to this folder or its contents.

The top level of the repository also contains the following files:

`.gitignore` - This should be obvious and should also, obviously, be left alone.

`README.md` - The file you are currently reading.

`actionTemplate` - An example of the structure of an action file.

`caseStudyOrPartnerTemplate` - An example of the structure of a case study or partner file.

`scenarioTemplate` - A general example for the structure of a scenario file.

`siteConfigTemplate` - An example for the structure of the siteConfig file.

`sitemap.xml` - This file provides search engine robots with the important discoverable URLs of the [Migration Guide](https://datamigration.microsoft.com). If you create a new scenario, you definitely need to update this file by including a new `<url>` tag and a new `<loc>` tag, which will contain the direct URL to the new scenario. For example:
```HTML
  ...
  <url>
    <loc>https://datamigration.microsoft.com/scenario/scenario-file-name</loc>
  </url>
</urlset>
```

### Contents of the en-US folder
Within the `en-US` folder, there are two files, `<readme>` and `<SiteConfigurl>`, as well as several subfolders for specific types of content files. 

#### SiteConfig
Along with various subfolders, the `en-US` folder contans a `siteConfig` file in JSON format.  The file has three main sections:
- questions
- caseStudies
- scenarioMap

##### "questions"
This section contains the questions presented to users, together with possible answers. Currently, there are only two questions - `source` and `target`. When a user selects a specific source and target, the selection maps to a specific `scenario`. Generally, you will only edit in this section to add an option to `source` and/or `target`. Simply add a data source enclosed in double quotation marks to the `options` list, making sure that each option except the last one is followed by a comma. For example:
```
...
"options":[
    "SQL Server",
    "Oracle",
    "DB2",
    "MySQL",
    "Sybase",
    "Access",   // a comma was added here since it was the old last item
    "Teradata"  // no comma should be here since it is the new last item in a list
],
...
```
An explanation of each of the properties and its expected values are as follows:

  * id
    * A meaningful name that is unique from all other questions
    * Must NOT contain spaces, numbers, or special characters (i.e. !@#$%^&\*()-\_\[]{};:'",.<>/?\|\`~)
  * text
    * The text of the question as displayed to the user.
  * options
    * The list of options of the question as displayed to the user.
  * required
    * Whether the response to a question in required or optional.
    * Accepts "true" or "false".
    * Currently, only the two questions marked as required are `source` and `target`; optional questions are
      placeholders for future features.

##### "caseStudies"
This section contains case studies of how other companies have benefited from migrating to Microsoft SQL technologies. Each item in this section has a single property, `filelocation`, the value of which references a file within the `caseStudies` folder. The value is in relation to the `caseStudies` folder, so it should ***not*** include any part of the path from the root of the repository to the `caseStudies` folder. See the following example.
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

##### "scenarioMap"
This section maps the selection of a source and a target to an actual scenario file. The format of each line in this section is as follows:

`"source[option index]_target[option index]" : "[scenario file name]"`

Consider the following emaple:

`"source0_target0" : "sql-to-sqlserver2016"`

Based on the current `siteConfig` file, a user selecting the first option for source (since Javascript has zero-based indexes this maps to 0) and the first option for target would be directed (mapped) to the file named "sql-to-sqlserver2016."

##Other Migration Guide components
Other components of the Migration Guide include scenarios, items, steps, actions, partners, and case studies. Each component is explained in further detail in the following sections.

### Scenarios
Within the context of the Migration Guide, a *scenario* is a collection of steps that define the process of migration from one data source to one of Microsoft's database technologies (e.g SQL Server of Azure SQL).

Each scenario is defined by a specific file located in the `scenarios` folder. Each file contains all the metadata necessary to display a single scenario and everything associated with it. The content of a scenario is displayed in two sections: Business and Technical. Each of these sections is further broken down into the "steps" that a user would go through either to justify the migration (Business) or to carry it out (Technical). Each "step" is a file located in the `steps` folder, and the contents appear in Markdown format.

An explanation of each of the properties and its expected values follows:

  * displayname
    * The title of the scenario as displayed to the user. The scenario title appears as the title of the browser tab, a heading to the scenario, the heading and file name when printing (or saving to PDF), and the email subject line when opting to email the scenario to someone.
  * emailmessage
    * The body of the message accompanying a scenario that is emailed.
  * description
    * Used in the scenario page's <meta content=""> tag, description text is useful for Search Engine Optimization.
  * businesssection
    * A collection of `items`, or "steps," explaining the business justification for migrating to Microsoft SQL technologies. The `item` format is explained [below](#items).
    * The format of "step" files are explained in their own section [below](#steps)
    * In addition to `items`, the business section contains a sections for related Partners and for Case Studies.
      * These are collections of entities that point to related Partners or Case Studies.
      * Partners and Case Studies can be empty, but you must include the `[ ]` to explicitly indicate an empty array.
      * The only property is filelocation, which represents the location of the file in relation to either the `partners` or `caseStudies` folders. Do ***not*** include `partners`/`caseStudies` or any folder above it in this path.
      * The format of partner and case study files are explained in their own section [below](#partners--case-studies).
  * technicalsection
    * A collection of `items` or "steps" that explain the step-by-step process for migrating.
  * footer
    * This section is not in use, but it acts as a placeholder for a future feature.

### Items
*Items* are subsections in the Business and Technical sections. Essentially, items refer to a file containing a "step" in the process of migrating. Each `item` can optionally contain one or more `actions`, which are links either to online resources, downloadable tools, or documents.

An explanation of each of the properties and its expected values follows:

  * filelocation
    * The location of the file in relation to the `steps` folder. Do ***not*** include `steps` or any folder above it in this path.
  * actions
    * This is a collection of resources the user can take advantage of for further help with migration.
    * Actions can be empty, but you must include `[ ]` to explicity indicate an empty array.
    * Each action has two properties:
      * actiontype
        * Accepts either "forwardlink" or "download"
        * "forwardlink" directs the user to an online resource in a new browser tab.
        * "download" directs the user to download either a document or a tool.
      * filelocation
        * The location of the action file in relation to the `actions` folder. As with each occurence of "filelocation", do ***not*** include `actions` or any folder above it in the path entered here.

### Steps
*Steps* provide the "real" content that makes up the Migration Guide. Step files, which are in [Markdown](http://commonmark.org/) format, reside in their own `steps` folder. A step describes an individual concept or unit of work during the migration process. To ensure that step content is relatively easy for the user to navigate, it is recommended to minimize step content without unnecessarily splitting related work.

**Note:** To help you make sense to Markdown, we've created a cheat sheet [below](#markdown).


### Actions
Actions are external resources (tools, documents, etc.) that can be displayed along with a step (as defined in the scenario file). Action files are in [JSON format](#json) and reside within their own `actions` folder.

An explanation of each of the properties its expected values follows:

  * text
    * The text of the link as displayed to the user.
  * url
    * The URL of the external resource.

### Partners and Case Studies
*Partners* and *Case Studies* are related online documents describing how our partners are using our technologies or how a company switched to Microsoft SQL technologies, respectively. While partner and case studies files are stored in separate folders, both are covered in this  section because they are in JSON format and share the same properties.

An explanation of each of the properties and its expected values follows:

* title
  * The title of the partner/case study as displayed to the user.
* text
  * The description of the partner/case study as displayed to the user.
* url
  * The URL to the content of the partner/case study.
* logoUrl
  * The company's logo. The logo be resized to approximately 320px wide by 191px high.
* logoAltText
  * The alt text displayed to the user if the image is unavailable; also used with screen readers.


## JSON format
The detail here will not be exhaustive, but remember that JSON is pretty finicky and there's little to no wiggle room. As a result, it is recommended to use the template and to adhere to the following rules:
  * Do NOT modify field names - only modify the values.
  * Values must be within quotation marks, for example "xyz".
  * Values appear on the right-hand side of the colon, for example:
    * "propertyName" : "value"
  * Except for the last line, each line must end with a comma (,)
    * Section will be bracketed with either {} OR [], but the symbols are not interchangeable:
      * Use {} brackets for a single entity, such as a single question, item in a scenario, or an item's action.
      * Use [] brackets for a collection of entities. An example of this is questions. Each single question is within a {} but **all** the questions are within [] (separated by commas).

## Markdown format
Markdown formatting is a little more forgiving that JSON, but there are still some rules. In addition, there are several different "flavors" of Markdown. The Migration Guide handles Markdown formatting that follows the [CommonMark specification](http://commonmark.org/). That said, the following examples illustrate almost all of what you'd want to accomplish while avoiding potential issues.

### Paragraphs
**The following Markdown:**
```
This is a paragraph

This is a separate paragraph. Notice that there is an empty line (two line breaks) in between the paragraph above and this one.

This is a third paragraph.<space><space>
This is a new line in the third paragraph. Notice there are two spaces after the above line and a single line break.
```
**Will be displayed as:**

This is a paragraph

This is a separate paragraph. Notice that there is an empty line (two line breaks) in between the paragraph above and this one.

This is a third paragraph.  
This is a new line in the third paragraph. Notice there's only one line break between the two.


### Headings
**The following Markdown:**
```
# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6
```
**Will be displayed as:**

# Heading 1

## Heading 2

### Heading 3

#### Heading 4

##### Heading 5

###### Heading 6


### Emphasis
**The following Markdown:**
```
*Italics*
**Bold**
***Bold Italics***
```
**Will be displayed as:**

*Italics*  
**Bold**  
***Bold Italics***


### Links
**The following Markdown:**
```
[The text you want displayed to the user](http://microsoft.com)
```
**Will be displayed as:**

[The text you want displayed to the user](http://microsoft.com)


### Images
**The following Markdown:**
```
Markdown for images looks the same as it does for links, but image references begin with an exclamation mark.
![Image Alt Text important to be descriptive here for HIPPA and other compliance](http://commonmark.org/help/images/favicon.png)
```
**Will be displayed as:**

Markdown for images look just like links but start with an exclamation mark.

![Image Alt Text which is important for accessibility](http://commonmark.org/help/images/favicon.png)


### Lists
**The following Markdown:**
```
This is a bulleted list:  
* Bullet 1
* Bullet 2
  * Sub bullet
    * Indented even further
* Bullet 3

This is a numbered list:  
1. Item 1
2. Item 2
   1. Sub Item 1
   2. Pay attention to the alignment. Use spaces to line up the      sub item with the text of the one above.
   * You can even mix and match numbers and bullets
3. Item 3
```
**Will be displayed as:**

This is a bulleted list:  
* Bullet 1
* Bullet 2
  * Sub bullet
    * Indented even further
* Bullet 3

This is a numbered list:  
1. Item 1
2. Item 2
   1. Sub Item 1
   2. Pay attention to the alignment. Use spaces to line up the sub item with the text of the one above.
   * You can even mix and match numbers and bullets
3. Item 3


### Tables
**The following Markdown:**
```
| Column 1          | Column 2     | Column 3      |
|:----------------- |:------------:| -------------:|
| Left-aligned      | Centered     | Right-aligned |
| *Most* Markdown   | `still`      | **Works**     |

```
**Will be displayed as:**

| Column 1          | Column 2     | Column 3      |
|:----------------- |:------------:| -------------:|
| Left-aligned      | Centered     | Right-aligned |
| *Most* Markdown   | `still`      | **Works**     |

### Block quotes and code
**The following Markdown:**
```
> A block quote that has
>> A nested block quote
>>
> Inside it

A single `word` of code

`A whole line of code`

​​​​```
A block of code
that spans
multiple lines
​​​​```

```

**Will be displayed as:**

> A block quote that has
>> A nested block quote
>>
> Inside it

A single `word` of code

`A whole line of code`

```
A block of code
that spans
multiple lines
```

### Horizontal Rules
**The following Markdown:**
```
---
```
**Will be displayed as:**

---

### Inline HTML
**The following Markdown:**
```
If Markdown just can't seem to do what you want, you can always put in HTML and it should work just fine. For instance, putting a list inside a table won't work with just Markdown but does work when you put HTML inside the table.

| Column 1          | Column 2     | Column 3      |
|:----------------- |:------------:| -------------:|
| Left-aligned      | Centered     | Right-aligned |
| *Most* Markdown   | `still`      | **Works**     |
| <ul><li>First bullet</li><li>Second Bullet</li></ul> | HTML | **Works** |
| Also notice | that the pipes delineating the columns don't have to line up | <hr /><p>More HTML just to prove the point</p> |
```
**Will be displayed as:**

If Markdown just can't seem to do what you want, you can always put in HTML and it should work just fine. For instance, putting a list inside a table won't work with just Markdown but does work when you put HTML inside the table.

| Column 1          | Column 2     | Column 3      |
|:----------------- |:------------:| -------------:|
| Left-aligned      | Centered     | Right-aligned |
| *Most* Markdown   | `still`      | **Works**     |
| <ul><li>First bullet</li><li>Second Bullet</li></ul> | HTML | **Works** |
| Also notice | that the pipes delineating the columns don't have to line up | <hr /><p>More HTML just to prove the point</p> |


## Microsoft Open Source Code of Conduct
This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/). For more information, see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.
