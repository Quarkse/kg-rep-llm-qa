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

Potential services of companies

***

Think: The user is asking about potential services that companies can offer. To formulate a query, we need to identify key resources related to companies and services. We can start by searching for keywords like "company" and "service" to find relevant URIs.

Act: search('company') | search('service')

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.5333
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Foundry', 'Company that produces semiconductors for other companies.']** 0.5153
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **['Taiwan Semiconductor Manufacturing Company']** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **['Canyon County']** 0.3443

***

The keyword search for `service` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **['A service offered to (potential) customers.', 'provides service']** 0.5698
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#serviceProvidedBy **['An organization that offers the service to (potential) customers.', 'service provided by']** 0.4856
    https://welektronik.iis.fraunhofer.de/entity/Q293 **['An offer by an organization.', 'Service']** 0.4472
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ246.ttl#this **['GigaDevice']** 0.3849
    https://welektronik.iis.fraunhofer.de/entity/Q291 **['Foundry Service', 'Producing semiconductors for others.']** 0.3841

***

Think: We have found some relevant URIs for "company" and "service". We can now dereference these URIs to gather more information about the resources and their properties. This will help us to construct a query to find potential services offered by companies.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService') | deref('https://welektronik.iis.fraunhofer.de/entity/Q293') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this')

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
        rdfs:range <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        owl:inverseOf tbox:serviceProvidedBy .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q293` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix skos: <http://www.w3.org/2004/02/skos/core#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q293> a rdfs:Class ;
        rdfs:label "Service"@en ;
        rdfs:comment "An offer by an organization."@en ;
        rdfs:subClassOf skos:Concept .
    
    <https://www.w3.org/ns/org#Organization> a rdfs:Class ;
        rdfs:label "Organization"@en .
    
    tbox:providesService a owl:ObjectProperty ;
        rdfs:label "provides service"@en ;
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://welektronik.iis.fraunhofer.de/entity/Q293> .
    
    tbox:serviceProvidedBy a owl:ObjectProperty ;
        rdfs:label "service provided by"@en ;
        rdfs:domain <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:range <https://www.w3.org/ns/org#Organization> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix ns2: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#headquarter> tbox:registeredSiteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1060> tbox:organizationTypeOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns2:Organization ;
        rdfs:label "Active Business Company"@en ;
        ns1:locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ279128.ttl#this> ;
        owl:sameAs <http://www.wikidata.org/entity/Q124743799>,
            <https://welektronik.iis.fraunhofer.de/entity/Q1104> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> ;
        ns2:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#headquarter> .

***

Think: We have gathered more information about the resources and their properties. We can now construct a query to find potential services offered by companies. We will use the `providesService` property to find services offered by organizations.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service ?organization WHERE { ?organization a org:Organization . ?organization tbox:providesService ?service . }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service ?organization WHERE { ?organization a org:Organization . ?organization tbox:providesService ?service . }' returned the following solution (first 20 results).
    service,organization
    https://welektronik.iis.fraunhofer.de/entity/Q292,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ734.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ922.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ125.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q288,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q292,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ75.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ805.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ905.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ917.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ917.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ923.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ925.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ927.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ929.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this

***

Think: We have successfully executed the query and obtained the results. We can now confirm the query as final and provide a concise message explaining the relevant steps we took.

Act: success('The query to find potential services offered by companies has been successfully executed, and the results have been obtained.')

{'loop': {'id': '67d2a475', 'question': 'Potential services of companies', 'iterations': 4, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service ?organization WHERE { ?organization a org:Organization . ?organization tbox:providesService ?service . }', 'elapsed_time': 32515}, 'tokens': {'prompt_tokens': 9346, 'completion_tokens': 413, 'elapsed_time_model': 25982, 'tokens_per_sec': 375.6003797166865}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}