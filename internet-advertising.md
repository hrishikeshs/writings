# Internet advertising - 1

Advertising has ruined the internet. The most visible example of this is on search engine results,
closely followed by every social media feed ever. Right off the bat, I have to take some blame
for it because I once worked on ad-campaign creation and optimization flows for enterprise
customers. Maybe I can make up for the small part I played by sharing some of the stuff I
do to avoid internet advertising as aggressively as possible.

I feel the need to explain why I hate internet ads (and ads in general) so much:
Internet advertising has ruined the web. It has made something that could have been
really cool and useful into a wasteland: just today, I tried to look up a blog I remember
reading a while back where the author had written about AI and how an 'AI model' is just a long
equation with thousands of terms. I remembered a few *exact phrases* the author had used, and when
I searched for them, I was greeted with multiple pages of SEO spam and endless ads.
As a programmer, my ~~googling~~ searching skills are top-notch, even so, I failed to find it
and gave up looking for it after about 20 minutes (which included me signing up to use
a new search engine).

Apart from the obviously frustrating experience of not being able to find what you found
before, internet advertising has done the following damage:

- Social media doesn't sell user data. It's a popular misconception. What social media
actually sells is your time and attention. It sells them both to the highest bidder. This is
arguably worse - think of the enormous scale at which this sale is happening and then cry for
a bit because humans do this stuff.

- Advertising is ostensibly about 'keeping the customer informed'. Think of the last time
you felt 'informed' about a product when you saw an ad. To quote Fight Club: They got us chasing
cars and clothes. Working jobs we hate so we can buy shit we don't need

- The kind of things that companies do for a tiny bit of user attention and ad revenue is
borderline [psychological torture](https://arstechnica.com/information-technology/2017/05/facebook-helped-advertisers-target-teens-who-feel-worthless/).
For example: They hire psychologists to build 'sticky' behaviors
into their apps and websites. 'Sticky' is just a synonym of 'addictive'.
Addictions are bad. What big tobacco used to do, big tech does now.

- Privacy is a fundamental human right. Advertising only works when it's targeted. By definition,
if someone is spending money serving you ads, they are only doing it by violating your privacy.
This is true because no one (well most people/companies) on the internet spends ad dollars without
specifying targeting criteria. Companies will have all sorts of disclaimers and hand-wave about
how they "respect user preferences and privacy", but they don't. They just don't.

- Social media has been proven to be detrimental to mental health. The entire business model is
based on users comparing their lives with those of others and feeling bad. Which is a perfect
time for someone to sell you shit which will supposedly make your life better. It won't.

- The incentives are completely mis-aligned the minute you end up being a business trying to monetize
your users' attention. That's why [MicroSoft is putting ads in the start menu](https://news.ycombinator.com/item?id=40018948).
Soon, most of your useful [work turns to shit as ads invade everything](https://www.hrishi.io/metrics).

(A few people will argue that they actually found a few things via ads which made their lives better.
Here's the thing though: If you needed those things, odds are you would have walked into a store and
asked for them, or at least, searched for them on the internet)

Anyway, onto some helpful tips/tricks to minimize ads exposure:

- If the product or service has an ad-free tier which is a bit more expensive, just buy the ad-free tier.
Creators have to get paid, and if the ad-free tier is not obscenely expensive, just buy it. Treat it
as a tax you're paying to keep the internet a bit sane.

- I try to not download any apps. Apps are the best way to collect user data, and I'm interested
in having as little of my data collected. Use the company's website if possible.

- Don't enable push notifications if you do download an app. Push notifications are designed to make you
look at the app and give your attention to the company's products so they can monetize your time and mental
energy. I never enable push notification for anything. The only apps that have push notifications enabled on my
phone are messaging apps and slack. Uber and Uber eats started abusing their push notification privileges, so
I turned them off and now I just keep the app open for the duration of my usage

- Use [Ublock Origin](https://github.com/gorhill/uBlock) on your desktop/laptop browser. The developer of this
software is amazing;

- Use firefox focus on iphone. It has built in tracking protection

- Use a VPN if you can. I recommend MullVad vpn

- Sign up to services using Apple's 'hide my email' feature when you're unsure. Email is the primary attribute
advertisers use to identify you across sites/apps/etc

- Slightly more advanced: turn off canvas access to the JavaScript code that runs on sites. It can be used for
browser fingerprinting

- A few people recommend configuring your browser to send the `Do not track` header, but no one really respects it
so I don't know how effective it really is.

- More advanced: Use raspberry pi and pi-hole to block ads on your entire network: https://pi-hole.net/

Hopefully readers who are interested in blocking ads find the above tips useful. I will post more
about this topic of internet and how it's evolved and how my usage of the web has evolved over the years
on this blog.
