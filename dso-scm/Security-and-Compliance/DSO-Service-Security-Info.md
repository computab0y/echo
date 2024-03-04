## The Defence DevSecOps Service and Secure-by-Design

### What does the MOD define as secure-by-design (SbD)?
The MOD defines Secure-by-Design as “An approach that enables a culture of proactive risk management and appropriate security consideration throughout a capabilities’ lifecycle by connecting cyber security principles, roles, processes, tools and techniques to achieve secure systems.” When this approach is followed, we can say a system is secure-by-design, according to <a href="https://github.com/defencedigital/dso-scm/blob/main/Security-and-Compliance/JSP440_Part2_Leaflet5C_Building%20Cyber%20Secure-by-Design%20Capabilities.pdf"> JSP 440 leaflet 5C</a>.

### How has SbD helped D2S to reduce security efforts for users in dev/test (ATHENA)?
Defence DevSecOps Services (D2S) was invited to participate as a Secure-by-Design pilot in the beta phase of the _Secure-by-Design and modernise accreditation_ project – breaking down the blockers to using SbD for devsecops in Defence, and paving the way for future teams to benefit from SbD. **The D2S platform and selected tools have already achieved assurance and are therefore secure-by-design**. As the dev/test environment (ATHENA) has achieved interim authority to operate, applications built on the DSO service can use the approved Software Development LifeCycle (SDLC) and default security controls with no further security protocols. This means that **application teams can use dev and test services at OFFICIAL without requiring authority to test (ATT) up-front.** JSP 604 assurance is still required for an application to move to production, but the requirement is limited to the application, its data, its governance and its specific security controls, without worrying about the dev/build environment or underlying infrastructure.

### How has SbD simplified the JSP 604 process for app teams moving to production (KANGOL)?
1. The MOD mandate the use of JSP 604 to ensure coherence, performance and integrity of Defence networks and this requires meeting the requirements for as many as 22 rules through engagement with a case officer and associated rule owners. The scope of the new Secure-by-Design process in JSP 440 leaflet 5C changes the way some rules are evaluated in JSP 604 e.g. rule 10
2. When moving to production, teams can expect a more straightforward JSP 604 process. The assurance of the dev/build (ATHENA) environment means less information and documentation is required and the process may be faster

### The D2S ambition for SbD
Foundry DevSecOps aspires to implement a fully secure-by-design methodology for all applications that use the platform. This will unlock the potential to rapidly develop and deploy applications to front line commands. The SbD approach will follow the NIST 800-37 risk management framework throughout the software delivery lifecycle, to enable a continuous authority to operate. It includes continuous monitoring and assurance of security, using the container-based platform and tooling, meaning applications will continue to be secure in operations. To enable this, D2S will develop guidance that provides a workable model that integrates SbD with the JSP604 process and JSP 440 leaflet 5C - providing a coherent shared responsiblity model.

### Considerations for D2S users
1. It will take time for the MOD to fully adopt a secure-by-design approach. The Foundry will communicate any changes to assurance processes as and when they are agreed.
2. There continues to be delays in assigning case officers for JSP 604 process. This means teams should kick off the process asap when joining the platform, to avoid delays in moving apps to production.

- - -

## The Defence DevSecOps Service (D2S) Device Requirements

### What devices can be used for D2S
It is mandatory that FDSO users have 'controlled' devices and it is recommended that devices also have MDM (mobile device management). This is in line with the Foundry SyOps, DevSecOps SyOps Annex and NCSC guidance. FDSO users are liable for any decision to not follow this recommendation.

### What is the requirement for a 'controlled' device?
Section 2 of the <a href="https://github.com/defencedigital/dso-scm/blob/main/Security-and-Compliance/Defence_Digital_Foundry_Security_Operating_Procedures.pdf"> Defence Digital Foundry SyOps</a> explains the criteria for a personal or supplier issued device. It must be running the latest version of a major operating system, with automatic updates enabled and data encrypted at rest. Any data backed up must be encrypted and we recommend the use of two-factor authentication, antivirus and password managers. Please see the Digital Foundry SyOps for full information.

