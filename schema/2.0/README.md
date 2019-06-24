# Colophon Spec

## Data Structure & File Format

Colophon files are required to be [`YAML`][yaml] files saved in `UTF-8` encoding, other encodings are forbidden.

### File Naming

Acceptable file name must match the following pattern:

```regex
^\.colophon\.yml$
```

###### Example

- [`.colophon.yml`](#full-example)

---

### `.colophon.yml`

```yml
version: 2.0
id: my-awesome-app
about: {}
contacts: []
schedule: {}
environments: []
references: []
```

| name             | type     | required | default | description                                             |
| ---------------- | -------- | -------- | ------- | ------------------------------------------------------- |
| **version**      | `String` | ✓        | `-`     | Spec version. Format must follow [semver][]             |
| **id**           | `String` | ✗        | `-`     | A unique, deterministic identifier for your application |
| **about**        | `Object` | ✓        | `-`     | [About Object](#about)                                  |
| **contacts**     | `Array`  | ✓        | `-`     | [Contacts Array](#contacts)                             |
| **schedule**     | `Object` | ✗        | `-`     | [Schedule Object](#schedule)                            |
| **environments** | `Array`  | ✓        | `-`     | [Environments Array](#environments)                     |
| **references**   | `Array`  | ✗        | `-`     | [References Object](#references)                        |

### `about`

> defines the context of "What" this application is

```yml
about:
  title: my-awesome-app
  description: an awesome app we built
```

| name            | type     | required | default | description                                  |
| --------------- | -------- | -------- | ------- | -------------------------------------------- |
| **title**       | `String` | ✓        | `-`     | Unique title representing the application    |
| **description** | `String` | ✗        | `-`     | Snippet describing the application in detail |

### `contacts`

> defines the context of "Who" is responsible for this application

```yml
contacts:
  - type: Lead Developer
    name: Ahmad Nassri 
    email: ahmad@acme.com

  - type: Lead Designer
    name: Alex
    email: alex@acme.com

  - type: Development Team
    name: dope jackalope
    email: dope@acme.com
```

Each item under `contacts` represents a "Contact Object", you can have as many as you want to describe your application contacts:

| name      | type     | required | default | description                  |
| --------- | -------- | -------- | ------- | ---------------------------- |
| **type**  | `String` | ✗        | `-`     | type of contact              |
| **name**  | `String` | ✓        | `-`     | name of contact              |
| **email** | `String` | ✓        | `-`     | email identifier for contact |

**Note**: at least one property is required to be present.

### `schedule`

> defines the context of "When" activities around this application are planned

```yml
schedule:
  launch: 2018-05-24T03:35:40.968Z
  sunset: 2020-01-31T03:35:40.968Z
```

| name         | type        | required | default | description                                                                   |
| ------------ | ----------- | -------- | ------- | ----------------------------------------------------------------------------- |
| **launch**   | `date-time` | ✗        | `-`     | Launch Date, with values defined in [`date-time`][rfc3339] format             |
| **sunset**   | `date-time` | ✗        | `-`     | Sunset Date, with values defined in [`date-time`][rfc3339] format             |
| **(custom)** | `date-time` | ✗        | `-`     | any date representation, with values defined in [`date-time`][rfc3339] format |

`date-time` format as defined in [RFC 3339, section 5.6][rfc3339]

### `environments`

> defines the context of "Where" this application is

```yml
environments:
  - type: production
    title: URL
    description: Web Application URL
    uri: https://www.acme.com

  - type: test
    title: URL
    description: Web Application URL
    uri: http://test.acme.com

  - type: production
    title: Database
    description: Application Database
    uri: mongodb://prod.db.acme.com:27017/acme
```

Each item under `environments` represents an "Environment Object", you can have as many as you want to describe your application environments:

| name            | type     | required | default | description                                                   |
| --------------- | -------- | -------- | ------- | ------------------------------------------------------------- |
| **type**        | `String` | ✗        | `-`     | Environment Type _(freeform identifier, useful for grouping)_ |
| **title**       | `String` | ✓        | `-`     | Environment Title                                             |
| **description** | `String` | ✗        | `-`     | Description of this Environment                               |
| **uri**         | `URI`    | ✓        | `-`     | Environment URI                                               |

### `references`

> defines additional context about application through external sources

```yml
references:
  - title: JIRA
    description: application backlog & issues
    uri: https://acme.atlassian.net/projects/APP/issues/

  - title: Wiki
    description: application technical wiki
    uri: https://github.com/acme/app/wiki
```

you add as many references as you want for your application:

| name            | type     | required | default | description                     |
| --------------- | -------- | -------- | ------- | ------------------------------- |
| **title**       | `String` | ✓        | `-`     | Reference Title                 |
| **description** | `String` | ✗        | `-`     | Description of this Reference   |
| **uri**         | `URI`    | ✓        | `-`     | Reference URI                   |

###### Full Example

> ```yaml
> version: 2.0
>
> id: my-awesome-app
>
> about:
>   title: My Awesome App
>   description: app that makes everything awesome!
>
> contacts:
>   - type: department
>     name: Awesome Department
>     email: awesome@acme.com
> 
>   - type: developers
>     name: app development
>     email: app-dev@acme.com
> 
>   - type: qa
>     name: app qa
>     email: app-qa@acme.com
> 
>   - type: Lead Developer
>     name: Alex Smith
>     email: ahmad@acme.com
> 
>   - type: Lead Designer
>     name: John Smith
>     email: alex@acme.com
>
> schedule:
>   launch: 2018-05-24T03:35:40.968Z
>   sunset: 2020-01-31T03:35:40.968Z
>
> environments:
>   - type: production
>     title: URL
>     description: Web Application URL
>     uri: https://www.acme.com
>
>   - type: test
>     title: URL
>     description: Web Application URL
>     uri: http://test.acme.com
>
>   - type: production
>     title: Database
>     description: Application Database
>     uri: mongodb://prod.db.acme.com:27017/acme
>
> references:
>   - title: JIRA
>     description: application backlog & issues
>     uri: https://acme.atlassian.net/projects/APP/issues/
>
>   - title: Wiki
>     description: application technical wiki
>     uri: https://github.com/acme/app/wiki
> ```

[semver]: https://semver.org

[yaml]: http://www.yaml.org/

[rfc3339]: https://tools.ietf.org/html/rfc3339#section-5.6

[rfc5322]: https://tools.ietf.org/html/rfc5322#section-3.4.1
