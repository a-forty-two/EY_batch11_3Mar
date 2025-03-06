---
lab:
    title: 'Get started with Azure OpenAI service'
---

# Get started with Azure OpenAI service

Azure OpenAI Service brings the generative AI models developed by OpenAI to the Azure platform, enabling you to develop powerful AI solutions that benefit from the security, scalability, and integration of services provided by the Azure cloud platform. In this exercise, you'll learn how to get started with Azure OpenAI by provisioning the service as an Azure resource and using Azure AI Foundry to deploy and explore generative AI models.

In the scenario for this exercise, you will perform the role of a software developer who has been tasked to implement an AI agent that can use generative AI to help a marketing organization improve its effectiveness at reaching customers and advertising new products. The techniques used in the exercise can be applied to any scenario where an organization wants to use generative AI models to help employees be more effective and productive.

This exercise takes approximately **30** minutes.



## Deploy a model

Azure provides a web-based portal named **Azure AI Foundry portal**, that you can use to deploy, manage, and explore models. You'll start your exploration of Azure OpenAI by using Azure AI Foundry portal to deploy a model.

> **Note**: As you use Azure AI Foundry portal, message boxes suggesting tasks for you to perform may be displayed. You can close these and follow the steps in this exercise.

1. In the Azure portal, on the **Overview** page for your Azure OpenAI resource, scroll down to the **Get Started** section and select the button to go to **AI Foundry portal** (previously AI Studio).
1. In Azure AI Foundry portal, in the pane on the left, select the **Deployments** page and view your existing model deployments. If you don't already have one, create a new deployment of the **gpt-35-turbo-16k** model with the following settings:
    - **Deployment name**: *A unique name of your choice*
    - **Model**: gpt-35-turbo-16k *(if the 16k model isn't available, choose gpt-35-turbo)*
    - **Model version**: *Use default version*
    - **Deployment type**: Standard
    - **Tokens per minute rate limit**: 5K\*
    - **Content filter**: Default
    - **Enable dynamic quota**: Disabled

    > \* A rate limit of 5,000 tokens per minute is more than adequate to complete this exercise while leaving capacity for other people using the same subscription.

## Use the Chat playground

Now that you've deployed a model, you can use it to generate responses based on natural language prompts. The *Chat* playground in Azure AI Foundry portal provides a chatbot interface for GPT 3.5 and higher models.

> **Note:** The *Chat* playground uses the *ChatCompletions* API rather than the older *Completions* API that is used by the *Completions* playground. The Completions playground is provided for compatibility with older models.

1. In the **Playground** section, select the **Chat** page. The **Chat** playground page consists of a row of buttons and two main panels (which may be arranged right-to-left horizontally, or top-to-bottom vertically depending on your screen resolution):
    - **Configuration** - used to select your deployment, define system message, and set parameters for interacting with your deployment.
    - **Chat session** - used to submit chat messages and view responses.
1. Under **Deployments**, ensure that your gpt-35-turbo-16k model deployment is selected.
1. Review the default **System message**, which should be *You are an AI assistant that helps people find information.* The system message is included in prompts submitted to the model, and provides context for the model's responses; setting expectations about how an AI agent based on the model should interact with the user.
1. In the **Chat session** panel, enter the user query `How can I use generative AI to help me market a new product?`

    > **Note**: You may receive a response that the API deployment is not yet ready. If so, wait for a few minutes and try again.

1. Review the response, noting that the model has generated a cohesive natural language answer that is relevant to the query with which it was prompted.
1. Enter the user query `What skills do I need if I want to develop a solution to accomplish this?`.
1. Review the response, noting that the chat session has retained the conversational context (so "this" is interpreted as a generative AI solution for marketing). This contextualization is achieved by including the recent conversation history in each successive prompt submission, so the prompt sent to the model for the second query included the original query and response as well as the new user input.
1. In the **Chat session** panel toolbar, select **Clear chat** and confirm that you want to restart the chat session.
1. Enter the query `Can you help me find resources to learn those skills?` and review the response, which should be a valid natural language answer, but since the previous chat history has been lost, the answer is likely to be about finding generic skilling resources rather than being related to the specific skills needed to build a generative AI marketing solution.

## Experiment with system messages, prompts, and few-shot examples

So far, you've engaged in a chat conversation with your model based on the default system message. You can customize the system setup to have more control over the kinds of responses generated by your model.

1. In the main toolbar, select the **Prompt samples**, and use the **Marketing Writing Assistant** prompt template.
1. Review the new system message, which describes how an AI agent should use the model to respond.
1. In the **Chat session** panel, enter the user query `Create an advertisement for a new scrubbing brush`.
1. Review the response, which should include advertising copy for a scrubbing brush. The copy may be quite extensive and creative.

    In a real scenario, a marketing professional would likely already know the name of the scrubbing brush product as well as have some ideas about key features that should be highlighted in an advert. To get the most useful results from a generative AI model, users need to design their prompts to include as much pertinent information as possible.

1. Enter the prompt `Revise the advertisement for a scrubbing brush named "Scrubadub 2000", which is made of carbon fiber and reduces cleaning times by half compared to ordinary scrubbing brushes`.
1. Review the response, which should take into account the additional information you provided about the scrubbing brush product.

    The response should now be more useful, but to have even more control over the output from the model, you can provide one or more *few-shot* examples on which responses should be based.

1. Under the **System message** text box, expand the dropdown for **Add section** and select **Examples**. Then type the following message and response in the designated boxes:

    **User**:
    
    ```prompt
    Write an advertisement for the lightweight "Ultramop" mop, which uses patented absorbent materials to clean floors.
    ```
    
    **Assistant**:
    
    ```prompt
    Welcome to the future of cleaning!
    
    The Ultramop makes light work of even the dirtiest of floors. Thanks to its patented absorbent materials, it ensures a brilliant shine. Just look at these features:
    - Lightweight construction, making it easy to use.
    - High absorbency, enabling you to apply lots of clean soapy water to the floor.
    - Great low price.
    
    Check out this and other products on our website at www.contoso.com.
    ```

1. Use the **Apply changes** button to save the examples and start a new session.
1. In the **Chat session** section, enter the user query `Create an advertisement for the Scrubadub 2000 - a new scrubbing brush made of carbon fiber that reduces cleaning time by half`.
1. Review the response, which should be a new advert for the "Scrubadub 2000" that is modeled on the "Ultramop" example provided in the system setup.

## Experiment with parameters

You've explored how the system message, examples, and prompts can help refine the responses returned by the model. You can also use parameters to control model behavior.

1. In the **Configuration** panel, select the **Parameters** tab and set the following parameter values:
    - **Max response**: 1000
    - **Temperature**: 1

1. In the **Chat session** section, use the **Clear chat** button to reset the chat session. Then enter the user query `Create an advertisement for a cleaning sponge` and review the response. The resulting advertisement copy should include a maximum of 1000 text tokens, and include some creative elements - for example, the model may have invented a product name for the sponge and made some claims about its features.
1. Use the **Clear chat** button to reset the chat session again, and then re-enter the same query as before (`Create an advertisement for a cleaning sponge`) and review the response. The response may be different from the previous response.
1. In the **Configuration** panel, on the **Parameters** tab, change the **Temperature** parameter value to 0.
1. In the **Chat session** section, use the **Clear chat** button to reset the chat session again, and then re-enter the same query as before (`Create an advertisement for a cleaning sponge`) and review the response. This time, the response may not be quite so creative.
1. Use the **Clear chat** button to reset the chat session one more time, and then re-enter the same query as before (`Create an advertisement for a cleaning sponge`) and review the response; which should be very similar (if not identical) to the previous response.

    The **Temperature** parameter controls the degree to which the model can be creative in its generation of a response. A low value results in a consistent response with little random variation, while a high value encourages the model to add creative elements its output; which may affect the accuracy and realism of the response.

