# Intermediate certificate

These steps generate an _intermediate_ certificate. This intermediate
certificate is signed by the root certificate and used to sign the final,
desired certificates. (Sometimes called leaf, server, or user certificates.)

These steps require the [root certificate](root.md), but may be performed
elsewhere. This allows the root certificate to remain air-gapped, but the
intermediate to be on-line.

## Set up configuration

Create a directory for the intermediate certificate and set up these files.

  - `req.config` and `ca.config` -- Start with the example files in
    `config/intermediate`. Read through, understand, and customize them.

    These configurations are distinct from the ones for the root certificate.

The remainging files are set up just like for the root certificate.

  - `key`
  - `serial`
  - `issued`
  - `issued/issued`

## Generate intermediate certificate

 1. Generate a certificate signing request (CSR), `req`, from the private key.
    This will prompt for the key passphrase.

    ```bash
    openssl req -new -config req.config -key key -out req
    ```

 2. Copy the CSR to the root certificate's directory.

 3. In the root certificate's directory, sign the CSR for the intermediate
    certificate. This will prompt for the root certificate's key passphrase.

      - `intermediate.req` -- The CSR copied over.

      - `intermediate.cert` -- The resulting intermediate certificate.

    ```bash
    openssl ca -config ca.config -extensions ext_intermediate -policy policy_intermediate -in intermediate.req -out intermediate.cert
    ```

 4. Copy the intermediate certificate back to its directory.

## Next

  - [Trusting the CA](trust.md)
  - [Generating CSRs](req.md)
