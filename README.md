# CareerAI

## Integrated Recommender System + Reinforcement Learning for Career Planning

CareerAI is an academic career-guidance prototype that combines a
content-based recommendation system with a Q-learning career planner. It
analyses resume text, recommends suitable occupation profiles,
identifies skill gaps, and suggests a sequence of connected roles toward
a selected target role.

> **Scope:** The prototype uses a curated occupation dataset and
> predefined role-transition links. It does not search live vacancies or
> predict a candidate's probability of being hired.

## Project workflow

1.  **Resume input:** Upload a PDF/TXT resume or paste resume text.
2.  **Skill extraction:** Extract skills using a predefined, editable
    vocabulary.
3.  **Role recommendations:** Compare resume text with occupation
    profiles and rank roles.
4.  **Skill-gap analysis:** Display matched and missing skills for
    recommended roles.
5.  **Career planning:** Select a target role and generate a transition
    path using Q-learning.
6.  **Evaluation:** Measure recommendation quality and compare the RL
    planner with a BFS shortest-path baseline.

## Key features

-   Resume upload and text input.
-   Rule-based, user-editable skill extraction.
-   TF-IDF (unigrams and bigrams) with cosine similarity.
-   Hybrid role scoring using text similarity and skill coverage.
-   Matched-skill and missing-skill explanations.
-   Q-learning-based career transition planning.
-   BFS shortest-path baseline.
-   Precision@K, Recall@K, and NDCG@K evaluation.
-   Adjustable recommendation and RL parameters.

## Recommendation system

Each occupation profile contains a role title, description, and required
skills. The system vectorises occupation text using TF-IDF and
calculates cosine similarity against the resume text.

Skill coverage is calculated as:

`Skill Coverage = Matched Required Skills / Total Required Skills`

The hybrid score is:

`Hybrid Score = 0.55 × TF-IDF Similarity + 0.45 × Skill Coverage`

The prototype can also apply small boosts for preferred-level and
keyword matches. These are heuristic relevance scores, **not hiring
probabilities**.

## Reinforcement learning planner

The career planner models role transitions as a Q-learning problem:

-   **State:** Current occupation/role.
-   **Action:** Move to a connected role through a predefined transition
    link.
-   **Reward:** `-1` step cost, `+2` for target-skill overlap, `+0.25`
    for newly relevant skills, and `+12` for reaching the goal.
-   **Default parameters:** Learning rate α = `0.12`, discount factor γ
    = `0.92`, exploration rate ε = `0.25`.

After training, the planner uses learned Q-values to produce a greedy
transition path. Revisited roles are blocked during path construction.

## Evaluation

The recommender is evaluated on 10 benchmark profiles using
illustrative, rule-derived relevant-role sets. Metrics include:

-   Precision@K
-   Recall@K
-   NDCG@K

TF-IDF, skill-coverage, and hybrid approaches are compared, including a
weight-sweep experiment. The RL career planner is compared with a
Breadth-First Search (BFS) shortest-path baseline across reachable role
pairs.

## Technologies and concepts

-   HTML, CSS, JavaScript
-   TF-IDF and cosine similarity
-   Content-based and hybrid recommendation
-   Rule-based skill extraction
-   Reinforcement Learning and Q-learning
-   Breadth-First Search (BFS)
-   Precision@K, Recall@K, NDCG@K

## How to run

The prototype is designed to run locally in a modern web browser.

1.  Clone or download this repository.
2.  Locate the main HTML file.
3.  Open the HTML file in a modern browser.
4.  Upload a PDF/TXT resume or paste resume text.
5.  Review and edit the extracted skills.
6.  Explore recommended roles and their skill gaps.
7.  Select a target role to generate a career transition pathway.

No backend server is required for the browser-based prototype, provided
all supporting files remain in their expected relative paths.

## Suggested repository structure

Adjust the filenames to match the files actually uploaded to this
repository.

``` text
Career-AI/
├── README.md
├── index.html
├── assets/
├── data/
└── docs/
```

## Limitations

-   The curated occupation dataset contains 20 distinct roles; it is not
    a live vacancy feed.
-   Role transitions rely on predefined links.
-   Benchmark relevance labels are illustrative and rule-derived, not
    independently annotated ground truth.
-   Rule-based skill extraction may miss synonyms, context, and
    proficiency levels.
-   Reward and transition assumptions have not been validated against
    real career outcomes.
-   The RL state represents the role and does not explicitly model
    skill-learning actions.
-   PDF processing extracts text; scanned documents requiring OCR may
    not be handled.

## Future improvements

-   Integrate licensed occupation and skills taxonomies such as O\*NET
    or ESCO.
-   Evaluate on manually labelled, held-out profiles.
-   Compare TF-IDF with sentence-embedding representations.
-   Extend the RL state and action space to include skill mastery,
    learning activities, and time constraints.
-   Run multiple random seeds and report mean and standard deviation.

## Team

-   **Riddhiraj Kaushik** --- R015
-   **Aditva Kulshreshtha** --- R018
-   **Devhuti Prabhakar** --- R028

## Disclaimer

CareerAI is an academic prototype for educational and demonstration
purposes. Its recommendations are indicative and should not be treated
as professional career, recruitment, or employment advice.
