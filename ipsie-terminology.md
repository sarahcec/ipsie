# IPSIE Terminology

## Roles

### Enterprise

Enterprises are generally defined as entities - e.g. corportations, non-profit organizations, partnerships.  Enterprises have a workforce comprised of employees, contractors, volunteers, and others who operate on behalf of the enterprise.  Enterprises deploy applications and services to support their organizational needs.  Government, non-governmental organizations, educational entities, small businesses, and others may consider themselves enterprises.

Ultimately, the goal of the IPSIE standard is to better serve the enterprise organization. Enterprises prefer to centralize the authentication process of all the applications used across the enterprise. Among other benefits, this allows users to have only one set of credentials to manage, and enables the company to manage which users can access which applications in a central location. In this framing, enterprises have identity services, applications, data, and the policies that are used to grant, suspend, and revoke user access.

The enterprise company is also referred to as the "customer", since they may be a customer of the Identity Service provider(s) and multiple Applications.

### Identity Service

The enterprise's "Identity Service" the logical set of services used by the enterprise to manage users within their organization. The Identity Service is often purchased by the enterprise company as a service or set of services, but can also be open source software or developed in-house.  The identity service may be a single component, or multiple components with discrete functionality.

The identity service is where the users' access to applications and other resources is managed and enforced.

### Application

The "Application" is ultimately used by people within the enterprise company during their day to day work. Applications have their own resources, and users may be limited in which applications they can access or what they can do within an application. Applications use the Identity Service to authenticate users through a "single sign-on" process.  Users and entitlements are provisioned to applications through the identity service.

Applications may be purchased by the enterprise company as a service from the application vendor, in which case they are commonly referred to "Software as a Service" (SaaS).

### User

The "User" is part of the workforce of the enterprise company, and is able to use the Identity Service to log in to applications.  

## Terminology

### Workforce

The people engaged in work for a particular organization. Employees, contractors, and university faculty and staff are common examples of these people within a workforce.

### Tenant

In a multitenant system, a tenant represents an organization or group of consumers, such as partners, customers, business units, departments, projects, or environments (e.g., production or test) within a larger entity. Each tenant has users and resources assigned to them, and only these users can access the resources within their specific tenant. Tenancy can be hierarchical, allowing a parent tenant to have sub-tenants, with resources potentially shared among them.

Isolation between tenants varies along a spectrum based on business needs. At one end, physical resources are shared by trusted parties with minimal disruption, while at the other end, tenants are completely unaware of each other and may have dedicated resources. High-end solutions ensure full privacy between untrusted parties, whereas lower-end solutions allow for reduced isolation among trusted parties sharing a system.

### User Group

A group is a collection of users that typically share a common set of permissions or access rights. Groups are used to simplify access management by allowing administrators to assign permissions to multiple users at once, based on their membership in the group. This makes it easier to manage and maintain consistent access controls across an organization.

### User Provisioning

User provisioning is the process of creating, updating, and managing user accounts.

#### Just-In-Time (JIT) Provisioning

A method of user provisioning that automatically creates and manages user accounts on-demand, typically as users attempt to access resources for the first time. JIT provisioning reduces the need for manual account creation and management, and helps ensure that users have access to the resources they need when they need them.

### User Sign-on

Sign-on is the process by which a user gains access to a computer system, network, or application by providing valid credentials, typically a username and password combination. The sign-on process is a crucial component of Identity and Access Management (IAM), as it helps to verify the user's identity and ensure that only authorized individuals can access protected resources. Sign-on is often the first step in the authentication and authorization process, which is followed by granting or denying access to specific resources based on the user's assigned permissions and roles. Additionally, sign-on mechanisms can be enhanced with various security measures, such as multi-factor authentication (MFA) or single sign-on (SSO), to provide an extra layer of protection against unauthorized access or potential security threats.

### Single sign-on (SSO)

A user authentication process that allows users to access multiple applications, services, or systems with a single set of credentials. Single Sign-On simplifies the user experience by eliminating the need for users to remember and enter multiple sets of credentials for different resources. SSO can be implemented using various protocols, such as SAML and OpenID Connect.

### Multi-Factor Authentication (MFA)

An authentication method that requires users to provide more than one independent factors to verify their identity. MFA typically combines something the user knows (e.g., password), something the user has (e.g., smartphone), and/or something the user is (e.g., fingerprint). MFA enhances security by making it more difficult for unauthorized individuals to access accounts, even if they have obtained the user's password.

MFA mechanisms vary greatly in their security properties.  Enterprises should choose authentication mechanisms, including MFA, which meet their authentication assurance needs.  [NIST SP800-63 B](https://pages.nist.gov/800-63-3/sp800-63b.html) provides a useful resource for enterprises to understand an academic view of authentication assurance.  Under the SP800-63 B, multi-factor authentication is classified as [Authentication Assurance Level 2](https://pages.nist.gov/800-63-3/sp800-63b.html#sec4) (AAL2).  AAL2 is generally considered the minimum bar for authentication to sensitive enterprise resources.  AAL1 may be considered for non-sensitive data such as access to the corporate cafeteria lunch menu.

### Governance

In a general context, refers to the process of establishing and implementing policies, procedures, and frameworks to effectively manage and control an organization or system. In the context of Identity and Access Management (IAM), governance involves overseeing the use of digital identities and their access to resources across an organization. This includes setting standards, guidelines, and best practices for managing identities and access, as well as defining roles and responsibilities for IAM stakeholders, such as administrators, users, and auditors.

## Protocols

A protocol is a set of rules and guidelines for communicating and exchanging data between different systems or entities. IAM protocols define standardized methods for user authentication, authorization, and access management, and enable different applications and services to interoperate and share identity information. Some of the commonly used IAM protocols include SAML (Security Assertion Markup Language), OAuth (Open Authorization), OpenID Connect, and SCIM (System for Cross-domain Identity Management). These protocols provide a common language and framework for implementing IAM solutions, and help ensure interoperability and compatibility across different systems and applications.

### OpenID Connect (OIDC)

A protocol built on top of the OAuth 2.0 framework of specification (IETF RFC 6749 and 6750), used for authentication purposes. OIDC allows for the exchange of identity information between parties, such as an Identity Service and a relying party (e.g., a web application). It is designed to provide single sign-on (SSO) capabilities, as well as support for user authentication using JSON Web Tokens (JWTs). OIDC is widely used in modern IAM solutions and is supported by many popular Identity Services and service providers.

### System for Cross-domain Identity Management (SCIM)

A standard protocol used for automating the exchange of user identity and access information between different systems or domains. SCIM is designed to simplify the management of digital identities and reduce the need for manual provisioning and deprovisioning of users across multiple systems. It enables organizations to automate user onboarding and offboarding, enforce consistent access policies, and reduce the risk of errors and inconsistencies. SCIM is widely used in IAM solutions, especially in cloud-based environments where multiple applications and services need to share identity information.



