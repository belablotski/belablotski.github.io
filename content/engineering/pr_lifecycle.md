+++
date = '2025-01-18T22:19:12-08:00'
draft = false
title = 'PR lifecycle'
+++

## PR lifecycle

In our group we follow simple yet effetive PR workflow: poly-repo setup with a simplified GitHub process. Basically we use `main` branch with automatic staging deployment and ability to promote a build to the production environment. The promotion script automatically creates a CRQ (a change record in ServiceNow), that we call "auto-CRQ" since it doesn't requite manual steps (approvals), unless the site status is not green.
<!--more-->

The key to success here is a GitHub PR lifecycle closely integrated with JIRA stories and ServiceNow CRQ records to ensure a smooth development and deployment process. When a developer starts working on a new feature or bug fix, they open a JIRA story, which has all the requirements and it will be used to track the progress as well. As they make changes, they commit and push their code, eventually opening a pull request (PR) on GitHub. The PR undergoes a review process where team members (at least 2 - the commonly accepted practice) provide feedback and request changes if necessary. Once the PR is approved and merged, the JIRA story is updated to reflect the completion of the task. For deployment, a ServiceNow CRQ record is created to manage the change request, ensuring that all necessary approvals and checks are in place before the code is deployed to production.

There are four different entities envolved in the process:
1. Code Commit
2. Pull Request
3. JIRA Ticket (typically story, but it doesn't really matter)
4. ServiceNow change record (aka CRQ)

The entire development process is described on the diagram below.

```goat
                                            o start                           o unexpected change
                                            |                                 |
                                            |                                 v                                  
                                            |                                 .                                
     .----------------.                     |                                / \                               
  .->| lines of code  |<----------.         |                               /   \                                       
  |  '-------+--------'           |         |JIRA status:                  /     \                                      
  |          |                    |start    |"in progress"                /context\ y           .-----------.                    
  |          |git add/commit      |building |                            + changed +----------->| closed PR +--.
  |          v                    |         v                             \   ?   /             '-----+-----'  |                        
  |  .---------------.        .---+------------.    stausu: "done"         \     /                    |        |
  |  |     commit    |       |    JIRA Story    o--------------------.      \   /         resolution: |        | 
  |  '-------+-------'        '---o--------o---'                     |       \ /           "won't do" |        |
  |          |                    |        |  status: "in review"    |        .   "works as designed" |        |
  |          |git push            |        +---------------------+   '----------------------+---------+        |
  |          v                    |                              |                          |                  |
  |          .               link |                          .---+-----.                    | resolution:      |
  |         / \              .----'                      .-->| open PR +---.                | "done"           v
  |        /   \             |                           |   '---------'   |                |       .--------->* end
  |       /     \            |                           |                 |            .---+----.  |          ^
  |      /  1st  \  y   .----+-----.           .         |                 .           | Auto CRQ +-'          |
  |     .         +---->| draft PR |          / \        |remove          / \           '---+----'    .        |
  |      \commit?/      '----+-----'         /   \       |draft          /   \              ^        / \       |
  |       \     /            |              /     \      |              /     \             |       /   \      |
  |        \   /             |             /       \     |             /       \            |      /     \     |
  |         \ /              v            /  ready  \  y |         y  / changes \  n        |  y  /       \  n |
  |          .               o---------->.    for    .---'       .---. requested .---.      '----+ deploy? +---'
  |          | n             ^            \ review? /            |    \    ?    /    |            \       /
  |          |               |             \       /             |     \       /     |             \     /
  |          '---------------'              \     /              |      \     /      |merge         \   /             
  |                                          \   /               |       \   /       |               \ /
  |                                           \ /                '---.    \ /    .---'                .  
  |                                            .                     |     .     |                    |                   
  |                                          n |                     |           |    .-----------.   |             
  |           continue building                v    address comments |           '--->| merged PR +---'                
  '--------------------------------------------o<--------------------'                '-----------'                    
```

1. **Commit the Code**: Start with the problem description in JIRA, generate some code and commit it when you have some logically completed part. Push code to the repo as often as you can.
1. **Open a PR**: Create a new pull request in Draft status from your feature branch to the main branch.
1. **Review**: Remove the Draft status from your PR and request reviews from your team members. They will review the code and leave comments or approve the changes. The JIRA ticket should be moved to "in-review" stage as well.
1. **Address Comments**: Make necessary changes based on the feedback received during the review.
1. **Approval**: Once all reviewers have approved the PR, it is ready to be merged.
1. **Merge**: Merge the PR into the main branch. Ensure all checks have passed before merging. The build will be deployed in the staging environment automatically.
1. **Deploy in Prod**: Initiate the deployment process, a ServiceNow change record will be created automatically. Validate the new functionality in production, demo it to the group and close the JIRA ticket.
