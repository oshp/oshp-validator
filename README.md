# OWASP Secure Headers Project validator

[![Validate test suites](https://github.com/oshp/oshp-validator/actions/workflows/validate-tests-suite.yml/badge.svg?branch=main)](https://github.com/oshp/oshp-validator/actions/workflows/validate-tests-suite.yml)

[Venom](https://github.com/ovh/venom) test suites to validate an [HTTP security response headers](https://owasp.org/www-project-secure-headers/#div-headers) configuration against [OSHP recommendation](https://owasp.org/www-project-secure-headers/#div-bestpractices).

🎯 The objective is to provide a way to validate the configuration of non-Internet exposed applications in a flexible/portable way.

💡 You can use the provided test suites, as a foundation, to tailor it to your context.

📑 Syntax for the test suitesfile is validated using this [yamllint](https://yamllint.readthedocs.io) configuration [file](.yamllint).

# Why venom?

🤔 We chose to leverage this tool for the following reasons:

* It is free and open source.
* It does not need any installation: Standalone binary file provided but you can easily compile it if you want a full control over the binary executed.
* It is cross-platform.
* It uses a descriptive approach for a [tests suite](tests_suite.yml) and, then, do not need any code (or coding skills) to add/update a test.

# Tests suite

> **Note**: This tests suite is always synchronized with the latest OSHP recommendation.

📋 It is provided via this [single file](tests_suite.yml).

💻 [Visual Studio Code](https://code.visualstudio.com/) is used for the tests suite development. A Visual Studio Code [workspace file](project.code-workspace) is provided for the project with [recommended extensions](.vscode/extensions.json).

📐 The following parameters are supported:

| **Parameter name**         |                                                                **Description**                                                                                              | **Default value** | **Mandatory** |
|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------|---------------|
| target_site                | URL of the site for which the headers configuration must be tested.                                                                                                         | ""                | Yes           |
| internet_facing            | Boolean to specify if the tested app is currently reachable from Internet and then can be tested with the [securityheaders.com](https://securityheaders.com/) online tools. | false             | No            |
| logout_url                 | Relative path to the logout endpoint of the app. Use to test the configuration of the header "Clear-Site-Data".                                                             | ""                | No            |
| request_timeout_in_seconds | Maximum waiting time in seconds for response from the target app.                                                                                                           | 20                | No            |

# How to use it?

💻 Follow the steps below.

1. Get a [release of venom](https://github.com/ovh/venom#installing) for your platform.
2. Run one the following commands corresponding to your context:

```bash
# Using default values for "internet_facing" and "logout_url" parameters
$ venom run --var="target_site=https://mysite.com" tests_suite.yml
# Using parameter to include the results from "securityheaders.com" online tools
$ venom run --var="target_site=https://mysite.com" --var="internet_facing=true" tests_suite.yml 
# Using parameter to specify the logout page for the test of the header "Clear-Site-Data"
$ venom run --var="target_site=https://mysite.com" --var="logout_url=/logout" tests_suite.yml 
```

:eye_speech_bubble: Live usage example:

[![asciicast](https://asciinema.org/a/391137.svg)](https://asciinema.org/a/391137)

:speech_balloon: Hints:

Venom returns a code different from zero when a test fail or when you try an update and your version is the latest one. Therefore, to prevent your script to fail then add `|| true` at the end of your command.

# Reporting

This [section](https://github.com/ovh/venom#export-tests-report) of the venom documentation describes the different formats supported for the integration in a CI/CD platform.
