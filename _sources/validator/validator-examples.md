# Validator Prototype and Examples

PubChem has, for demonstration purposes, created a prototype of this chemical structure validation service. In its simplest use, it takes chemical structure input (e.g. SMILES) and produces a JSON message:

[https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=validate\_structure&smiles=CCCC](https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=validate_structure&smiles=CCCC)

```
{

"Result": {

"Message": "Structure is valid",

"Statistics": [

{

"Type": "DefinedAtomStereo",

"Value": "0"

},

{

"Type": "UndefinedAtomStereo",

"Value": "0"

},

{

"Type": "DefinedBondStereo",

"Value": "0"

},

{

"Type": "UndefinedBondStereo",

"Value": "0"

},

{

"Type": "HeavyAtoms",

"Value": "4"

},

{

"Type": "IsotopeAtoms",

"Value": "0"

},

{

"Type": "CovalentUnits",

"Value": "1"

}

]

}

}
```

The service provides some basic chemical informatics properties, such as number of atoms, stereocenters, and so on. Again, the goal is to make sure that this machine-interpreted result matches the chemist's expectations.

(Technical note: the data model used for this response is available as an XML schema here: [https://pubchem.ncbi.nlm.nih.gov/resolver/resolver\_data.xsd](https://pubchem.ncbi.nlm.nih.gov/resolver/resolver_data.xsd) ; PubChem has tools that simplify XML and JSON input/output based on XML Schema, so it was more convenient to implement this prototype from XML Schema. If JSON is the default format of this service, it would probably be better ultimately to use JSON Schema if/when that, or something like it, becomes a more widely recognized standard. But it is important to have a fully defined data model so that any application that uses this service knows what to expect, and how to parse the results.)

Here is a slightly more complicated structure, with both atom (sp3) and bond (sp2) stereochemistry:

"https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=validate\_structure&smiles=C/C=C/[C@H]1[C@H]\(O1\)C"

```
{

"Result": {

"Message": "Structure is valid",

"Statistics": [

{

"Type": "DefinedAtomStereo",

"Value": "2"

},

{

"Type": "UndefinedAtomStereo",

"Value": "0"

},

{

"Type": "DefinedBondStereo",

"Value": "1"

},

{

"Type": "UndefinedBondStereo",

"Value": "0"

},

{

"Type": "HeavyAtoms",

"Value": "7"

},

{

"Type": "IsotopeAtoms",

"Value": "0"

},

{

"Type": "CovalentUnits",

"Value": "1"

}

]

}

}
```

The chemist can easily see that the stereocenters have been perceived and fully defined.

If there is an error in the structure, there should be some feedback as to what the problem is, for example a pentavalent carbon:

[https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=validate\_structure&smiles=CC(C)(C)(C)C](https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=validate_structure&smiles=CC(C)(C)(C)C)

```
{

"Fault": {

"Code": "Invalid",

"Message": "Structure is not valid",

"Details": [

"Record 0: Warning: \"pcData/pubchem\_valence.cpp\", line 290: Detected illegal valence for element \"C\": 5 sigma bonds, 0 pi bonds, 0 charge",

"Exception: Valence validation failed"

]

}

}
```

Here is another example, with an invalid isotope:

[https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=validate\_structure&smiles=C[5H]](https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=validate_structure&smiles=C%5B5H%5D)

```
{

"Fault": {

"Code": "Invalid",

"Message": "Structure is not valid",

"Details": [

"Record 0: Info: \"OpenEye/pubchem\_compound.cpp\", line 3121: Atom ID \"2\" has illegal isotope (5) for atomic number 1 (\"H\")",

"Exception: Element validation failed"

]

}

}
```

While 5H exists, it is PubChem's policy is to reject anything with isotopes with \<1ms lifetime. Other institutions may have different policies. It is not the intention here to define the precise validation rules, but rather to provide a way for each organization to give feedback on the structure according to their own existing internal rules, but in a standard format.

Chemists are used to looking at chemical structure drawings, and so may prefer to see an image rather than the data fields shown above. For example:

`"https://pubchem.ncbi.nlm.nih.gov/resolver/resolver.cgi?action=validate\_structure&format=png&smiles=C[C@H](CCCC(C)C)[C@H]1CC[C@@H]2[C@@]1(CC[C@H]3[C@H]2CC=C4[C@@]3(CC[C@@H](C4)O)C)C "`

![](validator-figure-1.png)
