# Step by step instructions

# Entering schema information
Below is an example schema that has been entered into the OCA template. By following the instructions you will be able to create your own schema.

![Example of entering capture base data into the OCA schema template.](/pictures/capture_base.png)
![Example of entering english overlayd data into the OCA schema template.](/pictures/overlay_en.png)

## Creating an OCA schema – Excel template
Download the Excel OCA schema template[link when available].

**Do not change the basic structure of the Excel sheet** as the parser needs this structure to create the OCA schema bundle. For example, you can see that data entry of sheet Main starts on row 3 so you should not delete the rows above.

1. Enter schema metadata onto 'Start Here' tab (Title, schema included, contact information etc). This is for your records so in the future when you (or someone else) looks at this Excel sheet you know what it is.
2. On the language tab (en and/or fr) for columns enter the schema name in **[Form Name]** and schema description in **[Form Description]**
3. For each column of your dataset on the Main tab:
   1. Enter the **Attribute Name** (aka variable name, data column header etc.)
      - examples are CollectionDate, Concentration, Insect_Type, SampleLocation, gene_name etc.
   2. Enter the **Attribute Type**. Choose from:      
      - *Text*: a data type that defines a human-readable sequence of characters and the words they form.
      - *Numeric*: a data type that defines anything relating to or containing numbers.
      - *Reference*: a data type that defines a Self-Addressing IDentifier (SAID) that references a set of attributes through its associated parent.
      - *Boolean*: a data type where the data only has two possible variables: true or false.
      - *Binary*: a data type that defines a binary code signal, a series of electrical pulses representing numbers, characters, and performed operations.
      - *DateTime*: a data type that defines dates and/or times. Common formats include dates (e.g., YYYY-MM-DD), times (e.g., hh:mm:ss), dates and times concatenated (e.g., YYYY-MM-DDThh:mm:ss.sss+zz:zz), and durations (e.g., PnYnMnD).
      - *Array* [attribute type]: a data type that defines a structure that holds several data items or elements of the same data type.
   4. Enter the **Character** (if you don't know, you should pick UTF-8)
   5. Enter the **Format**
      - note: default type is text.
      - If you are unsure about format, leave it blank (default) for now.
      - Check this page(not yet developed) for detailed examples.
   6. For each language tab enter the **Label** for each Attribute. A label can be language specific and longer if needed.
   7. For each language tab enter descriptions of the attributes into **Information**. Descriptions can be language specific.
   8. You will notice there are many other OL (overlay) columns available in the spreadsheet template. You can continue to refine and improve your schema by adding detail in the future.

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


# Convert from Excel to OCA

The [XLS to OCA Converter](https://browser.oca.argo.colossi.network/#/) is currently hosted at Human Colossus Foundation (HCF) in the first phase of development. Upload the Excel document into the parser to create the OCA Bundle. 

You can open the archive and view the JSON code that describes each Capture Base and Overlay in any text viewer. The [SAID](identifiers_and_saids.md) identifiers for Overlays, Capture Base and the entire OCA Bundle are the filenames. The "meta.json" file lists all Overlays and Capture Base including their SAID identifiers. 


# Detailed OCA Creation Instructions

[Follow this link to more detailed OCA schema creation instructions](create_OCA_schema.md).
