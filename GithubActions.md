# Github Actions

_Github actions_ is a CI/CD tool that is built into Github. It is free for public repositories and has a generous free tier for private repositories. It is a good choice for small projects that are hosted on Github.

- _File_: each yaml file is a _workflow_.
- _Workflow_: a set of _jobs_ that run in parallel.
- _Job_: a set of _steps_ that run in parallel.
- _Step_: a set of _actions_ that run in sequence.
- _Action_: a single task that can be run as part of a job.


## BuildKit Cache

BuildKit is a Docker feature that allows you to cache layers between builds. This can speed up builds significantly. It is enabled by default in Github Actions.

## QEUM

QEMU is a virtualization tool that allows you to run virtual machines on your computer. It is used by Github Actions to run Docker containers.

## Metadata

Github Actions allows you to add metadata to your workflow. This metadata is used to display information about your workflow in the Github UI.

## CVE Scanning

_Common Vulnerabilities and Exposures_:

Github Actions allows you to scan your Docker images for CVEs. This is a paid feature. _CVE Scanning_ is a feature that allows you to scan your Docker images for CVEs (Common Vulnerabilities and Exposures).

## Unit and Integration Tests

Github Actions allows you to run unit and integration tests as part of your CI/CD pipeline.

## Smoke Tests

_Smoke tests_ are a type of integration test that checks if your app is working correctly after a deployment. It differs from integration testing in that it does not test the integration between components, but rather the integration between the app and the environment.


