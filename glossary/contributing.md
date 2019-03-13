---
keywords: Contributing
summary:  Howto contribute to this documentation.
icon:     /images/icon_markdownpanel
---

This documentation is based on the `hise_documentation` repository on [GitHub](http://github.com/christophhart/hise_documentation/). 
It uses the Markdown files from there and merges it with autogenerated API references in order to keep the amount of boilerplate documentation as low as possible.

If you would like to contibute to this documentation, the best way is to pull the repository, make edits and then submit a pull request.

## Setup

For the normal user, the documentation will be created from two binary files, `Content.dat` and `Images.dat`, which will be 
periodically updated and fetched from the server on HISE startup.

If you want to edit the documentation, you will have to bypass this and use the markdown files directly. In order to do so, you must:

1. Clone this repository `http://github.com/christophhart/hise_documentation.git`
3. Point the markdown editor to the folder (**Settings -> Doc Settings -> Doc Repository**), then restart HISE.

> The editor will autogenerate certain elements like the scripting API and the HISE module reference. Make sure that you have compiled the latest version from the repository when you edit something in there.

Alternatively, you can just edit the files directly on github and make pull requests there, but then you miss out all the nice features of the editor.

## Directory structure

The directory structure in the repository will be used for sorting the content and create the HTML folder hierarchy. However it will process the directory names and remove trailing numbers for the links.


## Editing

## The Markdown Language

The HISE documentation uses Markdown, which is a pretty standardardised markup language. There are a few customizations to the language (also the Markdown renderer in HISE is not 100% standard compliant, so please use this reference as guideline.

### Text formatting

Headline: `### headline` (number of `#` marks the level)  
Bold: `**bold**` = **bold**  
Newline: two spaces  
Code: surround with `this`  
Link: `[Google](https://google.com)` = [Google](https://google.com)

### Paragraphs

`> This is a comment`
> This is a comment  

`- bullet point`

- bullet point

`1. numbered list`
1. Numbered list

### Images

`![ImageName](imageURL)` = shows a image

> If you want to embed local images, use the image creation tool - this will automatically copy the local file into the correct subfolder of the repository folder and create a correct relative link.


### Tables

Tables are defined using the standard Markdown syntax with the addition that you can define a fixed column width by adding `:#px` at the end of the `--` line definitions.  
This is useful for when using tables to display icons / shortcuts.


```
| First row | Second Row |
| ---:120px | ------ |
| cell 1 | cell 4 |
| cell 2 | cell 3|
```

| First row | Second Row |
| ---:120px | ------ |
| cell 1 | cell 4 |
| cell 2 | cell 3|

> The table parser in HISE is more strict than the usual parser. In order to make sure that the table is rendered correctly, use the Table generator in the editor.



### Links

The documentation uses relative links for internal links, but can also have URL links to link to external websites. 
Relative links will always start with `/`. 

> Use the link creation tool to create links that are guaranteed to work.

## Indexing / metadata

In order to build a index for the search engine, every markdown file needs a YAML header in the [Front Matter](https://jekyllrb.com/docs/front-matter/) format. You need at least two items, `keyword` and `summary`.

```
---
keyword: - Keyword 1
         - Keyword 2
summary:   A summary of the content in the file.
---
```

> If you create a new file in the editor, it will create a YAML header template for you.

There are a few content types which use additional metadata defined in this header (eg. the HISE module reference files). If you want to edit these files, take a look at the existing ones and follow their example.