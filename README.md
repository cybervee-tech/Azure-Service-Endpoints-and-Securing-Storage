# Azure-Service-Endpoints-and-Securing-Storage
 Private-only Azure File Share access using Service Endpoints &amp; NSG isolation – FuturinCLOUD Demonstrates subnet-restricted connectivity, public exposure elimination, and clear allowed/denied validation.
<div align="center">

  <p>AZ-500 Lab 5 | West US Region | March 2026</p>



</div>

## Project Summary

This lab demonstrates how to **eliminate public internet exposure** for an Azure File Share and enforce **subnet-level access isolation** using Virtual Network Service Endpoints and Network Security Groups.

**Security Objectives**
- Ensure all traffic to Azure Storage remains on the Azure backbone (private connectivity)  
- Restrict file share access to a single designated subnet only  
- Explicitly deny access from any other subnet or external network  
- Validate allowed vs. denied behavior with test VMs  

**Solution Delivered**
- VNet with private and public subnets  
- Storage service endpoint applied only to private subnet  
- NSG rules allowing SMB (port 445) exclusively from private subnet  
- Public network access disabled on storage account  
- Two test VMs placed in different subnets for clear validation  

## Architecture Delivered

- **VNet**: futuricloud-vnet (10.0.0.0/16)  
- **Subnets**:
  - private-subnet (10.0.1.0/24) – Microsoft.Storage service endpoint enabled  
  - public-subnet (10.0.2.0/24) – no endpoint  
- **NSGs**:
  - futuricloud-private-nsg – allows TCP 445 to Storage service tag  
  - futuricloud-public-nsg – allows RDP 3389 for testing  
- **Storage Account**: futuricloudstorage001  
- **File Share**: securefileshare  
- **Test VMs**:
  - vm-private (in allowed subnet)  
  - vm-public (in denied subnet)  

## Validation Results

| Test Case                               | VM Location       | Expected Outcome               | 
|-----------------------------------------|-------------------|--------------------------------|
| Mount file share (SMB)                  | private-subnet    | Successful connection          | 
| Mount file share (SMB)                  | public-subnet     | Connection fails / denied      | 
| Public internet access to storage       | Any               | Disabled / not possible        | 

## Full Documentation

📄 **Complete Lab 5 Documentation and screenshots (PDF)**  
[Open / View Full Report (PDF)](https://raw.githubusercontent.com/yourusername/your-repo-name/main/docs/Lab5-Securing-Azure-File-Shares-FuturinCLOUD.pdf)


## Challenges & Resolutions

- Service endpoint propagation delay → waited 1–2 minutes, refreshed VM networking page  
- DNS resolution issues → confirmed Azure DNS (168.63.129.16) was reachable  
- Storage connection refused on private VM → verified correct SMB path and storage account key  
- NSG rule not applying immediately → checked effective security rules on VM NIC  

## Conclusion

Lab 5 successfully demonstrated private-only access to Azure File Shares using service endpoints and NSG-based subnet isolation. The solution eliminates public exposure and enforces strict access control.i8

**FuturinCLOUD Limited** – Securing cloud environments across Africa  

