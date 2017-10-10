# dslink-java-v2-servicebus

* Version: 1.0.0.0
* Java - version 1.6 and up.
* [Apache License 2.0](http://www.apache.org/licenses/LICENSE-2.0)


## Overview

This is a link for sending and receiving messages through Microsoft Azure Service Bus.

If you are not familiar with DSA and links, an overview can be found at
[here](http://iot-dsa.org/get-started/how-dsa-works).

This link was built using the DSLink Java SDK which can be found
[here](https://github.com/iot-dsa-v2/sdk-dslink-java-v2).


## Link Architecture

This section outlines the hierarchy of nodes defined by this link.

- _RootNode_ - The root node of the link, has an action to add a Service Bus namespace to the view.
  - _ServiceBusNode_ - A node representing a specific Service Bus namespace, with actions to create new Queues and Topics, and add existing ones to the view.
    -_Queues_- - Serves as the container for Queue nodes.
      -_QueueNode_- -Represents a specific Queue in the Service Bus. Has actions to send/receive messages to/from the Queue.
    -_Topics_- - Serves as the container for Topic nodes .
      -_TopicNode_- -Represents a specific Topic in the Service Bus. Has actions to send messages to the Topic and add/create Subscriptions for the Topic.
        -_SubscriptionNode_- Represents a specific Subscription for the Topic. Has action to read messages from the Subscription.


## Node Guide

The following section provides detailed descriptions of each node in the link as well as
descriptions of actions, values and child nodes.


### RootNode

This is the root node of the link.

**Actions**
- Add Service Bus - Connect to a Service Bus Namespace and add a child _ServiceBusNode_ to represent it. 

**Child Nodes**
 - any _ServiceBusNode_s that have been added.

### ServiceBusNode

This node represents a specific Azure Service Bus Namespace.

**Actions**
- Remove - Remove this node.
- Refresh - Retry connecting to the Service Bus, and update the drop-down lists of available Queues and Topics.
- Edit - Change some of the connection settings and try to connect again.
- Create Queue - Create a new Service Bus Queue and a a child _QueueNode_ to represent it.
- Create Topic - Create a new Service Bus Topic and a a child _TopicNode_ to represent it.
- Add Queue - Choose a Queue that already exists in the namespace from the drop-down and add a child _QueueNode_ to represent it.
- Add Topic - Choose a Topic that already exists in the namespace from the drop-down and add a child _TopicNode_ to represent it.

**Values**
- STATUS - Whether or not we successfully connected to the Service Bus.

**Child Nodes**
- Queues - All _QueueNode_s added by the above actions will be children of this node.
- Topics - All _TopicNode_s added by the above actions will be children of this node.

### QueueNode

This node represents a specific Azure Service Bus Queue.

**Actions**
- Remove - Remove this node. If _Delete From Namespace_, also delete the Queue it represents from its Service Bus namespace.
- Receive Messages - Open a streaming table to read messages from the Queue.
- Send Message - Send a message to the Queue.

### TopicNode

This node represents a specific Azure Service Bus Topic.

**Actions**
- Remove - Remove this node. If _Delete From Namespace_, also delete the Topic it represents from its Service Bus namespace.
- Refresh - Update the drop-down list of available Subscriptions.
- Send Message - Send a message to the Topic.
- Create Subscription - Create a new Subscription to this topic and a a child _SubscriptionNode_ to represent it.
- Add Subscription - Choose a Subscription that already exists in the namespace from the drop-down and add a child _SubscriptionNode_ to represent it.

**Child Nodes**
 - any _SubscriptionNode_s that have been added.
 
### SubscriptionNode

This node represents a specific Subscription for an Azure Service Bus Topic.

**Actions**
- Remove - Remove this node. If _Delete From Namespace_, also delete the Subscription it represents from its Service Bus namespace.
- Receive Messages - Open a streaming table to read messages from the Subscription.


## Acknowledgements

SDK-DSLINK-JAVA

This software contains unmodified binary redistributions of 
[sdk-dslink-java-v2](https://github.com/iot-dsa-v2/sdk-dslink-java-v2), which is licensed 
and available under the Apache License 2.0. An original copy of the license agreement can be found 
at https://github.com/iot-dsa-v2/sdk-dslink-java-v2/blob/master/LICENSE

## History

* Version 1.0.0.0
  - Hello World

