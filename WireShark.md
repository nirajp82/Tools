# Wireshark Command/Cheatsheet

This README provides an overview of essential Wireshark commands, filters, keyboard shortcuts, and more, helping you effectively capture, analyze, and troubleshoot network traffic.

---

### Table of Contents

1. [Default Columns in a Packet Capture Output](#default-columns-in-a-packet-capture-output)
2. [Logical Operators](#logical-operators)
3. [Filtering Packets (Display Filters)](#filtering-packets-display-filters)
4. [Filter Types](#filter-types)
5. [Wireshark Capturing Modes](#wireshark-capturing-modes)
6. [Miscellaneous Features](#miscellaneous)
7. [Capture and Display Filter Syntax](#capture-and-display-filter-syntax)
8. [Keyboard Shortcuts - Main Display Window](#keyboard-shortcuts---main-display-window)
9. [Protocols - Values](#protocols---values)
10. [Common Filtering Commands](#common-filtering-commands)
11. [Special Operators](#Special-Operators)

## Default Columns in a Packet Capture Output

In Wireshark, the packet capture output contains a variety of columns to help you analyze network traffic. Below are the default columns displayed in a packet capture output.

| **Name**        | **Description**                                                                          |
|-----------------|------------------------------------------------------------------------------------------|
| **No.**         | Frame number from the beginning of the packet capture.                                  |
| **Time**        | Seconds from the first frame.                                                           |
| **Source (src)**| Source address, commonly an IPv4, IPv6, or Ethernet address.                           |
| **Destination (dst)**| Destination address.                                                                   |
| **Protocol**    | Protocol used in the Ethernet frame, IP packet, or TCP segment (e.g., TCP, UDP, HTTP).   |
| **Length**      | Length of the frame in bytes.                                                           |

These columns provide basic information about each captured packet. You can customize the columns displayed in Wireshark to suit your specific needs.

---

## Logical Operators

Logical operators in Wireshark display filters allow you to combine multiple conditions in a filter expression. Here are the most commonly used logical operators:

| **Operator**       | **Description**                          | **Example**                                                                                   |
|--------------------|------------------------------------------|-----------------------------------------------------------------------------------------------|
| **and** or **&&**   | **Logical AND**                          | All the conditions should match. Example: `ip.src == 192.168.1.1 and tcp.port == 80`         |
| **or** or **||**    | **Logical OR**                           | Either all or one of the conditions should match. Example: `ip.src == 192.168.1.1 or tcp.port == 443` |
| **xor** or **^^**   | **Logical XOR (Exclusive OR)**           | Exclusive alterations - only one of the two conditions should match, not both. Example: `ip.src == 192.168.1.1 xor ip.dst == 192.168.1.2` |
| **not** or **!**    | **Negation**                             | Inverts the condition. Example: `not ip.addr == 192.168.1.1` (show packets not from this IP) |
| **[n]** or **[...]**| **Substring operator**                   | Filters for specific words or text within the packet. Example: `http contains "GET"`              |

---

## Filtering Packets (Display Filters)

Display filters in Wireshark are used to selectively show packets based on various conditions. Below are common filter operators with examples:

| **Operator**       | **Description**                           | **Example**                                |
|--------------------|-------------------------------------------|--------------------------------------------|
| **eq** or **==**   | **Equal**                                 | `ip.dst == 192.168.1.1`                    |
| **ne** or **!=**   | **Not equal**                             | `ip.dst != 192.168.1.1`                    |
| **gt** or **>**    | **Greater than**                          | `frame.len > 10`                           |
| **lt** or **<**    | **Less than**                             | `frame.len < 10`                           |
| **ge** or **>=**   | **Greater than or equal**                 | `frame.len >= 10`                          |
| **le** or **<=**   | **Less than or equal**                    | `frame.len <= 10`                          |

### Explanation of Filtering Operators

1. **Equal (`eq`, `==`)**:
   - Filters packets that match a specific value.
   - **Example**: 
     ```bash
     ip.dst == 192.168.1.1
     ```
     This filter will show packets where the destination IP address is exactly `192.168.1.1`.

2. **Not Equal (`ne`, `!=`)**:
   - Filters packets that do **not** match a specific value.
   - **Example**:
     ```bash
     ip.dst != 192.168.1.1
     ```
     This filter will exclude packets where the destination IP address is `192.168.1.1`.

3. **Greater Than (`gt`, `>`)**:
   - Filters packets where the value is greater than the specified threshold.
   - **Example**:
     ```bash
     frame.len > 10
     ```
     This filter will show packets where the frame length is greater than 10 bytes.

4. **Less Than (`lt`, `<`)**:
   - Filters packets where the value is less than the specified threshold.
   - **Example**:
     ```bash
     frame.len < 10
     ```
     This filter will show packets where the frame length is less than 10 bytes.

5. **Greater Than or Equal (`ge`, `>=`)**:
   - Filters packets where the value is greater than or equal to the specified threshold.
   - **Example**:
     ```bash
     frame.len >= 10
     ```
     This filter will show packets with frame lengths greater than or equal to 10 bytes.

6. **Less Than or Equal (`le`, `<=`)**:
   - Filters packets where the value is less than or equal to the specified threshold.
   - **Example**:
     ```bash
     frame.len <= 10
     ```
     This filter will show packets with frame lengths less than or equal to 10 bytes.

---

## Filter Types

Wireshark supports two types of filters:

| **Name**            | **Description**                                                           |
|---------------------|---------------------------------------------------------------------------|
| **Capture filter**   | Filters packets during the capture process, reducing the amount of traffic stored in the capture file. |
| **Display filter**   | Filters packets after they have been captured, allowing you to hide unwanted packets from the display. |

---

## Wireshark Capturing Modes

Wireshark can be configured to capture packets in different modes, depending on the network interface.

| **Name**            | **Description**                                                                 |
|---------------------|---------------------------------------------------------------------------------|
| **Promiscuous mode**| Configures the network interface to capture all packets on the network segment to which it is connected. |
| **Monitor mode**    | Enables wireless interfaces (only on Unix/Linux systems) to capture all traffic that the interface can receive, including traffic not directed to the capturing device. |

---

## Miscellaneous

| **Name**                | **Description**                                                                 |
|-------------------------|---------------------------------------------------------------------------------|
| **Slice Operator**       | `[...]` - A range of values, e.g., `frame[0:4]` extracts the first 4 bytes. |
| **Membership Operator**  | `{}` - "In" operator to check if a value belongs to a set (e.g., `ip.addr in {192.168.1.1, 192.168.1.2}`). |
| **CTRL+E**               | Start or stop packet capture.                                                  |

---

## Capture and Display Filter Syntax

Understanding the syntax for capture and display filters is crucial for narrowing down packets of interest. Below are examples of filter syntax for both capture and display filters:

### Capture Filter Syntax

Capture filters are used to capture only the packets that meet specific conditions. They are applied before data is captured.

| **Syntax**                     | **Protocol**   | **Direction**   | **Hosts**             | **Value**         | **Logical Operator** | **Expressions**           |
|---------------------------------|----------------|-----------------|-----------------------|-------------------|----------------------|---------------------------|
| **Example**                    | `tcp`          | `src`           | `192.168.1.1`         | `80`              | `and`                | `tcp dst 202.164.30.1`    |

### Display Filter Syntax

Display filters are applied after data is captured, allowing you to refine your packet display.

| **Syntax**                     | **Protocol**   | **String 1**   | **String 2**  | **Comparison Operator** | **Value**         | **Logical Operator** | **Expressions**           |
|---------------------------------|----------------|----------------|---------------|-------------------------|-------------------|----------------------|---------------------------|
| **Example**                    | `http`          | `dest`         | `ip`           | `==`                    | `192.168.1.1`     | `and`                | `tcp port`                |

---

## Keyboard Shortcuts - Main Display Window

Wireshark provides several keyboard shortcuts to navigate efficiently through the packet list and details:

| **Accelerator**        | **Description**                                                                 |
|------------------------|---------------------------------------------------------------------------------|
| **Tab** or **

Shift+Tab** | Move between screen elements (e.g., from the toolbar to the packet list or packet detail). |
| **↓**                   | Move to the next packet or detail item.                                          |
| **↑**                   | Move to the previous packet or detail item.                                      |
| **Ctrl+↓** or **F8**    | Move to the next packet, even if the packet list isn't focused.                 |
| **Ctrl+↑** or **F7**    | Move to the previous packet, even if the packet list isn't focused.             |
| **Ctrl+→**              | In the packet detail, open the selected tree item.                             |
| **Ctrl+←**              | In the packet detail, close all the tree items.                                |
| **Ctrl+.**              | Move to the next packet of the conversation (TCP, UDP, or IP).                 |
| **Ctrl+,**              | Move to the previous packet of the conversation.                              |
| **Return or Enter**     | In the packet detail, toggle the selected tree item.                           |
| **Backspace**           | In the packet detail, jump to the parent node.                                |

---

## Protocols - Values

Wireshark supports a variety of protocols that can be filtered using their protocol names. Here is a list of common protocol values:

---

## Protocols - Values

| **Protocol** | **Description** | **When it's Used** | **Key Features** |
|--------------|-----------------|--------------------|------------------|
| **ether**    | **Ethernet** - A widely used Layer 2 protocol for wired networking. | Used in most local area networks (LANs) and data center environments. | - Standard for wired networking in homes and businesses.<br> - Frames encapsulate data for network communication.<br> - Supports IPv4 and IPv6 addressing.<br> - Uses MAC addresses for device identification. |
| **fddi**     | **Fiber Distributed Data Interface** - A high-speed (100 Mbps) network protocol designed for fiber-optic backbone networks. | Used in large enterprise networks for interconnecting routers, switches, and other devices in a backbone network (less common now). | - Operates on fiber-optic cables for high-speed communication.<br> - Uses a token-passing ring topology for fault tolerance.<br> - Primarily used for backbone networks and metropolitan area networks (MANs). |
| **ip**       | **Internet Protocol** - A Layer 3 (Network Layer) protocol responsible for addressing and routing packets across networks. | Used in nearly all IP-based communications over the internet and intranets. | - Core protocol for communication over the internet.<br> - Provides addressing (IP addresses) and routing of packets.<br> - Supports both IPv4 and IPv6.<br> - Divided into two versions: IPv4 (32-bit) and IPv6 (128-bit). |
| **arp**      | **Address Resolution Protocol** - A Layer 2 protocol used to map an IP address to a MAC address. | Used within a local network to map 32-bit IP addresses to 48-bit MAC addresses. | - Resolves IP addresses to MAC addresses in Ethernet networks.<br> - Used by devices when they need to communicate within the same network.<br> - Operates only in local network segments (LANs). |
| **rarp**     | **Reverse Address Resolution Protocol** - A Layer 2 protocol used to map a MAC address to an IP address. | Used in legacy systems, mainly by diskless workstations, to discover their IP address based on their MAC address. | - Reverse of ARP; it was used in legacy systems but is largely obsolete now.<br> - Useful in environments where devices don’t have persistent storage. |
| **decnet**   | **DECnet** - A proprietary protocol suite developed by Digital Equipment Corporation for interconnecting their devices. | Used in older DEC (Digital Equipment Corporation) systems and networks, typically in the 1970s and 1980s. | - Used primarily in DEC computer systems for network communication.<br> - Operated on various physical media, including Ethernet.<br> - Largely obsolete, replaced by TCP/IP in most networks. |
| **lat**      | **LAT (Local Area Transport)** - A protocol developed by Digital Equipment Corporation for remote terminal and application access within a LAN. | Used in older DEC VAX systems and terminals for remote access within a LAN. | - Supports terminal-to-host communication in LAN environments.<br> - Primarily used with DEC’s proprietary hardware and software.<br> - Obsolete, replaced by modern protocols like SSH and RDP. |
| **sca**      | **SCA (Serial Control and Alarm)** - A protocol used for managing serial communications in control systems. | Primarily used in industrial and control systems for serial communication and alarm management. | - Used in industrial systems and control applications for managing serial communication.<br> - Often found in legacy systems. |
| **moprc**    | **MOP (Maintenance Operations Protocol)** - A protocol used for remote diagnostics and maintenance of Digital Equipment Corporation (DEC) systems. | Used in DEC systems for network maintenance and diagnostics. | - Primarily used in DECnet environments.<br> - Allows for remote management and troubleshooting of DEC devices.<br> - Largely obsolete in modern networks. |
| **mopdl**    | **MOPDL (Maintenance Operations Protocol Download)** - A variation of MOP used for downloading operating system files to DEC systems. | Used in legacy DECnet systems for OS downloads to devices. | - Part of DEC’s maintenance protocol suite.<br> - Helps in downloading software or configurations to DEC devices.<br> - Obsolete in modern networks. |
| **tcp**      | **Transmission Control Protocol** - A Layer 4 (Transport Layer) protocol providing reliable, ordered, and error-checked delivery of data between applications. | Used for most internet communication (e.g., web browsing, email, file transfer). | - Ensures reliable communication with error checking and retransmission of lost packets.<br> - Provides ordered delivery of data packets.<br> - Commonly used with IP (together known as TCP/IP). |
| **udp**      | **User Datagram Protocol** - A Layer 4 (Transport Layer) protocol providing low-latency, connectionless communication without guaranteed delivery. | Used in applications where speed is critical and data loss is acceptable (e.g., video streaming, VoIP). | - Faster than TCP due to lack of overhead for error checking and retransmission.<br> - Often used for real-time applications such as streaming and gaming.<br> - Does not guarantee packet delivery or order. |

---

### Summary of Key Points:

- **Ethernet** is the most common Layer 2 protocol for wired networks.
- **FDDI** was historically used for high-speed backbone networks but has mostly been replaced by Ethernet.
- **IP** is the core protocol of the internet and is used to route packets between devices.
- **ARP** is crucial for mapping IP addresses to MAC addresses in a local network.
- **RARP** was once used for diskless workstations to obtain an IP address but is largely obsolete today.
- **DECnet**, **LAT**, **MOP**, and their variants (**MOPRC**, **MOPDL**) were once proprietary protocols used in DEC systems, but they are now outdated and rarely used.
- **TCP** is used for reliable, ordered communications in most applications, while **UDP** is used for fast, low-latency applications where speed is prioritized over reliability.

---

## Common Filtering Commands

| **Usage**                          | **Filter Syntax**                                       | **Description**                                                                                                                                                     |
|------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Wireshark Filter by IP**         | `ip.addr == 10.10.50.1`                                 | Matches packets where the **IP address** (source or destination) is **10.10.50.1**. Useful for filtering traffic to or from a specific IP address.               |
| **Filter by Destination IP**       | `ip.dest == 10.10.50.1`                                 | Filters packets where the **destination IP address** is **10.10.50.1**. Ideal for analyzing traffic sent to a particular host.                                    |
| **Filter by Source IP**           | `ip.src == 10.10.50.1`                                  | Filters packets where the **source IP address** is **10.10.50.1**. Useful for tracking the origin of traffic from a specific device.                             |
| **Filter by IP Range**             | `ip.addr >= 10.10.50.1 and ip.addr <= 10.10.50.100`     | Filters packets where the **IP address** falls within the range **10.10.50.1 to 10.10.50.100**. Useful for subnet or range-based traffic analysis.                  |
| **Filter by Multiple IPs**        | `ip.addr == 10.10.50.1 and ip.addr == 10.10.50.100`      | Filters packets where the **IP address** is **either 10.10.50.1 or 10.10.50.100**. Used to capture traffic from multiple specific IP addresses.                     |
| **Filter out an IP address**      | `! (ip.addr == 10.10.50.1)`                             | Excludes packets where the **IP address** is **10.10.50.1**. Useful when you want to ignore traffic from a particular device.                                      |
| **Filter by Subnet**               | `ip.addr == 10.10.50.1/24`                              | Filters packets where the **IP address** belongs to the **10.10.50.1/24 subnet**. Useful for analyzing traffic within a specific subnet or network segment.        |
| **Filter by Port**                 | `tcp.port == 25`                                        | Filters packets where the **TCP port** is **25**. Useful for analyzing traffic related to a specific service, like SMTP (email).                                   |
| **Filter by Destination Port**    | `tcp.dstport == 23`                                     | Filters packets where the **destination TCP port** is **23** (typically used for Telnet). Ideal for capturing Telnet traffic.                                      |
| **Filter by IP address and Port** | `ip.addr == 10.10.50.1 and tcp.port == 25`              | Filters packets where the **IP address** is **10.10.50.1** and the **TCP port** is **25**. Useful for analyzing specific communication from a particular device on a specific port. |
| **Filter by URL**                  | `http.host == "hostname"`                               | Filters HTTP packets where the **host** in the URL matches **hostname**. Useful for capturing traffic related to a specific website or web server.                 |
| **Filter by Timestamp**            | `frame.time >= "June 02, 2019 18:04:00"`                | Filters packets captured **on or after the specified timestamp** (June 02, 2019 18:04:00). Useful for analyzing packets captured during a specific time window.    |
| **Filter by SYN Flag**             | `tcp.flags.syn == 1 and tcp.flags.ack == 0`             | Filters packets where the **SYN flag** is set and the **ACK flag** is not set. Commonly used for capturing **TCP connection  **SYN flag == 1**: Typically used to capture **initial TCP handshake packets** when a initiation** (SYN packets).
| **Wireshark Beacon Filter**        | `wlan.fc.type_subtype == 0x08`                          | Filters **Wi-Fi beacon frames** (subtype 0x08). Useful for analyzing Wi-Fi networks and their beacon frames that advertise network information.                      |
| **Wireshark Broadcast Filter**     | `eth.dst == ff:ff:ff:ff:ff:ff`                           | Filters **broadcast packets** where the **destination MAC address** is set to **ff:ff:ff:ff:ff:ff**. Useful for capturing broadcast traffic on Ethernet networks.    |
| **Wireshark Multicast Filter**     | `(eth.dst[0] & 1)`                                       | Filters **multicast packets**. This checks if the **destination MAC address** starts with an odd number (which indicates multicast traffic).                        |
| **Host Name Filter**               | `ip.host == "hostname"`                                   | Filters packets where the **host** matches **hostname**. Useful for filtering traffic to or from a specific device identified by its hostname.                      |
| **MAC Address Filter**             | `eth.addr == 00:70:f4:23:18:c4`                         | Filters packets where the **MAC address** is **00:70:f4:23:18:c4**. Useful for tracking traffic to or from a specific device on the local network.                 |
| **RST Flag Filter**                | `tcp.flags.reset == 1`                                  | Filters packets where the **TCP RST (reset)** flag is set. Useful for detecting and analyzing connection resets in TCP communication.                             |


### Summary:

This table provides a collection of common Wireshark display filters that can be used to refine your analysis based on specific criteria, such as IP addresses, ports, protocols, flags, and other packet attributes. Each filter is designed for a different use case, whether you are investigating a particular IP, analyzing traffic on specific ports, filtering out certain types of traffic, or capturing connection handshakes. 

These filters can help you narrow down large capture files, making it easier to focus on relevant packets and identify potential network issues.
---
# Special Operators

| **Operator**   | **Description**                                                                                                                                   | **Example**                                            |
|----------------|---------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------|
| **contains**   | Filters packets by checking if a field contains a specific string (case-sensitive). It searches the entire frame, not limited to a protocol.     | `frame contains "Google"`                              |
| **matches**    | Allows filtering using regular expressions (case-insensitive). It’s useful for more flexible string matching, such as domain names or patterns. | `http.host matches "\.(org|com|net)"`             |
| **in**         | Checks if a field value is within a specified set or range of values. It is useful for filtering multiple values or ranges in a field.           | `tcp.port in {80 443}` or `tcp.port in [80-443]`       |

## Examples

| **Operator**   | **Example Usage**                                                                                                                                           |
|----------------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **contains**   | To filter frames containing the string "Google" anywhere in the packet:                                                                                   |
|                | `frame contains "Google"`                                                                                                                                  |
| **matches**    | To filter HTTP host headers that end with `.org`, `.com`, or `.net` (case-insensitive):                                                                   |
|                | `http.host matches "\.(org|com|net)"`                                                                                                                |
| **in**         | To filter packets with TCP ports 80 or 443, or any port between 80 and 443:                                                                                |
|                | `tcp.port in {80 443}`                                                                                                                                     |
|                | `tcp.port in [80-443]`                                                                                                                                     |

## Notes
| **Operator**   | **Details**                                                                                                      |
|----------------|------------------------------------------------------------------------------------------------------------------|
| **contains**   | Case-sensitive and matches exact strings.                                                                         |
| **matches**    | Case-insensitive and supports regular expressions (Perl-compatible).                                             |
| **in**         | Checks if a field’s value is in a specified list or a defined range.                                              |

## Summary of Operators

| **Operator**   | **Purpose**                                                     |
|----------------|---------------------------------------------------------------|
| **contains**   | Exact string match, case-sensitive.                            |
| **matches**    | Regular expression match, case-insensitive.                   |
| **in**         | Matches if a value is in a specified list or range.            |

---

## Conclusion

Wireshark is an incredibly powerful tool for network traffic analysis. Understanding how to use capture and display filters, logical operators, and protocols can significantly enhance your ability to troubleshoot and analyze network traffic effectively. This guide should help you navigate through the most commonly used commands and concepts in Wireshark.

For more detailed information, refer to the official Wireshark documentation: [Wireshark Documentation](https://www.wireshark.org/docs/).

Reference: 
https://www.stationx.net/wireshark-cheat-sheet/
https://scadahacker.com/library/Documents/Cheat_Sheets/Networking%20-%20Wireshark%20-%20Display%20Filters%201.pdf
