# 🧩 Questions Generator for Dataset

This project automatically generates **Question–Answer (Q&A) datasets** from a **geological ontology in OWL format** called miniKGraph based on PetroKgraph.  
The goal is to build structured corpora that can be used for **training and evaluating QA systems**, especially in the geosciences domain.

---

## 🚀 Key Features

- Extracts information from an RDF/OWL ontology using **RDFLib**.
- Used a **knowledge graph** called miniKGraph () based on PetroKgraph.
- Generates questions across different complexity levels:
  - `level=0`: simple synonym questions.
  - `level=1`: direct relation (1-hop) questions.
  - `level=2`: counting or listing questions (fields, basins, wells).
  - `level=3`: multi-hop reasoning questions.
  - `level=4`: conceptual definition questions.
- Supports **filtering questions by level** (e.g., only `level=0`, or `level=1 and 2`).
- Exports results as **JSON datasets**, ready to be used in NLP pipelines or RAG systems.

---

## 🌐 Knowledge Graph Structure

The system extracts entities (nodes) and their relationships from the ontology.  
The main **node types** are:

- **Basins** (`BASE_CD_BACIA`)  
  Geological basins where fields and wells are located.  
- **Fields** (`CAMP_CD_CAMPO`)  
  Oil & gas fields associated with basins and wells.  
- **Wells** (`POCO_CD_POCO`)  
  Wells located in fields/basins and crossing lithostratigraphic units.  
- **Lithostratigraphic units**  
  - **Formations** (`formacao_*`)  
  - **Groups** (`grupo_*`)  
  - **Members** (`membro_*`)  

Each node type has **labels (synonyms)** and may carry additional attributes (e.g., geological ages, structures).

The main **relationships** include:
- `located_in` → links wells/fields/formations to basins or higher-level units.  
- `crosses` → links wells to lithostratigraphic units.  
- `constituted_by` → links formations to lithologies.  
- `carrier_of` → links formations to geological structures.  
- `part_of` → hierarchical relation between formations, groups, and members.  

## 🛠 Requirements

- Python 3.9+
- Libraries:
  - `rdflib`
  - `networkx`

Install dependencies:  `pip install -r requirements.txt `
These relationships are used to automatically generate diverse types of questions.

## ▶️ Usage

Run the main script:

`python questions_generator.py`

This will generate datasets in JSON format, for example:

- `MiniKGraph_text_dataset_balanced.json`
- `MiniKGraph_text_dataset_unbalanced.json`

### 🔍 Filtering by Levels

You can generate datasets with specific levels:

Only level=0: synonym-based questions.
Only level=1 and 2: direct relation and listing questions.

Example outputs:

MiniKGraph_text_dataset_balanced_level0.json
MiniKGraph_text_dataset_unbalanced_lv1_2.json

## 📚 Citation

```bash
@inproceedings{navarro2024text,
  title={Text extraction from Knowledge Graphs in the Oil and Gas Industry},
  author={Navarro, Laura P and de Souza, Elvis A and Pacheco, Marco AC},
  booktitle={Simp{\'o}sio Brasileiro de Tecnologia da Informa{\c{c}}{\~a}o e da Linguagem Humana (STIL)},
  pages={524--529},
  year={2024},
  organization={SBC}
}
```

