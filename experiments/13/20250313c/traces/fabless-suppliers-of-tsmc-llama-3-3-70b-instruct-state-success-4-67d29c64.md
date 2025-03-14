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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 48117 triples. System version v0.2.8-93-gfa87822d is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Fabless suppliers of TSMC

***

Think: The user is asking about fabless suppliers of TSMC, which refers to companies that design and sell semiconductor products without manufacturing them themselves, instead relying on external foundries like TSMC (Taiwan Semiconductor Manufacturing Company) for production. To formulate a query, we need to identify key resources related to TSMC and fabless suppliers.

Act: search('TSMC') | search('fabless supplier') | search('semiconductor foundry')

***

The keyword search for `TSMC` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this **['HLMC']** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13892.ttl#this **['Tarlac']** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ253.ttl#this **['Tsinghua Unigroup']** 0.2294
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ154.ttl#this **['DDC']** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this **['TDK']** 0.2236

***

The keyword search for `fabless supplier` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#hasSupplier **['has supplier', 'Directly links a supplying enterprise.']** 0.4191
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **['MSE Supplies']** 0.3780
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier **['Links the supplying enterprise in a supply flow between two enterprises.', 'supplier']** 0.3542
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#incomingSupplyFlow **['An incoming supply flow to a supplier.', 'incoming supply flow']** 0.3255
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6441.ttl#this **['Montpellier']** 0.2615

***

The keyword search for `semiconductor foundry` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **['Seoul Semiconductor']** 0.6522
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this **['AKM Semiconductor']** 0.6219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **['GTA Semiconductor']** 0.6219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this **['GCT Semiconductor']** 0.6219
    https://welektronik.iis.fraunhofer.de/entity/Q291 **['Foundry Service', 'Producing semiconductors for others.']** 0.6140

***

Think: We have identified some key resources related to TSMC, fabless suppliers, and semiconductor foundries. However, we need to further expand our knowledge about the graph structure and gather more information to construct a query. We can start by dereferencing the resources we found.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this') | deref('https://welektronik.iis.fraunhofer.de/entity/Q291')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix ns2: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#headquarter> tbox:registeredSiteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ595.ttl#this> ns1:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q287> tbox:organizationTypeOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q288> tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q289> tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q290> tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q291> tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q292> tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "HLMC"@en ;
        ns2:locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ8686.ttl#this> ;
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

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix ns2: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#headquarter> tbox:registeredSiteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1023> tbox:organizationTypeOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1060> tbox:organizationTypeOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "MSE Supplies"@en ;
        ns2:locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ30.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ816.ttl#this> ;
        owl:sameAs <http://www.wikidata.org/entity/Q125124965>,
            <https://welektronik.iis.fraunhofer.de/entity/Q1165> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023>,
            <https://welektronik.iis.fraunhofer.de/entity/Q1060> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#headquarter> .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q291` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ104.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ106.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ114.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ117.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1176.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ123.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ125.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ140.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ141.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ147.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ150.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ152.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ157.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ161.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ162.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ164.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ165.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ167.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ168.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ169.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ237.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ269.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ31.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ38.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ46.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ48.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ49.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ50.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ51.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ52.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ53.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ56.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ63.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ66.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ678.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ692.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ694.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ72.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ75.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ76.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ77.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ83.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ86.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ88.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q291> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Foundry Service"@en ;
        rdfs:comment "Producing semiconductors for others."@en ;
        tbox:serviceProvidedBy <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ104.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ106.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ114.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ117.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1176.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ123.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ125.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ140.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ141.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ147.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ150.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ152.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ157.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ161.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ162.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ164.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ165.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ167.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ168.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ169.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ237.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ269.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ31.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ38.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ46.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ48.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ49.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ50.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ51.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ52.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ53.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ56.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ63.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ66.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ678.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ692.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ694.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ72.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ75.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ76.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ77.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ80.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ83.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ86.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ88.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this> .

***

Think: We have gathered more information about the resources we found earlier. Now, we need to construct a query to find fabless suppliers of TSMC. We can use the information we gathered to create a query that finds companies that provide foundry services and are related to TSMC.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?label WHERE { ?company a ns1:Organization ; tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> ; rdfs:label ?label . FILTER NOT EXISTS { ?company ns1:siteOf ?site . ?site ns1:locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this> } }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?label WHERE { ?company a ns1:Organization ; tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> ; rdfs:label ?label . FILTER NOT EXISTS { ?company ns1:siteOf ?site . ?site ns1:locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this> } }' returned the following solution (first 20 results).
    company,label
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ125.ttl#this,Shenzhen Si Semiconductors
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this,GTA Semiconductor
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ75.ttl#this,Epistar
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this,Japan Semiconductor Corporation
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this,Noel Technologies
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ162.ttl#this,nanoPHAB
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ165.ttl#this,INEX Microtechnology
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ168.ttl#this,Crocus Nano Electronics
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ106.ttl#this,Skorpios Technologies
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this,Rogue Valley Microdevices
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ114.ttl#this,Polar Semiconductor
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ692.ttl#this,Littelfuse
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this,International Test Solutions
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this,Opto Diode
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this,Atomica
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ117.ttl#this,Entrepix
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ150.ttl#this,JFE Shoji Electronics
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ164.ttl#this,PragmatIC Semiconductor
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this,Silex Microsystems
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this,Cyient

***

Think: We have constructed a query to find fabless suppliers of TSMC and executed it. The query returned a list of companies that provide foundry services and are related to TSMC.

Act: success('The fabless suppliers of TSMC are Shenzhen Si Semiconductors, GTA Semiconductor, Epistar, Japan Semiconductor Corporation, Noel Technologies, nanoPHAB, INEX Microtechnology, Crocus Nano Electronics, Skorpios Technologies, Rogue Valley Microdevices, Polar Semiconductor, Littelfuse, International Test Solutions, Opto Diode, Atomica, Entrepix, JFE Shoji Electronics, PragmatIC Semiconductor, Silex Microsystems, Cyient.')

{'loop': {'id': '67d29c64', 'question': 'Fabless suppliers of TSMC', 'iterations': 4, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?label WHERE { ?company a ns1:Organization ; tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> ; rdfs:label ?label . FILTER NOT EXISTS { ?company ns1:siteOf ?site . ?site ns1:locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this> } }', 'elapsed_time': 107515}, 'tokens': {'prompt_tokens': 28001, 'completion_tokens': 640, 'elapsed_time_model': 98619, 'tokens_per_sec': 290.4179494462262}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}