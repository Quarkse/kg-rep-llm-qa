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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 32346 triples. System version v0.2.8-93-gfa87822d is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Total equity of foundry companies

***

Think: The user is asking for the total equity of foundry companies. To formulate a query, we need to identify the key resources involved, which are "foundry companies" and "total equity". We should start by searching for URIs that match these keywords to gather more information about the entities and properties involved.

Act: search('foundry companies') | search('total equity') | search('equity')

***

The keyword search for `foundry companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.5827
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this **['GlobalFoundries']** 0.3895
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ548.ttl#this **['GlobalFoundries Malta Fab']** 0.2649
    https://welektronik.iis.fraunhofer.de/entity/Q291 **['Foundry Service', 'Producing semiconductors for others.']** 0.2644
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ551.ttl#this **['GlobalFoundries Dresden Fab']** 0.2556

***

The keyword search for `total equity` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity **['total equity', 'Observed total equity key figure of an enterprise.']** 0.7325
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1147.ttl#this **['Trinity']** 0.3563
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalAssets **['total assets', 'Observed total assets key figure of an enterprise.']** 0.3099
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalRevenue **['total revenue', 'Observed total revenue key figure of an enterprise.']** 0.3032
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5285.ttl#this **['Tarlac City']** 0.2965

***

The keyword search for `equity` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity **['total equity', 'Observed total equity key figure of an enterprise.']** 0.4845
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1147.ttl#this **['Trinity']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ494254.ttl#this **['Elk County']** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1359251.ttl#this **['Kaili City']** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ680842.ttl#this **['Yilan City']** 0.3062

***

Think: We have identified some key resources related to "foundry companies" and "total equity". The URI https://welektronik.iis.fraunhofer.de/entity/Q287 represents the concept of a foundry company, and the URI https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity represents the concept of total equity. We should now dereference these resources to gather more information about their properties and relationships.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q287') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q287` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ104.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ114.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ117.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1176.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ123.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ141.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ162.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ164.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ165.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ237.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ38.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ46.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ49.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ50.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ51.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ52.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ72.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ77.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q287> a tbox:OrganizationType ;
        rdfs:label "Foundry"@en ;
        rdfs:comment "Company that produces semiconductors for other companies."@en .

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    tbox:totalEquity a qb:MeasureProperty,
            owl:DatatypeProperty ;
        rdfs:label "total equity"@en ;
        rdfs:comment "Observed total equity key figure of an enterprise."@en ;
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

***

Think: We have gathered more information about the properties and relationships of the key resources. The URI https://welektronik.iis.fraunhofer.de/entity/Q287 represents the concept of a foundry company, and it has a property tbox:organizationType that relates it to various companies. The URI https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity represents the concept of total equity, and it is a measure property with a range of xsd:decimal. We should now construct a query that retrieves the total equity of foundry companies.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?observation tbox:observedValue ?company . ?observation tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?observation tbox:observedValue ?company . ?observation tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }')`.

***

Think: The query did not return any results. This could be due to the fact that the property tbox:observedValue is not correctly related to the companies. We should try to construct a new query that retrieves the total equity of foundry companies without using the tbox:observedValue property.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }')`.

***

Think: The query still did not return any results. This could be due to the fact that the property tbox:totalEquity is not directly related to the companies. We should try to construct a new query that retrieves the total equity of foundry companies by using a different approach.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company a <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company a <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }')`.

***

Think: The query still did not return any results. This could be due to the fact that the class https://welektronik.iis.fraunhofer.de/entity/Q287 is not correctly defined or instantiated in the knowledge graph. We should try to construct a new query that retrieves the total equity of foundry companies by using a different approach.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?observation tbox:observedObject ?company . ?observation tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?observation tbox:observedObject ?company . ?observation tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }')`.

***

Think: We have tried various queries to retrieve the total equity of foundry companies, but none of them returned any results. This suggests that the knowledge graph may not contain the necessary information to answer this question. We should inform the user that we were unable to find the required information.

Act: fail('Unable to find the required information to answer the question about the total equity of foundry companies.')

{'loop': {'id': '67d21c60', 'question': 'Total equity of foundry companies', 'iterations': 7, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?company ?totalEquity WHERE { ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?observation tbox:observedObject ?company . ?observation tbox:totalEquity ?totalEquity . FILTER (xsd:decimal(?totalEquity)) }', 'elapsed_time': 96663}, 'tokens': {'prompt_tokens': 27211, 'completion_tokens': 1178, 'elapsed_time_model': 87131, 'tokens_per_sec': 325.81693506852054}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}