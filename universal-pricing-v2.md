---
author:       fl
created:      2017-05-11
publish:      published
title:        "Universal App pricing V2 is here"
excerpt:      "More powerful plans, same price level."
lead:         "The Universal Stack was launched 5 months ago. We are now implementing a frequent feedback: Meet our new more powerful Universal Stack plans:"
image:        old-new-pricing-poster.gif
imagecredit:  'After/Before slider shamelessly stolen from: https://codepen.io/bamf/pen/jEpxOX'
---

1. The old entry level plan is going away.
2. The old middle plan is becoming the new entry plan — same specs, lower price.
3. A new powerful top plan is introduced.




<!--  After/Before slider shamelessly stolen from: https://codepen.io/bamf/pen/jEpxOX -->

<style type="text/css">
    .ba-slider {
        position: relative;
        overflow: hidden;
        min-height: 400px;
        border: 1px solid black;
    }
    .ba-slider img {
        width: 100%;
        display:block;
        border: 0;
    }
    .resize {
        position: absolute;
        top:0;
        left: 0;
        height: 100%;
        width: 50%;
        overflow: hidden;
    }
    .handle { /* Thin line seperator */
      position:absolute; 
      left:50%;
      top:0;
      bottom:0;
      width:4px;
      margin-left:-2px;
      background: rgba(0,0,0,.5);
      cursor: ew-resize;
    }
     
    .handle:after {  /* Big orange knob  */
        position: absolute;
        top: 50%;
        width: 64px;
        height: 64px;
        margin: -32px 0 0 -32px;
        font-family: Arial !important;
        content:'↔';
        color:white;
        font-weight:bold;
        font-size:36px;
        text-align:center;
        line-height:64px;
     
        background: #00e6bf; 
        border:1px solid #118771; /* darken(@orange, 5%) */
        border-radius: 50%;
        transition:all 0.3s ease;
        box-shadow:
          0 2px 6px rgba(0,0,0,.3), 
          inset 0 2px 0 rgba(255,255,255,.5),
          inset 0 60px 50px -30px #21FFD8;
    }

    .draggable:after {
        width: 48px;
        height: 48px;
        margin: -24px 0 0 -24px;
        line-height:48px;
        font-size:30px;
    }
</style>


<script>
    // Call & init
$(document).ready(function(){
  $('.ba-slider').each(function(){
    var cur = $(this);
    // Adjust the slider
    var width = cur.width()+'px';
    cur.find('.resize img').css('width', width);
    // Bind dragging events
    drags(cur.find('.handle'), cur.find('.resize'), cur);
  });
});

// Update sliders on resize. 
// Because we all do this: i.imgur.com/YkbaV.gif
$(window).resize(function(){
  $('.ba-slider').each(function(){
    var cur = $(this);
    var width = cur.width()+'px';
    cur.find('.resize img').css('width', width);
  });
});

function drags(dragElement, resizeElement, container) {
    
  // Initialize the dragging event on mousedown.
  dragElement.on('mousedown touchstart', function(e) {
    
    dragElement.addClass('draggable');
    resizeElement.addClass('resizable');
    
    // Check if it's a mouse or touch event and pass along the correct value
    var startX = (e.pageX) ? e.pageX : e.originalEvent.touches[0].pageX;
    
    // Get the initial position
    var dragWidth = dragElement.outerWidth(),
        posX = dragElement.offset().left + dragWidth - startX,
        containerOffset = container.offset().left,
        containerWidth = container.outerWidth();
 
    // Set limits
    minLeft = containerOffset + 10;
    maxLeft = containerOffset + containerWidth - dragWidth - 10;
    
    // Calculate the dragging distance on mousemove.
    dragElement.parents().on("mousemove touchmove", function(e) {
        
      // Check if it's a mouse or touch event and pass along the correct value
      var moveX = (e.pageX) ? e.pageX : e.originalEvent.touches[0].pageX;
      
      leftValue = moveX + posX - dragWidth;
      
      // Prevent going off limits
      if ( leftValue < minLeft) {
        leftValue = minLeft;
      } else if (leftValue > maxLeft) {
        leftValue = maxLeft;
      }
      
      // Translate the handle's left value to masked divs width.
      widthValue = (leftValue + dragWidth/2 - containerOffset)*100/containerWidth+'%';
            
      // Set the new values for the slider and the handle. 
      // Bind mouseup events to stop dragging.
      $('.draggable').css('left', widthValue).on('mouseup touchend touchcancel', function () {
        $(this).removeClass('draggable');
        resizeElement.removeClass('resizable');
      });
      $('.resizable').css('width', widthValue);
    }).on('mouseup touchend touchcancel', function(){
      dragElement.removeClass('draggable');
      resizeElement.removeClass('resizable');
    });
    e.preventDefault();
  }).on('mouseup touchend touchcancel', function(e){
    dragElement.removeClass('draggable');
    resizeElement.removeClass('resizable');
  });
}

</script>



### Compare yourself

<div class="ba-slider m-top-s">
    <img src="/dist/img/uni-pricing-v1.png" alt="Universal Apps Pricing V1 (deprectaed)">
    <div class="resize">
        <img src="/dist/img/uni-pricing-v2.png" alt="Universal Apps Pricing V2 (current)">
    </div>
    <span class="handle"></span>
</div>
<p class="type-xs">
    Left: new V2 plans — Right: old V1 plans
</p>



### Specs & prices comparison table

| ↓ Spec / Plan →     | Light-V1 | Light    | Basic-V1 | Standard | Plus-V1 | Plus    |
| ------------------- | -------- | -------- | -------- | -------- | ------- | ------- |
| PHP memory          | 128 MB   | 128 MB   | 128 MB   | 256 MB   | 128 MB  | 512 MB  |
| PHP processes       | 2        | 2        | 2        | 4        | 2       | 8       |
| Web storage         | 512 MB   | 1 GB     | 1 GB     | 5 GB     | 5 GB    | 10 GB   |
| MySQL storage       | 128 MB   | 256 MB   | 256 MB   | 512 MB   | 512 MB  | 1 GB    |
| Backups             | no       | no       | no       | yes      | yes     | yes     |
| Crons               | no       | no       | no       | yes      | yes     | yes     |
| App collaboration   | no       | yes      | yes      | yes      | yes     | yes     |
| Performance metrics | no       | yes      | yes      | yes      | yes     | yes     |
| Automatic HTTPS     | no       | yes      | yes      | yes      | yes     | yes     |
| Custom HTTPS        | no       | yes      | no       | yes      | yes     | yes     |
| Monthly price ($/€) | 3        | 5        | 6        | 15       | 12      | 30      |




### Why we are doing this

The Professional Stack is designed for modern web applications, this mostly means Laravel apps or modern high traffic websites. The Universal Stack with more backwards compatibility has a wider range of applications. So we are seeing more classical legacy content driven websites, mostly CMS-based. Especially Craft-CMS is raising. And those software-systems sometimes need a little more horse-power to behave well.

### Existing plans don't change — it's opt-in

If you have existing Apps: Don't worry! **Your current plans will not change.** You can scale up your App from your current V1 plan to a V2 plan. Any new Apps booked from now on need to be on the new V2-Pricing.

### The middle plan is now called Standard

We are also changing a wording: We think that "Standard" is a better than "Basic" when is comes to the name for the plan in the middle, the plan we do recommend for most common use cases.


### More details

Yes, this is a professionalisation of the Universal Stack. We are re-introducing the PHP processes here, an important metric that describes the number of maximum concurrent requests. More resources even for low/mid traffic sites with multiple (Ajax) requests per visit make a huge difference. 
And there are bigger PHP memory options available now, to support intensive tasks like image transformations without running into trouble.  

This is also a step back from features to hardware specs. For the sake of clarity we have skipped the distinctive features: Automatic HTTPS, Performance metrics and App collaboration, which are now always included.

**Are we doing the right thing?** We are very curious what you think. 
