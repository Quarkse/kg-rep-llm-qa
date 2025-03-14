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

Think: The User is asking about assembly or test sites, which could be related to manufacturing, production, or quality control. To formulate a query, we need to identify key resources and find their URIs.

Act: search('assembly site') | search('test site') | search('manufacturing')

***

The keyword search for `assembly site` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q298 **['Site of a company used for assembly and/or testing of semiconductors.', 'Assembly/Test facility']** 0.4889
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this **['Maxim Assembly/Test Cavite']** 0.4880
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this **['AEM Assembly/Test Singapore']** 0.4795
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ998.ttl#this **['Ardentec Assembly/Test Singapore']** 0.4428
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ398.ttl#this **['ams Osram Assembly/Test Singapore']** 0.4364

***

The keyword search for `test site` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ908.ttl#this **['Tesna']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ51685.ttl#this **['Tempe']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this **['Maxim Assembly/Test Cavite']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this **['AEM Assembly/Test Singapore']** 0.3359
    https://welektronik.iis.fraunhofer.de/entity/Q289 **['Testing of semiconductors.', 'Testing']** 0.3313

***

The keyword search for `manufacturing` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this **['Murata Manufacturing']** 0.8257
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ149.ttl#this **['Shindengen Electric Manufacturing']** 0.6110
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **['Taiwan Semiconductor Manufacturing Company']** 0.5060
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ629.ttl#this **['Shindengen Electric Manufacturing Akita Fab']** 0.5004
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this **['Taiwan Semiconductor Manufacturing Company Nanjing Fab']** 0.5000

***

Think: We have found several URIs related to assembly and test sites, as well as manufacturing companies and facilities. To gather more information, we can dereference these URIs.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q298') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q298` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1005.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1006.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1007.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1008.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1009.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1010.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1011.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1012.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1013.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1014.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1015.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1016.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1017.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1018.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1020.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1021.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ303.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ304.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ305.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ306.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ316.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ317.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ318.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ319.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ320.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ321.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ325.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ326.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ330.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ335.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ339.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ341.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ350.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ351.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ352.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ353.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ354.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ355.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ356.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ358.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ361.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ369.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ371.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ372.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ373.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ374.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ375.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ376.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ385.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ386.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ387.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ388.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ393.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ394.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ396.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ397.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ398.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ399.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ400.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ401.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ405.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ407.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ412.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ413.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ414.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ419.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ420.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ421.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ424.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ428.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ429.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ430.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ445.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ456.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ457.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ458.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ459.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ460.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ504.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ507.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ611.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ615.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ616.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ617.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ620.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ621.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ628.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ636.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ638.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ653.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ654.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ655.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ656.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ657.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ658.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ674.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ745.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ762.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ763.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ768.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ769.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ771.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ776.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ777.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ881.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ883.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ884.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ885.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ886.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ887.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ889.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ890.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ891.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ892.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ893.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ931.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ932.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ933.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ934.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ935.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ936.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ937.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ938.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ939.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ940.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ941.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ942.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ943.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ944.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ945.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ946.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ947.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ948.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ949.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ950.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ951.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ952.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ953.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ954.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ955.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ956.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ957.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ958.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ959.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ960.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ961.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ962.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ963.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ964.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ965.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ966.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ967.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ968.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ969.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ970.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ971.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ972.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ973.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ974.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ975.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ976.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ977.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ978.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ979.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ980.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ981.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ982.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ983.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ984.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ985.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ986.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ987.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ988.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ989.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ990.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ991.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ992.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ993.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ994.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ995.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ996.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ997.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ998.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ999.ttl#this> tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q298> a tbox:SiteType ;
        rdfs:label "Assembly/Test facility"@en ;
        rdfs:comment "Site of a company used for assembly and/or testing of semiconductors."@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix ns2: <https://www.w3.org/ns/org#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this> ns2:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this> a ns1:Feature,
            ns2:Site ;
        rdfs:label "Maxim Assembly/Test Cavite"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1482.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix ns2: <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ266.ttl#Q69> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#Q69> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#Q69> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#Q69> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#capex2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#employees2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#totalrevenue2022> tbox:observedEnterprise <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ736.ttl#Q69> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ76.ttl#Q69> ns2:supplier <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> a owl:Thing,
            ns2:Enterprise,
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

Think: We have gathered information about assembly and test sites, as well as manufacturing companies. To formulate a query, we need to identify the key resources and their relationships.

Act: query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?company WHERE { ?site tbox:siteType :Q298 . ?company :hasSite ?site . }')

***

No results for `query('PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?company WHERE { ?site tbox:siteType :Q298 . ?company :hasSite ?site . }')`.

***

Think: The query did not return any results. This could be due to the fact that the property `:hasSite` is not defined in the knowledge graph. We need to use the correct property to relate companies to their sites.

Act: query('PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <https://www.w3.org/ns/org#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?company WHERE { ?site tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> . ?company ns2:hasSite ?site . }')

***

The query 'PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <https://www.w3.org/ns/org#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?company WHERE { ?site tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> . ?company ns2:hasSite ?site . }' returned the following solution (first 20 results).
    site,company
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1005.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ921.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1006.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ921.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1007.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ921.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1008.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ921.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1009.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ923.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1010.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ924.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1011.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ924.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1012.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ925.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1013.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ926.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1014.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ926.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1015.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ926.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1016.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ926.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1017.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ927.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1018.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ928.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ928.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1020.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ928.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1021.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ928.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ303.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ304.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ305.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this

***

Think: The query returned a list of assembly and test sites, along with their corresponding companies. This suggests that the knowledge graph contains information about the relationships between companies and their sites.

Act: success('The query returned a list of assembly and test sites, along with their corresponding companies.')

{'loop': {'id': '67d21990', 'question': 'Assembly/test sites', 'iterations': 5, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX ns1: <http://www.geonames.org/ontology#> PREFIX ns2: <https://www.w3.org/ns/org#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?company WHERE { ?site tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> . ?company ns2:hasSite ?site . }', 'elapsed_time': 97535}, 'tokens': {'prompt_tokens': 52221, 'completion_tokens': 578, 'elapsed_time_model': 91809, 'tokens_per_sec': 575.0916370419219}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}