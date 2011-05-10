!SLIDE
# Vagrant #
[![Vagrant](vagrant_chilling.png)](http://vagrantup.com)

!SLIDE
# Ruby Development Environments Suck #

!SLIDE center
[![Dependencies](dependency_hell.jpeg)](http://www.flickr.com/photos/22392855@N08/5502369843/)
# Dependency Hell #

!SLIDE smbullets
## Dependency Hell ##

* Ruby
* Ruby Libraries (Gems)
* External Libraries (Search, Persistence, HTTP servers)

!SLIDE center
[![C Extensions](c.jpeg)](http://www.flickr.com/photos/lwr/101292696/)
# C Extensions #

!SLIDE center
[![Fix It](fix.jpeg)](http://www.flickr.com/photos/papemartin/2759839958/)
# We can fix it #

!SLIDE smbullets

# Vagrant #

* Ruby Wrapper for Virtual Box
* Easy to Provision
* Easy to Distribute
* Relatively Transparent

!SLIDE smbullets

## On your local machine ##

* Use of your text editor of choice
* Use of your SCM tools of choice
* Forwarded port to your browser
* SSH tunnel into the virtual machine

## On the Vagrant Machine ##

* Full webstack installed / running
* Tailored to mirror production.

!SLIDE smbullets center

## Gotchas ##

[![Gotchas](gotcha.jpeg)](http://www.flickr.com/photos/katerha/5036106702/)

* Difficult for Ruby IDE's.
* nginx is a little funny with symlinks.