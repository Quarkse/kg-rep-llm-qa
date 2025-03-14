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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 37057 triples. System version v0.2.8-91-g5e507554 is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Small companies

***

Think: The user has mentioned "small companies". To formulate a query, we need to identify the key resources and find their URIs. We can start by searching for keywords related to small companies.

Act: search('small company') | search('enterprise') | search('business')

***

The keyword search for `small company` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1046 **Small** 0.5855
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.4131
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.3873
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this **Sony** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ498141.ttl#this **Marshall County** 0.3131

***

The keyword search for `enterprise` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **Enterprise** 1.0000
    https://welektronik.iis.fraunhofer.de/entity/Q1045 **Enterprise size** 0.8402
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#observedEnterprise **observed enterprise** 0.6929
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ35775.ttl#this **Boise** 0.3273
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#journals-dt-WagnerG05 **Driving the $5 Billion Innovation Engine at Intel: An Interview with Patrick P. Gelsinger, Digital Enterprise Group Senior Vice President and General Manager, Intel.** 0.3079

***

The keyword search for `business` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5060
    https://welektronik.iis.fraunhofer.de/entity/Q286 **Fabless** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **Tampines** 0.3000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **Philippines** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#conf-hotchips-Gelsinger12 **Cloud transforms it Big Data transforms business.** 0.2627

***

Think: We have found several URIs related to small companies, including https://welektronik.iis.fraunhofer.de/entity/Q1046, https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this, and https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise. To gather more information about these resources, we can dereference them.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q1046') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this') | deref('https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1046` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ101.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ103.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1035.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ104.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ106.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1067.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1080.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1085.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1086.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1087.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1097.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1103.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1111.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ112.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1133.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ114.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1148.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1149.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ117.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1178.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ119.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ129.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ134.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ136.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ137.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ139.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ140.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ152.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ153.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ154.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ155.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ159.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ161.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ164.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ165.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ168.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ169.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ243.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ249.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ250.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ251.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ255.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ257.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ258.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ260.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ261.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ262.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ266.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ267.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ268.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ269.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ270.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ271.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ273.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ275.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ276.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ277.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ57.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ665.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ666.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ667.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ669.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ682.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ683.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ684.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ690.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ691.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ694.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ697.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ698.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ701.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ702.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ704.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ707.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ708.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ711.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ712.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ714.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ716.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ717.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ718.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ722.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ723.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ724.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ725.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ726.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ727.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ728.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ733.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ735.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ736.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ737.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ738.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ739.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ774.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ788.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ789.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ790.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ792.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ794.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ796.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ797.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ798.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ802.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ805.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1046> a <https://welektronik.iis.fraunhofer.de/entity/Q1045> ;
        rdfs:label "Small"@en .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix ns2: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns2:Organization ;
        rdfs:label "Active Business Company"@en ;
        ns1:locatedIn <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ183.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ279128.ttl#this> ;
        owl:sameAs <http://www.wikidata.org/entity/Q124743799>,
            <https://welektronik.iis.fraunhofer.de/entity/Q1104> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q1060> ;
        ns2:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#headquarter> .

***

The description of `https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> a rdfs:Class ;
        rdfs:label "Enterprise"@en ;
        rdfs:subClassOf <https://www.w3.org/ns/org#Organization> .
    
    <https://purl.org/supply-network/onto#SupplyFlow> a rdfs:Class ;
        rdfs:label "Supply Flow"@en .
    
    <https://www.w3.org/ns/org#Organization> a rdfs:Class ;
        rdfs:label "Organization"@en .
    
    tbox:hasCustomer a owl:ObjectProperty ;
        rdfs:label "has customer"@en ;
        rdfs:domain <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> ;
        rdfs:range <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> .
    
    tbox:hasSupplier a owl:ObjectProperty ;
        rdfs:label "has supplier"@en ;
        rdfs:domain <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> ;
        rdfs:range <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer> a owl:ObjectProperty ;
        rdfs:label "customer"@en ;
        rdfs:domain <https://purl.org/supply-network/onto#SupplyFlow> ;
        rdfs:range <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier> a owl:ObjectProperty ;
        rdfs:label "supplier"@en ;
        rdfs:domain <https://purl.org/supply-network/onto#SupplyFlow> ;
        rdfs:range <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> .

***

Think: We have gathered information about the resources related to small companies. We can see that `https://welektronik.iis.fraunhofer.de/entity/Q1046` is a size of a company, and `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this` is an active business company. We also have information about the enterprise ontology, which defines the concept of an enterprise and its relationships with customers and suppliers.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> . }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> . }' returned the following solution (first 20 results).
    company
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ103.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ115.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ130.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ139.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ154.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ165.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ166.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ168.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ243.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ250.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ267.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ271.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ275.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ277.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ672.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ697.ttl#this

***

Think: We have found the companies that have the size "Small". We can now provide the final answer to the user.

Act: success('The companies that are small are listed.')

{'loop': {'id': '67d188b5', 'question': 'Small companies', 'iterations': 4, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?company WHERE { ?company tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> . }', 'elapsed_time': 46492}, 'tokens': {'prompt_tokens': 24538, 'completion_tokens': 531, 'elapsed_time_model': 34527, 'tokens_per_sec': 726.0681503719101}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}