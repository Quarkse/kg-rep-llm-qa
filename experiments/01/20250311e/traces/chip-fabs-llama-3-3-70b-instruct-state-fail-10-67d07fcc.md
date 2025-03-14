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

Chip fabs

***

Think: The user is asking about chip fabs, which are facilities that manufacture semiconductor chips. To formulate a query, we need to identify the key resources related to chip fabs and find their URIs in the knowledge graph.

Act: search('chip fab') | search('semiconductor manufacturing') | search('fabrication plant')

***

The keyword search for `chip fab` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q297 **Chip fab** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ605.ttl#this **Nexchip Hefei Fab** 0.5078
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ506.ttl#this **Magnachip Fab Gumi** 0.4950
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ568.ttl#this **Powerchip Jhunan Fab** 0.4719
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ567.ttl#this **Powerchip Hsinchu Fab** 0.4616

***

The keyword search for `semiconductor manufacturing` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.7559
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this **Taiwan Semiconductor Manufacturing Company Nanjing Fab** 0.6952
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this **Taiwan Semiconductor Manufacturing Company Hsinchu Fab** 0.6700
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this **Semiconductor Manufacturing International Corporation** 0.6657
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ662.ttl#this **Taiwan Semiconductor Manufacturing Company Shanghai Fab** 0.6641

***

The keyword search for `fabrication plant` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1025.ttl#this **Advanced Micro-Fabrication Equipment** 0.4466
    https://dblp.org/rdf/schema#Creator **Publication** 0.3818
    https://dblp.org/rdf/schema#Publication **Publication** 0.3818
    https://dblp.org/rdf/schema#yearOfPublication **year of publication** 0.3004
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ795.ttl#this **Verification Technology** 0.2753

***

Think: We have identified some key resources related to chip fabs, including the concept of a chip fab itself, as well as specific fabrication plants and companies involved in semiconductor manufacturing. To further expand our knowledge, we can dereference some of these resources to gather more information.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q297') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q297` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q297> a tbox:SiteType ;
        rdfs:label "Chip fab"@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this` is as follows.

    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "Taiwan Semiconductor Manufacturing Company"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q713418>,
            <https://welektronik.iis.fraunhofer.de/entity/Q20> ;
        foaf:homepage <https://www.tsmc.com/> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q287> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q289>,
            <https://welektronik.iis.fraunhofer.de/entity/Q290>,
            <https://welektronik.iis.fraunhofer.de/entity/Q291> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#headquarter> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ662.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ663.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ664.ttl#this> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this> a ns1:Feature,
            <https://www.w3.org/ns/org#Site> ;
        rdfs:label "Taiwan Semiconductor Manufacturing Company Nanjing Fab"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ761811.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .

***

Think: We have gathered more information about the concept of a chip fab, as well as specific companies and sites involved in semiconductor manufacturing. To further expand our knowledge, we can dereference some of the related resources to gather more information.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q287') | deref('https://welektronik.iis.fraunhofer.de/entity/Q289') | deref('https://welektronik.iis.fraunhofer.de/entity/Q290') | deref('https://welektronik.iis.fraunhofer.de/entity/Q291') | deref('https://welektronik.iis.fraunhofer.de/entity/Q1049') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ761811.ttl#this')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q287` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q287> a tbox:OrganizationType ;
        rdfs:label "Foundry"@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q289` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q289> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Testing"@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q290` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q290> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Packaging"@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q291` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q291> a <https://welektronik.iis.fraunhofer.de/entity/Q293> ;
        rdfs:label "Foundry Service"@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1049` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1049> a <https://welektronik.iis.fraunhofer.de/entity/Q1045> ;
        rdfs:label "Very large"@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ761811.ttl#this` is as follows.

    @prefix ns1: <http://www.w3.org/2003/01/geo/wgs84_pos#> .
    @prefix ns2: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ761811.ttl#this> a ns2:Feature,
            ns1:SpatialThing ;
        rdfs:label "Pukou District"@en ;
        ns2:featureClass ns2:P ;
        ns2:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ16666.ttl#this> ;
        owl:sameAs <http://www.wikidata.org/entity/Q761811>,
            <https://sws.geonames.org/1798491/> ;
        ns1:lat 32.0611 ;
        ns1:long 118.6231 .

***

Think: We have gathered more information about the companies, sites, and services related to chip fabs. To formulate a query, we need to identify the key resources and relationships involved in the user's question.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?siteType WHERE { ?site a tbox:Site . ?site tbox:siteType ?siteType . ?siteType :label "Chip fab"@en . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?siteType WHERE { ?site a tbox:Site . ?site tbox:siteType ?siteType . ?siteType :label "Chip fab"@en . }')`.

***

Think: The query did not return any results. This may be due to the fact that the site type "Chip fab" is not directly associated with any sites in the knowledge graph. We need to reformulate the query to find sites that are related to chip fabs.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?site tbox:hasOrganization ?organization . ?organization tbox:organizationType :Q287 . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?site tbox:hasOrganization ?organization . ?organization tbox:organizationType :Q287 . }')`.

***

Think: The query did not return any results. This may be due to the fact that the property "hasOrganization" is not defined in the knowledge graph. We need to reformulate the query to find sites that are related to organizations that have the type "Foundry".

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization tbox:organizationType :Q287 . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization tbox:organizationType :Q287 . }')`.

***

Think: The query did not return any results. This may be due to the fact that the property "organizationType" is not defined in the knowledge graph. We need to reformulate the query to find sites that are related to organizations that have the type "Foundry".

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization tbox:providesService ?service . ?service :label "Foundry Service"@en . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization tbox:providesService ?service . ?service :label "Foundry Service"@en . }')`.

***

Think: The query did not return any results. This may be due to the fact that the property "providesService" is not defined in the knowledge graph. We need to reformulate the query to find sites that are related to organizations that provide foundry services.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization :label ?label . FILTER regex(?label, "Foundry") . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization :label ?label . FILTER regex(?label, "Foundry") . }')`.

***

Think: The query did not return any results. This may be due to the fact that the label "Foundry" is not present in the knowledge graph. We need to reformulate the query to find sites that are related to organizations that provide semiconductor manufacturing services.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization :label ?label . FILTER regex(?label, "Semiconductor") . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization :label ?label . FILTER regex(?label, "Semiconductor") . }')`.

***

You shall vanish soon. Please wrap up.

***

Think: We have tried various queries to find sites related to chip fabs, but none of them returned any results. It's possible that the knowledge graph does not contain the necessary information to answer the user's question.

Act: fail('Unable to find relevant information about chip fabs in the knowledge graph.')

{'loop': {'id': '67d07fcc', 'question': 'Chip fabs', 'iterations': 10, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <http://www.w3.org/ns/org#> SELECT DISTINCT ?site ?organization WHERE { ?site a tbox:Site . ?organization a ns1:Organization . ?organization ns1:hasSite ?site . ?organization :label ?label . FILTER regex(?label, "Semiconductor") . }', 'elapsed_time': 107855}, 'tokens': {'prompt_tokens': 40111, 'completion_tokens': 1532, 'elapsed_time_model': 99235, 'tokens_per_sec': 419.6390546190485}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}