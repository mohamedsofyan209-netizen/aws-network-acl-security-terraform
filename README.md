# aws-network-acl-security-terraform
Enterprise Network Security Architecture implementing Extended ACLs and AWS NACLs / Security Groups via Terraform.
# 🛡️ Enterprise Network Security & Traffic Filtering (ACLs & AWS Security)

## 📌 Overview
This project demonstrates traffic filtering and granular security controls in an enterprise architecture. It features a Cisco Extended Access Control List (ACL) deployment in Packet Tracer to restrict access to sensitive database servers, mapped directly to **AWS Network ACLs (NACLs) & Security Groups** using **Terraform (IaC)**.

---

## 🔒 Security Policy Requirements
1. **Deny:** Block the Sales Department (`172.16.0.0/25`) from accessing the Database Server (`172.16.0.226/32`).
2. **Permit:** Allow the Development Department (`172.16.0.128/26`) and Admin Department (`172.16.0.192/27`) full access to the Database Server.
3. **Permit:** Allow all other inter-VLAN and cross-site communications.

---

## 🧪 Cisco IOS Extended ACL Configuration

```text
! Applied on Router-DC (Close to Destination)
ip access-list extended DENY_SALES_TO_DB
 deny ip 172.16.0.0 0.0.0.127 host 172.16.0.226
 permit ip any any
exit

interface GigabitEthernet0/1.40
 ip access-group DENY_SALES_TO_DB out
exit
