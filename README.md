# DNS Configuration and Troubleshooting

![DNS Configuration and Troubleshooting](https://poshac.me/docs/v4/assets/images/social/Guides/Troubleshooting-DNS-Validation.png)


This repository demonstrates configuring and troubleshooting DNS settings to ensure proper network connectivity and domain resolution.

## Skills Covered:
- Setting up DNS records and zones
- Troubleshooting DNS errors
- Configuring forward and reverse lookup zones
- Ensuring DNS resolves domain names correctly across the network

## Key Steps:
1. **Set up DNS zones** for internal and external network resolution.
2. **Configure forward lookup zones** for domain name resolution.
3. **Troubleshoot common DNS errors** using tools like `nslookup`.
4. **Verify DNS server settings** to ensure proper domain resolution.

Please refer to the [DNS Configuration Guide](https://learn.microsoft.com/en-us/entra/identity/domain-services/tutorial-create-instance) for step-by-step instructions.

---
**Resources:**
- [DNS Setup Documentation](https://learn.microsoft.com/en-us/search/?terms=DNS%20Setup%20Documentation)
- [DNS Troubleshooting Tools](https://learn.microsoft.com/en-us/search/?terms=DNS%20Troubleshooting%20Tools)



---


# **Domain Name System (DNS) Configuration and Management**

**Domain Name System (DNS)** makes the internet more user-friendly by translating readable domain names (e.g., `example.com`) into IP addresses that computers use to locate and communicate with each other. Essentially, DNS functions as the internet’s "phonebook," directing users to the correct website when they type a web address. This project will cover the essential steps for configuring DNS using Microsoft Azure and other network tools.

---

<details>
<summary>Technologies and Operating Systems Used</summary>

### **Technologies Used**
- **Remote Desktop**
- **Microsoft Azure**

### **Operating Systems Used**
- **Windows 10**
- **Windows Server 2022**

</details>

---

<details>
<summary>Definitions</summary>

- **Ping**: A network tool that tests the reachability of a host on an IP network.
- **Nslookup**: A tool for mapping IP addresses to domain names and troubleshooting DNS configurations.
- **Ipconfig**: Displays and manages network IP configurations, including IP addresses, subnet masks, and DNS servers.

</details>

---

<details>
<summary>Prerequisites</summary>

Before starting, ensure that:
1. **Virtual Machines**: The virtual machines for DNS configuration (e.g., Domain Controller on Windows Server 2022 and client on Windows 10) should be in the same resource group and virtual network.
2. **Static NIC and Matching DNS**: The NIC of the Domain Controller is set to **static**, and the client DNS matches the Domain Controller DNS. Configure these settings in Azure.

</details>

---

<details>
<summary>DNS Configuration Steps</summary>

#### **1. A Record Configuration**

1. **Login to Domain Controller and Client**: Access `DC-1` and `Client-1` as **(username)-admin**.
   
2. **Test DNS Connection on Client-1**:
   - Open PowerShell as admin.
   - Run `nslookup mainframe` to test DNS resolution. **Expected**: It won’t work initially.

3. **Create A Record on Domain Controller**:
   - On `DC-1`, open **DNS Manager**.
   - Navigate to **Forward Lookup Zone > Your Domain**.
   - Right-click, select **New Host (A)**.
   - Enter `mainframe` as the hostname and the IP address of `DC-1`.
   - Check the **first box** below to complete the setup.

4. **Verify DNS Resolution on Client-1**:
   - Back on `Client-1`, run `ping mainframe` in PowerShell to confirm connectivity.

---

#### **2. Local DNS Cache**

1. **Update DNS Record on Domain Controller**:
   - Edit the `mainframe` IP address on `DC-1` to `8.8.8.8`.

2. **Test Cache Resolution on Client-1**:
   - Run `ping mainframe` again; it won’t work as the cached DNS is outdated.

3. **Clear Client-1 DNS Cache**:
   - Use `ipconfig /displaydns` and then `ipconfig /flushdns` to clear the cache.

4. **Re-test DNS Resolution**:
   - Run `ping mainframe` again, and observe the updated IP address.

---

#### **3. CNAME Record Setup**

1. **Create CNAME Record on Domain Controller**:
   - On `DC-1`, go to the **DNS Manager** and select **New Alias (CNAME)**.
   - In the Alias name box, type `search`.
   - Enter `www.google.com` in the FQDN box. (Example purpose only.)

2. **Verify CNAME Resolution on Client-1**:
   - Back on `Client-1`, run `ping search` and `nslookup search` to confirm connectivity to `www.google.com`.

</details>

---

<details>
<summary>Resources to Learn DNS in Depth</summary>

For a deeper understanding of DNS, consider exploring resources such as **[Cloudflare's DNS Learning Center](https://www.cloudflare.com/learning/dns/what-is-dns/)**.

</details>

---

**Project Metadata**
- **Stars**: 0
- **Watchers**: 1
- **Forks**: 0
- **Resources**: README.md and Documentation
