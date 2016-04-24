**********************************
GUI - NxClassifier
**********************************


We have 'NxClassifier' top menu on GUI. It has the following submenus.

Setup > Classifier Setup
************************

- DNS Test Timeout : NxClassifier only classifies the existing domains. So it does DNS testing first when it needs to classify a domain.
- HTTP Connection Timeout : After DNS testing, now it needs to download a webpage to analyze. This is the connection timeout value for HTTP connection.
- HTTP Read Timeout : This is the data read timeout value after you have an HTTP connection.
* If you make these timeout values too big you might have a performance degrading for NxClassifier.
- Classified Data Retention Days : NxClassifier makes the classification result log for the recently classified websites. NxClassifier doesn't do the classification if it is already classified or if it is in the classification log without an error.
- Disable Domain Pattern Dic : NxFilter has a domain pattern based calssification process.
- Disable Classification : You can disable the classification by NxClassifier.

Setup > Mass Import
*******************

You use this when you want to import a ruleset file or Jahaslist file exported from another system. It doesn't delete the existing data. But it overwrites the existing data if it is the same one.

Ruleset
*********

You can define your own ruleset here. Or modify the default ruleset. You can export the ruleset and share it with others.

Classified
*********

This is the classification result log by NxClassifier. It will show yout the recently classified domains and how they got classified or unclasssified. Based on this classification result you can improve your classification ruleset.
* With 'VIEW' button you can view the details of the log and with 'TEST' button you do the actual classification process for a domain with your current ruleset.

 .. note:: If you want to apply a new classification ruleset against the already classified sites use 'RECLASSIFY-ALL' button.

Excluded
*********

We exclude the domains making certain errors during the classification process. For example, if we have 403 response from a website we don't need to try to classify it as we can't access the website. Or if we get an image file or some other type of file instead of a text or HTML file we will exclude it.

 .. note:: Since we don't delete these excluded domains if you want to have NxClassifier trying to classify an excluded domain you would need to delete it from the list first.

Jahaslist
*********

You can view the contents of Jahaslist and modify it directly here. But we don't recommend you to do the reclassification here unless it is a mass importation of domains. We keep Jahaslist in a separated DB file and NxFilter doesn't do auto-backup for it. So you would better use 'Category > System' for reclassification as it is in the main config DB.

 .. note::
  When you do the reclassification on 'Logging > Request' or 'NxClassifier > Classified' your reclassification data goes into 'Category > System'.
  When you export Jahaslist, NxFilter merges your custom classified domains from 'Category > System' into Jahaslist and then export the merged result into a file.

Test Run
*********

After you add your own classification rules you want to see the result. You can do a test run for your classification ruleset against a website here.

 .. note:: 'Test Run' doesn't do actual classification. If you want to classify a domain you need to make a query for the domain against NxFilter.
