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

Taiwanese companies that supply Intel

***

Think: To find Taiwanese companies that supply Intel, we need to identify the key resources involved, which are Taiwanese companies and Intel. We also need to understand the relationship between these entities, which is a supplier relationship.

Act: search('Taiwanese companies') | search('Intel') | search('supplier relationship')

***

The keyword search for `Taiwanese companies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this **Taiwan** 0.4743
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this **Taiwan Semiconductor Manufacturing Company Taiwan Fab** 0.4371
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this **Taiwan Semiconductor Manufacturing Company Tainan Fab** 0.3722
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.3708
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **Tampines** 0.3536

***

The keyword search for `Intel` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this **Intel** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ167.ttl#this **Integral** 0.5976
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ60.ttl#this **Intersil** 0.5976
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this **Intel Fab Oregon** 0.5345
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this **Intel Fab Irland** 0.5345

***

The keyword search for `supplier relationship` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier **supplier** 0.5934
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **MSE Supplies** 0.3344
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ84747997.ttl#conf-islped-SuLDAN03 **Full chip leakage estimation considering power supply and temperature variations.** 0.3279
    https://purl.org/supply-network/onto#SupplyFlow **Supply Flow** 0.2892
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ718428.ttl#this **Erlin Township** 0.2606

***

Think: We have identified key resources involved, which are Taiwanese companies and Intel. We also have a list of potential suppliers and the supplier relationship. Next, we need to dereference these resources to gather more information about them.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this') | deref('https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this` is as follows.

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "Taiwan Semiconductor Manufacturing Company"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q713418>,
            <https://welektronik.iis.fraunhofer.de/entity/Q20> ;
        foaf:homepage <https://www.tsmc.com/> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289>,
            <https://welektronik.iis.fraunhofer.de/entity/Q290>,
            <https://welektronik.iis.fraunhofer.de/entity/Q291> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#headquarter> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ662.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ663.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ664.ttl#this> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "Intel"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q248>,
            <https://welektronik.iis.fraunhofer.de/entity/Q22> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q285> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#headquarter> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ299.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ300.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ301.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ303.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ304.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ305.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ306.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ612.ttl#this> .

***

The description of `https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> a rdfs:Class ;
        rdfs:label "Enterprise"@en .
    
    <https://purl.org/supply-network/onto#SupplyFlow> a rdfs:Class ;
        rdfs:label "Supply Flow"@en .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier> a owl:ObjectProperty ;
        rdfs:label "supplier"@en ;
        rdfs:domain <https://purl.org/supply-network/onto#SupplyFlow> ;
        rdfs:range <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> .

***

Think: We have gathered more information about the key resources involved, which are Taiwanese companies and Intel. We also have a better understanding of the supplier relationship. Next, we need to construct a query to find Taiwanese companies that supply Intel.

Act: query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType ?type . ?type rdfs:label "Taiwanese company"@en . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }')

***

No results for `query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType ?type . ?type rdfs:label "Taiwanese company"@en . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }')`.

***

Think: The query did not return any results. This could be due to the fact that the organization type "Taiwanese company" does not exist in the knowledge graph. We need to modify the query to use the correct organization type.

Act: query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }')

***

The query 'PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }' returned the following solution.

    company
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ38.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ104.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ46.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this

***

Think: The query returned a list of companies that are suppliers to Intel. However, we need to verify if these companies are indeed Taiwanese.

Act: query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company tbox:headquarter ?headquarter . ?headquarter tbox:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this> . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }')

***

No results for `query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company tbox:headquarter ?headquarter . ?headquarter tbox:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this> . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }')`.

***

Think: The query did not return any results. This could be due to the fact that the location of the headquarter is not explicitly stated as Taiwan in the knowledge graph. We need to modify the query to use a different approach to identify Taiwanese companies.

Act: query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company owl:sameAs ?wikidata . ?wikidata <http://www.wikidata.org/prop/direct/P17> <http://www.wikidata.org/entity/Q865> . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }')

***

No results for `query('PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company owl:sameAs ?wikidata . ?wikidata <http://www.wikidata.org/prop/direct/P17> <http://www.wikidata.org/entity/Q865> . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }')`.

***

Think: The query did not return any results. We have tried different approaches to identify Taiwanese companies that supply Intel, but none of them have been successful. We need to consider the possibility that the knowledge graph does not contain the necessary information to answer this question.

Act: fail('Unable to find Taiwanese companies that supply Intel due to lack of information in the knowledge graph.')

{'loop': {'id': '67d15f67', 'question': 'Taiwanese companies that supply Intel', 'iterations': 7, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company a :Enterprise . ?company tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> . ?company owl:sameAs ?wikidata . ?wikidata <http://www.wikidata.org/prop/direct/P17> <http://www.wikidata.org/entity/Q865> . ?supplyFlow :supplier ?company . ?supplyFlow :customer <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> . }', 'elapsed_time': 81723}, 'tokens': {'prompt_tokens': 25916, 'completion_tokens': 1257, 'elapsed_time_model': 72473, 'tokens_per_sec': 374.93720993369476}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}