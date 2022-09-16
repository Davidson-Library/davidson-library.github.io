# Download and Transform Bulk

## Davidson College Library Context

Davidson College is exporting metadata records from Alma to ingest both the metadata and media into Preservica for preservation. We are starting with Oral Histories and Interviews, including video, audio, and text files. Alma exports the `.xml` file with a `<record>` tag and Preservica needs the `<oai_dc:dc>` tag. The Alma DC record also comes with a `<discovery:resourceType>` tag that isn't allowed in Preservica. This process includes 1) bulk download from Alma, 2) `xsl` transformation, and 3) ingestion into Preservica.

## Process Steps

There are five (5) main steps to export and cleanup the metadata to get it ready for Preservica:

1. Create Analysis in Alma Analytics
2. Create Set from Analysis
3. Run "Export" job in Alma
4. Run XSLT on bib records
5. Rename XML Files

## Future Development

Documentation for ingesting into Preservica is coming soon. I'm also interested in speeding up the process of renaming the split `.xml` files to pair with the media for ingest into Preservica.
