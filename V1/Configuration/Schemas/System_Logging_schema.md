---
uid: system_Logging_schema
---

# System logging configuration schema

The System logging configuration schema specifies how to formally describe the logging parameters for the System.

| Abstract            | Extensible | Status       | Identifiable | Custom properties | Additional properties | Defined in                                               |
| ------------------- | ---------- | ------------ | ------------ | ----------------- | --------------------- | -------------------------------------------------------- |
| Can be instantiated | Yes        | Experimental | No           | Forbidden         | Forbidden             | [System_Logging_schema.json](System_Logging_schema.json) |

# EdgeLoggerConfiguration properties

| Property                                        | Type      | Required | Nullable | Defined by                            |
| ----------------------------------------------- | --------- | -------- | -------- | ------------------------------------- |
| [LogFileCountLimit](#logfilecountlimit)         | `integer` | Optional | Yes      | EdgeLoggerConfiguration (this schema) |
| [LogFileSizeLimitBytes](#logfilesizelimitbytes) | `integer` | Optional | Yes      | EdgeLoggerConfiguration (this schema) |
| [LogLevel](#loglevel)                           | reference | Optional | No       | EdgeLoggerConfiguration (this schema) |

## LogFileCountLimit

`LogFileCountLimit`

- is optional
- type: `integer`
- defined in this schema

### LogFileCountLimit type

`integer`, nullable

## LogFileSizeLimitBytes

`LogFileSizeLimitBytes`

- is optional
- type: `integer`
- defined in this schema

### LogFileSizeLimitBytes type

`integer`, nullable

## LogLevel

`LogLevel`

- is optional
- type: reference
- defined in this schema

### LogLevel type

- []() – `#/definitions/EdgeLogLevel`

**All** of the following _requirements_ need to be fulfilled.

#### Requirement 1

- []() – `#/definitions/EdgeConfigurationBase`

#### Requirement 2

`object` with following properties:

| Property                | Type    | Required |
| ----------------------- | ------- | -------- |
| `LogFileCountLimit`     | integer | Optional |
| `LogFileSizeLimitBytes` | integer | Optional |
| `LogLevel`              |         | Optional |

#### LogFileCountLimit

`LogFileCountLimit`

- is optional
- type: `integer`

##### LogFileCountLimit type

`integer`, nullable

#### LogFileSizeLimitBytes

`LogFileSizeLimitBytes`

- is optional
- type: `integer`

##### LogFileSizeLimitBytes type

`integer`, nullable

#### LogLevel

`LogLevel`

- is optional
- type: reference

##### LogLevel type

- []() – `#/definitions/EdgeLogLevel`
