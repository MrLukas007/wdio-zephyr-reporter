#Zephyr Reporter for Webdriver.io

Pushes test results into a Zephyr test cycle.
Forked from [wdio-testrail-reporter](https://github.com/oxynade/wdio-testrail-reporter)

## Installation

```shell
$ npm install wdio-zephyr-reporter --save-dev
```

## Usage
Ensure that your zephyr installation API is enabled and generate your API keys. See https://marketplace.atlassian.com/plugins/com.thed.zephyr.zapi/cloud/overview

Add reporter to wdio.conf.js:

```Javascript
let WdioZephyrReporter = require('./packages/wdio-zephyr-reporter/lib/wdio-zephyr-reporter');

...

    reporters: ['spec', WdioZephyrReporter],
    reporterOptions: {
        zephyr: {
            domain: "yourdomain.jira.com",
            username: "username",
            password: "password",
            projectId: 1,
            projectName: "FSA",
            cycleId: 12,
            cycleName: "Release 0.0.1",
            folderId: 123,   
            folderName: "Patch 0.0.1a"   
        }
    }
```


Mark your test names with the Ids of your Zephyr tests. Ensure that your ids are well distinct from test descriptions.
 
```Javascript
it("A-123 Authenticate with invalid user", . . .
it("Authenticate a valid user A-321", . . .
```

Only passed or failed tests will be published. Skipped or pending tests will not be published resulting in a "Unexecuted" status in zephyr test cycle.

## Options

**domain**: *string* domain name of your Jira instance where Zephyr and ZAPI are installed

**username**: *string* user under which the test results will be updated (e.g. jenkins or ci)

**password**: *string* password or API token for user

**projectId**: *number* (optional) project number with which the tests are associated

**projectName**: *string* project name with which the tests are associated. It must be unquie accross the given JIRA domain

**cycleId**: *number* (optional) cycle number which contains the tests to be executed

**cycleName**: *string* name of the test cycle which contains the tests to be executed. It must be unique within the given project

**folderId**: *number* (optional) folder number which contains the tests to be executed

**folderName**: *string* (optional) name of the folder which contains the tests to be executed. It must be unique within the given cycle


## References
- https://marketplace.atlassian.com/plugins/com.thed.zephyr.zapi/cloud/overview
- http://webdriver.io/guide/reporters/customreporter.html
- https://getzephyr.docs.apiary.io
