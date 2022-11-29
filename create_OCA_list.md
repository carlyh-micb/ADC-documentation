# Step by step instructions

## Creating an OCA schema – Excel template
Download the Excel OCA schema template[link when available].

**Do not change the basic structure of the Excel sheet** as the parser needs this structure to create the OCA schema bundle. For example, you can see that data entry of sheet Main starts on row 3 so you should not delete the rows above.

1. Enter schema metadata onto READ ME tab (Title, schema included, contact information etc). This is for your records.
2. On the language tab (en_CA and/or fr_CA) for columns enter the schema name in **OL-MN:Meta [Form Name]** and schema description in **OL-MD: Meta[Form Description]**
3. For each column of your dataset on the Main tab:
   1. Enter the **Attribute Name** (column header)
      - examples are CollectionDate, Concentration, InsectType, SampleLocation
   2. Enter the **Attribute Type**. Choose from:      
      - Text: a data type that defines a human-readable sequence of characters and the words they form.
      - Numeric: a data type that defines anything relating to or containing numbers.
      - Reference: a data type that defines a Self-Addressing IDentifier (SAID) that references a set of attributes through its associated parent.
      - Boolean: a data type where the data only has two possible variables: true or false.
      - Binary: a data type that defines a binary code signal, a series of electrical pulses representing numbers, characters, and performed operations.
      - DateTime: a data type that defines dates and/or times. Common formats include dates (e.g., YYYY-MM-DD), times (e.g., hh:mm:ss), dates and times concatenated (e.g., YYYY-MM-DDThh:mm:ss.sss+zz:zz), and durations (e.g., PnYnMnD).
      - Array [attribute type]: a data type that defines a structure that holds several data items or elements of the same data type.
   4. Enter the **Character** (recommendation UTF-8)
   5. Enter the **Format**
      - note: default type is text. Check this page for detailed examplexs.
   6. For each language tab enter the **Label** for each Attribute
   7. For each language tab enter descriptions of the attributes into **Information**
4. To limit data entry to a choice from a list (i.e. create a drop-down menu)
     1. **Attribute Type**: use array[text] or array[numeric] for the Attribute Type 
     2. **Format**: the format for the entry code
     3. **Entry Code**: write short names or numbers coding for the items in the list (separated by the pipe &#124; symbol)
     4. In each language tab for Entry give more human-readable labels matching each **Entry** to a language specific label

> Example 1: to limit gender entry to one of three choices
> 1. Attribute Type: array[text] 
> 2. Format: [A-Z]{1}
> 3. Entry codes: M&#124;F&#124;X 
> 4. In the language tab for Entry: “M:Male&#124;F:Female&#124;X:Other” for English and “M:Masculin&#124;F:Féminin&#124;X:Autre” for French

> Example 2: to limit bee types to only two choices
> 1. Attribute Type: Array[Numeric]
> 2. Format: [0-9]{3}
> 3. Entry codes: 501&#124;527
> 4. In the language tab for Entry: "501:Carniolan honey bee&#124;527:Russian honey bee" for English and "501:Abeille de Carniole&#124;527:Abeille russe" for French
