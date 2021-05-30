# Issuing certificates

These steps sign/issue a certificate based on a certificate signing request
(CSR).

 1. Copy the CSR to the intermediate certificate's directory.

 2. Generate the new certificate. This will prompt for the intermediate
    certificate's key passphase.

      - `example.req` -- The CSR.

      - `example.cert` -- The resulting certificate.

    ```bash
    openssl ca -config ca.config -in example.req -out example.cert
    ```

 3. Copy the new certificate next to its private key.

## Next

[Installing certificates](install.md)
