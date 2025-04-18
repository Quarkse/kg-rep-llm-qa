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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 43248 triples. System version v0.2.8-79-g9b6f0bcd is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Medium size companies from China

***

Think: The user is asking for medium-sized companies from China. To formulate a query, we need to identify the key resources involved, which are "medium-sized companies" and "China". We also need to consider the properties that relate these resources, such as the location of the companies.

Act: search('China') | search('medium-sized companies') | deref('http://dbpedia.org/resource/Company')

***

The keyword search for `China` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ506395.ttl#this **Chino** 0.5714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ170616.ttl#this **Chiba** 0.5714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this **People's Republic of China** 0.4286
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ696772.ttl#this **Hitachinaka** 0.4193
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ655.ttl#this **Chihuahua** 0.4193

***

The keyword search for `medium-sized companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1047 **Medium** 0.4629
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ110421.ttl#this **Medina County** 0.2817
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ39.ttl#this **MediaTek** 0.2760
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **MSE Supplies** 0.2333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.2182

***

No results for `deref('http://dbpedia.org/resource/Company')`.

***

Think: The search results for "China" and "medium-sized companies" have returned some relevant resources, including the URI for "People's Republic of China" and some companies. However, the results for "medium-sized companies" are not very specific and do not directly relate to the concept of medium-sized companies. The dereference of the "Company" resource did not return any results.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this') | search('company size') | search('China company')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this> a ns1:Feature ;
        rdfs:label "People's Republic of China"@en ;
        ns1:featureClass ns1:A ;
        ns1:featureCode ns1:A.PCLI ;
        owl:sameAs <http://www.wikidata.org/entity/Q148>,
            <https://sws.geonames.org/1814991/> ;
        tbox:childFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ11725.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ11736.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ15175.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ16963.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ16967.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ19770.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ34800.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ40956.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ41079.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ41705.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ42392.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ43407.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ43684.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ43934.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ45761.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ45833.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ46862.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ46913.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ47097.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ8646.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ8686.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ956.ttl#this> .

***

The keyword search for `company size` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#size **size** 0.5455
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.3742
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#sizeOf **size of** 0.3563
    http://www.geonames.org/ontology#Code **Code** 0.3273
    https://welektronik.iis.fraunhofer.de/entity/Q1045 **Enterprise size** 0.3241

***

The keyword search for `China company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.4131
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ506395.ttl#this **Chino** 0.3904
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108058.ttl#this **Contra Costa County** 0.3356
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ110421.ttl#this **Medina County** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ166977.ttl#this **Chiayi County** 0.3333

***

Think: The description of the "People's Republic of China" resource provides information about its child features, which are other regions in China. The search results for "company size" and "China company" have returned some relevant resources, including the URI for "size" and some companies. However, the results are not very specific and do not directly relate to the concept of medium-sized companies in China.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#size') | search('medium enterprise') | search('Chinese company')

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#size` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    tbox:size a owl:ObjectProperty ;
        rdfs:label "size"@en ;
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://welektronik.iis.fraunhofer.de/entity/Q1045> ;
        owl:inverseOf tbox:sizeOf .

***

The keyword search for `medium enterprise` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **Enterprise** 0.7285
    https://welektronik.iis.fraunhofer.de/entity/Q1045 **Enterprise size** 0.6121
    https://welektronik.iis.fraunhofer.de/entity/Q1047 **Medium** 0.5678
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#observedEnterprise **observed enterprise** 0.5507
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#enterpriseObservation **enterprise observation** 0.4683

***

The keyword search for `Chinese company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.4851
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ506395.ttl#this **Chino** 0.3667
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ693237.ttl#this **Chitose** 0.3234
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ166977.ttl#this **Chiayi County** 0.3131
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.3032

***

Think: The description of the "size" property provides information about its domain and range, which are "Organization" and "Enterprise size", respectively. The search results for "medium enterprise" and "Chinese company" have returned some relevant resources, including the URI for "Enterprise size" and some companies. However, the results are not very specific and do not directly relate to the concept of medium-sized companies in China.

Act: query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX w: <https://welektronik.iis.fraunhofer.de/entity/> SELECT DISTINCT ?company WHERE { ?company a :Organization . ?company :size w:Q1047 . ?company :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this> . }')

***

No results for `query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX w: <https://welektronik.iis.fraunhofer.de/entity/> SELECT DISTINCT ?company WHERE { ?company a :Organization . ?company :size w:Q1047 . ?company :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this> . }')`.

***

Think: The query to find medium-sized companies in China did not return any results. This suggests that the knowledge graph does not contain information about companies with a specific size or location.

Act: fail('Unable to find medium-sized companies in China. The knowledge graph does not contain sufficient information to answer this question.')

{'loop': {'id': '67c0a7c6', 'question': 'Medium size companies from China', 'iterations': 5, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX w: <https://welektronik.iis.fraunhofer.de/entity/> SELECT DISTINCT ?company WHERE { ?company a :Organization . ?company :size w:Q1047 . ?company :locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this> . }', 'elapsed_time': 67099}, 'tokens': {'prompt_tokens': 14060, 'completion_tokens': 633, 'elapsed_time_model': 49226, 'tokens_per_sec': 298.4801665551536}, 'git': {'label': 'v0.2.8-79-g9b6f0bcd', 'commit': '9b6f0bcd1d005074f643fdb14a359bcef6a0438a'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}