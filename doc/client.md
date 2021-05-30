# Client TLS

In a TLS session, the _server_ presents its certificate to the _client_ for the
client to [validate](trust.md). Optionally, the server may request that the
client present a certificate to the server. This is called _client TLS_ or
_mutual TLS_, and is a very smooth way of performing authentication.

Typically, a dedicated certificate authority (CA) is set up to issue client
certificates and the server will only trust certificates from that CA.

There are some key differences with a client certificate:

  - In the subject: Where the common name for a server certificate is the
    domain name of the server, the common name for a client certificate is
    (typically) a user's name.

  - In the extensions: The _extended key usage_ is appropriately set to either
    _server_ or _client_. This is performed by selecting a different extension
    section from the the configuration file with the `-extensions` option of
    `openssl ca`.
