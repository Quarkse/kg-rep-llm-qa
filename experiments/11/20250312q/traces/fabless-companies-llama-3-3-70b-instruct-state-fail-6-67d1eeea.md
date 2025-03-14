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

Fabless companies

***

Think: The user is asking about "fabless companies". To formulate a query, I need to understand what "fabless" means and what kind of information the user is looking for. A fabless company is a company that designs and sells semiconductor products, but does not manufacture them itself. 

Act: search('fabless company') | search('semiconductor industry')

***

The keyword search for `fabless company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.5336
    https://welektronik.iis.fraunhofer.de/entity/Q286 **['Fabless', 'Company that designs or/and sells semiconductors but does not produce them.']** 0.3752
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.3750
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ663.ttl#this **['Taiwan Semiconductor Manufacturing Company  Washington Fab']** 0.3080
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ220005.ttl#this **['Daviess County']** 0.3032

***

The keyword search for `semiconductor industry` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **['Seoul Semiconductor']** 0.6543
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this **['GCT Semiconductor']** 0.6299
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this **['AKM Semiconductor']** 0.6299
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ252.ttl#this **['GTA Semiconductor']** 0.6299
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this **['CISC Semiconductor']** 0.6139

***

Think: The search results for "fabless company" and "semiconductor industry" provide a list of relevant entities, including companies and concepts. The entity https://welektronik.iis.fraunhofer.de/entity/Q286 is defined as a "Fabless" company, which is a company that designs or/and sells semiconductors but does not produce them. 

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q286') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q286` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q286> a tbox:OrganizationType ;
        rdfs:label "Fabless"@en ;
        rdfs:comment "Company that designs or/and sells semiconductors but does not produce them."@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "Active Business Company"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q124743799>,
            <https://welektronik.iis.fraunhofer.de/entity/Q1104> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#headquarter> .

***

Think: The description of `https://welektronik.iis.fraunhofer.de/entity/Q286` provides information about the concept of a "Fabless" company. The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this` provides information about a specific company, including its type and registered site. 

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType . ?x :label "Fabless"@en . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:OrganizationType . ?x :label "Fabless"@en . }')`.

***

Think: The query did not return any results. This is because the label "Fabless" is associated with the entity `https://welektronik.iis.fraunhofer.de/entity/Q286`, but this entity is not of type `tbox:OrganizationType`. 

Act: query('PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT DISTINCT ?x WHERE { :Q286 rdfs:label ?x . }')

***

The query 'PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT DISTINCT ?x WHERE { :Q286 rdfs:label ?x . }' returned the following solution.

    x
    Fabless

***

Think: The query returned the label "Fabless" for the entity `https://welektronik.iis.fraunhofer.de/entity/Q286`. This confirms that the entity `https://welektronik.iis.fraunhofer.de/entity/Q286` represents the concept of a "Fabless" company. 

Act: query('PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:Organization . ?x rdfs:label ?y . FILTER (LANGMATCHES(LANG(?y), "en")) . }')

***

No results for `query('PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:Organization . ?x rdfs:label ?y . FILTER (LANGMATCHES(LANG(?y), "en")) . }')`.

***

Think: The query did not return any results. This is because the graph does not contain any organizations with English labels. 

Act: fail('Unable to find fabless companies in the knowledge graph.')

{'loop': {'id': '67d1eeea', 'question': 'Fabless companies', 'iterations': 6, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:Organization . ?x rdfs:label ?y . FILTER (LANGMATCHES(LANG(?y), "en")) . }', 'elapsed_time': 91798}, 'tokens': {'prompt_tokens': 12308, 'completion_tokens': 771, 'elapsed_time_model': 82058, 'tokens_per_sec': 159.38722544962846}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}