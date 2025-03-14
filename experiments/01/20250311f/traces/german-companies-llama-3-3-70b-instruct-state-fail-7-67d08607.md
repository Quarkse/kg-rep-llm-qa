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

German companies

***

Think: The user is asking about German companies, which suggests they are looking for information about companies based in Germany. To formulate a query, we need to identify the key resources and concepts related to German companies.

Act: search('Germany') | search('company')

***

The keyword search for `Germany` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this **Germany** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1206012.ttl#this **German Reich** 0.5345
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55309.ttl#this **French occupation zone in Germany** 0.4507
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55304.ttl#this **American occupation zone in Germany** 0.4384
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ982379.ttl#this **Sherman** 0.3333

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **Cook County** 0.3443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **Canyon County** 0.3443

***

Think: We have identified some key resources related to Germany and companies. The search results for 'Germany' include a resource about the country itself, as well as some related geographic and historical concepts. The search results for 'company' include a few specific companies, but no general concept of a company. To further refine our query, we should dereference the resource about Germany and see what properties and relationships it has.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this')

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

Think: We have dereferenced the resources for Germany and a company, and found some properties and relationships. The resource for Germany has a label, feature class, and feature code, as well as links to other datasets. The resource for the company has a label, type, and registered site. To further refine our query, we should explore the properties and relationships of the company resource, particularly the organization type and registered site.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q1060') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#headquarter')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1060` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1060> a tbox:OrganizationType ;
        rdfs:label "Materials producer"@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#headquarter` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#headquarter> a ns1:Feature,
            ns2:SpatialThing,
            <https://www.w3.org/ns/org#Site> ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ279128.ttl#this> ;
        ns2:lat 47.764556 ;
        ns2:long 12.456936 .

***

Think: We have explored the properties and relationships of the company resource, and found that it is a materials producer with a registered site in a specific location. To formulate a query, we need to identify the key resources and concepts related to German companies. We can use the properties and relationships we have found to construct a query that retrieves information about companies based in Germany.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> SELECT DISTINCT ?company ?companyLabel WHERE { ?company a ns1:Feature ; ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> ; rdfs:label ?companyLabel . }')

***

The query 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> SELECT DISTINCT ?company ?companyLabel WHERE { ?company a ns1:Feature ; ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> ; rdfs:label ?companyLabel . }' returned the following solution.

    company,companyLabel
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1055.ttl#this,Hamburg
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1194.ttl#this,Schleswig-Holstein
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1197.ttl#this,Lower Saxony
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1199.ttl#this,Hesse
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1208.ttl#this,Brandenburg
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1200.ttl#this,Rhineland-Palatinate
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1198.ttl#this,North Rhine-Westphalia
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1205.ttl#this,Thuringia
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ64.ttl#this,Berlin
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ985.ttl#this,Baden-Württemberg
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1202.ttl#this,Saxony
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ980.ttl#this,Bavaria

***

Think: The query returned a list of regions in Germany, but not companies. This is because the query was only searching for features that are parented by the Germany region, which includes states and cities, but not companies. To find companies, we need to modify the query to search for organizations that are located in Germany.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?companyLabel WHERE { ?company a org:Organization ; org:hasRegisteredSite ?site . ?site ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> ; rdfs:label ?companyLabel . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?companyLabel WHERE { ?company a org:Organization ; org:hasRegisteredSite ?site . ?site ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> ; rdfs:label ?companyLabel . }')`.

***

Think: The query did not return any results, which means that there are no organizations in the knowledge graph that have a registered site in Germany. This could be due to a lack of data or incorrect querying. To further investigate, we can try to find organizations that are related to Germany in any way.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?companyLabel WHERE { ?company a org:Organization ; ?p <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> ; rdfs:label ?companyLabel . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?companyLabel WHERE { ?company a org:Organization ; ?p <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> ; rdfs:label ?companyLabel . }')`.

***

Think: The query did not return any results, which means that there are no organizations in the knowledge graph that are directly related to Germany. This could be due to a lack of data or incorrect querying. Since we have explored various query options and did not get the desired results, we should consider giving up.

Act: fail('Unable to find German companies in the knowledge graph.')

{'loop': {'id': '67d08607', 'question': 'German companies', 'iterations': 7, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?companyLabel WHERE { ?company a org:Organization ; ?p <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this> ; rdfs:label ?companyLabel . }', 'elapsed_time': 69835}, 'tokens': {'prompt_tokens': 19220, 'completion_tokens': 1098, 'elapsed_time_model': 65601, 'tokens_per_sec': 309.71722189663865}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}