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

Assembly/test sites

***

Think: The user is asking about assembly or test sites, which could refer to locations where products are assembled or tested. To formulate a query, we need to identify the key resources and concepts related to assembly and test sites.

Act: search('assembly site') | search('test site') | search('manufacturing location')

***

The keyword search for `assembly site` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q298 **['Site of a company used for assembly and/or testing of semiconductors.', 'Assembly/Test facility']** 0.4889
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this **['Maxim Assembly/Test Cavite']** 0.4880
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this **['AEM Assembly/Test Singapore']** 0.4795
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ998.ttl#this **['Ardentec Assembly/Test Singapore']** 0.4428
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ398.ttl#this **['ams Osram Assembly/Test Singapore']** 0.4364

***

The keyword search for `test site` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ51685.ttl#this **['Tempe']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ908.ttl#this **['Tesna']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this **['Maxim Assembly/Test Cavite']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this **['AEM Assembly/Test Singapore']** 0.3359
    https://welektronik.iis.fraunhofer.de/entity/Q289 **['Testing of semiconductors.', 'Testing']** 0.3313

***

The keyword search for `manufacturing location` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this **['Murata Manufacturing']** 0.6093
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this **['Semiconductor Manufacturing International Corporation']** 0.5488
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ559.ttl#this **['Semiconductor Manufacturing International Corporation Beijing Fab']** 0.5118
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ558.ttl#this **['Semiconductor Manufacturing International Corporation Tianjin Fab']** 0.4778
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ557.ttl#this **['Semiconductor Manufacturing International Corporation Shanghai Fab']** 0.4746

***

Think: We have identified several key resources related to assembly and test sites, including specific companies and locations. To further refine our query, we need to gather more information about these resources and their relationships.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q298') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q298` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q298> a tbox:SiteType ;
        rdfs:label "Assembly/Test facility"@en ;
        rdfs:comment "Site of a company used for assembly and/or testing of semiconductors."@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this> a ns1:Feature,
            <https://www.w3.org/ns/org#Site> ;
        rdfs:label "Maxim Assembly/Test Cavite"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1482.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .

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

Think: We have gathered more information about the key resources and their relationships. We can now formulate a query to retrieve the desired information.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.geonames.org/ontology#> SELECT DISTINCT ?site ?label WHERE { ?site a ns1:Feature ; rdfs:label ?label ; tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.geonames.org/ontology#> SELECT DISTINCT ?site ?label WHERE { ?site a ns1:Feature ; rdfs:label ?label ; tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> }' returned the following solution (first 20 results).
    site,label
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1005.ttl#this,Besi Assembly/Test Austria
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1006.ttl#this,Besi Assembly/Test Singapore
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1007.ttl#this,Besi Assembly/Test Steinhausen
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1008.ttl#this,Besi Assembly/Test Netherlands
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1009.ttl#this,PacTech Assembly/Test Nauen
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1010.ttl#this,Semilab Assembly/Test Budapest
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1011.ttl#this,Semilab Assembly/Test Florida
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1012.ttl#this,3DiS Technologies  Assembly/Test Labège
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1013.ttl#this,RoodMicrotec Assembly/Test Nördlingen
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1014.ttl#this,RoodMicrotec Assembly/Test Stuttgart
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1015.ttl#this,RoodMicrotec Assembly/Test Zwolle
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1016.ttl#this,RoodMicrotec Assembly/Test Deventer
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1017.ttl#this,Sencio Assembly/Test Netherlands
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1018.ttl#this,AEM Assembly/Test Suzhou
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this,AEM Assembly/Test Singapore
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1020.ttl#this,AEM Assembly/Test Penang
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1021.ttl#this,AEM Assembly/Test Finland
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ303.ttl#this,Intel Assembly/Test Malaysia
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ304.ttl#this,Intel Assembly/Test Vietnam
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ305.ttl#this,Intel Assembly/Test Chengdu

***

Think: We have successfully formulated a query and retrieved the desired information. The query returns a list of assembly and test sites, along with their labels.

Act: success('We have identified several assembly and test sites, including specific companies and locations.')

{'loop': {'id': '67d1ee47', 'question': 'Assembly/test sites', 'iterations': 4, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.geonames.org/ontology#> SELECT DISTINCT ?site ?label WHERE { ?site a ns1:Feature ; rdfs:label ?label ; tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> }', 'elapsed_time': 38113}, 'tokens': {'prompt_tokens': 9329, 'completion_tokens': 398, 'elapsed_time_model': 31022, 'tokens_per_sec': 313.5455201780608}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}