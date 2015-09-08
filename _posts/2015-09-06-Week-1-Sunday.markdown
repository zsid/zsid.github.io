---
layout: post
title: "Week 1, Sunday"
date: 2015-09-06 20:03:43
---

Reflecting on my plan from yesterday, looks like today hasn't gone as expected. I have spent the whole day refactoring my code and adding additional features to my airport. For example,
any number of planes can now land and take off.

The code of the day is (my airport keeps track of planes in an array):

    def plane_took_off(*plane)
        plane.each { |plane| plane.take_off }
        planes.delete_if { |plane| plane.flying }
    end

It took ages to figure it out how to test it. Finally:

    it two planes can take off at the same time' do
            plane = double :plane
            plane2 = double :plane2
            allow(subject).to receive(:weather_stormy?) {false}
            allow(plane).to receive(:landing)
            allow(plane2).to receive(:landing)
            subject.permission_to_land(plane, plane2)
            allow(plane).to receive(:take_off)
            allow(plane2).to receive(:take_off)
            allow(plane).to receive(:flying).and_return(true)
            allow(plane2).to receive(:flying).and_return(true)
            subject.permission_to_take_off(plane, plane2)
            expect(subject.planes).to be_empty
          end
    end

There is definitely a way to make it shorter but I haven't figred it out yet. This is all for today.

Good night.

__Zhivko__

PS: sorry, the code is not very readable, I will try to fix it tomorrow.
