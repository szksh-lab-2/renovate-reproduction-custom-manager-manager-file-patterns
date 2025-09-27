# renovate-reproduction-custom-manager-manager-file-patterns

## Problem

Accounding to the document, customManager requires `managerFilePatterns`.

https://docs.renovatebot.com/modules/manager/regex/#required-fields

> Required Fields
> The first two required fields are managerFilePatterns and matchStrings:
> 
> managerFilePatterns works the same as any manager
> matchStrings is a regex custom manager concept and is used for configuring a regular expression with named capture groups

But `renovate-config-validator` fails if managerFilePatterns is used in customManager.

## How To Reproduce

- [renovate.json5](renovate.json5)
- [workflow](.github/workflows/test.yaml)

```sh
renovate-config-validator --strict renovate.json5
```

## Expected

The validation succeeds.

## Actual

The validation fails.

```
 INFO: Validating renovate.json5
ERROR: Found errors in configuration
       "file": "renovate.json5",
       "errors": [
         {
           "topic": "Configuration Error",
           "message": "Custom Manager contains disallowed fields: managerFilePatterns"
         },
         {
           "topic": "Configuration Error",
           "message": "Invalid configuration option: customManagers[0].managerFilePatterns"
         }
       ]
```

## Note

https://docs.renovatebot.com/configuration-options/#custommanagers

In this document, `customManagers` doesn't have `managerFilePatterns`.

But if I remember correctly, `managerFilePatterns` should have worked before.
