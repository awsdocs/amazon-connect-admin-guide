# Output file locations for files analyzed by Contact Lens<a name="example-contact-lens-output-locations"></a>

Following are examples of what the path looks like for Contact Lens output files when they are stored in the Amazon S3 bucket for your instance\. 
+ Original analyzed transcript file \(JSON\)
  + /connect\-instance\- bucket/**Analysis/Voice**/2020/02/04/*contact's\_ID*\_analysis\_2020\-02\-04T21:14:16Z\.json
  + /connect\-instance\- bucket/**Analysis/Chat**/2020/02/04/*contact's\_ID*\_analysis\_2020\-02\-04T21:14:16Z\.json
+ Redacted analyzed transcript file in \(JSON\)
  + /connect\-instance\- bucket/**Analysis/Voice/Redacted**/2020/02/04/*contact's\_ID*\_**analysis\_redacted**\_2020\-02\-04T21:14:16Z\.json
  + /connect\-instance\- bucket/**Analysis/Chat/Redacted**/2020/02/04/*contact's\_ID*\_**analysis\_redacted**\_2020\-02\-04T21:14:16Z\.json
+ Redacted audio file
  + /connect\-instance\- bucket/**Analysis/Voice/Redacted**/2020/02/04/*contact's\_ID*\_**call\_recording\_redacted**\_2020\-02\-04T21:14:16Z\.**wav**

**Important**  
To delete a recording, you must delete the files for both the redacted and unredacted recordings\. 