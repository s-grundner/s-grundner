# This Is What Makes Quantum Computers Powerful Problem Solvers

_Captured: 2017-04-04 at 17:55 from [singularityhub.com](https://singularityhub.com/2017/03/30/this-is-what-makes-quantum-computers-powerful-problem-solvers/)_

![](https://singularityhub.com/wp-content/uploads/2017/03/how-quantum-computers-work-6.jpg)

In a previous article, I introduced the recent [open-sourcing of quantum computing software](https://singularityhub.com/2017/01/28/quantum-computing-progress-will-speed-up-thanks-to-open-sourcing/) by DWave. DWave is the maker of a quantum computer being used and studied by a number of groups, including NASA and Google, and there are other quantum computers in the works too. Although the field is still young, recent progress has been making headlines.

If we can make practical quantum computers, they will be very powerful--but to see why requires understanding what makes them different. In this article, I'll explain the underlying physics that makes quantum computing possible.

Quantum computers aren't just a new, faster model of the computer in front of you. They're based on a completely different method of storing information and decision-making. It's like comparing a jet turbine to a propeller: they achieve the same purpose, but the complexity and power are vastly disproportionate.

### **A Bit About Traditional Computers**

Let's begin by reminding ourselves how digital computers work.

The basic ingredient is the binary digit, or _bit_, which may take only the values 0 or 1. In modern computers, bits take the form of tiny electrical switches called transistors. Transistors are in one of two states. When they are switched on, they conduct electrical current. This is the "1" state. When switched off, they are not conducting current. This is the "0" state.

![](https://singularityhub.com/wp-content/uploads/2017/03/quantum-computing-explainer-2.jpg)

In a physical computer chip, we might find a series of transistors in the following states: on, on, off, on. In binary, the mathematical language of computation, the series becomes 1101.

This might appear to be an inadequately crude method of communicating information--how could we possibly convey the rich tapestry of the world using only this black-and-white mold? The first step is recognizing that bits can represent numbers in our traditional counting system. For example, 1101 represents the number 13 and 0110 represents the number 6.

In fact, these are the _only_ ways we can represent 13 and 6 using bits, creating a unique translation dictionary between strings of bits and normal numbers. In this way, we can assemble arbitrarily large numbers by stringing together bits. The MacBook Pro uses a 64-bit processor to express every number up to 18,446,744,073,709,551,615.

(Check out this video to learn more about how binary works.)

But if computers could merely store numbers, we would not find them very useful. The reason computers have become ubiquitous is we can use these numbers to further represent many other things.

Take shades of gray: simply interpolate between pure black (0) and pure white (255, by convention). Colors can be decomposed into red, green, and blue components, each having their value interpolated up to 255. Logic operations, musical notes, letters in the alphabet, internet pages, online dating profiles and many other types of information may be expressed in the same way.

Modern computers use billions of transistors and multiple levels of code to produce high-def video and complex apps, but look closely enough, and the digital world reduces to a simple series of bits.

### **How Quantum Computers Are Different**

We need only look in our pocket to see that traditional computers are powerful. But there are some problems they're ill-suited to solve. This is where quantum computers come in. A quantum computer can solve a special set of problems many magnitudes of order faster than traditional computers.

What makes quantum computers so much faster? They can perform many calculations at once.

#### **"The building blocks of quantum computers are not bits and transistors. They are _qubits_ and physical components so small they operate by the rules of quantum physics."**

This is possible because the building blocks of quantum computers are not bits and transistors. They are _qubits_ and physical components so small they operate by the rules of quantum physics. These components might literally be elementary particles, such as electrons, suspended in magnetic fields.

This is where the weirdness of quantum physics comes into play. The standard shorthand explanation says traditional bits can be either 1 or 0, whereas according to the rules of quantum physics, qubits can be 1, 0, or _both at the same time_.

This is what truly makes a quantum computer quantum. But let's dig into what that means a bit more.

### **Let's Take a Quantum Hike**

To be clear, quantum computers do not offer more discrete states than a traditional computer--the states are still 1 and 0--but there is no longer an exclusive choice between these states required_ until the very end of a calculation_. This may seem paradoxical--how can something be 1 and 0 simultaneously? And even if this is so, why is a choice required at the end?

![](https://singularityhub.com/wp-content/uploads/2017/03/quantum-computing-explainer-1.jpg)

To better understand how this is possible, imagine hiking with a magnetic compass.

During the day you navigate as you please and the terrain dictates, glancing at your compass and noting that your direction changes. You might begin walking east, then turn north, spin around to go south, before finally nearing northwest. But at the end of each day, you record only whether your encampment is north or south of your departure point that morning.

An example log might read "Day 1: North. Day 2: North. Day 3: South. Day 4: North."

This two-choice answer belies your more elaborate trajectory containing all the other directions available to the compass. North represents "1" and south represents "0," but of course, there are many other "intermediate" choices which can be expressed. This is similar to a quantum calculation. During the calculation, a qubit may take any value, but in the final answer there is only a 1 or 0 logged.

![](https://singularityhub.com/wp-content/uploads/2017/03/what-is-quantum-computer-5.jpg)

So, the qubit's initial state--the hike's trailhead--is the problem it's trying to solve written in binary. The qubit's final state--the campsite or destination--is its part of the solution, also written in binary. And simplistically, we can think of the qubit's interim state as a combination of 1 and 0, just as the other directions you moved throughout your hike were combinations of north and south.

The day's hike around swamps, between hills, and through forests is the quantum calculation--a circuitous route exploring the solution set with a zig northeast, a zag due west, and so on. Eventually, however, each qubit falls into a binary state, and we arrive at our destination.

### **An Exponential Speed-Up**

During a calculation, a qubit pointing in the east direction isn't simply weighted 50 percent north, 50 percent south--it will specifically remember that it was an eastern direction. This preservation of the direction is called _coherence_, and it is the most important property for quantum computers.

Coherence is the property of a qubit to experience the full range of values and for qubits to share these values with each other. Four coherent qubits could possess values such as "east, northwest, southeast, west," whereas incoherent qubits would possess only values "north, north, south, north." Further, each of their values influences the values of their fellow coherent qubits.

![](https://singularityhub.com/wp-content/uploads/2017/03/how-quantum-computers-work-21.jpg)

Since qubits sharing mixed states speeds up computation--this is how they perform multiple calculations at once--_it is absolutely essential the qubit maintain coherence during the calculation_. Otherwise, we are just using a simple, slow digital computer only performing one calculation at a time.

A coherent quantum computer thus considers _both 0 and 1 simultaneously_, performing a calculation for the north as well as the south, but weighting the answer in a way that preserves the direction of the compass. Mathematically, this can be done using imaginary numbers, meaning we don't need to consider east as a direction unique from north or south but only as a strange combination of them.

Increasing coherence time has been a major obstacle in making commercially-viable quantum computers. Calculations require at least about 100 nanoseconds, and we have now achieved about 175 nanoseconds. As noted in my last article, this should improve as software improves--the more you can do with a quantum computer, the more resources will pour into the field.

The upshot of all this? Quantum computers offer a massive increase in computing power. A single qubit may concurrently perform two calculations, two qubits may perform four, three qubits eight, and so forth, producing exponentially increasing speed. Just thirty qubits can simultaneously perform _more than one billion calculations_.

Aimed at the right problems and with the right software, the rise of quantum computers may mark a very significant moment in the history of computation.
