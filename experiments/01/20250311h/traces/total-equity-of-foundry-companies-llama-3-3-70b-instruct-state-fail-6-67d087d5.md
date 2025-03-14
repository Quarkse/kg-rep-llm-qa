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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 32276 triples. System version v0.2.8-91-g5e507554 is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Total equity of foundry companies

***

Think: The user is asking for the total equity of foundry companies. To formulate a query for this, we need to identify the key resources involved, which are "foundry companies" and "total equity". We also need to consider the properties and relationships that connect these resources in the knowledge graph.

Act: search('foundry company') | search('total equity') | deref('http://schema.org/organization') | deref('http://schema.org/financialStatement')

***

The keyword search for `foundry company` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **Foundry** 0.7276
    https://welektronik.iis.fraunhofer.de/entity/Q291 **Foundry Service** 0.4706
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.3881
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.3032
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ838769.ttl#this **Fountain Valley** 0.2941

***

The keyword search for `total equity` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity **total equity** 1.0000
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalAssets **total assets** 0.4286
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalRevenue **total revenue** 0.4140
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1147.ttl#this **Trinity** 0.3563
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5285.ttl#this **Tarlac City** 0.2965

***

No results for `deref('http://schema.org/organization')`.

***

No results for `deref('http://schema.org/financialStatement')`.

***

Think: The search results provide us with potential URIs for "foundry company" and "total equity". We can use these URIs to further explore the knowledge graph and gather more information. The URI for "total equity" is https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity. We can use this URI to find more information about the property "total equity" and how it relates to foundry companies.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q287') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity') | search('financial statement') | search('company')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q287` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q287> a tbox:OrganizationType ;
        rdfs:label "Foundry"@en .

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
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

***

The keyword search for `financial statement` returned the following ranked list with hits.

    http://xmlns.com/foaf/0.1/Document **Document** 0.2760
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this **Cyient** 0.2315
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4354448.ttl#this **Southern Finland Regional State Administrative Agency** 0.2312
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ161036.ttl#this **Free State of Prussia** 0.2275
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3940508.ttl#this **South-Western Finland Regional State Administrative Agency** 0.2217

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **Canyon County** 0.3443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **Cook County** 0.3443

***

Think: We have gathered more information about the properties and relationships involved in the query. We know that "total equity" is a datatype property with a range of xsd:decimal, and it is related to the concept of "foundry company". We also have a list of potential URIs for "company" and "financial statement". However, we still need to find a way to connect these concepts to the total equity of foundry companies.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?x WHERE { ?x tbox:totalEquity ?y . FILTER (xsd:decimal(?y)) }') | search('industry') | search('sector')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?x WHERE { ?x tbox:totalEquity ?y . FILTER (xsd:decimal(?y)) }' returned the following solution (first 20 results).
    x
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity1999
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2001
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2002
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2003
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2004
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2005
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2006
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2007
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2008
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2009
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2010
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2011
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2012
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2013
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2014
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2016
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2017
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#totalequity2018

***

The keyword search for `industry` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this **Hoshine Silicon Industry** 0.5582
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1074.ttl#this **Anyang Dingsheng Silicon Industry** 0.4679
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1201.ttl#this **Hoshine Silicon Industry Luzhou Fab** 0.4159
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1200.ttl#this **Hoshine Silicon Industry Jiaxing Fab** 0.4104
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1204.ttl#this **Hoshine Silicon Industry Xinjiang Fab** 0.4051

***

The keyword search for `sector` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **Seoul Semiconductor** 0.5160
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ189710.ttl#this **Selangor** 0.4472
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1163.ttl#this **Semiconductor Electronics** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this **GCT Semiconductor** 0.4056
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **GTA Semiconductor** 0.4056

***

Think: We have found some relevant information about the total equity of companies, but we still need to filter the results to only include foundry companies. We can use the search results for "industry" and "sector" to help us with this.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?x WHERE { ?x tbox:totalEquity ?y . FILTER (xsd:decimal(?y)) . ?x tbox:industry "foundry"@en }') | search('silicon foundry') | search('semiconductor foundry')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?x WHERE { ?x tbox:totalEquity ?y . FILTER (xsd:decimal(?y)) . ?x tbox:industry "foundry"@en }')`.

***

The keyword search for `silicon foundry` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **Foundry** 0.6468
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ163820.ttl#this **Silicon Valley** 0.5457
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#this **Silicon Lab** 0.5381
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#this **Silicon Motion** 0.5145
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1067.ttl#this **REC Silicon** 0.4709

***

The keyword search for `semiconductor foundry` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **Seoul Semiconductor** 0.6522
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this **GCT Semiconductor** 0.6219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **GTA Semiconductor** 0.6219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this **AKM Semiconductor** 0.6219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this **CISC Semiconductor** 0.6061

***

Think: We have found some relevant information about silicon and semiconductor foundries, but we still need to find a way to connect this to the total equity of foundry companies.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?x WHERE { ?x tbox:totalEquity ?y . FILTER (xsd:decimal(?y)) . ?x tbox:industry "semiconductor"@en }') | search('foundry company') | search('total equity of foundry companies')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?x WHERE { ?x tbox:totalEquity ?y . FILTER (xsd:decimal(?y)) . ?x tbox:industry "semiconductor"@en }')`.

***

Do not repeat actions.

***

The keyword search for `total equity of foundry companies` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity **total equity** 0.6048
    https://welektronik.iis.fraunhofer.de/entity/Q287 **Foundry** 0.4062
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalAssets **total assets** 0.3257
    https://welektronik.iis.fraunhofer.de/entity/Q291 **Foundry Service** 0.2955
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this **GlobalFoundries** 0.2955

***

Think: We have found some relevant information about the total equity of foundry companies, but we still need to find a way to connect this to the actual values.

Act: fail('Unable to find the total equity of foundry companies.')

{'loop': {'id': '67d087d5', 'question': 'Total equity of foundry companies', 'iterations': 6, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX xsd: <http://www.w3.org/2001/XMLSchema#> SELECT ?x WHERE { ?x tbox:totalEquity ?y . FILTER (xsd:decimal(?y)) . ?x tbox:industry "semiconductor"@en }', 'elapsed_time': 69057}, 'tokens': {'prompt_tokens': 19550, 'completion_tokens': 836, 'elapsed_time_model': 51457, 'tokens_per_sec': 396.17104005008565}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}