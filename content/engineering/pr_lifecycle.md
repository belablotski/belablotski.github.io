+++
date = '2025-01-18T22:19:12-08:00'
draft = true
title = 'PR lifecycle'
+++

## GitHub PR lifecycle

The GitHub PR lifecycle is closely integrated with JIRA stories and ServiceNow CRQ records to ensure a smooth development and deployment process. When a developer starts working on a new feature or bug fix, they create a JIRA story to track the progress. As they make changes, they commit and push their code, eventually opening a pull request (PR) on GitHub. The PR undergoes a review process where team members provide feedback and request changes if necessary. Once the PR is approved and merged, the JIRA story is updated to reflect the completion of the task. For deployment, a ServiceNow CRQ record is created to manage the change request, ensuring that all necessary approvals and checks are in place before the code is deployed to production.

1. **Open a PR**: Create a new pull request from your feature branch to the main branch.
2. **Review**: Request reviews from your team members. They will review the code and leave comments or approve the changes.
3. **Address Comments**: Make necessary changes based on the feedback received during the review.
4. **Approval**: Once all reviewers have approved the PR, it is ready to be merged.
5. **Merge**: Merge the PR into the main branch. Ensure all checks have passed before merging.
6. **Close**: After merging, close the PR if it does not close automatically.
7. **Delete Branch**: Optionally, delete the feature branch to keep the repository clean.

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

## PR lifecycle

