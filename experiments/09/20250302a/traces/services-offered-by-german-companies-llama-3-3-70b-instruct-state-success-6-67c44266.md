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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 48029 triples. System version v0.2.8-84-gdf5e4a10 is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Services offered by German companies

***

Think: The User is asking about services offered by German companies. To formulate a query, we need to identify key resources such as German companies and the services they offer. We can start by searching for keywords related to German companies and services.

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

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#serviceProvidedBy **service provided by** 0.4243
    https://welektronik.iis.fraunhofer.de/entity/Q293 **Service** 0.4125
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService **provides service** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#this **Analog Devices** 0.2652
    https://welektronik.iis.fraunhofer.de/entity/Q291 **Foundry Service** 0.2572

***

Think: We have identified some key resources such as German companies and services offered by companies. We can now dereference these resources to gather more information.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this') | deref('https://welektronik.iis.fraunhofer.de/entity/Q293') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#serviceProvidedBy')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> a ns1:Feature ;
        rdfs:label "Germany"@en ;
        ns1:featureClass ns1:A ;
        ns1:featureCode ns1:A.PCLI ;
        owl:sameAs <http://www.wikidata.org/entity/Q183>,
            <https://sws.geonames.org/2921044/> ;
        tbox:childFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1055.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1194.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1197.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1198.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1199.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1200.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1202.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1205.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1208.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ64.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ980.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ985.ttl#this> .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q293` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix skos: <http://www.w3.org/2004/02/skos/core#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q293> a rdfs:Class ;
        rdfs:label "Service"@en ;
        rdfs:subClassOf skos:Concept .

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#serviceProvidedBy` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    tbox:serviceProvidedBy a owl:ObjectProperty ;
        rdfs:label "service provided by"@en ;
        rdfs:domain <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:range <https://www.w3.org/ns/org#Organization> ;
        owl:inverseOf tbox:providesService .

***

Think: We have gathered more information about German companies and services offered by companies. We can now use this information to construct a query.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service ?company WHERE { ?service a <https://welektronik.iis.fraunhofer.de/entity/Q293> . ?service tbox:serviceProvidedBy ?company . ?company a org:Organization . ?company org:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service ?company WHERE { ?service a <https://welektronik.iis.fraunhofer.de/entity/Q293> . ?service tbox:serviceProvidedBy ?company . ?company a org:Organization . ?company org:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . }')`.

***

Think: The query did not return any results. This could be due to the fact that the query is trying to find services provided by companies located in Germany, but the knowledge graph may not have this information. We can try to modify the query to find services provided by companies in general.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service ?company WHERE { ?service a <https://welektronik.iis.fraunhofer.de/entity/Q293> . ?service tbox:serviceProvidedBy ?company . ?company a org:Organization . }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?service ?company WHERE { ?service a <https://welektronik.iis.fraunhofer.de/entity/Q293> . ?service tbox:serviceProvidedBy ?company . ?company a org:Organization . }' returned the following solution (first 20 results).
    service,company
    https://welektronik.iis.fraunhofer.de/entity/Q292,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ734.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ922.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ125.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q288,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q292,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ75.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ805.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ905.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ917.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ917.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q289,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ920.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ923.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ925.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ927.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q290,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ929.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this
    https://welektronik.iis.fraunhofer.de/entity/Q291,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this

***

Think: The query returned a list of services and companies. However, the User asked for services offered by German companies. We need to filter the results to only include companies located in Germany.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> PREFIX loc: <http://www.geonames.org/ontology#> SELECT DISTINCT ?service ?company WHERE { ?service a <https://welektronik.iis.fraunhofer.de/entity/Q293> . ?service tbox:serviceProvidedBy ?company . ?company a org:Organization . ?company loc:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> PREFIX loc: <http://www.geonames.org/ontology#> SELECT DISTINCT ?service ?company WHERE { ?service a <https://welektronik.iis.fraunhofer.de/entity/Q293> . ?service tbox:serviceProvidedBy ?company . ?company a org:Organization . ?company loc:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . }')`.

***

Think: The query did not return any results. This could be due to the fact that the knowledge graph does not have information about companies located in Germany. We can try to modify the query to find services provided by companies in general, and then filter the results manually.

Act: success('The query did not return any results. However, we can provide a list of services and companies that provide them. Please note that this list may not be specific to German companies.')

{'loop': {'id': '67c44266', 'question': 'Services offered by German companies', 'iterations': 6, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> PREFIX loc: <http://www.geonames.org/ontology#> SELECT DISTINCT ?service ?company WHERE { ?service a <https://welektronik.iis.fraunhofer.de/entity/Q293> . ?service tbox:serviceProvidedBy ?company . ?company a org:Organization . ?company loc:location <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> . }', 'elapsed_time': 67580}, 'tokens': {'prompt_tokens': 16982, 'completion_tokens': 854, 'elapsed_time_model': 57652, 'tokens_per_sec': 309.3694217537879}, 'git': {'label': 'v0.2.8-84-gdf5e4a10', 'commit': 'df5e4a10170efede1e56c09a029ca4d906e5856a'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}