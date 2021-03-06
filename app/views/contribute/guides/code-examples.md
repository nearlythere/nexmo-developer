---
title: Code Examples
---

# Contributing Code Examples

Nexmo Developer hosts many code examples, we endeavour to make the as consistent as possible. You should follow this guide when contributing code examples to the building blocks repositories or directly to Nexmo Developer.

## Use the library

If an existing Nexmo-supported API library supports the functionality, you should use that library for code samples.

### Principle of Least Astonishment

Code samples should match the expectations and experience of a median-level competent developer in a language and try hard to not surprise or confuse them. Code samples for APIs are not a place to use flashy, experimental or cutting-edge techniques, but to try to maximise compatibility, and reduce ambiguity.

Code samples **MUST NOT** use any technique widely considered to be insecure, badly designed or likely to cause harm or confusion to the user.

## Placeholders

The following values should be used as placeholders in code examples. They can be specified assigned as constants out of the range of view of the rendered code to allow the code to be executed whist providing an obvious placeholders for the reader.

Key | Description | User customisation (future)
-- | -- | --
`NEXMO_API_KEY` | The users Nexmo API Key | ✅
`NEXMO_API_SECRET` | The users Nexmo API Key | ✅
`NEXMO_NUMBER` | The virtual number that the user holds with Nexmo | ❓
`TO_NUMBER` for outbound §§ `YOUR_NUMBER` for inbound | The number that the user owns or wants to communicate with | ❓
`NEXMO_APPLICATION_PRIVATE_KEY` | Represents a string of the actual private key | ❎
`NEXMO_APPLICATION_PRIVATE_KEY_PATH` | Represents a string that relates to the private key directory | ❎

### Future auto-magical user customisation

In the future we will customise code examples to the logged in user for example by adding API key and secret to the examples. To do this we need to be careful about how we use placeholders.

#### ✅ Good

{column:1/2}
This input:

```javascript
const nexmo = new Nexmo({
  apiKey: NEXMO_API_KEY,
  apiSecret: NEXMO_API_SECRET
})
```
{end}
{column:2/2}
Or this input:

```javascript
const nexmo = new Nexmo({
  apiKey: 'NEXMO_API_KEY',
  apiSecret: 'NEXMO_API_SECRET'
})
```
{end}


Would be converted to this into something like:

```javascript
const nexmo = new Nexmo({
  apiKey: 'abc123',
  apiSecret: 'abcdef123456789'
})
```

#### ❎ Bad

This input:

```javascript
NEXMO_API_KEY = process.env.NEXMO_API_KEY
NEXMO_API_SECRET = process.env.NEXMO_API_SECRET

// Something else
```

Would be converted to this invalid example:

```javascript
'abc123' =  process.env.'abc123'
'abcdef123456789' = process.env.'abcdef123456789'

// Something else
```

### SMS Specific

#### Message Body

```
A test SMS sent [demonstrating <feature>] using  the Nexmo SMS API
```

#### SenderID

```
Acme Inc
```

### Webhooks

The following URL paths should be used in examples that use Webhooks.

Path | Description
-- | --
`/webhook/answer` | The application `answer` event URL
`/webhook/event` | The application `event` event URL

Example code should always accept query string parameters for `GET` and `POST` requests.

Example code should always accept JSON for `POST` requests.

### NCCO examples

Below you can find static NCCO's that can be used in code examples. The source of these can be found in the `/public/ncco` directory of Nexmo Developer.

Example | URL
-- | --
Basic text-to-speech | <https://developer.nexmo.com/ncco/tts.json>

## Code

### Length

Where possible code should be kept to a maximum of 80 characters per-line.

The capacity before scrolling occurs is 101 characters however not all code examples are as wide as this.

```
----------------------- I am a line with 80 characters ------------------------
--------------------------------- I am a line with 101 characters ----------------------------------
```

### Linters, Formatters & Code Style Guides

Code throughout Nexmo Developer should be consistent. To help achieve this code examples should be tested with the following tools and against guides on their default configuration:

Language | Resource | Configuration
-- | -- | --
Node | [Standard JS](https://standardjs.com/) | Non configurable
Java | - | -
.NET | - | -
PHP | [PHPCS](https://github.com/squizlabs/PHP_CodeSniffer#installation) | [PSR-2](https://github.com/Nexmo/nexmo-php/blob/develop/phpcs.xml)
Python | [YAPF](https://github.com/google/yapf) | Default
Ruby| [Rubocop](https://github.com/bbatsov/rubocop) | Default

### Languages

#### JavaScript

Documentation should be clear whether JavaScript code is intended to run on the server (using, say, node.js), the client, or both.

#### Python

Avoid code that is significantly different in Python 2 and 3. When this is unavoidable, abstract away the incompatible code to the smallest area possible and use [`__future__`](https://docs.python.org/2/library/__future__.html) to ensure backwards compatibility with Python 2.

Inbound HTTP calls should use a WSGI-compatible web framework, preferably the [Flask](http://flask.pocoo.org/) micro-framework. Explanations of how to integrate Nexmo APIs with [Django](https://www.djangoproject.com/) are sensible too.
