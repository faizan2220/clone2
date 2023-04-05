The `node-html-markdown` package is a Node.js module that allows you to convert HTML to Markdown and vice versa. 

Here's a brief guide on how to use it:

1. Install the package using npm:  
npm install node-html-markdown
2. Require the module in your Node.js file:  
const nhm = require('node-html-markdown');
3. To convert HTML to Markdown, call the `translate` function and pass in the HTML string as an argument:  
const html = '<h1>Hello, world!</h1>';  
const markdown = nhm.translate(html);
4. To convert the HTML file to a Markdown file refer to the following code:  
const { NodeHtmlMarkdown, NodeHtmlMarkdownOptions } = require('node-html-markdown')  
const fs = require('fs');  
const nhm = new NodeHtmlMarkdown();  
const html = fs.readFileSync(`./packages/sample1.html`, 'utf8');  
const markdown = nhm.translate(html);  
fs.writeFile('packages/app/src/techdocs/myfile.md', markdown ,  function(err){});  
For readFileSync() and writeFile() we can provide desired location
  
  
## **Customizations** 

`node-html-markdown` provides **options** to customize the conversion process. 

Here's how you can use options in the code

const { NodeHtmlMarkdown, NodeHtmlMarkdownOptions } = require('node-html-markdown')
const fs = require('fs');

const options = {
  gfm: true,
  convertImgAlt: true,
  convertTableToCode: false,
  bulletListMarker: '-',
  orderedListMarker: '1.',
  headingStyle: 'atx',
  pedantic: true
}
const nhm = new NodeHtmlMarkdown(options);
const html = fs.readFileSync(`./packages/app/src/techdocs/api-page.html`, 'utf8');
const markdown = nhm.translate(html);
fs.writeFile('packages/app/src/techdocs/myfile6.md', markdown ,  function(err){});
  
  
**Listed below are a few options**

1. **`gfm` (default: `true`)**:  
   1. Set this to `false` if you want to disable GitHub Flavored Markdown support.
2. **`tables` (default: `true`)**:  
   1. Set this to `false` if you don't want to convert tables in the HTML to Markdown tables.
3. **`emoji` (default: `false`)**:  
   1. Set this to `true` if you want to enable Emoji support in the Markdown output.
4. **`breaks` (default: `false`)**:  
   1. Set this to `true` if you want to convert line breaks in the HTML to `<br>` tags in the Markdown output.
5. **`sanitize` (default: `true`)**:  
   1. Set this to `false` if you don't want to sanitize the HTML input.

  
Please refer to the following link for a detailed explanation:

[Read More](https://github.com/crosstype/node-html-markdown)

## **Observations:**

| Page                     | Link                                                                                                      | Focusing Elements      | Observation                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------------------ | --------------------------------------------------------------------------------------------------------- | ---------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Page1: API Standard      | [API Standards](https://confluence.bottomline.tech/display/BTAC/API+Standard+-+RESTful+Quick+Start+Guide) | Code blocks            | The code block was not converted properly**Reason:**Code block syntax is missing in the exported HTML file.when added the code tag in the HTML file, nhm was able to generate the code block**Fault:** Exported HTML file from the confluence                                                                                                                                                                                |
| Page2: Access Control    | [Access Control](https://confluence.bottomline.tech/display/SPFM/Access+control)                          | Overall Page Structure | Spaces present on the page were missing in the markdown fileThe html file export also had spacesNHM couldn't get the exact page structure**Tried:**Setting options → "break: true "added multiple <br> tags but nhm is not considering the <br> tags while conversion**Fault:** Node-html-markdown converter                                                                                                                 |
| Page3: Expertise Offered | [Expertise Offered](https://confluence.bottomline.tech/display/SPFM/Expertise+Offered-+API+Management)    | Large Table            | The table was converted to markdown syntax successfully                                                                                                                                                                                                                                                                                                                                                                      |
| Page4: Build Strategy    | [Build Strategy](https://confluence.bottomline.tech/display/SPFM/Build+Strategy)                          | Videos                 | In the confluence page videos were added using a widget connectorExported Html file used <iframe> tag to insert videosNHM was not able to add videos and completely ignored the <iframe> tag**Reason:**Markdown doesn't have any syntax for inserting videos we can use HTML <iframe> tag to insert videos in a markdown fileBut Backstage techdocs doesn't support HTML tags in markdown files**Fault:** Backstage techdocs |
| Page5: Implementation    | [Implementation](https://confluence.bottomline.tech/display/SPFM/Implement+on-behalf+capability)          | Content Alignment      | Few images, code blocks and content were center alignedAfter conversion, they were aligned to the left **Reason:**Markdown does not support alignment for images or text, so you will need to use HTML or CSS to achieve this effect.Backstage techdocs doesn't support HTML tags in markdown filesEven in the backstage docs, they haven't provided any alignment.**Fault:** Backstage Techdocs                             |

## **Note:**

* Some issues like heading being inserted in the above table or paragraph, adding extra boxes and other issues of pandoc were working fine with NHM.
* Confluence supports multiple macros but we were not able to use them in markdown files.

## **FAQs:**

**why we are using writeFile() method instead of writeFileSync()?**

* writeFileSync() is synchronous, meaning it will block the main thread until the file is written
* writeFile() is asynchronous, meaning it won't block the main thread while the file is being written

**What is a widget connector?**

* The Widget Connector is a feature in Atlassian Confluence that allows you to embed content from external sources, such as videos, images, and social media feeds, directly into a Confluence page.

**Which tag is used to insert media in an HTML file?**

* <iframe> HTML tag is used to add media
* The <iframe> HTML tag and the Widget Connector in Confluence are similar, allowing you to embed external content within a web or Confluence page.

  