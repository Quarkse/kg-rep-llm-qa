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

Customers of ASML

***

Think: The user is asking about customers of ASML, which is a company that manufactures semiconductor manufacturing equipment. To formulate a query, we need to identify the key resources involved, such as ASML and its customers.

Act: search('ASML') | search('semiconductor manufacturing equipment customers') | deref('https://en.wikipedia.org/wiki/ASML_Holding')

***

The keyword search for `ASML` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this **['ASML']** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this **['ASM International']** 0.3746
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ42114.ttl#this **['Asan']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1089.ttl#this **['ASUZAC']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4803324.ttl#this **['Asago district']** 0.2041

***

The keyword search for `semiconductor manufacturing equipment customers` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1023 **['Company that produces equipment for semiconductor manufacturing.', 'Equipment manufacturer']** 0.6891
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **['Taiwan Semiconductor Manufacturing Company']** 0.5815
    https://welektronik.iis.fraunhofer.de/entity/Q1060 **['Materials producer', 'Company that produces equipment for semiconductor manufacturing.']** 0.5411
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this **['Taiwan Semiconductor Manufacturing Company Nanjing Fab']** 0.5348
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this **['Taiwan Semiconductor Manufacturing Company Hsinchu Fab']** 0.5154

***

No results for `deref('https://en.wikipedia.org/wiki/ASML_Holding')`.

***

Think: We have identified ASML and some of its potential customers, such as Taiwan Semiconductor Manufacturing Company. We also have information about the company that produces equipment for semiconductor manufacturing. To further formulate the query, we need to gather more information about the relationships between ASML and its customers.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this') | deref('https://welektronik.iis.fraunhofer.de/entity/Q1023') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this` is as follows.

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix ns1: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> .
    @prefix ns2: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#employees2020> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#netprofit2021> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ46.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ668.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ676.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ719.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ98.ttl#Q1029> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> a owl:Thing,
            ns1:Enterprise,
            ns2:Organization ;
        rdfs:label "ASML"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q297879>,
            <https://welektronik.iis.fraunhofer.de/entity/Q1029> ;
        foaf:homepage <https://www.asml.com/> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> ;
        ns2:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#headquarter> .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1023` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1022.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1024.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1025.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1026.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1027.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1028.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1030.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1031.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1032.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1034.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1037.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1039.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1040.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1041.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1042.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1043.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1044.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1168.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ117.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1178.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ902.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ91.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ94.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1023> a tbox:OrganizationType ;
        rdfs:label "Equipment manufacturer"@en ;
        rdfs:comment "Company that produces equipment for semiconductor manufacturing."@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this` is as follows.

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix ns1: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> .
    @prefix ns2: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
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
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2017> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2020> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#netprofit2021> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#operatingincome2020> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#operatingincome2021> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalequity2021> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalequity2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#totalrevenue2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ24.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ29.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ713.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ98.ttl#Q20> ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> a owl:Thing,
            ns1:Enterprise,
            ns2:Organization ;
        rdfs:label "Taiwan Semiconductor Manufacturing Company"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q713418>,
            <https://welektronik.iis.fraunhofer.de/entity/Q20> ;
        foaf:homepage <https://www.tsmc.com/> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> ;
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

Think: We have identified ASML and some of its potential customers, such as Taiwan Semiconductor Manufacturing Company. We also have information about the company that produces equipment for semiconductor manufacturing. To further formulate the query, we need to gather more information about the relationships between ASML and its customers.

Act: query('PREFIX ns1: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> ns1:customer ?customer . }')

***

No results for `query('PREFIX ns1: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> ns1:customer ?customer . }')`.

***

Think: We have identified ASML and some of its potential customers, such as Taiwan Semiconductor Manufacturing Company. We also have information about the company that produces equipment for semiconductor manufacturing. To further formulate the query, we need to gather more information about the relationships between ASML and its customers.

Act: query('PREFIX ns1: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { ?customer ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> . }')

***

The query 'PREFIX ns1: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { ?customer ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> . }' returned the following solution (first 20 results).
    customer
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ46.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#Q1029
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ668.ttl#Q1029

***

Think: We have identified ASML and some of its potential customers, such as Taiwan Semiconductor Manufacturing Company. We also have information about the company that produces equipment for semiconductor manufacturing. To further formulate the query, we need to gather more information about the relationships between ASML and its customers.

Act: success('The customers of ASML are Taiwan Semiconductor Manufacturing Company and other companies that purchase equipment from ASML for semiconductor manufacturing.')

{'loop': {'id': '67d21595', 'question': 'Customers of ASML', 'iterations': 5, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX ns1: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { ?customer ns1:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> . }', 'elapsed_time': 84994}, 'tokens': {'prompt_tokens': 45774, 'completion_tokens': 709, 'elapsed_time_model': 81147, 'tokens_per_sec': 572.8189479329712}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}