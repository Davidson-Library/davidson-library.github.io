# Dublin Core XML Transformation into Preservica-ready XML

## Davidson College Context

Davidson College is exporting metadata records from Alma to ingest content into Preservica for preservation. We are starting with some Oral Histories and Interviews, including video, audio, and text files. Alma exports the .xml file with a `<record>` tag and Preservica needs the `<oai_dc:dc>` tag. The Alma DC record also comes with a `<discovery:resourceType>` tag that isn't allowed in Preservica.

- [Download and Transform Bulk](#download-and-transform-bulk)
  - [Create Analysis in Alma Analytics](#create-analysis-in-alma-analytics)
  - [Create Set From Analytics](#create-set-from-analytics)
  - [Run "Export Digital Titles" Job](#run-export-digital-titles-job)
  - [Run XSLT Code](#run-xslt-code)
  - [Rename XML Files for Media](#rename-xml-files-for-media)
- [Ingest Files along with Metadata into Preservica [TDB]](#ingest-files-along-with-metadata-into-preservica-tdb)
- [Download and Transform Individual Files](#download-and-transform-individual-files)
  - [How to Obtain the DC XML Record](#how-to-obtain-the-dc-xml-record)
  - [XSLT Code](#xslt-code)

### Download and Transform Bulk

Bulk export from Alma and splitting into multiple XML files after XSL transformation is the preferred method as it speeds the process up quite a bit.

#### Create Analysis in Alma Analytics

Click on **Analytics** then **Design Analytics** to open the Oracle Dashboard.

![Design Analytics link](help_files/Analytics_Design.png)

Click on **Catalog** then navigate to the **Alma Digital shared folder** and **click edit** of the analysis titled **"Digital Title Set Creation Template"**

![Catalog and Folder Directory](help_files/Analytics_Edit_Template.png)

It will by default show you the results, so click the **Criteria** tab at the top-left. Then **click the gear** next to the "Collection Name" column to apply a filter.

![Criteria Apply Filter](help_files/Analytics_Edit_Filter.png)

Click on the magnifying glass icon to open up the available filter for "Collection Name."

![Search Collection Name Magnifying Glass](help_files/Analytics_Edit_Filter_Search.png)

**Search for the Collection Name title** and either **double click it** or **click it once** before **clicking the `>`** to populate the "Selected" box with the collection you want to filter for a set. Finally, **click OK twice.**

![Select Collection to Filter](help_files/Analytics_Edit_Filter_Select.png)

The Filters panel will show the collection name. Once you confirm the collection name, **click Results** to make sure the PIDs are displaying.

![Confirm Collection Name](help_files/Analytics_Edit_Filter_Confirm.png)

You'll then see a table with PIDs and Collection Names. Now you will **Save As** a new analysis to keep the template empty of filters. Save it as the Collection Name Set, e.g., Irving Bienstock project Set. *This may go into a sub folder of sets?*

![Save As Set](help_files/Analytics_Edit_Filter_SaveAs_Set.png)

#### Create Set From Analytics

Now that the collection has been saved as an analysis, you can create a set "From Analytics." Back in Alma, select **Admin** then **Manage Sets**

![Admin Manage Sets](help_files/Analytics_Admin_Manage.png)

**Click Add Set** then **Itemized**

![Add Set](/help_files/Analytics_Create_Set.png)

Give the set a name (probably the name of the collection), **select Digital titles** from the "Set content type" dropdown, and **select From Analytics.** Alma will take a bit to process all the directories in analytics. Now's a good time for a stretch 🙆‍♀️  or coffee :coffee: (seriously).

The folder will default to "Recent reports" and the analysis you just saved doesn't always show up there. **Select** the `Davidson College 01DCOLL_INST/Reports/Alma Digital` folder directory and then the name of the analysis in the field below the folder. **Click Save**. You'll receive an email when the set has be created (usually instantly)

![Set Details](help_files/Analytics_Create_Details.png)

It will now show up as a set under **My Sets**. :tada:

![My Sets](help_files/Analytics_Create_Complete.png)

#### Run "Export Digital Titles" Job

**Click Admin** then **Run a Job**

![Admin Run Job](help_files/Job_Run.png)

**Search "export digital"** to narrow down the 100+ jobs. **Select Export Digital Titles** and **click Next**.

![Select Job](help_files/Job_Select.png)

**Select the Set** you want to perform the job on and **click Next**.

![Select Set for Job](help_files/Job_Select_Set.png)

**Change** the following parameters:

1. Target format = `OAI DC`
2. Bibliographic record formats to include = `Dublin Core`

Everything else can be left as is. **Click Next**.

![Job Parameters](help_files/Job_Parameters.png)

No need to give the job a name, so **click Submit**. You will receive an email once the job is complete (quick depending on size of collection/set). **Click the History tab** and then the **report link**.

![Job Success](help_files/Job_Success.png)

**Click** the "Link to Exported records" link.

![Link to XML](help_files/Job_Bibs.png)

**Click the `.xml` bibliographic link** to download the file. It should download to wherever your downloads directory is. Now you can run the XSLT to copy each record from the `.xml` file into individual `.xml` files for ingest to Preservica.

#### Run XSLT Code

- Open both the downloaded DC bib `.xml` file and the [Split_Single_to_Multiple_XML_Files.xsl file](./Split_Single_to_Multiple_XML_Files.xsl) in Oxygen XML Editor.
- Click the XSLT Debugger perspective button
![XSLT Debugger View](help_files/Rename_XSLT_Debugger.png)
- Make sure you have the two files selected (exported `.xml` file and `.xsl` file).
- Select where you want the individual files saved. I'd recommend saving local instead of the Preservica server folder. **Click the "Run to End"** button
![Oxygen Setup](help_files/XSTL_Setup2.png)

The files will now appear in the Output directory you selected.

![Files Output](help_files/XSL_Output_Folder.png)

#### Rename XML Files for Media

Since the `.xslt` created single `.xml` files, you now need to rename these to match the media files exactly, with the additional `.metadata`, e.g., `OHI-0357_V_ShowersCharlesO_20220310.mp4.metadata` This is what Preservica requires.

I recommend going back to the XML Editor perspective for a fuller screen of the long  `.xml` file.

![Editor View](help_files/Rename_XSLT_Editor.png)

The new list of files e.g., `file1-40.xml` are in the same order as they appear in the main `.xml` file exported from Alma. Scroll through that file to target the newly transformed individual files and match it with the `fileX.xml`. The easiest way is to find the OHI in the `<dc:identifier>` field.

![OHI ID](help_files/Rename_OHI_ID.png)

Copy the file name from one of the media files that match the OHI ID

![Copy file name](help_files/Rename_Multi_Files_Copy.png)

Rename `fileX.xml` and paste the copied text and edit the `.xml` with `.metadata`

![Paste file name](help_files/Rename_Multi_Files_Paste.png)

![change xml to metadata](help_files/Rename_Multi_Files_MetadataXML.png)

Open the newly named `.metadata` file and make sure the `dc:type` matches the media it's for. This is the only `dc` field that will need to be updated. Typical names are:

- V and .mp4 for `MovingImage`
- A and .mp3 or .m4a for `Sound`
- T and .pdf or .doc for `Text`

![type of media](help_files/Rename_Multi_Files_Type.png)

Once the `dc:type` matches the media file type, **Save As**

![save as screen](help_files/Rename_Multi_Files_SaveAs.png)

Rename the file (typical examples above). Oxygen Editor will add `.xml` after the `.metadata` so make sure to delete `.xml` as this speeds up the Ingest process in Preservica.

![rename file](help_files/Rename_Multi_Files.png)

If there's one (1) Audio, one (1) Video, and one (1) Transcript media, there should be three (3) metadata files, totalling six (6) files.

![3 metadata files](help_files/Rename_3_Files.png)
![3 media files](help_files/Rename_3_Files_Media.png)

Continue through the list of transformed `.xml` files from the `.xsl` using this method.

### Ingest Files along with Metadata into Preservica [TDB]

### Download and Transform Individual Files

#### How to Obtain the DC XML Record

The DC XML file is obtained through the ["Download BIB" Cloud Apps in Alma](https://developers.exlibrisgroup.com/blog/how-to-install-and-use-the-download-bib-cloud-app/).

![Download BIB Cloud Apps](help_files/Download-BIB_CloudApps.png)

#### XSLT Code

The following xslt transforms the xml into the right format for ingest into Preservica:

```xslt
<xsl:stylesheet version="2.0"
  xsi:schemaLocation="http://www.openarchives.org/OAI/2.0/oai_dc/ oai_dc.xsd"
  xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
  xmlns:dc="http://purl.org/dc/elements/1.1/"
  xmlns:oai_dc="http://www.openarchives.org/OAI/2.0/oai_dc/"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xmlns:discovery="http://purl.org/dc/elements/1.1/">
  <xsl:output method="xml" version="1.0" encoding="UTF-8" indent="yes"/>
  <xsl:strip-space elements="*"/>

  <xsl:template match="node()|@*">
    <xsl:copy>
      <xsl:apply-templates select="node()|@*"/>
    </xsl:copy>
  </xsl:template>
  <xsl:template match="discovery:resourceType">
    <xsl:apply-templates/>
  </xsl:template>
  <xsl:template match="record">
    <oai_dc:dc>
      <xsl:apply-templates/>
    </oai_dc:dc>
  </xsl:template>
</xsl:stylesheet>
```
