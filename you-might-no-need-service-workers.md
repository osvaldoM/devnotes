### You might not need service workers

In the past few years, I have been very keen to add improvements related with performance to our website. For a while I just felt that our website could be
faster, but I didn't really know how to start. I did not know what parts of the software needed improvements. I had heard about
lighthouse and 
I have tried to find opportunities for improvements from lighthouse audits but unfortunately all lighthouse provides are metrics
that are not simple to interpret and translate into numbers that scare the living shit out of the business people.
Somehow I learned about chrome UX reports and how it provided data about loading experiences collected real world devices
using the chrome browser. While I couldn't make much sense out of the 
Today I was s

Don't get me wrong when I say I can't make much sense out of the performance metrics provided by chrome ux reports or 
by lighthouse. I'm aware of the meaning held by most of the common user metrics such as : time to interactive(TTI), First 
Contentful Paint(FCP) or First Meaningful Paint(FMP), I have even made a presentation about them in this link. 
My problem with them is that there are so many nuances with them that make it hard to derive accurate or close to accurate
conclusions out of them. your time to interactive could be low not necessarily because your app makes the browser parse too much
javascript  and block the main thread, but it could really be because most of your users have really slow devices. your app's FMP 
could be fast in one region but be really slow in other regions because internet speeds might vary drastically. Bottom
line is that we can't just assume that one metric is simply low. We need to correlate it with other factors that might contribute to 
a good/bad experience and still there's no guarantee of certainity.

Although performance metrics be hard to understand, there's one thing that can easily motivate companies and that's competition.
I believe that is has already been established that site speed is related to bounce rate and conversion rate and ultimately, 
to the success of an online business. Business are always trying to get competitive advantage over other businesses, and because of that 
