# JSON Knowledge Graph (JKG)
**JSON Knowledge Graph (JKG)** is a specification for a format with which to import into or export information from
a knowledge graph--specifically, a property graph.

# Features of JKG

## Platform-independence
JKG specifies the entities (nodes), edges (rels), and properties of a knowledge graph. 
JKG makes no assumptions about the platform of the graph database that hosts the knowledge graph.

Various repositories such as [jkg-neo4j](https://github.com/x-atlas-consortia/jkg-neo4j/tree/main) support application architectures that support an implementation of JKG 
on a neo4j platform; however, it should be possible to use the actual JKG specification on
other platforms.

## Validation
It is possible to validate a JSON file against the JKG schema. If a JKG JSON
files passes validation tests, it should be possible to import data from the JKG JSON into a graph database 
without issues such as referential integrity.

The jkg-neo repository includes an [application](https://github.com/x-atlas-consortia/jkg-neo4j/blob/main/scripts/README.md#validate_jkg_json) (**validate_jkg_json**) that validates a JKG JSON file against
the JKG Schema. 

# JKG Schema and model

A JKG JSON that comforms to the JKG Schema consists of two 
arrays:
* a **nodes** array of node objects
* a **rels** array of relationship (rel) objects

Both node and rel objects have a required properties. Objects
must also satisfy structural criteria for the overall JSON, 
including a form of referential integrity.

## node objects

There are four types of node objects. The **label**/**labels** property
identifies the node object type.

### Source
Source nodes describe a source of encoded data used to populate a JKG JSON.
Types of sources include:
* ontologies (e.g., OWL files)
* vocabularies, such as those maintained in the National Library of Medicine's [UMLS](https://www.nlm.nih.gov/research/umls/index.html?_gl=1*51hudq*_ga*MTA3MjQ2MTgwMy4xNzc1MTM3NDEx*_ga_7147EPK006*czE3NzcwNDA0NzgkbzkkZzEkdDE3NzcwNDA0OTQkajQ0JGwwJGgw*_ga_P1FPTH9PL4*czE3NzcwNDA0NzgkbzgxJGcxJHQxNzc3MDQwNDk0JGo0NCRsMCRoMA..) Metathesaurus
* online repositories, such as [UniProtKB](https://www.uniprot.org/)

Required properties of the node object are:

#### **id**
An identifier for the source in format 
_owner_:_SAB_, 
where _SAB_ is an acronym called the _**S**ource **AB**breviation_.

When the source is a vocabulary from the UMLS, _owner_ is UMLS;
otherwise, the _owner_ is usually just the SAB for the source.

#### **properties**
An object (dict) containing key/value pairs:


```
 {
    "labels":["Source"],
    "properties":{
        "id":"UBERON:UBERON",
        "name":"Uberon",
        "description":"Uberon multi species anatomy ontology",
        "sab":"UBERON",
        "source_version":"2025-JAN-15",
        "source":"http://purl.obolibrary.org/obo/uberon/uberon-base.owl"
        }
  }
```