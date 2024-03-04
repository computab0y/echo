# DEFENCE DEVSECOPS SERVICE (D2S) SYOPS ADDENDUM
```version 1.1```

This Addendum ____SHALL____ be read in conjunction with the [Defence Digital Foundry SyOps](http://github.com/defencedigital/foundry-syops).

Users of D2S, in addition to following the requirements of the [Defence Digital Foundry SyOps](https://github.com/defencedigital/foundry-syops) __SHALL__ additionally abide by the following:

- __Responsible person:__ Each development team __SHALL__ have a responsible official/officer; this person __SHALL__ be a Crown servant with seniority not less than OF3/Chief Inspector/Senior Executive Officer (formerly C1). This person __SHALL__ be accountable to Defence Digital for ensuring the activities of the team overall adhere to the SyOps. Each user __MUST__ know who their responsible official/officer is. 

- __Classification:__ D2S' OFFICIAL environments are intended for creating assets with a classification of OFFICIAL (including all caveats) such as source code, comments, markdown files. Users are responsible for ensuring that assets they create or manage using the OFFICIAL environments __MUST NOT__ have a classification of SECRET or above, based on the [Government Security Classifications](https://assets.publishing.service.gov.uk/government/uploads/system/uploads/attachment_data/file/715778/May-2018_Government-Security-Classifications-2.pdf) policy. *Note: the classification of code will often be different than the classification of the information it is used to process.*

- Devices used to consume D2S __MUST__ be controlled devices, following the controls specified in Section 2 of the [Defence Digital Foundry SyOps](http://github.com/defencedigital/foundry-syops).

- These devices __SHOULD__ follow the [Device Security Guidance](https://www.ncsc.gov.uk/collection/device-security-guidance) and use a suitably configured Mobile Device Management system.

## Source Code Management

- __Sharing__: Users are reminded of the [Civil Service Code](https://www.gov.uk/government/publications/civil-service-code/the-civil-service-code)’s obligation to “handle information as openly as possible within the legal framework” and that all MOD users are expected to abide by the Code. In particular, users are reminded that source code is a Crown asset: users __MUST__ not keep assets from other teams unless there is a specific and compelling reason to enforce a ‘need to know’ restriction. Teams __SHOULD__ construct their assets in such a way as to maximise reuse opportunities, in particular by applying the [Security considerations when coding](https://www.gov.uk/government/publications/open-source-guidance/security-considerations-when-coding-in-the-open) in the open guidance and avoiding intellectual property barriers.

- __Review__: When providing or receiving feedback on code, users __SHOULD__ respect and value alternative viewpoints and seek, accept and offer honest criticisms of work as required by the Chartered Institute for IT’s [code of conduct](https://www.bcs.org/membership-and-registrations/become-a-member/bcs-code-of-conduct/). 

- __GitHub__: The following GitHub standards __SHALL__ be followed by all teams:

	- All repos are to be set as private or internal
	- All commits to a release branch must be signed
	- Have main as the default branch
	- Delete branch on merge
	- Have non-empty description (shouldn't be null or "")
	- Have issues enabled
	- Have recent activity (pushedAt < ?)
	- Checks for stored credentials is undertaken prior to commit
	- Have branch protection on main, with:
		- Require a pull request before merging
		- Require approvals option and a nominated person to approve the pull request
		- Require review from Code Owners option
		- Include administrators option
		- have Dependabot enabled

## For Development Environments:

- D2S development environments __SHALL ONLY__ be used for development and prototyping work only. Development includes all D2S activities short of integration testing with services or systems in another environment or running production workloads. This may include creating and carrying out unit testing, test automation, code creation, code compilation, [alpha prototypes](https://www.gov.uk/service-manual/agile-delivery/how-the-alpha-phase-works) and performance benchmarking within the assigned namespace(s). For the avoidance of doubt integration tests and production workloads __SHALL NOT__ be permitted in development environments.

- Work in development environments __MUST__ use synthetic test data unless approval has been obtained from appropriate person(s) to do otherwise. Synthetic test data means test records that do not reflect any genuine MOD activity or entities (only the schemata and data formats may be genuine). Because of the difficulty of achieving true anonymisation, test data __SHOULD__ be generated through a process other than anonymisation of genuine data.

## Integration Testing & Production Services:

- Users __SHALL__ be responsible for satisfying all [JSP604](https://www.gov.uk/government/publications/joint-service-publication-jsp-604-network-rules) rules, unless explicitly advised that a rule has been satisfied or an exemption has been obtained on their behalf by another party (e.g. via D2S assurance inheritance). Unless advised otherwise, users __SHALL__ be responsible for ensuring required approval from the Release and Deployment Board is obtained prior to integration testing with other services or providing a production service. This activity __SHOULD__ be started as early as possible, during the development process.

- Production workloads __SHOULD__ be run in a namespace designated for that purpose (i.e. not in a development namespace).

	 *For the avoidance of doubt, any workload used to conduct or transact real Defence business or process genuine Defence information constitutes a production workload (regardless of the intended purpose of the environment in which the workload is running). Production is sometimes described with the term ‘live’. For the avoidance of confusion this is not the same as [‘live’ in the meaning of the Government Service Manual](https://www.gov.uk/service-manual/agile-delivery/how-the-live-phase-works). Services in the [private beta, public beta or live service](https://www.gov.uk/service-manual/agile-delivery/how-the-beta-phase-works) phases as set out in the Manual are all considered to be ‘production’ services.*
