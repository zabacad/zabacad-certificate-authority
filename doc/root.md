# Root certificate

These steps generate a self-signed root certificate.

Ideally, perform these steps on an air-gapped machine.

## Set up configuration

Create a directory for the root certificate and set up these files.

  - `req.config` and `ca.config` -- Start with the example files in
    `config/root`. Read through, understand, and customize them. The names of
    the files below are set in these configurations.

    Note: It's possible to combine these configurations, but it's easier to
    understand what's what if they are separate.

  - `key` -- Generate a passphrase-protected private key. See
    [private keys](keys.md).

  - `serial` -- A serial number file. Create a file containing just the serial
    number for the root certificate in hexadecimal. Example:

    ```bash
    echo '0F00' > serial
    ```

  - `issued` -- A directory for issued certificates.

  - `issued/issued` -- An empty file that OpenSSL will populate.

## Generate root certificate

 1. Generate a certificate signing request (CSR), `req`, from the private key.
    This will prompt for the key passphrase.

    ```bash
    openssl req -new -config req.config -key key -out req
    ```

 2. Self-sign the CSR to generate the root certificate, `cert`. This will
    also prompt for the key passphrase.

    ```bash
    openssl ca -config ca.config -selfsign -keyfile key -in req -out cert
    ```

## Results

In addition to the root certificate, `cert`, the following files are updated:

  - `issued/${SERIAL}.pem` -- Another copy of `cert`.
  - `issued/issued` -- A list of all issued certificates.
  - `serial` -- The serial number has been incremented.

## Next

[Generating an intermediate certificate](intermediate.md)
