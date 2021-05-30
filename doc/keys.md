# Private keys

Every certificate requires a private key.

Many OpenSSL commands allow generating a new key when needed, but generating
the key separately allows more control.

`openssl rsa` exists to manage RSA keys, but is deprecated in favor of
`openssl genpkey`, which can also generate other kinds of keys.

## Key types

Widely supported key types are:

  - RSA -- Supported virtually everywhere. Varies in size. 4096 bits is good.
    2048 bits is the minimum recommended.

  - Elliptic-curve -- More modern. Comes in P-256 and P-384 flavors.

A certificate using one key type can issue/sign a certificate using another.

## Passphrases

A passphrase can be using to prevent use of the private key unless the
passphrase is given.

First choose or generate a passphrase, for example:

```bash
pwgen -s 32 1
```

To encrypt the private key when generating it, provide an OpenSSL-supported
encryption algorithm as a flag to the `genpkey` command. For example,
`-aes-256-cbs`. See the full list of algorithms with `openssl enc -list`.

## Generate private key

Generate a private key using **one** of the following commands.

  - To generate an elliptic-curve P-384 key:

    ```bash
    openssl genpkey -algorithm ec -pkeyopt ec_paramgen_curve:P-384 -out key
    ```

  - To generate a 4096-bit RSA key:

    ```bash
    openssl genpkey -algorithm rsa -pkeyopt rsa_keygen_bits:4096 -out key
    ```
