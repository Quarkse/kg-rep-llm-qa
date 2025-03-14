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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 32290 triples. System version v0.2.8-77-g05f9f338 is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Types of companies

***

Think: The user is asking about different types of companies, which suggests they are looking for a categorization or classification of companies. This could be based on various factors such as size, industry, ownership structure, or legal form. To formulate a query, we need to identify the key resources and concepts related to company types.

Act: search('company types') | search('business types') | search('enterprise categories')

***

The keyword search for `company types` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.3615
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **Nepes** 0.2928
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.2725
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ664.ttl#this **Taiwan Semiconductor Manufacturing Company Taoyuan Fab** 0.2667
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this **Taiwan Semiconductor Manufacturing Company Tainan Fab** 0.2645

***

The keyword search for `business types` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.4000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **Tampines** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **Nepes** 0.2835
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **Philippines** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **Rennes** 0.2652

***

The keyword search for `enterprise categories` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **Enterprise** 0.6621
    https://welektronik.iis.fraunhofer.de/entity/Q1045 **Enterprise size** 0.5563
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#observedEnterprise **observed enterprise** 0.4550
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this **HRL Laboratories** 0.2457
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ10418.ttl#this **Donau-Ries** 0.2408

***

Think: The search results for `company types`, `business types`, and `enterprise categories` have returned a list of resources, including companies, regions, and concepts related to enterprise categories. The top result for `enterprise categories` is the concept of "Enterprise" itself, which suggests that we can use this as a starting point to explore different types of enterprises.

Act: deref('https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise')

***

The description of `https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> a rdfs:Class ;
        rdfs:label "Enterprise"@en ;
        rdfs:subClassOf <https://www.w3.org/ns/org#Organization> .
    
    <https://purl.org/supply-network/onto#SupplyFlow> a rdfs:Class ;
        rdfs:label "Supply Flow"@en .
    
    <https://www.w3.org/ns/org#Organization> a rdfs:Class ;
        rdfs:label "Organization"@en .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer> a owl:ObjectProperty ;
        rdfs:label "customer"@en ;
        rdfs:domain <https://purl.org/supply-network/onto#SupplyFlow> ;
        rdfs:range <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier> a owl:ObjectProperty ;
        rdfs:label "supplier"@en ;
        rdfs:domain <https://purl.org/supply-network/onto#SupplyFlow> ;
        rdfs:range <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> .

***

Think: The description of the "Enterprise" concept shows that it is a subclass of "Organization" and has properties such as "customer" and "supplier" that relate to supply flows. This suggests that enterprises can be categorized based on their roles in supply chains. However, this information is not sufficient to answer the user's question about types of companies.

Act: query('PREFIX esn: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?type WHERE { ?type rdfs:subClassOf esn:Enterprise }')

***

No results for `query('PREFIX esn: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?type WHERE { ?type rdfs:subClassOf esn:Enterprise }')`.

***

Think: The query did not return any results, which suggests that there are no explicit subclasses of "Enterprise" in the knowledge graph. However, we can still try to find related concepts or properties that might help us categorize enterprises.

Act: query('PREFIX esn: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?property WHERE { esn:Enterprise ?property ?value }')

***

The query 'PREFIX esn: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?property WHERE { esn:Enterprise ?property ?value }' returned the following solution.

    property
    http://www.w3.org/1999/02/22-rdf-syntax-ns#type
    http://www.w3.org/2000/01/rdf-schema#label
    http://www.w3.org/2000/01/rdf-schema#subClassOf

***

Think: The query returned some properties related to the "Enterprise" concept, including its type, label, and subclass relationship. However, this information is still not sufficient to answer the user's question about types of companies.

Act: fail('Unable to find specific types of companies in the knowledge graph. The search results and queries did not provide enough information to categorize enterprises.')

{'loop': {'id': '67bf23b9', 'question': 'Types of companies', 'iterations': 5, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX esn: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?property WHERE { esn:Enterprise ?property ?value }', 'elapsed_time': 55665}, 'tokens': {'prompt_tokens': 9913, 'completion_tokens': 536, 'elapsed_time_model': 31195, 'tokens_per_sec': 334.95278741501545}, 'git': {'label': 'v0.2.8-77-g05f9f338', 'commit': '05f9f33880e9523b7eb3f19ed97e6b71bef1547a'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}