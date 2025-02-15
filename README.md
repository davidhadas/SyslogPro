SyslogPro
=========
[![Build Status](https://travis-ci.org/cyamato/SyslogPro.svg?branch=master)](https://travis-ci.org/cyamato/SyslogPro) 
[![Coverage Status](https://coveralls.io/repos/github/cyamato/SyslogPro/badge.svg?branch=master)](https://coveralls.io/github/cyamato/SyslogPro?branch=master)
![](https://img.shields.io/dub/l/vibe-d.svg?style=flat)

[Site](https://github.com/cyamato/SyslogPro) |
[Docs](https://cyamato.github.io/SyslogPro/) |
[Wiki](https://github.com/cyamato/SyslogPro/wiki "Changelog, Roadmap, etc.") |
[Code of Conduct](https://js.foundation/community/code-of-conduct)

A pure Javascript Syslog module with support for RFC3164, RFC5424, IBM LEEF 
(Log Event Extended Format), and HP CEF (Common Event Format) formatted 
messages. SyslogPro has transport options for UDP, TCP, and TLS. TLS includes 
support for Server and Client certificate authorization. For unformatted and 
RFC messages there is support for Basic and Extended ANSI coloring. RFC5424 
Structured Data is also included in the module. All 28 standard CEF Extensions 
are included in the default CEF class. All 45 standard LEEF Attributes are 
included in the default LEEF class. It is the goal of this project is for 
every release to offer full code coverage unit testing and documentation. 

[Please see the full JSDoc for usage and options: 
https://cyamato.github.io/SyslogPro/](https://cyamato.github.io/SyslogPro/).

### News
* ⚠ Please note that at present, the 0.1.x version of the SDK 
[requires Node 10.6 or later](https://github.com/nodejs/LTS). 
* This module makes use of [ECMA-262 Promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise)
and the [DNS Promises API](https://nodejs.org/api/dns.html#dns_dns_promises_api). 
* APIs do not support the callback model and only return promises.

### Installation
```shell
  npm install --save syslog-pro
```

## Usage
```js
  const SyslogPro = require('syslog-pro');
  let syslog = new SyslogPro.Syslog({
    target: 'localhost',
    protocol: 'udp',
    format: 'rfc5424'
  });
  syslog.rfc5424.info('My Message');
```
Optionally you can create each class or class options to pass to SyslogPro to 
create formatted messages or use directly
  
**RFC3164**
```js
  let rfc3164 = new SyslogPro.RFC3164({
    applacationName: 'MyApp',
    color: true,
    extendedColor: true,
    server: {
      target: 'myServer.fqdn'
    }
  });
  rfc3164.info('My Message');
```

**RFC5424**
```js
  let rfc5424 = new SyslogPro.RFC5424({
    applacationName: 'MyApp',
    timestamp: true,
    encludeStructuredData: true
    color: true,
    extendedColor: true,
    server: {
      target: 'myServer.fqdn'
    }
  });
  rfc5424.info('My Message');
```

**LEEF (Log Event Extended Format)**
```js
  let leef = new SyslogPro.LEEF({
    vendor: 'acme',
    product: 'doohickey1000',
    version: 'alpha',
    eventId: 'hack',
    attrabutes: {
      cat: 'CC Databreach'
    },
    server: {
      target: 'myServer.fqdn'
    }
  })
      .send()
          .then((result) => {})
          .catch((error) => {
            console.log(error);
          });
```

**CEF (Common Event Format)**
```js
  let cef = new SyslogPro.CEF({
    deviceVendor: 'acme',
    deviceProduct: 'doohickey1000',
    deviceVersion: 'alpha',
    deviceEventClassId: 'hack',
    name: 'My Reporting Service',
    severity: 'High',
    extensions: {
      rawEvent: 'CC Databreach'
    },
    server: {
      target: 'myServer.fqdn'
    }
  })
      .send()
          .then((result) => {})
          .catch((error) => {
            console.log(error);
          });
```

## API
For more details see:
* [JSDoc](https://cyamato.github.io/SyslogPro/) 
* [API.md](./docs/api.md)
* [Docco.html](./docs/docco/index.html)
* [Docco.md](./docs/docco/README.md)

## Test
```shell
  npm test
```

## Contributing

Please try to maintain the existing coding style. Add unit tests for any new or 
changed functionality. Lint and test your code.

* [Repository](https://github.com/cyamato/SyslogPro.git)
* [Bug Reporting](https://github.com/cyamato/SyslogPro/issues)
* [Wiki](https://github.com/cyamato/SyslogPro/wiki)