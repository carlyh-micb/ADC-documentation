# How to create an OCA Schema
This is a tutorial of how to create an Overlays Capture Architecture (OCA) data schema. This technology is currently under active development at ADC. 

By following this tutorial, you will create an Excel template document, upload it to the OCA parser, and generate the OCA schema bundle for download and use.
[Read a brief background in data schemas, and an introduction to the OCA schema](semantic_engine.md).

Overlays Capture Architecture is a machine-readable way to encode a schema and it is expressed in the JSON scripting language. 

Writing a schema in JSON is not very human-friendly, instead we will fill out the schema information in a template Excel spreadsheet. Then we will upload this Excel sheet into the semantic engine OCA schema parser, and it will generate the OCA schema bundle. In the future as we develop the Semantic Engine, we can create easier ways to generate these OCA schemas, but for now we are using an Excel template.

The advantage of OCA schemas is that they are modular. You can start with a very simple design, and because of the OCA layered architecture you can add more functionality to the schema later. The simplest OCA schema has a Capture Base (CB) which defines the basic structure of the data, and some additional overlays (OL) that help the user understand the data. OCA schemas are also shareable and machine-readable. You can publish your OCA schema with an identifier and others can reference and extend your work.

# Creating an OCA schema – Excel template

Download the Excel OCA schema template[link].

When you enter data into this template, do not change the basic structure as the parser needs this structure to create the OCA schema bundle. For example, you can see that data entry of sheet Main starts on row 3 so you should not delete the rows above.

The README tab is for your reference, and you can add some metadata here (like title and contact information) for the Excel sheet.

# Capture Base and Overlays

Capture Base (CB) is a stable base object that defines a single dataset in its purest form. It is good practice to keep the Capture Base stable and consistent. The Capture Base is given an identifier that is derived from its content, and all other overlays will reference this identifier. Furthermore, other users of your schema will confirm the Capture Base by its identifier. If you change even a character of the Capture Base, the identifier will change as well. You can [read more about identifiers and self-addressing identifiers here](identifiers_and_saids.md).

Overlays (OL) are additional pieces of the schema that aren’t part of the Capture Base. They reference the identifier of the Capture Base and specify additional information in the schema – such as language specific descriptions of different data columns. Because the Overlays are separate from the Capture Base, they can be added to a Capture Base later without disrupting the Capture Base description and identifier of the data structure.

# Entering schema information

The Main tab is where we enter information of the schema Capture Base (columns designated with CB). 
On the Main tab, under Attribute Names add your unique list of attribute names which can be the column label (or a simplified version of the column label). 
On the Main tab specify the Attribute Type, which should be one of the following:
* **Text**: a data type that defines a human-readable sequence of characters and the words they form.
* **Numeric**: a data type that defines anything relating to or containing numbers. 
* **Reference**: a data type that defines a Self-Addressing IDentifier (SAID) that references a set of attributes through its associated parent. 
* **Boolean**: a data type where the data only has two possible variables: true or false.
* **Binary**: a data type that defines a binary code signal, a series of electrical pulses representing numbers, characters, and performed operations. 
* **DateTime**: a data type that defines dates. Common formats include dates (e.g., YYYY-MM-DD), times (e.g., hh:mm:ss), dates and times concatenated (e.g., YYYY-MM-DDThh:mm:ss.sss+zz:zz), and durations (e.g., PnYnMnD).
 * **Array** [attribute type]: a data type that defines a structure that holds several data items or elements of the same data type. 

# Limiting data entry to a choice from a list (i.e. drop-down menu)

If you want to limit data input to only a select number of choices (like in a drop-down menu) you would use the array[text] or array[numeric] for the Attribute Type. In the Entry Code column, you can then put in the items in the list (separated by the pipe | symbol). 

For example, where you wish to limit gender entry to one of three choices the Attribute Type is array[text] and you may specify your genders as M|F|X in the Entry Codes. Later, in a language tab you can give more human-readable labels to this list such as “Male|Female|Other” for English or “Masculin|Féminin|Autre” for French.

# Sensitive or personal data flagging
The Flagged Attribute for sensitive data is also part of the Capture Base specified in the Main tab. Marking an entry with a “Y” will allow you to flag any attributes where identifying information about entities may be captured. With Flagged Attributes, all corresponding data can be treated as high-risk throughout the data lifecycle and encrypted or removed at any stage, reducing the risk of re-identification attacks against blinded datasets.

# Character encoding and format

The last two features of the Capture Base are Character Encoding and Format. The default value for Character Encoding is utf-8 (Unicode Transformation Format – 8 bits) which is the recommended choice.

The Format Overlay defines the input and display format of the data field. Examples include YYYY-MM-DD for date, image/jpeg, [A-Z0-9]{8} (8 character long alpha-numeric entry). If left blank the default is text.

# English language details

Final details that are required core overlays are found in the en tab for the English language (or in fr for French). Attribute Names are automatically copied from Main tab into the Attribute Name of the language tab. The first entry cell of the Meta[Form Name] column is where you put your schema name (e.g. “Biodiversity Schema”) and the same for the Meta[Form Description] cell (e.g. “A schema to capture biodiversity data”). These details will help make your schema more discoverable and can help people confirm that they have the right schema when they find yours.

# Adding language specific labels and more information

The final information to be added to the OCA schema is the language specific Label and Information. Labels are more reader friendly labels of attribute. If you are creating a questionnaire, the Label would be where you put the full text of your question.

Human readable list of labels – how?

Information is where you provide more details to help users of your schema understand exactly what is being collected for each attribute. It helps to add context to your data and helps people using your schema know what kind of information they should be inputting into each field.

# Convert from Excel to OCA

The XLS to OCA Converter is currently hosted at Human Colossus Foundation while under development. Uploading the Excel document into the parser to create the OCA Bundle. The OCA Bundle contains the Capture Base and its associated Overlays into an archival (.zip) format. You can view the JSON code that describes each Capture Base and Overlay in any text viewer. Each JSON file contains the SAID identifier for each layer and Capture Base. The SAID identifier for the entire OCA Bundle is in the filename of the bundle.

What to do with your OCA bundle

