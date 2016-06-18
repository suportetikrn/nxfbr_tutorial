Custom login script for single sign-on
***************************************
Currently NxFilter supports single sign-on with Active Directory. However some people want more than that. For example, you might want to have single sign-on with your OpenLDAP.
NxFilter supports an API set for creating login session through HTTP protocol. You need to write your custom login script to call some webpage on NxFilter's built-in webserver. And then your users don't need to go through NxFilter's login-page.
We have example code on '/nxfilter/example/login_user.jsp'. Initially the access of the page is restricted to localhost only for security reason but you can edit the JSP page to allow the calls from your local network.
You can call the webpage this way.

.. code-block::

  http://192.168.0.100/example/login_user.jsp?ip=192.168.0.100&uname=john


As you see there are two parameters being passed. One is the IP address of your user and the other one is the associated username. The username should be imported or created on NxFilter side already.
One thing you need to consider when you write your own login script is that it might be better to call the webpage periodically. There is a session timeout concept in NxFilter. If there is no activity from a logged-in user for certain amount of time the login session will be expired. So if you don't want to show your users NxFilter's login-page, you would need to refresh the login session periodically.
There are three methods of UserLoginDao class for custom login script.

.. code-block:: java
  
  create_ip_session(String ip, String uname) : Creating a login session with an IP and username.

  delete_ip_session(String ip) : Deleting a login session with an IP.

  find_user(String ip) : You can find a logged-in username by its associated IP address.


All the example JSP pages are in '/nxfilter/webapps/example' directory.

