# lookatme

Single file `curl` based shell script reporting external IPv6 and IPv4 address
in parallel to be as fast as possible.

## Usage

```text
$ lookatme --help
Look at me and tell me my IPv6 and IPv4 address.

lookatme [OPTION]
  ... via IPv6 and IPv4 in parallel while printing IPv6 before IPv4. Parallized
  only if /dev/shm and mktemp are available. Errors are silently ignored.
  Scripts may cover all four possible cases with:

  ipvx=$(lookatme) # Either IPv6\nIPv4\n, IPv6\n, IPv4\n, or empty.
  ipv6=$(echo "$ipvx" | grep -F :) # IPv6 or empty.
  ipv4=$(echo "$ipvx" | grep -F .) # IPv4 or empty.

  Security? ... make sure that:

  LOOKATME_OVER=https
  LOOKATME_FROM=<trustful-host>
  LOOKATME_DUDE=<trustful-ca-cert>

OPTIONs:
  -6, --ipv6     ... via IPv6 only.
  -4, --ipv4     ... via IPv4 only.

  -h, --help     Print help.
  -v, --version  Print version.

Environment variables:
  LOOKATME_OVER  http
  LOOKATME_FROM  ipvx.qu1x.org
  LOOKATME_DUDE  [CA_CERT]
  LOOKATME_HERE  [INTERFACE]
  LOOKATME_FAST  2
```

## Server

An `nginx` server block may be:

```nginx
server {
	listen 80;
	listen [::]:80;
	server_name ipvx.qu1x.org ipv6.qu1x.org ipv4.qu1x.org;
	default_type text/plain;
	return 200 "$remote_addr\n";
}
```

With following DNS records:

  * [ipvx.qu1x.org](https://ipvx.qu1x.org): A and AAAA for `lookatme`.
  * [ipv6.qu1x.org](https://ipv6.qu1x.org): AAAA only for IPv6 with web browser.
  * [ipv4.qu1x.org](https://ipv4.qu1x.org): A only for IPv4 with web browser.

## License

Copyright (c) 2017, 2019 Rouven Spreckels <n3vu0r@qu1x.org>

Usage of the works is permitted provided that
this instrument is retained with the works, so that
any entity that uses the works is notified of this instrument.

DISCLAIMER: THE WORKS ARE WITHOUT WARRANTY.

## Contribution

Unless you explicitly state otherwise, any contribution intentionally submitted
for inclusion in the works by you shall be licensed as above, without any
additional terms or conditions.
