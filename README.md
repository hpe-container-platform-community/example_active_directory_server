### Active Directory

You will need this when configuring the HPE Ezmeral Container Platform UI.

```
System Settings -> User Authentication
   -> Authentication Type: Active Directory
   -> Security Protocol: LDAPS
   -> Service Location: ${ad_server_ip} | Port: 636
   -> Bind Type: Search Bind
   -> User Attribute: sAMAccountName
   -> Base DN: CN=Users,DC=samdom,DC=example,DC=com
   -> Bind DN: cn=Administrator,CN=Users,DC=samdom,DC=example,DC=com
   -> Bind Password: 5ambaPwd@
```

Two AD groups and two AD users were created automatically when the enviroment was provisioned:

- `DemoTenantAdmins` group
- `DemoTenantUsers` group
- `ad_user1` and `ad_user2` in the `DemoTenantUsers` group with password `pass123`
- `ad_admin1` and `ad_admin2` in the `DemoTenantAdmins` group with password `pass123`


#### Tenant Setup

Recommended reading: http://docs.bluedata.com/40_authentication-groups

E.g. Demo Tenant 

```
Tenant Settings
  -> External User Groups: CN=DemoTenantAdmins,CN=Users,DC=samdom,DC=example,DC=com | Admin
  -> External User Groups: CN=DemoTenantUsers,CN=Users,DC=samdom,DC=example,DC=com | Member
```

- Login to BlueData as `ad_admin1/pass123` - you should be taken to the Demo Tenant and have 'Admin' privileges
- Create a new user (see below)
- Login to BlueData as `ad_user1/pass123` - you should be taken to the Demo Tenant and have 'Member' privileges

### Directory Browser

Sometimes it's useful to browse the AD tree with a graphical interface.  This section describes how to connect with the open source Apache Directory Studio.

- Download and install Apache Director Studio
- In Apache Directory Studio, create a new connection:
  - *Connection name:* choose something meaningful
  - *Hostname:* ${docker_host}
  - *Port:* 636
  - *Connection timeout(s):* 30
  - *Encryption method:* No encryption
  - *Provider:* Apache Directory LDAP Client API
  - **Click *Next***
  - *Authentication Method:* Simple Authentication
  - *Bind DN or user:* cn=Administrator,CN=Users,DC=samdom,DC=example,DC=com
  - *Bind password:* 5ambaPwd@
  - **Click *Finish***
