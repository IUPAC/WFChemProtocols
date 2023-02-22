# WorldFAIR Chemistry: Protocol Services

## Description

This project corresponds to Deliverable 3.3 of the WorldFAIR Chemistry project. The main scope of work will be to define a common protocol for resolving different chemical representations. The specification will articulate a shared data model for chemical information exchange through an API that can be implemented by any system that manages chemical records. Users will be able to query registered resources with different scopes and capabilities at a general level to determine where they can find additional data and information. The model will cover a range of chemical representations, including structural diagrams, nomenclature and other linear notations. The protocol will also provide a standard set of error codes for flagging ambiguous or conflicting representations.


## Objective

Representing chemical substances in structure form is one of the most critical functions in communicating chemistry, including sharing FAIR and machine-readable chemical data, as many resources are indexed by chemical structures. There are a range of approaches for articulating chemical substance information, depending on the scientific nature and context, and the digital motifs used in chemical databases and chemicals software, present additional layers of complexity. Chemical interpretation can vary between data systems and directly impact downstream reuse, especially when it comes to representation and analysis of associated data. Validation of chemical description is an essential requirement for the re-usability of chemical data, including discovery and in many modeling and predictive AI/ML applications.

This project aims to develop the specification for a web-based service that confirms chemical identity and provides real-time feedback on the machine-readability of chemical data and metadata representation, based on IUPAC standard rule sets and recommended best practices. The goal is thus to describe the **interface** of services that provide the functionality described. While a prototype **implementation** may be (and largely has been) developed, it is illustrative only and not a final product; participating organizations would be free to implement the service with whatever technology (toolkits, programming languages) is convenient to them.


## Target Audience

The people that this project will impact or influence are, broadly speaking:

- **Chemical database owners:** These are organizations that would implement and provide these web services to the public.
- **Chemistry application developers:** These are people writing applications that would directly use the web services described here.
- **Chemists:** The end users, who would be accessing these web services indirectly, through a chemical drawing program or ELN notebook or such.
- **Chemical toolkit developers:** These are people writing chemical toolkits that could be used to implement the web services described here.


## The Two Main Components Of This Project




### Global Resolver


### Chemical Structure Validator


## What's In This Repository

Currently this repository contains informational documents only, on what the project is about and what it's trying to accomplish. In the future, there may be more interactive example/demo pages, code snippets (e.g. a base implmentation of the structure validator in C++/RDKit), etc.
