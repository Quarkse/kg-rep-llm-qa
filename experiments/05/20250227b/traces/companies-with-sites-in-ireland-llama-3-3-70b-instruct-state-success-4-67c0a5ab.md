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

Companies with sites in Ireland

***

Think: The user is looking for companies that have sites in Ireland. To formulate a query, we need to identify the key resources involved, which are companies and their locations. We can start by searching for keywords related to companies and Ireland.

Act: search('companies') | search('Ireland') | search('location')

***

The keyword search for `companies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1438.ttl#this **Campania** 0.4000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **Crolles** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ208812.ttl#this **Corbeil-Essonnes** 0.2981

***

The keyword search for `Ireland` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ27.ttl#this **Ireland** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ26.ttl#this **Northern Ireland** 0.6285
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this **Intel Fab Irland** 0.4714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ774.ttl#this **Roland** 0.4714
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ33.ttl#this **Finland** 0.4444

***

The keyword search for `location` returned the following ranked list with hits.

    https://dblp.org/rdf/schema#Publication **Publication** 0.5262
    https://dblp.org/rdf/schema#Creator **Publication** 0.5262
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ84.ttl#this **London** 0.4472
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23939248.ttl#this **London** 0.4472
    http://purl.org/linked-data/cube#Observation **Observation** 0.4385

***

Think: We have identified some key resources related to companies and Ireland. The search results for `Ireland` include a resource about Intel Fab Ireland, which is a site in Ireland. We can use this information to formulate a query. We also need to consider the properties that connect companies to their locations.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ27.ttl#this')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix ns2: <https://www.w3.org/ns/org#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this> a ns1:Feature,
            ns2:Site ;
        rdfs:label "Intel Fab Irland"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ987797.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> ;
        ns2:siteOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ27.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ27.ttl#this> a ns1:Feature ;
        rdfs:label "Ireland"@en ;
        ns1:featureClass ns1:A ;
        ns1:featureCode ns1:A.PCLI ;
        owl:sameAs <http://www.wikidata.org/entity/Q27>,
            <https://sws.geonames.org/2963597/> ;
        tbox:childFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ131438.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ159736.ttl#this> .

***

Think: We have gathered more information about the resources related to Intel Fab Ireland and Ireland. We can see that Intel Fab Ireland is a site of Intel, and it is located in Ireland. We can use this information to formulate a query to find companies with sites in Ireland.

Act: query('PREFIX ns2: <https://www.w3.org/ns/org#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?site a ns2:Site ; ns2:siteOf ?company . ?site tbox:siteType ?type . FILTER (?type = <https://welektronik.iis.fraunhofer.de/entity/Q297>) . }')

***

The query 'PREFIX ns2: <https://www.w3.org/ns/org#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?site a ns2:Site ; ns2:siteOf ?company . ?site tbox:siteType ?type . FILTER (?type = <https://welektronik.iis.fraunhofer.de/entity/Q297>) . }' returned the following solution (first 20 results).
    company
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ31.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ34.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ53.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ56.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ59.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ62.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ63.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ64.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ66.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this

***

Think: The query returned a list of companies with sites in Ireland. We can use this information to provide an answer to the user.

Act: success('The query has been successfully executed and the results have been obtained.')

{'loop': {'id': '67c0a5ab', 'question': 'Companies with sites in Ireland', 'iterations': 4, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX ns2: <https://www.w3.org/ns/org#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?site a ns2:Site ; ns2:siteOf ?company . ?site tbox:siteType ?type . FILTER (?type = <https://welektronik.iis.fraunhofer.de/entity/Q297>) . }', 'elapsed_time': 37469}, 'tokens': {'prompt_tokens': 8389, 'completion_tokens': 430, 'elapsed_time_model': 29526, 'tokens_per_sec': 298.6781064116072}, 'git': {'label': 'v0.2.8-79-g9b6f0bcd', 'commit': '9b6f0bcd1d005074f643fdb14a359bcef6a0438a'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}