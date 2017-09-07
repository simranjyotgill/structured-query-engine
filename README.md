# Structured Query Engine

Structured Query Engine is an Elasticsearch like search engine which supports real time indexing of documents with some particular structure and searching over them with complex compound query through a RESTful API.

SQE supports most of the basic features of Elasticsearch which includes real time addition, updation and deletion of documents through a RESTful API and has support for building queries for searching using a Query DSL (which is again similar to Elasticsearch).

This project serves as a base for creating advanced structured search engines and serves as a concise implementation of Elasticsearch.

For a demo built with structured query engine, see [movie recommendations project](https://github.com/apsdehal/movie-recommendations). SQE was created as an academic project for [Search Engine Architecture](http://cs.nyu.edu/courses/spring17/CSCI-GA.3033-006/index.html) at NYU.

## Installation

- First we need to install google's snappy which is used for compressing the inverted index.

**DEB-based**: `sudo apt-get install libsnappy-dev`

**RPM-based**: `sudo yum install libsnappy-devel`

**Brew**:  `brew install snappy`

- Recommended Version: `Python >= 3.5`
- Use `pip install -r requirements.txt` to install python dependencies


## Running

- Run using `python -m app.start`

## Configuration

Structured Query Engine creates a `.data` folder into its root directory which has `config` json file with defaults present. You can edit this config file to change default configuration. In default scenario, SQE binds only to `localhost` and thus will not be accessible from outside. Change this setting to bind it to other interface and make it available from outside. Caution: Messing with other files will lead to deletion of indices and loss of data and in result SQE won't start. Delete `.data` folder, start and reindex again in such cases.

## Indexing and Querying

- First create an index with proper mappings and settings. See this [example](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-create-index.html#mappings). Nested, primitive, keyword and text datatypes are supported for the fields.
- Add documents with POST for automatic id generation or PUT for specific id. See [this](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-index_.html#_automatic_id_generation) and [this](https://www.elastic.co/guide/en/elasticsearch/reference/current/docs-index_.html#docs-index_)
- For querying on data, see this [documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl.html). SQE supports leaf and compound queries at one nested level at the moment.

## Architecture

![Architecture](http://i.imgur.com/Dv23Btb.png)

- You can add nginx load balancer on top of the structured query engine.
- Architecture shows how RESTful API delegates requests to indexer and retriever.
- Memory resources are shared between indexers and retreivers so as to save memory space and avoid duplication
- Indexer uses debounce technique to write to disk so as to lower the number of writes.

## Future work
- Support aggregations
- Support deeply nested queries for DSL
- Use event based architecture to decouple indexers and retrievers
- Use better compression settings and methods for decreasing inverted index size

## Authors
- Amanpreet Singh [@apsdehal](http://github.com/apsdehal)
- Karthik Venkatesan [@gamemaker007](http://github.com/gamemaker007)
- Simranjyot Singh Gill [@surgical](http://github.com/x-surgical-x)

## Credits

We will like to thank our [Search Engine Architecture](http://cs.nyu.edu/courses/spring17/CSCI-GA.3033-006/index.html) course at NYU's professor Matt Doherty.

## License

Apache License V2


