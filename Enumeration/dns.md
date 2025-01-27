Config
`~# cat ~/dns_tunneling
`~# resolvectl status


- Scan with Nmap

```nmap -T4 -p 53 --script broadcast-dns-service-discovery x.x.x.x```

```nmap -T4 -p 53 --script dns-brute x.x.x.x```

```nmap -Pn -sU -p 53 --script dns-recursion x.x.x.x```

```nmap -sU -p 53 --script dns-nsec-enum --script-args dns-nsec-enum.domains= domain.com x.x.x.x```
	



-  host:
	- `~# host -t ns domain.com    // Enumerates name servers.
	- `~# host -t mx domain.com    // Enumerates mail servers.
	- `~# host -t txt domain.com
	- bash script:
		`~# for ip in $(cat file.txt);do host $ip.domain.com;done
		`~# for ip in $(seq 10 100);do host 172.20.10.$ip;done | grep -v "not found" // reverse dns lookup == ptr


- nslookup:
	- nslookup -querytype=ns  domain.com   
	- nslookup -querytype=mx domain.com
	- nslookup -querytype=any domain.com    // Enumerates anything possible.
- dig
	`~# dig ANY sindadsec.ir
	`~# dig ns domain.com or dig +short NS zonetransfer.me
	`~# dig @a.ns.domain domain.com


- Zone Transfer ?        
	 `~# dig ns domain.com
	 `~# dig @NS domain.com A +recurse
	 `~# dig @NS domain.com A +norecurse
	 `~# dig axfr @NS domain.com
	 `~# nslookup> set querytype=soa
	 `~# nslookup> domain.com
	 `~# nslookup> ls -d ns1.sindadsec.ir //zone transfer on windows
   `~# dnsenum domain.com
	 `~# dnsrecon -d domain.com
	 `~# dnsrecon -d domain.com -t std
	 `~# dnsrecon -d domain.com -D file.txt -t brt // bruteforce
	 `~# dnsrecon -t axfr -d domain.com //zonetransfer
	 `~# fierce -dns domain.com
