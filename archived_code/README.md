# Archived code

## Context

We wanted to update the plugin to the latest upstream version and decided to create a new fork instead of rebasing. To make the fork easier to maintain, and since some custom features are now available out of the box (`jenkins.job.pause_duration` and `jenkins.job.build_duration`), we decided to remove most of our custom code. We're only keeping `jenkins.computer.bootstrap` / `jenkins.agent.bootstrap` for now.

For archive purposes and in case we want to pick the `BuildGraphWalker` work again, we're keeping our changes in this directory.

## Notes from the old readme

Scout24 specific:

    Why do we have our own fork?
        We historically added feature that weren't there in the upstream datadog plugin. This started out as https://github.com/scout24/fizz-metrics-plugin, but eventually converged again with the upstream plugin, so now we are only a couple patches off the mainline.
    What's added?
        Agent bootstrap time, emitted as jenkins.computer.bootstrap / jenkins.agent.bootstrap - both names since "computer" is the new official wording for all things regarding build nodes in the datadog plugin, but we used "agent" earlier and its used on dashboards.
        We attempted to add pause/checkout and pure build durations (without pauses) as jenkins.job.checkoutduration, jenkins.job.pauseduration and jenkins.job.buildduration. The values may currently be inaccurate with nested builds graphs (parallel stages within the pipeline etc.).
        A BuildGraphWalker was created ( https://github.com/Scout24/datadog-plugin/blob/master/src/main/java/org/datadog/jenkins/plugins/datadog/DatadogBuildGraphWalker.java ) as an attempt to gain more accurate insights to the individual durations of a build. It's not called in any code path yet - so we are free to extend it and add it to the DatadogBuildListener once we see it producing good results in the unit tests.


