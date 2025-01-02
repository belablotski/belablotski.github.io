+++
date = '2024-12-31T19:19:12-08:00'
draft = true
title = 'Team Productivity Metrics'
+++

https://dora.dev/#reports

Hugo behind the website https://github.com/dora-team/dora.dev/blob/main/hugo/config.toml
https://github.com/dora-team/dora.dev/tree/main


DORA Metrics
    1. Deploy frequency
    2. Development Cycle Time (in-progress, review, merge, deploy)
    3. Change Failure Rate
    4. Mean Time to Restore

Plan:
    1. Epic Lead Time
    2. Cycle Time
    3. Stories and Tasks In Progress
    4. Velocity Trend
    5. Unplanned Work (%)
    6. Sprint Completion Rate (%)
    7. Sprints Ready
    8. Sprint Velocity
    9. Sprint Acceptance Criteria Rate (%)

Code Metrics
    1. PR Cycle Time
    2. PR Review Time
    3. PR Review Depth (Review depth measures the average number of comments per pull request review.)
    4. PR Size
    5. PRs In Progress
    6. PR Merge Frequency

Build
    1. Build Success Rate
    2. Top Failed Jobs
    3. PR Build Success Rate
    4. Top Failed PR Jobs
    5. Avg Build Duration
    6. Avg PR Build Duration
    7. Avg Builds per PR

Deploy:
    1. Deploy Frequency
    2. Development Cycle Time
    3. Change Failure Rate
    4. Deploy Time

Quality Metrics
    1. Production Defect Arrival Rate
    2. Sonar Violations
    3. Automated Code Coverage
    4. Sonar Violations (Blocker)
    5. Container Security Vulnerabilities

Operate Metrics
    1. Major Incidents (Critical, High, Medium)
    2. Mean Time to Restore for Major Incidents (Critical, High, Medium)
    3. Non-Major Incidents (Critical, High, Medium)
Mean Time to Restore for Non-Major Incidents (Critical, High, Medium)


See also:
1. https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests


```
gh auth login

gh search commits '' --repo belablotski/belablotski.github.io --author belablotski --sort author-date --limit 10
```