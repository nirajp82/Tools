### 1. **WINDBG:**
   - **Description:** WINDBG is a powerful debugger for Windows. It is commonly used for debugging native Windows applications and can also be used for debugging .NET applications.
   - **Example Usage:**
     - Install WINDBG from [WinDbg Downloads](https://docs.microsoft.com/en-us/windows-hardware/drivers/debugger/debugger-download-tools).
     - Open a crash dump file:
       ```bash
       windbg -z C:\Path\To\Your\CrashDump.dmp
       ```
     - Analyze the crash dump using WINDBG commands. For example, use `!analyze -v` to get an automated analysis.

### 2. **SOSEX:**
   - **Description:** SOSEX is an extension for WINDBG that provides additional commands specifically designed for debugging managed .NET code.
   - **Example Usage:**
     - Download SOSEX from [SOSEX Extension](https://github.com/Microsoft/SOSEX).
     - Load SOSEX in WINDBG:
       ```bash
       .load path\to\sosex.dll
       ```
     - Use SOSEX commands. For example, `!mk` for viewing managed stack frames.

### 3. **Debugging .NET Crash Dumps with WINDBG:**
   - **Description:** The provided link explains how to use WINDBG to analyze .NET crash dumps. It covers basic commands and debugging techniques.
   - **Example Usage:**
     - Follow the tutorial [Using WINDBG to Analyze .NET Crash Dumps](https://stackify.com/using-windbg-to-analyze-net-crash-dumps-async-crash/).
     - Learn how to load symbols, analyze call stacks, and identify issues in a .NET crash dump.

### 4. **Troubleshooting w3wp.exe Crash with WINDBG:**
   - **Tutorial:** This link provides guidance on troubleshooting crashes of the w3wp.exe process, which is the IIS worker process for hosting .NET applications.
   - **Link:** [Troubleshoot w3wp.exe Crash](https://stackify.com/troubleshoot-w3wp-crash/)

### 5. **Melbourne ALT.NET - Debugging with WINDBG:**
   - **Video:** The YouTube link leads to a video tutorial on debugging with WINDBG by Melbourne ALT.NET.
   - **Link:** [Debugging with WINDBG - Melbourne ALT.NET](https://www.youtube.com/watch?v=BfwZ8RBNH0M&ab_channel=MelbourneALTNET)

### 6. **FullSocrates - IIS Stories:**
   - **Blog:** The link takes you to a blog category that shares stories and experiences related to IIS (Internet Information Services).
   - **Link:** [FullSocrates - IIS Stories](https://fullsocrates.wordpress.com/category/iis-stories/)

### 7. **PSTools:**
   - **Description:** PSTools is a suite of command-line utilities that facilitate various system administration tasks, including remote process management.
   - **Example Usage:**
     - Download PSTools from [PSTools](https://learn.microsoft.com/en-us/sysinternals/downloads/pstools).
     - Use PsExec to run a command on a remote machine:
       ```bash
       psexec \\RemoteMachine -u UserName -p Password Command
       ```
     - For example, open a remote command prompt:
       ```bash
       psexec \\RemoteMachine cmd
       ```

### 8. **TCPView:**
   - **Description:** TCPView is a sysinternals tool that provides a real-time display of active TCP and UDP connections on your system.
   - **Example Usage:**
     - Download TCPView from [TCPView](https://learn.microsoft.com/en-us/sysinternals/downloads/tcpview).
     - Run TCPView to see active TCP and UDP connections on your system.

### 9. **Procdump:**
   - **Description:** Procdump is a sysinternals tool that can create crash dumps of processes based on various criteria, such as CPU usage or specific exceptions.
   - **Example Usage:**
     - Download Procdump from [Procdump](https://learn.microsoft.com/en-us/sysinternals/downloads/procdump).
     - Create a crash dump when a process crashes:
       ```bash
       procdump -e -ma YourProcess.exe
       ```
     - Monitor CPU usage and create a dump when it exceeds 90%:
       ```bash
       procdump -c 90 -ma YourProcess.exe
       ```

### 10. **DebugDiag Tool:**
   - **Description:** DebugDiag is a tool designed to assist in troubleshooting issues such as crashes, hangs, and memory leaks in Windows applications.
   - **Link:** [DebugDiag Tool](https://www.microsoft.com/en-us/download/details.aspx?id=58210)

### 11. **dotnet-gcdump Global Tool:**
   - **Description:** The dotnet-gcdump global tool collects Garbage Collector (GC) dumps of live .NET processes using EventPipe.
   - **Link:** [dotnet-gcdump Global Tool](https://learn.microsoft.com/en-us/dotnet/core/diagnostics/dotnet-gcdump)

### 12. **RedisInsight:**
   - **Description:** RedisInsight is a graphical user interface for managing and monitoring Redis instances.
   - **Link:** [RedisInsight](https://redislabs.com/redisinsight/)

### 13. **Sysinternals Suite:**
   - **Description:** Sysinternals Suite is a collection of advanced system utilities designed to help you monitor, troubleshoot, and diagnose Windows systems and applications.
   - **Link:** [Sysinternals Suite](https://learn.microsoft.com/en-us/sysinternals/downloads/)

### 14. **PsPing:**
   - **Description:** PsPing is a sysinternals tool that implements ping functionality along with TCP ping, latency, and bandwidth measurement.
   - **Link:** [PsPing](https://learn.microsoft.com/en-us/sysinternals/downloads/psping)

### 15. **Windirstat:**
   - **Description:** WinDirStat is a handy tool for managing disk space efficiently, especially when you need to identify and eliminate large or unnecessary files that may be taking up valuable storage space on your Windows computer.
   - **Link:** [Windirstat](https://windirstat.net/download.html)

### 15. **Additional Resources:**
   - **WinDbg Commands Reference:** [Common WinDbg Commands](http://windbg.info/doc/1-common-cmds.html)
   - **Windows Debugger Documentation:** [Windows Debugger Documentation](https://developer.microsoft.com/en-us/windows/downloads/windows-sdk/)

### 16. **How to Create, Use, and Debug .NET Application Crash Dumps:**
   - **Tutorial:** The link provides a guide on creating, using, and debugging .NET application crash dumps in 2019.
   - **Link:** [How to Create, Use, and Debug .NET Application Crash Dumps](https://michaelscodingspot.com/how-to-create-use-and-debug-net-application-crash-dumps-in-2019/)

### 17. **AsmSpy**
   - AsmSpy is a command-line tool used in .NET development to analyze dependencies and references between assemblies within a .NET application. It helps developers understand the structure of their applications, identify unused dependencies, and manage assembly compatibility and versioning. AsmSpy generates detailed reports outlining assembly names, versions, and referenced types and members, aiding in optimizing application performance and reducing deployment package size. With its command-line interface, AsmSpy integrates easily into automated build processes and development workflows, making it a valuable tool for .NET developers.

### 18. **DotPeek**
   - DotPeek is a free .NET decompiler and assembly browser developed by JetBrains. It allows developers to decompile .NET assemblies into readable C# or VB.NET code, explore assembly contents, navigate and search through code, customize decompiler options, integrate with Visual Studio, export decompiled code, and analyze code for potential issues. DotPeek supports multiple .NET Framework versions and is a valuable tool for developers to explore and understand .NET applications and libraries.

### 19: **dotnet dev-certs https --trust**
```sh
dotnet dev-certs https --trust
```
 - This command generates a development certificate and installs it into the trusted certificate store on your system.
 - To establish trust for HTTPS connections in .NET Core applications during development, you can use the dotnet dev-certs command-line tool. This tool helps generate and manage development certificates. Here's how you can use it to trust the HTTPS certificate.
 - Trust the Certificate: The --trust option automatically trusts the generated certificate. This means that when you run your .NET Core application with HTTPS enabled, the application will use this certificate, and your browser or HTTP client will trust it.

### 20: https://jsonplaceholder.typicode.com/
Free fake and reliable API for testing and prototyping.

### 21: https://www.ssllabs.com/ssltest/analyze.htm
  - SSL Labs provides a detailed assessment of a website's SSL/TLS setup, including information about certificate validity, supported protocols, cipher suites, and security vulnerabilities.

### 22: TraceRoute:
   - [Traceroute](https://tools.keycdn.com/traceroute) -
   - Traceroute, also called tracert, is a utility that uses ICMP packets to record the route through the internet from one computer to another. It calculates the time taken for each hop as the packet is routed to the destination. To guarantee accuracy, each hop is queried multiple times (in this case four times) to better measure the response of that particular hop.
   -  https://tools.keycdn.com/traceroute: This tool is typically used to diagnose hiccups or interruptions in the transfer of data and pinpoint where along the chain it occurred. This IPv4 or IPv6 traceroute is unique in that it allows you to simultaneously test different locations at once. This lets you quickly determine if there is any packet loss or unexpected latency to the given IP or hostname. A CDN can help dramatically reduce latency by minimizing the distance between hops.

### 23: TNC: Displays diagnostic information for a connection. The command is essentially checking if your machine can establish a connection to the specified host using port. 
   ```ps1
      tnc ocsp.globalsign.com -Port 80
   ```
### 23 `certutil -urlcache` - It is used to **view or clear** the **certificate URL cache**. 
   - **View cache**: Shows the list of URLs of certificates and CRLs stored in the cache.
     ```bash
        certutil -urlcache
     ```
   - **Clear cache**: Removes all cached URLs, forcing the system to fetch fresh data.
     ```bash
        certutil -urlcache * delete
     ```

 

https://github.com/nirajp82/References

These examples provide a starting point for using these tools. Depending on your specific scenario, you may need to adjust commands and options. Always refer to the official documentation for each tool for comprehensive guidance.
