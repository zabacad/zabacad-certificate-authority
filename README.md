# Zabacad's certificate authority

This is a set of OpenSSL commands and configurations for creating a private
[certificate authority (CA)][wiki-ca] and issuing certificates.

## Why operate a CA?

Obtaining publicly-signed certificates is now free though [Let's Encrypt][le]
or included with cloud services such as [AWS's Certificate Manager (ACM)][acm].

There are still reasons to run a private CA:

  - [Client certificates](doc/client.md)
  - Certificates for private DNS
  - Bogus certificates for testing
  - MITM proxies

## Requirements

This guide is for OpenSSL 1.1.1. Check the version with `openssl version`.

Some commands assume Bash/Linux.

## The CA

 1. [Generating the root certificate](doc/root.md)
 2. [Generating an intermediate certificate](doc/intermediate.md)
 3. [Trusting the CA](doc/trust.md)

## Certificates

 1. [Generating certificate signing requests](doc/req.md)
 2. [Issuing certificates](doc/issue.md)
 3. [Installing certificates](doc/install.md)

## More

  - [Private keys](doc/keys.md)
  - [Troubleshooting](doc/trouble.md)
  - [Client TLS](doc/client.md) -- For authentication both ways.

## Future work

**Warning**: CAs cannot be modified. Any future changes require a rebuild.

  - Revoking certificates: CRLs, OCSP, and OCSP stapling.


[acm]: https://aws.amazon.com/certificate-manager/
[le]: https://letsencrypt.org/
[wiki-ca]: https://en.wikipedia.org/wiki/Certificate_authority
