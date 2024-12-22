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
Out of those 256 addresses, two addresses are reserved, and hense, can't be usable.
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


