# Scripting Agent Sending Emails to new Users in an Organization

If you want to send emails to new users created in your Exchange On-premises organization, a simple tool to use is the in-built Scripting Agent.

## Setup
You need:
* Exchange Server 2010 to 2016
* A valid user mailbox
* Access to Exchange Management Shell

## Tested in
Exchange Server 2016 CU14

## Installation

1. Edit the html and the scripting agent to your needs, as it currently stands, it sends an email to a newly created mailbox automatically when the New-Mailbox cmdlet is triggered
2. Once finished, place the ScriptingAgentConfig.xml on the <drive>:\Program Files\Bin\CmdletExtensionAgents.

Note: I recommend to add this xml file somewhere else and edit it there, once finised just copy it to this directory

3. Create an _images_ folder inside this same directory, and add the html file and images
4. Now we need to enable the scripting agent as:

`Enable-CmdletExtensionAgent "Scripting Agent"`

5. The Agent is enabled, now for testing, create a test user using:

`New-Mailbox -Alias user -Name "user" -FirstName user -DisplayName "user" -UserPrincipalName user@contoso.com -Password (ConvertTo-SecureString -String 'Pa$$w0rd1' -AsPlainText -Force) -Database DC02`

6. Once completed, create a profile for this new user or open it in OWA
7. The first item there should be a welcome email!

## How to disable

Just run:
`Disable-CmdletExtensionAgent "Scripting Agent"`

## Some considerations

You need to enable this on all valid servers where the Cmdlet for New-Mailbox might run. If you use Exchange Admin Center, be aware where is the
ECP conneting to.



