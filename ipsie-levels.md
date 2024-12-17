# IPSIE Levels

|                              | Log In                                            | MFA & Log Out                                                         | Provisioning                                 | Continuous Access                                                 | Entitlements                                          |
|------------------------------|---------------------------------------------------|-----------------------------------------------------------------------|----------------------------------------------|-------------------------------------------------------------------|-------------------------------------------------------|
| Requirement                  | IPSIE 1                                           | IPSIE 2                                                               | IPSIE 3                                      | IPSIE 4                                                           | IPSIE 5                                               |
| Single Sign-On               | Required (FAL2)                                   | Required (FAL3)                                                       | Same as 2                                    | Same as 3                                                         | Same as 4                                             |
| MFA                          | IdP-enforced (app doesn't need to do anything)    | IdP communicates MFA level to app. App can request MFA level from IdP | Same as 2                                    | Same as 3                                                         | Same as 4                                             |
| Revocation                   | RP matches session lifetime to assertion lifetime | IdP can terminate sessions for individual users in the app            | Same as 2                                    | Same as 3                                                         | Same as 4                                             |
| Provisioning                 | JIT provisioning from SSO                         | Same as 1                                                             | Users can be provisioned before they sign in | Same as 3                                                         | Same as 4                                             |
| Deprovisioning               | None                                              | None                                                                  | Users can be deprovisioned by the IdP        | Same as 3                                                         | Same as 4                                             |
| Continuous Access\n(RP->IdP) | None                                              | None                                                                  | None                                         | App communicates session changes to IdP such as IP address change | Same as 4                                             |
| Continuous Access\n(IdP->RP) | None                                              | None                                                                  | None                                         | IdP communicates changes in account and device posture to app     | Same as 4                                             |
| Entitlements                 | None                                              | None                                                                  | None                                         | None                                                              | Group provisioning and deprovisioning from IdP to app |



## Level 1 - Single Sign-On

Level 1 enables basic single sign-on from applications to the identity provider, communicating identity statements about the user. Single sign-on in Level 1 meets the requirements of [FAL2](https://pages.nist.gov/800-63-4/sp800-63c/fal/).

The RP respects the session lifetime as communicated by the IdP in the assertion, and reauthenticates the user through the IdP after the expiration.


## Level 2 - MFA and Log Out

Single sign-on in Level 3 meets the requirements of [FAL3](https://pages.nist.gov/800-63-4/sp800-63c/fal/).

Level 2 adds the ability to communicate information about the user's authentication method between IdP and RP. The IdP includes claims about the authentication level in the assertion to the RP. The RP can request a specific authentication level of the IdP.

Level 2 also adds the ability for the IdP to terminate sessions of individual users in the app.


## Level 3 - Provisioning

Level 3 adds the ability to provision and deprovision users in the application before they have logged in. Prior to level 3, users were only JIT-provisioned in the application as part of SSO.



