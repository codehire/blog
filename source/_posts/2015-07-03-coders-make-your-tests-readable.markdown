---
layout: post

cover: /images/cross-eyed-cat.jpg
comments: true
author: Dan Draper
categories: [Coding, Best Practices]
---

_When you’ve been coding as long as I have you see a lot of terrible code. The rule that so many coders completely forget? Make your code readable! And for some reason the last place coders tend to put in effort into readability is in their tests._

> I’ve wasted many a day trawling through hopelessly unreadable, unstable tests only to find that the test broke because of a typo

## Why are readable tests important?

If an app has tests (which it almost always should), they can be a huge insight into the behaviour of your application. Particularly in cases of complex logic or obscure requirements.

I recently had the privilege of working with a client on a large, complex government application. The requirement was to implement some very sophisticated business logic using a Ruby on Rails application. The project also involved a great deal of obscure domain specific language (aka jargon).

The project, while successful got to the stage where only one of the developers was the only one really across huge sections of the app. He was a brilliant developer but his tests were poorly written. No one could make sense of them and so when something broke this developer was usually the only person who could fix them!

Let's look at the following code:

<pre>
  <code class="ruby">
    describe "show" do
      it "should use FooSerializer to serialize if the logged in user is the same as params user" do
        user = FactoryGirl.create(:user)
        controller.stub(:current_user).and_return(user)
        FooSerializer.any_instance.should_receive(:to_json).and_return("{\"key\": \"value\"")
        get :show, :id => user.id
        response.should be_success
      end
    end
  </code>
</pre>

Can you work out what is happening? How long did it take you? Are you having suicidal thoughts now?

In this example we are using Ruby's RSpec so we could create a custom matcher and do the following:

<pre>
  <code class="ruby">
    describe "show" do
      before { get :show, id: user.id }

      it 'serializes the response' do
        expect(response).to serialize_object(user).with(FooSerializer)
      end
    end
  </code>
</pre>

A bit easier to get your head around now? The custom matcher can be reused many times now and would be defined as follows:

<pre>
  <code class="ruby">
    RSpec::Matchers.define :serialize_object do |object|
      match do |response|
        @serializer_klass.new(object).to_json == response.body
      end

      chain :with do |serializer_klass|
        @serializer_klass = serializer_klass
      end
    end
  </code>
</pre>

## Working in a team

When we work in a team (or even when writing open source software that will be used by the public), there _must_ be an emphasis placed on readability. On average, your code will be read by 7 other people so they need to be able to understand it.

> On average, your code will be read by 7 other people

## Making fixing tests bearable

I’ve never met anyone who likes fixing broken tests but if tests are highly readable and well structured the process can be made bearable. I’ve wasted many a day trawling through hopelessly unreadable, unstable tests only to find that the test broke because of a typo. Save yourself this heartache and write good, readable tests!



_Codehire Learning runs professional [workshops on mastering testing with RSpec for Ruby](https://codehire.com/learn/courses/rspec-mastery)._



