---
title: "Vector Database: What is it and why you should know it?"
source: "https://medium.com/@EjiroOnose/vector-database-what-is-it-and-why-you-should-know-it-ae7e7dca82a4"
author:
  - "[[Ejiro Onose]]"
published: 2023-12-22
created: 2024-12-15
description: "Well, it’s because Generative AI and Large Language Models (LLMs) are now popular and one of the best ways to handle LLM data is with a vector database because vector databases provide the ideal…"
tags:
  - "clippings"
---
[

![Ejiro Onose](https://miro.medium.com/v2/resize:fill:88:88/1*mwFEPoxHHII5CXEHncLiJQ.jpeg)

](https://medium.com/@EjiroOnose?source=post_page---byline--ae7e7dca82a4--------------------------------)

![](https://miro.medium.com/v2/resize:fit:933/1*0asc41sLiVWfIZOnOKkygw.jpeg)

> **“If 2021 was the year of graph databases, 2023 is the year of vector databases” —** [**Chip Huen**](https://huyenchip.com/)**.**

Why? you ask...

Well, it’s because [Generative AI](https://www.techtarget.com/searchenterpriseai/definition/generative-AI) and [Large Language Models (LLMs)](https://machinelearningmastery.com/what-are-large-language-models/) are now popular and one of the best ways to handle LLM data is with a vector database because vector databases provide the ideal infrastructure for managing the complex, high-dimensional data that LLMs produce and thrive on.

In this article, we’ll discuss what vector databases are, how they work, and some excellent vector database tools you should check out.

Before we dive into vector databases, let’s first understand what a vector is.

## What is a Vector?

In machine learning (ML), a vector is a collection of numerical values that represent the characteristics or features of multi-dimensional objects such as words, images, etc.

![](https://miro.medium.com/v2/resize:fit:933/0*0P9UcQteuL99SdHv)

[source](https://www.google.com/url?sa=i&url=https%3A%2F%2Fmedium.com%2F%40junxie2%2Fvector-in-machine-learning-a24880e3b96a&psig=AOvVaw3-f0xaN8JU_aP9kxhI2JYG&ust=1699645006697000&cd=vfe&opi=89978449&ved=0CBQQjhxqFwoTCLCLmZnVt4IDFQAAAAAdAAAAABAQ)

For example, a [vector](https://medium.com/@junxie2/vector-in-machine-learning-a24880e3b96a) representing an image might contain values corresponding to the pixel intensities of the image, in the order of the image’s color channels.

![](https://miro.medium.com/v2/resize:fit:853/1*iQLN40B-nq5xifEXHLM9Rg.png)

[Source](http://what-when-how.com/introduction-to-video-and-image-processing/neighborhood-processing-introduction-to-video-and-image-processing-part-1/#google_vignette)

## What are Embeddings?

An embedding is a technique for representing complex data, such as images, text, or audio, as numerical vectors.

These embeddings capture the essence of the data and show clearly the semantic similarity (or relationship) between different objects, with similar objects having vectors that are close to each other in the vector space. Thus, ML algorithms allow them to be efficiently processed and analyzed.

![](https://miro.medium.com/v2/resize:fit:899/1*cZxzpBABjLGnnzypErn02g.png)

[source](https://arize.com/blog-course/embeddings-meaning-examples-and-how-to-compute/)

ML models often generate embeddings as part of their training process. For LLMs, an [embedding model](https://medium.com/@ryanntk/choosing-the-right-embedding-model-a-guide-for-llm-applications-7a60180d28e3) is put in place to create the embeddings

Embeddings are vectors that represent the essential features of a data point. For example, a natural language processing model might generate embeddings for words or sentences.

Embeddings can be used for a variety of tasks, such as clustering, classification, and anomaly detection. Vector databases can be used to store and query embeddings efficiently, which makes them ideal for ML applications.

To see what embeddings look like, check out this [Vectorizer](http://vectorizer-kappa.vercel.app/) created by [Kenny](https://twitter.com/kenny_io), it converts texts to embeddings.

*Note: An embedding is a vector representation, but not all vectors are embeddings*.

Putting it all together, let us define a vector database.

## What is a Vector Database?

A vector database is a type of database that stores and manages unstructured data, such as text, images, or audio, in high-dimensional vectors, to make it easy to find and retrieve similar objects quickly at scale in production.

They work by using algorithms like vector similarity search to index and query vector embeddings,

The importance of vector databases in LLM projects lies in their ability to provide easy search, high performance, scalability, and data retrieval by comparing values and finding similarities between them

![](https://miro.medium.com/v2/resize:fit:933/1*BNqVKFDxppWihmVfMiOLmg.png)

Vector database’s search capabilities can be used in various applications ranging from classical ML use cases, such as recommender systems, to providing long-term memory to large language models in modern applications, to text understanding, video summarization, drug discovery, stock market analysis, and much more.

As data continues to grow in complexity and volume, the scalability, speed, and accuracy offered by vector databases position them as a critical tool for extracting meaningful insights and unlocking new opportunities across various domains.

## What are the benefits of Vector Databases?

Here are some specific reasons why vector databases are so well-suited for LLMs and generative AI:

## Handling Massive Data Loads

Vector databases can handle the massive amounts of data that are generated by LLMs and generative AI. Traditional databases might struggle with the millions or even billions of data points produced in a single run, but vector databases are purpose-built to handle such large datasets with efficiency.

## Efficient Similarity Searches

Vector databases can find data that is similar to a given query vector. This is essential for tasks such as image search and content recommendation, which are often used in conjunction with LLMs and generative AI. For example, if you are using an LLM to generate a new image, you can use a vector database to find other images that are similar to the generated image.

## Integration with ML Algorithms

Vector databases can be integrated with machine learning algorithms. This makes it easy to use vector databases to train and evaluate machine learning models. For example, you can use a vector database to store the data that is used to train a model, and then use the vector database to search for the data that is most relevant to the model.

## Handling Vector Embeddings

Vector databases provide a superior solution for handling vector embeddings by addressing the limitations of standalone vector indices, such as scalability challenges, cumbersome integration processes, and the absence of real-time updates and built-in security measures.

## List of Some Top Vector Databases

There are several vector database solutions available in the market, each with its own set of features and capabilities. Some of the top vector database solutions include:

- Weaviate
- Pinecone
- Chroma DB
- Qdrant
- Milvus

Here’s an overview of some of the features of these vector databases. You can go see this comprehensive [vector database features matrix](https://docs.google.com/spreadsheets/d/170HErOyOkLDjQfy3TJ6a3XXXM1rHvw_779Sit-KT7uc/edit?usp=sharing) by [Dhruv Anand](https://www.linkedin.com/in/dhruv-anand-ainorthstartech/overlay/about-this-profile/)

![](https://miro.medium.com/v2/resize:fit:933/0*ed-eBYgYzdeIQNTn)

Source: Author

## Weaviate

[Weaviate](https://weaviate.io/) is an open-source vector database that can be used to store, search, and manage vectors of any dimensionality. It is designed to be scalable and easy to use, and it can be deployed on-premises or in the cloud.

![](https://miro.medium.com/v2/resize:fit:853/0*WYdrJYZSAH48wlr9)

Features:

- Weaviate can store and search vectors from various data modalities, including images, text, and audio.
- Weaviate provides seamless integration with machine learning frameworks such as Hugging Face, Open AI, LangChain, Llamaindex, TensorFlow, PyTorch, and Scikit-learn.
- Weaviate can index vectors in real-time, making it ideal for applications that require [low-latency search](https://blog.twitter.com/engineering/en_us/topics/infrastructure/2020/reducing-search-indexing-latency-to-one-second).
- Weaviate can be scaled to handle large volumes of data and high query throughput.
- Weaviate can be used in memory for fast search or with disk-based storage for larger datasets.
- Weaviate provides a user-friendly interface for managing vectors and performing searches.

## Pinecone

[Pinecone](https://www.pinecone.io/) is a fully managed cloud-based vector database that is designed to make it easy for businesses and organizations to build and deploy large-scale ML applications.

![](https://miro.medium.com/v2/resize:fit:933/0*77t2Yo_fOu34jP9w)

**Some Pinecone Features:**

- Pinecone is designed to be fast and scalable, allowing for efficient retrieval of similar data points based on their vector representations.
- It can handle large-scale ML applications with millions or billions of data points.
- Pinecone provides infrastructure management or maintenance to its users.
- Pinecone can handle high query throughput and low latency search.
- Pinecone is a secure platform that meets the security needs of businesses and organizations.
- Pinecone is designed to be user-friendly and accessible via its simple API for storing and retrieving vector data, making it easy to integrate into existing ML workflows.
- Pinecone supports real-time updates, allowing for efficient updates to the vector database as new data points are added. This ensures that the vector database remains up-to-date and accurate over time.
- Pinecone can be synced with data from various sources using tools like Airbyte and monitored using Datadog

## Chroma DB

[Chroma DB](https://www.trychroma.com/) is an open-source vector store for storing and retrieving vector embeddings. It is mainly used to save embeddings along with metadata to be used later by LLMs and can also be used for semantic search engines over text data.

![](https://miro.medium.com/v2/resize:fit:933/0*eseq_k3jtDEjualK)

Chroma DB offers a self-hosted server option and supports different underlying storage options like DuckDB for standalone or ClickHouse for scalability.

Chroma DB offers two memory modes:

- The in-memory mode
- The persistent memory

**The in-memory mode** is used for rapid testing, providing proof of concept (POC) and querying, allowing the reuse of collections between runs.

**The persistent memory** allows users to save and load data to and from a disk, causing the persistence of the database beyond the current session. This allows for the addition and deletion of documents after collection creation, and it is essential for production use cases where an in-memory database is not sufficient.

Some of the key features of Chroma DB are:

- Chroma DB supports different underlying storage options like DuckDB for standalone or ClickHouse for scalability.
- It provides SDKs for Python and JavaScript/TypeScript and focuses on simplicity, speed, and enabling analysis.
- Chroma can store vectors from various data types, including text, images, and audio.

## Qdrant

[Qdrant](https://qdrant.tech/documentation/overview/) is an open-source vector database and vector search engine that provides fast and scalable vector similarity search services with additional payloads.

![](https://miro.medium.com/v2/resize:fit:933/0*T8Y2yo08BxeC2WQU)

Here are some of the features of Qdrant:

- Qdrant offers support for disk-stored collections, as storage space is cheaper than memory. It has introduced the Scalar Quantization mechanism recently, which makes it possible to reduce the memory requirements by up to four times.
- Qdrant allows users to express more complex conditions for nested structures.
- It provides an asynchronous I/O interface that reduces overhead by managing I/O operations asynchronously, thus minimizing context switches.
- It uses distance metrics to measure similarities among vectors, and they must be selected at the same time you are creating a collection.
- It can be used with the Python quadrant client, which provides a convenient API to store, search, and manage points (i.e., vectors) with an additional payload.

## Milvus

[Milvus](https://milvus.io/) is an open-source vector database that is designed for similarity searches in dense vector datasets containing millions or even billions of vectors. Milvus vector database adopts a [systemic approach to cloud-nativity](https://milvus.io/docs/architecture_overview.md) by separating compute from storage and allowing you to scale both up and out.

![](https://miro.medium.com/v2/resize:fit:933/1*AohBYJZHgLutz8WzD37hCw.png)

[Milvus docs](https://milvus.io/docs/overview.md)

Here are some of the features of Milvus:

- Milvus uses a distributed architecture that separates storage and computing, allowing for horizontal scalability in computing nodes.
- Milvus can be scaled to handle trillions of vectors and millions of queries per second.
- Milvus supports various data types, and it provides enhanced vector similarity search with attribute filtering, UDF support, configurable consistency level, time travel, and more
- Milvus can handle high query throughput and low latency searches.
- To help users try Milvus quicker, Bin Ji, a top contributor to the Milvus community, developed [Milvus Lite](https://milvus.io/docs/milvus_lite.md), a lightweight version of Milvus. It can help you get started with Milvus in minutes, while at the same time offering many benefits.
- Milvus provides a user-friendly interface for managing vectors and performing searches.

## How To Choose The Right Vector Database For Your LLM Projects

To choose the right vector database for LLM projects, there are some factors you should consider. They include:

**Scalability**: Since LLMs generate and consume vast amounts of vector data, it is best to choose a database that can efficiently store and manage large-scale datasets without compromising performance. Also, the vector database must be able to seamlessly handle future data additions and expansion of your LLM project’s scope.

**Performance:** It should deliver fast query execution and swift retrieval of relevant vectors. It should also efficiently handle multi-dimensional queries and complex similarity searches.

**Security:** The database should provide robust security features, including encryption, access controls, and authentication mechanisms. For use cases with personal or sensitive data, the vector database should align with applicable privacy regulations.

**Cost:** Using LLM APIs already costs a fortune when running at scale, so you look out for a vector base. with flexible pricing models and one that fits your use case.

**Query interfaces**: Evaluate the ease of interaction with the database, including available query languages, APIs, and user interfaces.

**Deployment options:** Make sure the vector database whether cloud-based, on-premise, or hybrid solutions matches your infrastructure preferences and data sensitivity.

**Integration capabilities**: Ensure seamless integration with your existing LLM infrastructure and other tools in your workflow.

Yep! That’s it.

Vector databases are generally useful when building LLM applications because they serve as an abstraction layer for handling and managing LLM data.

Let me know what you think about the vector database tools mentioned here and I hear there are some really interesting vector db out there. If you have used any, please comment on what your experience was like.

**Happy Building!**

….also you could [buy me coffee](https://buymeacoffee.com/ejiro) …pretty please🤗🤗