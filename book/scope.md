# Scope & Objectives 

The project aims to describe criteria for web-based services that participating organizations can implement based on their existing/preferred technologies (toolkits, programming languages). The services are intended to confirm chemical identity and provide real-time feedback on the machine-readability of chemical data and metadata representation based on IUPAC standard rule sets and community best practices. 

The goal is to support the following stakeholders and functions:

- **Chemical database owners:** These are organizations that would implement and provide these web services to the public.
- **Chemistry application developers:** These are people writing applications that would directly use the web services described here.
- **Chemists:** The end users, who would be accessing these web services indirectly, through a chemical drawing program or ELN notebook or such.
- **Chemical toolkit developers:** These are people writing chemical toolkits that could be used to implement the web services described here.

Two related objectives are proposed to address the following questions, described in more detail below:

- Does this organization know anything about this particular chemical?
- How does this organization interpret my chemical structure, does it match my expectations?


## Global Resolver

Many public databases have programmatic interfaces that let one query for a particular chemical, through some sort of web service. But these are all unique to individual organizations; PubChem's works very differently from EPA's, etc. So an application developer that wants to gather information from multiple resources would have to write separate, specialized code for each database. This is a heavy burden. 

If, instead, there were a common web service interface used by multiple database providers, then the developer could easily add the ability to query all these databases using a single code layer. One could even imagine writing a "global search" web site where a user could enter a single query, such as an InChI key or SMILES string, and have that go out to PubChem, EPA, ChEMBL, etc., to see if they have a corresponding record in their databases.

Such a system would require a standard interface, presumably to a CGI using the normal HTTP protocol (because just about any programming language has a way to send HTTP calls over the internet). And that, in turn, requires participating organizations to agree on the interface, and to implement a service that adheres to it. But the advantage to standardizing on the interface alone means that the web service itself could be implemented in any technology the organization chooses - C++, Java, etc. 

## Chemical Structure Validator

Machine readability of a chemical structure is a significant issue in cheminformatics. There are standard formats, of course, but different major chemical database organizations may interpret and process a record somewhat (or very) differently. This aspect of the project is not about creating a full standard for chemical structure interpretation, but rather providing a common way for individual organizations to provide feedback on what they make of the user's structure.

End user chemists, such as a laboratory researcher using an ELN system, may not be expert in the cheminformatics - how the computer interprets their structure. So it would be great if there were a way for the user (through their ELN application) to ask questions such as: What does this organization think of the structure as I've drawn it here? Does it have proper valences (e.g. no pentavalent carbons)? Does it have the right number of defined stereocenters? Where are there implicit hydrogens being perceived? Does their automatically generated image of this chemical match what I've drawn?

Having a common web service API to send the user's structure, and get feedback like this, would allow application developers, and by extension their users, to easily check their structures against multiple ogranizations, each of which may - and probably will - have their own rules for chemical processing, to see whether the chemicals are processed as the user expects, or whether there are ambiguities. In other words, "Is their computer handling my chemical structure the same way I (the expert chemist) have it in my head?" This is fundamental to machine readability.
