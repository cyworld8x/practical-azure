### Explanation of Subnet 10.0.0.0/24

To understand the subnet 10.0.0.0/24, we need to grasp some basic concepts about networking and IP addresses.

#### IP Address and Subnet

*   **IP Address**: A unique string of numbers assigned to each device connected to a network. For example, 10.0.0.1.
    
*   **Subnet**: A subdivision of a larger network, created to manage and optimize network traffic.
    

#### CIDR Notation

*   **CIDR (Classless Inter-Domain Routing)**: A method for allocating IP addresses and IP routing. It uses the format x.x.x.x/y, where x.x.x.x is the IP address and y is the number of bits in the network portion of the address.
    

#### Explanation of 10.0.0.0/24

*   **10.0.0.0**: This is the network address.
    
*   **/24**: This is the subnet mask, indicating that the first 24 bits of the IP address are the network part. This means the network portion of the IP address is 10.0.0, and the remaining 8 bits are used for host addresses within the network.
    

#### Details of Subnet 10.0.0.0/24

*   **Network Address**: 10.0.0.0
    
*   **Subnet Mask**: 255.255.255.0 (equivalent to /24)
    
*   **Number of Usable IP Addresses**: 2^8 - 2 = 254 addresses (subtracting 2 addresses reserved for the network address and the broadcast address).
    

#### Example

*   **First Usable IP Address**: 10.0.0.1
    
*   **Last Usable IP Address**: 10.0.0.254
    
*   **Broadcast Address**: 10.0.0.255

### Steps to Create a Public IP Address, Associate it to a Network Interface Card (NIC), and Open a Port for Internet Access on Azure
--------------------------------

#### 1\. Create a Public IP Address

1.  **Sign in to Azure**:
    
    *   Go to the Azure portal and sign in with your Azure account.
        
2.  **Create a Public IP Address**:
    
    *   Navigate to **Create a resource** > **Networking** > **Public IP address**.
        
    *   Fill in the required details:
        
        *   **Subscription**: Select your subscription.
            
        *   **Resource group**: Create a new one or select an existing one.
            
        *   **Name**: Enter a name for your public IP address.
            
        *   **Region**: Select your preferred region.
            
        *   **SKU**: Choose between Basic or Standard.
            
        *   **IP Version**: Select IPv4 or IPv6.
            
        *   **IP address assignment**: Choose Static or Dynamic.
            
    *   Click **Review + create**, then **Create** [(0)](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/create-public-ip-portal)[(1)](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/create-public-ip-portal).
        

#### 2\. Associate the Public IP Address to a NIC

1.  **Navigate to the Virtual Machine**:
    
    *   In the Azure portal, go to **Virtual machines** and select the VM you want to associate the public IP address with.
        
2.  **Select the Network Interface**:
    
    *   Under **Settings**, select **Networking**.
        
    *   Click on the network interface (NIC) associated with the VM.
        
3.  **Associate the Public IP Address**:
    
    *   Under **Settings** for the NIC, select **IP configurations**.
        
    *   Select the IP configuration you want to associate the public IP address with.
        
    *   Click **Associate public IP address**, then select the public IP address you created earlier from the drop-down list.
        
    *   Click **Save** [(0)](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/create-public-ip-portal)[(1)](https://learn.microsoft.com/en-us/azure/virtual-network/ip-services/associate-public-ip-address-vm).
        

#### 3\. Open a Port for Internet Access

1.  **Navigate to the Network Security Group (NSG)**:
    
    *   In the Azure portal, go to **Network security groups** and select the NSG associated with your VM’s subnet or NIC.
        
2.  **Add an Inbound Security Rule**:
    
    *   Under **Settings**, select **Inbound security rules**.
        
    *   Click **Add** to create a new rule.
        
    *   Fill in the required details:
        
        *   **Source**: Any or specify an IP range.
            
        *   **Source port ranges**: \* (all ports) or specify a range.
            
        *   **Destination**: Any.
            
        *   **Destination port ranges**: Enter the port number you want to open (e.g., 80 for HTTP, 443 for HTTPS).
            
        *   **Protocol**: TCP or UDP.
            
        *   **Action**: Allow.
            
        *   **Priority**: Set a priority value (lower numbers have higher priority).
            
        *   **Name**: Enter a name for the rule.
            
    *   Click **Add** to create the rule [(0)](https://learn.microsoft.com/en-us/answers/questions/1190066/how-can-i-open-a-port-in-azure-so-that-a-constant)

### Key Points to Understand About Network Security Groups (NSGs) in Azure
-----------------------

#### 1. **Purpose of NSGs**

*   **Traffic Filtering**: NSGs are used to filter network traffic to and from Azure resources within an Azure Virtual Network. They contain security rules that allow or deny inbound and outbound network traffic based on various criteria [(1}](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview).
    

#### 2. **Security Rules**

*   **Inbound and Outbound Rules**: NSGs can have multiple inbound and outbound security rules. Each rule specifies the source and destination, port, and protocol [(1)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works).
    
*   **Rule Properties**: Each rule has properties such as name, priority, source, destination, port, and protocol. Rules are processed in priority order, with lower numbers having higher priority [(1)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview).
    

#### 3. **Association**

*   **Subnets and NICs**: NSGs can be associated with either subnets or individual network interfaces (NICs) of virtual machines. This allows for flexible and granular control over network traffic [(1)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works).
    
*   **Multiple Associations**: The same NSG can be associated with multiple subnets and NICs, providing a centralized way to manage security rules [(1)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-group-how-it-works).
    

#### 4. **Default Security Rules**

*   **Predefined Rules**: Azure provides default security rules that are automatically applied to NSGs. These rules ensure basic network security and can be overridden by custom rules [(1)]](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview).
    

#### 5. **Augmented Security Rules**

*   [**Enhanced Capabilities**: Augmented security rules allow you to specify multiple IP addresses and IP address ranges in a single rule, reducing the number of rules needed [(1)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview).
    

#### 6. **Priority and Processing**

*   **Rule Processing Order**: Rules are processed in order of priority. Once traffic matches a rule, processing stops. This means that higher priority (lower number) rules take precedence over lower priority (higher number) rules [(1)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview).
    

#### 7. **Common Use Cases**

*   **Restricting Access**: NSGs can be used to restrict access to specific resources, such as allowing only certain IP addresses to access a virtual machine.
    
*   **Segmentation**: They help in segmenting network traffic within a virtual network, ensuring that only authorized traffic can flow between different subnets or resources [(1)](https://karansingh.gitbook.io/az-900-notes/securing-networks/network-security-groups)

### Steps to Create a User-Defined Route (UDR) in Azure
------------------------------------
#### 1\. Sign in to Azure

*   Go to the Azure portal and sign in with your Azure account.
    

#### 2\. Create a Route Table

1.  **Navigate to Route Tables**:
    
    *   In the Azure portal, select **Create a resource** > **Networking** > **Route table**.
        
2.  **Configure the Route Table**:
    
    *   Fill in the required details:
        
        *   **Subscription**: Select your subscription.
            
        *   **Resource group**: Create a new one or select an existing one.
            
        *   **Name**: Enter a name for your route table.
            
        *   **Region**: Select your preferred region.
            
    *   Click **Review + create**, then **Create** [(0)](https://learn.microsoft.com/en-us/azure/virtual-network-manager/how-to-create-user-defined-route)
        

#### 3\. Add a Route to the Route Table

1.  **Navigate to the Route Table**:
    
    *   Once the route table is created, go to **Route tables** in the Azure portal and select the route table you just created.
        
2.  **Add a Route**:
    
    *   Under **Settings**, select **Routes**.
        
    *   Click **Add** to create a new route.
        
    *   Fill in the required details:
        
        *   **Route name**: Enter a name for the route.
            
        *   **Address prefix**: Specify the destination IP address range (e.g., 0.0.0.0/0 for all traffic).
            
        *   **Next hop type**: Select the next hop type (e.g., Virtual appliance, Virtual network gateway, Internet, etc.).
            
        *   **Next hop address**: Enter the IP address of the next hop (if applicable).
            
    *   Click **OK** to add the route [(1)](https://learn.microsoft.com/en-us/azure/virtual-network-manager/how-to-create-user-defined-route)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview).
        

#### 4\. Associate the Route Table with a Subnet

1.  **Navigate to the Subnet**:
    
    *   In the Azure portal, go to **Virtual networks** and select the virtual network containing the subnet you want to associate with the route table.
        
2.  **Associate the Route Table**:
    
    *   Under **Settings**, select **Subnets**.
        
    *   Select the subnet you want to associate with the route table.
        
    *   Under **Route table**, select the route table you created earlier.
        
    *   Click **Save**[(1)](https://learn.microsoft.com/en-us/azure/virtual-network-manager/how-to-create-user-defined-route)[(2)](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-networks-udr-overview).

### Steps to Set Up NAT Rule, Network Rule, and Application Rule on Azure Firewall
-------------------------------

#### 1\. Set Up a NAT Rule

1.  **Sign in to Azure**:
    
    *   Go to the Azure portal and sign in with your Azure account.
        
2.  **Navigate to Your Azure Firewall**:
    
    *   In the Azure portal, go to **All services** > **Firewall** and select your Azure Firewall instance.
        
3.  **Create a NAT Rule Collection**:
    
    *   Under **Settings**, select **Rules**.
        
    *   Select the **NAT rule collection** tab and click **\+ Add NAT rule collection**.
        
    *   Fill in the required details:
        
        *   **Name**: Enter a name for the rule collection.
            
        *   **Priority**: Set the priority (lower numbers have higher priority).
            
        *   **Action**: Select **Dnat**.
            
    *   Add a rule to the collection:
        
        *   **Name**: Enter a name for the rule.
            
        *   **Source**: Specify the source IP address or range.
            
        *   **Destination**: Enter the destination IP address or range.
            
        *   **Destination ports**: Specify the destination port(s).
            
        *   **Translated address**: Enter the internal IP address to which the traffic should be translated.
            
        *   **Translated port**: Specify the internal port.
            
    *   Click **Add** to create the rule [[1]](https://petri.com/understanding-and-creating-nat-rules-in-azure-firewall/) [[2]](https://petri.com/understanding-and-creating-nat-rules-in-azure-firewall/).
        

#### 2\. Set Up a Network Rule

1.  **Navigate to Your Azure Firewall**:
    
    *   In the Azure portal, go to **All services** > **Firewall** and select your Azure Firewall instance.
        
2.  **Create a Network Rule Collection**:
    
    *   Under **Settings**, select **Rules**.
        
    *   Select the **Network rule collection** tab and click **\+ Add network rule collection**.
        
    *   Fill in the required details:
        
        *   **Name**: Enter a name for the rule collection.
            
        *   **Priority**: Set the priority (lower numbers have higher priority).
            
        *   **Action**: Select **Allow** or **Deny**.
            
    *   Add a rule to the collection:
        
        *   **Name**: Enter a name for the rule.
            
        *   **Protocol**: Select the protocol (TCP, UDP, etc.).
            
        *   **Source**: Specify the source IP address or range.
            
        *   **Source ports**: Specify the source port(s).
            
        *   **Destination**: Enter the destination IP address or range.
            
        *   **Destination ports**: Specify the destination port(s).
            
    *   Click **Add** to create the rule [[1]](https://techcommunity.microsoft.com/t5/azure-architecture/azure-firewall-deploy-configure-amp-control-network-access/td-p/1574830)

#### 3\. Set Up an Application Rule

1.  **Navigate to Your Azure Firewall**:
    
    *   In the Azure portal, go to **All services** > **Firewall** and select your Azure Firewall instance.
        
2.  **Create an Application Rule Collection**:
    
    *   Under **Settings**, select **Rules**.
        
    *   Select the **Application rule collection** tab and click **\+ Add application rule collection**.
        
    *   Fill in the required details:
        
        *   **Name**: Enter a name for the rule collection.
            
        *   **Priority**: Set the priority (lower numbers have higher priority).
            
        *   **Action**: Select **Allow** or **Deny**.
            
    *   Add a rule to the collection:
        
        *   **Name**: Enter a name for the rule.
            
        *   **Source**: Specify the source IP address or range.
            
        *   **Protocol**: Select the protocol (HTTP, HTTPS, etc.).
            
        *   **Target FQDNs**: Enter the Fully Qualified Domain Names (FQDNs) that the rule applies to.
            
    *   Click **Add** to create the rule [[1]](https://learn.microsoft.com/en-us/azure/firewall/tutorial-firewall-deploy-portal)


### Steps to Create and Configure Network Peering in Azure
-----------------------------------------

#### 1\. Sign in to Azure

*   Go to the Azure portal and sign in with your Azure account.
    

#### 2\. Create Virtual Networks

1.  **Create the First Virtual Network**:
    
    *   Navigate to **Create a resource** > **Networking** > **Virtual network**.
        
    *   Fill in the required details:
        
        *   **Subscription**: Select your subscription.
            
        *   **Resource group**: Create a new one or select an existing one.
            
        *   **Name**: Enter a name for your virtual network (e.g., vnet1).
            
        *   **Region**: Select your preferred region.
            
        *   **Address space**: Enter the address range (e.g., 10.0.0.0/16).
            
    *   Click **Review + create**, then **Create**.
        
2.  **Create the Second Virtual Network**:
    
    *   Repeat the above steps to create another virtual network (e.g., vnet2) with a different address space (e.g., 10.1.0.0/16).
        

#### 3\. Create Peering Between Virtual Networks

1.  **Navigate to the First Virtual Network**:
    
    *   In the Azure portal, go to **Virtual networks** and select the first virtual network (vnet1).
        
2.  **Add Peering**:
    
    *   Under **Settings**, select **Peerings**.
        
    *   Click **\+ Add** to create a new peering.
        
    *   Fill in the required details:
        
        *   **Name**: Enter a name for the peering (e.g., vnet1-to-vnet2).
            
        *   **Peer virtual network**: Select the second virtual network (vnet2).
            
        *   **Traffic to remote virtual network**: Select **Allow**.
            
        *   **Traffic forwarded from remote virtual network**: Select **Allow** if you want to allow traffic forwarding.
            
        *   **Virtual network gateway or Route Server**: Select **None** unless you have specific requirements.
            
    *   Click **Add** to create the peering [[0]](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-peering)[[1]](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-peering).
        
3.  **Repeat for the Second Virtual Network**:
    
    *   Navigate to the second virtual network (vnet2).
        
    *   Under **Settings**, select **Peerings**.
        
    *   Click **\+ Add** to create a new peering.
        
    *   Fill in the required details:
        
        *   **Name**: Enter a name for the peering (e.g., vnet2-to-vnet1).
            
        *   **Peer virtual network**: Select the first virtual network (vnet1).
            
        *   **Traffic to remote virtual network**: Select **Allow**.
            
        *   **Traffic forwarded from remote virtual network**: Select **Allow** if you want to allow traffic forwarding.
            
        *   **Virtual network gateway or Route Server**: Select **None** unless you have specific requirements.
            
    *   Click **Add** to create the peering [[1]](https://learn.microsoft.com/en-us/azure/virtual-network/tutorial-connect-virtual-networks-portal).
        

#### 4\. Verify Peering

*   **Check Peering Status**:
    
    *   Go to **Virtual networks** and select each virtual network.
        
    *   Under **Settings**, select **Peerings**.
        
    *   Ensure the peering status is **Connected** for both virtual networks [[1]](https://learn.microsoft.com/en-us/azure/virtual-network/virtual-network-manage-peering)


### Steps to Configure Public DNS and Private DNS in Azure
---------------------------

#### Configuring Public DNS

1.  **Sign in to Azure**:
    
    *   Go to the Azure portal and sign in with your Azure account.
        
2.  **Create a Public DNS Zone**:
    
    *   Navigate to **Create a resource** > **Networking** > **DNS zone**.
        
    *   Fill in the required details:
        
        *   **Subscription**: Select your subscription.
            
        *   **Resource group**: Create a new one or select an existing one.
            
        *   **Name**: Enter the domain name (e.g., contoso.com).
            
        *   **Resource group location**: Select your preferred region.
            
    *   Click **Review + create**, then **Create** [[1]](https://learn.microsoft.com/en-us/azure/dns/dns-getstarted-portal).
        
3.  **Create DNS Records**:
    
    *   Once the DNS zone is created, go to **DNS zones** and select your DNS zone.
        
    *   Click **\+ Record set** to add a new DNS record.
        
    *   Fill in the required details:
        
        *   **Name**: Enter the subdomain (e.g., www).
            
        *   **Type**: Select the record type (e.g., A for IPv4 address).
            
        *   **TTL**: Set the time-to-live value.
            
        *   **IP address**: Enter the IP address the domain should resolve to.
            
    *   [Click **OK** to create the record [[1]](https://learn.microsoft.com/en-us/azure/dns/dns-getstarted-portal).
        
4.  **Delegate the Domain to Azure DNS**:
    
    *   Retrieve the name servers from the DNS zone overview.
        
    *   Go to your domain registrar’s website and update the name server settings to point to the Azure DNS name servers [[1]]](https://learn.microsoft.com/en-us/azure/dns/dns-getstarted-portal)[2](https://learn.microsoft.com/en-us/azure/dns/dns-delegate-domain-azure-dns).
        

#### Configuring Private DNS

1.  **Sign in to Azure**:
    
    *   Go to the Azure portal and sign in with your Azure account.
        
2.  **Create a Private DNS Zone**:
    
    *   Navigate to **Create a resource** > **Networking** > **Private DNS zone**.
        
    *   Fill in the required details:
        
        *   **Subscription**: Select your subscription.
            
        *   **Resource group**: Create a new one or select an existing one.
            
        *   **Name**: Enter the domain name (e.g., private.contoso.com).
            
    *   Click **Review + create**, then **Create** [[1]](https://learn.microsoft.com/en-us/azure/dns/private-dns-getstarted-portal).
        
3.  **Link the Private DNS Zone to a Virtual Network**:
    
    *   Go to **Private DNS zones** and select your private DNS zone.
        
    *   Under **Settings**, select **Virtual network links**.
        
    *   Click **\+ Add** to create a new link.
        
    *   Fill in the required details:
        
        *   **Link name**: Enter a name for the link.
            
        *   **Virtual network**: Select the virtual network to link.
            
        *   **Enable auto registration**: Enable this option if you want Azure to automatically manage DNS records for VMs in the network.
            
    *   Click **OK** to create the link [[3]](https://learn.microsoft.com/en-us/azure/dns/private-dns-getstarted-portal).
        
4.  **Create DNS Records**:
    
    *   Go to **Private DNS zones** and select your private DNS zone.
        
    *   Click **\+ Record set** to add a new DNS record.
        
    *   Fill in the required details:
        
        *   **Name**: Enter the subdomain (e.g., vm1).
            
        *   **Type**: Select the record type (e.g., A for IPv4 address).
            
        *   **TTL**: Set the time-to-live value.
            
        *   **IP address**: Enter the IP address the domain should resolve to.
            
    *    Click **OK** to create the record [[3]](https://learn.microsoft.com/en-us/azure/dns/private-dns-getstarted-portal). 
        

### Advanced Use of Public and Private DNS in Azure

#### Public DNS

*   **Custom Domains for Azure Services**: Use public DNS to map custom domain names to Azure services like Azure App Service, Azure Storage, or Azure CDN. This allows users to access your services using friendly domain names.
    
*   **Traffic Management**: Combine Azure DNS with Azure Traffic Manager to distribute traffic across multiple endpoints globally, improving performance and availability.
    

#### Private DNS

*   **Private Link Integration**: Use private DNS zones to resolve private endpoints for Azure services like Azure SQL Database, Azure Storage, and more. This ensures that traffic stays within your virtual network, enhancing security [[4]](https://learn.microsoft.com/en-us/azure/private-link/private-endpoint-dns-integration).
    
*   **Hybrid Scenarios**: Integrate private DNS with on-premises networks using Azure Private Resolver or custom DNS servers. This allows seamless name resolution across hybrid environments [[4]](https://learn.microsoft.com/en-us/azure/private-link/private-endpoint-dns-integration).
    
*   **Split-Horizon DNS**: Implement split-horizon DNS by creating both public and private DNS zones with the same name. This allows different DNS responses based on the source of the query, useful for scenarios where internal and external clients need different DNS resolutions [[5]](https://learn.microsoft.com/en-us/azure/dns/private-dns-overview).


### Key Differences Between Virtual Network Peering and Network Gateway in Azure
---------------------------
#### Virtual Network Peering

1.  **Purpose**:
    
    *   **Seamless Connectivity**: Connects two Azure virtual networks, making them appear as one for connectivity purposes [[1]](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/vnet-peering).
        
    *   **Private Traffic**: Traffic between peered virtual networks is routed through the Microsoft backbone infrastructure, ensuring it remains private and does not traverse the public internet [[1]](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/vnet-peering).
        
2.  **Performance**:
    
    *   **Low Latency**: Provides low-latency, high-bandwidth connections because there are no gateways or extra hops involved [[2]](https://azure.microsoft.com/en-us/blog/vnet-peering-and-vpn-gateways/).
        
    *   **High Bandwidth**: Suitable for scenarios requiring high bandwidth, such as cross-region data replication and database failover [[2]](https://azure.microsoft.com/en-us/blog/vnet-peering-and-vpn-gateways/).
        
3.  **Use Cases**:
    
    *   **Cross-Region Connectivity**: Ideal for connecting virtual networks across different Azure regions (global peering) [[1]](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/vnet-peering).
        
    *   **Strict Data Policies**: Preferred when strict data policies require that traffic does not leave the Microsoft backbone [[2]](https://azure.microsoft.com/en-us/blog/vnet-peering-and-vpn-gateways/).
        

#### Network Gateway (VPN Gateway)

1.  **Purpose**:
    
    *   **Cross-Premises Connectivity**: Used to send traffic between an Azure virtual network and an on-premises location over the public internet [[1]](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/vnet-peering).
        
    *   **VNet-to-VNet Connectivity**: Can also be used to connect Azure virtual networks via VPN [[1]](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/vnet-peering).
        
2.  **Performance**:
    
    *   **Limited Bandwidth**: Provides a limited bandwidth connection, which may not be suitable for high-bandwidth requirements [[2]](https://azure.microsoft.com/en-us/blog/vnet-peering-and-vpn-gateways/).
        
    *   **Encryption**: Offers encrypted connections, which is beneficial for secure data transmission[[2]](https://azure.microsoft.com/en-us/blog/vnet-peering-and-vpn-gateways/).
        
3.  **Use Cases**:
    
    *   **Hybrid Scenarios**: Ideal for hybrid cloud scenarios where connectivity between on-premises networks and Azure is required [[1]](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/vnet-peering).
        
    *   **Encryption Needs**: Suitable for scenarios where data encryption is necessary, even if it means tolerating bandwidth restrictions [[2]](https://azure.microsoft.com/en-us/blog/vnet-peering-and-vpn-gateways/).
        

#### Summary

*   **Virtual Network Peering**: Best for low-latency, high-bandwidth, private connections within Azure, especially when strict data policies are in place.
    
*   **Network Gateway (VPN Gateway)**: Best for secure, encrypted connections between Azure and on-premises networks or between Azure virtual networks, even if it involves bandwidth limitations [[1]](https://learn.microsoft.com/en-us/azure/architecture/reference-architectures/hybrid-networking/vnet-peering)