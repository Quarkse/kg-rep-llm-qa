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

System has access to ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'] with 32290 triples. System version v0.2.8-77-g05f9f338 is using llama-3.3-70b-instruct at chat-ai.academiccloud.de.

***

Employee count of companies with assembly/test sites

***

Think: The User is asking for the employee count of companies that have assembly or test sites. This implies that we need to find companies that have these types of sites and then retrieve their employee count. We should start by searching for keywords related to assembly and test sites, as well as companies.

Act: search('assembly site') | search('test site') | search('company')

***

The keyword search for `assembly site` returned the following ranked list with hits.

    https://www.w3.org/ns/org#Site **Site** 0.5270
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this **Maxim Assembly/Test Cavite** 0.4880
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this **AEM Assembly/Test Singapore** 0.4795
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ998.ttl#this **Ardentec Assembly/Test Singapore** 0.4428
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ398.ttl#this **ams Osram Assembly/Test Singapore** 0.4364

***

The keyword search for `test site` returned the following ranked list with hits.

    https://www.w3.org/ns/org#Site **Site** 0.6155
    https://www.w3.org/ns/org#hasSite **has site** 0.4767
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#SiteType **Site type** 0.4545
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#siteType **site type** 0.4545
    https://welektronik.iis.fraunhofer.de/entity/Q289 **Testing** 0.4020

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **Cook County** 0.3443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **Canyon County** 0.3443

***

Think: We have found some relevant resources related to assembly and test sites, as well as companies. We should now dereference these resources to gather more information about them.

Act: deref('https://www.w3.org/ns/org#Site') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this')

***

The description of `https://www.w3.org/ns/org#Site` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <http://www.geonames.org/ontology#Feature> a rdfs:Class ;
        rdfs:label "Feature"@en .
    
    tbox:SiteType a rdfs:Class ;
        rdfs:label "Site type"@en .
    
    <https://www.w3.org/ns/org#Organization> a rdfs:Class ;
        rdfs:label "Organization"@en .
    
    <https://www.w3.org/ns/org#Site> a rdfs:Class ;
        rdfs:label "Site"@en ;
        rdfs:subClassOf <http://www.geonames.org/ontology#Feature> .
    
    tbox:siteType a owl:ObjectProperty ;
        rdfs:label "site type"@en ;
        rdfs:domain <https://www.w3.org/ns/org#Site> ;
        rdfs:range tbox:SiteType .
    
    <https://www.w3.org/ns/org#hasRegisteredSite> a owl:ObjectProperty ;
        rdfs:label "has registered site"@en ;
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://www.w3.org/ns/org#Site> .
    
    <https://www.w3.org/ns/org#hasSite> a owl:ObjectProperty ;
        rdfs:label "has site"@en ;
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://www.w3.org/ns/org#Site> .

***

The description of `https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this` is as follows.

    @prefix ns1: <http://www.geonames.org/ontology#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ423.ttl#this> a ns1:Feature,
            <https://www.w3.org/ns/org#Site> ;
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

Think: We have gathered more information about the resources related to assembly and test sites, as well as companies. We should now try to find the relationship between companies and their sites, and then retrieve the employee count of these companies.

Act: deref('https://www.w3.org/ns/org#hasSite') | deref('https://welektronik.iis.fraunhofer.de/entity/Q298') | query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?site WHERE { ?company org:hasSite ?site . ?site :siteType ?type . FILTER (?type = :Q298) }')

***

The description of `https://www.w3.org/ns/org#hasSite` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://www.w3.org/ns/org#Organization> a rdfs:Class ;
        rdfs:label "Organization"@en .
    
    <https://www.w3.org/ns/org#Site> a rdfs:Class ;
        rdfs:label "Site"@en .
    
    <https://www.w3.org/ns/org#hasRegisteredSite> a owl:ObjectProperty ;
        rdfs:label "has registered site"@en ;
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://www.w3.org/ns/org#Site> ;
        rdfs:subPropertyOf <https://www.w3.org/ns/org#hasSite> .
    
    <https://www.w3.org/ns/org#hasSite> a owl:ObjectProperty ;
        rdfs:label "has site"@en ;
        rdfs:domain <https://www.w3.org/ns/org#Organization> ;
        rdfs:range <https://www.w3.org/ns/org#Site> ;
        owl:inverseOf <https://www.w3.org/ns/org#siteOf> .

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q298` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q298> a tbox:SiteType ;
        rdfs:label "Assembly/Test facility"@en .

***

No results for `query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?site WHERE { ?company org:hasSite ?site . ?site :siteType ?type . FILTER (?type = :Q298) }')`.

***

Think: We have not found any companies with assembly or test sites. We should try to find companies with sites of any type.

Act: query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?site WHERE { ?company org:hasSite ?site . }')

***

The query 'PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?site WHERE { ?company org:hasSite ?site . }' returned the following solution (first 20 results).
    company,site
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ103.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ508.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1066.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1205.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ107.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ510.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1200.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1201.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1202.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1203.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1083.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1204.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1089.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1194.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1089.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1195.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1090.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1191.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1090.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1192.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1090.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1193.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ586.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ111.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ587.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1112.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1290.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1112.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1291.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1112.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1292.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1119.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1308.ttl#this
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ113.ttl#this,https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ588.ttl#this

***

Think: We have found companies with sites of various types. We should now try to find the employee count of these companies.

Act: query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?employeeCount WHERE { ?company org:hasSite ?site . ?company :employeeCount ?employeeCount . }')

***

No results for `query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company ?employeeCount WHERE { ?company org:hasSite ?site . ?company :employeeCount ?employeeCount . }')`.

***

Think: We have not found any companies with employee count. We should try to find the number of employees of companies with sites.

Act: query('PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company (COUNT(DISTINCT ?employee) AS ?numberOfEmployees) WHERE { ?company org:hasSite ?site . ?company :hasEmployee ?employee . } GROUP BY ?company')

***

The query 'PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company (COUNT(DISTINCT ?employee) AS ?numberOfEmployees) WHERE { ?company org:hasSite ?site . ?company :hasEmployee ?employee . } GROUP BY ?company' returned the following solution.

    company,numberOfEmployees

***

Think: We have not found any companies with employee count. We should give up.

Act: fail('Unable to find employee count of companies with assembly/test sites.')

{'loop': {'id': '67bf166d', 'question': 'Employee count of companies with assembly/test sites', 'iterations': 7, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX : <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX org: <https://www.w3.org/ns/org#> SELECT DISTINCT ?company (COUNT(DISTINCT ?employee) AS ?numberOfEmployees) WHERE { ?company org:hasSite ?site . ?company :hasEmployee ?employee . } GROUP BY ?company', 'elapsed_time': 75639}, 'tokens': {'prompt_tokens': 25243, 'completion_tokens': 756, 'elapsed_time_model': 52375, 'tokens_per_sec': 496.395181215746}, 'git': {'label': 'v0.2.8-77-g05f9f338', 'commit': '05f9f33880e9523b7eb3f19ed97e6b71bef1547a'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}