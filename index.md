Digital Twin Laboratory
============

Architecture Documentation
------

***a digital twin runtime framework***

-------

_this is the project's architecture documentation - follow the github link in the [blue box](https://github.com/dtlaboratory) above to get the code published so far_

-------

___STATUS: UNDER CONSTRUCTION - to run the software requires patience with the
state of the documentation and the tediousness of the initial API
ergonomics.___

-------

DT Lab is an actor-oriented distributed computing framework for hosting DTs
(Digital Twins).

DT Lab can compute near-realtime insights into the state of complex systems.

Suggested applications of DT Lab are Internet of Things (IOT), Augmented
Reality (AR), Logistics, streaming analytics - any problem that requires
near-realtime continuous calculation of actionable states at scale.  DT Lab is
especially suited to modeling complex systems of participants that combine and
advance over time in otherwise difficult to predict ways.

## What is a DT?

Digital twins are software analogs for devices, people, processes, or
collections of digital twins.  The term "digital twin" is used to distinguish
the DT from other software modeling. DTs emphasize individually programmable
software objects, each of whose state is recalculated continuously as
observations arrive in a low latency unbounded stream from the DT's
counterpart.

Examples of observations and events monitored by a DTs are:

  * Machine DTs might monitor a machine's engine temperature
  * Supply chain replenishment DTs may monitor retail sales transaction completions
  * Trading bots might monitor a bank account DT to act on the new availability of funds
  * Energy Efficiency DTs monitor doors that stay open too long
  * A truck fleet DT monitoring truck odometer readings might adjust truck assignments if it anticipates future mileage-based maintenance window overlaps - it can schedule long haul vs short haul assignments to stagger the out-of-service maintenance windows across the fleet
  * Security DTs fire alerts if motion detectors are triggered
  * A massively multiplayer online role-playing game (MMORPG) may use DTs for player avatar state
  * A hemisphere evacuation alerting system might act on an approaching asteroid's DT's current speed and distance values - our first demo app uses NASA's Near Earth Orbit API :)

In DT Lab, Each DT:

  * Computes its own state
  * Receives continuous input from counterparts
  * Is independently addressable - ask any DT about its state any time

## DT Lab Dependencies

  * A database that supports JDBC. We currently develop with Postgres DB - specifically Digital Ocean's managed Postres offering but should work with any post-9.6 Postgres.
  * Java and a Java Virtual Machine - development is currently done on Java 11 and 13
  
### DT Lab Quick Start (via Docker)

  * See dependencies above

TODO TODO TODO

### DT Lab Quick Start from Code

  * See dependencies above

```bash
git clone git@github.com:DTLaboratory/dtlab-scala-alligator.git
cd dtlab-scala-alligator
sbt assembly  # to create a superjar

export POSTGRES_HOST="<YOUR PGSQL HOST>"
export POSTGRES_PORT=<DB PORT>
export POSTGRES_DB="<DB NAME>"
export POSTGRES_USER="<DB USER>"
export POSTGRES_PASSWORD="<DB PWD>"

sbt run

# now you can interact with the unsecured on port 8080 - see examples dir for REST API usage
# see https://somind.tech/dtlab-alligator/doc/dtlab/ for Open API docs
```

## DT Lab Fully Functioning Cloud Deployment

TODO TODO TODO

## DT Lab Architecture

Introduction and Goals
-------

The DT Lab framework enables a user to instantiate a system of digital twins
in the public cloud or on-prem cluster of computers.

The project goal is that a useful system can be instantiated from configured
DT Lab components with complete security and integration features.  It is
also the goal of DT Lab to support configuration entirely in a declarative
deployment-time style via REST-like API - no first class programming language
coding should be required to program useful DTs.

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

External automation can interact with the DTs via the DT Lab HTTP API. An
external system will be able to register a webhook with a DT Lab cluster and
listen for all assessments calculated by all DTs as each DT state advances.

DT Lab may be operated by an organization for its own purposes or by a
service provider for its customers - perhaps as a SAAS.

If operated as a SAAS, the operator would need to provide a front-end to
its customers that supported multi-tenancy.  No changes to the
DT Lab base code would be required to support multi-tenancy but the API calls
to operate the system on behalf of the SAAS users should be sharded across
clusters with tenant ID enforced in the sharding.

Solution Strategy
-------

The DT Lab implementation values actor programming, asynchronous messaging, and
persistence via event sourcing.

The system is developed with modern cloud infrastructure-as-code tools and
practices in mind.  A new deployment can be instantiated in the cloud or via an
IOT solution pushing firmware/appware to a smart edge device

Input from the DT's analogs must arrive in standard marshaling syntaxes (JSON,
etc...) for out-of-the-box integration.  Output is marshaled in JSON and is
available as an unbounded stream so that it can be processed by modern
analytics tools like OpenTSDB, InfluxdB, Apache Spark, Grafana, Elastic Search,
or accumulated in cloud Blob services like Azure Storage or AWS S3, etc...

A foundational idea in DT Lab is that information from outside the DT Lab
runtime is normalized into multiple time series before any DT processing.  The
arriving data is transformed into `name,datetime,value(double)` records before
it is seen by a DT.  The only context surviving data after it arrives is the
`name` and `datetime`.  `name` can be overloaded at ingest time via enrichment
to provide more context to processing but the limitation of context to `name`
and `datetime` is a hard and fast rule.

#### NO BREAKING API CHANGES

Each repository name contains the service name, the computer language
implementation, and the version name.  The initial version names are
[animals](https://gist.github.com/navicore/b578e4c6e15d125b1a04ec522e295acf) in
alphabetic order.

The redundancy of embedding the version in the component name instead of just
advancing the semantic numeral major value is due to the propensity of
engineers to introduce breaking changes to APIs.  We want incompatible code to
be obvious, not subtle.  It is never OK to break backwards compatibility in DT
Lab.

*See [Hickey](https://www.youtube.com/watch?v=oyLBGkS5ICk) on semantic
versioning, "If it is not backward compatible, rename it."*

We make an explicit commitment to the user. A new backwards-incompatible
implementation will live in a new repository of a different name without the
overhead and false hopes of a git fork merge and semantic version number
advance. The successor to the
[alligator](https://github.com/DTLaboratory/dtlab-scala-alligator) version that
has a backwards-incompatible change is the
[badger](https://github.com/DTLaboratory/dtlab-scala-badger) version and no user
should expect the badger version to work with code designed for the alligator
version. However, we promise that all future releases of alligator will support
all software that has ever worked with earlier releases of alligator.  The
badger version may not be a full feature set of alligator and may not even be
of the quality of alligator and alligator could back-port badger features or
keep implementing new features as long is it does not break existing APIs.  The
new name merely indicates incompatibility.

```
<projectName>-<langName>-<versionName>

example 1: dtlab-scala-alligator
example 2: dtlab-rust-alligator
example 3: dtlab-rust-badger
example 4: dtlab-ingest-rust-badger
```


Building Block View
-------

![Building Block View](diagrams/building_blocks_1.png)

The primary building blocks are the digital twin and an incoming unbounded
stream of observations. The state of the digital twins can be processed by
traditional off-the-shelf data analytics tools.

Runtime View
-------

![Runtime View](diagrams/runtime_1.png)

The system tends to flow from left to right with observations starting at the
left and DT state shared to standard tools at the right.

Data in the above deployment is read from a remote MQTT server by a container
instantiated from the [DT Lab MQTT Ingest
Service](https://github.com/DTLaboratory/dtlab-ingest-mqtt).

The Ingest MQTT client then posts the incoming raw telemetry to the [DT Lab
Ingest Service](https://github.com/DTLaboratory/dtlab-ingest-scala-alligator)
via HTTP.

The Ingest Service then transforms the incoming data into a list of
`name,datetime,value(double)` observations that it then posts to the [DT Lab
runtime](https://github.com/DTLaboratory/dtlab-scala-alligator) where the DTs
will be updated in accordance with the `name` calculated/enriched by the ingest
service.

Deployment View
-------

![Deployment View](diagrams/deployment.png)

A normal deployment would be managed Kubernetes from a cloud provider paired
with a managed database.  However, all the DTLab Docker images make no
Kubernetes or PAAS-database assumption and the system can be run in any
Docker-enabled environment.

Cross Cutting Concepts
-------

  1. Actor programming - We value actor programming not so much as a means of
                        parallelism but as a way to build a system we can
                        then reason about.  Search Youtube for a great interview
                        of Alan Kay by Joe Armstrong to learn more of this perspective.
  2. Event Sourcing - in support of the goal of 
    * "Explainable AI"
    * Audits
    * Replay features
    * "What if" and back-test scenarios using the prototype-based DT clone feature
  3. 100% Config by HTTP API

Architectural Decisions
-------

Important, expensive, critical, large scale or risky architecture decisions including rationales.

1. Scala and Akka
  * The first implementation is written in Scala.
  * Actor programming and pattern matching are leveraged throughout the code - these two features are harder to use in other languages.  The choices were between Scala and Erlang/Elixir to get these features and Erlang/Elixir has not been made container-friendly yet.  Scala is a bit more accessible than Erlang/Elixir because of the popularity of the JVM it runs on on integration with Java.
  * Risk is the Scala community - ugh.
2. Webhooks
  * Pushing queue processing to the outer edges of the system and using webhooks and HTTP as the main composability approach.  Composing with webhooks can be optimized via sidecar containers.
  * A risk is HTTP overhead - future implementations will probably want gRPC or similar intra-system binary APIs.
3. Event Sourcing
  * Auditable
  * No complex database models improperly designed - fewer scaling problems due to poor partitioning and clustering.
  * Rewind and recalculation (back-testing) features are enabled with event sourcing.
  * Prototype-based programming of DTs is enabled via event sourcing.
4. DT Singletons
  * Containerization w/ sharding and actor resurrection - all DTs must advance their state and respond to queries w/o issue with the system at n-1 containers.


Quality Requirements
-------

1. Horizontally Scalable
  * Process back-testing of 1 million devices 24X faster than the live system collects the data.
  * Actor state query API must remain responsive under all ingest loads.
2. Fault Tolerant
  * Survive chaos agent testing.
  * All DTs must advance their state and respond to queries w/o issue with the system at n-1 containers.


Risks
-------

***NO ONE IS USING THIS SOFTWARE FOR REAL WORK TO OUR KNOWLEDGE***

## Project Status

DT Lab is currently a single-contributor project by [Ed Sweeney](https://github.com/navicore) 
and licensed with [the MIT Open Source license](https://github.com/dtlaboratory/dtlab-scala-alligator/blob/master/LICENSE).

Pull requests, feedback, and collaboration welcome.

We believe DT Lab is worth studying, implementing, and refining in other
programming languages and platforms - we intend to create Python, Rust, and
Erlang/Elixir implementations, time permitting.

### Links

1. [Github](https://github.com/dtlaboratory) - all the code is Open Source
1. CICD is managed by Github [Actions](https://github.com/features/actions)
1. Code quality is monitored by [Codacy](https://app.codacy.com/organizations/gh/dtlaboratory/repositories)
1. SBT dependency updates are managed by the [Scala Steward](https://github.com/scala-steward-org/scala-steward) bot PRs
1. Docker images are at [Dockerhub](https://hub.docker.com/orgs/dtlaboratory/repositories) (for now)
1. [UI](https://sandbox.dtlaboratory.com) - will host a react.js UI for talking to DTs - currently only demo for Auth0 SSO
1. [Notebooks (Jupyterhub)](https://notebook.somind.tech) - contact Navicore to get your github ID whitelisted
1. DTLab API [Docs](https://somind.tech/dtlab-alligator/doc/dtlab/) - OpenAPI 3.0
1. DTLab API sandbox endpoint - https://sandbox.somind.tech/dtlab-alligator/(type/actor)
1. DTLab Ingest API [Docs](https://somind.tech/dtlab-alligator/doc/dtlab-ingest/) - OpenAPI 3.0
1. DTLab Ingest API sandbox endpoint - https://sandbox.somind.tech/dtlab-alligator/extractor/(specId)
1. Security is Implemented by [Auth0](https://manage.auth0.com/dashboard/us/navicore/) - contact Navicore for access
1. Project Kanban with backlog and help wanted tags is [here](https://github.com/orgs/dtlaboratory/projects/1)
1. This page is generated from the `gh-pages` branch of the [DTLaboratory.github.io](https://github.com/dtlaboratory/dtlaboratory.github.io/blob/gh-pages/index.md)

### Hosting

1. The system is currently run on Digital Ocean managed Kubernetes.
1. TLS is implemented with Lets Encrypt.
1. DT event sourcing is persisted to Digital Ocean managed Postgres.
1. IOT Device Management and Connectivity via Cloud PAAS
    * AWS IOT Core is deployed with webhook forwarding to the DTLab sandbox Ingest Service (contact Navicore for access)
    * MQTT (TBD)
    * Azure IotHub (TBD)

### Support or Contact

Want more information or to get involved?  Open an issue [here](https://github.com/dtlaboratory/dtlaboratory.github.io/issues) and say hello or DM @navicore on Twitter.
