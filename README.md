# CI-CD Github Actions

# Description

This project is an implementation of a CI-CD pipeline, that simulates a real workflow of a production system. The project consists of a dummy main function and a dummy test (those are irrelevant for the purpose of the project), and the CI-CD Pipelines found in `.github/workflows`.

The workflow that is being simulated represents the following scenario:

* There are several developers working on the same project, each one on his local machine.
* There is a production server where the code is running.
* The project has 3 branches: `dev` (unique for each developer), `pre_master` and `master`.

Each developer works on his `dev` branch, and whenever a code feature is finished, they push it to `pre_master` (this is covered by the CI Pipeline). Whenever the developers want, they can deploy the code to `master` and production server (this is covered by the CD Pipeline).

**CI Pipeline:** Whenever a developer pushes a change to his personal `dev` branch, the CI Pipeline is automatically triggered, following these steps:

* Create a VM with the specified OS.
* Checkout the code in the VM and install the project dependencies.
* Run tests on the VM.
* If tests pass, the code is merged from `dev` to `pre_master`.

**CD Pipeline:** The CD Pipeline can only be triggered manually, whenever a developer decides to put the code in `pre_master` to production. When this pipeline is triggered, it follows these steps:

* Merge `pre_master` into `master`.
* Run tests on the production server.
* If tests pass, the `master` code is pulled to the server.

# How to use it

* Clone the repository.
* Go to `Settings` -> `Secrets and variables` -> `Actions` and create a secret token named `TOKEN`.
* Go to `Settings` -> `Actions` -> `Runners` and create a runner. Activate the runner on your production server.

On the actions tab of the repository you can see status of the pipelines. To trigger the CI Pipeline, just push something to the `dev` branch. To trigger the CD Pipeline go to `Actions` -> `CD Pipeline` -> `Run workflow` -> Select `Use workflow from: branch pre_master` -> `Run workflow`.

# Pipelines status

[![CI Pipeline](https://github.com/ygbuil/CI-CD-GitHub-Actions/actions/workflows/ci_pipeline.yml/badge.svg?branch=dev)](https://github.com/ygbuil/CI-CD-GitHub-Actions/actions/workflows/ci_pipeline.yml)

[![CD Pipeline](https://github.com/ygbuil/CI-CD-GitHub-Actions/actions/workflows/cd_pipeline.yml/badge.svg?branch=pre_master)](https://github.com/ygbuil/CI-CD-GitHub-Actions/actions/workflows/cd_pipeline.yml)