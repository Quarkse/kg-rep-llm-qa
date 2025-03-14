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

Company type of ASML

***

Think: The user is asking about the company type of ASML. To answer this, we need to identify the key resources in the question, which are "ASML" and "company type". We can start by searching for the URI of ASML.

Act: search('ASML')

***

The keyword search for `ASML` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this **['ASML']** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1038.ttl#this **['ASM International']** 0.3746
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ42114.ttl#this **['Asan']** 0.3333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1089.ttl#this **['ASUZAC']** 0.2887
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1116.ttl#this **['Alsil Material']** 0.2041

***

Think: We have found the URI of ASML, which is https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this. Now, we can dereference this URI to get more information about ASML, including its company type.

Act: deref("https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this")

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

Think: We have found that ASML is an organization of type https://welektronik.iis.fraunhofer.de/entity/Q1023. To determine the company type of ASML, we need to dereference this URI.

Act: deref("https://welektronik.iis.fraunhofer.de/entity/Q1023")

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1023` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1023> a tbox:OrganizationType ;
        rdfs:label "Equipment manufacturer"@en ;
        rdfs:comment "Company that produces equipment for semiconductor manufacturing."@en .

***

Think: We have found that the company type of ASML is "Equipment manufacturer". Now, we can construct a query to retrieve this information.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT ?companyType WHERE { :Q1029 tbox:organizationType ?companyType . ?companyType rdfs:label ?companyTypeLabel . FILTER(langMatches(lang(?companyTypeLabel), "en")) }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT ?companyType WHERE { :Q1029 tbox:organizationType ?companyType . ?companyType rdfs:label ?companyTypeLabel . FILTER(langMatches(lang(?companyTypeLabel), "en")) }')`.

***

Think: The query did not return any results. This is because the query is trying to match the language of the label to "en", but the label "Equipment manufacturer" does not have a language tag. We can modify the query to remove the language filter.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT ?companyTypeLabel WHERE { :Q1029 tbox:organizationType ?companyType . ?companyType rdfs:label ?companyTypeLabel . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT ?companyTypeLabel WHERE { :Q1029 tbox:organizationType ?companyType . ?companyType rdfs:label ?companyTypeLabel . }')`.

***

Think: The query still did not return any results. This is because the prefix for the ASML entity is incorrect. We can modify the query to use the correct prefix.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT ?companyTypeLabel WHERE { <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> tbox:organizationType ?companyType . ?companyType rdfs:label ?companyTypeLabel . }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT ?companyTypeLabel WHERE { <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> tbox:organizationType ?companyType . ?companyType rdfs:label ?companyTypeLabel . }' returned the following solution.

    companyTypeLabel
    Equipment manufacturer

***

Think: The query returned the correct result, which is "Equipment manufacturer". This means that the company type of ASML is indeed "Equipment manufacturer".

Act: success("The company type of ASML is Equipment manufacturer.")

{'loop': {'id': '67d1fad4', 'question': 'Company type of ASML', 'iterations': 7, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT ?companyTypeLabel WHERE { <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1029.ttl#this> tbox:organizationType ?companyType . ?companyType rdfs:label ?companyTypeLabel . }', 'elapsed_time': 65769}, 'tokens': {'prompt_tokens': 12905, 'completion_tokens': 772, 'elapsed_time_model': 63322, 'tokens_per_sec': 215.988297989572}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}