### Bluemix Docs for Knowledge Kits

#### Development
The documentation building process at its core relies on a Markdown-to-HTML generator used by Bluemix based on npm package called [marked-it-cli](https://www.npmjs.com/package/marked-it-cli) and Bluemix-specific extensions to that package. 

To install the package:
```bash
npm install -g marked-it-cli
```

To install the extensions:

-   Go [here](https://github.ibm.com/Bluemix/docs/tree/staging/developing/markdown) and copy `header.txt` and `footer.txt` into your `marked-it-cli` directory (found wherever you have global node modules saved)
-   Go [here](https://github.ibm.com/Bluemix-Docs/docs-build/blob/master/markdown/cloudoeconrefs.yml) and copy `cloudoeconrefs.yml` into your `marked-it-cli` directory 

Once you have that in place, you can start with the appropriate markdown using some of the [templating provided](https://github.ibm.com/Bluemix/docs/tree/staging/developing/content-kit). The first one to take a look at would be the `toc-template` used for the `toc` file where all navigation-related information is provided. 


To test whether markdown has been properly converted, with all the templating and formatting required, you will have to try the build out locally with the `marked-it-cli` package by issueing a command like this from the root directory:


***Note:** replace `$YOUR_NODE_MODULES` with the appropriate path to where you have your global node modules located. `example/accessibilityExt.js` and `example/xmlTocExt.js` should have come with the `marked-it-cli` package.



```bash
marked-it-cli . \
--output=../generated_html/ \
--header-file=$YOUR_NODE_MODULES/marked-it-cli/header.txt \
--footer-file=$YOUR_NODE_MODULES/marked-it-cli/footer.txt \
--conref-file=$YOUR_NODE_MODULES/marked-it-cli/cloudoeconrefs.yml \
--extension-file=$YOUR_NODE_MODULES/marked-it-cli/example/accessibilityExt.js \
--extension-file=$YOUR_NODE_MODULES/marked-it-cli/example/xmlTocExt.js \
--toc-xml \
--overwrite —verbose
```



#### Deployment
To be able to push up to this repository connected to Bluemix stage or prod, you have to get permission by opening a build request. This build request for this repo has already been opened in the [Bluemix/Documentation-content repo](https://github.ibm.com/Bluemix/Documentation-content/issues/1073). Request permission in that issue if necessary.

Once you have read/write permission, you can deploy through this repo. Merging anything into the `staging` branch will trigger a build for your documentation on console.stage1.bluemix.net and merging anything into `master` will trigger a build on console.bluemix.net.

Once deployed, the live docs can be found here:

-   Stage 
console.stage1.bluemix.net/docs/services/knowledge-kits/index.html
-   Production
console.bluemix.net/docs/services/knowledge-kits/index.html



#### Resources
For much more in depth documentation on creating Bluemix Documentation, including different levels of compliance required for different levels  of release, please visit: [https://dev-console.stage1.bluemix.net/docs/developing/writing/index.html#get-started](https://dev-console.stage1.bluemix.net/docs/developing/writing/index.html#get-started)

For more on `marked-it-cli` installation and usage see: https://console.stage1.bluemix.net/docs/developing/markdown/setup.html#set-up-your-markdown-environment

For specifc Markdown requirements, see: https://dev-console.stage1.bluemix.net/docs/developing/markdown/create.html#validmarkdown


