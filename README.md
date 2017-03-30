# Big-data AWS CloudFormation Templates

These are AWS CloudFormation templates for various big-data and supporting applications. As with most things, you will likely want to customize these templates a bit to suit your needs. Some applications might be supported on EMR ([see the list](http://docs.aws.amazon.com/emr/latest/ReleaseGuide/emr-release-components.html#w1ab1c17c11)).

## Templates

### `initial.template`

This template creates a VPC along with the supporting subnets and routing tables. This template creates three public subnets - each one in a different availability zone of the `US-EAST-1` region. **The other templates build upon the resources defined in `initial.template` to configure their respective applications.** The goal of this approach is to let you provision only the applications that you need.

### `zookeeper.template`

This template creates and configures three ZooKeeper instances - one in each subnet. Once the configuration is complete ZooKeeper will be started on each instance.

### `kafka.template`

This template creates and configures an autoscaling group of Kafka instances across three subnets. This template requires both the `initial.template` and the `zookeeper.template` to have been successfully created because this template configures Kafka based on the ZooKeeper settings defined in `zookeeper.template`.

* The `logs.dir` property is set to `/var/kafka-logs` and this directory is located on a second EBS volume.
* The `broker.id` property for each Kafka instance is calculated based on the instance's IP. (This will be improved.)

### `nifi-standalone.template`

This template creates a single EC2 instance running NiFi as a system service. Once the stack has been successfully created you can access NiFi at http://public-ip:8080/nifi.

### `nifi.template`

This template creates a three node NiFi cluster with one instance per subset. Once the stack has been successfully created NiFi will be available at http://public-ip:8080/nifi.

### `zeppelin.template`

This template creates a single EC2 instance running Zeppelin. Once the stack has been successfully created you can access Zeppelin at http://public-ip:8080. Applications like Spark, Pig, and others can be install manually.
