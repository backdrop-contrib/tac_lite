OVERVIEW
--------

Tac_lite stands for Taxonomy Access Control Lite.  This module
restricts access so that some users may see content that is
hidden from others.  A simple scheme based on taxonomy, roles and
users controls which content is hidden.

As the name implies, this module shares some functionality with an
earlier module called Taxonomy Access Control (TAC).  If you are
shopping around for an access control module to use, consider that one
as you may find that it suits your needs.  In my case, I wanted access
control but without some of the complexity introduced by TAC.  I also
wanted more flexibility in granting access on a per user basis.

Here are some key features of tac_lite:

* Designed to be as simple as possible in installation and administration.  

* Leverages Drupal's node_access table, db_rewrite_sql hook and
  taxonomy module to leave the smallest possible footprint while doing
  it's job.  For example, it introduces no new database tables.

* Grant permissions based on roles.

* Grant permissions per user.  (Give a specific user access beyond
  what his/her roles allow).

USE CASE
--------

Here's how I originally used this module.  This description might make
it easier to understand why one might prefer tac_lite over TAC.

My website helps me manage my work projects.  I use Drupal's project
module to track issues.  Some of my projects are for the public to see
(i.e. Drupal modules) others are limited to my clients and partners.
These restricted projects should be visible only to me, the client in
question, and partner(s) working on that particular project.

I've defined a vocabulary for my projects (same one used by
project.module) and I've defined a client role and a partner role.
Partners can contribute to the website, while clients can read content
but post only issues.

Using TAC (or as far as I know all other access control modules) I
would have to create a new role for each project/role combination.
That is, for the Acme project I'd have to create roles 'Acme Client'
and 'Acme Partner' in order to assign permissions just the way I want
them.

Using tac_lite, I simply associate each user with the project(s) they
are allowed to see.  That is, I associate some clients and some
partners with Acme.  Their role (client or partner) controls what they
can do, and the associations through tac_lite control what they can
see.

INSTALL
-------

For drupal 4.7.

Enable taxonomy module.  It's required.

Install this package the normal way.
- put this file in a subdirectory of the modules directory.
- enable using admin interface
- no database tables to install.


USAGE
-----

Log in as an administrator. (uid==1, or a user with
administer_tac_lite permission)

Create a vocabulary which you will use to categorize private nodes.
You may want to call this "Private Projects".

Associate the vocabulary with node types, as you would normally do.

Add several terms to that category.

Go to administer >> settings >> tac_lite.

Select the category you created in the earlier step ("Private Projects").

Create some content.  Choose a node type associated with "Private Projects".

Note that you can view the content you just created.  Other users cannot.

Edit the account of another user.  Go to the tac_lite access tab under edit.

Select a term you selected when creating the node and submit changes.

Now the user can also access the node you created.


IMPORTANT NOTE
--------------

If you have no access_control modules installed, when you first
install this module it will hide all existing content from most users
(except uid==1).  This has to do with the way Drupal's node_access
table works.  To make nodes visible, you have to re-save them
(i.e. edit the node and simply hit submit without changing anything).
This will cause the appropriate entries to be written to the
node_access table.  Of course, there should be a way to automate this
process.  Any volunteers?

RELATED MODULES
---------------

There is a sister module called cac_access which is nearly identical,
but uses the new Category module instead of the taxonomy module.  You
could theoretically install taxonomy, category, tac_lite and cac_lite
at the same time.  But you probably do not want to.

There is a sub-module of the devel module, called devel_node_access
which can give you some insight into the contents of your node_access
table.  Recommended for troubleshooting.


AUTHOR
------

Dave Cohen <http://drupal.org/user/18468>
