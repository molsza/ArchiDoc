# ArchiDoc 

Is a sample project for generating documentation from AsciiDoc files intended for IT Professional who likes to work with documentation-as-code approach.

## Features

* ADR - Architecture Decision Records
* PlantUML - diagrams
* AsciiDoc - documentation
* Confluence - integration

## Ways to generate documentation

Create your Archi project. Install JArchi plugin and copy scripts from `jarchi` folder.

Script [AsciiDocTemplate.ajs](jarchi%2FExport%20To%2FAsciiDocTemplate.ajs) can be run on specially crafted archi view of document structure to generate AsciiDoc files.

Use groups to create section of documents. You can nest them to create sub-sections. Connect them with trigger relationships to create a document structure, for example:
![example-docs.png](readme_files%2Fexample-docs.png)

## Hints for confluence exports

* use only english characters in plantuml file names
* don't use formatting in captions of tables and images  

## Notes

Add `-Dfile.encoding=UTF-8` to Idea's VM options to avoid encoding issues.
