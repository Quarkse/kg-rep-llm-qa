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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 32290 triples. System version v0.2.8-77-g05f9f338 is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Chip fabs

***

Think: The user is asking about chip fabs, which are facilities that manufacture microchips. To formulate a query, we need to identify the key resources related to chip fabs and find their URIs in the knowledge graph.

Act: search('chip fab') | search('microchip manufacturing') | search('semiconductor fabrication')

***

The keyword search for `chip fab` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q297 **Chip fab** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ605.ttl#this **Nexchip Hefei Fab** 0.5078
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ506.ttl#this **Magnachip Fab Gumi** 0.4950
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ568.ttl#this **Powerchip Jhunan Fab** 0.4719
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ567.ttl#this **Powerchip Hsinchu Fab** 0.4616

***

The keyword search for `microchip manufacturing` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this **Murata Manufacturing** 0.6528
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ149.ttl#this **Shindengen Electric Manufacturing** 0.4830
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ30.ttl#this **Microchip Technology** 0.4352
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.4308
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this **Taiwan Semiconductor Manufacturing Company Nanjing Fab** 0.4216

***

The keyword search for `semiconductor fabrication` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this **Japan Semiconductor Corporation** 0.6030
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this **Seoul Semiconductor** 0.6019
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ666.ttl#this **Actions Semiconductor** 0.6019
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this **Micron Semiconductor** 0.5893
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this **Brite Semiconductor** 0.5879

***

Think: We have identified several key resources related to chip fabs, including the concept of a chip fab itself, as well as specific companies and facilities involved in microchip manufacturing and semiconductor fabrication. To further expand our knowledge, we can dereference these resources to gather more information.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q297') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ605.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q297` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q297> a tbox:SiteType ;
        rdfs:label "Chip fab"@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ605.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ605.ttl#this> a ns1:Feature,
            <https://www.w3.org/ns/org#Site> ;
        rdfs:label "Nexchip Hefei Fab"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ185684.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "Murata Manufacturing"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q613325>,
            <https://welektronik.iis.fraunhofer.de/entity/Q69> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q285> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#headquarter> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ446.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ447.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ448.ttl#this> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ93.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "Japan Semiconductor Corporation"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q113105896>,
            <https://welektronik.iis.fraunhofer.de/entity/Q93> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q285> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ489.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ490.ttl#this> .

***

Think: We have gathered more information about the key resources related to chip fabs, including their types, locations, and relationships with other entities. To further refine our query, we can explore the properties and classes associated with these resources.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q285') | deref('https://welektronik.iis.fraunhofer.de/entity/Q291') | deref('https://welektronik.iis.fraunhofer.de/entity/Q297')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q285` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q285> a tbox:OrganizationType ;
        rdfs:label "Integrated Device Manufacturer"@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q291` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q291> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Foundry Service"@en .

***

Do not repeat actions.

***

Think: We have gathered more information about the properties and classes associated with the key resources related to chip fabs. To construct a query, we need to identify the specific information the user is asking for.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:SiteType . ?x :label "Chip fab"@en . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x a tbox:SiteType . ?x :label "Chip fab"@en . }')`.

***

Think: The query did not return any results. This is because the label "Chip fab" is associated with the resource `https://welektronik.iis.fraunhofer.de/entity/Q297`, which is of type `tbox:SiteType`. We can modify the query to directly ask for this resource.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :Q297 a tbox:SiteType . }')

***

The query 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { :Q297 a tbox:SiteType . }' returned the following solution.

    x

***

Think: The query returned a solution, which means we have successfully identified the resource `https://welektronik.iis.fraunhofer.de/entity/Q297` as a `tbox:SiteType`. This resource represents the concept of a chip fab. To provide a more informative answer, we can query for the sites that are of this type.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x tbox:siteType :Q297 . }')

***

The query 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x WHERE { ?x tbox:siteType :Q297 . }' returned the following solution (first 20 results).
    x
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ299.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ300.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ301.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ307.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ308.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ309.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ310.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ311.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ312.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ313.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ314.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ315.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ322.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ323.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ324.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ327.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ328.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ329.ttl#this

***

Think: The query returned a list of sites that are of type `tbox:SiteType` and have a `siteType` of `:Q297`, which represents a chip fab. This list includes various sites such as `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this`, `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ299.ttl#this`, and others. To provide a more informative answer, we can query for the labels of these sites.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x ?label WHERE { ?x tbox:siteType :Q297 . ?x rdfs:label ?label . }')

***

The query 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x ?label WHERE { ?x tbox:siteType :Q297 . ?x rdfs:label ?label . }' returned the following solution (first 20 results).
    x,label
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this,Intel Fab Irland
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ299.ttl#this,Intel Fab Kiryat Gat
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ300.ttl#this,Intel Fab New Mexico
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ301.ttl#this,Intel Fab Arizona
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this,Intel Fab Oregon
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ307.ttl#this,Texas Instruments So. Portland Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ308.ttl#this,Texas Instruments Sherman Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ309.ttl#this,Texas Instruments Dallas Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ310.ttl#this,Texas Instruments Richardson Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ311.ttl#this,Texas Instruments Lehi Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ312.ttl#this,Texas Instruments Freising Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ313.ttl#this,Texas Instruments Chengdu Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ314.ttl#this,Texas Instruments Aizu Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ315.ttl#this,Texas Instruments Miho Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ322.ttl#this,Micron Boise Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ323.ttl#this,Micron Hiroshima Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ324.ttl#this,Micron Manassas Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ327.ttl#this,Micron Singapore Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ328.ttl#this,Micron Taichung Fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ329.ttl#this,Micron Taoyuan Fab

***

Think: The query returned a list of sites that are of type `tbox:SiteType` and have a `siteType` of `:Q297`, which represents a chip fab, along with their labels. This list includes various sites such as Intel Fab Irland, Intel Fab Kiryat Gat, Texas Instruments So. Portland Fab, and others. 

Act: success('The query for chip fabs has been successfully executed and the results have been retrieved.')

{'loop': {'id': '67bf192f', 'question': 'Chip fabs', 'iterations': 8, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?x ?label WHERE { ?x tbox:siteType :Q297 . ?x rdfs:label ?label . }', 'elapsed_time': 1064939}, 'tokens': {'prompt_tokens': 28654, 'completion_tokens': 1144, 'elapsed_time_model': 1051441, 'tokens_per_sec': 28.340145616967174}, 'git': {'label': 'v0.2.8-77-g05f9f338', 'commit': '05f9f33880e9523b7eb3f19ed97e6b71bef1547a'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}