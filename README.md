# NL2GraphQL Bench

Start here. This repository is an index: it holds no code or data, only links.

**NL2GraphQL** is the task of turning a natural-language request into a GraphQL
query against a given schema. Because every API exposes a different schema, a
model that does well on one organisation's API says little about the next, so
the benchmark measures **cross-schema generalisation**: every evaluation
instance targets a schema that was never seen in training.

The corpus and framework come from the AutoGraphQL paper (EMNLP 2026 Industry
Track).

## Leaderboard

**https://nl2graphql-bench.github.io/**

Ranked by overall accuracy, with a per-category breakdown across the seven
GraphQL query categories. Scoring is semantic equivalence on normalised ASTs,
not exact string match.

## Datasets

**https://github.com/nl2graphql-bench/datasets** — MIT License

| split | rows | schemas | published |
|---|---|---|---|
| train | 9,118 | 104 | yes |
| public test | 6,403 | 49 | yes |
| hidden test | 2,100 | 20 | **no, withheld** |

Train and test schemas are disjoint. The hidden split is not released: it is
what submissions are verified against, so publishing it would make that
verification meaningless.

Each row is a validated triple of (GraphQL schema, natural-language query,
ground-truth GraphQL query). Every published row's query validates against its
own schema. Use the `CleanSchema` field for validation — see that repository's
README for the fields and for why the other schema columns are unsuitable.

## Code

| component | repository |
|---|---|
| generation | https://github.com/nl2graphql-bench/generation |
| evaluation | not yet published |
| validation | not yet published |

**generation** is the AutoGraphQL Bring-Your-Own-Schema framework: schema
feasibility analysis, schema-aware query synthesis, schema and execution
validation with deduplication, then natural-language generation. It produced the
datasets above.

The evaluation and validation components are being prepared for release. This
table is updated as they land.

## Submitting a result

The submission process is described on the leaderboard site under **Submit**.
In outline: score your model on the 6,403-instance public benchmark, open a
submission issue with your predictions and a model card, and the hidden split
is then scored independently before a headline number is posted.

Do not include production schemas, credentials or internal API packages in a
submission. Score against the public benchmark only.

## Paper

**AutoGraphQL: A Bring-Your-Own-Schema Framework for Adapting Open-Weight LLMs
to GraphQL APIs**
Keya Battu (IIT Kharagpur), Parth Mehta (DPS Bengaluru), Harikrishnan Balagopal
(IBM Bengaluru), Manish Kesarwani (IBM Bengaluru)
EMNLP 2026, Industry Track.
OpenReview: https://openreview.net/forum?id=NcuPXBFKAO

### Prior work this builds on

| year | venue | paper |
|---|---|---|
| 2024 | IJCAI, Demo | LLM-powered GraphQL Generator for Data Retrieval — https://www.ijcai.org/proceedings/2024/1002 |
| 2024 | EMNLP, Industry | GraphQL Query Generation: A Large Training and Benchmarking Dataset — https://aclanthology.org/2024.emnlp-industry.117/ |
| 2025 | NAACL, Industry | Schema and Natural Language Aware In-Context Learning for Improved GraphQL Query Generation — https://aclanthology.org/2025.naacl-industry.76/ |
| 2025 | IEEE ICWS | Robust Evaluation of LLM-Generated GraphQL Queries for Web Services — https://ieeexplore.ieee.org/abstract/document/11169687 |
| 2026 | SIGMOD, Workshop | Synthetic Data Generation for Schema-Aware Query Interfaces: Benchmarking NL2GraphQL Systems — https://doi.org/10.1145/3814574.3816745 |

Accuracies are not comparable across these papers: the evaluation metric
changed over the series, from execution-output comparison to the
semantic-equivalence AST scoring used here.

## License

Datasets are MIT. Code licensing is per repository.
