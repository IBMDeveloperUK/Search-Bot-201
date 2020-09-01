# Search-Bot-201 - enhancing your Watson Chatbot with Discovery

http://ibm.biz/chatbot_discover


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
+ Node-RED - flow-based programming tool and environment
+ Watson Assistant - natural language dialog support
+ Watson Discovery - content/document query and retrieval

You *will* need a IBM Cloud account [sign up here](http://ibm.biz/chatbot_discover) - **initially free**, but you're welcome to upgrade to "Pay As You Go"

Node-RED will be used to create custom front-ends, and additional integration options, and can be deployed using a choice of:
1. IBM Cloud [Node-RED Starter application](https://developer.ibm.com/components/node-red/tutorials/how-to-create-a-node-red-starter-application/)
1. [Red Hat OpenShift](https://www.openshift.com/) (through [Minishift](https://github.com/minishift/minishift)) as the Cloud Network component.
1. Locally installed Node-RED

## Node-RED

[Node-RED](https://nodered.org) is an open-source rapid application development and deployment tool, based on [node.js](https://nodejs.org).

![node-red](/assets/node-red.png)

If you have not yet had the pleasure of building applications with Node-RED, check out

**Tutorial:** [Node-RED introduction](https://github.com/watson-developer-cloud/node-red-labs/tree/master/introduction_to_node_red). 

This will give you the basic experience needed to build  Node-RED applications on any of its supported platforms.

## Watson Assistant

[Watson Assistant](https://www.ibm.com/cloud/watson-assistant/) is the IBM Cloud service for building chatbot conversation skills (intents, entities, dialogs)

![watson assistant](/assets/watson-assistant.png)

You can gain experience in defining skills through

**Tutorial:** [Watson Assistant 101 workshop](https://github.com/IBMDeveloperUK/Watson-Assistant-101). 

Labs 1,2 and 3 should be enough to get you comfortable with build a conversation skill and assistant. 

This workshop will use both conversation/dialog skills and search skills to process Discovery queries.

## Watson Discovery

[Watson Discovery](https://www.ibm.com/cloud/watson-discovery) is the IBM Cloud service for searching custom document repositories with natural langauge and structured queries.

![watson discovery](/assets/watson-discovery.png)

You provide a "corpus" of documents to be analysed and made searchable - through upload or by making available to a "crawler"; Watson Discovery "ingests" the documents, analysing them for entities (proper names, cities, countries, companies, etc), concepts, relations, and categories.

To get some experience with loading up a document corpus into Watson Discovery, and building queries into that corpus, take a look this tutorial:

**Tutorial:** [Discovery tutorial on Youtube](https://youtu.be/rlWvyV7vGc8 "Discovery")

<details><summary>
	<b>Openshift/Minishift deployment option</b>
	</summary>
<!-- VVVVVVVVVVVVV -->
While the Watson Discovery and Assistant services require you to have an IBM Cloud account, the Node-RED application can be run on most platforms that support node.js, as long as there is connectivity to the service instances in the IBM Cloud.

If you would like to try running Node-RED as an OpenShift node.js application, you can setup a local 

![minishift](/assets/minishift.png)

To get the experience of using Openshift as a delivery platform, you can use the Minishift local installation - you'll find a lightweight introduction to this at 

**Tutorial:** [Minishift 101](https://github.com/IBMDeveloperUK/minishift101)

## Launching Node-RED in Minishift

If you have working Minishift environment, you can deploy Node-RED into the cluster using the steps in this workshop:

[Node-RED starter](https://github.com/IBMDeveloperUK/node-red-workshop-starter)
<!-- AAAAAAAAAAAAAA -->
</details>

# Discovery Assistant

For this workshop, because we all need (and want) to know about **General Data Protection Regulation**, we will create:
1. Watson Dialog Skill to guide the user conversation -- based on an example [GDPR Advisor bot](https://github.com/IBM/bots/tree/master/bots/gdpr_advisor)
1. Watson Discovery data collection, using a website crawler -- based on the UK Information Commisioner's Office 
[GDPR Guide](https://ico.org.uk/for-organisations/guide-to-data-protection/guide-to-the-general-data-protection-regulation-gdpr/)
1. Watson Search Skill which references the Discovery collection, making it searchable by Watson Assistant
1. Watson Assistant instance that combines the Dialog and Search skills to produce an enhanced information service

**Note:** The use of search skills requires that your Watson Assistant service instance be either upgraded to the Plus plan, or enabled for the free Plus plan 30-day trail.

![plus-plan-trial](/assets/plus-plan-trial.png)

The following tutorial shows how to set up a Search Assistant using a combination of a dialog skill and a search skill.

**Tutorial:** [create a Watson Search Assistant](https://cloud.ibm.com/docs/services/assistant?topic=assistant-skill-search-add)

The standalone web integration of the Dialog skill and the Search skill should look something like this:
![standalone integrated search](/assets/watson-assistant-search-standalone.png)

# Discovery Chatbot

Once you have a Watson Discovery instance, and a Watson Assistant service, and can demonstrate interacting with the bot through the default web preview link, you can build a chatbot application to manage the flow of interactions and information presentation between the user and the Watson Assistant service.

This is where Node-RED can be used to rapidly build a user interface, and logic flow.

![node-red-flow](/assets/node-red-flow.png)

This flow can be created by importing the following json into the Node-RED editor:

<details>
	<summary><b>Node-red-flow json source</b></summary>
	
```
[{
	"id": "d4c8a74c.53eef8",
	"type": "tab",
	"label": "Flow 1",
	"disabled": false,
	"info": ""
}, {
	"id": "8a30be24.3d5ec",
	"type": "http in",
	"z": "d4c8a74c.53eef8",
	"name": "",
	"url": "/chat",
	"method": "post",
	"upload": false,
	"swaggerDoc": "",
	"x": 130,
	"y": 100,
	"wires": [
		["7815d1ec.001188", "fa83fdaa.695de8"]
	]
}, {
	"id": "7815d1ec.001188",
	"type": "change",
	"z": "d4c8a74c.53eef8",
	"name": "history-in",
	"rules": [{
		"t": "set",
		"p": "payload",
		"pt": "msg",
		"to": "req.body.in",
		"tot": "msg"
	}, {
		"t": "set",
		"p": "history",
		"pt": "msg",
		"to": "  \"<div style='color:green;'>\" \t& payload\t& \"</div>\"\t& req.body.history\t",
		"tot": "jsonata"
	}],
	"action": "",
	"property": "",
	"from": "",
	"to": "",
	"reg": false,
	"x": 320,
	"y": 100,
	"wires": [
		["ee68544a.99a7c8"]
	]
}, {
	"id": "fa83fdaa.695de8",
	"type": "debug",
	"z": "d4c8a74c.53eef8",
	"name": "",
	"active": false,
	"tosidebar": true,
	"console": false,
	"tostatus": false,
	"complete": "true",
	"x": 310,
	"y": 220,
	"wires": []
}, {
	"id": "8048a2d4.cbf33",
	"type": "http in",
	"z": "d4c8a74c.53eef8",
	"name": "",
	"url": "/chat",
	"method": "get",
	"upload": false,
	"swaggerDoc": "",
	"x": 120,
	"y": 300,
	"wires": [
		["647ed860.2859f", "fa83fdaa.695de8"]
	]
}, {
	"id": "24251ccf.8cb444",
	"type": "inject",
	"z": "d4c8a74c.53eef8",
	"name": "",
	"topic": "",
	"payload": "hello",
	"payloadType": "str",
	"repeat": "",
	"crontab": "",
	"once": false,
	"onceDelay": 0.1,
	"x": 330,
	"y": 160,
	"wires": [
		["ee68544a.99a7c8"]
	]
}, {
	"id": "c0cbb01.d83a1d",
	"type": "debug",
	"z": "d4c8a74c.53eef8",
	"name": "",
	"active": true,
	"tosidebar": true,
	"console": false,
	"tostatus": false,
	"complete": "true",
	"x": 930,
	"y": 100,
	"wires": []
}, {
	"id": "a2b4be3c.ecb018",
	"type": "template",
	"z": "d4c8a74c.53eef8",
	"name": "dialog",
	"field": "payload",
	"fieldType": "msg",
	"format": "handlebars",
	"syntax": "mustache",
	"template": "{{#payload}}\n  {{#output}}\n    {{#generic}}\n    {{text}}\n    {{/generic}}\n  {{/output}}\n{{/payload}}",
	"output": "str",
	"x": 690,
	"y": 140,
	"wires": [
		["dae785b.579ddf8"]
	]
}, {
	"id": "647ed860.2859f",
	"type": "template",
	"z": "d4c8a74c.53eef8",
	"name": "dialog/form",
	"field": "payload",
	"fieldType": "msg",
	"format": "handlebars",
	"syntax": "mustache",
	"template": "<h1>chatting with Watson</h1>\n\n<form method=POST>\n    <input type=text name=in><input type=submit>\n    <input type=text name=history hidden value=\"{{{history}}}\">\n</form>\n<div>\n    {{{history}}}\n</div>",
	"output": "str",
	"x": 790,
	"y": 300,
	"wires": [
		["aab49b0b.b783d8"]
	]
}, {
	"id": "dae785b.579ddf8",
	"type": "change",
	"z": "d4c8a74c.53eef8",
	"name": "history-out",
	"rules": [{
		"t": "set",
		"p": "history",
		"pt": "msg",
		"to": "  \"<div style='color:red;'>\" \t& payload\t& \"</div>\"\t& history\t",
		"tot": "jsonata"
	}],
	"action": "",
	"property": "",
	"from": "",
	"to": "",
	"reg": false,
	"x": 870,
	"y": 180,
	"wires": [
		["647ed860.2859f"]
	]
}, {
	"id": "aab49b0b.b783d8",
	"type": "http response",
	"z": "d4c8a74c.53eef8",
	"name": "",
	"statusCode": "",
	"headers": {},
	"x": 930,
	"y": 300,
	"wires": []
}, {
	"id": "ee68544a.99a7c8",
	"type": "watson-assistant-v2",
	"z": "d4c8a74c.53eef8",
	"name": "",
	"default-endpoint": false,
	"service-endpoint": "https://gateway.watsonplatform.net/assistant/api",
	"assistant_id": "<<your-assistant-id>>",
	"debug": false,
	"restart": false,
	"return_context": true,
	"alternate_intents": false,
	"multisession": true,
	"timeout": "",
	"optout-learning": false,
	"x": 530,
	"y": 100,
	"wires": [
		["c0cbb01.d83a1d", "a28454e7.31b6d8"]
	]
}, {
	"id": "a28454e7.31b6d8",
	"type": "switch",
	"z": "d4c8a74c.53eef8",
	"name": "type",
	"property": "payload.output.generic[0].response_type",
	"propertyType": "msg",
	"rules": [{
		"t": "eq",
		"v": "text",
		"vt": "str"
	}, {
		"t": "eq",
		"v": "search",
		"vt": "str"
	}, {
		"t": "else"
	}],
	"checkall": "true",
	"repair": false,
	"outputs": 3,
	"x": 530,
	"y": 180,
	"wires": [
		["a2b4be3c.ecb018"],
		["e6504a00.5649a8"],
		["fbc00ace.86d468"]
	]
}, {
	"id": "e6504a00.5649a8",
	"type": "template",
	"z": "d4c8a74c.53eef8",
	"name": "search",
	"field": "payload",
	"fieldType": "msg",
	"format": "handlebars",
	"syntax": "mustache",
	"template": "{{#payload}}\n  {{#output}}\n    {{#generic}}\n    {{header}}\n    {{#results}}\n    <details>\n        <summary>{{title}} ({{result_metadata.confidence}})</summary>\n        {{{highlight.body}}}\n    </details>\n    {{/results}}\n    {{/generic}}\n  {{/output}}\n{{/payload}}",
	"output": "str",
	"x": 690,
	"y": 180,
	"wires": [
		["dae785b.579ddf8"]
	]
}, {
	"id": "fbc00ace.86d468",
	"type": "template",
	"z": "d4c8a74c.53eef8",
	"name": "other",
	"field": "payload",
	"fieldType": "msg",
	"format": "handlebars",
	"syntax": "mustache",
	"template": "{{#payload}}\n  {{#output}}\n    {{#text}}\n    {{.}}\n    {{/text}}\n  {{/output}}\n{{/payload}}",
	"output": "str",
	"x": 690,
	"y": 220,
	"wires": [
		["dae785b.579ddf8"]
	]
}]
```

</details>	

After importing the flow into Node-RED, you will need to configure the `assistant V2` node to include the API key and assistant ID for your Watson search assistant.

+ access the settings for the Assistant:
![assistant-settings](/assets/assistant-settings.png)
+ copy the API and Assistant ID from the API details view:
![assistant-api-settings](/assets/assistant-api-settings.png)
+ paste the settings into the Node-RED Assistant node:
![node-red-assistant-settings](/assets/node-red-assistant-settings.png)

Deploy the updates to Node-RED, and visit the `/chat` page of your Node-RED application, and entry queries; you should see either responses from the dialog skill, or sections of documents from your Discovery corpus.

If all goes well, you should have a basic chat and search bot like this:
![node-red-chat](/assets/node-red-chat-results.png)

Unless you have a thing for brutally ugly user interfaces, please customise to your own taste ...


## Links ##

Tutorials, demos and applications if you would like to explore Watson Assistant and/or Watson Discovery in more detail:

1. [Demos and Hands-on Labs](https://www.ibm.com/demos/collection/Watson-Assistant/)
1. [Sample Apps](https://cloud.ibm.com/docs/assistant?topic=assistant-sample-apps)
1. [youtube playlist - Watson Assistant](https://www.youtube.com/playlist?list=PLZDyxLlNKRY8zx37vPh6s_pCtOXIp_5yL)
1. [youtube playlist - Watson Discovery](https://www.youtube.com/playlist?list=PLZDyxLlNKRY_GJskIreh9sQgExJ4z8oZO)
1. [Gary Wilson's Assistant labs](https://github.com/garyrwilson/Watson-Assistant-Labs)
1. [COVID-19 chatbot](https://developer.ibm.com/callforcode/get-started/covid-19/crisis-communication/)

