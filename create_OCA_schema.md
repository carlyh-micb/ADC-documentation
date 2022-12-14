# How to create an OCA Schema
This is a tutorial of how to create an [Overlays Capture Architecture](https://oca.colossi.network/specification/) (OCA) data schema. This technology is currently under active development at [Agri-food Data Canada](https://agrifooddatacanada.ca/) in cooperation with the [Human Colossus Foundation](https://humancolossus.foundation/)(HCF). 

## An Excel template is parsed to OCA schema bundle
By following this tutorial, you will create an Excel template document, upload it to the OCA parser, and generate the OCA schema bundle for download and use.
Read a [brief background in data schemas, and an introduction to the OCA schema](semantic_engine.md).

# Creating an OCA schema – Excel template
Download the Excel OCA schema template[link when available].

When you enter data into this template, do not change the basic structure as the parser needs this structure to create the OCA schema bundle. For example, you can see that data entry of sheet Main starts on row 3 so you should not delete the rows above.

The 'Start Here' tab is for your reference, and you should add metadata here (like title and contact information) which can help you understand and track your Excel schemas.


# Entering schema information
Below is an example schema that has been entered into the OCA template. By following the instructions you will be able to create your own schema. 

![Example of entering capture base data into the OCA schema template.](/pictures/capture_base.png)
![Example of entering english overlayd data into the OCA schema template.](/pictures/overlay_en.png)

## Required fields
All Capture Base (CB) fields are required as well as two Overlays (OL): Character Encoding and Format.

OCA schemas are very robust, you can start by adding minimal information and as you need you can add more details to your schema and complete more Overlays.

## Classification
On the Main tab, under Classification you can add classifications for each attribute. This overlay is not standardized but it is recommended to be in the format system:type. For example, to add classifications for [sustainable development goals](https://unstats.un.org/sdgs/indicators/indicators-list/) for each attribute you can use "SDG:15"

## Attribute Names
On the Main tab, under Attribute Names add your unique list of attribute names, also known as variable names or your data column labels. Because this field may be used by many different computer systems we recommend to not include spaces and use under_scores or CamelCase instead.

## Attribute Types
On the Main tab specify the Attribute Type, which should be one of the following:
* **Text**: a data type that defines a human-readable sequence of characters and the words they form.
* **Numeric**: a data type that defines anything relating to or containing numbers. 
* **Reference**: a data type that defines a [Self-Addressing IDentifier (SAID)](identifiers_and_saids.md) that references a set of attributes through its associated parent. 
* **Boolean**: a data type where the data only has two possible variables: true or false.
* **Binary**: a data type that defines a binary code signal, a series of electrical pulses representing numbers, characters, and performed operations. 
* **DateTime**: a data type that defines dates. Common formats include dates (e.g., YYYY-MM-DD), times (e.g., hh:mm:ss), dates and times concatenated (e.g., YYYY-MM-DDThh:mm:ss.sss+zz:zz), and durations (e.g., PnYnMnD).
 * **Array** [attribute type]: a data type that defines a structure that holds several data items or elements of the same data type. 

## Sensitive or personal data flagging
On the Main tab specify Flagged Attribute for sensitive data. Marking an entry with a “Y” will allow you to flag any attributes where identifying information about entities may be captured. 

With Flagged Attributes marked Y all corresponding data can be treated as high-risk throughout the data lifecycle and encrypted or removed at any stage, reducing the risk of re-identification attacks against blinded datasets.

## Character encoding and format
Character Encoding is on the Main tab. The recommended choice is utf-8 (Unicode Transformation Format – 8 bits) unless there is a very specific reason for this to be different.

The Format Overlay defines the input and display format of the data field. This will be very important for data validation which is the first step in making sure you data is accurate. Data validation is when you check for incorrect values, for example you want to make sure that there are no negative measurements allowed, or no zeros or numbers greater than 1000, or no null values etc.

Types of formats are: YYYY-MM-DD for date, image/jpeg, [A-Z0-9]{8} (8 character long alpha-numeric entry). If left blank the default is text.

## Limiting data entry to a choice from a list (i.e. drop-down menu)
To limit data input to only a select number of choices (like in a drop-down menu) for an attribute use:

1. Attribute Type: use [text] or [numeric] for the Attribute Type (for single selection, for multiple selection use array[text] or array[numeric])
2. Format: the format for the entry code
3. Entry Code: write short names or numbers coding for the items in the list (separated by the pipe &#124; symbol)
4. In each language tab for Entry give more human-readable labels matching each Entry Code to a language specific label

>Example 1: to limit gender entry to one of three choices
>1. Attribute Type: [text] 
>2. Format: [A-Z]{1}
>3. Entry codes: M&#124;F&#124;X 
>4. In the language tab for Entry: “M:Male&#124;F:Female&#124;X:Other” for English and “M:Masculin&#124;F:Féminin&#124;X:Autre” for French

>Example 2: to limit bee types to only two choices
>1. Attribute Type: [Numeric]
>2. Format: [0-9]{3}
>3. Entry codes: 501&#124;527
>4. In the language tab for Entry: "501:Carniolan honey bee&#124;527:Russian honey bee" for English and "501:Abeille de Carniole&#124;527:Abeille russe" for French

## Adding language specific labels and more information
Each language specific tab is where you add language specific details to your schema. 

Attribute Names are automatically copied from Main tab into the Attribute Name of each language tab.

Meta[Form Name] column is a single cell entry for schema name (e.g. “Biodiversity Schema” for English)

Meta[Form Description] is a single cell entry for a description of your schema (e.g. “A schema to capture biodiversity data” for English). 

These details will help make your schema more discoverable and can help people confirm that they have the right schema when they find yours.

Labels are more reader friendly labels of the attribute. If you are creating a questionnaire, the Label would be where you put the full text of your question.

Information contains details to help users of your schema understand exactly what is being collected for each attribute. It helps to add context to your data and helps people using your schema know what kind of information they should be inputting into each field. These fields should be quite descriptive.

# Other available Overlays

You will notice there are many other OL (overlay) columns available in the spreadsheet template. You can continue to refine and improve your schema by adding detail in the future and we will be adding this documentation in the future as well.

# Convert from Excel to OCA

The [XLS to OCA Converter](https://browser.oca.argo.colossi.network/#/) is currently hosted at Human Colossus Foundation (HCF) in the first phase of development. The Semantic Engine's template is derived from the template found hosted by HCF.

Upload the Excel document into the parser to create the OCA Bundle. 

The OCA Bundle contains the Capture Base and associated Overlays as files bundled into an archival (.zip) format. 

You can open the archive and view the JSON code that describes each Capture Base and Overlay in any text viewer. The [SAID](identifiers_and_saids.md) identifiers for Overlays, Capture Base and the entire OCA Bundle are the filenames. The "meta.json" file lists all Overlays and Capture Base including their SAID identifiers. 


# More information about OCA

[Read more about what you can do with your OCA schema bundle](what_can_you_do_with_OCA.md)

## OCA is expressed in JSON
Overlays Capture Architecture is a machine-readable way to encode a schema expressed in the JSON scripting language. You can view the JSON file contents using a text editor such as Notepad in Windows but since JSON files do not usually contain line breaks it is easier to read using a [JSON viewer](https://jsonformatter.curiousconcept.com/).

Writing a schema in JSON is not very human-friendly, instead we will fill out the schema information in a template Excel spreadsheet. Then we upload this Excel sheet into the semantic engine OCA schema parser, and it will generate the OCA schema bundle. In the future as we develop the Semantic Engine, we can create easier ways to generate these OCA schemas, but in phase one of development we use the Excel template.

## OCA is made of Capture Base and Overlays
**Capture Base (CB)** is a stable base object that defines a single dataset in its purest form. It is good practice to keep the Capture Base stable and consistent because the Capture Base is given an identifier (SAID) that is derived from its content and all other overlays will reference this identifier. Furthermore, other users of your schema will confirm the Capture Base by its SAID identifier. If you change even a character of the Capture Base, the SAID identifier will change as well. 

**Overlays (OL)** are additional pieces of the schema that aren’t part of the Capture Base. They reference the SAID identifier of the Capture Base and specify additional information in the schema – such as language specific descriptions of different data columns. Because the Overlays are separate from the Capture Base, they can be added to a Capture Base later without disrupting the Capture Base description and identifier of the data structure.

**OCA uses Self-Addressing Identifiers (SAIDs)** for each part of the schema which are calculated from a hash of each JSON file generated. Each SAID is a unique fingerprint for each file and if you find two files with the same SAIDs then you can be confident the files are identical. Overlays of the schema bundle reference the unique SAID of the Capture Base. You can [read more about identifiers and self-addressing identifiers(SAIDS) here](identifiers_and_saids.md).
