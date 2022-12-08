# Convert from Excel to OCA

The Excel template with the schema informatin can be parsed into a machine actionable representation of the schema called OCA.

[XLS to OCA Converter](https://browser.oca.argo.colossi.network/#/) is currently hosted at Human Colossus Foundation (HCF) in the first phase of development. The Semantic Engine's template is derived from the template found hosted by HCF.

Upload the Excel document into the [parser to create the OCA Bundle](https://browser.oca.argo.colossi.network/#/).

The OCA Bundle contains the Capture Base and associated Overlays as files bundled into an archival (.zip) format.

You can open the archive and view the JSON code of the schema. The "meta.json" file lists is the most human readable and lists all Overlays and Capture Base including their SAID identifiers. The SAID identifiers for Overlays, Capture Base and the entire OCA Bundle are also their filenames. 

After you have created a schema from an Excel template we recommend that you copy the schema bundle SAID identifier onto the 'Start Here' sheet of your Excel template.
