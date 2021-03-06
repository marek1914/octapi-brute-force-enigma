## What is Enigma, and how does it work?

Enigma is a cipher machine that was created in the early 20th century for commercial, diplomatic, and military applications. During World War II, the machine was adopted by the German military for secret communications. The Enigma encryption code was famously broken during the war at Bletchley Park, the forerunner of GCHQ, meaning intercepted messages from the German military could be decoded and read. This spectacular achievement is thought to have shortened the war, saving many lives on both sides of the conflict.

From an electrical point of view, the Enigma machine is simply a battery, 26 lightbulbs, and a switch circuit. It doesn't have any electronics, so it is an electro-mechanical device. Encryption is achieved by varying the path of an electric current through the wiring of the machine.

![Encoding a W as G on Enigma](images/Enigma-wiring.gif)

In the diagram above, you can see how a letter typed on the keyboard goes through many stages of transposition before being routed to a lightbulb on the lamp board representing the encrypted letter. The user types their plain-text message on the keyboard character by character, and reads the cipher text as each bulb is illuminated on the lamp board in response. Due to the way transposition is achieved, a typed-in letter is never encrypted as itself (e.g. typing in A will never illuminate the lightbulb for A).

The diagram might give you the impression that the transposition of letters is unchanging. This is not true though — how letters are transposed changes with every letter that is typed into the Enigma machine. That's what made the Enigma code so hard to break! The transposition changes because, as each letter is typed in, the path of the current changes as it flows to the bulbs. How does this work?

### Rotors and reflector

Inside the machine, a number of rotors with 26 contacts (one for each letter from A to Z) are stacked together to create the current path through the heart of the machine. Each rotor wheel has 26 electrical contacts on both sides and a jumble of wiring on the inside, so that typed-in letters are transposed from one side to the other. In practice this means that a specific rotor transposes A into E, B into K, C into M, and so on.

![Close-up view of rotor from a WWII captured Enigma machine](images/7X5A0921-closeup.png)

In the photo above, you can see the jumble of wiring inside an expanded rotor wheel from a WWII-captured Enigma machine. By stacking several rotors and using a reflector at the end to return the current back through the rotors, each letter is transposed many times. When using the Enigma machine, three rotors are selected from five available ones (there were also machines with four rotors). The reflector's transposition setting is fixed, ensuring that the current returns back through the machine without reversing the transposition.

So how is the path of the current flowing through these components changed?

### Movement of the rotors

So that a different transposition is used character by character, the first rotor advances step-wise as each letter of the message is typed, creating a new path for the current each time. As a result, the user can type in 'LL' and both letters will be encrypted differently, so the result might be 'XV'. After the first rotor has moved 26 positions (one full revolution), the machine starts advancing the next rotor position by position, and so on.

### Rotor start positions

Part of what makes the Enigma encryption difficult to break is the fact that each rotor can be used at a different starting position. For example, if a rotor is set to position 10 at the beginning and the letter A is typed into the machine, it will enter not where A enters by default, but where J (letter 10 in the alphabet) enters by default. Note that a rotor will advance 26 steps no matter what its start position is.

So that it can be set more easily, the rotor is marked by an alphabet ring. Hence a start position of 10 would be achieved by setting the rotor so that the letter J is visible; the 3-rotor start position "JFM" would mean setting the first rotor to J, the second to F, and the third to M.

### Slip rings

On top of that, the letter assignments can be shifted by slipping round ring on the rotor. Rotating the slip ring rotates the wiring **inside** the rotor. For example, let's say that with the slip ring in default position, the rotor's wiring would transpose A into E, B into K, C into M, and so on. Moving the slip ring by 1 would mean that the letter A would be transposed into K, B into M, etc.

### Plugboard

As if this wasn't enough, the German version of the Enigma machine also features a plugboard (the leftmost green box in the diagram at the top), which can be manually adjusted so that up to ten pairs of letters are transposed as they go into the rotors and again when they come back out.

### Encryption settings

Combining three rotors from a set of five, the rotor settings with 26 positions, and the plugboard with ten pairs of letters connected, the Enigma machine used by WWII military had 158962555217826360000 (nearly 159 quintillion) different settings.

The encryption relied on both the sending and receiving Enigma machines being set the same. To do this, secret identical settings sheets were used at both the sending and receiving communicating stations. The sheets specified:
- Which rotors should be selected, and in what order they should be inserted into the machine
- How much each rotor should be slipped round
- Which letters should be changed by the plugboard
- Which rotor start positions should be used

Different machine settings was used each day, and the rotor start positions were even changed every six hours, so the machine setting was highly time-sensitive. This is also why the settings sheets the military handed out were so carefully guarded.

![A captured Enigma settings sheet held by GCHQ](images/Enigma-settings-sheet.jpg)

### Settings sheet

This is an Enigma settings sheet captured at the end of WWII, which GCHQ has released for this project. In the expanded view of one of the lines shown below, you can see how the various settings are laid out:

![A line of settings from a WWII captured Enigma settings sheet](images/Enigma-settings-line.jpg)

+ The settings we've zoomed in on are for the first day of the month, hence the "1" in the second column from the left
+ The next column shows that rotors IV, I, and V should be selected and used in that order
+ The fourth column holds the slip ring settings: rotor IV should be slipped round to position 20, rotor I to position 5, and rotor V to position 10
+ Next comes the plugboard wiring: S to X, K to U, Q to F, and so on
+ Finally, the rotor start position for the four six-hour period of the day are "SRC", "EEJ, "FNZ", and "SZK"

On top of that, there were two reflectors, B and C, one of which was chosen for use. For the encryption and decryption programs here, we will assume use of reflector B.

### One-off key

For each message during WWII, the sender also selected three characters for themselves as a one-off message key — let's say "RPF". They encrypted this key using the settings from the settings sheet and noted down the result — let's say "QMD". They would then proceed to encrypt their message using their one-off key, here "RPF", as the start positions of the rotors, noting down the cypher text the machine returns. The encrypted version of the key, here "QMD", plus the cypher text were then sent to the recipient via radio.
