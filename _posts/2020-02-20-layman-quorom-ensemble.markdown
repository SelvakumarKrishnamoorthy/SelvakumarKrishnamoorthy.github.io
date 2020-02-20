---
layout: post
title:  "Layman Terms : Quorom vs Ensemble"
date:   2020-02-20 02:53:47 +0530
categories: jekyll update
---

**Ensemble** is an array of nodes (or servers, if you like) that form your Distributed Computer Ecosystem.

**Quorum** is when things get interesting. On a specific assignment/job, Quorum ensures that a healthy leader-follower majority can be maintained. In other words, a conduct which ensures that majority vote can be obtained to proceed with an activity (e.g. commit/update/delete etc.). In Replication strategy, quorum is a must to have.

## Beautiful Example to explain Quorom and Ensemble:

1) In your company - there is a board formed by 5 directors (ensemble).
|d1, d2, d3, d4, d5|----- BoD

2) Each director has equal say in each decision. But a majority if 3 directors at anytime should agree on a project. If no majority is there, the company will be dysfunctional.

3) One a particular project, P1 - they randomly voted to have a majority of d1,d2,d3 to be decision makers in the project. but d4 and d5 are fully aware of what's going on (so that they can step in anytime).

4) Now (God forbid), d3 passes away after a few months, again everyone agrees that the majority will be formed using d1,d2,d4. d5 is still aware of what's going on. NOte that we only have 4 directors left.

5) Disaster strikes again. d5 leaves the company for another competitor. But that doesn't change anything because the company is still functional with a 3-member BoD.

6) At any point of another disaster strikes the BoD and any of the directors become "unavailable" - company is dysfunctional i.e. we have lost the quorum forming criterion.

**Zookeeper uses ceil(N/2) - 1** formula to get the maximum number of failures allowed for an Ensemble and maintain a stable quorum. In this case, the minimum recommended ensemble nodes are 3 (tolerates 1 failure maximum).
