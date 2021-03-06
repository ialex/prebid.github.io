---
layout: page
title: Getting Started
head_title: Getting Started with Prebid.js for Header Bidding
description: An overview of Prebid.js, how it works, basic templates and examples, and more.
pid: 0
isNavDropdown: false
isNavParent: true


---



<div class="bs-docs-section" markdown="1">

#Live Demo

{% include live_demo.html %}

#### The above ad is auctioned with Prebid.js.

* **Hover over** the timeline bars to discover how long each bidder takes.
* Ad server is set to only wait for **up to 400ms**. If all bidders respond faster than that, Prebid.js will load the ad server early. If not, Prebid.js will ignore bidders that took too long. 
* You may notice Javascript cannot initiate all bidder calls at once. To prevent bidders that get installed last to always have less time to respond, Prebid.js helps you keep the auction fair and rotate the order that bidders get called.



</div>

<div class="bs-docs-section" markdown="1">

#Overview

###What is Prebid.js?

> Prebid.js is an open source Javascript framework to help publishers integrate and manage header bidding partners without writing custom code or increasing page load times. Prebid.js is 100% open source and free for anyone to use. 

* It has clean, built-in support for all major bidders (AppNexus, Rubicon, etc), as well as major ad servers (DFP, OAS, AdTech). 
* Prebid.js has solved many known problems publishers are facing - high latency, unfair auction mechanics, long development time, confusing line item and targeting setup.
* Plugging in prebid.js is easy. Adding new header bidding bidders is a matter of adding tag Ids into a JSON config.

<br>

<a name="basic-example">

###Basic Example
Here’s a basic example for Rubicon and AppNexus bidding into a DFP ad unit:

#####1. Register bidder tag Ids

In a simple JSON config, define a mapping of the bidders’ tag Ids to your ad units. Then load prebid.js library async. Call `pbjs.requestBids()` to send header bidding requests async to all bidders you've specified.

{% highlight js %}

// Load prebid.js library async.

pbjs.que.push(function() {
  var adUnits = [{
    code: "/1996833/slot-1",
    sizes: [[300, 250], [728, 90]],
    bids: [{
        bidder: "rubicon",
        params: {
            rp_account: "4934",
            rp_site: "13945",
            rp_zonesize: "23948-15"
        }
    }, {
        bidder: "appnexus",
        params: { placementId: "234235" }
    }]
  }];
  pbjs.addAdUnits(adUnits);

  pbjs.requestBids({
    bidsBackHandler: function() {
        // callback when requested bids are all back
    };
  });

});

{% endhighlight %}


#####2. Ad server waits for bids

Define the timeout to let your ad server wait for a few hundred milliseconds, so the bidders can respond with bids.

{% highlight js %}

PREBID_TIMEOUT = 300;
function initAdserver() {
    (function() {
        // To load GPT Library Async
    })();
    pbjs.initAdserverSet = true;
};
setTimeout(initAdserver, PREBID_TIMEOUT);

{% endhighlight %}



#####3. Set targeting for bids

Call the helper function `setTargetingForGPTAsync()` to handle all the targeting for all bidders. 

{% highlight js %}

pbjs.que.push(function() {
  pbjs.setTargetingForGPTAsync();
});

{% endhighlight %}

For detailed walkthrough and API references, check out the [Publisher API docs](publisher-api.html).

<br>

<a name="how-works">

###How does it work?
> Prebid.js sends bid requests to partners asynchronously and manages timeouts to keep page load times fast.

![Prebid Diagram Image]({{ site.github.url }}/assets/images/prebid-diagram.png)


<!--

<br> 

###Prebid.js is designed modularly
> Prebid.js exposes three API’s - a Publisher API used to request ads, a Bidder API used for Bidders to respond to ad requests, and an Ad Server API used to integrate with ad servers.

* **Publisher API**

	If you're a publisher, this is the main API you'll be using. You have already seen the skeleton in the above [How does it work](#how-works) and [Basic Example](#basic-example). You'll use the API to define the bidders' tag IDs, let your ad server wait for a certain amount of time and let bidders respond with bids, then set targeting on your ad units before sending the impressions to the ad server.

* **Bidder API**

	Prebid.js supports all major header bidding bidders out of the box. We used the same API to implement all the bidder integrations. If you'd like to add a new bidder into the framework, or just to study how it works, refer to [Bidder API Docs](adaptors.html).

* **Ad Server API**: 

	Prebid.js comes with support for most major ad servers. If you'd like to implement a custom ad server, or to add a new ad server into the list, refer to [Ad Server API Docs](adaptors.html).

-->

</div>



<div class="bs-docs-section" markdown="1">


#Download

<p class="lead">
Prebid.js is under rapid development. Get the latest version and stay in touch:
</p>

<div class="form-horizontal">
  
  <div class="form-group">
    <label class="col-sm-2 col-xs-6 control-label">Email</label>
    <div class="col-sm-4 col-xs-8">
      <input class="form-control" placeholder="Email" id="email-field" required>
    </div>
    <div class="col-sm-4 col-xs-4">
      <button class="btn btn-outline" id="submit-email" onclick="submitEmail()">Get Latest</button>
    </div>
  </div>
</div>

<div class="row bs-downloads">
    <div class="col-sm-12">
      <h3 id="download-bootstrap">Compiled and Minified</h3>
      <p>Compiled and minified JavaScript with example files. No docs or original source files are included.</p>
      <p>
        <a href="{{site.downloadUrl}}" class="btn btn-lg btn-default" onclick="ga('send', 'event', 'Getting started', 'Download', 'Download compiled');">Download Prebid.js</a>
      </p>
    </div>

  </div>

</div>

