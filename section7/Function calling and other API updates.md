---
title: "Function calling and other API updates"
source: "https://openai.com/index/function-calling-and-other-api-updates/"
author:
published:
created: 2024-12-15
description: "We’re announcing updates including more steerable API models, function calling capabilities, longer context, and lower prices."
tags:
  - "clippings"
---
June 13, 2023

We’re announcing updates including more steerable API models, function calling capabilities, longer context, and lower prices.

*July 20, 2023 update:*

We previously communicated to developers that `gpt-3.5-turbo-0301`, `gpt-4-0314` and `gpt-4-32k-0314` models were scheduled for sunset on Sept 13, 2023. After reviewing feedback from customers and our community, we are extending support for those models until at least June 13, 2024.

When we release new model versions, our top priority is to make newer models smarter across the board. We are targeting improvements on a large number of axes, such as instruction following, factual accuracy, and refusal behavior. For instance, the `gpt-4-0613` model introduced last month resulted in significant improvement on calling functions. 

We look at a large number of evaluation metrics to determine if a new model should be released. While the majority of metrics have improved, there may be some tasks where the performance gets worse. This is why we allow API users to pin the model version. For example, you can use `gpt-4-0314` instead of the generic `gpt-4`, which points to the latest model version. Each individually pinned model is stable, meaning that we won’t make changes that impact the outputs. 

We are working hard to ensure that new versions result in improvements across a comprehensive range of tasks. That said, our evaluation methodology isn’t perfect, and we’re constantly improving it. One way to help us ensure new models get better at domains you care about, is to contribute to [the OpenAI Evals library⁠(opens in a new window)](https://github.com/openai/evals/tree/main) to report shortcomings in our models.

We understand that model upgrades and behavior changes can be disruptive to your applications. We are working on ways to give developers more stability and visibility into how we release and deprecate models.

---

We released `gpt-3.5-turbo` and `gpt-4` earlier this year, and in only a short few months, have seen [incredible applications⁠](https://openai.com/stories/) built by developers on top of these models.

Today, we’re following up with some exciting updates:

- new function calling capability in the Chat Completions API
- updated and more steerable versions of `gpt-4` and `gpt-3.5-turbo`
- new 16k context version of `gpt-3.5-turbo` (vs the standard 4k version)
- 75% cost reduction on our state-of-the-art embeddings model
- 25% cost reduction on input tokens for `gpt-3.5-turbo`
- announcing the deprecation timeline for the `gpt-3.5-turbo-0301` and `gpt-4-0314` models

All of these models come with the same data privacy and security guarantees we introduced on March 1 — customers own all outputs generated from their requests and their API data will not be used for training.

## Function calling

Developers can now describe functions to `gpt-4-0613` and `gpt-3.5-turbo-0613`, and have the model intelligently choose to output a JSON object containing arguments to call those functions. This is a new way to more reliably connect GPT's capabilities with external tools and APIs.

These models have been fine-tuned to both detect when a function needs to be called (depending on the user’s input) and to respond with JSON that adheres to the function signature. Function calling allows developers to more reliably get structured data back from the model. For example, developers can:

- Create chatbots that answer questions by calling external tools (e.g., like ChatGPT Plugins)

Convert queries such as “Email Anya to see if she wants to get coffee next Friday” to a function call like `send_email(to: string, body: string)`, or “What’s the weather like in Boston?” to `get_current_weather(location: string, unit: 'celsius' | 'fahrenheit')`.

- Convert natural language into API calls or database queries

Convert “Who are my top ten customers this month?” to an internal API call such as `get_customers_by_revenue(start_date: string, end_date: string, limit: int)`, or “How many orders did Acme, Inc. place last month?” to a SQL query using `sql_query(query: string)`.

- Extract structured data from text

Define a function called `extract_people_data(people: [{name: string, birthday: string, location: string}])`, to extract all people mentioned in a Wikipedia article.

These use cases are enabled by new API parameters in our `/v1/chat/completions` endpoint, `functions` and `function_call`, that allow developers to describe functions to the model via JSON Schema, and optionally ask it to call a specific function. Get started with our [developer documentation⁠(opens in a new window)](https://platform.openai.com/docs/guides/gpt/function-calling) and [add evals⁠(opens in a new window)](https://github.com/openai/evals) if you find cases where function calling could be improved

## Function calling example

What’s the weather like in Boston right now?

Step 1·OpenAI API

Call the model with functions and the user’s input

```
curl https://api.openai.com/v1/chat/completions -u :$OPENAI_API_KEY -H 'Content-Type: application/json' -d '{
  "model": "gpt-3.5-turbo-0613",
  "messages": [
    {"role": "user", "content": "What is the weather like in Boston?"}
  ],
  "functions": [
    {
      "name": "get_current_weather",
      "description": "Get the current weather in a given location",
      "parameters": {
        "type": "object",
        "properties": {
          "location": {
            "type": "string",
            "description": "The city and state, e.g. San Francisco, CA"
          },
          "unit": {
            "type": "string",
            "enum": ["celsius", "fahrenheit"]
          }
        },
        "required": ["location"]
      }
    }
  ]
}'
```

```
{
  "id": "chatcmpl-123",
  ...
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": null,
      "function_call": {
        "name": "get_current_weather",
        "arguments": "{ \"location\": \"Boston, MA\"}"
      }
    },
    "finish_reason": "function_call"
  }]
}
```

Step 2·Third party API

Use the model response to call your API

```
curl https://weatherapi.com/...
```

```
{ "temperature": 22, "unit": "celsius", "description": "Sunny" }
```

Step 3·OpenAI API

Send the response back to the model to summarize

```
curl https://api.openai.com/v1/chat/completions -u :$OPENAI_API_KEY -H 'Content-Type: application/json' -d '{
  "model": "gpt-3.5-turbo-0613",
  "messages": [
    {"role": "user", "content": "What is the weather like in Boston?"},
    {"role": "assistant", "content": null, "function_call": {"name": "get_current_weather", "arguments": "{ \"location\": \"Boston, MA\"}"}},
    {"role": "function", "name": "get_current_weather", "content": "{\"temperature\": "22", \"unit\": \"celsius\", \"description\": \"Sunny\"}"}
  ],
  "functions": [
    {
      "name": "get_current_weather",
      "description": "Get the current weather in a given location",
      "parameters": {
        "type": "object",
        "properties": {
          "location": {
            "type": "string",
            "description": "The city and state, e.g. San Francisco, CA"
          },
          "unit": {
            "type": "string",
            "enum": ["celsius", "fahrenheit"]
          }
        },
        "required": ["location"]
      }
    }
  ]
}'
```

```
{
  "id": "chatcmpl-123",
  ...
  "choices": [{
    "index": 0,
    "message": {
      "role": "assistant",
      "content": "The weather in Boston is currently sunny with a temperature of 22 degrees Celsius.",
    },
    "finish_reason": "stop"
  }]
}
```

The weather in Boston is currently sunny with a temperature of 22 degrees Celsius.

Since the alpha release of ChatGPT plugins, we have learned much about making tools and language models work together safely. However, there are still open research questions. For example, a proof-of-concept exploit illustrates how untrusted data from a tool’s output can instruct the model to perform unintended actions. We are working to mitigate these and other risks. Developers can protect their applications by only consuming information from trusted tools and by including user confirmation steps before performing actions with real-world impact, such as sending an email, posting online, or making a purchase.

## New models

### GPT-4

`gpt-4-0613` includes an updated and improved model with function calling.

`gpt-4-32k-0613` includes the same improvements as `gpt-4-0613`, along with an extended context length for better comprehension of larger texts.

With these updates, we’ll be inviting many more people from [the waitlist⁠](https://openai.com/waitlist/gpt-4-api/) to try GPT-4 over the coming weeks, with the intent to remove the waitlist entirely with this model. Thank you to everyone who has been patiently waiting, we are excited to see what you build with GPT-4!

### GPT-3.5 Turbo

`gpt-3.5-turbo-0613` includes the same function calling as GPT-4 as well as more reliable steerability via the system message, two features that allow developers to guide the model's responses more effectively.

`gpt-3.5-turbo-16k` offers 4 times the context length of `gpt-3.5-turbo` at twice the price: $0.003 per 1K input tokens and $0.004 per 1K output tokens. 16k context means the model can now support ~20 pages of text in a single request.

### Model deprecations

Today, we’ll begin the upgrade and deprecation process for the initial versions of `gpt-4` and `gpt-3.5-turbo` that we [announced in March⁠](https://openai.com/index/introducing-chatgpt-and-whisper-apis/#:~:text=Chat%20guide.-,ChatGPT%20upgrades,-We%20are%20constantly). Applications using the stable model names (`gpt-3.5-turbo`, `gpt-4`, and `gpt-4-32k`) will automatically be upgraded to the new models listed above on June 27th. For comparing model performance between versions, our [Evals library⁠(opens in a new window)](https://github.com/openai/evals) supports public and private evals to show how model changes will impact your use cases. 

Developers who need more time to transition can continue using the older models by specifying `gpt-3.5-turbo-0301`, `gpt-4-0314`, or `gpt-4-32k-0314` in the ‘model’ parameter of their API request. These older models will be accessible through June 13th, 2024, after which requests specifying those model names will fail. You can stay up to date on model deprecations via our [model deprecation page⁠(opens in a new window)](https://platform.openai.com/docs/deprecations/). This is the first update to these models; so, we eagerly welcome [developer feedback⁠(opens in a new window)](https://community.openai.com/) to help us ensure a smooth transition.

## Lower pricing

We continue to make our systems more efficient and are passing those savings on to developers, effective today.

### Embeddings

`text-embedding-ada-002` is our most popular embeddings model. Today we’re reducing the cost by 75% to $0.0001 per 1K tokens.

### GPT-3.5 Turbo

`gpt-3.5-turbo` is our most popular chat model and powers ChatGPT for millions of users. Today we're reducing the cost of `gpt-3.5-turbo`’s input tokens by 25%. Developers can now use this model for just $0.0015 per 1K input tokens and $0.002 per 1K output tokens, which equates to roughly 700 pages per dollar.

`gpt-3.5-turbo-16k` will be priced at $0.003 per 1K input tokens and $0.004 per 1K output tokens.

Developer feedback is a cornerstone of our platform’s evolution and we will continue to make improvements based on the suggestions we hear. We’re excited to see how developers use these latest models and new features in their applications.

- [Announcements](https://openai.com/news/product/?tags=topic-announcements)
- [Product](https://openai.com/news/product/?tags=topic-product)