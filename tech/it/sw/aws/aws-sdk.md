# Overview

- General guide for SDKs and Tools
    + https://docs.aws.amazon.com/sdkref/latest/guide/overview.html
- Java
    + https://docs.aws.amazon.com/sdk-for-java
- JavaScript
    + https://docs.aws.amazon.com/sdk-for-javascript
- Python
    + https://docs.aws.amazon.com/pythonsdk
- Code examples
    + https://github.com/awsdocs/aws-doc-sdk-examples
- Toolkit for IDEs
    + JetBrains
        * https://docs.aws.amazon.com/toolkit-for-jetbrains/latest/userguide/welcome.html
        * More powerful than the toolkit for Visual Studio Code
    + Visual Studio Code
        * https://docs.aws.amazon.com/toolkit-for-vscode/latest/userguide/welcome.html
- AWS Encryption SDK
    + https://docs.aws.amazon.com/encryption-sdk/latest/developer-guide/introduction.html

# AWS SDK Maintenance and Support

## Maintenance policy

- AWS SDK major version life-cycle
    + Developer Preview
    + General Availability (GA)
    + Maintenance Announcement
    + Maintenance
    + End-of-support
- Current major versions support matrix
    + https://docs.aws.amazon.com/sdkref/latest/guide/version-support-matrix.html

# Configuration

## Introduction

- To interact with AWS service APIs, we need to configure the AWS SDK
  with
    + Credentials information
    + Other configuration details: AWS region, endpoints, etc.
- Some common credential providers
    + Environment variables: `AWS_ACCESS_KEY`, `AWS_SECRET_ACCESS_KEY`,
      etc.
    + `config` and `credentials` files
    + etc.
- Guide to set up credentials for common platforms
    + https://docs.aws.amazon.com/sdkref/latest/guide/supported-sdks-tools.html
    + Java
        * v2: https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.html
        * v1: https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html
        * Initialize a new service client without supplying the
          provider, then the default provider is used. (Recommended for
          Lambda)

## Shared `config` and `credentials` files

- Both `~/.aws/config` and `~/.aws/credentials` are plaintext files that
  contain only ASCII characters (UTF-8 encoded).
    + They take the form of what are generally referred to as `INI
      files`.
    + https://wikipedia.org/wiki/INI_file
- The shared AWS config and credentials files contain a set of profiles.
    + A profile is a set of configuration values that can be referenced
      from the SDK/tool using its profile name.
    + Configuration values are attached to a profile in order to
      configure some aspect of the SDK/tool when that profile is used.
- As a general rule, any value that you can place in the shared
  `credentials` file can alternatively be placed in the shared `config` file
    + The reverse isn't true; only a few settings can be placed in the
      `credentials` file.
    + As a security best practice, we recommend that you keep any
      sensitive values, such as access key IDs and secret keys, in the
      separate `credentials` file. This way, you can provide separate
      permissions for each file, if necessary.

### Profiles

- The `[default]` profile contains the values that are used by an SDK or
  tool operation if a specific named profile is not specified.
- Set a named profile that you want to use through your SDK code or AWS
  CLI commands.
    + Alternatively, you can use the environment variable `AWS_PROFILE`
      to specify which profile's settings to use.

```bash
export AWS_PROFILE="my_named_profile"
```

### Format of the `config` file

- The `config` file must be a plaintext file that uses the following format:
    + Each section begins with the profile name in square brackets `[ ]`.
    + All entries in a section take the general form of `setting-name=value`.
- Create a named profile

```
[profile developers]
...settings...
```

- Some settings have their own nested group of subsettings, such as the
  s3 setting and subsettings in the following example.
    + Associate the subsettings with the group by indenting them by one
      or more spaces.

```
[profile testers]
region = us-west-2
s3 =
    max_concurrent_requests=10
    max_queue_size=1000
```

### Format of the `credentials` file

- The section names don't begin with the word profile. Use only the
  profile name itself between square brackets.

```
[developers]
...settings...
```

# Config and auth settings reference

- https://docs.aws.amazon.com/sdkref/latest/guide/settings-reference.html

## Standardized credential providers

- https://docs.aws.amazon.com/sdkref/latest/guide/standardized-credentials.html

## Standardized features

- https://docs.aws.amazon.com/sdkref/latest/guide/standardized-features.html

# AWS Java SDK v2

- Migration from v1:
    + https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/migration.html
- What's new
    + You can configure your own HTTP clients
        * https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/http-configuration.html
    + Async clients are now tryly nonblocking and return
      `CompletableFuture` objects
        * https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/asynchronous.html
    + Operations that return multiple pages have autopaginated responses
        * https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/pagination.html
    + SDK Lambda Start Time Performance improvements
        * https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/lambda-optimize-starttime.html
    + New a new shorthand method for creating requests
        * `dynamoDbClient.putItem(request -> request.tableName(TABLE))`
- Using Credentials and Regions default providers
    + Credentials: https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/credentials.html#credentials-chain
    + Region: https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/region-selection.html#automatically-determine-the-aws-region-from-the-environment
- Exception handling
    + https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/handling-exceptions.html
- Logging
    + https://docs.aws.amazon.com/sdk-for-java/latest/developer-guide/logging-slf4j.html

# AWS Java SDK v1


