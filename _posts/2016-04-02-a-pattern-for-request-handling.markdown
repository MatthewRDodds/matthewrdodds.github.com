---
layout: post
title:  "Handling Api Requests in Rails"
date:   2016-04-02 21:42:17 +0000
categories: rails
desc: A pattern of handling API requests in rails
keywords: rails, patterns, web, internet, ruby, design, object oriented design
---
Recently I've been working on a few applications that use rails for their backend API, which is consumed by javascript based frontends.

The challenge I've encountered with building API controllers is handling the web of conditional logic that determines whether or not a request is successful, and also how to return a helpful API response reflecting the disposition of the request.

In dealing with this I've noticed a pattern emerge in my code, and it seems to help a lot in my projects in simplifying all of these concerns.

The handler class is very specifically designed to handle a request and only ever be used in an API controller context. This is in contrast to service objects which are much more flexible. The handler has specific logic for responding to requests that make it disadvantageous for other contexts (handling of status codes for example).

I've built a project to demonstrate all of this, available on [github](https://github.com/MatthewRDodds/request-handler-demo). (All of the following code samples are pulled from this repo.)

An instance of ApiController implemented using a handler class looks very clean and simple, the only conditional logic it cares about is whether or not the request was ultimately successful.

{% highlight ruby linenos %}
class Api::CheckOutsController < ApiController
  def create
    handler = CheckOutHandler.new(params: check_out_params)

    if handler.create
      render json: handler.check_out, serializer: CheckOutSerializer,
        status: handler.status
    else
      render json: { error: handler.error }, status: handler.status
    end
  end

  private

  def check_out_params
    params.require(:check_out).permit(:book_id, :user_id)
  end
end
{% endhighlight %}

The parent handler class that `CheckOutHandler` inherits from contains some abstracted concerns of all handler classes, such as converting symbols to status codes and formatting errors for invalid models to be returned in the response.

The `CheckOutHandler` class itself, in this case, takes the params provided by the controller and sets them on the model. The `create` method called from the controller begins by checking if the model is valid in a guard clause, and then tries to save the model.

{% highlight ruby linenos %}
class CheckOutHandler < Handler
  attr_reader :params, :check_out

  def initialize(args)
    @params = args[:params]
    @check_out = CheckOut.new(params)

    super
  end

  def create
    return if record_invalid?

    save
  end

  private

  def save
    check_out.save!
  rescue StandardError => ex
    @error = ex.message
    @status = status_for(:bad_request)

    return
  end

  def record_invalid?
    result = check_out.invalid?

    result.tap do |invalid|
      if invalid
        @error = error_message_for(check_out)
        @status = status_for(:bad_request)
      end
    end
  end
end
{% endhighlight %}

This is where I was seeing a lot of complexity in trying to do all of this from the controller. I wanted to return responses appropriate for the error encountered. So with this pattern, that is simply a matter of setting the error message and status code from the guard clause method. In this was `create` will return false and render json with the error and status set in handler.

I have a lot of handlers with `update` methods that check `record_not_found?` and return 404 with a helpful not found message. And I have other handlers that check things very specific to the model as well.

I could see a future where the private methods in `CheckOutHandler` are abstracted out to the parent at some point. But I want to note that while what happens in the `begin` block here seems pretty stupid and generic, it is only a simple example.

It is completely imaginable to have a complex action like performing some kind of transaction, which could have a dozen or more guard methods with all kinds of request dispositions. I haven't written anything that complex with this pattern yet but I think it would help manage that sort of logic.

**Potential Concerns**

There are a couple concerns I have with this pattern, even though on the whole I really like it.

One is that it's a little more awkward to test than a typical service object. I usually throroughly test the controller for all edge cases and leave the handler class minimally tested and consider it more as an implementation detail.

That's not to say it couldn't be thoroughly tested. But tests would end up checking error messages and response statuses, which I think is more naturally suited for controller testing. Given RESTful structuring of resources, a handler should really always correspond to only one controller, so I don't see this as too great of a code smell.


Please comment with any constructive feedback, would love to hear thoughts on this idea as well as suggestions for improvement.
