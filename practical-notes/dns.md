# DNS

{% tabs %}
{% tab title="DNS Records" %}
| Record                       | Description                                                                                                                                                                                                                                                            |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Resource Record`            | A domain name, usually a fully qualified domain name, is the first part of a Resource Record. If you don't use a fully qualified domain name, the zone's name where the record is located will be appended to the end of the name.                                     |
| `TTL`                        | In seconds, the Time-To-Live (`TTL`) defaults to the minimum value specified in the SOA record.                                                                                                                                                                        |
| `Record Class`               | Internet, Hesiod, or Chaos                                                                                                                                                                                                                                             |
| `Start Of Authority` (`SOA`) | It should be first in a zone file because it indicates the start of a zone. Each zone can only have one `SOA` record, and additionally, it contains the zone's values, such as a serial number and multiple expiration timeouts.                                       |
| `Name Servers` (`NS`)        | The distributed database is bound together by `NS` Records. They are in charge of a zone's authoritative name server and the authority for a child zone to a name server.                                                                                              |
| `IPv4 Addresses` (`A`)       | The A record is only a mapping between a hostname and an IP address. 'Forward' zones are those with `A` records.                                                                                                                                                       |
| `Pointer` (`PTR`)            | The PTR record is a mapping between an IP address and a hostname. 'Reverse' zones are those that have `PTR` records.                                                                                                                                                   |
| `Canonical Name` (`CNAME`)   | An alias hostname is mapped to an `A` record hostname using the `CNAME` record.                                                                                                                                                                                        |
| `Mail Exchange` (`MX`)       | The `MX` record identifies a host that will accept emails for a specific host. A priority value has been assigned to the specified host. Multiple MX records can exist on the same host, and a prioritized list is made consisting of the records for a specific host. |


{% endtab %}

{% tab title="nslookup/dig" %}
| Command                            | Description                                          |
| ---------------------------------- | ---------------------------------------------------- |
| `nslookup $TARGET`                 | Identify the `A` record for the target domain.       |
| `nslookup -query=A $TARGET`        | Identify the `A` record for the target domain.       |
| `dig $TARGET @<nameserver/IP>`     | Identify the `A` record for the target domain.       |
| `dig a $TARGET @<nameserver/IP>`   | Identify the `A` record for the target domain.       |
| `nslookup -query=PTR <IP>`         | Identify the `PTR` record for the target IP address. |
| `dig -x <IP> @<nameserver/IP>`     | Identify the `PTR` record for the target IP address. |
| `nslookup -query=ANY $TARGET`      | Identify `ANY` records for the target domain.        |
| `dig any $TARGET @<nameserver/IP>` | Identify `ANY` records for the target domain.        |
| `nslookup -query=TXT $TARGET`      | Identify the `TXT` records for the target domain.    |
| `dig txt $TARGET @<nameserver/IP>` | Identify the `TXT` records for the target domain.    |
| `nslookup -query=MX $TARGET`       | Identify the `MX` records for the target domain.     |
| `dig mx $TARGET @<nameserver/IP>`  | Identify the `MX` records for the target domain.     |


{% endtab %}
{% endtabs %}
