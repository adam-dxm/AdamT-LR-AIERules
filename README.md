# AdamT-LR-AIERules
Some AIE Rules for LogRhythm  
  
This repo contains the following:  
  
Rule ID: 1000000016  
Rule Name: New AD Dom Ctrlr Detected  
Descr: Uses object auditing on your Windows DNS zone to detect when a new Domain Controller is introduced to the environment. When you see this trigger, you should be looking to onboard the new Domain Controller ASAP, as without the security logs, you are losing visibility of AD changes. Remember: ANY (writeable) DC can process ANY change. An attacker may target a remote DC, rather than a nearby one, in order to evade scrutiny - especially if it's an 'unloved' part of the environment (eg a legacy site, or a mostly unmonitored DR environment).  You will need to apply custom SACLs to your root DNS zone, have object access auditing turned on your DCs, and have their security logs onboarded in LogRhythm for this to work.  
  
Rule ID: 1000000017  
Rule Name: New AD Dom Ctrlr Detected via DNS Audit  
Descr: Works as above, but using the Microsoft-Windows-DNS-Server/Audit log source instead of the Windows Security log (see my LR-DNSServerAudit-MPE repo for rules to parse that log source type).  
  
  
Rule ID: 1000000018  
Rule Name: Temp VolSnapshot  
Descr: Looks for the use of vssadmin to create and delete disk snapshots within an hour. This method is often employed to gain access to otherwise unreadable files, such as obtaining a copy of the NTDS.DIT file on a Domain Controller, for offline cracking.  
  
Rule ID: 1000000019  
Rule Name: GPO Modified  
Descr: Uses object access auditing and Domain Controller security logs, in order to detect modifications to Group Policy. NB: The object returned will be the GUID of the policy, not its name. The GUID will match a folder under sysvol\\<domain.fqdn>\Policies. Alternatively, an SRP is available from the LR Community to resolve these GUIDs for you.
