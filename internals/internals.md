!SLIDE 

# BrowserCMS Internals #

!SLIDE 

# Model Layer #

### The term is "Content Block" ###

    @@@ruby
    class Waffle < ActiveRecord::Base
    
      acts_as_content_block
      
    end

!SLIDE smbullets
# You have access to the full AR API #

* Validations
* Callbacks
* Relationships

!SLIDE 
# But... #

    @@@ruby
    #doesn't do what you'd want it to do.
    Waffles.create!(:name => "Belgium")
    
    #instead do this
    Waffles.publish!(:name => "Belgium")

!SLIDE smaller 
    
# You can only have one attachment #
## Must be named attachment ##
## Override it's default location ##

    @@@ruby 
    #The default generator is broken, instead of this
    acts_as_content_block
    belongs_to_attachment
    
    #Do this 
    acts_as_content_block :belongs_to_attachment => true
    
!SLIDE
# Controller Layer #

### The term is "Portlet" ###



!SLIDE smbullets
# Portlets #

* Allow you to query for Content Blocks or Rails models.
* Can have a view template stored via file or database
* Gives you "Dynamic Attributes"

!SLIDE small

## Portlet Implementation ##

    @@@ ruby 
    class RandomEmployee < Portlet
      #allows you to edit via administrative panel
      enable_template_editor true
      
      def render
        @employee = Employee.first(:order => "RANDOM()")
      end
    end
    
!SLIDE
# View Layer #

!SLIDE small
## Layouts containing content ##
    <!-- Create the CMS toolbar -->
    <%= cms_toolbar %>
    <div class="wrapper">
      <%= container :main %>
    </div>
    
## Dynamically generated menus ##

    <!-- Top Level Nav -->
    <%= render_menu :from_top => 0, :depth => 1 %>
    
## Breadcrumbs ##

    <%= render_breadcrumbs %>
    
!SLIDE small
# Views for Content Blocks #
## There is only one way to render a Content Block by default ##
### Can be overriden with portlets or slightly offensive view logic ###
### I would love a view_path override. ###
## There is also a form that you can customize ##

!SLIDE 
# What Makes BrowserCMS special? #

!SLIDE 
## The Rails CMS implementation problem: solved! ##

!SLIDE smbullets
# Gotchas #

* Requires separate authentication
* Be careful in config/routes.rb
* Is fairly opinionated on production deployment
* Consider CopyCopter instead!