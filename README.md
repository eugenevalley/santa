# santa
Integrate Santa with Intune

1. Download the Santa *.pkg here and deploy it using Intune: https://github.com/northpolesec/santa/releases/tag/2025.3
2. Download and modify the com.northpolesec.santa.example.mobileconfig file in this repo and customize it to contain any applications you want to block. The modified.com.northpolesec.santa.example.mobileconfig in this repo contains the xml required to block Firefox using the Team ID for Mozilla.  
3. Download the other remaining mobileconfig files in this repo:
    a. notificationsettings.santa.example.mobileconfig - Enables Santa notifications
    b. system-extension-policy.santa.example.mobileconfig - Alows the extension to run without user interaction
    c. tcc.configuration-profile-policy.santa.example.mobileconfig - Provides full disk access
4. Deploy all four mobileconfig files using the Custom macOS Configuration Profile in Intune


Here is an example of the xml required to block Firefox:
 <dict>
	<!-- Always BLOCK Firefox based on TEAMID-->
	<key>identifier</key>
	<string>43AQ936H96</string>
	<key>policy</key>
	<string>BLOCKLIST</string>
	<key>rule_type</key>
	<string>TEAMID</string>
</dict>

Note:
The modified.com.northpolesec.santa.example.mobileconfig in this repo includes this modification. 
