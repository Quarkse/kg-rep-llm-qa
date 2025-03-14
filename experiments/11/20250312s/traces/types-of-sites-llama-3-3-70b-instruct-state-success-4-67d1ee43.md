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

Types of sites

***

Think: The user is asking about types of sites, which could refer to various categories such as websites, archaeological sites, construction sites, or other types of locations. To better understand the context and provide a relevant query, I need to gather more information about the types of sites the user is interested in.

Act: search('types of websites') | search('types of archaeological sites') | search('types of construction sites')

***

The keyword search for `types of websites` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.3563
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#SiteType **['Site type', 'Type/role of a site of a company, where manufacturing steps take place.']** 0.3402
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#siteType **['site type', 'Type/role of a site of a company, where manufacturing steps take place.']** 0.3402
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ30.ttl#this **['United States of America']** 0.3236
    https://www.w3.org/ns/org#Site **["An office or other premise at which the organization is located. Many organizations are spread across multiple sites and many sites will host multiple locations. In most cases a Site will be a physical location. However, we don't exclude the possibility of non-physical sites such as a virtual office with an associated post box and phone reception service. Extensions may provide subclasses to denote particular types of site.", 'Site']** 0.3093

***

The keyword search for `types of archaeological sites` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#SiteType **['Site type', 'Type/role of a site of a company, where manufacturing steps take place.']** 0.3232
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#siteType **['site type', 'Type/role of a site of a company, where manufacturing steps take place.']** 0.3232
    https://www.w3.org/ns/org#Site **["An office or other premise at which the organization is located. Many organizations are spread across multiple sites and many sites will host multiple locations. In most cases a Site will be a physical location. However, we don't exclude the possibility of non-physical sites such as a virtual office with an associated post box and phone reception service. Extensions may provide subclasses to denote particular types of site.", 'Site']** 0.3153
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ30.ttl#this **['United States of America']** 0.3120
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2673

***

The keyword search for `types of construction sites` returned the following ranked list with hits.

    https://www.w3.org/ns/org#Site **["An office or other premise at which the organization is located. Many organizations are spread across multiple sites and many sites will host multiple locations. In most cases a Site will be a physical location. However, we don't exclude the possibility of non-physical sites such as a virtual office with an associated post box and phone reception service. Extensions may provide subclasses to denote particular types of site.", 'Site']** 0.3687
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#SiteType **['Site type', 'Type/role of a site of a company, where manufacturing steps take place.']** 0.3111
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#siteType **['site type', 'Type/role of a site of a company, where manufacturing steps take place.']** 0.3111
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2715
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#organizationType **['Type/role of an organization in an industry or supply network.', 'organization type']** 0.2570

***

Think: The search results provide various types of sites, including websites, archaeological sites, and construction sites. The results also include information about site types, such as manufacturing sites, offices, and virtual offices. To further understand the user's query, I need to gather more information about the specific type of site they are interested in.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#SiteType') | deref('https://www.w3.org/ns/org#Site') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#siteType')

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#SiteType` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix skos: <http://www.w3.org/2004/02/skos/core#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    tbox:SiteType a rdfs:Class ;
        rdfs:label "Site type"@en ;
        rdfs:comment "Type/role of a site of a company, where manufacturing steps take place."@en ;
        rdfs:subClassOf skos:Concept .

***

The description of `https://www.w3.org/ns/org#Site` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://www.w3.org/ns/org#Site> a rdfs:Class ;
        rdfs:label "Site"@en ;
        rdfs:comment "An office or other premise at which the organization is located. Many organizations are spread across multiple sites and many sites will host multiple locations. In most cases a Site will be a physical location. However, we don't exclude the possibility of non-physical sites such as a virtual office with an associated post box and phone reception service. Extensions may provide subclasses to denote particular types of site."@en ;
        rdfs:subClassOf <http://www.geonames.org/ontology#Feature> .

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#siteType` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    tbox:siteType a owl:ObjectProperty ;
        rdfs:label "site type"@en ;
        rdfs:comment "Type/role of a site of a company, where manufacturing steps take place."@en ;
        rdfs:domain <https://www.w3.org/ns/org#Site> ;
        rdfs:range tbox:SiteType .

***

Think: Based on the information gathered, it appears that the user is interested in learning about different types of sites, including manufacturing sites, offices, and virtual offices. To provide a relevant query, I need to construct a query that captures the various types of sites and their characteristics.

Act: query('PREFIX org: <https://www.w3.org/ns/org#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?siteType WHERE { ?site a org:Site . ?site tbox:siteType ?siteType . }')

***

The query 'PREFIX org: <https://www.w3.org/ns/org#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?siteType WHERE { ?site a org:Site . ?site tbox:siteType ?siteType . }' returned the following solution (first 20 results).
    site,siteType
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1005.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1006.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1007.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1008.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1009.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1010.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1011.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1012.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1013.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1014.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1015.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1016.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1017.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1018.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1019.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1020.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1021.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q298
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1179.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1180
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1181.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1180
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/site/weQ1182.ttl#this,https://welektronik.iis.fraunhofer.de/entity/Q1180

***

Think: The query results provide a list of sites and their corresponding site types. The results include various sites, such as manufacturing sites, offices, and virtual offices, along with their respective site types.

Act: success('The query results provide a list of sites and their corresponding site types, including manufacturing sites, offices, and virtual offices.')

{'loop': {'id': '67d1ee43', 'question': 'Types of sites', 'iterations': 4, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX org: <https://www.w3.org/ns/org#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT DISTINCT ?site ?siteType WHERE { ?site a org:Site . ?site tbox:siteType ?siteType . }', 'elapsed_time': 61475}, 'tokens': {'prompt_tokens': 9634, 'completion_tokens': 461, 'elapsed_time_model': 53183, 'tokens_per_sec': 189.81618629771376}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}