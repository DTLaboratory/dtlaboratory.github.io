DT Lab Architecture
===========

Introduction and Goals
-------

The DT Lab framework enables a user to instantiate a system of digital twins
in the public cloud or on-prem cluster of computers.

The project goal is that a useful system can be instantiated from configured
Dt Lab components with complete security and integration features.  It is
also the goal of DT LAB to support configuration entirely in a declarative
style deployment-time configuration via REST-like API - no dropping down into
first class programming languages required to host useful DTs.

Constraints
-------

* MIT/BSD/Apache2 licensed dependencies (100% Open Source)
* No reliance on VM abstractions (100% containerized)
* Can run on a system-on-a-board (1g RPi)
* Completely programmable via API (no config files)

Context and Scope
-------

The DT Lab system is operated as a utility and service.

In its initial releases, DT Lab can support DTs for sources that emit telemetry
in JSON format.  Other data formats will be added as they are requested.

External automation can interact with the DTs via the DT Lab HTTP API.
A normal use case would be for an external system to register a webhook with
a DT Lab cluster and listen for assessments calculated by the DTs as their
state advances.

DT Lab may be operated by an organization for its own purposes or by a
service provider for its customers - perhaps as a SAAS.

If operated as a SAAS, the operator would need to provide a front-end to
its customers that supported multi-tenancy.  No changes to the
DT Lab code base would be required to support multi-tenancy but the API calls
to operate the system on behalf of the SAAS users should be sharded across
clusters with tenant ID enforced in the sharding.

Solution Strategy
-------

The system is developed with modern cloud infrastructure-as-code tools and
practices in mind.  A new deployment should be able to be instantiated via
CI/CD pipelines in the cloud or via an IOT solution push of firmware/appware
to a a smart edge device with no manual intervention.  Input and output should
be in standard marshaling syntaxes (JSON, etc...) for off-the-shelf integration
with other systems.

Building Block View
-------

![My image](diagrams/building_blocks_1.png)


Runtime View
-------

![My image](diagrams/runtime_1.png)

Deployment View
-------

Technical infrastructure with environments, computers, processors, topologies. Mapping of (software) building blocks to infrastructure elements.

Cross Cutting Concepts
-------

Overall, principal regulations and solution approaches relevant in multiple parts (→ cross-cutting) of the system. Concepts are often related to multiple building blocks. Include different topics like domain models, architecture patterns and -styles, rules for using specific technology and implementation rules.

Architectural Decisions
-------

Important, expensive, critical, large scale or risky architecture decisions including rationales.


Quality Requirements
-------

Quality requirements as scenarios, with quality tree to provide high-level overview. The most important quality goals should have been described in section 1.2. (quality goals).

Risks
-------

***NO ONE IS USING THIS SOFTWARE FOR REAL WORK TO OUR KNOWLEDGE***
