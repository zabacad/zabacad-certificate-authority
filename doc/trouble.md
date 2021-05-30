# Troubleshooting

To open a TLS connection with the OpenSSL command line tools:

```bash
openssl s_client -connect ${HOST}:${PORT} </dev/null
```

Where:

  - `${HOST}` is the hostname or IP to connect to.
  - `${PORT}` is the TCP port. (Use 443 for HTTPS.)

This will show the certificate chain served and other TLS information.

Piping in `/dev/null` sends an end-of-file to close the connection. Other data
could be piped in or typed in until the connection times out.

Unless OpenSSL has had a trust store configured, it is normal to see:

```
verify error:num=19:self signed certificate in certificate chain
```

## Server name indication

Since multiple services might be hosted from the same IP address, TLS allows
clients to specify a desired hostname when opening the connection. This is
called _server name indication_ (SNI).

Since OpenSSL version 1.0.0, `openssl s_client` has a `-servername` option to
specify the desired hostname and test SNI.

Since OpenSSL version 1.1.0i and 1.1.1, SNI is set based on the hostname given
to `-connect`. `-servername` is still useful for connecting by IP address.
