# Measuring Noise

Cities are noisy places -- I know, because I live in the middle of one -- but what is unreasonable noise? That was the question I wanted to try and answer for residents of a nearby street who were being woken up in the early mornings by the noise of buses leaving a depot to reach the start of their routes. First, I had to measure the noise to a reasonably high standard using cheap and relatively simple equipment, but that turned out to be the easy bit. Much more difficult was then understanding what I had measured and demonstrating what it meant. I'm still not sure if I've succeeded -- read on and see what you think!

## What is noise?

At a physical level, sound is simply pressure waves travelling through a fluid (air or water). When those pressure waves reach us, they are converted into nerve signals by the structures in our ears, and our brains interpret those signals into what we experience as sounds. Human ears have an amazing range of sensitivity -- there is roughly a trillion times difference in sound pressure between the quietest sounds that we can hear and the loudest sounds at the threshold of pain. As well as magnitude, our ears can sense the frequency of the pressure waves, the shape of the waveform, and also the direction they are coming from, allowing us to experience the soundscape around us in exquisite detail. But beyond those purely physical aspects, the interpretation of sounds by our brains creates a more subjective experience. Sounds can sooth or startle, be pleasurable or painful, attract or annoy.

The word "noise" usually means sounds that are negative or undesirable in some way, but that still allows for a broad range of interpretation. Irritating noises can be quiet (a dripping tap) or loud (a backfiring exhaust), they can vary in frequency (the high-pitched whine of a fan or the thumping bass from a nightclub), they can be continuous (the roar of a nearby motorway) or intermittent (passing cars on a quiet street). Whether or not a particular noise negatively affects someone can depend on who they are, what they are expecting, how close it is, and even what time of day it is. A sudden sound in the dead of night might be enough to wake someone up, while that same person might not even notice an identical sound during the daytime.

Finding a way to wrap all that variation up into a single definition of "noise" and then measure it might seem like an impossible task, but in the early 2000s the European Union decided to try ...

## The END of noise

In response to a World Health Organisation report about the negative health impacts of noise, the European Parliament passed the Environmental Noise Directive (END). This required member states to consider the impacts of noise on people and take steps to mitigate those impacts where they were excessive. It created a framework for how authorities should determine, communicate and reduce the effects of environmental noise. In Scotland, the result was a website, [Scotland's Noise](https://noise.environment.gov.scot/index.html), which maps the expected noise levels in the main population centres ("agglomerations") across the country. Here's what it looks like for central Edinburgh, where I live:

![Central Edinburgh daytime noise map](/home/douglas/code/web/scripsi.uk/docs/science/statistics/measuring-noise01.png)

My flat lies in a red-shaded area of the map, so it looks like I should experience noise levels of between 60 and 65 dB, but what does that actually mean? Well, the [FAQ section of the website](https://noise.environment.gov.scot/frequently-asked-questions.html) does a pretty good job of explaining how they made the map. They did NOT send out an army of people to measure sound levels on every street corner over a long period! Instead, they fed existing data on things like traffic, public transport, industrial sites, building locations and population density into a mathematical model that would predict the expected environmental noise level at any point. The model divides the area up into 10m squares and predicts _Leq_ (_equivalent continuous sound pressure level_) at a point 4m above the ground in the centre of each of those squares. The noise contours on the map are then calculated from those predictions.

So the map shows the average noise level I should _expect_ to experience in a particular location on a typical day (provided I happen to be floating 4m above ground level, of course). That's relatively straightforward, but how accurate or useful is it?

## What the L?

