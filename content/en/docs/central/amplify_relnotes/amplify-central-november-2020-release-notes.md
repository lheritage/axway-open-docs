---
title: AMPLIFY Central November 2020 Release Notes
linktitle: AMPLIFY Central November 2020
weight: 90
description: AMPLIFY Central enables the user to manage their provider /
  consumer view. For more information, see the AMPLIFY Central documentation.
---
## New features and enhancements

The following new features and enhancements are available in this update.

### AMPLIFY Central CLI

The AMPLIFY Central CLI is a package for managing AMPLIFY Central resources with a DevOps approach to API Management.

AMPLIFY Central CLI version 0.1.19 is now available on NPM (<https://www.npmjs.com/package/@axway/amplify-central-cli/v/0.1.19>)

The CLI extension is compatible **only** with the AMPLIFY CLI **version 1.4** (<https://www.npmjs.com/package/@axway/amplify-cli/v/1.4.0>)

**This is not yet compatible with the Axway CLI**.

The AMPLIFY Central CLI includes the following enhancements:

* Support EU region while installing agents.
* installation of AWS agent: it output the command to be given to AWS CLI to install the agent in AWS environment (EC2 instance or ECS-fargate instance).
* AMPLIFY CLI login using `amplify auth login` without the need for "--client-id" parameter.  The defaults to use the AMPLIFY Central credentials ("--client-id=apicentral").
* Ability to get resources by name where the name of the resource can exist across multiple scopes. The result of the command has been enhanced to display multiple tables with the resource kind prefixed to the name of the resource to improve readability.
    * Example 1:  "amplify central get secret test" will return secret resources named "test" from all environments or integration root scopes.
    * Example 2:  "amplify central get secret –s test" will return secret resources from an environment and/or integration named "test".
    * Example 3:  "amplify central get webhook,secret –s test" will return webhook/secret  resources from an environment and/or integration named "test".

### AMPLIFY Central WebUI

The AMPLIFY Central CLI includes the following enhancements:

* View if a discovery agent is connected to an environment. The `Manual Sync.` badge is replace by:
    * `CONNECTED` when discovery agent is up and running.
    * `CONNECTION ERROR` when the discovery agent is not able to connect to the Gateway
    * `DISCONNECTED` when the discovery agent is down
* Improved Provider UX for the Environment details page to include:
    * Activity report metrics of the aggregated count of API Services, Catalog Items and Subscriptions for the selected Environment.  
* Improved Provider UX of the API Service details page to include:
    * View of multiple API Service Versions.
    * Activity report metrics of the related Endpoints, Catalog Items and Subscriptions for the selected API Service version.  
    * Rendering of WSDL and PROTOBUF specifications in addition to OAS2/OAS3.

### Axway Edge Gateway / AWS Agents

In order to provide a better visibility of your mutli-type gateway eco system, two sets of agents are provided. These agents collect data from the Gateway (API / traffic) and expose them in AMPLIFY Central, giving you a global vision of your eco system from a single interface.

The agents includes the following enhancements:

* Default behavior when subscribing is now to create unique credentials for each consumer (API Key / oauth credentials). Refer to [Subscription workflow](/docs/central/connect-api-manager/subscription-for-the-consumer/)
* Discovery agent handles log rotation/retention. Refer to [logging variables](/docs/central/connect-api-manager/agent-variables)

### Mesh governance

AMPLIFY Central mesh governance enables you to govern and manage your APIs, public and private services, along with the hybrid environments where they are located.

No new update

#### Fixed issues

* Previously, within AMPLIFY Central CLI 0.1.17 version, when installing service account with a wrong name, the CLI froze. Now, a proper message is displayed to help the user understand the error.
* Previously, when a subscription fails, no email were sent to the subscriber by the discovery agent. Now, the email is sent and contains the reason of failure.
* Previously, when an API has not the PUBLISHED status, a consumer can start the subscription. Now, only PUBLISHED status API enables a consumer to subscribe to it.
* The Central CLI results listing for the Mesh Discovery resources now indicates the correct SCOPE and SCOPE NAME the resources are related to.

### Known limitations

This version of AMPLIFY Central has the following limitations:

* Users that are assigned the Consumer role cannot see their subscription usage on the API Observer screen.  
* Axway Edge Gateway Agents:

    * Discovery Agent can only discover APIs having PassThrough, API Key and Oauth security.
    * Discovery Agent cannot expose discovered APIs in multiple teams, meaning that the Organization structure on API Manager is lost in Central. The API provider has to create the team in AMPLIFY Platform and share the API within appropriate teams.
    * Discovery Agent is not able to detect that an API has been renamed. Consequently, on the AMPLIFY Central side, you will see two APIs: the old one and the new one.
    * Discovery Agent does not handle frontend API deletion. Consequently, Unified Catalog API is out of sync.
    * Traceability Agent is not working in an Externally Managed Topology deployment.

* AWS Gateway agents:

    * Discovery Agent is working with one AWS Region only (the one used when installing the agent).
    * Discovery Agent does not associate the usage plan and API when a subscriber chooses a usage plan that is not already linked to the chosen API.

* Mesh Governance alpha Discovery Agents:

    * The alpha Discovery Agents do not work with the Mesh Traceability Agent.
