******************
O que é NxCloud?
******************
NxCloud is a fully rebrandable multi-tenancy cloud based DNS filter software. It is based on NxFilter and inherited the most of the features of NxFilter. Simply speaking, you can build your own cloud filtering service like OpenDNS.
These are the features only available on NxCloud.

Multi-level admin
^^^^^^^^^^^^^^^^^^
If you want to build your own cloud service, one of the essential factors would be being able to create accounts for your customers and the customers need to be able to set up their own policy on their own GUI.
On NxCloud there are 3 kinds of users.
Admin > Operator > User
'Admin' is actually the administrator of NxCloud. It has almost the same GUI as the NxFilter but being an administrator you can create the operator accounts. These operator accounts are for your customers and it is something like a sub-admin on NxCloud. They can create and manage their own users and policies.

Creating an operator
^^^^^^^^^^^^^^^^^^^^^

To create an operator you need to login to NxCloud GUI with admin account. On 'Config > operator' you can create an operator. When you create an operator NxCloud creates a default user and a default policy for the operator with the same name.
You can change the number of users and policies the operator can create. This means you can have several levels on your service based on the permission for an operator.

Operator GUI
^^^^^^^^^^^^^

On NxCloud each operator have their own GUI. If you login to NxCloud GUI with an operator account you will be on the operator mode GUI. It is a bit more restrictive compared to the admin GUI as you only can manipulate the operator specific parameters.

Operator and user
^^^^^^^^^^^^^^^^^^^

Operators can create their own users and apply a different policy based on user authentication. Users can be authenticated based on IP address or using NxClient.
Operator specific dashboard and report
Dashboard and report of NxCloud is still available on operator GUI.

Operator specific free-time
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each operator can define their own free-time and they can set up a work-time policy and a free-time policy for their user.

Operator specific whitelist and blacklist
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can add operator specific whitelist/blacklist based on domain name. But you still have the global whitelist/blacklist for admin. So you can have more flexibility to deal with these whitelist and blacklist as an admin.
Operator specific alert-email
NxCloud sends an alert email about the blocking incidents to each operator. Operators can setup their email addresses to receive the email and define alert period on 'Config > Alert'.
* You need to set up the global alert email first to send the operator specific alert email. You can set it up on 'Config > Alert'.

Operator specific block-page
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Each operator can have their own block-page. If there is no block-page defined by operator NxCloud shows the default block-page by admin.

Authentication over cloud
^^^^^^^^^^^^^^^^^^^^^^^^^^

NxClient still works against NxCloud. This means you can differentiate users behind their router and you can apply a different policy based on user.

Dynamic IP updater
^^^^^^^^^^^^^^^^^^^

Many of your clients will be using the service from a dynamic IP address. You can use NxUpdate as a dynamic IP updater for your service.

Dynamic DNS association
^^^^^^^^^^^^^^^^^^^^^^^^^

Some of your users may have a dynamic domain for their own network. You can associate a domain to a user on NxCloud.

NxRelay to differentiate users behind a router
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
NxCloud supports NxRelay that is a relaying DNS server being installed behind a router and let you apply a different policy based on a private IP or IP range in your network.

Rebranding or customization of GUI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Its GUI layer is designed for easy customization. The GUI layer is separated from its core part. You just need to modify all the JSP pages in '/nxcloud/webapps' directory. These JSP files have a naming rule corresponding to the GUI menu structure. So it is easy to find which file you need to modify.
