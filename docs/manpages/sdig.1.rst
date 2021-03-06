sdig
====

Synopsis
--------

:program:`sdig` *IP-ADDRESS-OR-DOH-URL* *PORT* *QNAME* *QTYPE* [*OPTION*]

Description
-----------

:program:`sdig` sends a DNS query to *IP-ADDRESS-OR-DOH-URL* on port *PORT* and displays the answer in a formatted way.
If the address starts with an ``h``, it is assumed to be a DoH endpoint, and *PORT* is ignored.
If qname and qtype are both `-` and tcp is used, multiple lines are read from stdin, where each line contains a qname and a type.
If the address is ``stdin``, a DNS packet is read from stdin instead of from the network, and *PORT* is ignored.
All input is literal and case sensitive.
Queries need option `recurse` to expect a resource record reply if the query target is not known to be the authoritative server for that record.

Options
-------

These options can be added to the commandline in any order.

class *CLASSNUM*
    Send the query in the numbered class (like 3 for CHAOS) instead of the default 1 (for IN).
dnssec
    Set the DO bit to request DNSSEC information.
ednssubnet *SUBNET*
    Send *SUBNET* in the edns-client-subnet option. If this option is not set, no edns-client-subnet option is set in the query.
hidesoadetails
    Don't show the SOA serial in the response.
hidettl
    Replace TTLs with `[ttl]` in the response.
proxy *TCP?* *SRC* *DST*
    Wrap query in PROXYv2 protocol with these parameters. The first parameter accepts 0 for UDP and 1 for TCP. The second and third take IP addresses and port.
recurse
    Set the RD bit in the question.
showflags
    Show the NSEC3 flags in the response (they are hidden by default).
tcp
    Use TCP instead of UDP to send the query.
xpf *XPFCODE* *XPFVERSION* *XPFPROTO* *XPFSRC* *XPFDST*
	Send an *XPF* additional with these parameters.

Examples
--------

Simple queries to local resolvers 
    sdig 127.0.0.1 53 example.com AAAA recurse
    sdig ::1 53 example.com A recurse

Query to a DNS-over-HTTPS server requesting dnssec and recursion
    sdig https://dns.example.net/dns-query 443 example.com A dnssec recurse

