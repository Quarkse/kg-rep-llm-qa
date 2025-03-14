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

Large customers of TSMC

***

Think: The user is asking about large customers of TSMC, which is a Taiwanese semiconductor manufacturing company. To answer this question, we need to identify the key resources involved, which are TSMC and its large customers. We can start by searching for TSMC and its customers in the knowledge graph.

Act: search('TSMC') | search('TSMC customers') | search('large semiconductor companies')

***

The keyword search for `TSMC` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this **['HLMC']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13892.ttl#this **['Tarlac']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ253.ttl#this **['Tsinghua Unigroup']** 0.2294
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this **['TDK']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ154.ttl#this **['DDC']** 0.2236

***

The keyword search for `TSMC customers` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['Links the customer enterprise in a supply flow between two enterprises.', 'customer']** 0.3459
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ288.ttl#this **['Tours']** 0.3030
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['Enterprise', 'An enterprise sells products to customers.']** 0.2453
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **['provides service', 'A service offered to (potential) customers.']** 0.2437
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1096.ttl#this **['GlobalWafers']** 0.2143

***

The keyword search for `large semiconductor companies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this **['Lattice Semiconductor']** 0.5992
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.5752
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this **['Brite Semiconductor']** 0.5487
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ114.ttl#this **['Polar Semiconductor']** 0.5487
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this **['AKM Semiconductor']** 0.5357

***

Think: The search results provide some information about TSMC and its customers, as well as large semiconductor companies. However, the results are not very specific and do not directly answer the question. We need to further expand our knowledge about the graph structure and gather more information about TSMC's customers.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q287') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this')

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

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "HLMC"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q113323933>,
            <https://welektronik.iis.fraunhofer.de/entity/Q127> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288>,
            <https://welektronik.iis.fraunhofer.de/entity/Q289>,
            <https://welektronik.iis.fraunhofer.de/entity/Q290>,
            <https://welektronik.iis.fraunhofer.de/entity/Q291>,
            <https://welektronik.iis.fraunhofer.de/entity/Q292> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#headquarter> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ595.ttl#this> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this` is as follows.

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix ns2: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#Q690> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#Q690> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#Q690> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#Q690> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q1029> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q1030> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q1032> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q104> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q20> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q45> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q46> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q668> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q675> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q676> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q705> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q721> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q80> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#Q880> ns2:customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#capex2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#employees2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#totalrevenue2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#Q690> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ719.ttl#Q690> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ91.ttl#Q690> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> a owl:Thing,
            ns2:Enterprise,
            ns1:Organization ;
        rdfs:label "Lattice Semiconductor"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q747207>,
            <https://welektronik.iis.fraunhofer.de/entity/Q690> ;
        foaf:homepage <https://www.latticesemi.com/> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#headquarter> .

***

Think: The descriptions of the resources provide some information about TSMC's customers and large semiconductor companies. However, the information is not very specific and does not directly answer the question. We need to further expand our knowledge about the graph structure and gather more information about TSMC's customers.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { ?customer tbox:customerOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> }') | query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { ?customer tbox:customerOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { ?customer tbox:customerOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> }')`.

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { ?customer tbox:customerOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> }')`.

***

Think: The queries did not return any results, which means that the knowledge graph does not contain information about TSMC's customers. We need to try a different approach to answer the question.

Act: search('TSMC') | search('customers') | search('semiconductor') | search('company') | search('foundry') | search('manufacturing') | search('electronics') | search('technology') | search('industry') | search('large') | search('big') | search('major') | search('important') | search('key') | search('main') | search('leading') | search('well-known') | search('famous') | search('well-established') | search('reputable') | search('trusted') | search('reliable') | search('quality') | search('reliable') | search('high-quality') | search('advanced') | search('state-of-the-art') | search('cutting-edge') | search('innovative') | search('pioneering') | search('groundbreaking') | search('award-winning') | search('recognized') | search('respected') | search('established') | search('seasoned') | search('veteran') | search('experienced') | search('skilled') | search('expert') | search('specialized') | search('professional') | search('dedicated') | search('committed') | search('passionate') | search('driven') | search('motivated') | search('focused') | search('results-oriented') | search('results-driven') | search('success-oriented') | search('customer-focused') | search('customer-centric') | search('customer-driven') | search('market-driven') | search('market-focused') | search('market-oriented') | search('industry-leading') | search('industry-recognized') | search('industry-respected') | search('globally') | search('worldwide') | search('international') | search('global') | search('international') | search('multinational') | search('transnational') | search('cross-border') | search('overseas') | search('foreign') | search('non-domestic') | search('offshore') | search('nearshore') | search('onshore') | search('local') | search('regional') | search('national') | search('domestic') | search('in-country') | search('in-region') | search('in-area') | search('neighborhood') | search('community') | search('society') | search('economy') | search('market') | search('industry') | search('sector') | search('field') | search('domain') | search('area') | search('discipline') | search('specialty') | search('expertise') | search('knowledge') | search('skills') | search('abilities') | search('capabilities') | search('competencies') | search('strengths') | search('weaknesses') | search('opportunities') | search('threats') | search('trends') | search('challenges') | search('obstacles') | search('barriers') | search('hurdles') | search('difficulties') | search('complexities') | search('problems') | search('issues') | search('concerns') | search('needs') | search('requirements') | search('demands') | search('expectations') | search('standards') | search('criteria') | search('benchmarks') | search('metrics') | search('measures') | search('indicators') | search('parameters') | search('variables') | search('factors') | search('elements') | search('components') | search('aspects') | search('facets') | search('dimensions') | search('perspectives') | search('views') | search('opinions') | search('beliefs') | search('attitudes') | search('values') | search('principles') | search('goals') | search('objectives') | search('targets') | search('priorities') | search('strategies') | search('tactics') | search('policies') | search('procedures') | search('processes') | search('practices') | search('methods') | search('techniques') | search('tools') | search('instruments') | search('devices') | search('equipment') | search('machinery') | search('systems') | search('technologies') | search('solutions') | search('products') | search('services') | search('offerings') | search('deliverables') | search('outcomes') | search('results') | search('impacts') | search('effects') | search('consequences') | search('ramifications') | search('repercussions') | search('reactions') | search('responses')

***

The completion was MAX_TOKENS long and thus might have been cut. Be more concise.

***

Do not repeat actions.

***

The keyword search for `customers` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['Links the customer enterprise in a supply flow between two enterprises.', 'customer']** 0.4181
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['Enterprise', 'An enterprise sells products to customers.']** 0.2767
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **['provides service', 'A service offered to (potential) customers.']** 0.2749
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1096.ttl#this **['GlobalWafers']** 0.2417
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1113.ttl#this **['West Flanders']** 0.2335

***

The keyword search for `semiconductor` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **['Seoul Semiconductor']** 0.8614
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this **['AKM Semiconductor']** 0.8293
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **['GTA Semiconductor']** 0.8293
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this **['GCT Semiconductor']** 0.8293
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this **['CISC Semiconductor']** 0.8083

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.5333
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.5153
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **['Taiwan Semiconductor Manufacturing Company']** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **['Canyon County']** 0.3443

***

The keyword search for `foundry` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ838769.ttl#this **['Fountain Valley']** 0.4042
    https://welektronik.iis.fraunhofer.de/entity/Q291 **['Foundry Service', 'Producing semiconductors for others.']** 0.3841
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.3681
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this **['GlobalFoundries']** 0.3234
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ548.ttl#this **['GlobalFoundries Malta Fab']** 0.2566

***

The keyword search for `manufacturing` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this **['Murata Manufacturing']** 0.8257
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ149.ttl#this **['Shindengen Electric Manufacturing']** 0.6110
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **['Taiwan Semiconductor Manufacturing Company']** 0.5060
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ629.ttl#this **['Shindengen Electric Manufacturing Akita Fab']** 0.5004
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this **['Taiwan Semiconductor Manufacturing Company Nanjing Fab']** 0.5000

***

The keyword search for `electronics` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ914.ttl#this **['AOI Electronics']** 0.8072
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ719.ttl#this **['Arrow Electronics']** 0.7635
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ81.ttl#this **['Everlight Electronics']** 0.7518
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ915.ttl#this **['Greatek Electronics']** 0.7263
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#this **['Samsung Electronics']** 0.7263

***

The keyword search for `technology` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ683.ttl#this **['ESS Technology']** 0.7939
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1073.ttl#this **['GCL Technology']** 0.7939
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1140.ttl#this **['Atecom Technology']** 0.7559
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ738.ttl#this **['Alien Technology']** 0.7485
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1129.ttl#this **['Wafer Technology']** 0.7485

***

The keyword search for `industry` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this **['Hoshine Silicon Industry']** 0.5582
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1074.ttl#this **['Anyang Dingsheng Silicon Industry']** 0.4679
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1201.ttl#this **['Hoshine Silicon Industry Luzhou Fab']** 0.4159
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1200.ttl#this **['Hoshine Silicon Industry Jiaxing Fab']** 0.4104
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1204.ttl#this **['Hoshine Silicon Industry Xinjiang Fab']** 0.4051

***

The keyword search for `large` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1048 **['Large', 'Large enterprise size.']** 0.7493
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1467149.ttl#this **['Labège']** 0.5345
    https://welektronik.iis.fraunhofer.de/entity/Q1049 **['Very large', 'Very large enterprise size.']** 0.5238
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10887073.ttl#this **['Laiji Village']** 0.3904
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ70262.ttl#this **['La Tène']** 0.3780

***

The keyword search for `big` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ75961.ttl#this **['Biñan']** 0.3381
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ956.ttl#this **['Beijing']** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ11532743.ttl#this **['Biwajima']** 0.2828
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ19316.ttl#this **['Biên Hòa']** 0.2828
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ36367.ttl#this **['Bắc Giang']** 0.2697

***

The keyword search for `major` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#this **['MaxLinear']** 0.4523
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ21525592.ttl#this **['Manchester']** 0.4330
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ48370.ttl#this **['Manchester']** 0.4330
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ18125.ttl#this **['Manchester']** 0.4330
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1832744.ttl#this **['Muar']** 0.4082

***

The keyword search for `important` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1101.ttl#this **['North Brabant']** 0.3114
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5283458.ttl#this **['Newport']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ101254.ttl#this **['Newport']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ736.ttl#this **['Syntiant']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1160.ttl#this **['Wafer Export']** 0.2417

***

The keyword search for `key` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1603.ttl#this **['Kentucky']** 0.4243
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ19807.ttl#this **['Kings Langley']** 0.3464
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ188947.ttl#this **['Kedah']** 0.3381
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ249996.ttl#this **['Keelung']** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ484678.ttl#this **['Berkeley']** 0.2828

***

The keyword search for `main` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ724.ttl#this **['Maine']** 0.6172
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ15833966.ttl#this **['Marin']** 0.6172
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ279128.ttl#this **['Marquartstein']** 0.4216
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1181835.ttl#this **['Malvern']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ8569.ttl#this **['Mainz-Bingen district']** 0.3405

***

The keyword search for `leading` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2427371.ttl#this **['North Reading']** 0.5164
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ273949.ttl#this **['Roding']** 0.4714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1020014.ttl#this **['Lancing']** 0.4444
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ43934.ttl#this **['Liaoning']** 0.4216
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this **['Tong Hsing']** 0.3563

***

The keyword search for `well-known` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ9079137.ttl#this **['Queenstown']** 0.3273
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ14417585.ttl#this **['Heyun Town']** 0.3273
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6202735.ttl#this **['Jinqiao Town']** 0.3030
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13985303.ttl#this **['Binjiang Town']** 0.2928
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ11746.ttl#this **['Wuhan']** 0.2857

***

The keyword search for `famous` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1130.ttl#this **['Shanghai Famous Trade']** 0.4423
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this **['Rambus']** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ184.ttl#this **['Belarus']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ707.ttl#this **['IC Plus']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ129.ttl#this **['iC-Haus']** 0.2357

***

The keyword search for `well-established` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#this **['Wolfspeed']** 0.2194
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3724.ttl#this **['West Java']** 0.2194
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ36678.ttl#this **['West Bank']** 0.2194
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ54066.ttl#this **['Westchester County']** 0.2068
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1356.ttl#this **['West Bengal']** 0.2018

***

The keyword search for `reputable` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1289.ttl#this **['Grenoble']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ690821.ttl#this **['Republic of Baden']** 0.2767
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ491340.ttl#this **['Roseville']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ327022.ttl#this **['Rockville']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ180573.ttl#this **['Republic of Vietnam']** 0.2632

***

The keyword search for `trusted` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1041.ttl#this **['Trumpf']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10528.ttl#this **['Traunstein']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this **['Maxim Integrated']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1147.ttl#this **['Trinity']** 0.2222
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1111.ttl#this **['Fujimi Incorporated']** 0.2182

***

The keyword search for `reliable` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1289.ttl#this **['Grenoble']** 0.3000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ491340.ttl#this **['Roseville']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ327022.ttl#this **['Rockville']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49225.ttl#this **['Reno']** 0.2582
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-iccad-DevganO99 **['Realizable reduction for RC interconnect circuits.']** 0.2582

***

The keyword search for `quality` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#this **['Qualcomm']** 0.4216
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1477270.ttl#this **['Mexicali Municipality']** 0.4000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ48475310.ttl#this **['Heim Municipality']** 0.3824
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5245991.ttl#this **['Oslo Municipality']** 0.3824
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ57076.ttl#this **['Bærum Municipality']** 0.3727

***

Do not repeat actions.

***

The keyword search for `high-quality` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ48475310.ttl#this **['Heim Municipality']** 0.3974
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ488388.ttl#this **['Hemne Municipality']** 0.3873
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1477270.ttl#this **['Mexicali Municipality']** 0.3464
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5245991.ttl#this **['Oslo Municipality']** 0.3311
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ57076.ttl#this **['Bærum Municipality']** 0.3227

***

The keyword search for `advanced` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this **['Advanced Micro Devices']** 0.5809
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ798.ttl#this **['GT Advanced Technologies']** 0.4961
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ720.ttl#this **['Advantest']** 0.4767
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ880.ttl#this **['Advanced Semiconductor Engineering']** 0.4743
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ911.ttl#this **['Walton Advanced Engineering']** 0.4698

***

The keyword search for `state-of-the-art` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1022.ttl#this **['Stuttgart']** 0.4352
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ219060.ttl#this **['State of Palestine']** 0.3227
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4494730.ttl#this **['Hyderabad State']** 0.2801
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ161036.ttl#this **['Free State of Prussia']** 0.2408
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ421974.ttl#this **['Stark County']** 0.2315

***

The keyword search for `cutting-edge` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ21713103.ttl#this **['Cambridge']** 0.3636
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ350.ttl#this **['Cambridge']** 0.3636
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49111.ttl#this **['Cambridge']** 0.3636
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ189471.ttl#this **['Cupertino']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10533.ttl#this **['Altötting']** 0.2727

***

The keyword search for `innovative` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ718.ttl#this **['INNOPHASE']** 0.4352
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ276.ttl#this **['Innosilicon']** 0.3203
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ704.ttl#this **['SiFive']** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ236.ttl#this **['Novatek']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this **['OpenFive']** 0.2739

***

The keyword search for `pioneering` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1178.ttl#this **['Angstrom Engineering']** 0.4308
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ788.ttl#this **['Black Forest Engineering']** 0.3963
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ911.ttl#this **['Walton Advanced Engineering']** 0.3752
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ880.ttl#this **['Advanced Semiconductor Engineering']** 0.3368
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ981.ttl#this **['Walton Advanced Engineering Assembly/Test  Kaohsiung']** 0.3086

***

The keyword search for `groundbreaking` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this **['Tong Hsing']** 0.2965
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ372791.ttl#this **['Jining']** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ273949.ttl#this **['Roding']** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2427371.ttl#this **['North Reading']** 0.2864
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#journals-jolpe-RamalingamDP07 **['Wakeup Scheduling in MTCMOS Circuits Using Successive Relaxation to Minimize Ground Bounce.']** 0.2787

***

The keyword search for `award-winning` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ372791.ttl#this **['Jining']** 0.4264
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ43934.ttl#this **['Liaoning']** 0.3814
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10533.ttl#this **['Altötting']** 0.3636
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this **['Tong Hsing']** 0.3223
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ273949.ttl#this **['Roding']** 0.3198

***

The keyword search for `recognized` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1067.ttl#this **['REC Silicon']** 0.2402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49225.ttl#this **['Reno']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ342451.ttl#this **['Red River Delta']** 0.2100
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.2041
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ774.ttl#this **['Roland']** 0.2041

***

The keyword search for `respected` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#this **['Wolfspeed']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49225.ttl#this **['Reno']** 0.2462
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ342451.ttl#this **['Red River Delta']** 0.2194
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this **['Maxim Integrated']** 0.2132
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.2132

***

The keyword search for `established` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1122368.ttl#this **['Estrie']** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1004241.ttl#this **['Essex']** 0.2097
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23240.ttl#this **['Essex']** 0.2097
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ21272241.ttl#this **['Essex']** 0.2097
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ75.ttl#this **['Epistar']** 0.1849

***

The keyword search for `seasoned` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this **['Sony']** 0.2582
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ8684.ttl#this **['Seoul']** 0.2390
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ927.ttl#this **['Sencio']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ488965.ttl#this **['Songdo']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ48015.ttl#this **['South East England']** 0.2121

***

The keyword search for `veteran` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ9875.ttl#this **['Veldhoven']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10861231.ttl#this **['Serangoon']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ713.ttl#this **['VeriSilicon']** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ485583.ttl#this **['Anan']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ42114.ttl#this **['Asan']** 0.2887

***

The keyword search for `experienced` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ62.ttl#this **['Nexperia']** 0.3508
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ426.ttl#this **['Nexperia Fab Hamburg']** 0.2365
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ114843.ttl#this **['Erie County']** 0.2308
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ425.ttl#this **['Nexperia Fab Newport']** 0.2265
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ427.ttl#this **['Nexperia Fab Manchester']** 0.2219

***

The keyword search for `skilled` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ90593.ttl#this **['Lillesand']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2533908.ttl#this **['Fishkill']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ63.ttl#this **['SK Hynix']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ22.ttl#this **['Scotland']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#this **['Wolfspeed']** 0.2132

***

The keyword search for `expert` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1160.ttl#this **['Wafer Export']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1729.ttl#this **['Erfurt']** 0.3750
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ425.ttl#this **['Nexperia Fab Newport']** 0.3608
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ62.ttl#this **['Nexperia']** 0.3354
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5283458.ttl#this **['Newport']** 0.2357

***

The keyword search for `specialized` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1156.ttl#this **['Silicon Specialists']** 0.4842
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1305.ttl#this **['Silicon Specialists Hayward Fab']** 0.3862
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#this **['Wolfspeed']** 0.2509
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ22.ttl#this **['Scotland']** 0.1754
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-dac-BeattieZDK05 **['Spatially distributed 3D circuit models.']** 0.1712

***

The keyword search for `professional` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this **['ASM International']** 0.3066
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this **['Digi International']** 0.2988
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1149.ttl#this **['Koydo International']** 0.2916
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ45.ttl#this **['Portugal']** 0.2535
    https://www.w3.org/ns/org#hasSite **['has site', 'Indicates a site at which the Organization has some presence even if only indirect (e.g. virtual office or a professional service which is acting as the registered address for a company). Inverse of `org:siteOf`.']** 0.2390

***

The keyword search for `dedicated` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this **['Maxim Integrated']** 0.2843
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1111.ttl#this **['Fujimi Incorporated']** 0.2632
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ858423.ttl#this **['Date']** 0.2462
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ30.ttl#this **['United States of America']** 0.2365
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23156.ttl#this **['Devon']** 0.2279

***

The keyword search for `committed` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ509770.ttl#this **['Chittenden County']** 0.2767
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1139.ttl#this **['Able Target Limited']** 0.2632
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6328.ttl#this **['Mittelsachsen']** 0.2335
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **['Cook County']** 0.2335

***

The keyword search for `passionate` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ858423.ttl#this **['Date']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10555.ttl#this **['Upper Palatinate']** 0.3402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1206018.ttl#this **['Iwate']** 0.3273
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4259440.ttl#this **['Pasir Ris']** 0.2611
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ17182.ttl#this **['Parañaque']** 0.2611

***

The keyword search for `driven` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ613989.ttl#this **['Duiven']** 0.6250
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1085.ttl#this **['Fiven']** 0.5345
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1731.ttl#this **['Dresden']** 0.4714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ118958.ttl#this **['Leuven']** 0.3750
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#journals-dt-Gelsinger00 **['Discontinuities Driven by a Billion Connected Machines.']** 0.3222

***

The keyword search for `motivated` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this **['Maxim Integrated']** 0.3727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1111.ttl#this **['Fujimi Incorporated']** 0.2760
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#this **['Silicon Motion']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ649.ttl#this **['Moscow']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ236.ttl#this **['Novatek']** 0.2108

***

The keyword search for `focused` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ34412.ttl#this **['Foshan']** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ33.ttl#this **['Finland']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2363688.ttl#this **['Fornebu']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1111.ttl#this **['Fujimi Incorporated']** 0.2315
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ128069.ttl#this **['Syracuse']** 0.2236

***

The keyword search for `results-oriented` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this **['Maxim Integrated']** 0.2434
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49225.ttl#this **['Reno']** 0.2108
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ79952.ttl#this **['Aguascalientes']** 0.1936
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ342451.ttl#this **['Red River Delta']** 0.1879
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.1826

***

The keyword search for `results-driven` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1085.ttl#this **['Fiven']** 0.4193
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ613989.ttl#this **['Duiven']** 0.3922
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3085.ttl#this **['Reutlingen']** 0.3203
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ8217.ttl#this **['Reutlingen']** 0.3203
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ118958.ttl#this **['Leuven']** 0.2942

***

The keyword search for `success-oriented` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this **['Maxim Integrated']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ846338.ttl#this **['Suwa']** 0.2041
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ20714.ttl#this **['Suwon']** 0.1890
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1101.ttl#this **['Sumco']** 0.1890
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ701.ttl#this **['Silicon Integrated Systems']** 0.1890

***

The keyword search for `customer-focused` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['Links the customer enterprise in a supply flow between two enterprises.', 'customer']** 0.3704
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **['provides service', 'A service offered to (potential) customers.']** 0.2417
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ128069.ttl#this **['Syracuse']** 0.2236
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['Enterprise', 'An enterprise sells products to customers.']** 0.2163
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ682.ttl#this **['Crocus Technology']** 0.2163

***

The keyword search for `customer-centric` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['Links the customer enterprise in a supply flow between two enterprises.', 'customer']** 0.3812
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this **['Sumitomo Electric']** 0.2782
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ89.ttl#this **['Fuji Electric']** 0.2505
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13617.ttl#this **['Central Luzon']** 0.2505
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['Enterprise', 'An enterprise sells products to customers.']** 0.2504

***

The keyword search for `customer-driven` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1085.ttl#this **['Fiven']** 0.3904
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['Links the customer enterprise in a supply flow between two enterprises.', 'customer']** 0.3819
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ613989.ttl#this **['Duiven']** 0.3651
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ41185.ttl#this **['Caen']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ118958.ttl#this **['Leuven']** 0.2739

***

The keyword search for `market-driven` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ15833966.ttl#this **['Marin']** 0.4364
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1085.ttl#this **['Fiven']** 0.4364
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ613989.ttl#this **['Duiven']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3123263.ttl#this **['Marcy']** 0.3273
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ118958.ttl#this **['Leuven']** 0.3062

***

The keyword search for `market-focused` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1391.ttl#this **['Maryland']** 0.3508
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ15833966.ttl#this **['Marin']** 0.3145
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3123263.ttl#this **['Marcy']** 0.3145
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this **['Maxim Integrated']** 0.2615
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ58706.ttl#this **['Marcianise']** 0.2402

***

The keyword search for `market-oriented` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this **['Maxim Integrated']** 0.3651
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1391.ttl#this **['Maryland']** 0.3266
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ15833966.ttl#this **['Marin']** 0.2928
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3123263.ttl#this **['Marcy']** 0.2928
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ58706.ttl#this **['Marcianise']** 0.2236

***

The keyword search for `industry-leading` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1074.ttl#this **['Anyang Dingsheng Silicon Industry']** 0.4521
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2427371.ttl#this **['North Reading']** 0.3873
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1200.ttl#this **['Hoshine Silicon Industry Jiaxing Fab']** 0.3650
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ273949.ttl#this **['Roding']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this **['Hoshine Silicon Industry']** 0.3432

***

The keyword search for `industry-recognized` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this **['Hoshine Silicon Industry']** 0.3149
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ899.ttl#this **['Lingsen Precision Industries']** 0.2932
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ863462.ttl#this **['Suzhou Industrial Park']** 0.2810
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ687.ttl#this **['Industrial Technology Research Institute']** 0.2767
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ902.ttl#this **['Siliconware Precision Industries']** 0.2754

***

The keyword search for `industry-respected` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this **['Hoshine Silicon Industry']** 0.3236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ687.ttl#this **['Industrial Technology Research Institute']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ863462.ttl#this **['Suzhou Industrial Park']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ15912525.ttl#this **['Hsinchu Industrial Park']** 0.2828
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1201.ttl#this **['Hoshine Silicon Industry Luzhou Fab']** 0.2712

***

The keyword search for `globally` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1096.ttl#this **['GlobalWafers']** 0.5071
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this **['GlobalFoundries']** 0.4602
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ548.ttl#this **['GlobalFoundries Malta Fab']** 0.3651
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ551.ttl#this **['GlobalFoundries Dresden Fab']** 0.3523
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ550.ttl#this **['GlobalFoundries Vermont Fab']** 0.3523

***

The keyword search for `worldwide` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1109.ttl#this **['Wafer World']** 0.4623
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49243.ttl#this **['Riverside']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1102.ttl#this **['Wafer Works']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ54174.ttl#this **['Woburn']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1270.ttl#this **['Wafer Works Erlin Fab']** 0.2085

***

The keyword search for `international` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this **['ASM International']** 0.8293
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this **['Digi International']** 0.8083
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1149.ttl#this **['Koydo International']** 0.7888
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.7085
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ801.ttl#this **['International Test Solutions Reno Fab']** 0.6300

***

The keyword search for `global` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1096.ttl#this **['GlobalWafers']** 0.5669
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this **['GlobalFoundries']** 0.5145
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ548.ttl#this **['GlobalFoundries Malta Fab']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ551.ttl#this **['GlobalFoundries Dresden Fab']** 0.3939
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ550.ttl#this **['GlobalFoundries Vermont Fab']** 0.3939

***

Do not repeat actions.

***

The keyword search for `multinational` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this **['ASM International']** 0.4739
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this **['Digi International']** 0.4619
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1149.ttl#this **['Koydo International']** 0.4507
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1028.ttl#this **['Multibeam Corporation']** 0.4307
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.3985

***

The keyword search for `transnational` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this **['ASM International']** 0.4905
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this **['Digi International']** 0.4781
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1149.ttl#this **['Koydo International']** 0.4666
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.4125
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ801.ttl#this **['International Test Solutions Reno Fab']** 0.3668

***

The keyword search for `cross-border` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2729021.ttl#this **['Agder']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ192517.ttl#this **['Boulder']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49272.ttl#this **['Chandler']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ682.ttl#this **['Crocus Technology']** 0.2075

***

The keyword search for `overseas` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ773.ttl#this **['Overijssel']** 0.3651
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1114.ttl#this **['East Flanders']** 0.2449
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1507709.ttl#this **['Camas']** 0.2390
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1439.ttl#this **['Texas']** 0.2390
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ16557.ttl#this **['Dallas']** 0.2236

***

The keyword search for `foreign` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ34412.ttl#this **['Foshan']** 0.3750
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2363688.ttl#this **['Fornebu']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ790.ttl#this **['DXCorr Design']** 0.2739
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1146.ttl#this **['Valley Design']** 0.2739
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1085.ttl#this **['Fiven']** 0.2673

***

The keyword search for `non-domestic` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1097.ttl#this **['Okmetic']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ993575.ttl#this **['Novi']** 0.2265
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ20.ttl#this **['Norway']** 0.1961
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ47967.ttl#this **['North West England']** 0.1861
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ236.ttl#this **['Novatek']** 0.1849

***

The keyword search for `offshore` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ334.ttl#this **['Singapore']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ261.ttl#this **['Graphcore']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ237683.ttl#this **['Ome']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ248.ttl#this **['GalaxyCore']** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1151.ttl#this **['Onse']** 0.2887

***

The keyword search for `nearshore` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ759.ttl#this **['New Hampshire']** 0.3114
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ342.ttl#this **['NXP Fab Singapore']** 0.2767
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ334.ttl#this **['Singapore']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ261.ttl#this **['Graphcore']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ248.ttl#this **['GalaxyCore']** 0.2611

***

The keyword search for `onshore` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1151.ttl#this **['Onse']** 0.5443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#this **['Onsemi']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ334.ttl#this **['Singapore']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ261.ttl#this **['Graphcore']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ911717.ttl#this **['Ono']** 0.2981

***

The keyword search for `local` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49162.ttl#this **['Lowell']** 0.4009
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ482657.ttl#this **['Logan']** 0.2857
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ416988.ttl#this **['Loudi']** 0.2857
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ84.ttl#this **['London']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23939248.ttl#this **['London']** 0.2673

***

The keyword search for `regional` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ382458.ttl#this **['Regional Municipality of Halton']** 0.4954
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ175735.ttl#this **['Regional Municipality of Waterloo']** 0.4811
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2091778.ttl#this **['Central Region']** 0.4743
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2091502.ttl#this **['East Region']** 0.4385
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1061069.ttl#this **['Metro Vancouver Regional District']** 0.4276

***

The keyword search for `national` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this **['ASM International']** 0.5804
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this **['Digi International']** 0.5657
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1149.ttl#this **['Koydo International']** 0.5521
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.4881
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ801.ttl#this **['International Test Solutions Reno Fab']** 0.4340

***

The keyword search for `domestic` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1097.ttl#this **['Okmetic']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ154.ttl#this **['DDC']** 0.2828
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3861.ttl#this **['Doha']** 0.2582
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ669566.ttl#this **['Douliu']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ265.ttl#this **['Amlogic']** 0.2108

***

The keyword search for `in-country` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ133853.ttl#this **['Ingham County']** 0.4472
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ494254.ttl#this **['Elk County']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109820.ttl#this **['Ada County']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ488659.ttl#this **['Montgomery County']** 0.3311
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ188612.ttl#this **['Pest County']** 0.3203

***

The keyword search for `in-region` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2091502.ttl#this **['East Region']** 0.5262
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ231.ttl#this **['Walloon Region']** 0.5217
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ478465.ttl#this **['North Region']** 0.5071
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2228755.ttl#this **['North Region']** 0.5071
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ46070.ttl#this **['Plzeň Region']** 0.5071

***

The keyword search for `in-area` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ668.ttl#this **['India']** 0.4286
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ389562.ttl#this **['Inazawa']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1415.ttl#this **['Indiana']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ109.ttl#this **['Infinera']** 0.3586
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ252.ttl#this **['Indonesia']** 0.3419

***

The keyword search for `neighborhood` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2415892.ttl#this **['Norwood']** 0.4714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ991177.ttl#this **['Englewood']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ850812.ttl#this **['Newark']** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1227.ttl#this **['Nevada']** 0.2500

***

The keyword search for `community` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.4523
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6363765.ttl#this **['Kanksa community development block']** 0.4523
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1147.ttl#this **['Trinity']** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **['Cook County']** 0.3892
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ111174.ttl#this **['Collin County']** 0.3656

***

The keyword search for `society` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this **['Sony']** 0.4330
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ421974.ttl#this **['Stark County']** 0.2835
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ119.ttl#this **['Soraa']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ54072.ttl#this **['Suffolk County']** 0.2652
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ54065.ttl#this **['Suffolk County']** 0.2652

***

The keyword search for `economy` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4881126.ttl#this **['Beijing Economic and Technological Development Area']** 0.2428
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ877941.ttl#this **['Echizen']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ494254.ttl#this **['Elk County']** 0.2041
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ114843.ttl#this **['Erie County']** 0.1961
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ54076.ttl#this **['Essex County']** 0.1890

***

The keyword search for `market` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ15833966.ttl#this **['Marin']** 0.4286
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3123263.ttl#this **['Marcy']** 0.4286
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1391.ttl#this **['Maryland']** 0.3586
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55737.ttl#this **['Mabalacat']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ58706.ttl#this **['Marcianise']** 0.3273

***

Do not repeat actions.

***

The keyword search for `sector` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **['Seoul Semiconductor']** 0.5160
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ189710.ttl#this **['Selangor']** 0.4472
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1163.ttl#this **['Semiconductor Electronics']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this **['AKM Semiconductor']** 0.4056
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **['GTA Semiconductor']** 0.4056

***

The keyword search for `field` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ24214227.ttl#this **['Krefeld']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ33.ttl#this **['Finland']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ265412.ttl#this **['Radfeld']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1085.ttl#this **['Fiven']** 0.2857
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1145.ttl#this **['Fineeco']** 0.2520

***

The keyword search for `domain` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ59218.ttl#this **['Dongguan']** 0.3354
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3861.ttl#this **['Doha']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ161885.ttl#this **['Kingdom of Great Britain']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ515712.ttl#this **['Yulin']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ724.ttl#this **['Maine']** 0.2673

***

The keyword search for `area` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ816.ttl#this **['Arizona']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ259.ttl#this **['arm']** 0.3651
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ884.ttl#this **['South Korea']** 0.3397
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1175.ttl#this **['TBEA']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ206872.ttl#this **['Ajka']** 0.3333

***

The keyword search for `discipline` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ724.ttl#this **['Maine']** 0.3273
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49219.ttl#this **['Irvine']** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ823927.ttl#this **['Higashine']** 0.2611
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ858423.ttl#this **['Date']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ698162.ttl#this **['Rhine Province']** 0.2165

***

The keyword search for `specialty` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1156.ttl#this **['Silicon Specialists']** 0.4830
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1305.ttl#this **['Silicon Specialists Hayward Fab']** 0.3853
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this **['Sony']** 0.2582
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ421974.ttl#this **['Stark County']** 0.2535
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ54072.ttl#this **['Suffolk County']** 0.2372

***

The keyword search for `expertise` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ35775.ttl#this **['Boise']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ62.ttl#this **['Nexperia']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ189471.ttl#this **['Cupertino']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ58706.ttl#this **['Marcianise']** 0.2611
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ30027234.ttl#this **['Marcianise']** 0.2611

***

The keyword search for `knowledge` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ21713103.ttl#this **['Cambridge']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ350.ttl#this **['Cambridge']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49111.ttl#this **['Cambridge']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ48320.ttl#this **['Kobe']** 0.3086
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1467149.ttl#this **['Labège']** 0.2673

***

The keyword search for `skills` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1087.ttl#this **['Washington Mills']** 0.3563
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this **['Skyworks Solutions']** 0.2535
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ735.ttl#this **['Sentons']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2533908.ttl#this **['Fishkill']** 0.2390
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ223.ttl#this **['Synopsys']** 0.2390

***

The keyword search for `abilities` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6272.ttl#this **['Aachen cities region']** 0.3214
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ572472.ttl#this **['Anthisnes']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ95.ttl#this **['ABB']** 0.2697
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ806.ttl#this **['Akrion Technologies']** 0.2632
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10418.ttl#this **['Donau-Ries']** 0.2611

***

The keyword search for `capabilities` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1507709.ttl#this **['Camas']** 0.3145
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3249.ttl#this **['Calvados']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10418.ttl#this **['Donau-Ries']** 0.2402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6272.ttl#this **['Aachen cities region']** 0.2365

***

The keyword search for `competencies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.2774
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.2757
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ208812.ttl#this **['Corbeil-Essonnes']** 0.2615
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ274.ttl#this **['Ampere Computing']** 0.2615

***

The keyword search for `strengths` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ582447.ttl#this **['St. Marys']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ124661.ttl#this **['Strathclyde']** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ41358.ttl#this **['Styria']** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ144.ttl#this **['Seiko Instruments']** 0.2433

***

The keyword search for `weaknesses` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **['Tampines']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ208812.ttl#this **['Corbeil-Essonnes']** 0.2843
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ572472.ttl#this **['Anthisnes']** 0.2727

***

The keyword search for `opportunities` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ45.ttl#this **['Portugal']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10418.ttl#this **['Donau-Ries']** 0.2402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6272.ttl#this **['Aachen cities region']** 0.2365
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ878.ttl#this **['United Arab Emirates']** 0.2365
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **['MSE Supplies']** 0.2224

***

The keyword search for `threats` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ250.ttl#this **['Moore Threads']** 0.4303
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ288.ttl#this **['Tours']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1439.ttl#this **['Texas']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this **['Texas Instruments']** 0.2294
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ68959.ttl#this **['Thalwil']** 0.2222

***

The keyword search for `trends` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5254438.ttl#this **['Woodlands']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55.ttl#this **['Netherlands']** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2223.ttl#this **['Riau Islands']** 0.2835
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ47994.ttl#this **['East Midlands']** 0.2739
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ288.ttl#this **['Tours']** 0.2673

***

The keyword search for `challenges` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.3849
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10424.ttl#this **['Cham']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ334906.ttl#this **['Chachoengsao']** 0.3086
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ994523.ttl#this **['Changji']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ30002.ttl#this **['Chengdu']** 0.2887

***

The keyword search for `obstacles` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.3586
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ8522.ttl#this **['Ostalbkreis']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ65.ttl#this **['Los Angeles']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.2390

***

The keyword search for `barriers` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13744.ttl#this **['Batangas']** 0.3000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ807311.ttl#this **['Barbacena']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4874282.ttl#this **['Bayan Lepas']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ85.ttl#this **['BAE Systems']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1096.ttl#this **['GlobalWafers']** 0.2535

***

The keyword search for `hurdles` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ65.ttl#this **['Los Angeles']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2520

***

The keyword search for `difficulties` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this **['Diodes']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10418.ttl#this **['Donau-Ries']** 0.3086
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ797.ttl#this **['Deca Technologies']** 0.2453
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **['MSE Supplies']** 0.2143
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this **['Dream Chip Technologies']** 0.2138

***

The keyword search for `complexities` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ138.ttl#this **['Melexis']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.2774
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.2757
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ208812.ttl#this **['Corbeil-Essonnes']** 0.2615

***

The keyword search for `problems` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ18632185.ttl#this **['Premstätten']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ85.ttl#this **['BAE Systems']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ105.ttl#this **['D-Wave Systems']** 0.2372
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1085.ttl#this **['Prague']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1127.ttl#this **['Province of Liege']** 0.2176

***

The keyword search for `issues` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ802.ttl#this **['ISE Labs']** 0.3354
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ78.ttl#this **['IXYS']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ12559.ttl#this **['Isère']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1040.ttl#this **['Zeiss']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.2673

***

The keyword search for `concerns` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3834.ttl#this **['Constance']** 0.3814
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ677.ttl#this **['Bourns']** 0.3354
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ275.ttl#this **['Cerebras']** 0.3000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108058.ttl#this **['Contra Costa County']** 0.2936
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **['Cook County']** 0.2449

***

The keyword search for `needs` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.4286
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55.ttl#this **['Netherlands']** 0.4193
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ133.ttl#this **['Lumileds']** 0.3586
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ850812.ttl#this **['Newark']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1227.ttl#this **['Nevada']** 0.2673

***

The keyword search for `requirements` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1115.ttl#this **['American Elements']** 0.3679
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ144.ttl#this **['Seiko Instruments']** 0.3066
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this **['Texas Instruments']** 0.3066
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.2835
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ702196.ttl#this **['arrondissement of Rennes']** 0.2621

***

The keyword search for `demands` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5254438.ttl#this **['Woodlands']** 0.4558
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55.ttl#this **['Netherlands']** 0.4193
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2223.ttl#this **['Riau Islands']** 0.4041
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ47994.ttl#this **['East Midlands']** 0.3904
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23156.ttl#this **['Devon']** 0.2857

***

The keyword search for `expectations` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.3667
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this **['Skyworks Solutions']** 0.2988
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-iccad-NguyenD97 **['State transformation in event driven explicit simulation.']** 0.2896
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ801.ttl#this **['International Test Solutions Reno Fab']** 0.2853
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1044.ttl#this **['LG Chem Water Solutions']** 0.2673

***

The keyword search for `standards` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ847607.ttl#this **['Sanda']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1095.ttl#this **['Standford Advanced Materials']** 0.3303
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ582447.ttl#this **['St. Marys']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5254438.ttl#this **['Woodlands']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55.ttl#this **['Netherlands']** 0.2509

***

The keyword search for `criteria` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ62.ttl#this **['Nexperia']** 0.4000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ41358.ttl#this **['Styria']** 0.3354
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ980.ttl#this **['Bavaria']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ40.ttl#this **['Austria']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1903.ttl#this **['Catania']** 0.3162

***

The keyword search for `benchmarks` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ184.ttl#this **['Belarus']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1102.ttl#this **['Wafer Works']** 0.2509
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ921.ttl#this **['Besi']** 0.2462
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ677.ttl#this **['Bourns']** 0.2132
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ64.ttl#this **['Berlin']** 0.2132

***

The keyword search for `metrics` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13580.ttl#this **['Metro Manila']** 0.3563
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-dac-AlpertLKD03 **['Delay and slew metrics using the lognormal distribution.']** 0.3443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#journals-tcad-AlpertLKD04 **['Closed-form delay and slew metrics made easy.']** 0.3404
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1061069.ttl#this **['Metro Vancouver Regional District']** 0.3381
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ138.ttl#this **['Melexis']** 0.3333

***

The keyword search for `measures` returned the following ranked list with hits.

    http://purl.org/linked-data/cube#MeasureProperty **['Measure property', 'The class of components which represent the measured value of the phenomenon being observed.']** 0.3591
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.3586
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ138.ttl#this **['Melexis']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ151.ttl#this **['MegaChips']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **['MSE Supplies']** 0.2535

***

The keyword search for `indicators` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ668.ttl#this **['India']** 0.4364
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1415.ttl#this **['Indiana']** 0.3849
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ589.ttl#this **['NHanced Semiconductors Indiana Fab']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ252.ttl#this **['Indonesia']** 0.2611
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ72.ttl#this **['Win Semiconductors']** 0.2582

***

The keyword search for `parameters` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ17182.ttl#this **['Parañaque']** 0.3636
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4259440.ttl#this **['Pasir Ris']** 0.2727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-dac-RaoDBS04 **['Parametric yield estimation considering leakage variability.']** 0.2680
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1122.ttl#this **['Pam-Xiamen']** 0.2611
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ42153.ttl#this **['Paju']** 0.2462

***

The keyword search for `variables` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-glvlsi-DartuDM05 **['Variability modeling and variability-aware design in deep submicron integrated circuits.']** 0.3079
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ980.ttl#this **['Bavaria']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ65.ttl#this **['Los Angeles']** 0.2509

***

The keyword search for `factors` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ72.ttl#this **['Win Semiconductors']** 0.3727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#this **['NXP Semiconductors']** 0.3727
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ710.ttl#this **['Truly Semiconductors']** 0.3553
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this **['NHanced Semiconductors']** 0.3402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ131.ttl#this **['Osram Opto Semiconductors']** 0.3208

***

The keyword search for `elements` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1115.ttl#this **['American Elements']** 0.6529
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ144.ttl#this **['Seiko Instruments']** 0.3627
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this **['Texas Instruments']** 0.3627
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ81.ttl#this **['Everlight Electronics']** 0.2638
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ316.ttl#this **['Texas Instruments Assembly/Test Aguascalientes']** 0.2631

***

The keyword search for `components` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.2887
    http://purl.org/linked-data/cube#DimensionProperty **['The class of components which represent the dimensions of the cube.', 'Dimension property']** 0.2753
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ144.ttl#this **['Seiko Instruments']** 0.2649
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1115.ttl#this **['American Elements']** 0.2649
    http://purl.org/linked-data/cube#AttributeProperty **['The class of components which represent attributes of observations in the cube, e.g. unit of measurement.', 'Attribute property']** 0.2649

***

The keyword search for `aspects` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1156.ttl#this **['Silicon Specialists']** 0.3086
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this **['ASML']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ42114.ttl#this **['Asan']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ986.ttl#this **['AOI Electronics  Assembly/Test Takamatsu']** 0.2665
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ914.ttl#this **['AOI Electronics']** 0.2572

***

The keyword search for `facets` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1196.ttl#this **['Fiven Barbacena Fab']** 0.2474
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ547071.ttl#this **['Farnborough']** 0.2097
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ482.ttl#this **['Fuji Electric Fab Philippines']** 0.2037
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalAssets **['Observed total assets key figure of an enterprise.', 'total assets']** 0.1992
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ771.ttl#this **['Massachusetts']** 0.1952

***

The keyword search for `dimensions` returned the following ranked list with hits.

    http://purl.org/linked-data/cube#DimensionProperty **['The class of components which represent the dimensions of the cube.', 'Dimension property']** 0.4756
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this **['Diodes']** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ735.ttl#this **['Sentons']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ249.ttl#this **['Smartsens']** 0.2611
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this **['Skyworks Solutions']** 0.2582

***

The keyword search for `perspectives` returned the following ranked list with hits.

    http://xmlns.com/foaf/0.1/Person **['A person.', 'Person']** 0.3474
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2197371.ttl#this **['Perai']** 0.3030
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ188953.ttl#this **['Perak']** 0.3030
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#this **['Everspin Technologies']** 0.2229
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2224

***

The keyword search for `views` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ881.ttl#this **['Vietnam']** 0.4472
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486860.ttl#this **['Mountain View']** 0.3464
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1112.ttl#this **['Vital Materials']** 0.3254
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ123.ttl#this **['VisEra']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ712.ttl#this **['Vimicro']** 0.2981

***

The keyword search for `opinions` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ735.ttl#this **['Sentons']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this **['Skyworks Solutions']** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.2858
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1151.ttl#this **['Onse']** 0.2722
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1044.ttl#this **['LG Chem Water Solutions']** 0.2667

***

The keyword search for `beliefs` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ184.ttl#this **['Belarus']** 0.5443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1140130.ttl#this **['Belfast']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10686.ttl#this **['Belfast']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ31.ttl#this **['Belgium']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ921.ttl#this **['Besi']** 0.3333

***

The keyword search for `attitudes` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this **['Diodes']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ572472.ttl#this **['Anthisnes']** 0.2727
    http://www.w3.org/2003/01/geo/wgs84_pos#lat **['The WGS84 latitude of a SpatialThing (decimal degrees).', 'latitude']** 0.2586
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.2279
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.2279

***

The keyword search for `values` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1146.ttl#this **['Valley Design']** 0.2739
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this **['Rogue Valley Microdevices']** 0.2722
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2673

***

The keyword search for `principles` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.3273
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ65273.ttl#this **['Plan-les-Ouates']** 0.2801
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ65.ttl#this **['Los Angeles']** 0.2402

***

The keyword search for `goals` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1162.ttl#this **['JX Metals']** 0.4045
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1105.ttl#this **['ALB Materials']** 0.3464
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ723.ttl#this **['Ares Materials']** 0.3354
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1112.ttl#this **['Vital Materials']** 0.3254
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ983840.ttl#this **['Goleta']** 0.3162

***

The keyword search for `objectives` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this **['Diodes']** 0.2357

***

The keyword search for `targets` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1139.ttl#this **['Able Target Limited']** 0.3637
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13892.ttl#this **['Tarlac']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **['Tampines']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5285.ttl#this **['Tarlac City']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49255.ttl#this **['Tampa']** 0.2520

***

The keyword search for `priorities` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this **['HRL Laboratories']** 0.2722
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ806.ttl#this **['Akrion Technologies']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10418.ttl#this **['Donau-Ries']** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6272.ttl#this **['Aachen cities region']** 0.2462
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2402

***

The keyword search for `strategies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ124661.ttl#this **['Strathclyde']** 0.4003
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-iccd-DevganaR93 **['ACES: A Transient Simulation Strategy for Integrated Circuits.']** 0.3402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ794.ttl#this **['Stratus Automation']** 0.3227
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ903.ttl#this **['Integra Technologies']** 0.3077
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ106.ttl#this **['Skorpios Technologies']** 0.3010

***

The keyword search for `tactics` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ907.ttl#this **['Signetics']** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#this **['Synaptics']** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this **['Racyics']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1166.ttl#this **['Firebird Optics']** 0.3234
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **['Tampines']** 0.3162

***

The keyword search for `policies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10418.ttl#this **['Donau-Ries']** 0.2739
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **['MSE Supplies']** 0.2535
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ322792.ttl#this **['Porto']** 0.2390
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.2390

***

The keyword search for `procedures` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.3273
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#conf-iccd-FuSG89 **['Performance and microarchitecture of the i486TM processor.']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.2182
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2182

***

The keyword search for `processes` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-dac-SapatnekarHKDKMPS08 **['Reinventing EDA with manycore processors.']** 0.2759
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#conf-iccd-FuSG89 **['Performance and microarchitecture of the i486TM processor.']** 0.2725
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2509
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1199.ttl#this **['Hesse']** 0.2279
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1004241.ttl#this **['Essex']** 0.2279

***

The keyword search for `practices` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1085.ttl#this **['Prague']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#this **['Analog Devices']** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10445111.ttl#this **['Kanagawa Prefectural offices']** 0.2752
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2509
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this **['Advanced Micro Devices']** 0.2462

***

The keyword search for `methods` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ138.ttl#this **['Melexis']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ151.ttl#this **['MegaChips']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1162.ttl#this **['JX Metals']** 0.3198
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55.ttl#this **['Netherlands']** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13580.ttl#this **['Metro Manila']** 0.2835

***

The keyword search for `techniques` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ159.ttl#this **['NMB Technologies']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-islped-RaoBDB03 **['Efficient techniques for gate leakage estimation.']** 0.4042
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ797.ttl#this **['Deca Technologies']** 0.3974
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this **['Noel Technologies']** 0.3974
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ925.ttl#this **['3DiS Technologies']** 0.3974

***

The keyword search for `tools` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ288.ttl#this **['Tours']** 0.5071
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ43695.ttl#this **['Tocantins']** 0.4045
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1490.ttl#this **['Tokyo']** 0.3381
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1439.ttl#this **['Texas']** 0.3381
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1159.ttl#this **['Topsil']** 0.3162

***

The keyword search for `instruments` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ144.ttl#this **['Seiko Instruments']** 0.7635
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this **['Texas Instruments']** 0.7635
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ315.ttl#this **['Texas Instruments Miho Fab']** 0.5766
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ311.ttl#this **['Texas Instruments Lehi Fab']** 0.5766
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ314.ttl#this **['Texas Instruments Aizu Fab']** 0.5766

***

The keyword search for `devices` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#this **['Analog Devices']** 0.6667
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this **['Advanced Micro Devices']** 0.5443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ157.ttl#this **['Nisshinbo Micro Devices']** 0.5333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ335.ttl#this **['Analog Devices Assembly/Test Philippines']** 0.4523
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this **['Rogue Valley Microdevices']** 0.4491

***

The keyword search for `equipment` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1023 **['Equipment manufacturer', 'Company that produces equipment for semiconductor manufacturing.']** 0.5024
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1022.ttl#this **['Shanghai Micro Electronics Equipment']** 0.4891
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1025.ttl#this **['Advanced Micro-Fabrication Equipment']** 0.4891
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this **['Cyient']** 0.3198
    http://xmlns.com/foaf/0.1/Document **['Document', 'A document.']** 0.2974

***

The keyword search for `machinery` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ100.ttl#this **['Magnachip']** 0.3636
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ724.ttl#this **['Maine']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3123263.ttl#this **['Marcy']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ97.ttl#this **['Macronix']** 0.2860
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ492.ttl#this **['Hitachi Fab Haramachi']** 0.2799

***

The keyword search for `systems` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ85.ttl#this **['BAE Systems']** 0.7396
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ105.ttl#this **['D-Wave Systems']** 0.6667
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ273.ttl#this **['Espressif Systems']** 0.6118
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this **['Silex Microsystems']** 0.5963
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ701.ttl#this **['Silicon Integrated Systems']** 0.5669

***

The keyword search for `technologies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ159.ttl#this **['NMB Technologies']** 0.8189
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ797.ttl#this **['Deca Technologies']** 0.7971
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this **['Noel Technologies']** 0.7971
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ925.ttl#this **['3DiS Technologies']** 0.7971
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ806.ttl#this **['Akrion Technologies']** 0.7582

***

The keyword search for `solutions` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this **['Skyworks Solutions']** 0.7416
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.6205
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1044.ttl#this **['LG Chem Water Solutions']** 0.6030
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#this **['MACOM Technology Solutions']** 0.5698
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ729.ttl#this **['Micross Silicon Turnkey Solutions']** 0.5096

***

The keyword search for `products` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1060 **['Materials producer', 'Company that produces equipment for semiconductor manufacturing.']** 0.3686
    https://welektronik.iis.fraunhofer.de/entity/Q291 **['Foundry Service', 'Producing semiconductors for others.']** 0.3239
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['Enterprise', 'An enterprise sells products to customers.']** 0.2902
    https://welektronik.iis.fraunhofer.de/entity/Q297 **['Chip fab', 'Site of a company that produces semiconductors.']** 0.2834
    https://welektronik.iis.fraunhofer.de/entity/Q286 **['Company that designs or/and sells semiconductors but does not produce them.', 'Fabless']** 0.2609

***

The keyword search for `services` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **['provides service', 'A service offered to (potential) customers.']** 0.4685
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#this **['Analog Devices']** 0.3953
    https://welektronik.iis.fraunhofer.de/entity/Q293 **['An offer by an organization.', 'Service']** 0.3300
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this **['Advanced Micro Devices']** 0.3227
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ735.ttl#this **['Sentons']** 0.3162

***

The keyword search for `offerings` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49258.ttl#this **['Colorado Springs']** 0.3553
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ898.ttl#this **['UTAC Holdings']** 0.3114
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1178.ttl#this **['Angstrom Engineering']** 0.2571
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ19807.ttl#this **['Kings Langley']** 0.2335
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ148.ttl#this **['Olympus']** 0.2010

***

The keyword search for `deliverables` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.3145
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this **['Diodes']** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ342451.ttl#this **['Red River Delta']** 0.2691
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ797.ttl#this **['Deca Technologies']** 0.2545

***

The keyword search for `outcomes` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ237683.ttl#this **['Ome']** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.2357

***

The keyword search for `results` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.3750
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49225.ttl#this **['Reno']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this **['Rambus']** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ40.ttl#this **['Realtek']** 0.2357

***

The keyword search for `impacts` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1119.ttl#this **['InPACT']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-vlsid-DevganN05 **['Power Variability and Its Impact on Design.']** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ78.ttl#this **['IXYS']** 0.2722
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ857266.ttl#this **['Imari']** 0.2520
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ707.ttl#this **['IC Plus']** 0.2222

***

The keyword search for `effects` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ716.ttl#this **['EFFECT Photonics']** 0.5500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-iccad-DevganJD00 **['How to Efficiently Capture On-Chip Inductance Effects: Introducing a New Circuit Element K.']** 0.2628
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-aspdac-JiDD01 **['KSim: a stable and efficient RKC simulator for capturing on-chip inductance effect.']** 0.2420
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ123376.ttl#this **['Ehime Prefecture']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-iccad-Devgan97 **['Efficient coupled noise estimation for on-chip interconnects.']** 0.2100

***

The keyword search for `consequences` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3834.ttl#this **['Constance']** 0.4181
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ661216.ttl#this **['Wil Constituency']** 0.3269
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **['Crolles']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ208812.ttl#this **['Corbeil-Essonnes']** 0.2615
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108058.ttl#this **['Contra Costa County']** 0.2575

***

The keyword search for `ramifications` returned the following ranked list with hits.

    https://dblp.org/rdf/schema#Publication **['A publication.', 'Publication']** 0.3818
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this **['Rambus']** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ795.ttl#this **['Verification Technology']** 0.3742
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.3667
    https://dblp.org/rdf/schema#Creator **['Publication', 'A creator of a publication.']** 0.3341

***

The keyword search for `repercussions` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.2739
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ159.ttl#this **['Russia']** 0.2739
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ735.ttl#this **['Sentons']** 0.2582
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this **['Skyworks Solutions']** 0.2309
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.2214

***

The keyword search for `reactions` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ666.ttl#this **['Actions Semiconductor']** 0.3772
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this **['International Test Solutions']** 0.3620
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this **['Skyworks Solutions']** 0.3371
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ801.ttl#this **['International Test Solutions Reno Fab']** 0.3219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.3198

***

The keyword search for `responses` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.4264
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **['Ypres']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49225.ttl#this **['Reno']** 0.2462
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1151.ttl#this **['Onse']** 0.2462
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ25.ttl#this **['Wales']** 0.2279

***

Think: The search results provide a list of companies and regions related to the semiconductor industry. However, the results are not very specific and do not directly answer the question about large customers of TSMC.

Act: fail('Unable to find large customers of TSMC.')

{'loop': {'id': '67d21b6a', 'question': 'Large customers of TSMC', 'iterations': 5, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?customer WHERE { ?customer tbox:customerOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> }', 'elapsed_time': 557662}, 'tokens': {'prompt_tokens': 72115, 'completion_tokens': 1623, 'elapsed_time_model': 192615, 'tokens_per_sec': 382.82510837667235}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}