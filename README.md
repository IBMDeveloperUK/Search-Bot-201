# search-bot-101
Build a chatbot to handle conversational search against a document base with Watson Discovery and Watson Assistant

A common scenario for chatbots, voice assistants, and agents to answer user questions from preconfigured "FAQ" responses, or produce search results from a set of documents and content relevant to the user's domain.

Think [Siri](https://www.apple.com/siri/), and its "here's what I found on the web - check it out!", but constrained to a private/custom document set.

+ [Architecture overview](#architecture)
+ [Get set up](#setup-and-preparation)
+ [Build a Discovery Assistant](#discovery-assistant)
+ [Chabot-enhanced Discovery Assistant](#discovery-chatbot)

# Architecture

![chatbot-architecture](/assets/chatbot-architecture.png)

# Setup and preparation

this workshop will exploit capabilities in the following technologies:
+ Node-RED - flow-based programming toll and environment
+ Watson Assistant - natural language dialog support
+ Watson Discovery - content/document query and retrieval

using [Red Hat OpenShift](https://www.openshift.com/) (through [Minishift](https://github.com/minishift/minishift)) as the Cloud Network component.

## Node-RED

[Node-RED](https://nodered.org) is an open-source rapid application development and deployment tool, based on [node.js](https://nodejs.org).

![node-red](/assets/node-red.png)

If you have yet had the pleasure of building applications with Node-RED, check out the [Node-RED introduction](https://github.com/watson-developer-cloud/node-red-labs/tree/master/introduction_to_node_red). This will give you the basic experience needed to build  Node-RED applications on any of its supported platforms.

## Watson Assistant

[Watson Assistant](https://www.ibm.com/cloud/watson-assistant/) is the IBM Cloud service for building chatbot conversation skills (intents, entities, dialogs)

![watson assistant](/assets/watson-assistant.png)

You can gain experience in defining skills through the [Watson Assistant 101 workshop](https://github.com/IBMDeveloperUK/Watson-Assistant-101). Labs 1,2 and 3 should be enough to get you comfortable with build a conversation skill and assistant. 

This workshop will use both conversation/dialog skills and search skills to process Discovery queries.

## Watson Discovery

[Watson Discovery](https://www.ibm.com/cloud/watson-discovery) is the IBM Cloud service for searching custom document repositories with natural langauge and structured queries.

![watson discovery](/assets/watson-discovery.png)

You provide a "corpus" of documents to be analysed and made searchable - through upload or by making available to a "crawler"; Watson Discovery "ingests" the documents, analysing them for entities (proper names, cities, countries, companies, etc), concepts, relations, and categories.

To get some experience with loading up a document corpus into Watson Discovery, and building queries into that corpus, take a look this tutorial:

[Discovery tutorial on Youtube](https://youtu.be/rlWvyV7vGc8 "Discovery")

## Openshift/Minishift

While the Watson Discovery and Assistant services require you to have an IBM Cloud account, the Node-RED application can be run on most platforms that support node.js, as long as there is connectivity to the service instances in the IBM Cloud.

If you would like to try running Node-RED as an OpenShift node.js application, you can setup a local 

![minishift](/assets/minishift.png)

To get the experience of using Openshift as a delivery platform, you can use the Minishift local installation - you'll find a lightweight introduction to this at [Minishift 101](https://github.com/IBMDeveloperUK/minishift101)

# Discovery Assistant

The following tutorial shows how to set up a Search Assistant using a combination of a dialog skill and a search skill.

**Note:** The use of search skills requires that your Watson Assistant service instance be either upgraded to the Plus plan, or enabled for the free Plus plan 30-day trail.

![plus-plan-trial](/assets/plus-plan-trial.png)

[create a search assistant](https://cloud.ibm.com/docs/services/assistant?topic=assistant-skill-search-add)

