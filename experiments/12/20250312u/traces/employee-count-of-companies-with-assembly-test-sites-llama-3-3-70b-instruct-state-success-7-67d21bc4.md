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

Employee count of companies with assembly/test sites

***

Think: The User is asking for the employee count of companies that have assembly or test sites. This implies that we need to find companies that have these types of sites and then retrieve their employee counts. We should start by searching for keywords related to assembly and test sites, as well as companies.

Act: search('assembly site') | search('test site') | search('company')

***

The keyword search for `assembly site` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q298 **['Assembly/Test facility', 'Site of a company used for assembly and/or testing of semiconductors.']** 0.4889
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this **['Maxim Assembly/Test Cavite']** 0.4880
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this **['AEM Assembly/Test Singapore']** 0.4795
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ998.ttl#this **['Ardentec Assembly/Test Singapore']** 0.4428
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ398.ttl#this **['ams Osram Assembly/Test Singapore']** 0.4364

***

The keyword search for `test site` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this **['Maxim Assembly/Test Cavite']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ51685.ttl#this **['Tempe']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ908.ttl#this **['Tesna']** 0.3419
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this **['AEM Assembly/Test Singapore']** 0.3359
    https://welektronik.iis.fraunhofer.de/entity/Q289 **['Testing of semiconductors.', 'Testing']** 0.3313

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.5333
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Foundry', 'Company that produces semiconductors for other companies.']** 0.5153
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **['Taiwan Semiconductor Manufacturing Company']** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **['Canyon County']** 0.3443

***

Think: We have found several companies and sites related to assembly and testing. We should now dereference these resources to gather more information about them.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q298') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this')

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

Think: We have found several sites and companies related to assembly and testing. We should now query the graph to find the employee count of companies that have assembly or test sites.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?employeeCount WHERE { ?company a <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> . ?company tbox:hasSite ?site . ?site tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> . ?company tbox:employeeCount ?employeeCount . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company ?employeeCount WHERE { ?company a <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> . ?company tbox:hasSite ?site . ?site tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> . ?company tbox:employeeCount ?employeeCount . }')`.

***

Think: The query did not return any results. This could be due to the fact that the property `tbox:hasSite` is not used in the graph, or that the property `tbox:employeeCount` is not used in the graph. We should try to find alternative properties that can be used to link companies to their sites and to their employee counts.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q1060') | deref('https://welektronik.iis.fraunhofer.de/entity/Q298') | query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?property WHERE { <https://welektronik.iis.fraunhofer.de/entity/Q1060> ?property ?value . }') | query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?property WHERE { <https://welektronik.iis.fraunhofer.de/entity/Q298> ?property ?value . }')

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
        rdfs:label "Materials producer"@en ;
        rdfs:comment "Company that produces equipment for semiconductor manufacturing."@en .

***

Do not repeat actions.

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?property WHERE { <https://welektronik.iis.fraunhofer.de/entity/Q1060> ?property ?value . }' returned the following solution.

    property
    http://www.w3.org/1999/02/22-rdf-syntax-ns#type
    http://www.w3.org/2000/01/rdf-schema#comment
    http://www.w3.org/2000/01/rdf-schema#label

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?property WHERE { <https://welektronik.iis.fraunhofer.de/entity/Q298> ?property ?value . }' returned the following solution.

    property
    http://www.w3.org/1999/02/22-rdf-syntax-ns#type
    http://www.w3.org/2000/01/rdf-schema#comment
    http://www.w3.org/2000/01/rdf-schema#label

***

Think: We have found the properties used by the entities Q1060 and Q298. We should now try to find the properties used by the companies and sites.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?property WHERE { ?company a <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> . ?company ?property ?value . }') | query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?property WHERE { ?site a <https://www.w3.org/ns/org#Site> . ?site ?property ?value . }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?property WHERE { ?company a <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> . ?company ?property ?value . }' returned the following solution.

    property
    http://www.w3.org/1999/02/22-rdf-syntax-ns#type
    http://www.w3.org/2000/01/rdf-schema#label
    http://www.w3.org/2002/07/owl#sameAs
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#organizationType
    https://www.w3.org/ns/org#hasRegisteredSite
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#size
    https://www.w3.org/ns/org#hasSite
    http://xmlns.com/foaf/0.1/homepage
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#providesService

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?property WHERE { ?site a <https://www.w3.org/ns/org#Site> . ?site ?property ?value . }' returned the following solution.

    property
    http://www.w3.org/1999/02/22-rdf-syntax-ns#type
    http://www.geonames.org/ontology#featureClass
    http://www.geonames.org/ontology#parentFeature
    http://www.w3.org/2003/01/geo/wgs84_pos#lat
    http://www.w3.org/2003/01/geo/wgs84_pos#long
    http://www.w3.org/2000/01/rdf-schema#label
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#siteType

***

Think: We have found the properties used by the companies and sites. We should now try to find the employee count of companies that have assembly or test sites.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?employeeCount WHERE { ?company a <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> . ?company org:hasSite ?site . ?site tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> . ?company tbox:size ?employeeCount . }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?employeeCount WHERE { ?company a <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> . ?company org:hasSite ?site . ?site tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> . ?company tbox:size ?employeeCount . }' returned the following solution (first 20 results).
    company,employeeCount
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ139.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ126.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ677.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ124.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1047
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ147.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ62.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ99.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ102.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1047
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ53.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ169.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ59.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1049
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1049
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1049
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ56.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1049
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ70.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1046
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ673.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1047
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ61.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ272.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1047
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ33.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1048

***

Think: We have found the employee count of companies that have assembly or test sites. We should now provide the final answer.

Act: success('The employee count of companies with assembly/test sites are as follows: ...')

{'loop': {'id': '67d21bc4', 'question': 'Employee count of companies with assembly/test sites', 'iterations': 7, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?employeeCount WHERE { ?company a <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> . ?company org:hasSite ?site . ?site tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q298> . ?company tbox:size ?employeeCount . }', 'elapsed_time': 147263}, 'tokens': {'prompt_tokens': 105520, 'completion_tokens': 1216, 'elapsed_time_model': 138422, 'tokens_per_sec': 771.0877295717022}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}