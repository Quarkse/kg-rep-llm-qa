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

Number of employees of very large companies

***

Think: The user is asking for the number of employees of very large companies. To answer this question, we need to identify the key resources involved, which are "very large companies" and "number of employees". We also need to consider what constitutes a "very large company" and how to define it in the context of the knowledge graph.

Act: search('very large company') | search('number of employees')

***

The keyword search for `very large company` returned the following ranked list with hits.

    https://welektronik.iis.fraunhofer.de/entity/Q1049 **Very large** 0.7100
    https://welektronik.iis.fraunhofer.de/entity/Q1048 **Large** 0.4226
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.3578
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.2697
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109626.ttl#this **DuPage County** 0.2309

***

The keyword search for `number of employees` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#employees **employees** 0.6742
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ2090.ttl#this **Nuremberg** 0.2697
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ906.ttl#this **Nepes** 0.2535
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23079.ttl#this **Northumberland** 0.2236
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ188712.ttl#this **Empire of Japan** 0.2169

***

Think: We have identified some key resources related to "very large companies" and "number of employees". The search results include a concept for "very large company" (https://welektronik.iis.fraunhofer.de/entity/Q1049) and a property for "employees" (https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#employees). We can use these resources to construct a query.

Act: deref('https://welektronik.iis.fraunhofer.de/entity/Q1049') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#employees')

***

The description of `https://welektronik.iis.fraunhofer.de/entity/Q1049` is as follows.

    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1075.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1092.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1098.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1123.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1175.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ143.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ150.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ163.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ245.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ254.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ31.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ45.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ54.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ56.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ59.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ63.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ65.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ67.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ679.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ68.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ69.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ699.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ706.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ709.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ719.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ76.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ82.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ85.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ90.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ91.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ92.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ94.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ95.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ96.ttl#this> tbox:size <https://welektronik.iis.fraunhofer.de/entity/Q1049> .
    
    <https://welektronik.iis.fraunhofer.de/entity/Q1049> a <https://welektronik.iis.fraunhofer.de/entity/Q1045> ;
        rdfs:label "Very large"@en .

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#employees` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    tbox:employees a qb:MeasureProperty,
            owl:DatatypeProperty ;
        rdfs:label "employees"@en ;
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

***

Think: We have obtained the descriptions of the key resources "very large company" and "number of employees". The description of "very large company" includes a list of companies that are classified as very large, and the description of "number of employees" includes information about the property "employees" which is a measure property with a range of decimal values. We can use this information to construct a query to retrieve the number of employees for very large companies.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT ?company ?employees WHERE { ?company :Q1049 ?size . ?company tbox:employees ?employees . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT ?company ?employees WHERE { ?company :Q1049 ?size . ?company tbox:employees ?employees . }')`.

***

Think: The query did not return any results. This could be due to the fact that the property "Q1049" is not a valid property for the companies, or that the companies do not have a value for the "employees" property. We need to re-evaluate the query and the data to determine the correct approach.

Act: query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT ?company ?employees WHERE { ?company tbox:size :Q1049 . ?company tbox:employees ?employees . }')

***

No results for `query('PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT ?company ?employees WHERE { ?company tbox:size :Q1049 . ?company tbox:employees ?employees . }')`.

***

Think: The query still did not return any results. This could be due to the fact that the data is not properly connected or that the query is not correctly formulated. We need to re-evaluate the data and the query to determine the correct approach.

Act: fail('Unable to retrieve the number of employees for very large companies. The query did not return any results.')

{'loop': {'id': '67d1918e', 'question': 'Number of employees of very large companies', 'iterations': 5, 'state': <State.FAIL: 'FAIL'>, 'sparql': 'PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> PREFIX : <https://welektronik.iis.fraunhofer.de/entity/> SELECT ?company ?employees WHERE { ?company tbox:size :Q1049 . ?company tbox:employees ?employees . }', 'elapsed_time': 103376}, 'tokens': {'prompt_tokens': 17510, 'completion_tokens': 670, 'elapsed_time_model': 99480, 'tokens_per_sec': 182.75029496329242}, 'git': {'label': 'v0.2.8-91-g5e507554', 'commit': '5e507554e7591bf3e1500b8f32ab0205253aa1ca'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}