<img src="https://r2cdn.perplexity.ai/pplx-full-logo-primary-dark%402x.png" style="height:64px;margin-right:32px"/>

## What the exam wants

The case describes a fragile delivery process: developers commit directly to `main`, testing is manual and late, releases are copied manually, and there is no issue tracking or operational control. That creates clear risks around quality, traceability, security, and scaling, especially for a business-critical internal system.[^1_2][^1_3]

Your solution should therefore show a shift to a modern delivery model built around **version control discipline, CI/CD, automated tests, controlled promotion between environments, and Kubernetes-based deployment**. GitLab is especially relevant here because it combines source control, CI/CD, environments, approvals, and the container registry in one platform.[^1_4][^1_5][^1_1]

## Recommended framing

I would present your project as: **“From ad hoc development to controlled continuous delivery.”** That is a much stronger narrative than just “we added a pipeline.”[^1_6][^1_1]

A good structure is:

- Analyze current workflow weaknesses.
- Map each weakness to a DevOps practice.
- Demonstrate the new target workflow with the Flask app.
- Show a change moving from commit to staging to approved production.[^1_7][^1_1]


## Key risks to analyze

The current workflow has several high-value weaknesses you should explicitly call out:

- **Direct commits to `main`** increase integration risk and reduce review quality; DORA research links continuous integration practices with stronger delivery performance.[^1_8][^1_6]
- **Manual end-of-week testing** delays feedback, which increases batch size and makes defects more expensive to isolate and fix.[^1_9][^1_6]
- **Manual deployment by the team lead** creates a bottleneck and a single point of failure; OWASP SAMM recommends automated deployment or manual deployment by personnel other than developers, with strong control and auditing.[^1_3][^1_2]
- **No issue tracking or structured incident handling** means weak traceability and poor basis for improvement metrics such as change failure rate and time to restore.[^1_10][^1_11]
- **Little DevOps experience while scaling from 3 to ~10 developers** means process weakness will compound as the organization grows unless workflows are standardized early.[^1_12][^1_1]


## Best-practice target state

Your recommended target process should look roughly like this:


| Area | Current | Recommended |
| :-- | :-- | :-- |
| Branching | Direct commits to `main` | Short-lived feature branches + merge requests + protected `main` [^1_1][^1_13] |
| Testing | Manual, end of week | Automated tests in CI on every push/MR, with coverage reporting [^1_8][^1_9] |
| Build artifacts | Unclear/manual | Build immutable container images in CI and push to GitLab Container Registry [^1_1][^1_5] |
| Staging | Manual release transfer | Automatic deploy to `staging` namespace after successful pipeline on `main` [^1_1] |
| Production | Manual release by leader | Manual approval gate + protected production environment + controlled deploy [^1_4][^1_13] |
| Runtime | Not formalized | Gunicorn in staging/production, SQLite only for development, Postgres in staging/production [^1_14] |
| Kubernetes access | Likely broad/manual | Least-privilege deployment access using RBAC and GitLab/Kubernetes integration practices [^1_2][^1_12] |

## Concrete solution design

For the technical implementation, I would recommend this architecture:

- **Development**
    - Run Flask locally with SQLite for simplicity.
    - Use environment-based config so database backend changes by environment, not by code edits.[^1_14]
- **CI pipeline**
    - Lint/test stage.
    - Coverage report stage.
    - Container build stage.
    - Push image to GitLab Container Registry.
    - Deploy to Kubernetes staging namespace automatically.
    - Deploy to production namespace only after approval.[^1_5][^1_1][^1_4]
- **Kubernetes**
    - Separate namespaces: `staging` and `production`.
    - App image pulled from GitLab registry using `imagePullSecrets`.
    - App container contains only the built artifact, not mounted source code.
    - Postgres deployed separately per non-dev environment.
    - Gunicorn as the WSGI server in staging and production.[^1_15][^1_16][^1_14]

That design directly satisfies the stated requirements around namespaces, deployment flow, registry usage, database separation, and Gunicorn.[^1_1][^1_14][^1_5]

## GitLab practices to emphasize

GitLab gives you several things you should explicitly mention in both slides and documents:

- **Protected environments** let you restrict who can deploy to production.[^1_13]
- **Deployment approvals** allow production jobs to pause until an authorized approval is given.[^1_17][^1_4]
- **Environments** provide visibility into what is deployed where.[^1_4][^1_1]
- **Container Registry** keeps deployment artifacts versioned and tied to commits.[^1_5]

This matters because your audience is both management and developers; management cares about control and auditability, while developers care about speed and repeatability.[^1_2][^1_1]

## Suggested workflow

A strong proposed workflow for the company is:

1. Developer creates an issue/task.
2. Developer creates a short-lived branch.
3. Changes are pushed and CI runs tests automatically.
4. A merge request is opened and reviewed.
5. After merge to `main`, CI builds the image and deploys automatically to staging.
6. Staging is validated.
7. Production deployment requires manual approval and then deploys to the production namespace.
8. Deployment outcome is visible in GitLab and rollback uses a previous image tag if needed.[^1_13][^1_1][^1_4]

This is a much better answer than “use DevOps tools,” because it shows an operating model, not just a tool list.[^1_6][^1_1]

## Metrics and maturity

If you want to look more advanced, add a short section on **how the company should measure improvement** using DORA-style metrics:

- Deployment frequency
- Lead time for changes
- Change failure rate
- Time to restore service[^1_11][^1_10][^1_6]

You do not need to fully implement all of that for the exam, but mentioning these metrics makes your analysis more professional because it connects DevOps practices to measurable business outcomes.[^1_11][^1_9]

## What to put in each deliverable

### Presentation

Keep it management-friendly and visual:

- What DevOps is
- What is wrong today
- What the new pipeline does
- Why this reduces risk and supports growth
- Demo: commit → pipeline → staging → approval → production[^1_7][^1_1]


### Process Guide

Document the human workflow:

- Roles and responsibilities
- Branching and merge request rules
- Definition of done
- Release approval flow
- Incident/bug handling process[^1_3][^1_2]


### Setup Guide

Document the technical setup:

- Local developer setup
- GitLab variables/secrets
- Registry auth
- Kubernetes namespaces
- Postgres/Gunicorn deployment details
- How to trigger and approve deployments[^1_16][^1_14][^1_4]


### Appendices

Include:

- `.gitlab-ci.yml`
- Dockerfile(s)
- Kubernetes manifests or Helm values
- Modified 
Flask code
- Test suite
- Coverage config
- Any helper scripts[^1_1][^1_5]


## What will impress the examiner

The strongest submissions usually do three things well:

- They connect **business risk** to **technical controls**.[^1_2][^1_3]
- They show a **working pipeline**, not just diagrams.[^1_1]
- They explain both **why** a practice exists and **how** it is implemented.[^1_6][^1_1]

For this assignment, I would avoid shallow buzzwords and instead argue that the new setup improves **feedback speed, deployment safety, traceability, reproducibility, and team scalability**. Those are the real themes underneath the formal requirements.[^1_9][^1_2][^1_1]

If you want, I can next help you with one of these:

1. a **full slide-by-slide presentation outline** for the 10-minute talk
2. a **recommended architecture and `.gitlab-ci.yml` design** for the Flask app
3. a **full report structure** for `Process Guide.pdf` and `Setup Guide.pdf`
<span style="display:none">[^1_18][^1_19][^1_20][^1_21][^1_22][^1_23][^1_24][^1_25][^1_26][^1_27][^1_28][^1_29][^1_30]</span>

<div align="center">⁂</div>

[^1_1]: https://about.gitlab.com/blog/from-code-to-production-a-guide-to-continuous-deployment-with-gitlab/

[^1_2]: https://owaspsamm.org/model/implementation/secure-deployment/stream-a/

[^1_3]: https://blog.convisoappsec.com/en/implementation-according-to-samm-secure-deployment-in-application-security/

[^1_4]: https://docs.gitlab.com/ci/environments/deployment_approvals/

[^1_5]: https://docs.gitlab.com/user/packages/container_registry/

[^1_6]: https://launchdarkly.com/blog/dora-metrics/

[^1_7]: https://www.youtube.com/watch?v=TMQziI2VDbQ

[^1_8]: https://dora.dev/capabilities/continuous-integration/

[^1_9]: https://www.red-gate.com/simple-talk/devops/what-are-the-key-devops-performance-metrics-you-should-track/

[^1_10]: https://grafana.com/blog/cd-observability-extracting-dora-metrics-from-a-cd-pipeline/

[^1_11]: https://cloud.google.com/blog/products/devops-sre/another-way-to-gauge-your-devops-performance-according-to-dora

[^1_12]: https://docs.gitlab.com/user/clusters/agent/enterprise_considerations/

[^1_13]: https://docs.gitlab.com/ci/environments/protected_environments/

[^1_14]: https://testdriven.io/blog/flask-docker-traefik/

[^1_15]: https://stackoverflow.com/questions/70826356/how-can-you-use-a-private-gitlab-container-registry-to-pull-an-image-in-kubernet

[^1_16]: https://chris-vermeulen.com/using-gitlab-registry-with-kubernetes/

[^1_17]: https://genboree.org/gitlab/help/ci/environments/deployment_approvals.md

[^1_18]: https://www.glukhov.org/post/2025/11/devops-metrics-dora/

[^1_19]: https://grafana.com/blog/2024/03/26/ci/cd-observability-extracting-dora-metrics-from-a-cd-pipeline/

[^1_20]: https://github.com/OWASP/samm/blob/master/Current Releases/head/core/implementation/i-secure-deployment.md

[^1_21]: https://www.reddit.com/r/devops/comments/1kq7m3p/is_dora_enough_what_we_learned_after_building/

[^1_22]: https://oneuptime.com/blog/post/2025-12-21-gitlab-ci-environments/view

[^1_23]: https://oneuptime.com/blog/post/2025-12-21-gitlab-deployment-approvals/view

[^1_24]: https://devwelt.de/help/ci/environments/deployment_approvals.md

[^1_25]: https://microfluidics.utoronto.ca/gitlab/help/ci/environments/deployment_approvals.md

[^1_26]: https://vdemir.github.io/assets/lisp-c/How to configure Flask to run on Docker with Postgres, Gunicorn, Nginx.pdf

[^1_27]: https://github.com/diffblue/gitlab/blob/master/doc/ci/environments/deployment_approvals.md

[^1_28]: https://dev.to/rahatnaqvi/building-a-multi-tier-flask-app-with-gunicorn-nginx-postgresql-and-systemd-using-ansible-5579

[^1_29]: https://repository.prace-ri.eu/git/help/ci/environments/deployment_approvals.md

[^1_30]: https://stackoverflow.com/questions/77644263/optimising-gunicorn-configuration-for-high-concurrency-i-o-intensive-tasks-with


---

# how would the manual approval deployment work. in terms of interface for the approver etc?

In GitLab, the approver does **not** SSH into anything or run Kubernetes commands directly; the approval is handled in the GitLab web UI as part of the deployment workflow for a protected environment. A deployment to production is held in a blocked or waiting-for-approval state until the required approver(s) explicitly approve it in GitLab.[^2_1][^2_2]

## What the approver sees

The approver typically works in **GitLab → Operate → Environments → production**. There, they can open the pending deployment, inspect its status badge, and see whether it is waiting for approval before it can proceed.[^2_1]

From that deployment view, GitLab shows:

- Eligible approvers.
- How many approvals are required and how many have already been given.
- Which users already approved.
- Approval or rejection history.[^2_1]

GitLab also allows the approver to add a comment when approving or rejecting, which is useful for auditability and for explaining why a release was accepted or blocked.[^2_1]

## Important nuance

Approval and execution are **separate** steps in GitLab’s deployment approval model. After the required approvals are granted, the deployment job still must be run manually; approval alone does not automatically execute the job.[^2_1]

That means the production flow is usually:

1. Pipeline reaches the production deploy stage.
2. Deployment is blocked pending approval.
3. Authorized approver opens the deployment in GitLab and clicks **Approve** or **Reject**.
4. Once approved, an authorized user manually starts the deploy job.[^2_1]

For your presentation, this is actually a good thing to highlight: it creates a deliberate two-step control point rather than “one click instantly goes live.”[^2_2][^2_1]

## Who can approve

Only users with permission to deploy to the protected environment can approve or reject that deployment. Protected environments let you define exactly which users, roles, or groups are allowed to deploy, and separately who can act as approvers.[^2_2][^2_1]

GitLab also supports approval rules, including multiple approval rules, but the number of required approvals must be lower than the number of eligible deployers/approvers in the rule set. A single user can only give one approval per deployment.[^2_1]

## How this looks in practice

A realistic exam-friendly setup would be:

- **Staging**: deploys automatically after tests pass.[^2_1]
- **Production**: deploy job targets a protected `production` environment, so GitLab stops and waits for approval.[^2_2][^2_1]
- **Approver**: team lead, ops person, or designated release manager opens the environment page, reviews the pending deployment, optionally checks staging, then clicks **Approve**.[^2_1]
- **Release execution**: the production deploy job is then started manually by an authorized user.[^2_1]

So the approver interface is essentially a **GitLab deployment approval screen**, not a custom UI you need to build.[^2_1]

## How to explain it simply

You can phrase it like this in your report or slides:

> “When a production deployment is created, GitLab places it in a waiting-for-approval state. An authorized approver reviews the deployment in the GitLab Environments interface, sees who requested it and whether all checks passed, and then approves or rejects it. Only after approval can the production deployment job be started.”[^2_2][^2_1]

## What I would recommend for your case

For this assignment, I would keep the approval model simple and defensible:

- 1 required approval for production.[^2_1]
- Only team lead or release-responsible members as approvers.[^2_2]
- Developers can deploy automatically to staging, but not directly to production.[^2_2]
- Require the approver to verify the staging deployment before approving production. This is a process recommendation rather than a GitLab-enforced rule, but it fits the case well.[^2_2][^2_1]

If you want, I can next show you:

- a **concrete `.gitlab-ci.yml` example** for staging + production approval, or
- a **mock walkthrough of the exact GitLab UI flow** step by step for your presentation.
<span style="display:none">[^2_10][^2_11][^2_12][^2_13][^2_14][^2_15][^2_16][^2_17][^2_3][^2_4][^2_5][^2_6][^2_7][^2_8][^2_9]</span>

<div align="center">⁂</div>

[^2_1]: https://www.glukhov.org/post/2025/11/devops-metrics-dora/

[^2_2]: https://dora.dev/capabilities/continuous-integration/

[^2_3]: https://docs.gitlab.com/ci/environments/deployment_approvals/

[^2_4]: https://genboree.org/gitlab/help/ci/environments/deployment_approvals.md

[^2_5]: https://gitlab.com/groups/gitlab-org/-/epics/6832

[^2_6]: https://repository.prace-ri.eu/git/help/ci/environments/deployment_approvals.md

[^2_7]: https://www.youtube.com/watch?v=DRQuGCGfrKA

[^2_8]: https://gitlab.com/gitlab-org/gitlab/-/issues/345683

[^2_9]: https://docs.gitlab.com/ci/environments/protected_environments/

[^2_10]: https://microfluidics.utoronto.ca/gitlab/help/ci/environments/deployment_approvals.md

[^2_11]: https://gitlab.com/gitlab-org/gitlab/-/issues/342180

[^2_12]: https://gitlab.com/gitlab-org/gitlab/-/issues/343864

[^2_13]: https://dds.uel.br/gitlab/help/ci/environments/deployment_approvals.md

[^2_14]: https://gitlab.com/gitlab-org/gitlab/-/issues/35412

[^2_15]: https://gitlab.com/gitlab-org/gitlab/-/issues/345678

[^2_16]: https://labs.etsi.org/rep/help/ci/environments/deployment_approvals.md

[^2_17]: https://gitlab.com/gitlab-org/gitlab/-/issues/328813



