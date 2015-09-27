---
layout: post
title: "Week 4, Sunday"
date: 2015-09-27 22:01:22
---
Today hasn't been as productive as yesterday. One of the things that I have struggled with was how to display the time of my chitter post. I have found a very helpful [blog post](http://blog.runbikeco.de/blog/2014/02/27/datamapper-datetime-fields-with-default/) on how to create a time fields in DataMapper - it was a life-saver. Alas, the problem came at writing a test and displaying the time stamp.

So my `Peep` class is:

    class Peep
      include DataMapper::Resource

      property :id,   Serial
      property :time, DateTime, :default => lambda{ |p,s| DateTime.now}
      property :peep, String, length: 1..140

      attr_reader :peep
      attr_reader :time

      belongs_to :user

    end

After some time I have realised that I could use the method `strftime` on the DateTime info from DataMapper. Not only this but I can also use it in Rspec. Nice! So my test shaped as:

    scenario "I can see the name and username of the creator, the peep and the date it was posted" do
      sign_in(user: user.username, password: user.password)
      create_peep(text: "I can see you")
      expect(page).to have_content "Name: #{user.name}"
      expect(page).to have_content "Username: #{user.username}"
      expect(page).to have_content "#{Time.now.strftime("%H:%M %d/%m/%Y")}"
      expect(page).to have_content "I can see you"
    end

And then the code in my view was easy to replicate, displaying my `peep` with the most recent on top:

    <% @peeps.reverse.each do |peep| %>
      <li> Name: <%= User.get(peep.user_id).name %>, Username: <%= User.get(peep.user_id).username %><br />
      Date: <%=  peep.time.strftime("%H:%M %d/%m/%Y") %> <br />
      Peep: <%= peep.peep %>
      </li>
    <% end %>

It isn't rocket science but hey every little helps.

Good night.

__Zhivko__
