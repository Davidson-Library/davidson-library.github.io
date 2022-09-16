# Run "Export Digital Titles" Job

**Click Admin** then **Run a Job**

![Admin Run Job](../help\_files/Job\_Run.png)

**Search "export digital"** to narrow down the 100+ jobs. **Select Export Digital Titles** and **click Next**.

![Select Job](../help\_files/Job\_Select.png)

**Select the Set** you want to perform the job on and **click Next**.

![Select Set for Job](../help\_files/Job\_Select\_Set.png)

**Change** the following parameters:

1. Target format = `OAI DC`
2. Bibliographic record formats to include = `Dublin Core`

Everything else can be left as is. **Click Next**.

![Job Parameters](../help\_files/Job\_Parameters.png)

No need to give the job a name, so **click Submit**. You will receive an email once the job is complete (quick depending on size of collection/set). **Click the History tab** and then the **report link**.

![Job Success](../help\_files/Job\_Success.png)

**Click** the "Link to Exported records" link.

![Link to XML](../help\_files/Job\_Bibs.png)

**Click the `.xml` bibliographic link** to download the file. It should download to wherever your downloads directory is. Now you can run the XSLT to copy each record from the `.xml` file into individual `.xml` files for ingest to Preservica.
