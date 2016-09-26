Removing embedded adverts in webpages
**************************************

There are webpages having embedded adverts from other domains. One of the problems for blocking these adverts with NxFilter would be having a mangled webpage as a result of blocking. Your block-page replaces the embedded adverts.

To avoid of having this kind of problem, there are two ways of removing embedded adverts with NxFilter. One is using a special category in 'Category > Custom' which is called 'ad-remove'. If you add a domain into this category and block the category somewhere, NxFilter blocks the domain with a blank block-page.

The other method is to block it using the 'Ad-remove' option on a policy. With this option NxFilter blocks 'Ads' category of Jahaslist.

.. note::

  After you add a domain into 'ad-remove' category you need to block the domain on whitelist or policy otherwise it will not be blocked.
