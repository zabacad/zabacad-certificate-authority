# Installing certificates

Certificate installation varies by software, but always requires:

  - The certificate itself.
  - The **private** key.
  - The passphrase for the private key, if any. Generally not used, since:
      - Saving the passphrase along side what it protects defeats the security.
      - Many pieces of software do not support passphrases.
  - The [chain of additional certificates](trust.md) to serve. It is best
    practice to serve the whole chain to help "dumber" clients. This is
    typically formated as a series of PEM-formatted certificates concatenated
    together in the same file.
  - The correct format for everything.

## Formats

The most common formats for certificates and keys are:

  - _PEM_ ("privacy enhanced mail"):
    - Most common format. Often assumed when no format is specified.
    - Usually understood by the `file` utility.
    - Contains only ASCII characters.
    - Starts with `-----BEGIN ...`
    - Ends with `-----END ...`

  - _DER_ ("distinguished encoding rules"):
    - Binary format.

Other formats include _PKCS12_ (p12), which can contain multiple certificates
and keys and JKS (Java Keystore) used by (older) versions of Java.

## Converting formats

```bash
openssl ${CMD} -in ${IN} -inform ${INFORM} -out ${OUT} -outform ${OUTFORM}
```

Where:

  - `${CMD}` is `x509` for certificates or `pkey` for keys.
  - `${IN}` is the input file.
  - `${INFORM}` is the format (`pem` or `der`) of the input file.
  - `${OUT}` is the output file.
  - `${OUTFORM}` is the format (`pem` or `der`) of the output file.

## PEM RSA key trouble

PEM-formatted RSA keys may begin/end with either:

  - `-----BEGIN`/`END PRIVATE KEY-----`
  - `-----BEGIN`/`END RSA PRIVATE KEY-----`

Some software only expects one or the other. It is safe to add or remove `RSA`
with a text editor.

## Specific software

It should be possible to install a certificate given a piece of software's
documentation. The information here is only for filling in gaps.

### Asustor NAS software

(The "documentation" for this is useless.) Replacing an existing certificate
does not work. Instead, add a new one. Set it as "default" to use it for the
web UI. All PEM format. The three files in the wizard are:

  - Key: Concatenate key and server certificate.
  - Certificate: Server certificate only.
  - Chain: Entire certificate chain, including server and root certificates.

### Ubiquiti EdgeMAX switch firmware

Requires the "legacy" UI and **disabling** HTTPS.

### pfSense

Under certificate manager, entire PEM-formatted chain goes in certificate box.

Pick certificate for web UI under _system_ -> _advanced_.
