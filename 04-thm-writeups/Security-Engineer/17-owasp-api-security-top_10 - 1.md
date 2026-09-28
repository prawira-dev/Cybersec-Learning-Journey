# OWASP API Security Top 10 - 1
##  Task 1: Introduction
* **Overview:** Introduces the fundamental goals of designing secure network architecture, highlighting how properly designed networks defend against unauthorized access, mitigate lateral movement, and protect critical assets.
* **Core Objectives:**
    * Understanding network segmentation and secure zoning principles.
    * Identifying strategies to minimize attack surfaces and manage traffic flow effectively.

## Task 2: Network Segmentation
* **Overview:** Explores the practice of dividing a physical or virtual network into distinct, isolated subnetworks (segments) to contain security breaches and control traffic flow.
* **Key Concepts:**
    * **VLANs & Trunks:** Utilizing Virtual Local Area Networks (VLANs) to logically segregate network traffic at Layer 2 and trunk lines to carry traffic across switches.
    * **Virtual Switching (e.g., Open vSwitch):** Adapting traditional switching concepts to virtualized and cloud environments to isolate guest virtual machines and containers.
    * **Attack Surface Reduction:** Limiting an attacker's ability to pivot laterally across the network if a single host becomes compromised.

## Task 3: Common Secure Network Architecture
* **Overview:** Covers standard architectural designs and structural zones used in enterprise environments to segregate systems based on trust levels and operational roles.
* **Key Network Zones:**
    * **External Zone:** The untrusted internet or public network.
    * **Demilitarized Zone (DMZ):** A perimeter subnetwork hosting public-facing services (e.g., public web servers) isolated from the internal network.
    * **Internal / Trusted Zone:** Houses internal corporate workstations, business applications, and intranet infrastructure.
    * **Restricted / High-Security Zone:** Highly isolated network segments reserved for critical assets (e.g., core Domain Controllers, payment databases, or critical infrastructure management).

## Task 4: Network Security Policies and Controls
* **Overview:** Focuses on defining administrative guidelines and technical controls that dictate how data and resources are protected within a network.
* **Key Concepts:**
    * **Policies vs. Controls:** Security policies set the organizational rules and guidelines, while security controls (such as firewalls, Access Control Lists [ACLs], IDS/IPS, NAC, and VPNs) enforce those rules in practice.
    * **Access Control Lists (ACLs):** Rules applied on routers or switches that evaluate packet headers (source/destination IP addresses, ports, and protocols) to explicitly allow or deny network traffic.
    * **Administrative Controls:** Establishing change management, user access governance, and acceptable use policies to maintain network consistency and compliance.

## Task 5: Zone-Pair Policies and Filtering
* **Overview:** Explores Zone-Based Policy Firewalls (ZFW), where network interfaces are grouped into logical security zones based on trust levels to control inter-zone traffic flow.
* **Key Concepts & Best Practices:**
    * **Zone Pairs:** Traffic policies are applied specifically to pairs of zones (e.g., External-to-DMZ or Internal-to-External), establishing granular rules for unidirectional or bidirectional communication.
    * **Default Deny Strategy:** Applying an implicit "deny all" rule by default for any unspecified zone-pair traffic, ensuring unapproved connections are automatically dropped.
    * **Preventing Lateral Movement:** Restricting direct paths between low-trust zones and sensitive internal networks to stop attackers from pivoting across network boundaries.

## Task 6: Validating Network Traffic
* **Overview:** Examines techniques and security platforms used to perform deep packet inspection and ensure network traffic adheres to legitimate, safe patterns.
* **Key Concepts & Security Platforms:**
    * **Deep Packet Inspection (DPI):** Analyzing packet payloads beyond basic Layer 3/4 headers to detect malware signatures, protocol anomalies, and unauthorized data transfers.
    * **SSL/TLS Inspection:** Utilizing proxies to decrypt, inspect, and re-encrypt encrypted traffic channels to prevent attackers from hiding malicious activities within HTTPS streams.
    * **Unified Threat Management (UTM):** Consolidating multiple security features—such as firewalls, intrusion prevention (IPS), anti-malware, and web filtering—into a single platform to process and validate intercepted network traffic.

## Task 7: Zero Trust Architecture (ZTA)
* **Overview:** Focuses on the Zero Trust security model, which operates under the fundamental principle of "never trust, always verify"—assuming that threats exist both outside and inside the traditional network perimeter.
* **Key Concepts:**
    * **Explicit Verification:** Always authenticating and authorizing based on all available data points (user identity, location, device health, service, and workload context) before granting access.
    * **Micro-segmentation:** Breaking down network security perimeters into granular, isolated zones to restrict east-west lateral movement across workloads and services.
    * **Least Privilege Access:** Granting users and services only the minimal access necessary (Just-In-Time and Just-Enough-Access) to perform their specific functions.

## Task 8: Conclusion
* **Overview:** Wraps up the room by summarizing the core tenets of modern network design and defense.
* **Key Takeaways:**
    * **A secure network architecture** relies on a multi-layered defense-in-depth approach combining segmentation, strict zone-pair filtering, deep traffic validation, and zero-trust principles.
    * **Regularly reviewing and updating network security controls** ensures that enterprise infrastructure remains resilient against evolving threat landscapes and lateral movement techniques.