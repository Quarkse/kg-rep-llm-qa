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

Fabless suppliers of TSMC

***

Think: The user is asking about fabless suppliers of TSMC, which refers to companies that design and sell semiconductor products without manufacturing them themselves, relying on external foundries like TSMC for production. To formulate a query, we need to identify key resources such as TSMC, fabless suppliers, and relevant relationships between them.

Act: search('TSMC') | search('fabless supplier') | search('semiconductor foundry')

***

The keyword search for `TSMC` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this **HLMC** 0.4082
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ13892.ttl#this **Tarlac** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ253.ttl#this **Tsinghua Unigroup** 0.2294
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this **TDK** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ154.ttl#this **DDC** 0.2236

***

The keyword search for `fabless supplier` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier **supplier** 0.6708
    https://welektronik.iis.fraunhofer.de/entity/Q286 **Fabless** 0.6285
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **MSE Supplies** 0.3780
    https://purl.org/supply-network/onto#SupplyFlow **Supply Flow** 0.2615
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6441.ttl#this **Montpellier** 0.2615

***

The keyword search for `semiconductor foundry` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **Seoul Semiconductor** 0.6522
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this **GCT Semiconductor** 0.6219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **GTA Semiconductor** 0.6219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this **AKM Semiconductor** 0.6219
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this **CISC Semiconductor** 0.6061

***

Think: The search results provide some relevant information, including potential URIs for TSMC, fabless suppliers, and semiconductor foundries. However, none of the results directly point to TSMC or its fabless suppliers. We need to further expand our search and explore the relationships between these entities.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q286') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this') | search('TSMC fabless')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q286` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q286> a tbox:OrganizationType ;
        rdfs:label "Fabless"@en .

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

The keyword search for `TSMC fabless` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q286 **Fabless** 0.7698
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ438.ttl#this **TDK Texas Fab** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ582.ttl#this **Teledyne DALSA Quebec Fab** 0.2222
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ479.ttl#this **Teledyne e2v Fab Grenoble** 0.2222
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ480.ttl#this **Fuji Electric Fab Tsugaru** 0.2222

***

Think: The search results provide some relevant information, including potential URIs for fabless suppliers and semiconductor foundries. However, none of the results directly point to TSMC or its fabless suppliers. We need to further expand our search and explore the relationships between these entities.

Act: search('TSMC customer') | search('fabless company') | deref('https://welektronik.iis.fraunhofer.de/entity/Q286')

***

The keyword search for `TSMC customer` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **customer** 0.7894
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2729021.ttl#this **Agder** 0.2097
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ9924.ttl#this **Haarlemmermeer** 0.2080
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ192517.ttl#this **Boulder** 0.1849
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ131438.ttl#this **Munster** 0.1849

***

The keyword search for `fabless company` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q286 **Fabless** 0.6468
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5336
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ663.ttl#this **Taiwan Semiconductor Manufacturing Company  Washington Fab** 0.3080
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ220005.ttl#this **Daviess County** 0.3032
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ115148.ttl#this **Dutchess County** 0.2941

***

Do not repeat actions.

***

Think: The search results provide some relevant information, including potential URIs for TSMC customers and fabless companies. However, none of the results directly point to TSMC or its fabless suppliers. We need to further expand our search and explore the relationships between these entities.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType ; :label ?y . FILTER regex(?y, "fabless", "i") }') | search('TSMC') | search('semiconductor manufacturing') | search('company') | search('customer') | search('supplier') | search('foundry')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType ; :label ?y . FILTER regex(?y, "fabless", "i") }')`.

***

Do not repeat actions.

***

The keyword search for `semiconductor manufacturing` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.7559
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this **Taiwan Semiconductor Manufacturing Company Nanjing Fab** 0.6952
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this **Taiwan Semiconductor Manufacturing Company Hsinchu Fab** 0.6700
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this **Semiconductor Manufacturing International Corporation** 0.6657
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ662.ttl#this **Taiwan Semiconductor Manufacturing Company Shanghai Fab** 0.6641

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **Canyon County** 0.3443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **Cook County** 0.3443

***

The keyword search for `customer` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **customer** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ49272.ttl#this **Chandler** 0.3000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2729021.ttl#this **Agder** 0.2390
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ9924.ttl#this **Haarlemmermeer** 0.2372
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ192517.ttl#this **Boulder** 0.2108

***

The keyword search for `supplier` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier **supplier** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **MSE Supplies** 0.5071
    https://purl.org/supply-network/onto#SupplyFlow **Supply Flow** 0.4385
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ6441.ttl#this **Montpellier** 0.3508
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ846338.ttl#this **Suwa** 0.2582

***

The keyword search for `foundry` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **Foundry** 1.0000
    https://welektronik.iis.fraunhofer.de/entity/Q291 **Foundry Service** 0.6468
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ838769.ttl#this **Fountain Valley** 0.4042
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this **GlobalFoundries** 0.3234
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ548.ttl#this **GlobalFoundries Malta Fab** 0.2566

***

Think: The search results provide some relevant information, including potential URIs for semiconductor manufacturing companies, customers, suppliers, and foundries. We have found a URI for Taiwan Semiconductor Manufacturing Company, which is the company the user is asking about. We can use this URI to formulate a query to find fabless suppliers of TSMC.

Act: query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :company/weQ20.ttl#this tbox:providesService ?x . ?x a tbox:ServiceType ; tbox:serviceType :serviceType_1 . }') | query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType ; :label ?y . FILTER regex(?y, "fabless", "i") }') | query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :company/weQ20.ttl#this tbox:hasCustomer ?x . }') | query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :company/weQ20.ttl#this tbox:hasSupplier ?x . }') | query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :company/weQ20.ttl#this tbox:hasFoundry ?x . }') | query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType ; tbox:organizationType :organizationType_1 . }')

***

Error in `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :company/weQ20.ttl#this tbox:providesService ?x . ?x a tbox:ServiceType ; tbox:serviceType :serviceType_1 . }'). Expected SelectQuery, found ':'  (at char 249), (line:1, col:250)

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType ; :label ?y . FILTER regex(?y, "fabless", "i") }')`.

***

Error in `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :company/weQ20.ttl#this tbox:hasCustomer ?x . }'). Expected SelectQuery, found ':'  (at char 249), (line:1, col:250)

***

Error in `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :company/weQ20.ttl#this tbox:hasSupplier ?x . }'). Expected SelectQuery, found ':'  (at char 249), (line:1, col:250)

***

Error in `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :company/weQ20.ttl#this tbox:hasFoundry ?x . }'). Expected SelectQuery, found ':'  (at char 249), (line:1, col:250)

***

No results for `query('PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType ; tbox:organizationType :organizationType_1 . }')`.

***

Think: The search results provide some relevant information, including potential URIs for semiconductor manufacturing companies, customers, suppliers, and foundries. We have found a URI for Taiwan Semiconductor Manufacturing Company, which is the company the user is asking about. However, we were unable to find any fabless suppliers of TSMC using the given actions.

Act: fail('Unable to find fabless suppliers of TSMC.')

{'loop': {'id': '67d08a6f', 'question': 'Fabless suppliers of TSMC', 'iterations': 6, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType ; tbox:organizationType :organizationType_1 . }', 'elapsed_time': 98789}, 'tokens': {'prompt_tokens': 19832, 'completion_tokens': 1309, 'elapsed_time_model': 77711, 'tokens_per_sec': 272.0435524052248}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}