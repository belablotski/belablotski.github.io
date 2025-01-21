+++
date = '2025-01-18T22:19:12-08:00'
draft = true
title = 'PR lifecycle'
+++

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

link to JIRA
external world changed - abandone


https://github.com/bep/goat?tab=readme-ov-file

    hard_work --> commit
    commit --> draft_pr
    draft_pr --> incremental_commits
    incremental_commits --> review_pr
    review_pr --> comments
    comments --> merge_pr
    merge_pr --> deploy

    hard_work[Hard Work]
    commit[Submit Logical Completed Unit of Work as a Commit]
    draft_pr[Open Draft PR on the First Commit]
    incremental_commits[Complete the Work Pushing the Incremental Units of Work as Commits]
    review_pr[Open PR for the Review]
    comments[Work on Comments from the Reviewers]
    merge_pr[Merge the PR]
    deploy[Deploy]
```