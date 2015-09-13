---
layout: post
title: "Week 2, Sunday, Ruby Gems"
date: 2015-09-13 20:16:55
---
It's been a long day today. I have finally managed to get my Takeaway Restaurant to send me text messages, confirming my order. But never mind, I still haven't done a blog post on __'Ruby Gems'__ so here it is.

You can think of a gem as a library or plug-in which we will use to fulfill a specific need that we don’t currently have and it’s really useful as we don’t need to reinvent the wheel.

We now know what a gem is, the next step is to install one. Are gems easy to install? Well, it’s pretty simple, the hard part is finding the gem which will solve our problem.

    Gem install GEM_NAME

Ruby gems also have documentations and it’s essential to familiarise ourselves with it. There may be some parameters which we should add to the above command but in most cases this should be enough. A thing to keep in mind is that a gem’s documentation tells us to use sudo when installing it. If you’re on a Mac and use RVM (as you should be :) ), just leave sudo off. Using it will install the gem for all users on the computer, and it can cause problems with the multiple Ruby environments you might have with RVM.

Once, we have installed the gem, we will need to ‘require’ it.

    require 'twilio-ruby'


We have now required the gem in our file and we can start using its functionality. In the example below, I have used twilio in my Takeaway challenge to send me a text message once  the order has been completed. It’s really amazing and I didn’t have to write the functionality. PHEW!

    require 'twilio-ruby'

    class Restaurant
      include Menu

      def initialize
        @name = 'Bella'
      end

      def take_away
        delivery = Time.now + 3600
        delivery_time = delivery.strftime("%H:%M")

         @client = Twilio::REST::Client.new ENV['ACCOUNT_SID'], ENV['AUTH_TOKEN']

         message = @client.account.messages.create(
           :from => ENV['TWILIO_NUM'],
           :to => ENV['NUM'],
           :body => "Thank you! Your order was placed and will be delivered before #{delivery_time}."
         )
      end
    end

####__Dangers__

The danger of using ruby gems is that we are relaying on someone else’s code rather  than our own and trading control for convenience. Sometimes this trade works out splendidly, but other times just call the ambulance. Other pitfalls are:

* One of our goals as developers is to achieve mastery over our tools – programming languages. This means understanding how the various components work in our software and relaying too heavily on functionality packed into others’ gems is pretty much relaying on magic.

* It is not uncommon to find violations of SOLID principles when using gems and quality documentation is also a rarity.

* If a gem we are using has a new version with features which we will want to have, we cannot always just upgrade it as gems frequently rely on other gems, and those dependencies may clash.

__Zhivko__
