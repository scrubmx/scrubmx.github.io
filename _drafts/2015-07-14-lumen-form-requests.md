---
title: Lumen Form Requests
date: 2015-07-14 16:20:00
description: Adding the Form Requests functionality from Laravel to Lumen.
---

# The Problem <a name="the-problem" href="#the-problem">#</a>

Recently I was building a webservice so naturally I decided that Lumen seemed like a reasonable choice. Since it was built specifically for this kind of use-case. So I got to work and very quickly built a first pass at a simple  UserController class.

{% highlight php %}
public function postUser(Request $request)
{
    $validator = Validator::make($request->all(), [
        'name'  => 'required|string|max:255',
        'email' => 'required|string|email|max:255',
        'location' => 'sometimes|string|max:255'
    ]);

     if ($validator->fails()) {
        $this->logger->error($validator->messages()->toArray());

        return response($validator->messages(), 422);
    }


    // TODO: Some business logic...

    return response('Accepted', 202);
}
{% endhighlight %}

Seems simple enough right? However as you can imagine the validation rules can get more complex than this example. We are not handling authorization yet and we still haven't implemented the business logic, not to mention unit testing this method is a nightmare. I think we can all agree that this approach falls apart very quickly.

The first thing that comes to mind is getting the validation out of the controller and what better way than the awesome Laravel Form Requests, which are a special type of class devoted to validation and authorization. Unfortunately Lumen dosen't have this feature out of the box.

So I google a bit and found this [github issue]. and found out that there is no plan to implement this in Lumen. So I decided to build my own package.

# Lumen Form Requests <a name="lumen-form-requests" href="#lumen-form-requests">#</a>

So you can download the package from [packagist](https://packagist.org/) or simply: 

{% highlight shell %}
composer require intonate/lumen-form-requests
{% endhighlight %}


....

So going back to the first example.
{% highlight php %}
public function postUser(PostUserRequest $request)
{
    // TODO: Some business logic...

    return response('Accepted', 202);
}
{% endhighlight %}

As we can see this is much better and in fact unit testing this method is as easy as:
{% highlight php %}
public function testPostUserValidation()
{
    $this->post('v1/users', ['name' => 'John Doe'])
         ->seeStatusCode(422)
         ->seeJsonContains(['email' => ['The email field is required.']]);
}
{% endhighlight %}

[github issue]: https://github.com/laravel/lumen-framework/issues/124
