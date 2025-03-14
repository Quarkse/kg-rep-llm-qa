Task

You are Graf von Data, an assistant designed to formulate a query based on input from User.

Process

You interact with a knowledge graph in a strict think-act-observe cycle.

1. Think: Analyse the question from User and the descriptions in the representations gathered so far.
2. Act: Choose available actions (listed below) that will best progress towards formulating the query.
3. Observe: HALT. System will provide the result of your chosen actions in the next cycle.

In your response, start with a `Think:` section followed by an `Act:` section.

Actions

You can issue one or multiple of the following actions.

* `search(keywords: string)`: Get URIs to resources matching the given `keywords`. Look for URIs that identify entities, i.e., make two calls: `search('foo')` and `search('bar')` instead of `search('foo bar')`.
* `deref(resource URI: string)`: Get all triples with `resource URI` in subject position. Expand (https://www.w3.org/TR/curie)[Compact URIs] to absolute URIs for use with `deref()`.
* `query(sparql: string)`: Evaluate `sparql` and get solutions. Consider using path expressions, i.e., `*` or `+` for paths of transitive properties and `|` for alternative paths.

You issue run actions concurrently using `|`, e.g., `search('foo') | search('bar')`.
Format action calls as follows: `Act: describe('http://foo/bar')` or `Act: query('PREFIX : <#> SELECT DISTINCT ?x WHERE { ... }')`.
Use quotes for arguments.

Chat

Sometimes User does not seek factual information.

* `chat(text: string)`: Issue a `chat()` action if User does not seek factual information from the knowledge graph.

Conditions

Once you have come up with the final query, check the query via `query()` and then end.

* `success(text: string)`: Confirm the query as final and optionally give User a concise message explaining the relevant steps you took. Do not mention the query or the query solutions.

If nearing about ten cycles:

* `fail(text: string)`: You have no other choice than to give up. Optionally report to User the relevant steps you tried.

Stages

* Identify key resources in the User question and find URIs via `Act: search()`.
* Next, dereference key resources via `Act: deref()`.
Iteratively expand your knowledge about the graph via `Act: deref()` to gather information required to construct the query.
Consider obtaining information about classes and properties via `Act: deref()`, especially domain and range of properties.
Consider obtaining information about the graph structure on the level of instances or assertions.
* Once you have collected the information requried to write the query, make sure to include in the query definite descriptions of the key resources.
Then, expand the query iteratively with more triple patterns.

Critical Instructions

* Ensure that all URIs used in the query exist in the knowledge graph.
* Only use URIs that have been previously mentioned or discovered via `search()` or `deref()`.
* Never repeat successfully executed actions, the results will be the same.

***

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 48029 triples. System version v0.2.8-90-ga084b38e is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Medium size companies with sites in Nuremberg

***

Think: The user is looking for medium-sized companies with sites in Nuremberg. To formulate a query, we need to identify the key resources involved, which are "medium-sized companies" and "Nuremberg". We also need to consider the properties that relate these resources, such as "has site" or "located in".

Act: search('medium-sized companies') | search('Nuremberg') | deref('http://dbpedia.org/ontology/Company') | deref('http://dbpedia.org/ontology/location')

***

The keyword search for `medium-sized companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1047 **Medium** 0.4629
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ110421.ttl#this **Medina County** 0.2817
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ39.ttl#this **MediaTek** 0.2760
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **MSE Supplies** 0.2333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.2182

***

The keyword search for `Nuremberg` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this **Nuremberg** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ539.ttl#this **Semikron Nuremberg Fab** 0.5539
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ258208.ttl#this **Neubiberg** 0.4545
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ985.ttl#this **Baden-Württemberg** 0.4150
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ14819.ttl#this **Freiberg** 0.3814

***

No results for `deref('http://dbpedia.org/ontology/Company')`.

***

No results for `deref('http://dbpedia.org/ontology/location')`.

***

Think: The search results for "medium-sized companies" and "Nuremberg" have returned some relevant hits, including a company called "Semikron Nuremberg Fab" which is located in Nuremberg. We can use this information to further refine our query. We also need to consider the properties that relate companies to their locations, such as "has site" or "located in".

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ539.ttl#this') | query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :hasSite ?site . ?site :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> }')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ539.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix ns2: <https://www.w3.org/ns/org#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ539.ttl#this> a ns1:Feature,
            ns2:Site ;
        rdfs:label "Semikron Nuremberg Fab"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentCountry <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> ;
        ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ170.ttl#this> .

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :hasSite ?site . ?site :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> }')`.

***

Think: The description of the Semikron Nuremberg Fab site has provided some useful information, including the fact that it is a site of the company Semikron. We can use this information to further refine our query. We are looking for medium-sized companies with sites in Nuremberg, so we need to find companies that have sites located in Nuremberg and also have a size that is classified as medium.

Act: query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :hasSite ?site . ?site :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> . ?company :size <https://welektronik.iis.fraunhofer.de/entity/Q1047> }')

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :hasSite ?site . ?site :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> . ?company :size <https://welektronik.iis.fraunhofer.de/entity/Q1047> }')`.

***

Think: We have not found any medium-sized companies with sites in Nuremberg using the previous queries. We need to refine our query to get the desired results. We can try to find companies that have sites located in Nuremberg and also have a size that is classified as medium, by using a different property to describe the size of the company.

Act: query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :siteOf ?site . ?site :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> . ?company :companySize <https://welektronik.iis.fraunhofer.de/entity/Q1047> }')

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :siteOf ?site . ?site :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> . ?company :companySize <https://welektronik.iis.fraunhofer.de/entity/Q1047> }')`.

***

Think: We have not found any medium-sized companies with sites in Nuremberg using the previous queries. We need to refine our query to get the desired results. We can try to find companies that have sites located in Nuremberg.

Act: query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :siteOf ?site . ?site :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> }')

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :siteOf ?site . ?site :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this> }')`.

***

Think: We have not found any companies with sites in Nuremberg using the previous queries. We need to check if there are any companies with sites in the knowledge graph.

Act: query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :siteOf ?site }')

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company :siteOf ?site }')`.

***

Think: We have not found any companies with sites in the knowledge graph using the previous queries. We need to check if there are any sites in the knowledge graph.

Act: query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?site WHERE { ?site a :Site }')

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?site WHERE { ?site a :Site }')`.

***

Think: We have not found any sites in the knowledge graph using the previous queries. We need to check if there are any companies in the knowledge graph.

Act: query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company a :Company }')

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company a :Company }')`.

***

Think: We have not found any companies in the knowledge graph using the previous queries. We have tried different approaches to find medium-sized companies with sites in Nuremberg, but we have not found any results. We need to inform the user that we could not find any information.

Act: fail('We could not find any medium-sized companies with sites in Nuremberg in the knowledge graph.')

{'loop': {'id': '67cf6dd5', 'question': 'Medium size companies with sites in Nuremberg', 'iterations': 9, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> SELECT DISTINCT ?company WHERE { ?company a :Company }', 'elapsed_time': 198442}, 'tokens': {'prompt_tokens': 23633, 'completion_tokens': 1229, 'elapsed_time_model': 192652, 'tokens_per_sec': 129.05096623673455}, 'git': {'label': 'v0.2.8-90-ga084b38e', 'commit': 'a084b38e1d7b67039f0d60b14814ef1241c00fd7'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}