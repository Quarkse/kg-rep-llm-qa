# kg-representations-llm-qa

This repository provides the knowledge graph, corpus, and experiments of a paper on knowledge graph representations for LLM-augmented question answering.

## Knowledge graph

The default variant of the knowledge graph conforms to the [SupplyBench](https://github.com/wintechis/supplybench) knowledge graph (version 0.2), but excludes the membership pattern from the [Organization Ontology](https://www.w3.org/TR/vocab-org/) used to model CEOs because memberships with corresponding time intervals and time instants would be represented by blank nodes.

The different files in the [a-box](./knowledgegraph/a-box/) and [t-box](./knowledgegraph/t-box/) directories correspond to the variants discussed in the paper. Each experiment uses one a-box and one t-box file, which are linked from the README files in the numbered [experiments](./experiments/) directories.

## Corpus

The corpus conforms to the [SupplyBench](https://github.com/wintechis/supplybench) query corpus (version 0.2), but excludes question-query-pairs that contain the membership pattern.

## Experiments

Each experiment consists of five runs with identical setup. The directories of each run contain the tracelogs for all evaluated corpus queries and the evaluation results.

## Specific class and object property boundaries

The file [class-boundaries.rq](./entity-boundaries/class-boundaries.rq) contains a SPARQL Contruct query describing the triples added to the specific entity boundaries of classes on top of outgoing triples.

The file [objectproperty-boundaries.rq](./entity-boundaries/objectproperty-boundaries.rq) contains a SPARQL Contruct query describing the triples added to the specific entity boundaries of object properties on top of outgoing triples.

## Graf von Data prompt

The file [gvd-prompt.txt](./agent/gvd-prompt.txt) contains the prompt used in all experiments.

## Graf von Data screenshot

The file [gvd-screenshot.PNG](./agent/gvd-screenshot.PNG) shows a screenshot of Graf von Data answering an example question.
