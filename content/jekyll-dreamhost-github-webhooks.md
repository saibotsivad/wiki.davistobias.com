# setup jekyll and github webhook on dreamhost

The dreamhost PHP server doesn't come with a version of Ruby that will let you run [Jekyll](jekyllrb.com),
so you need to install Ruby manually.

## install ruby

Install `rvm` (the [Ruby version manager](https://rvm.io/)) using the command (check the website for
current command):

	gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

	\curl -sSL https://get.rvm.io | bash -s stable

I received two warnings. The first one looked like this:

	* WARNING: You have '~/.profile' file, you might want to load it,
	to do that add the following line to '/home/username/.bash_profile':

	  source ~/.profile

This is simple enough to do, with this one-liner:

	echo "source ~/.profile" >> ~/.bash_profile

(The double angle-brackets `>>` append the text to the file.)

The second warning looked like this:

	* WARNING: you have GEM_HOME="/home/websites1982349/.gems" this is conflicting with RVM, make sure to:

	  unset GEM_HOME

And, as far as I can tell so far, can be ignored.

See what the latest version of [Ruby](https://www.ruby-lang.org/en/downloads/) is, then install, e.g.:

	rvm install 2.2.3

Set that version as the default:

	rvm use 1.9.2 --default

Make sure that worked, by testing which version of Ruby you've got:

	ruby -v

This should tell you something like this:

	ruby 2.2.3p173 (2015-08-18 revision 51636) [x86_64-linux]

## install jekyll

Then install Jekyll like this (see [the website](http://jekyllrb.com/) for current instructions):

	gem install jekyll

This may take several minutes.

Dreamhost doesn't run Node, so it needs a JavaScript runtime to handle some things, and instead of
trying to install Node, you can install [therubyracer](https://github.com/cowboyd/therubyracer).

	gem install therubyracer

Finally, verify everything installed by going to a Jekyll folder and running:

	jekyll build

## setup php file for webhook

We want to setup a webhook on Github, so that when things get merged into the master branch, the
server will grab the latest and greatest, and update it.

Opinions no doubt vary on how to do this, but the main idea is this:

* When the webhook fires, it hits the server that serves the site
* The server downloads the latest from Github into a temporary folder
* The server runs `jekyll build` to build the site
* The server renames the existing site to `site.old` and the temp folder to `site`
* The server then deletes the old folder

In this way, the updated site is built on the server, but the files are unavailable
for a bare minimum amount of time.

Here is how I accomplish this:

Make a PHP file, and then make it executable (`chmod +x`):

	touch update.php && chmod +x update.php

Then paste this inside it:

	$FOLDER  = "site.com";
	$ROOT    = "/home/username";
	$REPO    = "https://github.com/username/repo.git";
	$BRANCH  = "master";
	if ( $_POST['payload'] ) {
		shell_exec("cd {$ROOT} && git clone --depth=1 -b {$BRANCH} {$REPO} {$FOLDER}-build");
		shell_exec("cd {$ROOT}/{$FOLDER}-build && jekyll build");
		shell_exec("mv {$ROOT}/{$FOLDER} {$ROOT}/{$FOLDER}-old && mv {$ROOT}/{$FOLDER}-build {$ROOT}/{$FOLDER}");
		shell_exec("rm -rf {$ROOT}/{$FOLDER}-old");
	    die("done " . mktime());
	  }
	}

This will clone only the latest version (`--depth=1`) of the repo.

If you run `git --version` and it's `1.8.x` or higher, you can use this command, which will only check out
one branch (it'll be a little faster, if you've got multiple branches):

	git clone --depth=1 -b {$BRANCH} --single-branch {$REPO} {$FOLDER}-build

(Note: If you've got a lot of large files, that method will be a bit slow. You'll want to change
your approach to do a hard reset, then git fetch and rebase, then build. Message me if you get stuck.)

You'll want this file to run on the same server, but not under the same domain, since you'll
probably be deleting that domain when you run this. I recommend making some other subdomain,
such as `github-updater.site.com` and only using it to run the webhooks.

Inside the Github repo, under "Settings > Webhooks & services", add a new webhook with the
content type as `application/x-www-form-urlencoded` to the appropriate URL.

