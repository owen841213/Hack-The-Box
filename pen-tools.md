# Pentesting tools
## Recon & Enumeration

### port scanning
- nmap

    ```bash
    nmap -sC -sV -oA irked 10.10.10.117
    ```

    `-sC` enables the default script scanning.

    `-sV` detects the version of services running on the host.

    `-oA` specifies the output format.

    ```bash
    nmap -vvv -p- 10.10.10.117
    ```

    `-vvv` is the verbosity level of the output.

    `-p-` scans all 65535 ports.

### directory scanning
- gobuster

    ```bash
    gobuster -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt -u http://10.10.10.104 -t 30
    ```

    `-w` is the path of the wordlists.
    
    `-u` is the url.
     
    `-t` is the number of thread, default is 10

- dirb

### inspectation on a file
- exiftool: 

    ```bash
    exiftool giddy.jpg
    ```

- strings

    ```bash
    strings giddy.jpg
    ```

- xxd

    ```bash
    xxd giddy.jpg
    ```

- binwalk

    ```bash
    binwalk giddy.jpg
    ```

### SQL injection
- sqlmap

    ```bash
    sqlmap -r search.req --dbms=mssql --force-dbms mssql
    ```
    
    `-r` is the request file. You can use a custom injection marker ('*') to specify the position you want the injection to take place at.
    
    `--dbms` specifies the database management system in the back-end

    `--force` make the sqlmap more obedient

### network sniffing
- tcpdump

    ```bash
    tcpdump -i tun0 icmp -n
    ```

    `-i` is the interface; `icmp` is the protocol.
    
    `-n` disable displaying DNS information. Sometimes tcpdump will try to look up in DNS which may cause LAG, and this is why `-n` is used.

- netcat

    ```bash
    nc -l -v -n -p 445
    ```

    or

    ```bash
    nc -lvnp 445
    ```
    
    `-l` listens for an incoming connection.
    
    `-v` means verbose output.
    
    `-n` disable DNS lookups.
    
    `-p` uses specific source port

- responder

    ```bash
    responder -I tun0
    ```
    
    It will try to harvest some credentials through the interface specified.

## Exploiting Vulnerabilities
- Exploit DataBase

    ```base
    searchsploit unifi
    ```
    This will perform a search in Exploit-DB and return the results that contain the word "unifi"

    ```bash
    searchsploi -m exploits/windows/local/43390.txt
    ```

    `-m` will make a copy of the exploit's details to your machine.

    `exploits/windows/local/43390.txt` is the path of the exploit.
    
## Windows Post-Exploitation
- powershell

    ```bash
    echo "PleaseSubscribe" > TestWrite
    ```
    The command will write "PleaseSubscribe" into a file called TestWrite.

    ```bash
    type TestWrite
    ```
    This will display the content in the file TestWrite.


## Cracking

### password
- hashcat

    ```bash
    hashcat -h | grep -i ntlm
    ```

    This will try to find the word "ntlm" in the help page of hashcat.
    
    `-i` means to perform a case-insensitive match.

    ```bash
    hashcat -m 5600 hashes/giddy.ntlmv2 /opt/wordlists/rockyou.txt
    ```

    `-m` specifies the hash type.

    `hashes/giddy.ntlmv2` is the path of the hash file.

    ` /opt/wordlists/rockyou.txt` is the path of the wordlist.

## Others

### hiding information
- steghide

    ```bash
    steghide extract -sf irked.jpg -p UPupDOWNdownLRlrBAbaSSss
    ```

    The command above will try to extract the information embeded in the file according to the passphrase.

    `-sf` is the name of the input file to be extract.

    `-p` specifies the passphrase.