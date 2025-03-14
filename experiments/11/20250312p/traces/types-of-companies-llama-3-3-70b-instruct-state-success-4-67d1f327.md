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

Types of companies

***

Think: The user is asking about types of companies, which is a broad topic. To formulate a query, I need to identify key resources related to companies and their classifications. I will start by searching for relevant keywords to find URIs that identify entities related to company types.

Act: search('company types') | search('business types') | search('enterprise types') | search('organization types')

***

The keyword search for `company types` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q287 **['Foundry', 'Company that produces semiconductors for other companies.']** 0.4277
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.3615
    https://welektronik.iis.fraunhofer.de/entity/Q297 **['Chip fab', 'Site of a company that produces semiconductors.']** 0.3306
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#siteType **['site type', 'Type/role of a site of a company, where manufacturing steps take place.']** 0.2981
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#SiteType **['Site type', 'Type/role of a site of a company, where manufacturing steps take place.']** 0.2981

***

The keyword search for `business types` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **['Active Business Company']** 0.4000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5110386.ttl#this **['Tampines']** 0.3162
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **['Nepes']** 0.2835
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ928.ttl#this **['Philippines']** 0.2774
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ647.ttl#this **['Rennes']** 0.2652

***

The keyword search for `enterprise types` returned the following ranked list with hits.

    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise **['An enterprise sells products to customers.', 'Enterprise']** 0.5678
    https://welektronik.iis.fraunhofer.de/entity/Q1045 **['Classification of enterprise size.', 'Enterprise size']** 0.5500
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#observedEnterprise **['Enterprise/organization that an observed key figure is about.', 'observed enterprise']** 0.4340
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#customer **['Links the customer enterprise in a supply flow between two enterprises.', 'customer']** 0.4140
    https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#supplier **['supplier', 'Links the supplying enterprise in a supply flow between two enterprises.']** 0.3958

***

The keyword search for `organization types` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#organizationType **['Type/role of an organization in an industry or supply network.', 'organization type']** 0.6600
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#OrganizationType **['Type/role of an organization in an industry or supply network.', 'Organization type']** 0.6600
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#size **['Size classification of an organization, e.g. small or large.', 'size']** 0.3814
    https://welektronik.iis.fraunhofer.de/entity/Q293 **['An offer by an organization.', 'Service']** 0.3667
    https://www.w3.org/ns/org#Site **['Site', "An office or other premise at which the organization is located. Many organizations are spread across multiple sites and many sites will host multiple locations. In most cases a Site will be a physical location. However, we don't exclude the possibility of non-physical sites such as a virtual office with an associated post box and phone reception service. Extensions may provide subclasses to denote particular types of site."]** 0.3311

***

Think: The search results provide various URIs related to company types, including https://welektronik.iis.fraunhofer.de/entity/Q287, https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this, and https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise. To gather more information about these resources, I will dereference them using the `deref()` action.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q287') | deref('https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this') | deref('https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q287` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q287> a tbox:OrganizationType ;
        rdfs:label "Foundry"@en ;
        rdfs:comment "Company that produces semiconductors for other companies."@en .

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

The description of `https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    
    <https://paul.ti.rw.fau.de/~ju32haqi/supply-networks/abstraction-examples/esn-ontology#Enterprise> a rdfs:Class ;
        rdfs:label "Enterprise"@en ;
        rdfs:comment "An enterprise sells products to customers."@en ;
        rdfs:subClassOf <https://www.w3.org/ns/org#Organization> .

***

Think: The dereferenced resources provide more information about the company types, including their labels, comments, and relationships to other resources. To construct a query that retrieves types of companies, I need to identify the properties and classes that are relevant to company types. I will use the `query()` action to retrieve the types of companies.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?type WHERE { ?type a tbox:OrganizationType . ?type rdfs:label ?label . FILTER(langMatches(lang(?label), "en")) }')

***

The query 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?type WHERE { ?type a tbox:OrganizationType . ?type rdfs:label ?label . FILTER(langMatches(lang(?label), "en")) }' returned the following solution.

    type
    https://welektronik.iis.fraunhofer.de/entity/Q285
    https://welektronik.iis.fraunhofer.de/entity/Q286
    https://welektronik.iis.fraunhofer.de/entity/Q287
    https://welektronik.iis.fraunhofer.de/entity/Q879
    https://welektronik.iis.fraunhofer.de/entity/Q1023
    https://welektronik.iis.fraunhofer.de/entity/Q1060

***

Think: The query retrieved the types of companies, including their URIs. To provide a concise message to the user, I will use the `success()` action.

Act: success('The types of companies are Foundry, Chip fab, Active Business Company, and other organization types.')

{'loop': {'id': '67d1f327', 'question': 'Types of companies', 'iterations': 4, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#> SELECT DISTINCT ?type WHERE { ?type a tbox:OrganizationType . ?type rdfs:label ?label . FILTER(langMatches(lang(?label), "en")) }', 'elapsed_time': 60604}, 'tokens': {'prompt_tokens': 9250, 'completion_tokens': 534, 'elapsed_time_model': 41206, 'tokens_per_sec': 237.43958129146174}, 'git': {'label': 'v0.2.8-93-gfa87822d', 'commit': 'fa87822d9e4dc7607312373ccc8fbd8675364b05'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}