# Multicloud and multiservice] infrastructure

## Why

We need to build high-reliable and high-trhoutput infrastructure based on hybrid multicloud network.
Right now we have a lot of legacy code/solutions and don't want to support/develop them anymore.

## Key principles

### Infrastructure as a Service

#### Dependent blocks

All infra is a set of (in)dependent blocks.
On update of the one block all dependent blocks may be updated.

#### Self-management for each team/person

Each team may update his own blocks. All nested blocks will be updated automatically (if required) after tests.

### Automation

#### git repository(ies) is the source of truth for all changes

The changes in repo with webhook produce action test/update of infra according to dependency and scenarios

#### Changes in prod only after automated tests

Each block must have described conditions for monitoring and health-checks.

* [(no)chef](docs/NoChef.md)
* [provisioning](docs/provisioning.md)

### links

* [Site Reliability Engineering Principles](https://medium.com/@alexbmeng/site-reliability-engineering-principals-fd52229bfcd6)
