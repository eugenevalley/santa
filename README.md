# Integrate Santa with Intune

Santa is a binary and file access authorization system for macOS. It consists of a system extension that allows or denies attempted executions using a set of rules stored in a local database, a GUI agent that notifies the user in case of a block decision, a sync daemon responsible for syncing the database, and a server, and a command-line utility for managing the system.

It is named Santa because it keeps track of binaries that are naughty or nice.

The project and the latest release is available on GitHub.

Currently, Intune does not have functionality to block applications from running like it does on Windows endpoints.
To work around this, we can implement Santa with custom mobileconfig profiles.
When using custom mobileconfig profiles, there is no need to bring up a Santa sync server as the rules are applied directly via Intune.

```xml
1. Download the Santa *.pkg here and deploy it using Intune: https://github.com/northpolesec/santa/releases/tag/2025.3
2. Download and modify the com.northpolesec.santa.example.mobileconfig file in this repo and customize it to contain any applications you want to block. The modified.com.northpolesec.santa.example.mobileconfig in this repo contains the xml required to block Firefox using the Team ID for Mozilla.  
3. Download the other remaining mobileconfig files in this repo:
    a. notificationsettings.santa.example.mobileconfig - Enables Santa notifications
    b. system-extension-policy.santa.example.mobileconfig - Alows the extension to run without user interaction
    c. tcc.configuration-profile-policy.santa.example.mobileconfig - Provides full disk access
4. Deploy all four mobileconfig files using the Custom macOS Configuration Profile in Intune
```

Here is an example of the xml required to block Firefox:

```xml
 <dict>
	<!-- Always BLOCK Firefox based on TEAMID-->
	<key>identifier</key>
	<string>43AQ936H96</string>
	<key>policy</key>
	<string>BLOCKLIST</string>
	<key>rule_type</key>
	<string>TEAMID</string>
 </dict>
```

Note:
The modified.com.northpolesec.santa.example.mobileconfig in this repo includes this modification. 
