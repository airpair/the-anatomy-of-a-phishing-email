I came across an article detailing the [anatomy of a phishing email](http://www.howtogeek.com/58642/online-security-breaking-down-the-anatomy-of-a-phishing-email/) and thought it'd be interesting to analyse one of the phishing emails that slipped through my spam filter recently. *Note: I seriously hope I didn't end up installing any malware on my computer by clicking the links.*

Here's how the actual email looked like in my inbox:

<a href="http://imgur.com/I9gmWDv"><img src="http://i.imgur.com/I9gmWDvl.jpg" title="source: imgur.com" /></a>

So a couple of things stood out to me immediately.
1. Use of a tick in the email header
    - Perhaps this was a play on the "Verified" indicator on popular sites like Twitter and Facebook
    - The tick showed up as an emoji on my iPad though
2. Use of camel-case in the sentence
    - This is more a personal pet peeve, but capitalising each word was as annoying to my eye as a neon-coloured flashing gif dancing across the page
3. Incorrect spelling and punctionation
    - I read on [Quora](http://www.quora.com/Why-are-email-scams-written-in-broken-English) that email scams are written in broken English on purpose as a initial filter
    - As an aside, I find it amazing that even scammers do "client"-filtering so why is it so many talented designers don't
4. The 5 links on the footer are real
    - If you hover over those links, the target URL is  `https://email-edg.paypal.com/r/PNFB1X9/A74OFA/QNKT3RK/FDQLFE/5C4YA1/NN/h` but it actually redirects to the real PayPal customer support page at `https://www.paypal.com/us/webapps/helpcenter/helphub/home/`
5. The links for updating your information are, obviously, not real
    - On hover, the target URL is a bit.ly link, `http://bitly.com/1EsP3y7`
    - On click, the link led to a `.ga` domain, and it was not https either


<a href="http://imgur.com/GsEonuY"><img src="http://i.imgur.com/GsEonuYl.png" title="source: imgur.com" /></a>

Viewing source on the email showed that the logo was served from `https://image.paypal-communication.com/`. I'm honestly not sure if that's a legit domain or not though.

Somehow the email originated from what seems like a legit PayPal account. But I'm not sure what the actual PayPal support email address is either.

<a href="http://imgur.com/j3JNDYC"><img src="http://i.imgur.com/j3JNDYCl.png" title="source: imgur.com" /></a>

If you did click the link to update your information, this is what you'll see:

<a href="http://imgur.com/tQELfU2"><img src="http://i.imgur.com/tQELfU2l.jpg" title="source: imgur.com" /></a>

The only thing you can do on this page is fill in your Email address and Password, then click the Login button. Everything else is not clickable. Just for reference sake, here's what the real PayPal login looks like:

<a href="http://imgur.com/bX3EOpW"><img src="http://i.imgur.com/bX3EOpWl.png" title="source: imgur.com" /></a>

If you ask me, it looks pretty close and unless you regularly access PayPal, you may not even tell the difference. Unless you click on other links. That kind of gave the game away.

A quick peek at the page source revealed a non-PayPal domain and the rest of the server requests would go to this domain for all subsequent activities on this site.

<a href="http://imgur.com/dLmWYFC"><img src="http://i.imgur.com/dLmWYFCl.png" title="source: imgur.com" /></a>

After logging in, you will be asked to update your billing address. 

<a href="http://imgur.com/kqkeIo8"><img src="http://i.imgur.com/kqkeIo8l.jpg" title="source: imgur.com" /></a>

The breadcrumbs on the footer were not clickable. And all the links on the site lead back to the current site. I thought it was a nice touch to include the security verification icons, but this just goes to show that anyone can copy and paste a security image on their site.

You're next expected to update your Credit/Debit card information.

<a href="http://imgur.com/Fx6KaK4"><img src="http://i.imgur.com/Fx6KaK4l.jpg" title="source: imgur.com" /></a>

Given they also asked for the VBV password, I wonder if there is some automated system that makes a transaction once you send over this information, because usually there is a time limit on the validity of the VBV password. Just a thought.

Finally, you have to update your bank account information.

<a href="http://imgur.com/mRJtmsY"><img src="http://i.imgur.com/mRJtmsYl.png" title="source: imgur.com" /></a>

If you've noticed, from the previous screens, there is a notification number on the top right corner of the profile icon. This number counts down as you go through the site. I'm pretty sure using notifications as pagination is not common UI, but maybe the rationale behind it is the same as using broken English on the site.

Interesting fact, the routing number field had validation on it. Not sure if the credit card number field had it, because I used a generated number for that.

Unfortunately, after you're done giving them your information, they sort of abandon you completely.

<a href="http://imgur.com/4XJZvyb"><img src="http://i.imgur.com/4XJZvybl.jpg" title="source: imgur.com" /></a>

All you get is a static Thank You message, and no, you do not get redirected within 3 seconds. All the links on the site just lead back to this Thank You page. I found it intruiging that the source was completely empty. There was a console log error that I obviously was ill-qualified to make sense of as well.

I tried running the domain through [IP Checker](http://ipinfo.info/html/ip_checker.php) and found that it was an IP address from India. 

I normally don't get a lot of such messages landing in my inbox because my email client does a reasonably good job of kicking them into the spam folder so I thought I'd just poke around it a bit. Hopefully I didn't get myself into trouble for this, but I thought it'd be interesting to just share my observations of how a phishing email worked.

Echoing the words of [Jason Faulkner](http://jasonfaulkner.com/), when it comes to staying safe online, it never hurts to have a good bit of cynicism.
