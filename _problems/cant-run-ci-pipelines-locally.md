---
slug: cant-run-ci-pipelines-locally
title: "CI pipelines can't be run locally — debugging means pushing 'fix' commits and waiting for the runner"
who: "software engineers and DevOps/platform engineers maintaining CI/CD"
vertical: dev-tools
summary: "The commit-push-wait-for-CI-to-fail loop is a recurring productivity drain: the CI environment can't be reproduced locally, so debugging a pipeline means dozens of throwaway commits pushed just to see if the runner passes. Emulators like nektos/act exist for GitHub Actions, but users report breakage on secrets, environment variables, workload identity federation, and CPU-architecture mismatches. For GitLab, native local pipeline execution has been one of the most-upvoted open feature requests for nearly a decade."
evidence:
  - url: "https://news.ycombinator.com/item?id=33750654"
    source: "Hacker News"
    date: "2022-11"
    note: "'Act: Run your GitHub Actions locally' — commenters describe pushing 'fix' commits repeatedly until the pipeline works"
  - url: "https://news.ycombinator.com/item?id=44003184"
    source: "Hacker News"
    date: "2025-05"
    note: "Same pain three years later; commenters cite secrets, workload identity federation, and Apple-Silicon-vs-runner mismatches that keep act from reproducing CI failures"
  - url: "https://gitlab.com/gitlab-org/gitlab-runner/-/issues/2797"
    source: "GitLab issue (gitlab-runner)"
    date: "2017-09"
    note: "'Local pipeline execution' — heavily-upvoted feature request, originally marked 'Won't do', still open with status updates through 2026"
current_workarounds: "nektos/act to emulate GitHub Actions locally (frequent breakage on secrets, permissions, architecture); wrapping CI logic in a Makefile so the same steps run locally and in CI; the deprecated gitlab-runner exec and third-party gitlab-ci-local; most commonly, pushing throwaway commits and waiting on the hosted runner."
why_unsolved: "CI runs depend on runner images, injected secrets, OIDC federation, and cloud permissions that can't be faithfully reproduced on a laptop — emulators diverge exactly where failures happen. GitLab treated true local execution as out of scope for years, and GitHub Actions has no first-party local runner."
signals:
  - "379 and 273 points on the two Hacker News threads, three years apart (observed 2026-07)"
  - "396 upvotes / 196 comments on the GitLab issue, open since 2017 (observed 2026-07 via GitLab API)"
status: curated
date_curated: 2026-07-24
---
