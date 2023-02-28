# Sample Web Application

The examples above show the actual HTTP URLs used by this proposed service. Of course, chemists aren't generally going to be typing in URLs into their web browser, but would instead be using this as part of some other application. PubChem has a (very simplistic) example of this as a web page service that uses a simple form input to the validation CGI:

[https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=input\_form](https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=input_form)

This sample web interface lets the user select an input type, and choose whether to get validation details (as JSON) or an image. It also demonstrates the possibility of accepting MOL/SDF as input, which is a multi-line format not amenable to simple URL syntax as in the examples above.

Two different implementations are provided to illustrate distinctions in validation rules: one using PubChem's existing but internal standardization software, and another using [RDKit](https://www.rdkit.org/) – an open-source chemical information toolkit. 
