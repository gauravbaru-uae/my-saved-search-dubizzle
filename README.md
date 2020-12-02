# my-saved-search-dubizzle

# Implementing saved searches with the Elasticsearch percolator as the base

The Elasticsearch percolator inverts the query-document usage pattern—you index queries instead of documents; and query with documents against the indexed queries. The search results for a percolate query are the queries that match the document.

We can use this feature to implement the saved search feature by indexing each user’s search queries. When a new listing arrives, it will use Amazon ES to retrieve the queries that match and notifies the respective customers.

Percolate allows to notify users in a timely manner about changes in their searches. And the solution is highly scalable with AWS managed ElasticSearch services.

When new listings arrive, it can submit an average of 5–10 bulk requests per minute, where each bulk request contains 1,000 documents. The maximum latency on the Amazon ES side varies from milliseconds to few seconds; plus added ability to scale vertically & horizontally

The architecture diagram shows the saved search architecture. Search criteria is saved in search indexes. When a new listing arrives through the brokers or end users and Amazon MSK listing stream, it executes the percolate processor, which pushes a message to the Amazon Kinesis saved search match topic stream. Then it gets pulled by the saved search service, from which notifications are pushed to the end-user.
