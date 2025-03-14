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

Operating income of companies in 2021

***

Think: The user is asking for the operating income of companies in 2021. To formulate a query, we need to identify the key resources involved, such as companies and operating income. We also need to consider the time frame, which is 2021.

Act: search('company') | search('operating income') | search('2021')

***

The keyword search for `company` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1104.ttl#this **Active Business Company** 0.5333
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ109204.ttl#this **Comal County** 0.4167
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#this **Taiwan Semiconductor Manufacturing Company** 0.4020
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ486078.ttl#this **Canyon County** 0.3443
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ108418.ttl#this **Cook County** 0.3443

***

The keyword search for `operating income` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#operatingIncome **operating income** 1.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ237683.ttl#this **Ome** 0.4216
    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#incomingSupplyFlow **incoming supply flow** 0.3015
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ695.ttl#this **OpenFive** 0.2981
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ274.ttl#this **Ampere Computing** 0.2778

***

The keyword search for `2021` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/person/wdQ7143480.ttl#conf-hotchips-Gelsinger22 **Semiconductors Run the World : Hot Chips 2022.** 0.1667
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ23048142.ttl#this **Carmelray Industrial Park 1** 0.1072
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ110.ttl#this **Rogue Valley Microdevices** 0.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ131277.ttl#this **Gifu Prefecture** 0.0000
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ204308.ttl#this **Miyazaki** 0.0000

***

Think: We have identified some key resources, including companies, operating income, and the year 2021. However, the search results for "2021" do not seem to be directly related to the year. We need to refine our search to get more accurate results.

Act: deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#operatingIncome') | search('financial year') | search('annual report')

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#operatingIncome` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    tbox:operatingIncome a qb:MeasureProperty,
            owl:DatatypeProperty ;
        rdfs:label "operating income"@en ;
        rdfs:domain qb:Observation ;
        rdfs:range xsd:decimal .

***

The keyword search for `financial year` returned the following ranked list with hits.

    https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#accountingYear **accounting year** 0.3032
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1145.ttl#this **Fineeco** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ33.ttl#this **Finland** 0.2500
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ693.ttl#this **MaxLinear** 0.2261
    https://dblp.org/rdf/schema#yearOfPublication **year of publication** 0.2182

***

The keyword search for `annual report` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ101254.ttl#this **Newport** 0.3849
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5283458.ttl#this **Newport** 0.3849
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1160.ttl#this **Wafer Export** 0.3086
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ564234.ttl#this **Annaka** 0.3062
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ45.ttl#this **Portugal** 0.2739

***

Think: We have found some relevant information about operating income, financial year, and annual reports. However, we still need to find a way to link this information to the year 2021. We can try to search for companies that have published annual reports for 2021.

Act: search('annual report 2021') | deref('https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#accountingYear')

***

The keyword search for `annual report 2021` returned the following ranked list with hits.

    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ564234.ttl#this **Annaka** 0.2835
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ101254.ttl#this **Newport** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ5283458.ttl#this **Newport** 0.2673
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ45.ttl#this **Portugal** 0.2535
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/region/wdQ485583.ttl#this **Anan** 0.2182

***

The description of `https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#accountingYear` is as follows.

    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix qb: <http://purl.org/linked-data/cube#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    
    tbox:accountingYear a qb:DimensionProperty,
            owl:DatatypeProperty ;
        rdfs:label "accounting year"@en ;
        rdfs:domain qb:Observation ;
        rdfs:range xsd:integer .

***

Think: We have found some information about annual reports and accounting years, but we still need to find a way to link this information to the operating income of companies in 2021. We can try to construct a query that uses the accounting year and operating income properties to find the operating income of companies in 2021.

Act: query('PREFIX qb: <http://purl.org/linked-data/cube#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT ?company ?operatingIncome WHERE { ?company a qb:Observation . ?company tbox:accountingYear 2021 . ?company tbox:operatingIncome ?operatingIncome . }')

***

The query 'PREFIX qb: <http://purl.org/linked-data/cube#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT ?company ?operatingIncome WHERE { ?company a qb:Observation . ?company tbox:accountingYear 2021 . ?company tbox:operatingIncome ?operatingIncome . }' returned the following solution (first 20 results).
    company,operatingIncome
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1030.ttl#operatingincome2021,5381822000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ1036.ttl#operatingincome2021,98980000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ17.ttl#operatingincome2021,3648000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ20.ttl#operatingincome2021,649980897000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ21.ttl#operatingincome2021,10041000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ22.ttl#operatingincome2021,19456000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ23.ttl#operatingincome2021,9789000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ245.ttl#operatingincome2021,89678000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ25.ttl#operatingincome2021,8960000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ26.ttl#operatingincome2021,6283000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ27.ttl#operatingincome2021,1692201000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ28.ttl#operatingincome2021,2583000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ31.ttl#operatingincome2021,2419000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ32.ttl#operatingincome2021,1612700000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ35.ttl#operatingincome2021,108949000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ36.ttl#operatingincome2021,53351827000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ37.ttl#operatingincome2021,-59812000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ58.ttl#operatingincome2021,4837000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ668.ttl#operatingincome2021,1347000000.0
    https://solid.iis.fraunhofer.de/oe-40200/2024/10/velektronik-graph-clean/company/weQ675.ttl#operatingincome2021,6889000000.0

***

Think: We have successfully constructed a query that retrieves the operating income of companies in 2021. The query uses the accounting year and operating income properties to find the operating income of companies in 2021.

Act: success('The operating income of companies in 2021 can be retrieved using the constructed query.')

{'loop': {'id': '67d03702', 'question': 'Operating income of companies in 2021', 'iterations': 5, 'state': <State.SUCCESS: 'SUCCESS'>, 'sparql': 'PREFIX qb: <http://purl.org/linked-data/cube#> PREFIX tbox: <https://github.com/wintechis/natural-language-query-answering/tree/main/knowledge-graph/velektronik-graph-clean/tbox.ttl#> SELECT ?company ?operatingIncome WHERE { ?company a qb:Observation . ?company tbox:accountingYear 2021 . ?company tbox:operatingIncome ?operatingIncome . }', 'elapsed_time': 87077}, 'tokens': {'prompt_tokens': 12748, 'completion_tokens': 524, 'elapsed_time_model': 59242, 'tokens_per_sec': 224.02961639608495}, 'git': {'label': 'v0.2.8-90-ga084b38e', 'commit': 'a084b38e1d7b67039f0d60b14814ef1241c00fd7'}, 'sources': ['..\\knowledge-graph\\velektronik-graph-clean\\abox-en.ttl.gz', '..\\knowledge-graph\\velektronik-graph-clean\\tbox.ttl'], 'client_info': {'model': 'llama-3.3-70b-instruct', 'max_tokens': 1024, 'temperature': 0, 'top_p': 1, 'baseuri': 'https://chat-ai.academiccloud.de/v1/'}, 'platform': {'node': 'r10389', 'platform': 'Windows-10-10.0.19045-SP0', 'system': 'Windows', 'processor': 'Intel64 Family 6 Model 142 Stepping 12, GenuineIntel', 'machine': 'AMD64', 'physical_memory': 15.342079162597656, 'python_version': '3.12.7'}}