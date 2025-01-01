# Types of Actions

## Summary

- container actions
- JavaScript actions
- composite actions

## Content

### Container Actions

With container actions, the environment is part of the action's code. These
actions can only be run in a Linux environment that GitHub hosts. Container
actions support many different languages.

### JavaScript Actions

JavaScript actions don't include the environment in the code. You'll have to
specify the environment to execute these actions. You can run these actions in a
VM in the cloud or on-premises. JavaScript actions support Linux, macOS, and
Windows environments.

### Composite Actions

Composite actions allow you to combine multiple workflow steps within one
action. For example, you can use this feature to bundle together multiple run
commands into an action, and then have a workflow that executes the bundled
commands as a single step using that action.
