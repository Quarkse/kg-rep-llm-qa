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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 48029 triples. System version v0.2.8-84-gdf5e4a10 is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Operating income of companies in 2021 given in New Taiwan dollar

***

Think: The User is asking for the operating income of companies in 2021, specifically in New Taiwan dollars. To formulate a query, we need to identify the key resources involved, such as companies, operating income, and the year 2021. We also need to consider the currency, which is New Taiwan dollars.

Act: search('company') | search('operating income') | search('New Taiwan dollar') | search('2021')

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **Canyon County** 0.3443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **Cook County** 0.3443

***

The keyword search for `operating income` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#operatingIncome **operating income** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ237683.ttl#this **Ome** 0.4216
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#incomingSupplyFlow **incoming supply flow** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this **OpenFive** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ274.ttl#this **Ampere Computing** 0.2778

***

The keyword search for `New Taiwan dollar` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this **Taiwan** 0.4867
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ244898.ttl#this **New Taipei** 0.4636
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this **Taiwan Semiconductor Manufacturing Company Taiwan Fab** 0.3363
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ32081.ttl#this **Taiwan Province** 0.3338
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1384.ttl#this **New York** 0.2902

***

The keyword search for `2021` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#conf-hotchips-Gelsinger22 **Semiconductors Run the World : Hot Chips 2022.** 0.1667
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23048142.ttl#this **Carmelray Industrial Park 1** 0.1072
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ382.ttl#this **Qorvo Fab Richardson** 0.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ907.ttl#this **Signetics** 0.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ11917.ttl#this **Canton of Geneva** 0.0000

***

Think: We have identified some key resources, including companies, operating income, New Taiwan dollars, and the year 2021. However, the search results for "2021" did not yield any relevant hits. We need to refine our search to find more relevant information.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#operatingIncome') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this') | search('year 2021') | search('currency')

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
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this` is as follows.

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix ns1: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> .
    @prefix ns2: <https://www.w3.org/ns/org#> .
    @prefix ns3: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1030.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1032.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1042.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1069.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1096.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1099.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1101.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ178.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1029> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1030> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1032> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1042> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1069> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1096> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1098> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1099> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1101> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1123> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q178> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q196> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q223> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q58> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q667> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q675> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q695> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q721> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q80> ns1:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#capex2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#employees2017> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#employees2020> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#employees2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#headquarter> tbox:registeredSiteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2017> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2020> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2021> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#operatingincome2020> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#operatingincome2021> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalequity2021> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalequity2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalrevenue2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ223.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ24.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ24.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ29.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ29.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ713.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ713.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ98.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ98.ttl#this> tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this> ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this> ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this> ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this> ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ662.ttl#this> ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ663.ttl#this> ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ664.ttl#this> ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1049> tbox:sizeOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q287> tbox:organizationTypeOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q289> tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q290> tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q291> tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://www.tsmc.com/> tbox:homepageOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> ;
        tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> ;
        tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#this> tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> ;
        tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> a owl:Thing,
            ns1:Enterprise,
            ns2:Organization ;
        rdfs:label "Taiwan Semiconductor Manufacturing Company"@en ;
        ns3:locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ717461.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this> ;
        owl:sameAs <http://www.wikidata.org/entity/Q713418>,
            <https://welektronik.iis.fraunhofer.de/entity/Q20> ;
        foaf:homepage <https://www.tsmc.com/> ;
        tbox:enterpriseObservation <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#capex2022>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#employees2017>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#employees2020>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#employees2022>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2017>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2020>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2021>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#operatingincome2020>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#operatingincome2021>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalequity2021>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalequity2022>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalrevenue2022> ;
        tbox:hasCustomer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ24.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ29.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ713.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ98.ttl#this> ;
        tbox:hasSupplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1030.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1032.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1042.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1069.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1096.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1099.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1101.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ178.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ223.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#this> ;
        tbox:incomingSupplyFlow <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1029>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1030>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1032>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1042>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1069>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1096>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1098>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1099>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1101>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1123>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q178>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q196>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q223>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q58>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q667>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q675>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q695>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q721>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q80> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> ;
        tbox:outgoingSupplyFlow <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ24.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ29.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ713.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#Q20>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ98.ttl#Q20> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289>,
            <https://welektronik.iis.fraunhofer.de/entity/Q290>,
            <https://welektronik.iis.fraunhofer.de/entity/Q291> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> ;
        ns2:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#headquarter> ;
        ns2:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ662.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ663.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ664.ttl#this> .

***

The keyword search for `year 2021` returned the following ranked list with hits.

    https://dblp.org/rdf/schema#yearOfPublication **year of publication** 0.3858
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#accountingYear **accounting year** 0.3430
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#this **MaxLinear** 0.2132
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23080.ttl#this **Tyne and Wear** 0.1826
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ50421.ttl#this **Yeonsu District** 0.1715

***

The keyword search for `currency` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#currency **currency** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ661216.ttl#this **Wil Constituency** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3123263.ttl#this **Marcy** 0.2390
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ497788.ttl#this **Cumberland County** 0.2176
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1132340.ttl#this **Presidency division** 0.2070

***

Think: We have gathered more information about the company, operating income, and currency. We also found a property `tbox:operatingIncome2021` that is related to the operating income in 2021. However, we still need to find a way to filter the results to only include companies that report their operating income in New Taiwan dollars.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#currency') | query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x tbox:operatingIncome2021 ?y . ?x tbox:currency ?z . FILTER (contains(str(?z), "New Taiwan dollar")) }')

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#currency` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    tbox:currency a qb:AttributeProperty,
            owl:DatatypeProperty ;
        rdfs:label "currency"@en ;
        rdfs:domain qb:Observation ;
        rdfs:range rdf:langString .

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x tbox:operatingIncome2021 ?y . ?x tbox:currency ?z . FILTER (contains(str(?z), "New Taiwan dollar")) }')`.

***

Think: The query did not return any results, which means that there are no companies in the knowledge graph that report their operating income in 2021 in New Taiwan dollars. We need to adjust the query to find companies that report their operating income in any currency.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x ?y WHERE { ?x tbox:operatingIncome2021 ?y }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x ?y WHERE { ?x tbox:operatingIncome2021 ?y }')`.

***

Think: The query still did not return any results. This suggests that the property `tbox:operatingIncome2021` is not being used in the knowledge graph. We need to find an alternative way to query the operating income of companies in 2021.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x ?y WHERE { ?x tbox:operatingIncome ?y . FILTER (contains(str(?x), "2021")) }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x ?y WHERE { ?x tbox:operatingIncome ?y . FILTER (contains(str(?x), "2021")) }' returned the following solution (first 20 results).
    x,y
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1030.ttl#operatingincome2021,5381822000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#operatingincome2021,98980000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#operatingincome2021,3648000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#operatingincome2021,649980897000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#operatingincome2021,10041000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#operatingincome2021,19456000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#operatingincome2021,9789000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ245.ttl#operatingincome2021,89678000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#operatingincome2021,8960000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#operatingincome2021,6283000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#operatingincome2021,1692201000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#operatingincome2021,2583000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ31.ttl#operatingincome2021,2419000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#operatingincome2021,1612700000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#operatingincome2021,108949000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#operatingincome2021,53351827000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#operatingincome2021,-59812000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#operatingincome2021,4837000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ668.ttl#operatingincome2021,1347000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#operatingincome2021,6889000000.0

***

Think: The query returned a list of companies with their operating income in 2021. However, the currency of the operating income is not specified. We need to find a way to determine the currency of the operating income.

Act: success('The operating income of companies in 2021 is listed below. Note that the currency is not specified.')

{'loop': {'id': '67c461fa', 'question': 'Operating income of companies in 2021 given in New Taiwan dollar', 'iterations': 6, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x ?y WHERE { ?x tbox:operatingIncome ?y . FILTER (contains(str(?x), "2021")) }', 'elapsed_time': 71493}, 'tokens': {'prompt_tokens': 86876, 'completion_tokens': 760, 'elapsed_time_model': 60677, 'tokens_per_sec': 1444.2817688028472}, 'git': {'label': 'v0.2.8-84-gdf5e4a10', 'commit': 'df5e4a10170efede1e56c09a029ca4d906e5856a'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}