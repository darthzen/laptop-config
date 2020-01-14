Scripts and files I use to customize my laptop (currently a Dell Precision 5530)

## Layout
On the host laptop I keep my data isolated on a single block device mounted at `/data` and the SUSE-related RPM media under the following structure:

```
/data/suse/iso            # Downloaded ISO images (unextracted)
           install        # Extracted ISO contents for installation - available via http using name-based vhost
           smt            # Contents of my SMT/RMT server - updated by NFS mounting it to an SMT/RMT VM
```

## Services

#### NFS
`/data/suse/smt` mounted up to SMT VM at `/srv/www/htdocs/repo` or RMT at `/var/lib/rmt/public/repo`

#### HTTP
Served via Nginx (though Apache works just as well).
I have name-based vhosts defined for:
- install.ash4d.com (served from `/data/suse/install` and consists of extracted ISO contents)
- repos.ash4d.com (served from `/data/suse/smt` and contains my patch content - could be setup using rmt package on openSUSE)

#### Libvirt dnsmasq
Use the libvirt network definition to enable PXE booting, create static DHCP assignments and localized DNS

#### TFTP
Served via TFTP server in the libvirt dnsmasq instances.  Uses the standard location, `/srv/tftpboot`

