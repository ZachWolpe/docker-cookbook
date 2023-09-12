# Automation CI/CD

`Pull Request Workflow`: Standard industry practice for managing changes to a codebase.


Automation (including CI/CD) is growing rapidly closer to the actual development cycle - GitOps. GitHub Actions is a great example of this.

----
# Basic Workflow

Phase 1.
1. Push to PR Branch
2. Image Build
3. Image Test

Once tests pass.

Phase 2.
1. PR merged to master
2. Image Build
3. Image push to registry
4. Deploy


----
# Intermediate Code PR Automation Workflow

Phase 1.
1. Push to PR Branch
2. Image Build test stage
3. Image Test
4. Linting
5. Unit Test
6. Integration Test
7. CVE Scanning

Once tests pass.

Phase 2.
1. PR merged to master
2. Image Build prod stage
3. Image push to registry
4. Deploy

----
# Advanced Code PR Automation Workflow

Phase 1.
1. Push to PR Branch
2. Image Build test stage
    2.1 Unit Test
    2.2 Integration Test
    2.3 CVE scanning
3. Linting
4. SAST (security testing)
5. Deployment smoke test

Once tests pass.

Phase 2.
1. PR merged to master
2. Image Build prod stage
3. Image push to registry
4. Deploy


----
# Linting

Linting is the process of running a program that will analyse code for potential errors.


----
# GitHub Actions

GitHub Actions is a CI/CD tool that is built into GitHub. It is a great example of GitOps.
