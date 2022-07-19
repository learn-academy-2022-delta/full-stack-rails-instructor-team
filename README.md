
## Params
Parameters are content added to the url. It is a way of passing in information to the controller method.

# Hard Coded Tacos

Create a instance variable with a hard coded value

    def tacos
    @my_taco = 'zofritas'
    end

Create the view called tacos.html.erb
<h1> Hey it Taco Tuesday!  We like Tacos!</h1>


<h2> I like <%= @my_taco %> tacos!!!</h2>

Create the route

get '/tacos' => 'home#tacos'

The browser will render our data.

# Tacos as Params
Create a instance variable that looks for a value from params
    def tacos
    @my_taco = params[:my_taco]
    end

Pass params to the url by assigning my_taco to a value

http://localhost:3000/tacos?my_taco=fish

The browser will render our data.

# Tacos as Params with Routes
Update the route to expect a param

get '/tacos/:my_taco' => 'home#tacos'

http://localhost:3000/tacos/fish

The browser will render our data.

# Multiple Params
Create two instance variables that looks for values from params

  def how_many
        @your_tacos = params[:your_tacos]
        @my_tacos = params[:my_tacos]
        if @your_tacos.to_i < @my_tacos.to_i
            @result = "I WIN!!!"
        else
            @result = "You WIN!!!"
        end    
    end
Create a view how_many.html.erb



Create a route that expects two params
  get '/how_many/:your_tacos/:my_tacos' => 'home#how_many'

In the browser pass two params
http://localhost:3000/my_tacos/8/3

Parameters are a hash, we can see how they are stored in the Rails log in the terminal:

Processing by HomeController#how_many as HTML

Can perform logic on the instance variables

 def how_many
    @your_tacos = params[:your_tacos]
    @my_tacos = params[:my_tacos]   
 end

Update the view

<h1>How many tacos do you have??</h1>
#  we use ERB to display the value passed in the params from the URL
    <h3> You have <%= @your_tacos %> tacos!! </h3>
    <h3> I have <%= @my_tacos %> tacos!! </h3>
    
    <h1><%= @result %></h1>


<!-- //// -->
# files

routes.rb

Rails.application.routes.draw do
  get '/tacos/:my_taco' => 'home#tacos'
  get '/how_many/:your_tacos/:my_tacos' => 'home#how_many'
end


home_controller.rb

class HomeController < ApplicationController

   def tacos
    @my_taco = params[:my_taco]
   end

    def how_many
        @your_tacos = params[:your_tacos]
        @my_tacos = params[:my_tacos]
        # we write a conditional to determine who has more and output the result 
        if @your_tacos.to_i < @my_tacos.to_i
            @result = "I WIN!!!"
        else
            @result = "You WIN!!!"
        end    
    end
end
