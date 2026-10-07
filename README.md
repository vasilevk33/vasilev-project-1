# Smart Water Bottle Documentation

| Table of Contents |
| -------- |
| [Project Description](#project-description) |
| [Design](#design) |
| [Describing The Interface](#describing-the-interface) |
| [Implementation](#implementation) |
| [Future Work](#future-work) |
| [AI Documentation](#ai-documentation) |
| [Demo Video](#demo-video) |
| [Link to Repo and Hosted Application](#link-to-repo-and-hosted-application) |

## Project Description
The Smart Water Bottle is a prototype designed to help users track daily hydration, monitor water quality, and provide handy utility for active lifestyles. Traditional water bottles require manual hydration tracking and offer no insight into water freshness or temperature, often leading to dehydration or consumption of stale water.  

This water bottle contains three distinct components and a mobile device application:  
1. Physical Bottle: Features a real-time liquid-level LED light and a digital thermometer readout embedded directly into the sturdy body of the bottle.
2. Interactive Cap: Has a circular LED sanitization status ring (indicating Cleaning (🟡), Clean (🟢), and Stale (🔴) alerts) and a real-time LED progress ring displaying progress toward daily water consumption goals.
3. Detachable Modular Power Bank: A rechargeable power bank that powers internal bottle sensors while also serving as a charger for external devices when on the go.
4. Mobile Phone Companion App: A secondary interface enabling users to configure hydration goals, switch between Imperial and Metric units, tune alert durations, and monitor water bottle telemetry in real time (Exact Goal Progress and Water Remaining).  

The web interface for the Smart Water Bottle provides both manual testing controls and an autonomous simulation simulating gradual water warming to room temperature, periodic sips, battery discharge (power bank + external device), automated sanitization, and maintenance stale-water dumping cycles.  

[⬆️ Back to Table of Contents](#smart-water-bottle-documentation)

## Design

### 1. Characterizing the Affordances
* Small, lightweight, and fully portable
* Cannot fit into typical pockets, but can fit into backpack pockets and cupholders in cars 
* Able to stand up right on a flat surface without falling
* Throwable
* Can be flipped upside down
* Grippable: can be held (via handle or comfortable grip to hold and pick up with one hand)
* Drinkable: drinking spout allows drinking and pouring
* Fillable: hollow inside, can store stuff (ideally water/liquids)
* Liquid Durability: can hold liquids without breaking or spilling anything, can be in a body of water without being damaged
* Openable: Cap to twist, cap to flip open
* Closeable: Cap to twist, cap to flip down and shut
* Washable: Can be washed by hand or in a dishwasher 

### 2. Capturing User Needs
**Interview Questions with Responses:**  
**Q1.) Tell me about your favorite water bottle? What did you like the most about it?**   
Person 1: Glass bottle, rubbery protector around the glass, wooden cap; liked it because it was made of natural materials.  
Person 2: Teal water bottle with lots of stickers applied. Liked it because it was very easy to apply stickers to it.  
Person 3: My favorite water bottle that i get is a one-time-use smart water bottle that i reuse for around 4 months on average. I like this water bottle because its lose cost and if i lose it, its not a big deal. I also enjoy that on the inside portion of the label it has a little goldfish.  

**Q2.) How do you maintain/clean your water bottle?**    
Person 1: Rinse it every time it is used and done with water. Washes it once every two weeks under running water with soap, using a brush to clean the inside of the bottle.  
Person 2: Rinses it with a little bit of water once a month and uses dish soap to scrub it.  
Person 3: I put a little water into the bottle, put the cap on, and then shake it. I don’t clean my bottles with soap or anything like that.  

**Q3.) When shopping for a new water bottle, what drawbacks make you avoid buying a particular bottle?**   
Person 1: Doesn’t want the bottle to be plastic or made of metal. The material is problematic. Doesn’t want the bottle to be too big or too small. 500 to 750 ml is an ideal size.  
Person 2: If the bottle is too big, it doesn’t fit into a backpack pocket. Also, if the bottle is too small and slips out of the pocket of a backpack, having a handle on the side is also inconvenient.  
Person 3: If it’s heavy or prone to leaking.  

**Q4.) If you could change or add anything to your current water bottle, what would it be?**    
Person 1: Would put a rope handle on top of the bottle to carry it more easily. Would also add a tracker to track how much water they drink in a day and whether they reached their daily goal of drinking enough water.  
Person 2: Would add a portable plug-in that has USB ports available to charge devices. A way to alert if the water going inside the bottle is filtered and clean water to drink.  
Person 3: Maybe a way to clip it in to a backpack, when I go hiking and put it in my backpack it can fall out. It would be nice if there was a proper way to secure it.  

**Q5.) What does a typical day with your water bottle look like? Where does it go with you, and how often do you interact with it?**  
Person 1: The water bottle is always around. Stays on the desk at work and is used quite frequently to take small sips. The water bottle also stays quite frequently inside the car on weekends when doing various things.  
Person 2: Stays in the backpack pocket very frequently. Whenever a drink or refill is needed, takes it out of the backpack to use and then put it back into the pocket.  
Person 3: It comes with me to school / work and at the start of the day I refill it and then place it in my backpack. Throughout the day as needed I take it from my backpack and drink from it, and then return it to my backpack. I interact with it only when I need to.  

**Q6.) Can you describe any difficulties or frustrations you had with a water bottle you owned?**  
Person 1: The rubber protector on the glass bottle didn’t fit smoothly inside backpack pockets or holders, as the rubber created friction.  
Person 2: Dropping the bottle from a small distance causes it to get dents and get damaged.  
Person 3: The cap has a capillary action sort of thing where the threads of the bottle will get water interlocked into them, which then causes water to drip when I take a sip.  

**Q7.) How many water bottles do you own? If multiple, what makes you pick one over the others on a given day?**  
Person 1: Owns multiple. Picks the bigger one most frequently, as it requires fewer refills. Picks the smaller bottle if it needs to be carried by hand frequently, as it weighs less. When traveling or walking with a purse, a smaller bottle is preferred.  
Person 2: Owns one water bottle only.  
Person 3: I only own one at a time.  

**Q8.) What makes you decide to refill your water bottle? Where do you typically refill it?**   
Person 1: When the bottle is empty. Refills it wherever there is a water fountain in public. Or at home, uses the water from the fridge.  
Person 2: When the bottle is empty. Refills it at water fountains in public areas.  
Person 3: When it's empty or the water in the bottle has been sitting in it for too long and then will taste like plastic. I refill it at filling stations that are at school, the gym, and work.  

**Q9.) At the end of a day, how do you know whether you drank enough water?**    
Person 1: Not sure if they drank enough water in a day.  
Person 2: Listening to own body. If not feeling thirsty, then believes enough water is consumed.  
Person 3: If I'm not thirsty and I don’t have a headache.  

### 3. Assumptions About the Smart/Sensing Features
* Measures water level
* Measures water temperature
* Tracks water consumption amounts
* Can indicate if a user reaches their daily water intake goal via visual or auditory cues
* Sensor on the cap that senses when the cap is opened or closed (track how many sips the user takes in a day)
* A sensor to detect how long water sits in the bottle to ensure water freshness
* Technology to sanitize and purify the water after filling it (to eliminate bacteria and impurities)
* Powerbank can supply power to all the sensors, lights, and technology in the water bottle

### 4. User Needs and Design Requirements
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

### 5. Sketching Design Alternatives to 3 Design Challenges (10-plus-10)
**Design Challenge 1:** Enable a user to determine their remaining water volume (in fl oz or ml) and daily hydration goal progress at a glance.  
**Design Challenge 2:** Enable a user to receive immediate and simple-to-understand feedback signaling whether refilled water is sanitized and fresh or in the process of being sanitized.  
**Design Challenge 3:** Enable a user to comfortably carry and use the bottle as a power bank across various environments while preventing drop damage and water damage to electrical components.   

*Assumptions for 10-plus-10 Sketching:* I did one instance of 10-plus-10 sketching with all the design challenges incorporated instead of three separate instances of 10-plus-10 sketching focusing on one design challenge per instance. For the second round of sketches of my 10-plus-10 I focused on specific design challenges more as indicated by the DC label on the top left of the sketch (e.g., DC 2 focuses on design challenge 2).

**First Round Sketches**
<img width="3917" height="2815" alt="1" src="https://github.com/user-attachments/assets/f470f977-b899-4d55-b90e-30a19da4d0b0" />
<img width="3939" height="2759" alt="2" src="https://github.com/user-attachments/assets/b83d9fc7-32f7-41e0-aa1e-ea8bc2ff1458" />

**Second Round Sketches**
<img width="3851" height="2740" alt="3" src="https://github.com/user-attachments/assets/c3675353-4c46-440c-aa37-7150ddd59bad" />
<img width="3803" height="2647" alt="4" src="https://github.com/user-attachments/assets/72540739-5ec7-4bcf-9c86-8c76f2b1843f" />

### 6. Sketching the Interface (“The Vanilla Sketch”)
<img width="3187" height="2489" alt="vanilla" src="https://github.com/user-attachments/assets/4bc59e2e-9a01-4e8f-b873-6e0f811b5abe" />

### 7. Hybrid Sketch
<img width="4032" height="2599" alt="hybridsketch (1)" src="https://github.com/user-attachments/assets/6aa3c088-cadf-40b8-ae4c-39e37f4f1458" />

### 8. User Feedback
Person 1: The rubber handle looks very convenient for carrying the water bottle wherever I go. I also like being able to see the temperature of my water at any time I want. I am also a big fan of the ring showing the hydration progress. I like how simple it is to see where I am in the day for drinking water and whether I am getting enough. One thing I am unsure about is the height of the cap to open to drink the water. I think it is too short to drink from comfortably. Also, it is not clear that I can open that cap with a button.  
  
Person 2: I like the rubber handle to hold the bottle nicely. I also like the light bar on the side for displaying the water level with the percent next to it. Another plus is the temperature readout on the side of the bottle so I know what temperature the water is. One thing that I am unsure about is the green color for when the water is ready to drink. I feel like a calm blue color would be better. 
   
Person 3: I like the push button for the spout a lot; it fixes that annoying water drip from the cap threads I deal with. The handle looks easy to clip into my backpack with a carabiner so it stops sliding out of the side pocket. The stale water alert is cool too, so I know when to dump it. My only worry is if the battery pack makes it feel too heavy in my bag, and if that flip cap stays shut tight so no dirt gets on the straw.  

[⬆️ Back to Table of Contents](#smart-water-bottle-documentation)

## Describing The Interface
### 1. Overall View
TODO: SC of Whole display  

#### **Two Regions:**  
**Project Information & Controls (Left Region):** Contains general project information, link to documentation, the info button, manual controls (Buttons), and the simulation button.  
**Device Interface (Right Region):** Displays the 3 visual cards representing the physical bottle surfaces (Front + Top View) and the mobile app interface.

### 2. Bottle Front View
TODO: SC Of Bottle  

#### **Features:**
* **Water Level LED Strip:** A liquid water level along the wall of the bottle that reflects real-time water volume. The illuminated blue bar scales proportionally from 0% to 100% of maximum capacity (40 oz / 1183 ml), and a numerical percentage label follows the top of the current fluid level.
* **Digital Thermometer:** An embedded digital display showing live internal water temperature. This updates dynamically based on environmental warming and unit conversions (°F / °C).
* **Modular Power Bank Battery:** Located at the bottom of the bottle, this indicator displays the rechargeable base's remaining battery percentage. A pulsing animation on the battery indicates active charging.

### 3. Bottle Top View
TODO: SC Of Cap  

#### **Features:**
* **Sanitization Status Ring:** An outer LED ring communicating water purity and safety through 3 distinct states:
  * **Off (Gray):** Water is clean, fresh, and safe to drink.
  * **Cleaning (Pulsing Yellow):** Active 10-second cleaning/sanitization cycle triggered automatically upon refilling the water bottle.
  * **Clean (Pulsing Green):** Indicates successful sanitization cycle completion, remains active for the configured clean alert duration then switches to Off (Gray) to preserve power in the bottle.
  * **Stale (Pulsing Red):** Alerts the user that water is stale and is not the purest it can be (Simulation Logic: water has rested at room temperature (≥70°F) for 10 seconds)
* **Hydration Progress Ring:** An inner LED progress ring that advances clockwise as water is consumed, showing progress toward the daily hydration goal with a percentage label following the progress.

### 4. Phone App (Secondary Device)
TODO: SC Of Phone  

The phone app represents an interactive secondary device operating over Bluetooth connection to handle user preferences and display Smart Water Bottle telemetry.   

#### **Features & Controls:**
* **Connection & Battery:** Features a Bluetooth status indicator and the phone's current battery percentage with a visual battery icon.
* **Basic Telemetry:** Displays exact remaining volume in bottle and current goal progress formatted in the active unit system.
* **Daily Hydration Goal Configuration:** An interactive range slider (80 oz to 180 oz) allowing users to adjust their daily water consumption goals whenever they want.
* **Unit System Selection:** Radio buttons to switch between Imperial (oz, °F) and Metric (ml, °C), propagating conversions instantly across the bottle displays and phone display.
* **Alert Timing Customization:** Two sliders enabling users to tune how long Clean (Green) and Stale (Red) alert lights remain illuminated (1–30 seconds).  

#### **Role of the Secondary Device**
1. **Minimizing Physical Bottle Look & Enhancing Durability:** Placing full touchscreens, menus, or buttons onto a physical water bottle clutters the bottle and compromises water resistance. Putting configurations to a secondary device (Mobile Phone) keeps the bottle lightweight, sturdy, water resistant, and minimalistic.
2. **Visuals vs. Configuration:** The physical bottle is optimized for clear visual cues while working out or on the go (LED ring color, liquid fill line, temperature readout). The phone app provides personalization (setting custom goals, tuning alert durations, and switching units).
3. **Bottle to Phone Connection:** Changes on the phone (such as unit preferences or alert times) propagate immediately to the physical bottle system. Bottle actions (drinking, refilling, emptying) instantly mirror on the phone display. The phone can also be charged by the detachable power bank located on the bottle.

### 5. Testing Controls
TODO: SC of Controls  

The left region provides controls for validating bottle behavior manually and through a simulation.  

#### **Features & Controls:**
* **Manual Controls:**
  * **Drink (2oz / 60ml):** Deducts water volume from the bottle, increases progress towards daily goal, and doesn't drink if a cleaning cycle is in progress. If the water is stale, taking a drink immediately flashes the Red warning light and the user cannot drink.
  * **Refill Water:** Fills the bottle to maximum capacity (40oz), sets temperature to 55°F, clears stale status of the water, and triggers the automatic 10 second cleaning cycle (Yellow Light).
  * **Make Water Stale:** Forces an immediate stale water state, lighting the red LED alert for stale water.
  * **Empty Water:** Discards all water to 0oz / 0ml and turns any alert lights off.
  * **Charge External Device:** Transfers battery from the power bank to the connected phone in 10% increments every 2 seconds to simulate charging.
  * **Charge Power Bank (100%):** Recharges the bottle's power bank battery to 100% in 10% steps every half second.
* **Simulation:** Clicking **Start Simulation** activates a simulation modeling realistic daily water bottle use:
  * Temperature of the water gradually warms toward room temperature (70°F).
  * Phone battery and power bank battery lose charge over time.
  * Drinking from the water bottle happens automatically every 2 seconds.
  * Water resting at room temperature (70°F) for 10 seconds turns stale and is automatically emptied after the alert duration ends.
  * The bottle automatically refills when emptied.
  * When the phone battery reaches 20%, the bottle power bank starts supplying power to the phone.
  * When the power bank battery reaches 0%, the power bank starts charging to get back to 100% battery.
  * The simulation automatically halts and displays "Goal reached!" once the daily hydration goal is achieved.
  * All manual controls are still active during the simulation and will not break the simulation.
  * Clicking **Pause Simulation** after clicking **Start Simulation** pauses the simulation.
  * There is a status update below the **Pause Simulation** button that informs the user of critical actions happening (Nothing Yet ..., Refilled water!, Emptied stale water!, Charging device..., Charging power bank..., Paused, Goal reached!)

### 6. Info Button
TODO: SC of Info Button Output  

Clicking the info button opens a pop-up describing all bottle features, sanitization logic, and controls similar to what is shown in this section of the documentation. 

### 7. Interface in Action
**Bottle during active sanitization cycle (Yellow Light):**  
TODO: SC of yellow  

**Bottle after several drinks showing reduced water level and increased hydration goal progress on cap:**   
TODO: SC of Cap after drink

[⬆️ Back to Table of Contents](#smart-water-bottle-documentation)

## Implementation  
### 1. Framework & Libraries
* **Framework:** Svelte
* **Build Tool:** Vite 
* **Deployment & Hosting:** Vercel
* I did not use any additional third-party UI libraries. The web interface was created using standard Svelte components, HTML, CSS, and JavaScript.  

### 2. Code Structure
The application is divided into several components so that each part of the interface has a clear responsibility:
- `App.svelte` contains the main application state and logic, including water level, temperature, hydration progress, sanitization state, battery levels, unit conversion, charging behavior, and the simulation.
- `WaterBottleUI.svelte` organizes the three main interfaces (Front Bottle, Top Bottle, Phone App) and connects the bottle views and phone interface to the state stored in `App.svelte`.
- `WaterBottleSide.svelte` displays the front view of the bottle. CSS elements are overlaid on top of the bottle drawing to show the current water level, water temperature, and power bank battery level.
- `WaterBottleCap.svelte` displays the top view of the bottle. It includes the sanitization status ring and the hydration goal progress ring. CSS elements are overlaid on top of the bottle cap drawing to show the rings.
- `Controls.svelte` contains the controls for testing to manually simulate actions such as drinking water, refilling the bottle, making the water stale, emptying water, charging the phone, charging the power bank, and starting or pausing the simulation.
- `PhoneUI.svelte` represents the secondary device (Mobile Phone) interface. It displays information such as water remaining and hydration goal progress, and allows the user to change the daily hydration goal, units, and alert durations.

### 3. Key Implementation Details

#### 1. Reactive States
Svelte's reactive state features are used so that changes made through the testing controls, phone interface, or simulation automatically update the bottle UI. For example, drinking water decreases the water-level indicator, changing units updates all displayed measurements, and changing the daily goal updates the hydration progress ring.    

**Reactive Unit Conversion:**
```javascript
let displayWaterAmount = $derived(
    unitSystem === "Imperial" ? Math.round(waterAmount): Math.round(waterAmount * 29.5735));
```

#### 2. UI Overlays on Bottle Sketches
The bottle graphics were created separately on Google Drawings and stored in the `public` folder. The interactive indicators were then positioned over the drawings using CSS so that the digital interface appears to be integrated into the physical bottle design. Container-relative sizing and `cqw` units are used so text and indicators scale with their component containers.  

**Sanitization Ring Overlay:**
```CSS
.sanitization-ring {
        position: absolute;

        left: 2.5%;
        top: 1.45%;

        width: 95.4%;
        aspect-ratio: 1;

        box-sizing: border-box;

        border: 1.3cqw solid #8d8c8c;
        border-radius: 50%;

        pointer-events: none;
    }
```

#### 3. Timers
Cleaning, stale water, and clean water alerts use JavaScript timers. A shared `activeAlertTimer` variable and `clearAlertTimer()` helper function prevent older timers from changing the sanitization light after a newer alert has started.

#### 4. Simulation
The simulation uses JavaScript timers to model how the smart bottle changes over time. A one-second `setInterval` loop simulates the bottle operating over time. During each simulation tick, the application updates water temperature, water consumption, phone and power-bank battery levels, stale water timing, automatic refilling and charging behavior, and checks whether the user's hydration goal has been reached.  

[⬆️ Back to Table of Contents](#smart-water-bottle-documentation)

## Future Work
Although the current Smart Water Bottle prototype includes the main bottle interfaces, phone app, and simulation, these features could be improved with more development time.

### Interactive Bottle Cap
One future improvement would be making the cap interactive. I would place a clickable button over the physical button shown in the front view drawing of the bottle. Pressing it would visually open the top cap of the bottle (Shown in the middle of the top view drawing of the bottle) and have a straw pop out of it. Pressing "Drink" would only be allowed while the bottle is open, which mimics real world interaction better.

### Improved Phone App and Pairing
The phone app could be improved with more personalization options, such as additional alert preferences (notifications on phone for stale water or hot/cold water alerts), hydration settings (e.g, different water goals for different days), and better statistics. I would also like to show the Bluetooth pairing process rather than assuming that the phone and bottle are always connected. This could include a pairing screen, connection status changing, and a disconnect/reconnect button.

### Detachable Power Bank
The detachable power bank could also become interactive. A testing control could simulate unscrewing or removing the power bank from the bottom of the bottle. The interface could then react differently depending on whether the power bank is attached or not. The interface will also separate the physical bottle and power bank visually leaving them as separate parts.

### Simulation Improvements
Another improvement would be improving the simulation logic. This includes adding simulation speed options, such as 2x, 4x or even 10x speed. This would make it easier to demonstrate long term behaviors such as battery drain, hydration progress, water warming, and stale water detection without waiting through the full simulation time. The simulation could also simulate real world time and have a clock display to have battery drain be more accurate (To show how long the power bank's battery actually lasts). A real world time simulation could also better model how the bottle actually works.  

*Note: I did not have any partially implemented features that needed to be removed before the deadline, so there are no unfinished screenshots to document.*

[⬆️ Back to Table of Contents](#smart-water-bottle-documentation)

## AI Documentation
I used AI to assist with the front-end implementation of my design as well as fixing logic errors with the JavaScript timers for my sanitization ring. I created the water bottle concept and graphics, determined what controls and indicators should exist, implemented the core application logic and simulation, and decided the overall page layout and interface behavior.   

AI was used primarily to translate my ideas/sketches into HTML/CSS, the main use being positioning interface elements over my bottle drawings, styling the bottle components, and troubleshooting layout/CSS issues. I had the AI provide a general HTML/CSS skeleton given my sketches. I then updated the HTML/CSS code it gave me to get the design I wanted that most closely followed my sketches and ideas. I reviewed, tested, and updated the code thoroughly to ensure I got the design I wanted. AI was also briefly used to debug and fix errors related to sanitization status timers while I was implementing the simulation code.  

[⬆️ Back to Table of Contents](#smart-water-bottle-documentation)

## Demo Video
[⬆️ Back to Table of Contents](#smart-water-bottle-documentation)

## Link to Repo and Hosted Application
[GitHub Repo](https://github.com/vasilevk33/vasilev-project-1)  
[Hosted App](https://vasilev-project-1.vercel.app/)  

[⬆️ Back to Table of Contents](#smart-water-bottle-documentation)
