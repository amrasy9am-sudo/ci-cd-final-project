# CI/CD Final Project – Counter Service

**Project name:** ci-cd-final-project
**Author:** Mohamad Amirul Asyraf

Final project for the Coursera course **Continuous Integration and Continuous Delivery (CI/CD)** by IBM Skills Network.

## Overview

A small Python Flask REST service (a counter API) with a complete CI/CD pipeline:

| Stage | Tool | Location |
|---|---|---|
| Continuous Integration | GitHub Actions (flake8 lint + nose unit tests) | `.github/workflows/workflow.yml` |
| Pipeline tasks | Tekton (`cleanup`, `nose`, `flake8`) | `.tekton/tasks.yml` |
| Continuous Delivery | OpenShift Pipelines (clone → lint/test → build → deploy) | `.tekton/pipeline.yml` |

## Pipeline flow

```
cleanup → git-clone → flake8 ┐
                    → nose   ┴→ buildah (build image) → openshift-client (deploy)
```

## Run locally

```bash
bash bin/setup.sh
exit            # start a new shell to activate the venv
pip install -r requirements.txt
flake8 service --count --max-complexity=10 --max-line-length=127 --statistics
nosetests -v --with-spec --spec-color --with-coverage --cover-package=service
```

## License

Licensed under the Apache License. See LICENSE.

© IBM Corporation 2023. All rights reserved.
