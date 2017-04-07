# api documentation for  [node-jsx (v0.13.3)](https://github.com/petehunt/node-jsx)  [![npm package](https://img.shields.io/npm/v/npmdoc-node-jsx.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-node-jsx) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-node-jsx.svg)](https://travis-ci.org/npmdoc/node-npmdoc-node-jsx)
#### transparently require() jsx from node

[![NPM](https://nodei.co/npm/node-jsx.png?downloads=true)](https://www.npmjs.com/package/node-jsx)

[![apidoc](https://npmdoc.github.io/node-npmdoc-node-jsx/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-node-jsx_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-node-jsx/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-node-jsx/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-node-jsx/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Pete Hunt"
    },
    "bugs": {
        "url": "https://github.com/petehunt/node-jsx/issues"
    },
    "dependencies": {
        "jstransform": "11"
    },
    "description": "transparently require() jsx from node",
    "devDependencies": {
        "jasmine-node": "1.12.0",
        "react": "^0.13.2"
    },
    "directories": {},
    "dist": {
        "shasum": "3d0568c10601c72f154e872d0e6b9cdf0a6dc4f8",
        "tarball": "https://registry.npmjs.org/node-jsx/-/node-jsx-0.13.3.tgz"
    },
    "gitHead": "169d038c398d70ac507aa63ba54a5dd00559f370",
    "homepage": "https://github.com/petehunt/node-jsx",
    "license": "Apache 2",
    "main": "index.js",
    "maintainers": [
        {
            "name": "floydophone",
            "email": "floydophone@gmail.com"
        }
    ],
    "name": "node-jsx",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/petehunt/node-jsx.git"
    },
    "scripts": {
        "test": "jasmine-node node-jsx.spec.js"
    },
    "version": "0.13.3"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module node-jsx](#apidoc.module.node-jsx)
1.  [function <span class="apidocSignatureSpan">node-jsx.</span>install (options)](#apidoc.element.node-jsx.install)



# <a name="apidoc.module.node-jsx"></a>[module node-jsx](#apidoc.module.node-jsx)

#### <a name="apidoc.element.node-jsx.install"></a>[function <span class="apidocSignatureSpan">node-jsx.</span>install (options)](#apidoc.element.node-jsx.install)
- description and source-code
```javascript
function install(options) {
  if (installed) {
    return;
  }

  options = options || {};

  // Import everything in the transformer codepath before we add the import hook
  jstransform.transform('', options);

  require.extensions[options.extension || '.js'] = function(module, filename) {
    if (!options.hasOwnProperty("react"))
      options.react = true;

    var src = fs.readFileSync(filename, {encoding: 'utf8'});
    if (typeof options.additionalTransform == 'function') {
      src = options.additionalTransform(src);
    }
    try {
      src = jstransform.transform(src, options).code;
    } catch (e) {
      throw new Error('Error transforming ' + filename + ' to JS: ' + e.toString());
    }
    module._compile(src, filename);
  };

  installed = true;
}
```
- example usage
```shell
...

# node-jsx

Transparently 'require()' jsx from node.

## Usage

'require('node-jsx').install()'

If you want to use a different extension, do:

'require('node-jsx').install({extension: '.jsx'})'

If you want to couple with an additional transform (such as CoffeeScript), do:
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
