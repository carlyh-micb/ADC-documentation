# How to create an OCA Schema
This is a tutorial of how to create an Overlays Capture Architecture (OCA) data schema. This technology is currently under active development at [Agri-food Data Canada](https://agrifooddatacanada.ca/). 

By following this tutorial, you will create an Excel template document, upload it to the OCA parser, and generate the OCA schema bundle for download and use.
[Read a brief background in data schemas, and an introduction to the OCA schema](semantic_engine.md).

Overlays Capture Architecture is a machine-readable way to encode a schema and it is expressed in the JSON scripting language. 

Writing a schema in JSON is not very human-friendly, instead we will fill out the schema information in a template Excel spreadsheet. Then we will upload this Excel sheet into the semantic engine OCA schema parser, and it will generate the OCA schema bundle. In the future as we develop the Semantic Engine, we can create easier ways to generate these OCA schemas, but in phase 1 of development we use the Excel template.

The advantage of OCA schemas is that they are modular. You can start with a very simple design, and because of the OCA layered architecture you can add more functionality to the schema later. The simplest OCA schema has a Capture Base (CB) which defines the basic structure of the data, and some additional overlays (OL) that help the user understand the data. OCA schemas are also shareable and machine-readable. You can publish your OCA schema with an identifier and others can reference and extend your work.

# Creating an OCA schema – Excel template

Download the Excel OCA schema template[link].

When you enter data into this template, do not change the basic structure as the parser needs this structure to create the OCA schema bundle. For example, you can see that data entry of sheet Main starts on row 3 so you should not delete the rows above.

The README tab is for your reference, and you can add some metadata here (like title and contact information) for the Excel sheet.

# Capture Base and Overlays

**Capture Base (CB)** is a stable base object that defines a single dataset in its purest form. It is good practice to keep the Capture Base stable and consistent. The Capture Base is given an identifier that is derived from its content, and all other overlays will reference this identifier. Furthermore, other users of your schema will confirm the Capture Base by its identifier. If you change even a character of the Capture Base, the identifier will change as well. You can [read more about identifiers and self-addressing identifiers here](identifiers_and_saids.md).

**Overlays (OL)** are additional pieces of the schema that aren’t part of the Capture Base. They reference the identifier of the Capture Base and specify additional information in the schema – such as language specific descriptions of different data columns. Because the Overlays are separate from the Capture Base, they can be added to a Capture Base later without disrupting the Capture Base description and identifier of the data structure.

# Entering schema information

## Required fields
All Capture Base (CB) fields are required as well as two Overlays (OL): Character Encoding and Format.

## Classification
On the Main tab, under Classification you can add classifications for each attribute. This overlay is not standardized but it is recommended to be in the format system:type. For example, to add classifications for sustainable development goals for each attribute you can use "SDG:15"

## Attribute Names
On the Main tab, under Attribute Names add your unique list of attribute names which can be the column label (or a simplified version of the column label). Because this field may be used by many different computer systems we recommend to not include spaces and use underscores or CamelCase instead.

## Attribute Types
On the Main tab specify the Attribute Type, which should be one of the following:
* **Text**: a data type that defines a human-readable sequence of characters and the words they form.
* **Numeric**: a data type that defines anything relating to or containing numbers. 
* **Reference**: a data type that defines a Self-Addressing IDentifier (SAID) that references a set of attributes through its associated parent. 
* **Boolean**: a data type where the data only has two possible variables: true or false.
* **Binary**: a data type that defines a binary code signal, a series of electrical pulses representing numbers, characters, and performed operations. 
* **DateTime**: a data type that defines dates. Common formats include dates (e.g., YYYY-MM-DD), times (e.g., hh:mm:ss), dates and times concatenated (e.g., YYYY-MM-DDThh:mm:ss.sss+zz:zz), and durations (e.g., PnYnMnD).
 * **Array** [attribute type]: a data type that defines a structure that holds several data items or elements of the same data type. 

## Sensitive or personal data flagging
On the Main tab specify Flagged Attribute for sensitive data. Marking an entry with a “Y” will allow you to flag any attributes where identifying information about entities may be captured. 

With Flagged Attributes marked Y all corresponding data can be treated as high-risk throughout the data lifecycle and encrypted or removed at any stage, reducing the risk of re-identification attacks against blinded datasets.

## Character encoding and format
Character Encoding is on the Main tab. The recommended choice is utf-8 (Unicode Transformation Format – 8 bits) unless there is a very specific reason for this to be different.

The Format Overlay defines the input and display format of the data field. 

Types of formats are: YYYY-MM-DD for date, image/jpeg, [A-Z0-9]{8} (8 character long alpha-numeric entry). If left blank the default is text.

## Limiting data entry to a choice from a list (i.e. drop-down menu)
To limit data input to only a select number of choices (like in a drop-down menu) use:

1. Attribute Type: use array[text] or array[numeric] for the Attribute Type 
2. Format: the format for the entry code
3. Entry Code: write short names for the items in the list (separated by the pipe | symbol)
4. In each language tab for Entry give more human-readable labels matching each Entry Code to a language specific label

Example 1: to limit gender entry to one of three choices
1. Attribute Type: array[text] 
2. Format: [0-9]{1}
3. Entry codes: M|F|X 
4. In the language tab for Entry: “M:Male|F:Female|X:Other” for English and “M:Masculin|F:Féminin|X:Autre” for French

Example 2: to limit bee types to only two choices
1. Attribute Type: Array[Numeric]
2. Format: [0-9]{3}
3. Entry codes: 501|527
4. In the language tab for Entry: "501:Carniolan honey bee|527:Russian honey bee" for English and "501:Abeille de Carniole|527:Abeille russe" for French

## English language details
Attribute Names are automatically copied from Main tab into the Attribute Name of each language tab.

Meta[Form Name] column is a single cell entry for schema name (e.g. “Biodiversity Schema”) 

Meta[Form Description] is a single cell entry for a description of your schema (e.g. “A schema to capture biodiversity data”). 

These details will help make your schema more discoverable and can help people confirm that they have the right schema when they find yours.

## Adding language specific labels and more information
Each language specific tab is where you add language specific details to your schema. 

Labels are more reader friendly labels of attribute. If you are creating a questionnaire, the Label would be where you put the full text of your question.

Information contains details to help users of your schema understand exactly what is being collected for each attribute. It helps to add context to your data and helps people using your schema know what kind of information they should be inputting into each field. These fields should be quite descriptive.

# Convert from Excel to OCA

The [XLS to OCA Converter](https://browser.oca.argo.colossi.network/#/) is currently hosted at Human Colossus Foundation in the first phase of development. 

Upload the Excel document into the parser to create the OCA Bundle. 

The OCA Bundle contains the Capture Base and its associated Overlays into an archival (.zip) format. 

You can view the JSON code that describes each Capture Base and Overlay in any text viewer. Each JSON file contains the SAID identifier for each layer and Capture Base. The SAID identifier for the entire OCA Bundle is in the filename of the bundle.

# What to do with your OCA bundle

