# Perl oneliners

Curl (not support tls)

```bash
perl -MHTTP::Tiny -E 'my $r=HTTP::Tiny->new->get("http://gitlab.com/"); say "$r->{status} $r->{reason}"; while(my($k,$v)=each %{$r->{headers}}){for(ref $v eq "ARRAY"?@$v:$v){say "$k: $_"}} print $r->{content}'
```

Port avaibility check

```bash
perl -E 'use IO::Socket::INET; IO::Socket::INET->new(PeerAddr => "some.smb.host", PeerPort => 445, Timeout => 2) ? print "Open\n" : print "Closed\n";'
```

Domain resolver

```bash
perl -MSocket=:addrinfo -E '($e, @r) = getaddrinfo("domain.com", ""); $e ? warn "Lookup failed: $e" : say for map { (getnameinfo($_->{addr}, NI_NUMERICHOST))[1] } @r'
```

