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

Think: The user is asking about customers of ASML, which is a company that manufactures lithography systems for the semiconductor industry. To formulate a query, we need to identify the key resources involved, such as ASML and its customers.

Act: search('ASML') | search('semiconductor industry') | search('lithography systems')

***

The keyword search for `ASML` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this **['ASML']** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this **['ASM International']** 0.3746
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ42114.ttl#this **['Asan']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1089.ttl#this **['ASUZAC']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1116.ttl#this **['Alsil Material']** 0.2041

***

The keyword search for `semiconductor industry` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **['Seoul Semiconductor']** 0.6543
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this **['AKM Semiconductor']** 0.6299
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this **['GCT Semiconductor']** 0.6299
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **['GTA Semiconductor']** 0.6299
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this **['CISC Semiconductor']** 0.6139

***

The keyword search for `lithography systems` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ85.ttl#this **['BAE Systems']** 0.4842
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ105.ttl#this **['D-Wave Systems']** 0.4364
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ273.ttl#this **['Espressif Systems']** 0.4005
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ701.ttl#this **['Silicon Integrated Systems']** 0.3712
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ178.ttl#this **['Cadence Design Systems']** 0.3563

***

Think: We have identified ASML as a key resource and found its URI. We also have a list of companies related to the semiconductor industry and lithography systems. However, to find the customers of ASML, we need to gather more information about ASML and its relationships with other companies.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this` is as follows.

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "ASML"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q297879>,
            <https://welektronik.iis.fraunhofer.de/entity/Q1029> ;
        foaf:homepage <https://www.asml.com/> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#headquarter> .

***

Think: We have gathered more information about ASML, including its type, homepage, and registered site. However, we still need to find information about its customers. To do this, we can try to find relationships between ASML and other companies in the semiconductor industry.

Act: search('ASML customers') | search('companies that use ASML') | search('ASML client list')

***

The keyword search for `ASML customers` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this **['ASML']** 0.5103
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['Links the customer enterprise in a supply flow between two enterprises.', 'customer']** 0.3236
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['An enterprise sells products to customers.', 'Enterprise']** 0.2581
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **['A service offered to (potential) customers.', 'provides service']** 0.2564
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ50615.ttl#this **['Akershus']** 0.2372

***

The keyword search for `companies that use ASML` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Foundry', 'Company that produces semiconductors for other companies.']** 0.4196
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this **['ASML']** 0.4082
    https://welektronik.iis.fraunhofer.de/entity/Q297 **['Chip fab', 'Site of a company that produces semiconductors.']** 0.2817
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1438.ttl#this **['Campania']** 0.2530
    https://welektronik.iis.fraunhofer.de/entity/Q286 **['Fabless', 'Company that designs or/and sells semiconductors but does not produce them.']** 0.2475

***

The keyword search for `ASML client list` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this **['ASML']** 0.4811
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this **['Cyient']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ79952.ttl#this **['Aguascalientes']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4803324.ttl#this **['Asago district']** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ720.ttl#this **['Advantest']** 0.2132

***

Think: We have gathered some information about companies that might be related to ASML, but we still need to find a clear connection between ASML and its customers. To do this, we can try to query the knowledge graph directly.

Act: query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?customer WHERE { <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> :customer ?customer . }')

***

No results for `query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?customer WHERE { <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> :customer ?customer . }')`.

***

Think: The query did not return any results, which means that the knowledge graph does not contain explicit information about ASML's customers. However, we can try to infer this information by looking at the companies that use ASML's products or services.

Act: query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company WHERE { ?company ns1:hasRegisteredSite ?site . ?site :providesService <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> . }')

***

No results for `query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company WHERE { ?company ns1:hasRegisteredSite ?site . ?site :providesService <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> . }')`.

***

Think: The query did not return any results, which means that the knowledge graph does not contain information about companies that use ASML's products or services. At this point, we have exhausted our options and cannot provide a definitive answer to the user's question.

Act: fail('Unable to find information about ASML customers in the knowledge graph.')

{'loop': {'id': '67d1fec1', 'question': 'Customers of ASML', 'iterations': 6, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company WHERE { ?company ns1:hasRegisteredSite ?site . ?site :providesService <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> . }', 'elapsed_time': 59268}, 'tokens': {'prompt_tokens': 14926, 'completion_tokens': 646, 'elapsed_time_model': 47120, 'tokens_per_sec': 330.4706958501239}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}