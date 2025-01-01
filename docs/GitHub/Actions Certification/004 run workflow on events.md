# Run on events

## Summary

[events-that-trigger-workflows](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)
are the available workflow events in GitHub

- How to specify the event to run in workflow
  - `on` action
  - on a list of actions
  - on event-configuration map
    - run on schedules
    - restricts the execution of a workflow to specific files, tags, or branch
      changes

## Content

### how to Specify the Event to Run in Workflow

- In following example, the workflow will run on push action

```yml
name: A workflow for my Hello World file
on: push
```

- In following, we can pass a list of events to trigger the workflow. As a
  result, any one of these events will trigger the workflow

```yml
on: [push, pull_request]
```

- In following, `on` is a type of `event-configuration` map. Here, we can
  schedule, or add extra constraints to the workflow that should be met before
  running the workflow.

```yml
on:
  # Trigger the workflow on push or pull request,
  # but only for the main branch
  push:
    branches:
      - main
  pull_request:
    branches:
      - main
  # Also trigger on page_build, as well as release created events
  page_build:
  release:
    types:
      - created
```
