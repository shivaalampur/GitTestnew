# Azure dev environment details

This document describes Azure dev environment details for the project and getting an access to the environment.

    Tenant ID: a11959d0-ca0a-422e-80d3-b05cf9cafb22

    Primary domain: MngEnvMCAP786396.onmicrosoft.com

    License: Microsoft Entra ID P2

## Getting access to the environment

    1.  Login to [Azure Entra](https://ms.portal.azure.com/#view/Microsoft_AAD_UsersAndTenants/UserManagementMenuBlade/~/AllUsers) with your MngEnvMCAP786396.onmicrosoft.com account.

    2.  Create a new account. Make sure the user principal and display name are the same as Microsoft account to maintain similarity. 
        In the assignments tab add group and select "TardigradeTeam". Access to the environment is provisioned through this SG to avoid manual work

    3.  Share password to the user in any secure manner. Preferably KeyVault.

## Accessing environment for the first time

    1.  From your corp laptop search for "Azure VPN Client" and open it.

    2.  Connect "MSFT-AzVPN-Manual" from the list

    3.  Now in the Edge browser connect [Azure portal](https://portal.azure.com) and login with MngEnvMCAP786396.onmicrosoft.com user and password

    4.  First time login will take you Microsoft Authenticator app download (if you already have app installed on mobile, click next)

    5.  In the setup your account clicks next and scan QC code in Authenticator app. This will add your account to the app

    6.  In the next screen displays pin to enter in the app for two factor auth and proceed to next screen

    7.  Update your password in the next screen. Once done you are all set.
