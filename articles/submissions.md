---
title: Submission
layout: article
excerpt: Explore the features of submissions made to evaluation queues
category: howto
---

<style>
#image {
    width: 50%;
}
</style>

Every submission you make to an Evaluation queue has a unique id.  This id should not be confused with Synapse ids which start with `syn...`.  All submissions have a `Submission` and `SubmissionStatus` object.  Annotations can be added to a `SubmissionStatus` to be displayed on leaderboards.  Each of these added annotations can be set to either public or private.  Private annotations cannot be read by people on the a leaderboard unless the Team or Synapse user has `Can Score` or `Admin` permissions on the evaluation queue.  Public annotations can be viewed by any Team or user that at least has `Can View` permissions.  See more about [evaluation queues](evaluation_queues.md).
