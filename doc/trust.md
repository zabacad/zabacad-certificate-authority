# Trust

When a TLS server presents a certificate, clients need a way to know if the
certificate should be trusted. This is performed by building a _chain of trust_
and matching it to a local _trust store_.

First, the client verifies the domain name (or IP address) appears on the
certificate. Newer client libraries only check the _subject alternate names_
(SANs). These include NSS (CURL, Firefox) and Go (etcd). Historically, the
`commonName` of the subject was used instead.

Domain names can contain a `*` as a wildcard, under certain conditions. In
practice, it is only ever the leftmost component, for example `*.example.com`.
A wildcard only matches a single domain component, for example
`foo.example.com`, but not `bar.foo.example.com`.

## Chain of trust

The _chain of trust_ is simply a certificate, the certificate that issued it,
the certificate that issued that one, and so on. The final certificate in the
chain is always self-signed. If the first certificate is self-signed, the chain
is only one certificate long.

This chain is formed by matching the _issuer_ field of a certificate to the
_subject_ field of its issuer. For additional security, the _authority key
identifier_ is also matched to the _subject key identifier_ of the issuer, if
present.

The TLS server may send some or part of the chain to aid the client in building
the chain. Some clients rely on this and cannot build the chain themselves.

## Trust store

TLS clients rely on a list of trusted certificates, called a _trust store_. A
certificate is trusted if one of the certificates in its chain of trust is in
the trust store.

There are several public trust stores, each manually curated by software
vendors or organizations such as the CA/Browser Forum. Operating systems
contain a trust store which TLS software may use, or software may contain its
own trust store.

Users and administrators may also add certificates (such as the CA generated
here) to their local copies of trust stores.

Note: Most trust stores require all certificates to have unique subjects. This
is why most CAs include a year or other number in the subject.

## Specific software

Here are instructions for managing the trust store for various pieces of
software.

### Firefox

Firefox contains its own trust store, located under:

 1. _preferences_
 2. _privacy and security_
 3. heading _certificates_
 4. button _view certificates_
 5. tab _authorities_

  - Add certificates with the _import_ button.
  - Remove certificates with the _delete or distrust_ button.

Additionally, Firefox will also use the operating system's trust store if
`security.enterprise_roots.enabled` is `true`. This setting will be changed to
`true` when Firefox encounters an unknown issuer and 
`security.certerrors.mitm.auto_enable_enterprise_roots` is set to `true`.
