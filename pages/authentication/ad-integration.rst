Integração com o AD
^^^^^^^^^^^^^^^^^^^

NxFilter supports Active Directory integration but some people find it hard to understand. So we want to explain what is Active Directory integration for NxFilter and when to use it and how to implement it at conceptual level.
What is Active Directory integration
One of the reasons why people want to integrate NxFilter into Active Directory is that they want to apply filtering policies based on Active Directory user and group. They also don't want to have their users going through any extra login step to use the Internet except when they login to their own PC. So for NxFilter, 'Active Directory integration' means using the same user account from your Active Directory to differentiate users and having single sign-on with your Active Directory.
User importation
Now we know what is Active Directory integration and why we need it. But how to do that? On NxFilter the first thing you need to do for implementing Active Directory integration is to import the users and groups from Active Directory. It means you need to let NxFilter be aware of your users and groups. You can do that on 'User & Group > Active Directory'.
After you import your users and groups, your users will be able to use their Active Directory credentials on NxFilter's login-page. So we already achieved Active Directory integration to a certain level.
Single sign-on with Active Directory
We can say that we achieved Active Directory integration as your users can use their Active Directory credentials on NxFilter's login-page. However your users don't want to go through the login-page so the next thing you need to do is implementing single sign-on with your Active Directory. To impelment single sign-on you need to use an agent program working with NxFilter. We have several agents that are NxLogon, NxMapper, NxClient. You can use just one of them or mix and match them to complement each other.

.. note::

  For more information, read single sign-on or agent related parts of this tutorial.

MS DNS server and NxFilter
**************************

  When you deploy NxFilter in an Active Directory environment you might be worrying about the possibility of breaking the integrity of Active Directory as NxFilter is a DNS server and the role of a DNS server in Active Directory is very important. But we don't disable or replace the existing Active Directory DNS server. Our approach is to work with the existing Active Directory DNS server in cooperation. So you have to maintain your existing MS DNS server even though you use NxFilter as the DNS server for your network.
  1. Where to install it
       Some people try to install NxFilter on their domain controller. But you already have a DNS server there. It is your MS DNS server. It would be better to install it on another system to avoid of having a port collision problem.
  2. Dynamic host update
       MS DNS server in Active Directory does a lot of things. It lets the hosts in Active Directory know the location of resources using SRV records. And it maintains a DNS zone for every hosts. It does dynamic host IP update when you change an IP address of a system. To keep all these things working NxFilter bypasses the internal DNS queries for Active Directory domain to MS DNS server automatically. It assumes that you have your MS DNS server on the DC you imported your users from.
  3. Which upstream server for NxFilter
      You might have a question about which DNS server you should use as an upstream server for NxFilter because you already have a DNS server that is your MS DNS server. You can use any DNS server as an upstream DNS server for your NxFilter including your MS DNS server. NxFilter still forwards your Active Directory internal DNS queries to your MS DNS server. So you can use whichever DNS server you think the best.
  4. Manual setup for MS DNS server
     After you import Active Directory users and groups, NxFilter tries to work with your MS DNS server automatically based on your Active Directory importation setup but sometimes you want to have a different settings for your MS DNS server. Or you might want to have a redundancy for your MS DNS server. In that case, you can do all these things on the edit page of your Active Directory importation setup. For having redundancy, you can add multiple DNS servers separated by commas.

.. note::

   You might need to allow 'Nonsecure Dynamic Update' on your MS DNS zone properties for NxFilter to update the IP addresses of the hosts in your MS DNS zone.

An examplary deployment scenario
********************************
                                                                               Lastly, we will give you an examplary deployment scenario. Suppose we are in a company environment. Many Windows PCs and some Macbooks and recently we bought several Chromebooks. And people bring their own iPhones and Android phones. And plus we have several Linux servers for our own website and file sharing. There are some mobile workers using company laptops. Some are using Windows and some are using Macbooks. And you want to filter all of them whether they are inside office or outside office with their Active Directory accounts.
                                                                               The first thing you need to do is to set up Active Directory user and group importation. And then use NxLogon for these Windows PCs. But NxLogon doesn't work with Macbooks. For these Macbooks you can use NxMapper. Install and run it on your domain controller.
   And then you want to deal with these mobile workers. You can install NxClient on their laptops. NxClient is basically a remote filtering agent for NxFilter but they will try to do single sign-on when they are in a local Active Directory. There are Windows and Mac versions for NxClient.
   For Chromebook, you can try NxBlock. It is a Chrome extension and you can use it as a remote filtering agent or single sign-on agent for Active Directory.
   For your servers you'd better not to filter them and set them up with static IP addresses and use another DNS server for them or put them under a policy allowing everything. You don't need to block anything from them normally.
   For your iPhone and Android phones, just let them go through NxFilter's login-page.
