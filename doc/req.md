# Certificate signing requests

These steps generate a certificate signing request (CSR).

Where a certificate is desired, a private key and CSR are generated, and the
CSR is sent off to a certificate authority (CA) to be signed.

The CSR informs the CA of the the *public* key and information about the
desired certificate. (Though they may ignore this information.) The private key
never has to move.

## Set up configuration

Create a directory for the CSR (and future certificate) and set up these files.

  - `key` -- Generate a private key. See [private keys](keys.md).

  - `req.config` -- Start with the example `config/req-example.config`.
    Read through, understand, and customize it.

## Generate CSR

```bash
openssl req -new -config req.config -key key -out req
```

## Next

[Issuing certificates](issue.md)
