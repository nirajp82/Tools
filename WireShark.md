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

---

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

| **Protocol** |
|--------------|
| **ether**    |
| **fddi**     |
| **ip**       |
| **arp**      |
| **rarp**     |
| **decnet**   |
| **lat**      |
| **sca**      |
| **moprc**    |
| **mopdl**    |
| **tcp**      |
| **udp**      |

These protocols represent different types of traffic that can be filtered during packet capture or analysis.

---

## Common Filtering Commands

These are some common commands used to filter packets in Wireshark:

| **Usage**                          | **Filter Syntax**                                       |
|------------------------------------|---------------------------------------------------------|
| **Wireshark Filter by IP**         | `ip.addr == 10.10.50.1`                                 |
| **Filter by Destination IP**       | `ip.dest == 10.10.50.1`                                 |
| **Filter by Source IP**           | `ip.src == 10.10.50.1`                                  |
| **Filter by IP Range**             | `ip.addr >= 10.10.50.1 and ip.addr <= 10.10.50.100`      |
| **Filter by Multiple IPs**        | `ip.addr == 10.10.50.1 and ip.addr == 10.10.50.100`      |
| **Filter out an IP address**      | `! (ip.addr == 10.10.50.1)`                             |
| **Filter by Subnet**               | `ip.addr == 10.10.50.1/24`                              |
| **Filter by Port**                 | `tcp.port == 25`                                        |
| **Filter by Destination Port**    | `tcp.dstport == 23`                                     |
| **Filter by IP address and Port** | `ip.addr == 10.10.50.1 and tcp.port == 25`              |
| **Filter by URL**                  | `http.host == "hostname"`                               |
| **Filter by Timestamp**            | `frame.time >= "June 02, 2019 18:04:00"`                |
| **Filter by SYN Flag**             | `tcp.flags.syn == 1 and tcp.flags.ack == 0`             |
| **Wireshark Beacon Filter**        | `wlan.fc.type_subtype == 0x08`                          |
| **Wireshark Broadcast Filter**     | `eth.dst == ff:ff:ff:ff:ff:ff`                           |
| **Wireshark Multicast Filter**     | `(eth.dst[0] & 1)`                                       |
| **Host Name Filter**               | `ip.host == hostname`                                   |
| **MAC Address Filter**             | `eth.addr == 00:70:f4:23:18:c4`                         |
| **RST Flag Filter**                | `tcp.flags.reset == 1`                                  |

---

## Conclusion

Wireshark is an incredibly powerful tool for network traffic analysis. Understanding how to use capture and display filters, logical operators, and protocols can significantly enhance your ability to troubleshoot and analyze network traffic effectively. This guide should help you navigate through the most commonly used commands and concepts in Wireshark.

For more detailed information, refer to the official Wireshark documentation: [Wireshark Documentation](https://www.wireshark.org/docs/).

Reference: 
https://www.stationx.net/wireshark-cheat-sheet/
https://scadahacker.com/library/Documents/Cheat_Sheets/Networking%20-%20Wireshark%20-%20Display%20Filters%201.pdf
