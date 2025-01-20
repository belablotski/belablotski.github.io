+++
date = '2025-01-18T22:19:12-08:00'
draft = true
title = 'PR lifecycle'
+++

```goat
     .----------------.
  .->| lines of code  |<----------.         o start
  |  '-------+--------'           |         |
  |          |                    |start    |
  |          |add/commit          |building |
  |          v                    |         v
  |  .---------------.        .---+------------.
  |  |     commit    |       |    JIRA Story    |
  |  '-------+-------'        '----------------'
  |          |                    ^
  |          |push                |link
  |          v                    |
  |          .               .----+-----.                    .---------.                 .-----------.
  |         / \         .--->| draft PR +------.         .-->| open PR +---.         .-->| merged PR | 
  |        /   \        |    '----------'      |         |   '---------'   |         |   '-----------'
  |       /     \       |open                  v         |                 v         |
  |      /  1st  \  y   |                      .         |                 .         |
  |     .         +-----'                     / \        |remove          / \        |merge
  |      \commit?/                           /   \       |draft          /   \       |
  |       \     /                           /     \      |              /     \      |
  |        \   /                           /       \     |             /       \     |
  |         \ /                           /  ready  \  y |         y  / changes \    |
  |          .               .---------->.    for    .---'       .---. requested .---'
  |          | n             |            \ review? /            |    \    ?    /
  |          |               |             \       /             |     \       /
  |          '---------------'              \     /              |      \     /
  |                                          \   /               |       \   /
  |                                           \ /                '---.    \ /
  |                                            .                     |     .
  |           continue building              n |    address comments |
  '--------------------------------------------'<--------------------'

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