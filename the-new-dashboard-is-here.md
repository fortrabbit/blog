---

author:    fl
created:   2015-02-25 14:00
title:     "The new Dashboard is here"
excerpt:   "That's one small step for mankind, a giant leap for us."

---


# The new fortrabbit

It took longer than anticipated — more than a year from planning until launch. And it's a bigger update than we first anticipated. 

We have been in stealth mode working quietly for quite a while now — hopefully not too long. We have shifted our original roadmap to fully concentrate on this release. 

But now it's here. Finally. Release. Step into the light.



## Good got gooder

This is an optimization release — no REVOLUTIONARY features nor technologies. Everything is just smoother, more stable, some early design mistakes fixed. The focus was to harden the system.

Our clients use fortrabbit in production. The Dashboard should reflect this. It now feels more robust and more production-ready. 

Behind the scenes, there is much more. This update includes all the groundwork for our upcoming changes. The backend is more maintainable, manageable and scalable for us. 

### Enhanced collaboration

The most notable changes are made in the area of team work. Our new and unique [collaboration solution](http://help.fortrabbit.com/collaboration) maps real world working relationships for startups, agencies and freelancers.

We hope you like it and make heavy use of it.

### Different support model

We must acknowledge that we could not serve all clients with the same high level of support in the past. So we have made some strategic changes [here](http://forttabbit.com/support).

Support is tricky. It turned out to be a good sales channel for us as people really appreciate that kind of help on a personal level. But it's also a lot of work. Like most SaaS and hosting services, we have hidden the support costs in the general fees. On top of that we offered "premium support plans".

We have clients leveraging the general support and we have others using fortrabbit as a self-service platform. We now (hopefully) have a better offering for both groups: 

**Help yourself**: Our updated [help center](http://help.fortrabbit.com) is better structured, it's better integrated into the Dashboard, has more up-to-date content, on a higher level.

**Get support**: We have dramatically lowered the entry level prices for professional support plans by 600%!!!! — the entry level prices for professional support plans. It's really affordable now. We haven't seen something alike elsewhere. 

On top of that we now offer a Professional Support trial period. That's crucial. Most support questions statistically get asked in the first weeks. So boarding and migrating is still handled with special personal care.

Yes, we took away the included free support. So far it is an experiment. Maybe it rocks, maybe it also doesn't scale? Who knows. We hope you understand and like it. We are really curious on your feedback on this.


## Looking ahead

We will now fully concentrate on our next generation of Apps — project **Hack App**. This will be our big bet in 2015. The goal is to crack the impossible. A new architecture to make the Apps faster, more stable and at the same time even more affordable. In other words: Fast, Good **and Cheap**.

* * *

The nice [Falling Confetti](http://codepen.io/linrock/details/Amdhr/) animation was shamelessly stolen from Linmiao Xu.

<style>
	html, body {
		margin: 0;
		padding: 0;
		background: #f1f0ee;
	}
	canvas {
		position: fixed;
		left: 0;
		top: 0;
		width: 100%;
		height: 100%;
	}
	.content {
		z-index: 100;
		background: transparent;
	}
	header, aside {
		z-index: 101;
	}
</style>


<script>

	// set the stage
	$('body').prepend('<canvas id="world"></canvas>');
	
	// brutforce remove confetti anim for readability
	// TODO: stop script from consuming CPU
	setTimeout(function() {
			$('#world').fadeOut(3000, function() {
				$( '#world' ).remove();
			});
	}, 10000);

	// copied script from: http://codepen.io/linrock/details/Amdhr
	(function() {
		var COLORS, Confetti, NUM_CONFETTI, PI_2, canvas, confetti, context, drawCircle, i, range, resizeWindow, xpos;

		NUM_CONFETTI = 1000;

		COLORS = [[255, 255, 0], [255, 255, 255], [219, 100, 255], [150, 255, 255], [148, 255, 255]];

		PI_2 = 2 * Math.PI;

		canvas = document.getElementById("world");

		context = canvas.getContext("2d");

		window.w = 0;

		window.h = 0;

		resizeWindow = function() {
			window.w = canvas.width = window.innerWidth;
			return window.h = canvas.height = window.innerHeight;
		};

		window.addEventListener('resize', resizeWindow, false);

		window.onload = function() {
			return setTimeout(resizeWindow, 0);
		};

		range = function(a, b) {
		return (b - a) * Math.random() + a;
		};

		drawCircle = function(x, y, r, style) {
		context.beginPath();
		context.arc(x, y, r, 0, PI_2, false);
		context.fillStyle = style;
		return context.fill();
		};

		xpos = 0.5;

		document.onmousemove = function(e) {
		return xpos = e.pageX / w;
		};

		window.requestAnimationFrame = (function() {
		return window.requestAnimationFrame || window.webkitRequestAnimationFrame || window.mozRequestAnimationFrame || window.oRequestAnimationFrame || window.msRequestAnimationFrame || function(callback) {
			return window.setTimeout(callback, 1000 / 60);
		};
		})();

		Confetti = (function() {
		function Confetti() {
			this.style = COLORS[~~range(0, 5)];
			this.rgb = "rgba(" + this.style[0] + "," + this.style[1] + "," + this.style[2];
			this.r = ~~range(2, 6);
			this.r2 = 2 * this.r;
			this.replace();
		}

		Confetti.prototype.replace = function() {
			this.opacity = 0;
			this.dop = 0.03 * range(1, 4);
			this.x = range(-this.r2, w - this.r2);
			this.y = range(-20, h - this.r2);
			this.xmax = w - this.r;
			this.ymax = h - this.r;
			this.vx = range(0, 2) + 8 * xpos - 5;
			return this.vy = 0.7 * this.r + range(-1, 1);
		};

		Confetti.prototype.draw = function() {
			var _ref;
			this.x += this.vx;
			this.y += this.vy;
			this.opacity += this.dop;
			if (this.opacity > 1) {
			this.opacity = 1;
			this.dop *= -1;
			}
			if (this.opacity < 0 || this.y > this.ymax) {
			this.replace();
			}
			if (!((0 < (_ref = this.x) && _ref < this.xmax))) {
			this.x = (this.x + this.xmax) % this.xmax;
			}
			return drawCircle(~~this.x, ~~this.y, this.r, "" + this.rgb + "," + this.opacity + ")");
		};

		return Confetti;

		})();

		confetti = (function() {
		var _i, _results;
		_results = [];
		for (i = _i = 1; 1 <= NUM_CONFETTI ? _i <= NUM_CONFETTI : _i >= NUM_CONFETTI; i = 1 <= NUM_CONFETTI ? ++_i : --_i) {
			_results.push(new Confetti);
		}
		return _results;
		})();

		window.step = function() {
			var c, _i, _len, _results;
			requestAnimationFrame(step);
			context.clearRect(0, 0, w, h);
			_results = [];
		for (_i = 0, _len = confetti.length; _i < _len; _i++) {
			c = confetti[_i];
			_results.push(c.draw());
		}
		return _results;
		};

		step();

	}).call(this);
</script>