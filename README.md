# go-credential

[![Build Status](https://github.com/beyondstorage/go-credential/workflows/Unit%20Test/badge.svg?branch=master)](https://github.com/beyondstorage/go-credential/actions?query=workflow%3A%22Unit+Test%22)
[![Go dev](https://pkg.go.dev/badge/github.com/beyondstorage/go-credential)](https://pkg.go.dev/github.com/beyondstorage/go-credential)
[![License](https://img.shields.io/badge/license-apache%20v2-blue.svg)](https://github.com/beyondstorage/go-credential/blob/master/LICENSE)

Both human and machine-readable credential format.

## Format

```
<protocol>:<value>+
```

For example:

- hmac: `hmac:access_key:secret_key`
- apikey: `apikey:apikey`
- file: `file:/path/to/config/file`

## Quick Start

```go
cred, err := credential.Parse("hmac:access_key:secret_key)
if err != nil {
	log.Fatal("parse: ", err)
}

switch cred.Protocol() {
case ProtocolHmac:
    ak, sk := cred.Hmac()
    log.Println("access_key: ", ak)
    log.Println("secret_key: ", sk)
case ProtocolAPIKey:
    apikey := cred.APIKey()
    log.Println("apikey: ", apikey)
case ProtocolFile:
    path := cred.File()
    log.Println("path: ", path)
case ProtocolEnv:
    log.Println("use env value")
case ProtocolBase64:
    content := cred.Base64()
    log.Println("base64: ", content)
default:
    panic("unsupported protocol")
}
```
