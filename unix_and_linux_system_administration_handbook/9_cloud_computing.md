# 9 Cloud Computing

The practice of leasing computer resources from a pool of shared capacity

Grouped into 3 categories

1. **Infrastructure as a Service (IaaS)**: users request raw compute memory, network, and storage resources
2. **Platfotm as a Service (PaaS)**: users submit custom applications for vendors to run on their behalf
3. **Software as a Service (SaaS)**: vendor hosts and manages software and users pay some kind of subscription

**Virtual private serves** or **instances** are VMs running on provider's hardware

- Can have unlimited number of them (limit is resource)

Instances are created from "images", the saved state of an OS that includes a root filesystem and a boot loader

It is possible to create virtual networks with custom topologies that isolate your system from each other and the Internet

Some important ways to store data in the cloud:

- Object stores contain collections of discrete objects in a flat namespace
- Block storage are virtualize hard disks
- Ephemeral storage is temporary, non persistent storage

Access control should follow the principle of least privilage

- everything should be granted the minimum level of access unless otherwise

AWS Identity and Access Management (IAM) defines users, groups, and roles for systems

- server can be assigned policies

Automation allows for starting systems usually involve submiting a template to CloudFormation (usually in JSON or YAML) and then letting Terraform call the proper API

**Serverless functions** allow developers to perform server responses without managing a server or infrastructure
