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

Total revenue of companies offering foundry services

***

Think: The user is asking for the total revenue of companies that offer foundry services. To answer this question, we need to identify the key resources involved, which are companies that offer foundry services and their respective revenues. We can start by searching for companies that offer foundry services and then try to find information about their revenues.

Act: search('foundry services companies') | search('revenue of foundry services companies')

***

The keyword search for `foundry services companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q291 **Foundry Service** 0.6756
    https://welektronik.iis.fraunhofer.de/entity/Q287 **Foundry** 0.4952
    https://welektronik.iis.fraunhofer.de/entity/Q293 **Service** 0.3714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this **GlobalFoundries** 0.3603
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **provides service** 0.3502

***

The keyword search for `revenue of foundry services companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q291 **Foundry Service** 0.5437
    https://welektronik.iis.fraunhofer.de/entity/Q287 **Foundry** 0.3736
    https://welektronik.iis.fraunhofer.de/entity/Q293 **Service** 0.3203
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this **GlobalFoundries** 0.3107
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **provides service** 0.3019

***

Think: We have identified some key resources, including companies that offer foundry services, such as GlobalFoundries, and the concept of foundry services. We also have a property "providesService" that might be useful. However, we still need to find information about the revenues of these companies. We can try to dereference the URIs of the companies and the concept of foundry services to see if we can find any relevant information.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this') | deref('https://welektronik.iis.fraunhofer.de/entity/Q291') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this` is as follows.

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "GlobalFoundries"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q691592>,
            <https://welektronik.iis.fraunhofer.de/entity/Q37> ;
        foaf:homepage <https://gf.com/> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288>,
            <https://welektronik.iis.fraunhofer.de/entity/Q289>,
            <https://welektronik.iis.fraunhofer.de/entity/Q290>,
            <https://welektronik.iis.fraunhofer.de/entity/Q291>,
            <https://welektronik.iis.fraunhofer.de/entity/Q292> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1048> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#headquarter> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ548.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ549.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ550.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ551.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ552.ttl#this> .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q291` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q291> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Foundry Service"@en .

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
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://welektronik.iis.fraunhofer.de/entity/Q293> .

***

Think: We have found some information about GlobalFoundries, including its type, services provided, and size. We also have information about the concept of foundry services and the property "providesService". However, we still need to find information about the revenues of companies that offer foundry services. We can try to query the graph to see if we can find any relevant information.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?revenue WHERE { ?company a ns1:Organization . ?company tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> . ?company ns1:hasFinancialReport ?report . ?report ns1:reports ?revenue . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?revenue WHERE { ?company a ns1:Organization . ?company tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> . ?company ns1:hasFinancialReport ?report . ?report ns1:reports ?revenue . }')`.

***

Think: The query did not return any results, which means that the graph does not contain the specific information we are looking for. We can try to modify the query to see if we can find any related information.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?service WHERE { ?company a ns1:Organization . ?company tbox:providesService ?service . FILTER (?service = <https://welektronik.iis.fraunhofer.de/entity/Q291>) . }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?service WHERE { ?company a ns1:Organization . ?company tbox:providesService ?service . FILTER (?service = <https://welektronik.iis.fraunhofer.de/entity/Q291>) . }' returned the following solution (first 20 results).
    company,service
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ125.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ162.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ165.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ168.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ678.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ692.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ75.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ800.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ88.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ106.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ114.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291

***

Think: The query returned a list of companies that provide foundry services. However, the graph does not contain information about the revenues of these companies. We can try to query the graph to see if we can find any related information, such as the size of the companies or their financial reports.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?size WHERE { ?company a ns1:Organization . ?company tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> . ?company tbox:size ?size . }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?size WHERE { ?company a ns1:Organization . ?company tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> . ?company tbox:size ?size . }' returned the following solution (first 20 results).
    company,size
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ165.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ168.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ106.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ114.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ117.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ152.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ161.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ164.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ269.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ237.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ52.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1047
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ694.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046

***

Think: The query returned a list of companies that provide foundry services, along with their sizes. However, the graph does not contain information about the revenues of these companies. We have reached the limit of our knowledge graph and cannot provide a precise answer to the user's question.

Act: fail('The knowledge graph does not contain information about the revenues of companies that provide foundry services.')

{'loop': {'id': '67d15c70', 'question': 'Total revenue of companies offering foundry services', 'iterations': 6, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?size WHERE { ?company a ns1:Organization . ?company tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> . ?company tbox:size ?size . }', 'elapsed_time': 56861}, 'tokens': {'prompt_tokens': 17878, 'completion_tokens': 894, 'elapsed_time_model': 51524, 'tokens_per_sec': 364.32892096891055}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}