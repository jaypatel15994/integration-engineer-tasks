# integration-engineer-tasks
My attempt to tasks similar to daily tasks of an Integration Engineer of an IT Company

We will Complete 5 tasks and document the changes. 

### <ins>Task 1: Network Debugging</ins>
Here we need to explain debugging steps for a web application in case of a form submission failure. 
We need to use browser's developer tools to identify the issue.

- Please check <code>task-1.txt</code> to know possible steps we can use, to navigate through this issue.
It includes steps to reproduce or identify most common issues with form submission. 

### <ins>Task 2: Network Configuration - Subnet Calculation</ins>

1. Number of available IP address in any /24 network is 256 (2 ^ 8).
Out of those 256 addresses, two addresses are reserved, and hence, can't be usable.
198.168.0.0 is Network address and 198.168.0.255 is Broadcast address. 

2. If we devide this network in two subnets, each will have 128 addresses.
For each subnet, two addresses will be reserved for network address and broadcast address, resulting in 126 usable addresses in each subnet. 
Subnet 1: 198.168.0.0 to 198.168.0.127
Subnet 2: 198.168.0.128 to 198.168.0.255

3. Subnetting means taking bits from host portion of a network and use it for creating new network identifiers. 
Each IP address has 32 bits which are divided into network and host portions.
For a /24 network, first 24 bits are network part and remaining 8 are for host part. 
When we subnet to a /25 network, 1 bit (25 - 24) is borrowed from network part.
This will create 2 (2 ^ 1) subnets and each subnet will have half of original hosts, and borrowed bit becomes part of network identifier.

### <ins>Task 3: File Management</ins>

1. Commands used to do file operations are as under.
    
    (i) - archiving and compressing:
    ```
    tar -czvf logs_archive.tar.gz ./logs/
    ```
    (ii) - Giving example of both commands for secure transfer.
    ```
    rsync -avz --partial --progress logs_archive.tar.gz user@server:/destination/
    OR
    scp -C logs_archive.tar.gz user@server:/destination/
    ```
    (iii) - Extraction
    ```
    # Create directory if doesn't exist, then extract.
    mkdir -p customerlogs

    tar -xzvf logs_archive.tar.gz -C customerlogs/
    ```

2. Handling file inturraption
- For rsync command, --partial flag keeps partially transmitted files, and the --progress flag shows progress of a file transfer. 
In case of interruption, we can run the same command and file transmission will resume from where it was interrupted. 

### <ins>Task 4: HTTPS Configuration</ins>
We can use <code>ssl_protocols TLSv1.2;</code>  in server setup to ensure that TLS 1.2 is enforced and older protocols are disabled.

Here is an example of server (nginx) setup:
```
server {
    listen 443 ssl;
    server_name demo.com;

    # SSL certificate and key
    ssl_certificate /etc/nginx/ssl/certificate.crt;
    ssl_certificate_key /etc/nginx/ssl/private.key;

    # configuration of ssl protocols
    ssl_protocols TLSv1.2;  # Here we are only allowing TLS 1.2
    
    # configuration of cipher suite 
    ssl_ciphers 'ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256';
    
    # security headers
    add_header Strict-Transport-Security "max-age=31536000; includeSubDomains" always;
    
    # Optimizing SSL configuration
    ssl_session_timeout 1d;
    ssl_session_cache shared:SSL:50m;
    ssl_session_tickets off;
    
    # Modern configuration
    ssl_prefer_server_ciphers on;
}
```

### <ins>Task 5: Troubleshooting Error Messages</ins>
A "No route to host" error indicated there is a network connectivity issue. 
There are couple of probable cause for this error.
Network configuration issue: It might be possible that the network we are trying to reach is set up incorrectly and has incorrect routing, or firewall is blocking port 443 of the network. It is also possible that there is an issue with DNS resolution. 
It is also possible that server is down or server is not running for port 443, or there is issue with load balancer. 

To resolve this issue, we can begin with basic connectivity tests for server and port.
```
# check if network is reachable
ping example.com

# check for DNS resolution existance
nslookup example.com

# Check TCP connection to port 443
telnet example.com 443

# Scan for port status
nc -zv example.com 443
```

We can also check if port is being filtered out or not by firewall with this command.
```
sudo netstat -tulpn | grep 443
```

### [ PS: For tasks #2 and #4 I had to google few things about network configuration as I have basic knowledge of networking and network debugging, but I have limited knowledge about setup of a network. I find it interesting and I can work on those skills. ]