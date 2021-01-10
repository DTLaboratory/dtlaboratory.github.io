Digital Twin Laboratory
============

***a digital twin runtime framework***

-------

DT Lab is an actor-oriented distributed computing framework that can be programmed
to host clusters of DTs (Digital Twins).

Typical applications are IOT, AR, Logistics, general purpose streaming analytics -
any problem that requires near-realtime continuous calculation of actionable
states at scale.

The DT Lab implementation values actor programming, asynchronous messaging, and
persistence via event sourcing.

## What is a DT?

Digital twins are software analogs for devices, processes, or collections of other digital
twins.  The term "digital twin" is used to distinguish the DT from other software modeling
with an emphasis on individually programmable software objects, each of whose state is
recalculated continuously as observations arrive in a low latency unbounded stream from the DT's counterpart.

In DT Lab, DTs have the following characteristics:

*Each DT...*
  * computes its own state
  * receives continuous input from counterparts
  * is independently addressable - ask any DT about its state any time

## DT Lab Architecture

See [here](ARCHITECTURE.md)

## Project Status

DT Lab is currently a single-contributor project by Ed Sweeney and licensed 
with [the MIT Open Source license](https://github.com/DTLaboratory/dtlab-scala-alligator/blob/master/LICENSE).

Pull requests, feedback, and collaboration welcome.

We believe the features and component responsibility divisions in DT Lab are
worth studying, implementing, and refining in other languages and platforms - we
intend to create Python, Rust, and Erlang/Elixir implementations, time permitting.

### Links

1. [Github](https://github.com/DtLaboratory) - all the code is Open Source
1. CICD is managed by Github [Actions](https://github.com/features/actions)
1. Code quality is monitored by [Codacy](https://app.codacy.com/organizations/gh/DtLaboratory/repositories)
1. SBT dependency updates are managed by the [Scala Steward](https://github.com/scala-steward-org/scala-steward) bot PRs
1. Docker images are at [Dockerhub](https://hub.docker.com/orgs/dtlaboratory/repositories) (for now)
1. [UI](https://sandbox.dtlaboratory.com) - will host a react.js UI for talking to DTs - currently only demo for Auth0 SSO
1. [Notebooks (Jupyterhub)](https://notebook.dtlaboratory.com) - contact Navicore to get your github ID whitelisted
1. DtLab API [Docs](https://dtlaboratory.com/dtlab-alligator/doc/dtlab/) - OpenAPI 3.0
1. DtLab API sandbox endpoint - https://sandbox.dtlaboratory.com/dtlab-alligator/(type/actor)
1. DtLab Ingest API [Docs](https://dtlaboratory.com/dtlab-alligator/doc/dtlab-ingest/) - OpenAPI 3.0
1. DtLab Ingest API sandbox endpoint - https://sandbox.dtlaboratory.com/dtlab-alligator/extractor/(specId)
1. Security is Implemented by [Auth0](https://manage.auth0.com/dashboard/us/navicore/) - contact Navicore for access
1. Project Kanban with backlog and help wanted tags is [here](https://github.com/orgs/DtLaboratory/projects/1)
1. This page is generated from the `gh-pages` branch of the [DtLaboratory.github.io](https://github.com/DtLaboratory/DtLaboratory.github.io/blob/gh-pages/index.md)

### Hosting

1. The system is currently run on Digital Ocean managed Kubernetes.
1. TLS is implemented with Lets Encrypt.
1. DT event sourcing is persisted to Digital Ocean managed Postgres.
1. IOT Device Management and Connectivity via Cloud PAAS
    * AWS IOT Core is deployed with webhook forwarding to the DtLab sandbox Ingest Service (contact Navicore for access)
    * MQTT (TBD)
    * Azure IotHub (TBD)

### Support or Contact

Want more information or to get involved?  Open an issue [here](https://github.com/DtLaboratory/DtLaboratory.github.io/issues) and say hello or DM @navicore on Twitter.
