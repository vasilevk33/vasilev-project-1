# Smart Water Bottle Documentation

## Project Description

## Design

### 1.) Characterizing the Affordances
* Small, lightweight, and fully portable
* Cannot fit into typical pockets, but can fit into backpack pockets and cupholders in cars 
* Able to stand up right on a flat surface without falling
* Throwable
* Can be flipped upside down
* Grippable: can be held (via handle or comfortable grip to hold and pick up with one hand)
* Drinkable: drinking sprout allows drinking and pouring
* Fillable: hollow inside, can store stuff (ideally water/liquids)
* Liquid Durability: can hold liquids without breaking or spilling anything, can be in a body of water without being damaged
* Openable: Cap to twist, cap to flip open
* Closeable: Cap to twist, cap to flip down and shut
* Washable: Can be washed by hand or in a dishwasher 

### 2.) Capturing User Needs
**Interview Questions with Responses:**  
**Q1.)** Tell me about your favorite water bottle? What did you like the most about it?  
Person 1 (Mom): Glass bottle, rubbery protector around the glass, wooden cap; liked it because it was made of natural materials.  
Person 2 (Little Brother): Teal water bottle with lots of stickers applied. Liked it because it was very easy to apply stickers to it.  
Person 3 (Friend): My favorite water bottle that i get is a one-time-use smart water bottle that i reuse for around 4 months on average. I like this water bottle because its lose cost and if i lose it, its not a big deal. I also enjoy that on the inside portion of the label it has a little goldfish.  

**Q2.)** How do you maintain/clean your water bottle?  
Person 1 (Mom): Rinse it every time it is used and done with water. Washes it once every two weeks under running water with soap, using a brush to clean the inside of the bottle.  
Person 2 (Little Brother): Rinses it with a little bit of water once a month and uses dish soap to scrub it.  
Person 3 (Friend): I put a little water into the bottle, put the cap on, and then shake it. I don’t clean my bottles with soap or anything like that.  

**Q3.)** When shopping for a new water bottle, what drawbacks make you avoid buying a particular bottle?  
Person 1 (Mom): Doesn’t want the bottle to be plastic or made of metal. The material is problematic. Doesn’t want the bottle to be too big or too small. 500 to 750 ml is an ideal size.  
Person 2 (Little Brother): If the bottle is too big, it doesn’t fit into a backpack pocket. Also, if the bottle is too small and slips out of the pocket of a backpack, having a handle on the side is also inconvenient.  
Person 3 (Friend): If it’s heavy or prone to leaking.  

**Q4.)** If you could change or add anything to your current water bottle, what would it be?  
Person 1 (Mom): Would put a rope handle on top of the bottle to carry it more easily. Would also add a tracker to track how much water they drink in a day and whether they reached their daily goal of drinking enough water.  
Person 2 (Little Brother): Would add a portable plug-in that has USB ports available to charge devices. A way to alert if the water going inside the bottle is filtered and clean water to drink.  
Person 3 (Friend): Maybe a way to clip it in to a backpack, when I go hiking and put it in my backpack it can fall out. It would be nice if there was a proper way to secure it.  

**Q5.)** What does a typical day with your water bottle look like? Where does it go with you, and how often do you interact with it?  
Person 1 (Mom): The water bottle is always around. Stays on the desk at work and is used quite frequently to take small sips. The water bottle also stays quite frequently inside the car on weekends when doing various things.  
Person 2 (Little Brother): Stays in the backpack pocket very frequently. Whenever a drink or refill is needed, takes it out of the backpack to use and then put it back into the pocket.  
Person 3 (Friend): It comes with me to school / work and at the start of the day I refill it and then place it in my backpack. Throughout the day as needed I take it from my backpack and drink from it, and then return it to my backpack. I interact with it only when I need to.  

**Q6.)** Can you describe any difficulties or frustrations you had with a water bottle you owned?  
Person 1 (Mom): The rubber protector on the glass bottle didn’t fit smoothly inside backpack pockets or holders, as the rubber created friction.  
Person 2 (Little Brother): Dropping the bottle from a small distance causes it to get dents and get damaged.  
Person 3 (Friend): The cap has a capillary action sort of thing where the threads of the bottle will get water interlocked into them, which then causes water to drip when I take a sip.  

**Q7.)** How many water bottles do you own? If multiple, what makes you pick one over the others on a given day?  
Person 1 (Mom): Owns multiple. Picks the bigger one most frequently, as it requires fewer refills. Picks the smaller bottle if it needs to be carried by hand frequently, as it weighs less. When traveling or walking with a purse, a smaller bottle is preferred.  
Person 2 (Little Brother): Owns one water bottle only.  
Person 3 (Friend): I only own one at a time.  

**Q8.)** What makes you decide to refill your water bottle? Where do you typically refill it?  
Person 1 (Mom): When the bottle is empty. Refills it wherever there is a water fountain in public. Or at home, uses the water from the fridge.  
Person 2 (Little Brother): When the bottle is empty. Refills it at water fountains in public areas.  
Person 3 (Friend): When it's empty or the water in the bottle has been sitting in it for too long and then will taste like plastic. I refill it at filling stations that are at school, the gym, and work.  

**Q9.)** At the end of a day, how do you know whether you drank enough water?  
Person 1 (Mom): Not sure if they drank enough water in a day.  
Person 2 (Little Brother): Listening to own body. If not feeling thirsty, then believes enough water is consumed.  
Person 3 (Friend): If I'm not thirsty and I don’t have a headache.  

### 3.) Assumptions About the Smart/Sensing Features
* Measures water level
* Measures water temperature
* Tracks water consumption amounts
* Has a mechanism to heat/cool the bottle: can heat/cool water to a specific temperature
* Can indicate if a user reaches their daily water intake goal via visual or auditory cues
* Sensor on the cap that senses when the cap is opened or closed (track how many sips the user takes in a day)
* A sensor to detect how long water sits in the bottle to ensure water freshness

### 4.) User Needs and Design Requirements
#### **User Need 1**  
**What user needs to do:** The user needs an easy way to know if they are meeting their daily hydration goals.  

**What problems do they face:** The user guesses or relies on how thirsty they feel to figure out if they drank enough water for the day. The user also struggles to determine how much water they consumed at a given time.  

**What do they want:**  
- User wants to have automatic tracking of how much water they drink throughout the day  
- User wants to see the exact current water level inside the water bottle at a glance  
- User wants clear confirmation when their daily hydration goal has been met  

**Design Requirement 1:**  The bottle must have a sensor detecting current water levels and visual indicators indicating the current water level and daily hydration goal progress.  
#### **User Need 2**  
**What user needs to do:** The user needs to carry their water bottle effortlessly in different environments (school, work, commute, gym) without any physical discomfort or damage to the bottle.  

**What problems do they face:** The user has discomfort carrying full water bottles with a full hand grip, has issues placing their bottles inside backpack pockets and cup holders, and gets frustrated when small dents and damage form from small drops.  

**What do they want:**  
- User wants a comfortable rope/cord/loop/handle on top of the bottle for single-finger transport and backpack clip transport  
- User wants a smooth material and compact body that can slide and fit easily into backpack pockets and cup holders without getting stuck or sliding out  
- User wants the body to be durable to withstand drops and prevent dents  

**Design Requirement 2:** The body of the bottle must have a smooth and durable exterior, fit inside standard 2.5”-4” diameter and 2”-3” depth cup holders, and have a convenient carry handle on the cap.  

#### **User Need 3**  
**What user needs to do:** The user needs to keep their water bottle clean with regular washing without breaking internal electronics.  

**What problems do they face:** Smart water bottles have electrical components that risk damage when scrubbed with water and soap or when placed in dishwashers.  

**What do they want:**  
- Users want to clean the interior and exterior of the water bottle using water and soap without disassembling the water bottle  
- Users want the electrical components in the water bottle to be sealed and protected from water so they do not break  

**Design Requirement 3:** All electronic components (interfaces and ports) must be waterproof and properly sealed to allow full washing under water.  

#### **User Need 4**  
**What user needs to do:** The user needs to know whether the water they are drinking is safe and fresh to drink.  

**What problems do they face:** When the user refills their water bottles at public fountains, it may taste stale and possibly be contaminated. Also, water left sitting can become stale.  

**What do they want:**  
- Users want immediate feedback to know if their refilled water is safe and fresh  
- Users want active sanitization and preservation to prevent any bacteria from forming and having any staleness in the water  

**Design Requirement 4:** The bottle must have a sanitizing system in the cap and provide a visual indicator to confirm if the water is safe and fresh to consume.  
#### **User Need 5**  
**What user needs to do:** The user needs a convenient way to keep portable devices (phones, laptops, AirPods, etc.) charged while traveling and with no easy access to outlets.  

**What problems do they face:** When the user is traveling or has long days away from home, their mobile devices lose charge when outlets are not available.  

**What do they want:**  
- Users want access to charging power from a portable object they already take with them everywhere  

**Design Requirement 5:** The bottle must have a power bank with USB-C ports that can charge external devices.  

### 5.) Sketching Design Alternatives to 3 Design Challenges (10-plus-10)
**Design Challenge 1:** Enable a user to determine their remaining water volume (in fl oz or ml) and daily hydration goal progress at a glance.  
**Design Challenge 2:** Enable a user to receive immediate and simple-to-understand feedback signaling whether refilled water is sanitized and fresh or in the process of being sanitized.  
**Design Challenge 3:** Enable a user to comfortably carry and use the bottle as a power bank across various environments while preventing drop damage and water damage to electrical components.   

*Assumptions for 10-plus-10 Sketching:* I did one instance of 10-plus-10 sketching with all the design challenges incorporated instead of three seperate instances of 10-plus-10 sketching focusing on one design challenge per instance. For the second round of sketches of my 10-plus-10 I focused on specfic design challenges more as indicated by the DC label on the top left of the sketch (e.g. DC 2 focuses on design challenge 2).

**First Round Sketches**
Todo: Pic 1
Todo: Pic 2  

**Second Round Sketches**
Todo: Pic 1
Todo: Pic 2  

### 6.) Sketching the Interface (“The Vanilla Sketch”)
Todo: Pic

### 7.) Hybrid Sketch
Todo: Pic

### 8.) User Feedback
Person 1 (Mom):  
Person 2 (Brother):  
Person 3 (Friend): I like the push button for the spout a lot; it fixes that annoying water drip from the cap threads I deal with. The handle looks easy to clip into my backpack with a carabiner so it stops sliding out of the side pocket. The stale water alert is cool too, so I know when to dump it. My only worry is if the battery pack makes it feel too heavy in my bag, and if that flip cap stays shut tight so no dirt gets on the straw.  

## Describing the Interface
TODO: Make sure to mention role of the phone. Why have this secondary device?

## Implementation

## Future Work

## AI Documentation

## Demo Video

## Link to Hosted Application
[Hosted App](https://vasilev-project-1.vercel.app/)
