# lookatme

Single file shell script reporting external IPv4 and IPv6 address in parallel to
be as fast as possible. Requires `curl`.

## Usage

```text
$ lookatme --help
Look at me and tell me my IPv4 and IPv6 address

lookatme [OPTION]
  ...via IPv4 and IPv6 in parallel (output unordered)

OPTIONs:
  -4             Via IPv4 only
  -6             Via IPv6 only
  -h, --help     Print help
  -v, --version  Print version

Environment variables:
  LOOKATME_OVER  http
  LOOKATME_FROM  ipvx.qu1x.net
```

## Server

An `nginx` server block could be:

```nginx
server {
        listen 80;
        listen [::]:80;

        server_name ipvx.qu1x.net ipv4.qu1x.net ipv6.qu1x.net;

        default_type text/plain;
        return 200 "$remote_addr\n";
}
```

With following DNS records:

  * <ipvx.qu1x.net>: A and AAAA
  * <ipv4.qu1x.net>: A only
  * <ipv6.qu1x.net>: AAAA only

Last two are supposed to be entered in a web browser.

## License

Copyright (c) 2017 Rouven Spreckels <n3vu0r@qu1x.org>

Usage of the works is permitted provided that
this instrument is retained with the works, so that
any entity that uses the works is notified of this instrument.

DISCLAIMER: THE WORKS ARE WITHOUT WARRANTY.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the works by you shall be licensed as above, without any
additional terms or conditions.
