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

Small companies

***

Think: The user has mentioned "small companies". To formulate a query, we need to identify the key resources and find their URIs. We can start by searching for keywords related to small companies.

Act: search('small company') | search('enterprise') | search('business')

***

The keyword search for `small company` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1046 **['Small enterprise size.', 'Small']** 0.4725
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.4131
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **['Comal County']** 0.3873
    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Company that produces semiconductors for other companies.', 'Foundry']** 0.3707
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this **['Sony']** 0.3162

***

The keyword search for `enterprise` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['Enterprise', 'An enterprise sells products to customers.']** 0.7285
    https://welektronik.iis.fraunhofer.de/entity/Q1045 **['Classification of enterprise size.', 'Enterprise size']** 0.7057
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#observedEnterprise **['Enterprise/organization that an observed key figure is about.', 'observed enterprise']** 0.5581
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['Links the customer enterprise in a supply flow between two enterprises.', 'customer']** 0.5071
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier **['Links the supplying enterprise in a supply flow between two enterprises.', 'supplier']** 0.4848

***

The keyword search for `business` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.5060
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **['Tampines']** 0.3000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2631
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#conf-hotchips-Gelsinger12 **['Cloud transforms it Big Data transforms business.']** 0.2627
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ467664.ttl#this **['Butte']** 0.2390

***

Think: We have found several URIs related to small companies, including https://welektronik.iis.fraunhofer.de/entity/Q1046, which is described as a "Small enterprise size". We can now dereference this URI to gather more information about small companies.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q1046')

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
        rdfs:label "Small"@en ;
        rdfs:comment "Small enterprise size."@en .

***

Think: We have found that the URI https://welektronik.iis.fraunhofer.de/entity/Q1046 represents a "Small enterprise size". We can now use this information to construct a query to find small companies.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> }' returned the following solution (first 20 results).
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

Think: We have successfully constructed a query to find small companies and obtained a list of companies that match the criteria. We can now confirm that the query is final and provide a concise message explaining the relevant steps we took.

Act: success('We have identified small companies by searching for the keyword "small company" and then using the URI of the "Small enterprise size" to construct a query. The query returned a list of companies that match the criteria.')

{'loop': {'id': '67d216b8', 'question': 'Small companies', 'iterations': 4, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?company WHERE { ?company tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1046> }', 'elapsed_time': 54315}, 'tokens': {'prompt_tokens': 21968, 'completion_tokens': 358, 'elapsed_time_model': 44720, 'tokens_per_sec': 499.23550545613546}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}