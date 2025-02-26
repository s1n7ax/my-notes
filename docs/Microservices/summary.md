# Microservices

## Why Microservices

According to `Matt Ranney` from DoorDash,

The main reason to move to microservices is more so about deployment than development.
When you have a large engineering team, and large monolith app, deployment takes hours instead of minutes. More over, one bad change makes the entire release to rollback.

However, microservices moves pretty fast for some time. In the beginning, slow teams would not slow other teams down.

## Challenges of microcervices

- Over time, adding features become more difficult. One feature may require changes in multiple microservices and we have to figure out the order of release of each and once all done we have make sure all of them work together.

- Not so obvious errors. If another team complains about an error from our service, but we propagate the error due to another, we end up tagging most microservices to find the error
