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

Potential services of companies

***

Think: The user is asking about potential services that companies can offer. This is a broad topic, and I need to identify key resources and find relevant URIs to gather more information. I will start by searching for keywords related to company services.

Act: search('company services') | search('business services') | search('enterprise services')

***

The keyword search for `company services` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Foundry', 'Company that produces semiconductors for other companies.']** 0.4165
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **['A service offered to (potential) customers.', 'provides service']** 0.3492
    https://welektronik.iis.fraunhofer.de/entity/Q285 **['Company that designs, produces and sells semiconductors.', 'Integrated Device Manufacturer']** 0.3368
    https://welektronik.iis.fraunhofer.de/entity/Q297 **['Chip fab', 'Site of a company that produces semiconductors.']** 0.3320
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.3300

***

The keyword search for `business services` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.3671
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **['A service offered to (potential) customers.', 'provides service']** 0.3660
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **['Tampines']** 0.2902
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#this **['Analog Devices']** 0.2868
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ335.ttl#this **['Analog Devices Assembly/Test Philippines']** 0.2767

***

The keyword search for `enterprise services` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['An enterprise sells products to customers.', 'Enterprise']** 0.5757
    https://welektronik.iis.fraunhofer.de/entity/Q1045 **['Classification of enterprise size.', 'Enterprise size']** 0.5577
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#observedEnterprise **['observed enterprise', 'Enterprise/organization that an observed key figure is about.']** 0.4821
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier **['Links the supplying enterprise in a supply flow between two enterprises.', 'supplier']** 0.3858
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['customer', 'Links the customer enterprise in a supply flow between two enterprises.']** 0.3833

***

Think: The search results have returned several relevant URIs related to company services, including https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService, which defines a service offered to customers. I will dereference this URI to gather more information about the properties and relationships related to company services.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService')

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q293> a rdfs:Class ;
        rdfs:label "Service"@en .
    
    <https://www.w3.org/ns/org#Organization> a rdfs:Class ;
        rdfs:label "Organization"@en .
    
    tbox:providesService a owl:ObjectProperty ;
        rdfs:label "provides service"@en ;
        rdfs:comment "A service offered to (potential) customers."@en ;
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://welektronik.iis.fraunhofer.de/entity/Q293> .

***

Think: The dereferenced URI provides information about the `providesService` property, which has a domain of `Organization` and a range of `Service`. This suggests that companies can offer various services to their customers. I will query the knowledge graph to find specific services offered by companies.

Act: query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service WHERE { ?company a org:Organization . ?company :providesService ?service . }')

***

The query 'PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service WHERE { ?company a org:Organization . ?company :providesService ?service . }' returned the following solution.

    service
    https://welektronik.iis.fraunhofer.de/entity/Q288
    https://welektronik.iis.fraunhofer.de/entity/Q290
    https://welektronik.iis.fraunhofer.de/entity/Q291
    https://welektronik.iis.fraunhofer.de/entity/Q289
    https://welektronik.iis.fraunhofer.de/entity/Q292

***

Think: The query results have returned several services offered by companies, including https://welektronik.iis.fraunhofer.de/entity/Q288, https://welektronik.iis.fraunhofer.de/entity/Q290, https://welektronik.iis.fraunhofer.de/entity/Q291, https://welektronik.iis.fraunhofer.de/entity/Q289, and https://welektronik.iis.fraunhofer.de/entity/Q292. I will dereference these URIs to gather more information about the specific services.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q288') | deref('https://welektronik.iis.fraunhofer.de/entity/Q290') | deref('https://welektronik.iis.fraunhofer.de/entity/Q291') | deref('https://welektronik.iis.fraunhofer.de/entity/Q289') | deref('https://welektronik.iis.fraunhofer.de/entity/Q292')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q288` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ104.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ129.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ141.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ152.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ162.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ164.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ169.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ237.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ276.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ48.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ49.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ51.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ52.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ63.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ669.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ677.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ678.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ682.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ692.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ696.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ72.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ720.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ73.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ77.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ83.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ86.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q288> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Design"@en ;
        rdfs:comment "Design of semiconductors."@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q290` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ104.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ129.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ151.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ157.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ161.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ169.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ38.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ50.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ53.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ676.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ677.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ678.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ716.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ72.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ720.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ77.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ86.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ88.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ880.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ882.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ888.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ894.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ895.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ896.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ897.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ898.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ899.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ900.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ901.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ902.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ903.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ904.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ907.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ909.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ910.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ911.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ912.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ913.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ914.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ915.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ916.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ917.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ921.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ922.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ923.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ925.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ927.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ929.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ930.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q290> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q290> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Packaging"@en ;
        rdfs:comment "Assembly and packaging of semiconductors."@en .

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
        rdfs:comment "Producing semiconductors for others."@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q289` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ129.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ151.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ152.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ161.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ169.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ38.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ49.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ50.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ51.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ53.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ676.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ678.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ716.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ72.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ720.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ78.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ802.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ805.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ83.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ86.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ88.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ880.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ882.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ888.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ894.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ895.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ896.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ897.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ898.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ899.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ900.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ901.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ902.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ903.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ904.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ905.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ907.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ908.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ909.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ910.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ911.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ912.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ913.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ914.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ915.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ916.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ917.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ918.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ919.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ924.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ926.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ928.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ930.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q289> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Testing"@en ;
        rdfs:comment "Testing of semiconductors."@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q292` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ141.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ151.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ178.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ223.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ237.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ259.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ276.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ277.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ46.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ48.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ49.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ50.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ51.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ52.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ53.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ63.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ720.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ726.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ734.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ76.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ77.ttl#this> tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q292> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q292> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "IP-Core"@en ;
        rdfs:comment "Reusable unit of integrated circuit layout design."@en .

***

Think: The descriptions of the services provided by companies have been retrieved. The services include Design, Packaging, Foundry Service, Testing, and IP-Core. I will now provide a final answer to the user's question.

Act: success('Companies can offer various services, including design, packaging, foundry services, testing, and IP-Core.')

{'loop': {'id': '67d20f2f', 'question': 'Potential services of companies', 'iterations': 5, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service WHERE { ?company a org:Organization . ?company :providesService ?service . }', 'elapsed_time': 74333}, 'tokens': {'prompt_tokens': 30753, 'completion_tokens': 636, 'elapsed_time_model': 66439, 'tokens_per_sec': 472.44183574447015}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}