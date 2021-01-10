## Welcome to the DT Lab Software Project

This page documents where the various parts of the project are hosted or supported from.

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
