!SLIDE 
# Enter Ranked Model #

!SLIDE 
# Usage #

    @@@ ruby
      class Issue < ActiveRecord::Base
    
        include RankedModel
      
        # must have integer column row_order!
        ranks :row_order
      end

!SLIDE smbullets

# Selling Points #

* Uses large integer range for ordering
* Models can contain multiple ordering columns for scopes
* Encourages use of 'update' action

!SLIDE small
# Smarter Ordering #

    @@@ ruby
      100.times do |counter|
        Issue.create!(:name => "issue-#{counter}")
      end

      # Changes first from -65353 (or so) to 53423 (or so) 
      # only one record is updated
      Issue.first.row_order_position = :last
    
!SLIDE small
    
# Multiple Scopes 

    @@@ ruby
      class Issue < ActiveRecord::Base
        
        scope :pending, where(:state => "pending")
        ranks :pending_order, :scope => :pending
      end
      
      class IssuesController < ApplicationController
        def index
          @all_items = Issue.rank(:row_order)
          @pending_items = Issue.pending.rank(:pending)
        end
      end
      
!SLIDE smaller

# Encourages use of 'update' #
### View ###
    @@@ javascript
      // Implementation of a JQuery UI sortable move to top button.
      $("#sortable a.top").bind('click', function() {
        var idToMove = $(this).attr("id");
        var updateUrl = '/issues/' + idToMove
        $.ajax({
          type: 'PUT', 
          url: updateUrl, 
          data: { issue: {row_order_position: "first"}}
        });
        // update sortable positions!
      });
      
### Controller ###
    @@@ ruby
      class IssuesController < ApplicationController
        def update
          @issue = Issue.find(params[:id])
          
          if @issue.update_attributes(params[:issue])
            flash[:notice] = "I'm a standard controller action!"
          end
        end
      end
!SLIDE smbullets
# Gotchas #

* Zero-based (works fine for JQueryUI Sortable).
* No Sane ordering default.
* Very new.
