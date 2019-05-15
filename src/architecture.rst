
WebJive Architecture
####################

WebJive is composed of four projects: 

#. **webjive**  .. _link: https://gitlab.com/MaxIV/webjive

#. **WebJive Dashboards**  .. _link: https://gitlab.com/MaxIV/dashboard-repo

#. **WebJive Auth**  .. _link: https://gitlab.com/MaxIV/webjive-auth

#. **web-maxiv-tangogql**  .. _link: https://gitlab.com/MaxIV/web-maxiv-tangogql

In the diagram above, an overview of WebJive architecture has been shown. 

\ |IMG1|\ 

#. *WebJive Architecture diagram* 

\ |STYLE5|\  is a \ |LINK5|\  client that permits to explore Tango devices and to create custom dashboards, using a collection of widgets. webjive accesses to the Tango Control Framework through \ |STYLE6|\ . The communication between webjive and tangogql is managed by a library into webjive. \ |STYLE7|\  is a \ |LINK6|\  interface for Tango.

In order to sends command and save dashboards, it is necessary to login to the system. webjive uses \ |STYLE8|\  to manage users. \ |STYLE9|\  accesses to LDAP repository or JSON file to retrieve user information. 

The dashboards created by the user logged in the system, are stored in a \ |LINK7|\  database through \ |STYLE10|\  application. 


.. bottom of content


.. |STYLE4| replace:: *WebJive Architecture diagram*

.. |STYLE5| replace:: **webjive**

.. |STYLE6| replace:: **tangogql**

.. |STYLE7| replace:: **tangogql**

.. |STYLE8| replace:: **webjive-auth**

.. |STYLE9| replace:: **webjive-auth**

.. |STYLE10| replace:: **dashboard-repo**





.. |LINK5| raw:: html

    <a href="https://reactjs.org/" target="_blank">react</a>

.. |LINK6| raw:: html

    <a href="https://graphql.org/" target="_blank">GraphQL</a>

.. |LINK7| raw:: html

    <a href="https://www.mongodb.com/" target="_blank">MongoDB</a>


.. |IMG1| image:: static/WebJive_Architecure_1.png
   :height: 310 px
   :width: 596 px
   :target: https://www.draw.io/?page-id=EoXmubeZtLr9LTINJ_n0&scale=auto#G1C2NcH695GHxfXjRBXC3uMcAOVl3pXdno
