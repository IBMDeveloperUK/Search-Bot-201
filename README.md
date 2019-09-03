# search-bot-101
Build a chatbot to handle conversational search against a document base with Watson Discovery and Watson Assistant

A common scenario for chatbots, voice assistants, and agents to answer user questions from preconfigured "FAQ" responses, or produce search results from a set of documents and content relevant to the user's domain.

Think [Siri](https://www.apple.com/siri/), and its "here's what I found on the web - check it out!", but constrained to a private/custom document set.

# setup

this workshop will exploit capabilities in the following technologies:
+ Node-RED - flow-based programming toll and environment
+ Watson Assistant - natural language dialog support
+ Watson Discovery - content/document query and retrieval

and optionally, [Red Hat OpenShift](https://www.openshift.com/) (through [Minishift](https://github.com/minishift/minishift))

# architecture

![chatbot-architecture](/assets/chatbot-architecture.png)

## Node-RED

[Node-RED](https://nodered.org) is an open-source rapid application development and deployment tool, based on [node.js](https://nodejs.org).

![node-red](/assets/node-red.png)

If you have yet had the pleasure of building applications with Node-RED, check out the [Node-RED 101 workshop](https://github.com/IBMDeveloperUK/Node-RED-Watson-101)

## Watson Assistant

[Watson Assistant](https://www.ibm.com/cloud/watson-assistant/) is the IBM Cloud service for building chatbot conversation skills (intents, entities, dialogs)

![watson assistant](/assets/watson-assistant.png)

You can gain experience in defining skills through the [Watson Assistant 101 workshop](https://github.com/IBMDeveloperUK/Watson-Assistant-101)

## Watson Discovery

[Watson Discovery](https://www.ibm.com/cloud/watson-discovery) is the IBM Cloud service for searching custom document repositories with natural langauge and structured queries.

![watson discovery](/assets/watson-discovery.png)

You provide a "corpus" of documents to be analysed and made searchable - through upload or by making available to a "crawler"; Watson Discovery "ingests" the documents, analysing them for entities (proper names, cities, countries, companies, etc), concepts, relations, and categories.

## Openshift/Minishift

While the Watson Discovery and Assistant services require you to have an IBM Cloud account, the Node-RED application can be run on most platforms that support node.js, as long as there is connectivity to the service instances in the IBM Cloud.

![minishift](/assets/minishift.png)

To get the experience of using Openshift as a delivery platform, you can use the Minishift local installation - you'll find a lightweight introduction to this at [Minishift 101](https://github.com/IBMDeveloperUK/minishift101)
