# newman-reporter-testrail

Improved TestRail reporter for Newman
    - test cases filtering capability;
    - reading options from reporterOption;
    - added 'host' parameter;
    - added 'errors' logging mode.

Based on the original https://github.com/billylam/newman-reporter-testrail.

## Installation

`npm install git+https://github.com/romanukhaav/newman-reporter-testrail.git -g`

## Usage

### Prefix all test assertions you wish to map with the test number.
Include the letter C. You may map more than one test case to an assertion.
```
pm.test("C226750 C226746 Status code is 200", function () {
    pm.response.to.have.status(200);
});
```

### Export the following environment variables.

#### REQUIRED Environment Variables

| Name | Description |
| --- | --- |
| TESTRAIL_DOMAIN | TestRail domain.  Do not include protocol. |
| TESTRAIL_USERNAME | TestRail username / email. |
| TESTRAIL_APIKEY | TestRail [API key](http://docs.gurock.com/testrail-api2/accessing#username_and_api_key). |
| TESTRAIL_PROJECTID | TestRail project id. |

#### OPTIONAL Environment Variables
| Name | Description |
| --- | --- |
| TESTRAIL_RUNID | TestRail run id.  Update a specific run instead of creating a new run.  Can use the string "latest" to update latest run. |
| TESTRAIL_SUITEID | TestRail suite id.  Mandatory in multi-suite projects.  Do not use in single-suite projects. |
| TESTRAIL_MILESTONEID | Milestone to link test to. |
| TESTRAIL_VERSION | Version of API tested. |
| TESTRAIL_TITLE | Title of test run to create. |
| TESTRAIL_INCLUDEALL | Whether to include all tests in run, regardless of whether actually run by Newman.  Defaults to true. |
| TESTRAIL_CUSTOM_* | A fixed testrail field, where * is the field key |
| TESTRAIL_LOGGING | Output logging.  Options are full, headers, none.  Defaults to full. |

You can use [direnv](https://github.com/direnv/direnv) to easily maintain directory-specific options.

You may also set some or all of these variables using bash exports or by declaring directly in the run command.

### Run newman with the reporter option
Reporter option can be set as environment variables or from reporter options arguments
`-r testrail`

Example for environment variables:

```
TESTRAIL_DOMAIN=example.testrail.com TESTRAIL_USERNAME=exampleuser 
TESTRAIL_APIKEY=yourkey TESTRAIL_PROJECTID=99 TESTRAIL_TITLE="Dev-API Regression" 
newman run my-collection.postman_collection.json -r testrail,cli
```

Example for reporterOptions:
```
 newman run my-collection.postman_collection.json -r cli,testrail \
--reporter-testrail-host 'https://testrail.domain.com' \
--reporter-testrail-username 'username@domain.com' \
--reporter-testrail-password 'password' \
--reporter-testrail-projectId 'testrail_project_id' \
--reporter-testrail-suiteId 'testrail_suite_id' \
--reporter-testrail-title 'Automation run'  \
--reporter-testrail-includeAll
```
