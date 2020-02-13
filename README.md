# EdgeWorker cdaley-demo

An Akamai EdgeWorker that provides the function of:

```quote
things
```

## Structure

The EdgeWorker has the following structure:

* `src` - the location of your main.js and bundle.json.  All additional modules should go here.
* `test` - unit tests

## Running Tests

Testing is provided via the [Jest](https://jestjs.io/) framework.
To run you unit tests, execute the following command from the command line:

```
npm test
```

This will run all tests in the `test` directory following the `Jest` conventions.  If you want more tests, name them in the pattern *.test.js.

A good overview of using Jest can be found [here](https://flaviocopes.com/jest/).

### Dependencies
There are a a couple of modules that are provided when deploying an EdgeWorker:  cookies and url-search-params.  These are documented on the developer.akamai.com site.  Since the packages are not available in npm, Jest mocks are provided to be able to control what is going on with the modules.

These mocks are provided using [manual mocks](https://jestjs.io/docs/en/manual-mocks) and allow for user control of their functions.  Its not perfect, but it will have to do for now.

## Deployments

Deployments can be done easily through the Akamai CLI (provided it is installed).  The following commands describe the basic workflow for handling your EdgeWorker.

### Uploading Your Bundle
The following commands should be run from the workspace root.

#### Uploading the src directory directly
This command will upload the source directory and handle creation of the code bundle.
```
akamai edgeworkers upload --codeDir ./src 345345
```

#### Createing the bundle and uploading manually
This example will upload the created bundle
```
mkdir -p out && tar -czvf ./out/bundle.tgz -C src/ .
akamai edgeworkers upload --bundle ./out/bundle.tgz 345345
```

### Checking the status of your bundle
Check the status of the uploaded bundle.
```
akamai edgeworkers status 345345
```

### Activate the bundle to staging
To use this command, you will need to enter the version number that is in the bundle.json.
```
akamai edgeworkers activate staging 345345 {version}
```

### Activate the bundle to production
Why wait for staging when you can YOLO your way directly to production?  That sounds like a great idea.  Don't forget what your current version is.
```
akamai edgeworkers activate production 345345 {version}
```


## Changelog

Insert some details about changes in your EdgeWorker here!