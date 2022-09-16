# Rename XML Files for Media

Since the `.xslt` created single `.xml` files, you now need to rename these to match the media files exactly, with the additional `.metadata`, e.g., `OHI-0357_V_ShowersCharlesO_20220310.mp4.metadata` This is what Preservica requires.

I recommend going back to the XML Editor perspective for a fuller screen of the long `.xml` file.

![Editor View](../help\_files/Rename\_XSLT\_Editor.png)

The new list of files e.g., `file1-40.xml` are in the same order as they appear in the main `.xml` file exported from Alma. Scroll through that file to target the newly transformed individual files and match it with the `fileX.xml`. The easiest way is to find the OHI in the `<dc:identifier>` field.

![OHI ID](../help\_files/Rename\_OHI\_ID.png)

Copy the file name from one of the media files that match the OHI ID

![Copy file name](../help\_files/Rename\_Multi\_Files\_Copy.png)

Rename `fileX.xml` and paste the copied text and edit the `.xml` with `.metadata`

![Paste file name](../help\_files/Rename\_Multi\_Files\_Paste.png)

![change xml to metadata](../help\_files/Rename\_Multi\_Files\_MetadataXML.png)

Open the newly named `.metadata` file and make sure the `dc:type` matches the media it's for. This is the only `dc` field that will need to be updated. Typical names are:

* V and .mp4 for `MovingImage`
* A and .mp3 or .m4a for `Sound`
* T and .pdf or .doc for `Text`

![type of media](../help\_files/Rename\_Multi\_Files\_Type.png)

Once the `dc:type` matches the media file type, **Save As**

![save as screen](../help\_files/Rename\_Multi\_Files\_SaveAs.png)

Rename the file (typical examples above). Oxygen Editor will add `.xml` after the `.metadata` so make sure to delete `.xml` as this speeds up the Ingest process in Preservica.

![rename file](../help\_files/Rename\_Multi\_Files.png)

If there's one (1) Audio, one (1) Video, and one (1) Transcript media, there should be three (3) metadata files, totalling six (6) files.

![3 metadata files](../help\_files/Rename\_3\_Files.png) ![3 media files](../help\_files/Rename\_3\_Files\_Media.png)

Continue through the list of transformed `.xml` files from the `.xsl` using this method.
