# kg-representations-llm-qa

This repository provides the knowledge graph, corpus, and experiments of a paper on knowledge graph representations for LLM-augmented question answering.

## Knowledge Graph

The default variant of the knowledge graph conforms to the [SupplyBench](https://github.com/wintechis/supplybench) knowledge graph (version 0.2), but excludes the membership pattern from the [Organization Ontology](https://www.w3.org/TR/vocab-org/) used to model CEOs because memberships with corresponding time intervals and time instants would be represented by blank nodes.

The different files correspond to the variants discussed in the paper. Each experiment uses one a-box and one t-box file. The files for each experiement are included in the numbered `experiments` directories (duplicates of the files in the `knowledgegraph` directory).

## Corpus

The corpus conforms to the [SupplyBench](https://github.com/wintechis/supplybench) query corpus (version 0.2), but excludes question-query-pairs that contain the membership pattern.
