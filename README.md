Introduction
------------------
jsonToRfd is a Python library that converts MEDFORD JSON data into RDF/XML format using the rdflib library. It provides a simple way to transform MEDFORD JSON-based metadata into RDF triples, making it easier to work with Linked Data and semantic web applications.

Installing
------------------
To use jsonToRfd, you need to have the following Python libraries installed:
    rdflib: The library to work with RDF data.
You can install this library using pip:
    pip install rdflib

How to Use
------------------
1. Import the jsonToRfd class from the library into your Python script or application.
2. Read your JSON data from a file or obtain it through any other means.
3. Create an instance of the jsonToRfd class, passing the MEDFORD JSON data as a parameter.
Call the json_to_graph() method of the instance to convert the JSON data into RDF triples.
And call the graph_to_rdfxml() method to serialize the RDF data into RDF/XML format.
4. Save the RDF/XML data to a file or use it as needed in your application.

Here is a basic example:

    from json_to_rdf import jsonToRfd

    # Read JSON data from a file or any other source
    with open('data.json', 'r') as json_file:
        json_data = json.load(json_file)

    # Convert JSON data to RDF/XML
    converter = jsonToRfd(json_data)
    converter.json_to_graph()
    rdf_xml_data_bytes = converter.graph_to_rdfxml()

    # Save the RDF/XML data to a file
    with open('output.rdf', 'wb') as rdf_file:
        rdf_file.write(rdf_xml_data_bytes)

Design Principles
------------------
The jsonToRfd library follows the following design principles:
1. Validity: Ensure that the RDF/XML adheres to the RDF specifications and is a valid XML document. Use proper namespace declarations and well-formed XML syntax.
2. Use namespaces: Utilize namespaces to uniquely identify resources and properties. This helps avoid conflicts and ensures clarity in the RDF data.
3. Clear subject-predicate-object structure: Represent triples (subject-predicate-object) clearly in the RDF/XML. Use appropriate XML elements and attributes to express this structure.
4. Reusability: Reuse existing vocabularies (e.g., Dublin Core, BIBO, VCARD) when appropriate instead of reinventing terms. This enhances interoperability and consistency.
5. Avoid deep nesting: Keep the RDF/XML structure simple and avoid excessive nesting of elements. 
6. Avoid using the about or id attributes in RDF descriptions as they are not part of the official RDF specification. In the global scope, using these attributes can lead to issues as we lack the actual global URL for the about. Conversely, within the local scope, our MEDFORD operates on different bases. Using a local id can hinder interoperability with other RDF datasets and make it confusing for users. It is preferable to adhere to the standard RDF triple structure, which ensures consistency and clarity in RDF data modeling.

Theory of Operation
------------------
The jsonToRfd library works by traversing the MEDFORD JSON data recursively and mapping JSON properties to appropriate RDF terms using predefined namespaces. It identifies major tokens, such as "code," "data," "journal," etc., and creates RDF triples accordingly. It also handles minor tokens, such as "ref," "primary," and "copy," to provide additional information about the triples.

The library follows a two-step process:

Conversion: The MEDFORD JSON data is traversed, and RDF triples are generated based on the mapping of JSON properties to RDF terms.

Serialization: The generated RDF triples are serialized into RDF/XML format using the rdflib library.

RDF/XML Validation
------------------ 
You can utilize the online RDF/XML validator available at https://www.w3.org/RDF/Validator/. This tool allows you to check the correctness and conformance of your RDF/XML data with the RDF specifications provided by the World Wide Web Consortium (W3C)."

References
------------------
rdflib library documentation: https://rdflib.readthedocs.io/en/stable/

RDF/XML specification: https://www.w3.org/TR/rdf-syntax-grammar/

DublinCore RDF/XML examples: https://www.dublincore.org/specifications/dublin-core/dcmes-xml/

Qualified DC: https://www.dublincore.org/specifications/dublin-core/dcq-rdf-xml/

Feel free to contribute to the project by submitting issues or pull requests on the repository page. If you have any questions or need further assistance, please don't hesitate to reach out. Happy converting!
