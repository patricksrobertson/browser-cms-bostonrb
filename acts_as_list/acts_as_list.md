!SLIDE smbullets
## What's wrong with ActsAsList? ##

* Naive implementation of ordering
* No chain-able scope support
* Encourages Non-RESTful actions

!SLIDE

# Naive ordering #

    @@@ ruby
    100.times do |counter|
      Issue.create!(:name => "issue-#{counter}")
    end
    
    # Update every single issue record.
    Issue.first.move_to_bottom

!SLIDE smbullets
    
# No Chain-able Support #

* Scoping only possible with has many / belongs to relationship.
* Library was built around Rails 1.0.
* Actively under development.

!SLIDE smaller

# Encourages Non-RESTful actions #
### View ###
    @@@ javascript
      // Implementation of a JQuery UI sortable move to top button.
      $("#sortable a.top").bind('click', function() {
        var idToMove = $(this).attr("id");
        var updateUrl = '/issues/' + idToMove + '/move_to_top'
        $.ajax({
          type: 'PUT', 
          url: updateUrl, 
          data: {}
        });
        // update sortable positions!
      });
### Controller ###
    @@@ ruby
    class IssuesController < ApplicationController
      def move_to_top
        @issue = Issue.find(param[:id])
        @issue.move_to_top
      end