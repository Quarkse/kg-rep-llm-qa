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

Operationg income of very large companies

***

Think: The user is asking about the operating income of very large companies. To formulate a query, we need to identify the key resources involved, such as the concept of "operating income" and "very large companies". We also need to consider the relevant properties and classes that might be used to describe these resources in the knowledge graph.

Act: search('operating income') | search('very large companies') | search('company size') | search('financial metrics')

***

The keyword search for `operating income` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#operatingIncome **['Observed operating income key figure of an enterprise.', 'operating income']** 0.7938
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ237683.ttl#this **['Ome']** 0.4216
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this **['OpenFive']** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ274.ttl#this **['Ampere Computing']** 0.2778
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ559.ttl#this **['Semiconductor Manufacturing International Corporation Beijing Fab']** 0.2417

***

The keyword search for `very large companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1049 **['Very large enterprise size.', 'Very large']** 0.5909
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.3532
    https://welektronik.iis.fraunhofer.de/entity/Q1048 **['Large enterprise size.', 'Large']** 0.3251
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ16551.ttl#this **['Vermont']** 0.2132
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.2132

***

The keyword search for `company size` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.3837
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.3742
    https://welektronik.iis.fraunhofer.de/entity/Q297 **['Chip fab', 'Site of a company that produces semiconductors.']** 0.3080
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ662.ttl#this **['Taiwan Semiconductor Manufacturing Company Shanghai Fab']** 0.2832
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **['Taiwan Semiconductor Manufacturing Company']** 0.2820

***

The keyword search for `financial metrics` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1166.ttl#this **['Firebird Optics']** 0.2782
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1061069.ttl#this **['Metro Vancouver Regional District']** 0.2714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-dac-AlpertLKD03 **['Delay and slew metrics using the lognormal distribution.']** 0.2666
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#journals-tcad-AlpertDK01 **['RC delay metrics for performance optimization.']** 0.2596
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#journals-tcad-AlpertLKD04 **['Closed-form delay and slew metrics made easy.']** 0.2342

***

Think: The search results provide some relevant resources, including the concept of "operating income" and "very large companies". We also have some resources related to company size and financial metrics. However, we need to further expand our knowledge about these resources and their relationships in the knowledge graph.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#operatingIncome') | deref('https://welektronik.iis.fraunhofer.de/entity/Q1049') | deref('https://welektronik.iis.fraunhofer.de/entity/Q287') | deref('https://welektronik.iis.fraunhofer.de/entity/Q297')

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#operatingIncome` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    tbox:operatingIncome a qb:MeasureProperty,
            owl:DatatypeProperty ;
        rdfs:label "operating income"@en ;
        rdfs:comment "Observed operating income key figure of an enterprise."@en ;
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1049` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1075.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1092.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1175.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ150.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ245.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ254.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ31.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ56.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ59.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ63.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ65.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ699.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ706.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ709.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ719.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ76.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ85.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ90.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ91.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ92.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ94.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ95.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ96.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1049> a <https://welektronik.iis.fraunhofer.de/entity/Q1045> ;
        rdfs:label "Very large"@en ;
        rdfs:comment "Very large enterprise size."@en .

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

The description of `https://welektronik.iis.fraunhofer.de/entity/Q297` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ299.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ300.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ301.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ307.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ308.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ309.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ310.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ311.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ312.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ313.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ314.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ315.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ322.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ323.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ324.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ327.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ328.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ329.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ331.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ332.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ334.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ336.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ337.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ338.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ342.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ343.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ344.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ345.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ346.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ347.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ348.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ349.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ357.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ359.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ360.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ362.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ363.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ364.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ365.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ366.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ367.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ368.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ370.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ378.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ379.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ380.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ381.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ382.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ385.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ389.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ390.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ391.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ392.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ395.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ402.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ403.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ406.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ408.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ409.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ410.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ411.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ415.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ416.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ417.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ418.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ422.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ425.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ426.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ427.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ431.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ432.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ433.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ434.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ435.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ436.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ437.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ438.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ439.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ440.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ442.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ443.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ444.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ446.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ447.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ448.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ449.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ450.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ451.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ452.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ453.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ454.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ455.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ461.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ462.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ463.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ464.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ465.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ466.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ467.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ468.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ469.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ470.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ471.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ472.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ473.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ474.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ476.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ477.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ478.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ479.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ480.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ481.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ482.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ483.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ484.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ485.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ486.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ487.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ489.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ490.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ491.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ492.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ493.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ494.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ495.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ496.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ497.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ498.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ499.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ500.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ501.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ502.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ503.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ505.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ506.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ508.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ509.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ510.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ511.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ512.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ513.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ514.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ515.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ516.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ517.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ518.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ519.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ520.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ521.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ522.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ523.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ524.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ525.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ526.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ527.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ528.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ529.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ530.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ531.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ532.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ533.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ534.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ535.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ536.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ537.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ538.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ539.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ540.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ541.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ542.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ543.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ544.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ545.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ546.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ548.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ549.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ550.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ551.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ552.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ553.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ554.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ555.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ556.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ557.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ558.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ559.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ560.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ561.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ562.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ563.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ564.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ565.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ566.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ567.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ568.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ569.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ570.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ571.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ572.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ573.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ574.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ575.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ576.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ577.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ578.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ579.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ580.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ581.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ582.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ583.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ584.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ585.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ586.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ587.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ588.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ589.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ590.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ591.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ592.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ593.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ594.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ595.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ596.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ597.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ598.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ600.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ601.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ602.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ603.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ604.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ605.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ606.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ607.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ608.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ609.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ610.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ612.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ613.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ614.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ618.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ619.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ622.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ623.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ624.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ625.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ627.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ629.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ630.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ631.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ632.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ634.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ635.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ637.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ639.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ640.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ641.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ642.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ643.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ644.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ645.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ646.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ647.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ648.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ649.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ650.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ651.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ652.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ662.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ663.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ664.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ689.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ740.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ741.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ742.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ743.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ744.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ746.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ747.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ748.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ749.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ750.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ751.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ752.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ753.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ754.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ755.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ756.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ757.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ758.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ759.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ760.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ761.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ764.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ765.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ766.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ767.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ770.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ772.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ773.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ775.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ778.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ779.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ780.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ781.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ782.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ783.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ784.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ785.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ786.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ787.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ793.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ799.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ801.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q297> a tbox:SiteType ;
        rdfs:label "Chip fab"@en ;
        rdfs:comment "Site of a company that produces semiconductors."@en .

***

Think: We have gathered information about the key resources involved in the user's question, including the concept of "operating income" and "very large companies". We also have information about company size and financial metrics. However, we need to further expand our knowledge about these resources and their relationships in the knowledge graph.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?size ?operatingIncome WHERE { ?company tbox:size ?size . ?company tbox:operatingIncome ?operatingIncome . ?size rdfs:label "Very large"@en . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?size ?operatingIncome WHERE { ?company tbox:size ?size . ?company tbox:operatingIncome ?operatingIncome . ?size rdfs:label "Very large"@en . }')`.

***

Think: The query did not return any results, which means that there are no companies in the knowledge graph that have a size labeled as "Very large" and also have an operating income. This could be due to the fact that the size of a company is not directly related to its operating income, or that the knowledge graph does not contain enough information about companies and their financial metrics.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?size ?operatingIncome WHERE { ?company tbox:size ?size . ?company tbox:operatingIncome ?operatingIncome . FILTER NOT EXISTS { ?size rdfs:label ?label . FILTER (?label != "Very large"@en) . } . }') 

Note that the query has been modified to include a FILTER NOT EXISTS clause to exclude companies with sizes that are not labeled as "Very large".

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?size ?operatingIncome WHERE { ?company tbox:size ?size . ?company tbox:operatingIncome ?operatingIncome . FILTER NOT EXISTS { ?size rdfs:label ?label . FILTER (?label != "Very large"@en) . } . }')`.

***

Think: The query still did not return any results, which means that there are no companies in the knowledge graph that have a size labeled as "Very large" and also have an operating income. This could be due to the fact that the size of a company is not directly related to its operating income, or that the knowledge graph does not contain enough information about companies and their financial metrics.

Act: fail('Unable to find companies with very large size and operating income.')

{'loop': {'id': '67d21893', 'question': 'Operationg income of very large companies', 'iterations': 5, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?size ?operatingIncome WHERE { ?company tbox:size ?size . ?company tbox:operatingIncome ?operatingIncome . FILTER NOT EXISTS { ?size rdfs:label ?label . FILTER (?label != "Very large"@en) . } . }', 'elapsed_time': 119890}, 'tokens': {'prompt_tokens': 89065, 'completion_tokens': 766, 'elapsed_time_model': 108621, 'tokens_per_sec': 827.0093076313835}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}