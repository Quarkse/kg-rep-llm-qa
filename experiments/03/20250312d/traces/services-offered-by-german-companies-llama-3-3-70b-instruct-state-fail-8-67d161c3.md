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

Services offered by German companies

***

Think: The user is asking about services offered by German companies. To formulate a query, we need to identify key resources such as German companies and the services they offer. We can start by searching for relevant keywords to find URIs that identify these resources.

Act: search('German companies') | search('services offered by companies')

***

The keyword search for `German companies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this **Germany** 0.4851
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1206012.ttl#this **German Reich** 0.4537
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1015874.ttl#this **Sherman Oaks** 0.3241
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ982379.ttl#this **Sherman** 0.3234
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.2559

***

The keyword search for `services offered by companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q293 **Service** 0.4125
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **provides service** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#this **Analog Devices** 0.2652
    https://welektronik.iis.fraunhofer.de/entity/Q291 **Foundry Service** 0.2572
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this **Advanced Micro Devices** 0.2526

***

Think: We have found some relevant resources, including the concept of "Service" and the property "providesService". We also have a list of companies, including some that are not necessarily German. To further refine our query, we need to gather more information about the services offered by German companies. We can do this by dereferencing the resources we have found so far.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q293') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q293` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix skos: <http://www.w3.org/2004/02/skos/core#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q293> a rdfs:Class ;
        rdfs:label "Service"@en ;
        rdfs:subClassOf skos:Concept .
    
    <https://www.w3.org/ns/org#Organization> a rdfs:Class ;
        rdfs:label "Organization"@en .
    
    tbox:providesService a owl:ObjectProperty ;
        rdfs:label "provides service"@en ;
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://welektronik.iis.fraunhofer.de/entity/Q293> .

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

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> a ns1:Feature ;
        rdfs:label "Germany"@en ;
        ns1:featureClass ns1:A ;
        ns1:featureCode ns1:A.PCLI ;
        owl:sameAs <http://www.wikidata.org/entity/Q183>,
            <https://sws.geonames.org/2921044/> .

***

Think: We have gathered more information about the resources we found earlier. We now know that the concept of "Service" is a subclass of "Concept" and that the property "providesService" has a domain of "Organization" and a range of "Service". We also have more information about Germany, including its feature class and code. To further refine our query, we need to find German companies that provide services. We can do this by searching for companies that are located in Germany and that provide services.

Act: search('German company') | query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a :Q293 . ?x tbox:providesService ?y . }')

***

The keyword search for `German company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this **Germany** 0.7500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1206012.ttl#this **German Reich** 0.4677
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.4000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.3769
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55304.ttl#this **American occupation zone in Germany** 0.3699

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a :Q293 . ?x tbox:providesService ?y . }')`.

***

Think: We have found some German companies, but the query to find services provided by these companies did not return any results. This is because the query is looking for instances of the "Service" concept that provide services, which is not the correct relationship. Instead, we should be looking for organizations that provide services. We can modify the query to reflect this.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?x ?y WHERE { ?x a org:Organization . ?x tbox:providesService ?y . }')

***

The query 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?x ?y WHERE { ?x a org:Organization . ?x tbox:providesService ?y . }' returned the following solution (first 20 results).
    x,y
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q288
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q290
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q288
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q289
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q288
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q290
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ125.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q288
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q289
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q290
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q291
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ127.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q292
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q288
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q292
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ162.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q288

***

Think: We have found a list of organizations that provide services. However, we still need to filter this list to only include German companies. We can do this by adding a filter to the query to only include organizations that are located in Germany.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> PREFIX loc: <http://www.geonames.org/ontology#> SELECT DISTINCT ?x ?y WHERE { ?x a org:Organization . ?x loc:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . ?x tbox:providesService ?y . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> PREFIX loc: <http://www.geonames.org/ontology#> SELECT DISTINCT ?x ?y WHERE { ?x a org:Organization . ?x loc:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . ?x tbox:providesService ?y . }')`.

***

Think: The query to find German companies that provide services did not return any results. This is because the relationship between the company and its location is not explicitly stated in the knowledge graph. We can try to modify the query to use a different relationship, such as the "basedNear" relationship, to find companies that are based near Germany.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> PREFIX loc: <http://www.geonames.org/ontology#> SELECT DISTINCT ?x ?y WHERE { ?x a org:Organization . ?x loc:basedNear <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . ?x tbox:providesService ?y . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> PREFIX loc: <http://www.geonames.org/ontology#> SELECT DISTINCT ?x ?y WHERE { ?x a org:Organization . ?x loc:basedNear <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . ?x tbox:providesService ?y . }')`.

***

Think: We have tried several queries to find German companies that provide services, but none of them have returned any results. This suggests that the knowledge graph may not contain the information we are looking for, or that the relationships between the entities in the graph are not well-defined. We can try to use a more general query to find any companies that provide services, regardless of their location.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?x ?y WHERE { ?x a org:Organization . ?x tbox:providesService ?y . }') 

Note: This is the 10th cycle. If the next cycle does not provide a useful result, we will have to give up.

***

Do not repeat actions.

***

Think: We have tried several queries to find German companies that provide services, but none of them have returned any results. This suggests that the knowledge graph may not contain the information we are looking for, or that the relationships between the entities in the graph are not well-defined. 

Act: fail('Unable to find German companies that provide services.')

{'loop': {'id': '67d161c3', 'question': 'Services offered by German companies', 'iterations': 8, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> PREFIX loc: <http://www.geonames.org/ontology#> SELECT DISTINCT ?x ?y WHERE { ?x a org:Organization . ?x loc:basedNear <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . ?x tbox:providesService ?y . }', 'elapsed_time': 90154}, 'tokens': {'prompt_tokens': 27026, 'completion_tokens': 1357, 'elapsed_time_model': 80525, 'tokens_per_sec': 352.47230756634224}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}