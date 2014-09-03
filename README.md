#UCSF Utility Scripts

The Utitlity Scripts are primaryly useful if you are on Acquia Cloud hosting. Posting on Github so that other Acquia clients can use and collaborate on the scripts. These are provided as is with no support. That being said, we are happy to collaborate with other groups, particularly other Higher Ed and Non-profits.

###Iterator:

This is a server-side script that needs to be executed from within your `/docroot` directory.

Iterator Script runs through drupal sites and runs drush based on file added to "deploy folder". Can also be run via command line.

####Syntax
<pre>
Drush command|target module
</pre>

####Example file command:
<pre>
updb|chosen
cc all|ucsf_images_gallery
</pre>

The first would run a update on all sites with chosen module enabled.<br>
The second would run status on all sites with the ucsf pharmacy image module.

This script is a workhorse for us. We use this with post deploy scripts that have the git date tag.<br> Example
<pre>
2014-09-02
</pre>

This means that the same drush commands run in test and production along with the deployment of the git tag.

That's a Good Thing!

####Installation

Add the `iterator` script to the `/scripts` directory underneath your repository root.

####Running Iterator Manually

Execute iterator from within your `/docroot` whilst providing it with the path to your commands script and the indicator of the environment you're operating in.

For example, if you want to execute the Drush commands defined in `/deploy/2014-09-02` directory in your *production server` run this from withing `/docroot`.

```bash
./../scripts/iterator file ./../deploy/2014-09-02 prod
```

Alternatively, you may give iterator a single (piped) Drush command (see syntax described above) directly, instead of a file path. Use `run` as the second argument, followed by the Drush command in quotes.

E.g. this will clear all caches on sites in the *test* environment that have the Views module enabled.

```bash
./../scripts/iterator run "cc all|views" test
```

###Module Madness:

Module Madness is a reporting script. It let's you know which site is running which module. Useful when managing 500+ sites!

####Dependencies

Piggy-backs on the Iterator script and requires the custom Drush commands defined in `ucsf.drush.inc`, so make sure that Drush can find them.

###Site Builder:

This script uses the Acquia API and git to quickly build empty site document roots based on an orginal site called mysite.ucsf.edu

###Sync files: 

This script allow for more fine grained file updates between sites than the current Acquia workflow tool. Very useful when migrating a new site from Dev to Test and then Produciton.
