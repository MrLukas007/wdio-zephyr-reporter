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
      domain: "yourdomain.jira.com",
      username: "username",
      password: "password",
      projectId: 1,
      cycleId: 1,
      cycleName: "My test cycle"
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

**projectId**: *number* projet number with which the tests are associated

**cycleId**: *number* cycle number with which the tests are associated

**cycleName**: *string* (optional) name of the test cycle with which the tests are associated


## References
- https://marketplace.atlassian.com/plugins/com.thed.zephyr.zapi/cloud/overview
- http://webdriver.io/guide/reporters/customreporter.html
- https://getzephyr.docs.apiary.io
