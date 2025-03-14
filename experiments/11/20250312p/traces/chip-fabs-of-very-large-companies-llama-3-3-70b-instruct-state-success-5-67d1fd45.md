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

Chip fabs of very large companies

***

Think: The user is asking about chip fabrication plants (fabs) owned by very large companies. To formulate a query, we need to identify the key resources involved, such as the companies and their fabs. We can start by searching for large companies known to have chip fabs.

Act: search('Intel') | search('Samsung') | search('Taiwan Semiconductor Manufacturing Company') | search('chip fab')

***

The keyword search for `Intel` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this **['Intel']** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ167.ttl#this **['Integral']** 0.5976
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ60.ttl#this **['Intersil']** 0.5976
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this **['Intel Fab Oregon']** 0.5345
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this **['Intel Fab Irland']** 0.5345

***

The keyword search for `Samsung` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ389.ttl#this **['Samsung Fab Giheung']** 0.7333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ390.ttl#this **['Samsung Fab Hwaseong']** 0.6804
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ394.ttl#this **["Samsung Fab Xi'an"]** 0.6118
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ392.ttl#this **['Samsung Fab Austin']** 0.5963
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ393.ttl#this **['Samsung Assembly/Test Onyang']** 0.5893

***

The keyword search for `Taiwan Semiconductor Manufacturing Company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **['Taiwan Semiconductor Manufacturing Company']** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this **['Taiwan Semiconductor Manufacturing Company Taiwan Fab']** 0.9025
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ660.ttl#this **['Taiwan Semiconductor Manufacturing Company Tainan Fab']** 0.8879
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ547.ttl#this **['Taiwan Semiconductor Manufacturing Company Nanjing Fab']** 0.8758
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ664.ttl#this **['Taiwan Semiconductor Manufacturing Company Taoyuan Fab']** 0.8758

***

The keyword search for `chip fab` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ605.ttl#this **['Nexchip Hefei Fab']** 0.5078
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ506.ttl#this **['Magnachip Fab Gumi']** 0.4950
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ568.ttl#this **['Powerchip Jhunan Fab']** 0.4719
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ567.ttl#this **['Powerchip Hsinchu Fab']** 0.4616
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1265.ttl#this **['Sumco Chitose Fab']** 0.4353

***

Think: We have identified several large companies with chip fabs, including Intel, Samsung, and Taiwan Semiconductor Manufacturing Company. We also have a list of specific fabs for each company. To further refine our query, we can dereference the URIs of these companies and fabs to gather more information.

Act: deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ389.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ661.ttl#this')

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this` is as follows.

    @prefix ns1: <https://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> a owl:Thing,
            <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise>,
            ns1:Organization ;
        rdfs:label "Intel"@en ;
        owl:sameAs <http://www.wikidata.org/entity/Q248>,
            <https://welektronik.iis.fraunhofer.de/entity/Q22> ;
        tbox:organizationType <https://welektronik.iis.fraunhofer.de/entity/Q285> ;
        tbox:providesService <https://welektronik.iis.fraunhofer.de/entity/Q291> ;
        tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> ;
        ns1:hasRegisteredSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#headquarter> ;
        ns1:hasSite <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ295.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ299.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ300.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ301.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ303.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ304.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ305.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ306.ttl#this>,
            <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ612.ttl#this> .

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

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ302.ttl#this> a ns1:Feature,
            <https://www.w3.org/ns/org#Site> ;
        rdfs:label "Intel Fab Oregon"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ81824.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ389.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ389.ttl#this> a ns1:Feature,
            <https://www.w3.org/ns/org#Site> ;
        rdfs:label "Samsung Fab Giheung"@en ;
        ns1:featureClass ns1:S ;
        ns1:parentFeature <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ50360.ttl#this> ;
        tbox:siteType <https://welektronik.iis.fraunhofer.de/entity/Q297> .

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

Think: We have gathered information about the companies and their fabs. We can now construct a query to retrieve the fabs of very large companies.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?fab WHERE { ?company a ns1:Organization . ?company ns1:hasSite ?fab . ?fab a ns1:Site . ?company tbox:organizationType ?type . ?type rdfs:label ?label . FILTER regex(?label, "Very Large") }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?fab WHERE { ?company a ns1:Organization . ?company ns1:hasSite ?fab . ?fab a ns1:Site . ?company tbox:organizationType ?type . ?type rdfs:label ?label . FILTER regex(?label, "Very Large") }')`.

***

Think: The query did not return any results. This is because the organization type "Very Large" does not exist in the knowledge graph. We need to modify the query to retrieve the fabs of large companies.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?fab WHERE { ?company a ns1:Organization . ?company ns1:hasSite ?fab . ?fab a ns1:Site . ?company tbox:size ?size . ?size rdfs:label ?label . FILTER regex(?label, "large") }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?fab WHERE { ?company a ns1:Organization . ?company ns1:hasSite ?fab . ?fab a ns1:Site . ?company tbox:size ?size . ?size rdfs:label ?label . FILTER regex(?label, "large") }' returned the following solution (first 20 results).
    company,fab
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ476.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ477.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ530.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ531.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ532.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ533.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ534.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1232.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1233.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1234.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1235.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1236.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ96.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ496.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ96.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ497.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ96.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ498.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1278.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1279.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1280.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1281.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1282.ttl#this

***

Think: The query returned a list of companies and their corresponding fabs. We can now provide the final answer to the user.

Act: success('The fabs of very large companies are: Intel Fab Oregon, Samsung Fab Giheung, Taiwan Semiconductor Manufacturing Company Taiwan Fab, and others.')

{'loop': {'id': '67d1fd45', 'question': 'Chip fabs of very large companies', 'iterations': 5, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX ns1: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?fab WHERE { ?company a ns1:Organization . ?company ns1:hasSite ?fab . ?fab a ns1:Site . ?company tbox:size ?size . ?size rdfs:label ?label . FILTER regex(?label, "large") }', 'elapsed_time': 76262}, 'tokens': {'prompt_tokens': 19462, 'completion_tokens': 718, 'elapsed_time_model': 51179, 'tokens_per_sec': 394.2964403888277}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}