I recently reviewed [NIST SP800-63C rev4 (draft)](https://pages.nist.gov/800-63-4/sp800-63c.html).  Below, I've copied what I believe to be the full set of _security_ requirements_ for an IPSIE SL1 profile to meet FAL2 in the draft guidance.  I have not yet assessed OIDC SL1 against these requirements.  My intent is to document conformance/non-conformance in the r

See the questions at the bottom of the issue regarding non-security requirements such as trust agreements, and privacy.   

- [Table 1](https://pages.nist.gov/800-63-4/sp800-63c.html#table-1) provides an overview of the requirements, I've bolded the FAL2 requirements:

| **Requirement**	| **FAL1** | **FAL2** | **FAL3**| 
|--------------|------|------|------|
|Audience Restriction | Multiple RPs allowed per assertion, Single RP per assertion recommended	| **Single RP per assertion** | Single RP per assertion |
| Injection Protection | Recommended for all transactions | **Required; transaction begins at the RP** | Required; transaction begins at the RP |
| Trust Agreement Establishment	| Subscriber-driven or A priori | **A priori** | A priori |
| Identifier and Key Establishment | 	Dynamic or Static | 	**Dynamic or Static** |	Static |
|Presentation | Bearer Assertion | **Bearer Assertion** | Holder-of-Key Assertion or Bound Authenticator|

1. At all FALs, the RP needs to trust the IdP to provide valid assertions representing the subscriber’s authentication event and SHALL validate the assertion.
2. IdPs and RPs SHALL employ appropriately tailored security controls from the moderate baseline security controls defined in [[SP800-53]](https://pages.nist.gov/800-63-4/sp800-63c.html#ref-SP800-53) or an equivalent federal (e.g., [[FEDRAMP]](https://pages.nist.gov/800-63-4/sp800-63c.html#ref-FEDRAMP)) or industry standard that the organization has determined for the information systems, applications, and online services that these guidelines are used to protect.
3. IdPs and RPs SHALL ensure that the minimum assurance-related controls for the appropriate systems, or equivalent, are satisfied. Additional security controls are discussed in [Sec. 3.10](https://pages.nist.gov/800-63-4/sp800-63c.html#security-controls).
4. FAL2 provides a high level of protection for federation transactions, providing protections against a variety of attacks against federated systems. All the requirements for FAL1 apply at FAL2 except where overridden by more specific or stringent requirements here.
  a. At FAL1, the IdP SHALL sign the assertion using approved cryptography. 
  b. The RP SHALL validate the signature using the key associated with the expected IdP.
  c.  The RP SHALL validate that it is one of the targeted RPs for the given assertion.
  d.  At FAL1, the trust agreement MAY be established by the subscriber during the federation transaction. Note that at FAL1, it is still possible for the trust agreement to be established a priori by the RP and IdP.
5. At FAL2, the assertion SHALL be strongly protected from injection attacks, as discussed in [Sec. 3.10.1](https://pages.nist.gov/800-63-4/sp800-63c.html#injection-protection). The federation transaction SHALL be initiated by the RP.
6.  At FAL2, the assertion SHALL audience restricted to a single RP.
7.  At FAL2, an a priori trust agreement SHALL be established prior to the federation transaction taking place.
8. IdPs SHALL support a mechanism for RPs to specify a set of minimum acceptable xALs as part of the trust agreement and SHOULD support the RP specifying a more strict minimum set at runtime as part of the federation transaction. 
9. When an RP requests a particular xAL, the IdP SHOULD fulfill that request, if possible, and SHALL indicate the resulting xAL in the assertion. 
10. The IdP SHALL inform the RP of the following information for each federation transaction:
  a. The IAL of the subscriber account being presented to the RP, or an indication that no IAL claim is being made
  b. The AAL of the currently active session of the subscriber at the IdP, or an indication that no AAL claim is being made
  c. The FAL of the federation transaction
11. If the xAL is unchanging for all messages between the IdP and RP, the xAL information SHALL be included in the terms of the trust agreement between the IdP and RP.
12. The IdP MAY indicate that no claim is made to the IAL or AAL for a given federation transaction. In such cases, no default value is assigned to the resulting xAL by the RP. 
13. The RP SHALL determine the minimum IAL, AAL, and FAL it is willing to accept for access to any offered functionality. 
14. An RP MAY vary its functionality based on the IAL, AAL, and FAL of a specific federated authentication. 
15. The RP SHALL ensure that it meets its obligations in the federation transaction for the FAL declared in the assertion. 
16. The subscriber SHALL be identified in the federation transaction using a federated identifier unique to that subscriber. A federated identifier is the logical combination of a subject identifier, representing a subscriber account, and an issuer identifier, representing the IdP. The subject identifier is assigned by the IdP, and the issuer identifier is assigned to the IdP usually through configuration.
17. Federated identifiers SHALL contain no plaintext personally-identifiable information (PII), such as usernames, email addresses, or employee numbers, etc.
18. The discovery and registration processes SHALL be established in a secure fashion as defined by the trust agreement governing the transaction. Protocols requiring the transfer of cryptographic key information SHALL use an authenticated protected channel to exchange cryptographic key information needed to operate the federated relationship, including any shared secrets or public keys. Any symmetric keys used in this relationship SHALL be unique to a pair of federation participants.
19. When domain names, URIs, or other structured identifiers are used to identify parties, wildcards SHALL NOT be used. 
20. The allowable update process for any cryptographic keys and identifiers SHALL be defined by the trust agreement and SHALL be executed using an authenticated protected channel, as in the initial cryptographic key establishment.
21. CSPs, IdPs (including subscriber-controlled wallets), and RPs SHALL store all private and shared keys used for signing, encryption, and any other cryptographic operations in a secure fashion. 
22. A subscriber’s attributes SHALL be transmitted between IdP and RP only for federation transactions or support functions such as identification of compromised subscriber accounts as discussed in [Sec. 3.9](https://pages.nist.gov/800-63-4/sp800-63c.html#privacy-reqs). 
23. A subscriber’s attributes SHALL NOT be transmitted for any other purposes, even when parties are allowlisted.
24. A subscriber’s attributes SHALL NOT be used by the RP for purposes other than those stipulated in the trust agreement. 
25. A subscribers attributes SHALL be stored and managed in accordance with [Sec. 3.10.3](https://pages.nist.gov/800-63-4/sp800-63c.html#store-subscriber-info).
26. The subscriber SHALL be informed of the transmission of attributes to an RP. 
27. In the case where the authorized party is the organization, the organization SHALL make available to the subscriber the list of approved RPs and the associated sets of attributes sent to those RPs. 
28. The RP subscriber account SHALL be bound to at least one federated identifier, and a given federated identifier is bound to only one RP subscriber account at a given RP.
29. An RP subscriber account is terminated when the RP removes all access to the account at the RP. Termination SHALL include removal of all federated identifiers and bound authenticators from the RP subscriber account (to prevent future federation transactions) as well as removal of attributes and information associated with the account in accordance with [Sec. 3.10.3](https://pages.nist.gov/800-63-4/sp800-63c.html#store-subscriber-info). 
30. An RP MAY terminate an RP subscriber account independently from the IdP for a variety of reasons, regardless of the current validity of the subscriber account from which it is derived.
31. A single RP subscriber account MAY be associated with more than one federated identifier. This practice is sometimes known as account linking. 
  a. If the RP allows a subscriber to manage multiple accounts in this way, the RP SHALL require an authenticated session with the subscriber account for all management and linking functions. 
  b. This authenticated session SHOULD require one existing federated identifier before linking the new federated identifier to the RP subscriber account. 
  c. An RP MAY offer a means of recovery of an RP subscriber account with no current means of access.
32. When a federated identifier is removed from an RP subscriber account, the RP SHALL disallow access to the RP subscriber account from the removed federated identifier.
33. The RP SHALL document its practices and policies that it enacts when an RP subscriber account reaches a state of having zero associated federated identifiers, no means of access, and no means of recovery. 
  a. In such cases, the RP subscriber account SHOULD be terminated and information associated with the account in accordance with [Sec. 3.10.3](https://pages.nist.gov/800-63-4/sp800-63c.html#store-subscriber-info).
34. The RP SHALL provide notice to the subscriber when:
  a. A new federated identifier is added to an existing RP subscriber account
  b. A federated identifier is removed from an RP subscriber account, but the account is not terminated
35. The RP MAY allow a subscriber to access their RP subscriber account using direct authentication processes by allowing the subscriber to add and remove authenticators in the RP subscriber account.
36. An authenticated session SHALL be created by the RP only when the following conditions are true:
  a. The RP has processed and verified a valid assertion
  b. The assertion is from the expected IdP for a transaction
  c. The IdP that issued the assertion is the IdP identified in the federated identifier of the assertion
  d. The assertion is associated with an RP subscriber account (which may be ephemeral)
  e. The RP subscriber account has been provisioned at the RP through the method specified in the trust agreement
37. The IdP and RP SHALL employ appropriately tailored security controls from the moderate baseline security controls defined in [[SP800-53]](https://pages.nist.gov/800-63-4/sp800-63c.html#ref-SP800-53) or equivalent federal (e.g., [[FEDRAMP]](https://pages.nist.gov/800-63-4/sp800-63c.html#ref-FEDRAMP)) or industry standard that the organization has determined for the information systems, applications, and online services that these guidelines are used to protect. 
38. The IdP and RP SHALL ensure that the minimum assurance-related controls for the appropriate systems, or equivalent, are satisfied.
39. Communications between the IdP and the RP SHALL be protected in transit using an authenticated protected channel.
40. Communications between the subscriber and either the IdP or the RP (usually through a user agent) SHALL be made using an authenticated protected channel.
41. Additional attributes about the user MAY be included outside of the assertion itself by use of authorized access to an identity API as discussed in [Sec. 3.11.3](https://pages.nist.gov/800-63-4/sp800-63c.html#s-identity-api).
42. When derived attribute values are available and fulfill the RP’s needs, the RP SHOULD request derived attribute values rather than full attribute values as described in [Sec. 7.3](https://pages.nist.gov/800-63-4/sp800-63c.html#minimization). 
43. The IdP SHOULD support derived attribute values to the extent the underlying federation protocol allows.
44. The IdP and RP SHALL delete personal identity information in the subscriber account and RP subscriber account (respectively) upon account termination, unless required otherwise by legal action or policy.
45.  Whenever personal identity information is stored in a subscriber account or RP subscriber account, whether the account is active or not, the IdP and RP SHALL determine and use appropriate controls to ensure secure storage of the personal identity information.
46. When the RP uses an ephemeral provisioning mechanism as described in [Sec. 4.6.3](https://pages.nist.gov/800-63-4/sp800-63c.html#provisioning), the RP SHALL remove all subscriber attributes at the termination of the session, unless required by legal action or policy.
47. Attributes SHALL be either unbundled (presented directly by the IdP) or bundled into a package that is cryptographically signed by the CSP, as described in [Sec. 3.11.1](https://pages.nist.gov/800-63-4/sp800-63c.html#attribute-bundles).
48. Attributes SHALL be either attribute values (e.g., a date of birth) or derived attribute values (e.g., an indication of age of majority).
49. Attributes SHALL be either presented in the assertion (and therefore covered by the assertion’s signature) or made available as part of a protected identity API.
50. Attributes about the subscriber, including profile information, MAY be provided to the RP through a protected API known as the identity API.
51. All possible use of identity APIs, including which provisioning models are available through the API, SHALL be recorded and disclosed as part of the trust agreement. 
52. Access to the identity API SHALL be time limited by the trust agreement. 
53. Access to the identity API SHOULD be limited to the duration of the federation transaction plus time necessary for synchronization of attributes, as discussed in [Sec. 4.6.4](https://pages.nist.gov/800-63-4/sp800-63c.html#attribute-sync). 
54. Since the time limitation is separate from the validity time window of the assertion and the lifetime of the authenticated session at the RP, access to an identity API by the RP without an associated valid assertion SHALL NOT be sufficient for the establishment of an authenticated session at the RP.
55. [W]hen access to the identity API is granted within the context of a federation transaction, the attributes provided by an identity API SHALL be associated with only the single subscriber identified in the associated assertion. 
56. If the identity API is hosted by the IdP, the returned attributes SHALL include the subject identifier for the subscriber. This allows the RP to positively correlate the assertion’s subject to the returned attributes. 
57. For pre-provisioning use cases, the privacy considerations SHALL be evaluated and recorded as part of the trust agreement. 
58. Assertions SHALL include a set of protections to prevent attackers from manufacturing valid assertions or reusing captured assertions at disparate RPs.
59. Assertions SHALL be sufficiently unique to permit unique identification by the target RP. Assertions MAY accomplish this by use of an embedded nonce, issuance timestamp, assertion identifier, or a combination of these or other techniques.
60. Assertions SHALL be cryptographically signed by the issuer (IdP). 
61. The RP SHALL validate the digital signature or MAC of each such assertion based on the issuer’s key. 
62. This signature SHALL cover the entire assertion, including its identifier, issuer, audience, subject, and expiration.
63. The assertion signature SHALL either be a digital signature using asymmetric keys or a MAC using a symmetric key shared between the RP and issuer. 
64. Shared symmetric keys used for this purpose by the IdP SHALL be independent for each RP to which they send assertions, and are normally established during registration of the RP.
65. Public keys for verifying digital signatures SHALL be transferred to the RP in a secure manner, and MAY be fetched by the RP in a secure fashion at runtime, such as through an HTTPS URL hosted by the IdP. 
66. Approved cryptography SHALL be used.
67. When encrypting assertions, the IdP SHALL encrypt the contents of the assertion using either the RP’s public key or a shared symmetric key. 
68. Shared symmetric keys used for this purpose by the IdP SHALL be independent for each RP to which they send assertions, and are normally established during registration of the RP. 
69. Public keys for encryption SHALL be transferred over an authenticated protected channel and MAY be fetched by the IdP at runtime, such as through an HTTPS URL hosted by the RP.
70. All encryption of assertions SHALL use approved cryptography applied to the federation technology in use.
71. Assertions SHALL use audience restriction techniques to allow an RP to recognize whether or not it is the intended target of an issued assertion. 
72. All RPs SHALL check that the audience of an assertion contains an identifier for their RP to prevent the injection and replay of an assertion generated for one RP at another RP.
73. In order to limit the places that an assertion could successfully be replayed by an attacker, IdPs SHOULD issue assertions designated for only a single audience. Restriction to a single audience is required at FAL2 and above.
74. To perform a federation transaction with a general-purpose IdP, the RP SHALL associate the assertion signing keys and other relevant configuration information with the IdP’s identifier, as stipulated by the trust agreement. 
  a. If these are retrieved over a network connection, request and retrieval SHALL be made over a secure protected channel from a location associated with the IdP’s identifier by the trust agreement. 
75. Additionally, the RP SHALL register its information either with the IdP or with an authority the IdP trusts, as stipulated by the trust agreement.
  a. In many federation protocols, the RP is assigned an identifier during this stage, which the RP will use in subsequent communication with the IdP.
76. The IdP MAY use a trusted third party to facilitate its discovery and registration processes, so long as that trusted third party is identified in the trust agreement.
77. At all FALs, the cryptographic keys and identifiers of the RP and IdP can be exchanged in a manual process, whereby the administrator of the RP submits the RP’s configuration to the IdP (either directly or through a trusted third party) and receives the identifier to use with that IdP.
  a. This process MAY be facilitated by some level of automated tooling, whereby the manual configuration points the systems in question to a trusted source of information that can be updated over time. 
  b. If such automation is used, the trust agreement SHALL enumerate the allowable terms of the cryptographic key distribution and assignment, including allowable cache lifetimes.
78. At FAL1 and FAL2, the cryptographic keys and identifiers of the RP can be exchanged in a dynamic process, whereby the RP software presents its configuration to the IdP (either directly or through a trusted third party) and receives the identifier to use with that IdP. This process is specific to the federation protocol in use but requires machine readable configuration data to be made available over the network. All transmission of configuration information SHALL be made over a secure protected channel to endpoints associated with the IdP’s identifier by the trust agreement.
79. IdPs SHOULD consider the risks of information leakage to multiple RP instances and take appropriate countermeasures, such as issuing PPIs to dynamically registered RPs as discussed in Sec. 3.3.1.
80. Dynamic registration SHOULD be augmented by attestations about the RP software and device, as discussed in Sec. 3.5.3.

*Section 4.5*

81. The IdP SHALL require the subscriber to have an authenticated session before any of the following events:
  a. Approval of attribute release
  b. Creation and issuance of an assertion
  c. Establishment of a subscriber-driven trust agreement.

*Section 4.6*
82. In an a priori trust agreement, IdPs MAY establish allowlists of RPs authorized to receive authentication and attributes from the IdP without a runtime decision from the subscriber. 
  a. When placing an RP on its allowlist, the IdP SHALL confirm that the RP abides the terms of the trust agreement. 
  b. The IdP SHALL determine which identity attributes are passed to the allowlisted RP upon authentication. 
  c. IdPs SHALL make allowlists available to subscribers as described in Sec. 7.2.
  d. IdP allowlists SHALL uniquely identify RPs through the means of domain names, cryptographic keys, or other identifiers applicable to the federation protocol in use.
  e. Any entities that share an identifier SHALL be considered equivalent for the purposes of the allowlist. 
  f. Allowlists SHOULD be as specific as possible to avoid unintentional impersonation of an RP.
  
83. IdP allowlist entries for an RP SHALL indicate which attributes are included as part of an allowlisted decision. 
  a. If additional attributes are requested by the RP, the request SHALL be either:
    1. subject to a runtime decision of the authorized party to approve the additional attributes requested,
    2. redacted to only the attributes in the allowlist entry, or
    3. denied outright by the IdP.
       
84. IdP allowlists MAY include other information, such as the xALs under which the allowlist entry is applied.
85. IdPs MAY establish blocklists of RPs not authorized to receive authentication assertions or attributes from the IdP, even if requested to do so by the subscriber. 
86. If an RP is on an IdP’s blocklist, the IdP SHALL NOT produce an assertion targeting the RP in question under any circumstances.
87. IdP blocklists SHALL uniquely identify RPs through the means of domain names, cryptographic keys, or other identifiers applicable to the federation protocol in use. 
  a. Any entities that share an identifier SHALL be considered equivalent for the purposes of the blocklist.
88. Every RP that is in a trust agreement with an IdP but not on an allowlist with that IdP SHALL be governed by a default policy in which runtime authorization decisions will be made by an authorized party identified by the trust agreement.
89. When processing a runtime decision, the IdP prompts the authorized party interactively during the federation transaction. The authorized party provides consent to release an authentication assertion and specific attributes to the RP. The IdP SHALL provide the authorized party with explicit notice and prompt them for positive confirmation before any attributes about the subscriber are transmitted to the RP.
  a. At a minimum, the notice SHOULD be provided by the party in the position to provide the most effective notice and obtain confirmation, consistent with Sec. 7.2.
  b. The IdP SHALL disclose which attributes will be released to the RP if the transaction is approved.
  c. If the federation protocol in use allows for optional or selective attribute disclosure at runtime, the authorized party SHALL be given the option to decide whether to transmit specific attributes to the RP without terminating the federation transaction entirely.
  d. If the authorized party is the subscriber, the IdP SHALL provide mechanisms for the subscriber to view the attribute values and derived attribute values to be sent to the RP.
  e. To mitigate the risk of unauthorized exposure of sensitive information (e.g., shoulder surfing), the IdP SHALL, by default, mask sensitive information displayed to the subscriber.
90. An IdP MAY employ mechanisms to remember and re-transmit the same set of attributes to the same RP, remembering the authorized party’s decision. This mechanism is associated with the subscriber account as managed by the IdP.
  a. If such a mechanism is provided, the IdP SHALL allow the authorized party to revoke such remembered access at a future time.
91. RPs MAY establish allowlists of IdPs from which the RP will accept authentication and attributes without a runtime decision from the subscriber to use the IdP.
  a. When placing an IdP in its allowlist, the RP SHALL confirm that the IdP abides by the terms of the trust agreement.
92. RP allowlists SHALL uniquely identify IdPs through the means of domain names, cryptographic keys, or other identifiers applicable to the federation protocol in use.
93. RP allowlist entries MAY be applied based on aspects of the subscriber account (such as the xALs required for the transaction).
94. RPs MAY also establish blocklists of IdPs that the RP will not accept authentication or attributes from, even when requested by the subscriber.
95. RP blocklists SHALL uniquely identify IdPs through the means of domain names, cryptographic keys, or other identifiers applicable to the federation protocol in use.
96. Every IdP that is in a trust agreement with an RP but not on an allowlist with that RP SHALL be governed by a default policy in which runtime authorization decisions will be made by the authorized party indicated in the trust agreement.
97. The RP MAY employ mechanisms to remember the authorized party’s decision to use a given IdP. S
  a. If such a mechanism is provided, the RP SHALL allow the authorized party to revoke such remembered options at a future time.
98. The RP subscriber account SHALL be provisioned at the RP prior to the establishment of an authenticated session at the RP in one of the following ways
  a. Just-In-Time Provisioning: An RP subscriber account is created automatically the first time the RP receives an assertion with an unknown federated identifier from an IdP. Any identity attributes learned during the federation process, either within the assertion or through an identity API as discussed in Sec. 3.11.3, MAY be associated with the RP subscriber account.
  b. the RP SHALL be responsible for managing any cached attributes it might have. See Fig. 7.
  c. Pre-provisioning: Pre-provisioned accounts SHALL be bound to a federated identifier at the time of provisioning. 
  d. In this model, the RP also receives attributes about subscribers who have not yet interacted with the RP (and who may never do so). This is in contrast to other models, where the RP receives information only about the subset of subscribers that use the RP, and then only after the subscriber uses the RP for the first time. The privacy considerations of the RP having access to this information prior to a federation transaction SHALL be accounted for in the trust agreement.
99. All organizations SHALL document their provisioning models as part of their trust agreement.
100. The RP MAY additionally collect, and optionally verify, other attributes to associate with the RP subscriber account, as discussed in Sec. 4.6.6.
101. The IdP SHOULD signal downstream RPs when the attributes of a subscriber account available to the RP have been updated, and the RP MAY respond to this signal by updating the attributes in the RP subscriber account. 
102. If the RP is granted access to an identity API as in Sec. 3.11.3, the IdP SHOULD allow the RP access to the API for sufficient time to perform synchronization operations after the federation transaction has concluded.
103. The IdP SHOULD signal downstream RPs when a subscriber account is terminated, or when the subscriber account’s access to an RP is revoked. 
  a. Upon receiving such a signal, the RP SHALL process the RP subscriber account as stipulated in the trust agreement.
  b. If the RP subscriber account is terminated, the RP SHALL remove all personal information associated with the RP subscriber account, in accordance with Sec. 3.10.3.
  c. If the reason for termination is suspicious or fraudulent activity, the IdP SHALL include this reason in its signal to the RP to allow the RP to review the account’s activity at the RP for suspicious activity, if specified in the trust agreement with that RP.


  


https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-63C-4.2pd.pdf 4.6.1.3



Open questions: 
1. I explicitly left out federation proxies, do we need to pull these into the requirements?
2. I left our pairwise pseudonymous identifiers (section 3.3.1) since I felt it was irrelevant to the enterprise use case.  Is this necessary for IPSIE SL1?
3. How should IPSIE deal with trust agreements?  My initial thought is that these are implicit through the business relationship between identity services and applications as defined by the enterprise.  3.4 states, "Establishment of a trust agreement is required for all federation transactions, even those in which the roles and applications exist within a single security domain or shared legal ownership. _**In such cases, the establishment of the trust agreement can be an internal process and does not need to involve a formal agreement.**_ Even in such cases, it is still required for the IdP to document and disclose the trust agreement to the subscriber upon request."
4. 3.7.2 covers account resolution.  We need to confirm this is not needed at SL1.
5. Item 35 above allows for a break glass account.  IPSIE does not yet allow for this, we should consider how IPSIE can support break glass accounts.
6. I left out the privacy requirements in 3.9.  Should these privacy requirements be met at SL1?
7. Section 4.6 regarding attribute disclosure appears unnecessary in the enterprise context, I have left it out of the requirements for now.
8. 
