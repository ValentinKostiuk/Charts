# Create new application
## PUT `/applications`
### request body
```json
{
  "name": "appName"
}
```
### response
```json
{
  "name": "appName",
  "id": 123
}
```

# Add test run
## PUT `/applications/<appName>/testRuns/`
### request body
```json
{
  "attributes": {
    "branch": "tested application branch name"
  }
}
```
### response
```json
{
  "id": 567,
  "attributes": {
    "branch": "branchName"
  }
}
```

# Add test result
## PUT `/applications/<appName>/testRuns/<testRunId>/results`
### request body
```json
{
  "results": [
    {
      "testName": "test1Name",
      "result": "success", //[success|fail|ignored|inconclusive]
      "testType": "integration", //[unit|component|integration]
      "displayName": "test1DisplayName",
      "duration": 4637,
      "OS": "OS name",
      "Browser": "SomeBrowser",
      "parameters": "parametrized tests parameters string"
    },
    {
      "testName": "test2Name",
      "result": "success",
      "testType": "integration",
      "displayName": "test2DisplayName",
      "duration": 5749,
      "OS": "OS name",
      "Browser": "SomeBrowser",
      "parameters": "parametrized tests parameters string"
    }
  ]
}
```

# Get test run results
## GET `/applications/<appName>/testRuns/<testRunId>/results`
### response
```json
{
  "results": [
    {
      "testName": "test1Name",
      "result": "success", //[success|fail|ignored|inconclusive]
      "displayName": "test1DisplayName",
      "testType": "integration",
      "duration": 4637,
      "OS": "OS name",
      "Browser": "SomeBrowser",
      "parameters": "parametrized tests parameters string"
    },
    {
      "testName": "test2Name",
      "isSuccess": "fail",
      "displayName": "test2DisplayName",
      "testType": "integration",
      "duration": 5749,
      "OS": "OS name",
      "Browser": "SomeBrowser",
      "parameters": "parametrized tests parameters string"
    }
  ]
}
```

# Get test run summary
## GET `/applications/<appName>/testRuns/<testRunId>/summary`
### response
```json
{
  "totalDuration": 47503485,
  "meanDuration": 1233,
  "medianDuration": 456,
  "totalTest": 264,
  "testsSucceed": 120,
  "testsFailed": 120,
  "testsInconclusive": 20,
  "testsIgnored": 4
}
```

# Get app tests
All tests created implicitly
## GET `/applications/<appName>/tests/`
### response
```json
{
  "tests": [
    {
      "id": 93765,
      "testName": "test1Name",
      "testType": "integration"
    }
  ]
}
```

# Get test summary
## GET `/applications/<appName>/tests/<testId>/summary`
### response
```json
{
  "tests": [
    {
      "id": 93765,
      "testName": "test1Name",
      "testType": "integration",
      "totalRuns": 134,
      "meanDuration": 23,
      "medianDuration" 34,
      "failsRatio": 0.34, //how frequently fails in all cases
    }
  ]
}
```

# *Drill down into statistics*
Getting statistics of tests runs can be done using **filters**
Those filters will describe restrictions which should be applied
Firlters can be applied to filter test runs statistics, for example filter all test runs for branch A, get top 10.
Also filters can be applied to get statistics for single test, to view history of runs. Filter for test can be done by any test attribue: neme, OS, Browser.

How can we select summary for all attributes which exist for current test. For example we want to know on which OS and Browsers test was run. (?)
