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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 48029 triples. System version v0.2.8-90-ga084b38e is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Total assets of fabless companies

***

Think: The user is asking for the total assets of fabless companies. To formulate a query, we need to identify the key resources involved, which are "fabless companies" and "total assets". We should start by finding the URIs for these resources in the knowledge graph.

Act: search('fabless company') | search('total assets')

***

The keyword search for `fabless company` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q286 **Fabless** 0.6468
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5336
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ663.ttl#this **Taiwan Semiconductor Manufacturing Company  Washington Fab** 0.3080
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ220005.ttl#this **Daviess County** 0.3032
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ115148.ttl#this **Dutchess County** 0.2941

***

The keyword search for `total assets` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalAssets **total assets** 1.0000
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalEquity **total equity** 0.4286
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalRevenue **total revenue** 0.4140
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ288.ttl#this **Tours** 0.3030
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ37043.ttl#this **Tallahassee** 0.2965

***

Think: We have found the URIs for "fabless company" and "total assets". The next step is to dereference these resources to gather more information about them. We can use the `deref()` action to get all triples with the resource URIs in the subject position.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q286') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalAssets')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q286` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ118.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ129.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ136.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ138.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ144.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ151.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ153.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ154.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ155.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ178.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ223.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ236.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ24.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ240.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ241.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ242.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ243.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ245.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ246.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ247.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ248.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ249.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ250.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ251.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ254.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ255.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ257.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ258.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ259.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ260.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ261.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ265.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ266.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ267.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ270.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ271.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ273.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ274.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ275.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ276.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ277.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ29.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ39.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ40.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ42.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ665.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ666.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ669.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ671.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ680.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ682.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ683.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ686.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ687.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ691.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ696.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ697.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ699.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ700.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ701.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ702.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ704.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ707.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ708.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ711.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ712.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ713.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ714.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ715.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ716.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ718.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ719.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ723.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ724.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ725.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ726.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ728.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ732.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ734.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ735.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ736.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ737.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ738.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ739.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ774.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ788.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ789.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ790.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ791.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ794.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ795.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ796.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ797.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ802.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ805.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ806.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ85.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ92.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ98.ttl#this> tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q286> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q286> a tbox:OrganizationType ;
        rdfs:label "Fabless"@en ;
        tbox:organizationTypeOf <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ118.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ129.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ136.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ138.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ144.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ151.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ153.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ154.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ155.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ178.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ223.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ236.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ24.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ240.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ241.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ242.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ243.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ245.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ246.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ247.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ248.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ249.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ250.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ251.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ254.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ255.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ257.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ258.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ259.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ260.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ261.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ264.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ265.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ266.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ267.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ270.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ271.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ273.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ274.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ275.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ276.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ277.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ29.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ39.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ40.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ42.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ43.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ44.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ633.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ665.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ666.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ669.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ671.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ680.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ681.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ682.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ683.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ686.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ687.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ691.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ696.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ697.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ699.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ700.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ701.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ702.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ704.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ705.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ707.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ708.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ711.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ712.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ713.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ714.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ715.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ716.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ718.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ719.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ721.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ723.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ724.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ725.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ726.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ728.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ732.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ734.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ735.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ736.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ737.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ738.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ739.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ774.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ788.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ789.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ790.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ791.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ794.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ795.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ796.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ797.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ802.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ805.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ806.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ85.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ92.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ98.ttl#this> .

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalAssets` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    tbox:totalAssets a qb:MeasureProperty,
            owl:DatatypeProperty ;
        rdfs:label "total assets"@en ;
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

***

Think: We have gathered information about the "fabless company" and "total assets" resources. The next step is to construct a query that retrieves the total assets of fabless companies. We can use the `query()` action to evaluate a SPARQL query.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT ?x ?y WHERE { ?x a :Q286 . ?x tbox:totalAssets ?y . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT ?x ?y WHERE { ?x a :Q286 . ?x tbox:totalAssets ?y . }')`.

***

Think: The query did not return any results. This could be due to the fact that the "fabless company" resource is not directly related to the "total assets" property. We need to find a way to connect these two resources. Let's try to find a property that relates a company to its financial data.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q286') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#totalAssets') | search('financial data')

***

Do not repeat actions.

***

Do not repeat actions.

***

The keyword search for `financial data` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ504690.ttl#this **Sakata** 0.2652
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1347432.ttl#this **Murata** 0.2652
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1348.ttl#this **Kolkata** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1145.ttl#this **Fineeco** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ33.ttl#this **Finland** 0.2500

***

Think: We have found some resources related to "financial data", but they do not seem to be directly related to the "fabless company" or "total assets" resources. We need to find a way to connect these resources. Let's try to find a property that relates a company to its financial data.

Act: search('company financial data') | search('fabless company financials') | search('financial statement') | search('balance sheet')

***

The keyword search for `company financial data` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.2858
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ1438.ttl#this **Campania** 0.2582
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.2552
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ800.ttl#this **Costa Rica** 0.2357
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this **Taiwan Semiconductor Manufacturing Company Tainan Fab** 0.2352

***

The keyword search for `fabless company financials` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q286 **Fabless** 0.5669
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.3780
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this **Taiwan Semiconductor Manufacturing Company Tainan Fab** 0.2662
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this **Taiwan Semiconductor Manufacturing Company Nanjing Fab** 0.2440
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ659.ttl#this **Taiwan Semiconductor Manufacturing Company Hsinchu Fab** 0.2273

***

The keyword search for `financial statement` returned the following ranked list with hits.

    http://xmlns.com/foaf/0.1/Document **Document** 0.2760
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ196.ttl#this **Cyient** 0.2315
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ4354448.ttl#this **Southern Finland Regional State Administrative Agency** 0.2312
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ161036.ttl#this **Free State of Prussia** 0.2275
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3940508.ttl#this **South-Western Finland Regional State Administrative Agency** 0.2217

***

The keyword search for `balance sheet` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ142.ttl#this **France** 0.2942
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#13165754 **Balancing your family, faith & work** 0.2708
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ55737.ttl#this **Mabalacat** 0.2509
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ3834.ttl#this **Constance** 0.2509
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ59725905.ttl#this **Ballycummin** 0.2308

***

Think: We have found some resources related to financial data, but we still need to find a way to connect them to the "fabless company" and "total assets" resources. Let's try to find a property that relates a company to its financial data.

Act: fail('Could not find a property that relates a company to its financial data.')

{'loop': {'id': '67d049c8', 'question': 'Total assets of fabless companies', 'iterations': 6, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT ?x ?y WHERE { ?x a :Q286 . ?x tbox:totalAssets ?y . }', 'elapsed_time': 181803}, 'tokens': {'prompt_tokens': 63347, 'completion_tokens': 647, 'elapsed_time_model': 75212, 'tokens_per_sec': 850.8446127820846}, 'git': {'label': 'v0.2.8-90-ga084b38e', 'commit': 'a084b38e1d7b67039f0d60b14814ef1241c00fd7'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}