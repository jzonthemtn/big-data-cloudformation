# Big-data AWS CloudFormation Templates

These are AWS CloudFormation templates for various big-data and supporting applications. As with most things, you will likely want to customize these templates a bit to suit your needs.

## Templates

### `initial.template`

This template creates a VPC along with the supporting subnets and routing tables. This template creates three public subnets - each one in a different availability zone of the `US-EAST-1` region. **The other templates build upon the resources defined in `initial.template` to configure their respective applications.** The goal of this approach is to let you provision only the applications that you need.

### `zookeeper.template`

This template creates and configures three ZooKeeper instances - one in each subnet. Once the configuration is complete ZooKeeper will be started on each instance.

### `kafka.template`

This template creates and configures three Kafka instances - one in each subnet. This template requires both the `initial.template` and the `zookeeper.template` to have been successfully created because this template configures Kafka based on the ZooKeeper settings defined in `zookeeper.template`.

The `broker.id` property for each Kafka instance will be set to the EC2 instance ID.

### `nifi-standalone.template`

This template creates a single EC2 instance running NiFi as a system service.
