# OWASP Secure Headers Project validator

[Venom](https://github.com/ovh/venom) test suites to validate an [HTTP security response headers](https://owasp.org/www-project-secure-headers/#div-headers) configuration against [OSHP recommendation](https://owasp.org/www-project-secure-headers/#div-bestpractices).

The objective is to provide a way to validate the configuration of non-Internet exposed application.

# Why Venom?

We chose to leverage this tool for the following reasons:

* It is free and open source.
* It does not need any installation (standalone binary file).
* It is cross-platform.
* It uses a descriptive approach for a [tests suite](tests_suite.yml) and then do not need any code (or coding skills) to add/update a test.

# Tests suite

> This tests suite is always synchronized with the latest OSHP recommendation.

It is provided via this [single file](tests_suite.yml).

The following parameters are supported:

| **Parameter name** |                                                                **Description**                                                                | **Default value** | **Mandatory** |
|------------------|---------------------------------------------------------------------------------------------------------------------------------------------|-----------------|-------------|
| target_site        | URL of the site for which the headers configuration must be tested.                                                                           | ""                | Yes           |
| internet_facing    | Flag (`true` or `false` value) to specify if the tested app is currently reachable from Internet and then can be tested with the [securityheaders.com](https://securityheaders.com/) online tools.  | false             | No            |
| logout_url         | Relative path to the logout endpoint of the app. Used to test the configuration of the header "Clear-Site-Data".                               | ""                | No            |

# How to use it?

Follow the steps below.

1. Get a [release of Venom](https://github.com/ovh/venom/releases) for your platform.
2. Run one the following commands corresponding to your context:

```bash
# Using default values for "internet_facing" and "logout_url" parameters
$ venom run --var="target_site=https://mysite.com" tests_suite.yml
# Using parameter to include the results from "securityheaders.com" online tools
$ venom run --var="target_site=https://mysite.com" --var="internet_facing=true" tests_suite.yml 
# Using parameter to specify the logout page for the test of the header "Clear-Site-Data"
$ venom run --var="target_site=https://mysite.com" --var="logout_url=/logout" tests_suite.yml 
```

Live usage example:

[![asciicast](https://asciinema.org/a/391137.svg)](https://asciinema.org/a/391137)


