# ArchiDoc 

Is a sample project for generating documentation from AsciiDoc files intended for IT Professional who likes to work with documentation-as-code approach.

## Features

* ADR - Architecture Decision Records
* PlantUML - diagrams
* AsciiDoc - documentation
* Confluence - integration

## Examples

There is an example provided based on the ArchiMetal project [ArchiMetal.archimate](ArchiMetal.archimate).

Sample document generated from archimate project is available in [documents/architecture](documents/architecture), including output PDF [Document.pdf](documents%2Farchitecture%2FDocument.pdf).

Another example [cr1.pdf](documents/cr/cr1/cr1.pdf)

## Ways to generate documentation

Script is a modification of @rich-biker script https://gist.github.com/rich-biker/9a3c86c5a576ce0d8639856f3ee81651 which creates Markdown files instead of AsciiDoc.

Create your Archi project. Install JArchi plugin and copy scripts from `jarchi` folder.

Script [AsciiDocTemplate.ajs](jarchi%2FExport%20To%2FAsciiDocTemplate.ajs) can be run on specially crafted archi view of document structure to generate AsciiDoc files.

Use groups to create section of documents. You can nest them to create sub-sections. Connect them with trigger relationships to create a document structure, for example:
![example-docs.png](readme_files%2Fexample-docs.png)

Script has some flags which you place on groups in a View of document structure, which can control how your document will be generated:

```
"Overwrite": true, //if false then the file will not be overwritten if exists
"CreateChildAdoc": true, // if true will generate a separate adoc file for this group
"FlatThisGroup": false, // if true will not create a section for this group, but will still process the views
"IncludeDiagram": true, // if true, will include the view's diagram
"IncludeDocumentation": true, // if true, will include the view's documentation text (which itself can have markdown, by the way)
"IncludeViewElements": true, // if true, will include a catalogue of the view's elements
"IncludeProperties": false, // if true, will include the "properties" field in a catalogue of elements from a view
"CreateSectionPerView": false, // if true, will create an individual section for each view in a group,
"IncludeElementsWithoutDocumentation": false, // if true, will include elements without documentation in the list of elements,
"GroupElementAsInView": false, // if true, will group element in the groups as in the view
"FilterViewElements": [] // if set, will only include elements of the specified types in the list of elements
```

## Build

```
gradlew documents:asciidoctorPdf
```
or
```
gradlew adr:asciidoctorPdf
```

Or build html version
```
gradlew documents:asciidoctor
```

Or selected directory
```
gradle documents:asciidoctorPdf -DdocDir="./documents/cr/cr1"
```

## Creating Word document

* install pandoc https://github.com/jgm/pandoc/releases/
* install rsvg-convert (for windows https://sourceforge.net/projects/tumagcc/)
  * extract it to any directory and add it to PATH 
* generate dockbook from asciidoctor
  ```
  gradlew documents:asciidoctor
  ```
* go to the directory with the document `cd build/docs/asciidoc/...`, where the `<Document>.xml` file should be
* convert to docx `pandoc --from docbook --to docx --output Document.docx "<Document>.xml"`

You can use IntelliJ IDEA plugin to automate the process. However, you still need to install pandoc and rsvg-convert. If the plugin hangs, it means you don't have rsvg-convert on PATH. (https://intellij-asciidoc-plugin.ahus1.de/docs/users-guide/features/advanced/creating-docx.html)

## Hints for confluence exports

* use only english characters in plantuml file names
* don't use formatting in captions of tables and images

## Notes

Add `-Dfile.encoding=UTF-8` to Idea's VM options to avoid encoding issues.