+++
date = '2025-01-18T22:19:12-08:00'
draft = true
title = 'PR lifecycle'
+++

```goat
     .----------------.
  .->| lines of code  |
  |  '-------+--------'
  |          |
  |          |add/commit
  |          v
  |  .---------------.
  |  |     commit    |
  |  '-------+-------'
  |          |
  |          |push
  |          v
  |          .               .----------.
  |         / \         .--->| draft PR +------.
  |        /   \        |    '----------'      |
  |       /     \      open                    v
  |      / 1st   \  y   |                      .
  |     .         +-----'                     / \         
  |      \commit /                           /   \          
  |       \     /                           /     \         
  |        \   /                           /       \         
  |         \ /                           /  ready  \        
  |          .               .---------->.    for    .
  |          | n             |            \ review? /        
  |          |               |             \       /        
  |          '---------------'              \     /        
  |                                          \   /           
  |                                           \ /           
  |                                            .      
  |                   build                  n |
  '--------------------------------------------'

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