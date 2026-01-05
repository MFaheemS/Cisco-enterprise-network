# Cisco-enterprise-network
End-to-end enterprise network implementation using Cisco technologies, featuring VLSM, multi-protocol routing, redistribution, DHCP, NAT, and ACL-based access control.


The implementation focuses on realistic enterprise practices: variable-length subnetting, multi-protocol routing, controlled redistribution, centralized DHCP, NAT, and access control. All design choices were made to ensure scalability, efficiency, and policy enforcement across the network.

Design Approach

The network was built by first analyzing IP addressing constraints and host requirements, then designing a VLSM strategy that efficiently utilized address space while allowing future growth. Routing domains were segmented using different routing protocols to simulate a heterogeneous enterprise environment, with redistribution applied only where necessary to maintain stability and avoid routing loops.

Security and traffic control were handled at the routing layer using ACLs, reflecting how access policies are commonly enforced in real deployments.

IP Addressing and VLSM

All networks use Variable Length Subnet Masking (VLSM).

Host requirements were prioritized from largest to smallest to minimize address waste.

Networks labeled alphabetically were subnetted first.

Unlabeled networks (connected to Routers 5–9) were assigned from unused VLSM blocks.

When host requirements exceeded the capacity of the original CIDR block, the prefix length was expanded accordingly.

All CIDR adjustments were made deliberately and documented in the VLSM tree with justification.

This approach ensures efficient address utilization and long-term scalability.

Routing Architecture

Multiple routing protocols were intentionally deployed to reflect real-world mixed environments.

Routing Protocols

OSPF Area 1 in the first block

EIGRP (AS 11) in the second block

RIP in the third block (first row)

RIP in the second row (first block)

OSPF Area 2 in the second row (last block)

Route Redistribution

Controlled redistribution was implemented to provide full connectivity between routing domains:

Router 1: OSPF ↔ EIGRP

Router 2: OSPF ↔ RIP

Router 3: EIGRP ↔ RIP

Router 4:

OSPF Area 1 ↔ OSPF Area 2

Functions as an Area Border Router (ABR)

Redistribution was configured with care to maintain predictable routing behavior and prevent instability.

DHCP Design

Two centralized DHCP servers were used to simplify host configuration and management.

DHCP Server 2

Provides IP addresses to hosts in:

OSPF Area 1

EIGRP

RIP (first row)

DHCP Server 1

Provides IP addresses to hosts in:

OSPF Area 2

RIP (second row)

Routers were configured with DHCP relay to allow hosts in different subnets to obtain addresses from the appropriate server.

NAT Configuration

NAT is implemented on Router 10.

Network G is translated using the provided private IP address range.

Inside and outside interfaces are explicitly defined.

NAT enables internal hosts to communicate externally while preserving private addressing.

Access Control and Traffic Restrictions

Extended ACLs were used to enforce network access policies:

One specific host in Network L is blocked from accessing the Web Server.

One specific host in Network E is blocked from accessing the Data Server in the first block.

All hosts in Network A are blocked from accessing the TFTP Server.

The servers are treated as standard hosts; no application services are required to be running. The focus is strictly on traffic control at the network layer.

Validation and Testing

The network was verified using:

End-to-end connectivity testing across routing domains

DHCP lease validation

NAT translation table inspection

ACL behavior verification

Routing table consistency checks

All results align with the intended design and policies.

Repository Contents

Cisco Packet Tracer (.pkt) file containing the complete implementation

This README documenting the design and configuration

Summary

This project demonstrates practical experience in designing and implementing a multi-protocol enterprise network using Cisco technologies. It reflects real-world decision-making, efficient address planning, controlled routing integration, and policy-based access control rather than a purely theoretical or academic exercise.
