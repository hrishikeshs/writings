# Information processing problems in disguise

**published on : Saturday, September 28, 2024**

When visiting Bangalore recently, I saw that the city had installed a newer
traffic signal switching system. The old traffic signals used set timers for
things - most of the traffic lights would stay red/green for a specific length of
time in seconds, before switching.

The timers were individually set based on, I assume, simulations of various
traffic conditions. The newer system was much more efficient because
it didn't use a set timer. Instead, it could dynamically switch between
red/green lights based on the vehicle density in different lanes/streets.

It was probably communicating with a central hub to pull traffic information
througout the city and was "co-ordinating" with various other traffic lights
to flash red/green and the experience for commuters was much better.
I waited at fewer lights, and traffic congestion was way lower. In other words,
it was a global optimum.

This experience made me think about how so many of the 'real-world' problems that
need to be solved are actually just information-processing problems in
disguise.

For this post, I define a 'problem' as something that needs to be done.
It's a very broad definition, so to make it more concrete, here are a few
examples:

* Directing traffic to reduce congestion in a city

* Making sure enough inventory is present to serve holiday demand

* Selecting candidate molecules for drug discovery

* Estimating the capacity that needs to be provisioned for a popular web-service
so the user/traffic growth can be handled

* Estimating lifetime earnings of a company to determine if it's undervalued or over-valued.

* Scheduling patients for appointments at a hospital depending on the availability of doctors/nurses/patient's schedules, etc

* Refactoring a large codebase to use a newer syntax/rename identifiers that
occur within a specific context

etc etc...

When we first look at this, most of these problems seem un-related because most
people think of  "traffic-congestion-control" and "patient scheduling system"
as two completely different problems to solve. They are mostly right.. to an
extent.

The similarity can be found when you take a step back and see that both the
problems above are information processing problems.

If you could somehow collect all the information about a city's traffic
patterns in real time, you could build a much better system by using
heuristics/algorithms to determine the optimal traffic flow paths, and use
that information to control the traffic light switching for commuters.

Similarly, if you could get every patient's schedule, and the information about
the hospital - doctors' existing appointments, availability of nurses, rooms, etc,
you could build a pretty good system for matching doctors with patients.

Earlier, it was hard to obtain this kind of information because we just didn't
have networks that could feed this info from the source where it was generated
(e.g: roads and streets carrying vehicular traffic), to a place where it could
be processed(servers/compute & storage needed)  and the results sent back.

However, that's no longer an issue today because we can deploy cameras/sensors
and use the internet to seamlessly send back data and get back processed info.
Of course, I had learned about [Information theory](https://en.wikipedia.org/wiki/Information_theory) when I was an undergrad, but getting to experience it's
proper application while sitting in traffic made it very tangible.

This experience has given me a new tool for problem solving - If I come across
something that needs to be done, which seems hard, I'll now try
and see if the specific problem can be turned into an information processing
problem, which is orders of magnitude easier to solve.

Further reading: [Philosophy_of_information](https://en.wikipedia.org/wiki/Philosophy_of_information)
