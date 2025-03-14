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

Total equity of companies given in New Taiwan dollar

***

Think: The user is asking for the total equity of companies given in New Taiwan dollar. To formulate a query, I need to identify the key resources involved, such as companies and their equity information. I also need to consider the currency, which is New Taiwan dollar.

Act: search('company') | search('equity') | search('New Taiwan dollar')

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **Canyon County** 0.3443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **Cook County** 0.3443

***

The keyword search for `equity` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity **total equity** 0.6614
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1147.ttl#this **Trinity** 0.3536
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ494254.ttl#this **Elk County** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1359251.ttl#this **Kaili City** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ680842.ttl#this **Yilan City** 0.3062

***

The keyword search for `New Taiwan dollar` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this **Taiwan** 0.4867
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ244898.ttl#this **New Taipei** 0.4636
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this **Taiwan Semiconductor Manufacturing Company Taiwan Fab** 0.3363
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ32081.ttl#this **Taiwan Province** 0.3338
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1384.ttl#this **New York** 0.2902

***

Think: The search results for `company`, `equity`, and `New Taiwan dollar` have returned several relevant resources, including a company, a property for total equity, and the currency. To further formulate the query, I need to gather more information about these resources and their relationships.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this')

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    tbox:totalEquity a qb:MeasureProperty,
            owl:DatatypeProperty ;
        rdfs:label "total equity"@en ;
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

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

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ865.ttl#this> a ns1:Feature ;
        rdfs:label "Taiwan"@en ;
        ns1:featureClass ns1:A,
            ns1:P ;
        ns1:featureCode ns1:A.PCLI ;
        owl:sameAs <http://www.wikidata.org/entity/Q865>,
            <https://sws.geonames.org/1668284/> .

***

Think: The descriptions of the resources have provided more information about the company, the total equity property, and the region. To further formulate the query, I need to gather more information about the relationships between these resources and the currency.

Act: query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?x WHERE { ?x rdfs:label ?y . FILTER (lang(?y) = \'en\') }') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#headquarter') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this')

***

Error in `query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?x WHERE { ?x rdfs:label ?y . FILTER (lang(?y) = \'en\') }'). Expected SelectQuery, found 'FILTER'  (at char 232), (line:1, col:233)

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#headquarter` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix ns2: <http://www.w3.org/2003/01/geo/wgs84_pos#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#headquarter> a ns1:Feature,
            ns2:SpatialThing,
            <https://www.w3.org/ns/org#Site> ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ717461.ttl#this> ;
        ns2:lat 24.769558 ;
        ns2:long 121.01206 .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this> a ns1:Feature,
            <https://www.w3.org/ns/org#Site> ;
        rdfs:label "Taiwan Semiconductor Manufacturing Company Taiwan Fab"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ245023.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .

***

Think: The descriptions of the headquarter and the site have provided more information about their locations and types. However, the query to retrieve labels in English failed due to a syntax error. To further formulate the query, I need to correct the query and gather more information about the relationships between the company, its sites, and the currency.

Act: query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?x ?y WHERE { ?x rdfs:label ?y . FILTER (langMatches(lang(?y), "en")) }') | deref('https://welektronik.iis.fraunhofer.de/entity/Q297') | deref('https://welektronik.iis.fraunhofer.de/entity/Q20')

***

The query 'PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?x ?y WHERE { ?x rdfs:label ?y . FILTER (langMatches(lang(?y), "en")) }' returned the following solution (first 20 results).
    x,y
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1022.ttl#this,Shanghai Micro Electronics Equipment
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1025.ttl#this,Advanced Micro-Fabrication Equipment
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1026.ttl#this,NAURA Technology Group
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1027.ttl#this,Präzisionsteilefertigung Steffen Pfüller
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1028.ttl#this,Multibeam Corporation
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ103.ttl#this,Changxin Memory Technologies
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1034.ttl#this,Episil Precision
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1037.ttl#this,HCT Co.
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1039.ttl#this,Jenoptik
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1040.ttl#this,Zeiss
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1043.ttl#this,Mühlbauer
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ105.ttl#this,D-Wave Systems
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1063.ttl#this,High-Purity Silicon America Corporation
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1066.ttl#this,Qatar Solar Technologies
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1068.ttl#this,Sichuan Yongxiang Energy Technology
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this,Opto Diode
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1071.ttl#this,Asia Silicon (Qinghai)
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1074.ttl#this,Anyang Dingsheng Silicon Industry
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1076.ttl#this,Xingjiang East Hope New Energy
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1081.ttl#this,Qiya Silicon

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q297` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q297> a tbox:SiteType ;
        rdfs:label "Chip fab"@en .

***

No results for `deref('https://welektronik.iis.fraunhofer.de/entity/Q20')`.

***

Think: The query to retrieve labels in English has returned several results, including companies and their labels. The descriptions of the site type and the company have provided more information about their types and labels. However, the description of the company with ID Q20 was not found. To further formulate the query, I need to gather more information about the relationships between the companies, their sites, and the currency.

Act: query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?x ?y WHERE { ?x rdfs:label ?y . FILTER (langMatches(lang(?y), "en")) ?x :totalEquity ?y }') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this') | deref('https://welektronik.iis.fraunhofer.de/entity/Q297')

***

No results for `query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?x ?y WHERE { ?x rdfs:label ?y . FILTER (langMatches(lang(?y), "en")) ?x :totalEquity ?y }')`.

***

Do not repeat actions.

***

Do not repeat actions.

***

Think: The query to retrieve companies with their total equity was not successful. The description of the company with ID Q20 was already retrieved in a previous action. The description of the site type was also already retrieved in a previous action. To further formulate the query, I need to gather more information about the relationships between the companies, their sites, and the currency.

Act: fail('Unable to formulate a query to retrieve the total equity of companies in New Taiwan dollar.')

{'loop': {'id': '67d15655', 'question': 'Total equity of companies given in New Taiwan dollar', 'iterations': 6, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?x ?y WHERE { ?x rdfs:label ?y . FILTER (langMatches(lang(?y), "en")) ?x :totalEquity ?y }', 'elapsed_time': 76054}, 'tokens': {'prompt_tokens': 20858, 'completion_tokens': 1022, 'elapsed_time_model': 67210, 'tokens_per_sec': 325.54348719050574}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}