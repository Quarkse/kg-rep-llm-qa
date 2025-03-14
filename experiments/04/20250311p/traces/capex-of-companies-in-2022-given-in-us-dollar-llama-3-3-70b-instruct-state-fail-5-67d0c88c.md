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

Capex of companies in 2022 given in US dollar

***

Think: The user is asking for the capital expenditures (Capex) of companies in 2022, given in US dollars. To formulate a query, we need to identify the key resources involved, such as companies and their Capex data for 2022. We also need to consider the unit of measurement, which is US dollars.

Act: search('companies') | search('capital expenditures') | search('2022') | search('US dollar')

***

The keyword search for `companies` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1438.ttl#this **Campania** 0.4000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **Crolles** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ208812.ttl#this **Corbeil-Essonnes** 0.2981

***

The keyword search for `capital expenditures` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ26073.ttl#this **Capital Region of Denmark** 0.3282
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#capex **capex** 0.2417
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ102728.ttl#this **Ypres** 0.2417
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1507709.ttl#this **Camas** 0.2417
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ579807.ttl#this **Crolles** 0.2132

***

The keyword search for `2022` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#conf-hotchips-Gelsinger22 **Semiconductors Run the World : Hot Chips 2022.** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1207746.ttl#this **Kita-ku** 0.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ57787.ttl#this **Suqian** 0.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ128196.ttl#this **Mie Prefecture** 0.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ12556.ttl#this **Indre-et-Loire** 0.0000

***

The keyword search for `US dollar` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1205.ttl#this **Qatar Solar Technologies Doha Fab** 0.2478
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1832744.ttl#this **Muar** 0.2462
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1075.ttl#this **Tongwei Solar** 0.2335
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ845792.ttl#this **Usuki** 0.2279
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5880748.ttl#this **Holla** 0.2279

***

Think: We have identified some key resources related to companies, capital expenditures, 2022, and US dollars. However, the search results do not provide a clear connection between these concepts. We need to further explore the relationships between these resources to formulate a query.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#capex') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1205.ttl#this')

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#capex` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    tbox:capex a qb:MeasureProperty,
            owl:DatatypeProperty ;
        rdfs:label "capex"@en ;
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

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

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1205.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix ns2: <http://www.geonames.org/ontology#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1066.ttl#this> ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1205.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1205.ttl#this> a ns2:Feature,
            ns1:Site ;
        rdfs:label "Qatar Solar Technologies Doha Fab"@en ;
        ns2:featureClass ns2:S ;
        ns2:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ111387350.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .

***

Think: We have gathered more information about the key resources, including the concept of capital expenditures (capex) and its relationship to companies and sites. However, we still need to find a connection between these resources and the year 2022, as well as the unit of measurement (US dollars).

Act: search('financial report') | search('annual report') | search('2022 financial data') | deref('https://welektronik.iis.fraunhofer.de/entity/Q1060') | deref('https://welektronik.iis.fraunhofer.de/entity/Q1180')

***

The keyword search for `financial report` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5283458.ttl#this **Newport** 0.3234
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ101254.ttl#this **Newport** 0.3234
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1160.ttl#this **Wafer Export** 0.2593
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1145.ttl#this **Fineeco** 0.2425
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ33.ttl#this **Finland** 0.2425

***

The keyword search for `annual report` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5283458.ttl#this **Newport** 0.3849
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ101254.ttl#this **Newport** 0.3849
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1160.ttl#this **Wafer Export** 0.3086
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ564234.ttl#this **Annaka** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ45.ttl#this **Portugal** 0.2739

***

The keyword search for `2022 financial data` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ504690.ttl#this **Sakata** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1347432.ttl#this **Murata** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1348.ttl#this **Kolkata** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ179691.ttl#this **Niigata** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ217234.ttl#this **Ota** 0.2108

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1060` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1035.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1042.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1061.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1062.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1063.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1064.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1065.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1066.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1067.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1068.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1069.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1070.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1071.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1072.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1073.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1074.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1075.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1076.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1078.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1079.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1080.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1081.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1084.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1085.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1086.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1087.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1088.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1089.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1090.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1092.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1093.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1094.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1095.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1096.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1097.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1099.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1101.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1102.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1103.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1105.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1106.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1108.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1109.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1110.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1111.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1112.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1113.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1115.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1116.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1117.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1118.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1119.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1120.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1121.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1122.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1124.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1128.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1129.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1130.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1131.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1132.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1133.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1134.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1135.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1136.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1137.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1138.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1139.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1140.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1141.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1142.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1143.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1144.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1145.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1146.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1147.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1148.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1149.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1150.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1151.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1152.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1154.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1155.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1156.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1157.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1158.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1159.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1160.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1161.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1162.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1163.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1164.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1165.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1166.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1167.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1168.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1169.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1170.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1171.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1173.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1174.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1175.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1177.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1060> a tbox:OrganizationType ;
        rdfs:label "Materials producer"@en .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1180` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1179.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1181.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1182.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1183.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1184.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1185.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1186.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1187.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1188.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1189.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1190.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1191.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1192.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1193.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1194.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1195.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1196.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1197.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1198.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1199.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1200.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1201.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1202.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1203.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1204.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1205.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1206.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1207.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1208.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1209.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1210.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1211.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1212.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1213.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1214.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1215.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1216.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1217.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1218.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1219.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1220.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1221.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1222.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1223.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1224.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1225.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1226.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1227.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1228.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1229.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1230.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1231.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1232.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1233.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1234.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1235.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1236.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1259.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1260.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1261.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1262.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1263.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1264.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1265.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1266.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1267.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1268.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1269.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1270.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1271.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1272.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1273.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1274.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1275.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1276.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1277.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1278.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1279.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1280.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1281.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1282.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1283.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1284.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1285.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1286.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1287.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1288.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1289.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1290.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1291.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1292.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1293.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1294.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1295.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1296.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1297.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1298.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1299.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1300.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1305.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1306.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1307.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1308.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1310.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q1180> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1180> a tbox:SiteType ;
        rdfs:label "Material fab"@en .

***

Think: We have gathered more information about the key resources, including the concept of capital expenditures (capex) and its relationship to companies and sites. We have also identified the organization type and site type for some companies and sites. However, we still need to find a connection between these resources and the year 2022, as well as the unit of measurement (US dollars).

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?capex WHERE { ?company a tbox:Organization ; tbox:organizationType tbox:MaterialsProducer ; tbox:capex ?capex . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?capex WHERE { ?company a tbox:Organization ; tbox:organizationType tbox:MaterialsProducer ; tbox:capex ?capex . }')`.

***

Think: The query did not return any results, which means that there is no data in the knowledge graph that matches the query. This could be due to several reasons, such as the data not being available or the query being too specific.

Act: fail('No data found for companies with capex in 2022.')

{'loop': {'id': '67d0c88c', 'question': 'Capex of companies in 2022 given in US dollar', 'iterations': 5, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?capex WHERE { ?company a tbox:Organization ; tbox:organizationType tbox:MaterialsProducer ; tbox:capex ?capex . }', 'elapsed_time': 79351}, 'tokens': {'prompt_tokens': 43460, 'completion_tokens': 646, 'elapsed_time_model': 65824, 'tokens_per_sec': 670.0506251477216}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}