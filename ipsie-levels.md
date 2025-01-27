# IPSIE 

The capabilities documented in the levels below are specified as functionality for the relying party / applications to implement. In practice, enterprises that purchase SaaS applications should use these levels in RFPs to define the capabilities required of their applications.  The enterprise's identity systems (IdP, directory, etc.) may or may not support all of the functionality supported by a particular relying party / application.

## Session Lifecycle Management

|                              | Log In                                            | MFA & Log Out                                                         | Continuous Access                                                 |
|------------------------------|---------------------------------------------------|-----------------------------------------------------------------------|-------------------------------------------------------------------|
| Requirement                  | IPSIE A1                                          | IPSIE A2                                                              | IPSIE A3                                                          |
| Single Sign-On               | Required (FAL2)                                   | Same as A2                                                            | Same as A2                                                        |
| MFA                          | IdP-enforced (app doesn't need to do anything). IdP communicates MFA level to app.     | IdP MUST accept MFA level requests from the app | Same as A2                                                        |
| Revocation                   | RP MUST match session lifetime to assertion lifetime | App MUST accept session termination requests from IdP for individual users            | Same as A2                                                        |
| Continuous Access (RP->IdP)  | None                                              | None                                                                  | App communicates session changes to IdP such as IP address change |
| Continuous Access (IdP->RP)  | None                                              | None                                                                  | IdP communicates changes in account and device posture to app     |

### IPSIE Authentication Level A1 - Single Sign-On

Level A1 enables basic single sign-on from applications to the identity provider, communicating identity statements about the user. Single sign-on in Level A1 meets the requirements of [FAL2](https://pages.nist.gov/800-63-4/sp800-63c/fal/).

The RP respects the session lifetime as communicated by the IdP in the assertion, and reauthenticates the user through the IdP after the expiration.


### IPSIE Authentication Level A2 - MFA and Log Out

Level A2 adds the ability to communicate information about the user's authentication method between IdP and RP. The IdP includes claims about the authentication level in the assertion to the RP. The RP can request a specific authentication level of the IdP.

Level A2 also adds the ability for the IdP to terminate sessions of individual users in the app.


### IPSIE Authentication Level A3 - Continuous Access

Level A3 adds continuous access to the authentication between IdP and application.

The app communicates session changes to the IdP such as IP address change, enabling the IdP to be aware of more context around what is happening to users' sessions after the initial sign-in.

The IdP communicates changes in the account and device posture to the application, enabling the application to take actions it determines are necessary based on its own policies about these changes.



## Identity Lifecycle Management

|                              | JIT User Provisioning Control               | User Pre-Provisioning and Deprovisioning Control| 
|------------------------------|---------------------------------------------|-------------------------------------------------|
| Requirement                  | IPSIE P1                                    | IPSIE P2                                        |
| Provisioning Control         | User provisioning MUST be controlled by the enterprise via the IdP. <br> Out of band provisioning / self provisioning by users SHALL NOT be allowed. | Same as P1 | 
| Provisioning                 | JIT-based provisioning MUST be enabled.     | App MUST allow users to be provisioned by the IdP prior to sign in. <br> JIT-based provisioning MAY be enabled. |
| Deprovisioning               | None                                        | App MUST allow users to be deprovisioned by the IdP.|


### IPSIE Provisioning Level P1 - JIT User Provisioning Control

IPSIE Provisioning Level P1 requires the IdP to provision users in the application when they log in via SSO. Users must not exist in the application prior to the user logging in for the first time, eliminating alternative pathways for user provisioning (e.g. self-provisioning).

### IPSIE Provisioning Level P2 - User Pre-Provisioning and Deprovisioning Control 

Level P2 adds the ability to provision and deprovision users in the application before they have logged in. Prior to level P2, users were only JIT-provisioned in the application as part of SSO. An application at P2 MUST support pre-provisioning and deprovisioning of users.  IdPs and Apps at P2 MAY support JIT provisioning for downward compatability with an IdP / RP operating at Level P1.

## Entitlements Management

|                              | No Entitlements Management Control | Group and Group Membership Pre-Provisioning and Deprovisioning Control| Group and Group Membership Anti-Entropy Control|
|------------------------------|------------------------------------|-----------------------------------------------------------------------|---------------------------------------------------|
| Requirement                  | IPSIE E1                           | IPSIE E2                                                              | IPSIE E3                                       |
| Entitlements                 | Entitlements are managed independently by the IdP and application | IdP and App MUST enable asynchronous pre-provisioning / deprovisioning of groups and group memberships.| Groups and group memberships MUST be controlled by the enterprise via the IdP as a single source of truth.<br> <br> Group and group membership provisioning via the App SHALL NOT be allowed. <br> IdP and application MUST implement anti-entropy controls for groups and group membership. |

### IPSIE Entitlements Management Level E1 - No Entitlements Management Control

IPSIE Level E1 allows the IdP and application to independently manage entitlements for users.

### IPSIE Entitlements Management Level E2 - Group and Group Membership Pre-Provisioning and Deprovisioning Control

Level E2 adds the capability of communicating groups and group memberships from the IdP to the application.  Groups and group memberships MUST be pre-provisioned and SHALL NOT be JIT provisioned.  Entitlements MAY be managed at the app, however, this is discouraged.  

### IPSIE Entitlements Management Level E3 - Group and Group Membership Anti-Entropy Control 

At Level E3, the IdP is a single source of truth regarding the state of the groups and group membership.  Building upon E2, the control of provisioning / deprovisionions groups and group membership is the sole responsibility of the IdP and SHALL NOT be enabled within the application. Anti-entropy control must be established to prevent drift. 

This SHALL NOT preclude the application from dynamically assessing privileges in real time as a component of session management.



