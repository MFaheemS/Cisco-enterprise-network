# Cisco-enterprise-network
End-to-end enterprise network implementation using Cisco technologies, featuring VLSM, multi-protocol routing, redistribution, DHCP, NAT, and ACL-based access control.


IMPLEMENTATION OVERVIEW
-----------------------
The implementation focuses on realistic enterprise practices, including:
- Variable Length Subnet Masking (VLSM)
- Multi-protocol routing
- Controlled route redistribution
- Centralized DHCP
- Network Address Translation (NAT)
- Access control using ACLs

All design decisions were made to ensure scalability, efficiency, and enforceable
network policies across the entire topology.


DESIGN APPROACH
---------------
The network was designed by first analyzing IP addressing constraints and host
requirements. A VLSM strategy was then developed to efficiently utilize address
space while allowing room for future growth.

Routing domains were intentionally segmented using different routing protocols
to simulate a heterogeneous enterprise environment. Redistribution was applied
only where required to maintain stability and avoid routing loops.

Security and traffic control were enforced at the routing layer using ACLs,
reflecting common real-world enterprise deployments.


IP ADDRESSING AND VLSM
---------------------
- All networks use Variable Length Subnet Masking (VLSM)
- Host requirements were prioritized from largest to smallest
- Alphabetically labeled networks were subnetted first
- Unlabeled networks (Routers 5–9) were assigned from unused VLSM blocks
- CIDR prefixes were expanded when host requirements exceeded original limits
- All CIDR adjustments were documented and justified in the VLSM tree

This approach ensures efficient address utilization and long-term scalability.


ROUTING ARCHITECTURE
--------------------
Multiple routing protocols were deployed to reflect real-world mixed environments.

Routing Protocols Used:
- OSPF Area 1 in the first block
- EIGRP (AS 11) in the second block
- RIP in the third block (first row)
- RIP in the second row (first block)
- OSPF Area 2 in the second row (last block)


ROUTE REDISTRIBUTION
--------------------
Controlled redistribution was implemented to ensure full connectivity:

- Router 1: OSPF ↔ EIGRP
- Router 2: OSPF ↔ RIP
- Router 3: EIGRP ↔ RIP
- Router 4:
  - OSPF Area 1 ↔ OSPF Area 2
  - Acts as an Area Border Router (ABR)

Redistribution was carefully configured to maintain predictable routing behavior
and prevent instability.


DHCP DESIGN
-----------
Two centralized DHCP servers were deployed.

DHCP Server 2 provides addresses to:
- OSPF Area 1
- EIGRP
- RIP (first row)

DHCP Server 1 provides addresses to:
- OSPF Area 2
- RIP (second row)

DHCP relay was configured on routers to allow hosts in different subnets to obtain
addresses from the appropriate server.


NAT CONFIGURATION
-----------------
- NAT is implemented on Router 10
- Network G is translated using the provided private IP address range
- Inside and outside interfaces are explicitly defined
- NAT enables internal hosts to communicate externally while preserving private IPs


ACCESS CONTROL AND TRAFFIC RESTRICTIONS
---------------------------------------
Extended ACLs were used to enforce access policies:

- One specific host in Network L is blocked from accessing the Web Server
- One specific host in Network E is blocked from accessing the Data Server (1st block)
- All hosts in Network A are blocked from accessing the TFTP Server

Servers are treated as standard hosts; no application services are required.
The focus is strictly on network-layer traffic control.


VALIDATION AND TESTING
---------------------
The network was verified using:
- End-to-end connectivity tests
- DHCP lease verification
- NAT translation table inspection
- ACL behavior validation
- Routing table consistency checks

All results align with the intended design and policies.


REPOSITORY CONTENTS
-------------------
- Cisco Packet Tracer (.pkt) file containing the complete implementation
- README documenting the design and configuration


SUMMARY
-------
This project demonstrates practical experience in designing and implementing a
multi-protocol enterprise network using Cisco technologies. It reflects real-world
decision-making, efficient address planning, controlled routing integration, and
policy-based access control rather than a purely academic exercise.
