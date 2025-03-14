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

Medium size companies from China

***

Think: The user is asking for medium-sized companies from China. To formulate a query, we need to identify the key resources involved, which are "medium-sized companies" and "China". We also need to consider the properties that relate these resources, such as the location of the companies.

Act: search('China') | search('medium-sized companies') | deref('http://dbpedia.org/ontology/company')

***

The keyword search for `China` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ170616.ttl#this **['Chiba']** 0.5714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ506395.ttl#this **['Chino']** 0.5714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this **["People's Republic of China"]** 0.4286
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ655.ttl#this **['Chihuahua']** 0.4193
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ696772.ttl#this **['Hitachinaka']** 0.4193

***

The keyword search for `medium-sized companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1047 **['Medium enterprise size.', 'Medium']** 0.4258
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.3224
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ110421.ttl#this **['Medina County']** 0.2692
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ39.ttl#this **['MediaTek']** 0.2638
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this **['MSE Supplies']** 0.2229

***

No results for `deref('http://dbpedia.org/ontology/company')`.

***

Think: The search results for "China" and "medium-sized companies" have returned some relevant hits, including the URI for "People's Republic of China" and a definition for "Medium enterprise size.". However, the results for "medium-sized companies" are not directly related to companies, but rather to a definition of medium-sized enterprises. We need to refine our search to find medium-sized companies from China.

Act: search('Chinese medium-sized companies') | deref('https://welektronik.iis.fraunhofer.de/entity/Q1047') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this')

***

The keyword search for `Chinese medium-sized companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1047 **['Medium enterprise size.', 'Medium']** 0.3406
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.2975
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ506395.ttl#this **['Chino']** 0.2715
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.2514
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ693237.ttl#this **['Chitose']** 0.2395

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1047` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1047> a <https://welektronik.iis.fraunhofer.de/entity/Q1045> ;
        rdfs:label "Medium"@en ;
        rdfs:comment "Medium enterprise size."@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ148.ttl#this> a ns1:Feature ;
        rdfs:label "People's Republic of China"@en ;
        ns1:featureClass ns1:A ;
        ns1:featureCode ns1:A.PCLI ;
        owl:sameAs <http://www.wikidata.org/entity/Q148>,
            <https://sws.geonames.org/1814991/> .

***

Think: The search results for "Chinese medium-sized companies" did not return any relevant hits. The description of the URI for "Medium enterprise size." and "People's Republic of China" were retrieved, but no medium-sized companies from China were found. We need to refine our search to find medium-sized companies from China.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company a :Q287 . ?company rdfs:label ?label . FILTER (regex(?label, "China")) }') | search('China companies') | deref('https://welektronik.iis.fraunhofer.de/entity/Q287')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company a :Q287 . ?company rdfs:label ?label . FILTER (regex(?label, "China")) }')`.

***

The keyword search for `China companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.4018
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ506395.ttl#this **['Chino']** 0.3667
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this **['China Resources Microelectronics']** 0.3328
    https://welektronik.iis.fraunhofer.de/entity/Q297 **['Chip fab', 'Site of a company that produces semiconductors.']** 0.3105
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ894.ttl#this **['ChipMOS Technologies']** 0.3103

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q287` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q287> a tbox:OrganizationType ;
        rdfs:label "Foundry"@en ;
        rdfs:comment "Company that produces semiconductors for other companies."@en .

***

Think: The search results for "China companies" returned some relevant hits, including the URI for "China Resources Microelectronics". The description of the URI for "Foundry" was also retrieved. We can use this information to formulate a query to find medium-sized companies from China.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company a :Q287 . ?company rdfs:label ?label . FILTER (regex(?label, "China")) }') | search('medium-sized China companies') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this')

***

Do not repeat actions.

***

The keyword search for `medium-sized China companies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ110421.ttl#this **['Medina County']** 0.3836
    https://welektronik.iis.fraunhofer.de/entity/Q1047 **['Medium enterprise size.', 'Medium']** 0.3792
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.2871
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ39.ttl#this **['MediaTek']** 0.2349
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ151.ttl#this **['MegaChips']** 0.2240

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "China Resources Microelectronics"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q15928538>,
            <https://welektronik.iis.fraunhofer.de/entity/Q126> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1023>,
            <https://welektronik.iis.fraunhofer.de/entity/Q285> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q288>,
            <https://welektronik.iis.fraunhofer.de/entity/Q289>,
            <https://welektronik.iis.fraunhofer.de/entity/Q290>,
            <https://welektronik.iis.fraunhofer.de/entity/Q291>,
            <https://welektronik.iis.fraunhofer.de/entity/Q292> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1048> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#headquarter> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ618.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ619.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ620.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ621.ttl#this> .

***

Think: The search results for "medium-sized China companies" did not return any relevant hits. The description of the URI for "China Resources Microelectronics" was retrieved, which is a company from China. We can use this information to formulate a query to find medium-sized companies from China.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company a :Q287 . ?company rdfs:label ?label . FILTER (regex(?label, "China")) . ?company :size ?size . FILTER (?size = :Q1048) }') | search('China medium-sized semiconductor companies') | deref('https://welektronik.iis.fraunhofer.de/entity/Q1048')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company a :Q287 . ?company rdfs:label ?label . FILTER (regex(?label, "China")) . ?company :size ?size . FILTER (?size = :Q1048) }')`.

***

The keyword search for `China medium-sized semiconductor companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.5052
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this **['CISC Semiconductor']** 0.4774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this **['NHanced Semiconductors']** 0.4669
    https://welektronik.iis.fraunhofer.de/entity/Q879 **['Outsourced semiconductor assembly and test', 'Company that packages and tests semiconductors.']** 0.4594
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **['GTA Semiconductor']** 0.4548

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1048` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1048> a <https://welektronik.iis.fraunhofer.de/entity/Q1045> ;
        rdfs:label "Large"@en ;
        rdfs:comment "Large enterprise size."@en .

***

Think: The search results for "China medium-sized semiconductor companies" returned some relevant hits, including the URI for "CISC Semiconductor". However, the description of the URI for "Large" was retrieved, which is not relevant to medium-sized companies. We need to refine our search to find medium-sized companies from China.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company a :Q287 . ?company rdfs:label ?label . FILTER (regex(?label, "China")) . ?company :size ?size . FILTER (?size = :Q1047) }') | search('Chinese semiconductor companies') | deref('https://welektronik.iis.fraunhofer.de/entity/Q1047')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company a :Q287 . ?company rdfs:label ?label . FILTER (regex(?label, "China")) . ?company :size ?size . FILTER (?size = :Q1047) }')`.

***

The keyword search for `Chinese semiconductor companies` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.5767
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this **['CISC Semiconductor']** 0.5449
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this **['Brite Semiconductor']** 0.5318
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **['GTA Semiconductor']** 0.5192
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this **['GCT Semiconductor']** 0.5192

***

Do not repeat actions.

***

Think: The search results for "Chinese semiconductor companies" returned some relevant hits, including the URI for "CISC Semiconductor". We can use this information to formulate a query to find medium-sized companies from China.

Act: fail('Unable to find medium-sized companies from China.')

{'loop': {'id': '67d1f43a', 'question': 'Medium size companies from China', 'iterations': 7, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company a :Q287 . ?company rdfs:label ?label . FILTER (regex(?label, "China")) . ?company :size ?size . FILTER (?size = :Q1047) }', 'elapsed_time': 92295}, 'tokens': {'prompt_tokens': 21392, 'completion_tokens': 1027, 'elapsed_time_model': 64511, 'tokens_per_sec': 347.5206809765953}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}