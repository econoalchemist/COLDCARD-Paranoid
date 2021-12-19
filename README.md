# ColdCard Paranoid Guide
A paranoid guide for advanced users with a focus on security, privacy, & verification to ensure their self-custodied cold storage wallet is ready for adversarial environments. 

<p align="center">
  <img width="756" height="406" src="Assets/ParanoidTitleImage-M.png">
</p>

This guide covers:
- Checking the tamper-evident bag
- Verifying & updating firmware
- Setting up a PIN
- Verifying the dice roll math
- Generating a seed phrase with 256 bit of entropy by dice rolls
- Creating a passphrase
- Air-gapped communication between ColdCard and [Sparrow Wallet](https://www.sparrowwallet.com/)
- Steel plate backup demonstration

## Checking the tamper-evident bag:
Upon receiving your ColdCard, ensure that the tamper-evident bag has not been compromised. If anything seems amiss or if you have any problems contact [support@coinkite.com.](mailto:support@coinkite.com?subject=%5BContact%5D%20-%20). Visually inspect the surfaces and edges of the bag for indications of tampering, openings, or damage. The concern is being victim of a supply chain attack in which your ColdCard gets intercepted in transit and modified in a way that puts your funds at risk. Ensuring the integrity of the tamper-evident bag is the first step in mitigating this type of sophisticated attack. 

<p align="center">
  <img width="400" height="300" src="Assets/Bag0.png">
  <img width="400" height="300" src="Assets/Bag1.png">
</p>

<p align="center">
  <img width="400" height="300" src="Assets/Bag2.png">
  <img width="400" height="300" src="Assets/Bag3.png">
</p>

You will see the tamper-evident words "void" appear when the seal is opened. Inside you will find your new ColdCard, the Wallet Recovery Backup Card, sticker(s), and an additional copy of the bag number which should match the bag number printed on the outside of the bag. 

<p align="center">
  <img width="388" height="208" src="Assets/IMG_6079.JPG">
  <img width="399" height="277" src="Assets/IMG_6080.JPG">
</p>

If everything looks good, then you are ready to power on your new ColdCard and get it setup. Here is a diagram you can reference to learn the ColdCard's navigation:

<p align="center">
  <img width="853" height="505" src="Assets/Navigation.png">
</p>

## Verifying & updating firmware
A great security feature of the ColdCard is that it can be used completely air-gapped. Meaning that you never have to connect it to a computer, although the option to is there if you choose to use it. You can use a standard USB outlet transformer or even a 9v battery with the ColdPower adaptor, which CoinKite offers [here](https://store.coinkite.com/store/cldpwr). To power on the ColdCard simply connect a USB to micro-USB [cable](https://store.coinkite.com/store/category/accessories) to the port on top of the ColdCard and the other end to a USB port on your ColdPower adaptor & 9v battery.

<p align="center">
  <img width="403" height="302" src="Assets/IMG_5557.JPG">
  <img width="403" height="302" src="Assets/IMG_5556.JPG">
</p>

Stay up to date on firmware releases, follow the Twitter account [@COLDCARDwallet](https://twitter.com/COLDCARDwallet), or bookmark the [Coinkite Blog](https://blog.coinkite.com/). Firmware upgrades provide new features, enhancements, bugfixes, and the latest security updates to your ColdCard. Firmware upgrade files have a `.dfu` file extension and should be approximately 690 kB in size. The abbreviation should be `20...-coldcard.dfu` to represent the full firmware file name. Make sure to use the full file name in your commands. ColdCards only load and run files signed by a CoinKite approved key.

Once powered on, first read and accept the terms of sale & use. Then you will be asked to confirm the bag number. If there are any discrepancies, contact [support@coinkite.com](mailto:support@coinkite.com?subject=%5BContact%5D%20-%20).

<p align="center">
  <img width="605" height="454" src="Assets/BagNumber.jpg">
</p>

Next, figure out which firmware version the ColdCard currently has on it by selecting `Advanced` and then scroll down to `Upgrade Firmware` and finally `Show Version`. If your displayed firmware version is older than the most recent version available on the CoinKite website [here](https://coldcard.com/docs/upgrade), then follow the next steps to upgrade. 

<p align="center">
  <img width="403" height="302" src="Assets/Advanced.jpg">
  <img width="403" height="302" src="Assets/UpgradeFirmware.jpg">
</p>

<p align="center">
  <img width="403" height="302" src="Assets/ShowVersion.JPG">
  <img width="403" height="302" src="Assets/VersionNumber.JPG">
</p>

Even the firmware can be upgraded air-gapped by utilizing the microSD card. These steps will show you how to do that and verify the integrity of the firmware file on a Windows desktop using Kleopatra OpenPGP from the [GPG4win](https://www.gpg4win.org/download.html) bundle. If you are using a Linux distrobution, you will want to use [GnuPG](https://gnupg.org/download/index.html). Or if you are using a Mac, you will want to use [GPGtools](https://gpgtools.org/). You can also watch [this video tutorial](https://youtu.be/RYcB5HpfcaE). The basic process here is to save the PGP signed hash value of the `.dfu` firmware file and verify it with [Doc Hex's PGP public key](https://twitter.com/dochex) and then calculate your own hash value on the firmware to confirm. 

From the CoinKite [website](https://coldcard.com/docs/upgrade), click on the link for the latest firmware version at the top of the page. This will automatically download a .dfu file. 

<p align="center">
  <img width="938" height="713" src="Assets/Firmware2.png">
</p>
  
From that same web page, scroll down towards the bottom to the advanced section and then click on the `this clear-signed text file` link. That link will open a PGP signed message containing the SHA256 hash values of various firmware versions.

<p align="center">
  <img width="403" height="302" src="Assets/Firmware3.png">
  <img width="403" height="302" src="Assets/Firmware4.png">
</p>

You want to save this PGP signed message as an `.asc` file, you can just hit `ctrl+s` from your web browser and you should be presented with a pop-up window like the one below. Make sure you have the `All Files (*.*)` option selected from the `Save as type:` drop-down menu. And then save the file with the `.asc` extension. You can leave it named `signatures`. 

<p align="center">
  <img width="948" height="532" src="Assets/Firmware5.png">
</p>
  
Next, you need to get Doc Hex's public PGP key and import it to your Kleopatra keychain so you can certify it. Doc Hex's public key can be copied from this keyserver [here](https://keyserver.ubuntu.com/pks/lookup?op=get&search=0xA3A31BAD5A2A5B10).

Once you copy his public key to your clipboard, then in Kleopatra navigate to `Tools` then `Clipboard` then `Certificate Import`. You will then be asked for your PGP password to certify DocHex's public key. Once certified, this public key will be added to your keychain.

<p align="center">
  <img width="950" height="499" src="Assets/Firmware7.png">
</p>
  
You can confirm that the finger print of the public key you just imported for Doc Hex matches the fingerprint of the Doc Hex account from KeyBase [here](https://keybase.io/dochex).

<p align="center">
  <img width="950" height="681" src="Assets/Firmware6.png">
</p>

Now that you have Doc Hex's key imported and certified, you can verify that the signed message with the firmware hash values was actually signed by Doc Hex. Open the folder containing the signed message `.asc` file and right click on it, then select `More GpgEX options` then `Verify`.

<p align="center">
  <img width="833" height="669" src="Assets/Firmware10.png">
</p>

Kleopatra will start calculating the veracity of the signature and after a moment, you should receive a dialog box confirming that the signature matches the public key you certified. 

<p align="center">
  <img width="651" height="521" src="Assets/Firmware11.png">
</p>

At this point, you have verified that the PGP signed message containing the hash values for the firmware files was in fact signed by Doc Hex. But you now need to verify that the `.dfu` firmware file does in fact return the same hash value as the one in the signed message. 

To do this, a freeware hex editing program called [HxD](https://mh-nexus.de/en/hxd/) is a user-friendly tool. Once the application is downloaded and launched, simply navigate to `File` then select `Open` and navigate to the file path where you have the firmware `.dfu` file saved. Once opened, then navigate to `Analysis` then `Checksums` then scroll down to `SHA-256` and hit `OK`. Then the software will return the calculated Sha256 hash value on the firmware file you downloaded. Visually compare this returned hash value with the hash value that you can look at in the signed message by opening it with a text editor.

<p align="center">
  <img width="315" height="183" src="Assets/Firmware12.png">
  <img width="315" height="187" src="Assets/Firmware13.png">
  <img width="315" height="208" src="Assets/Firmware14.png">
</p>

Now you know that the firmware file you downloaded is an exact match to the file that CoinKite intended on you receiving and that it is safe to install on your new ColdCard. 

Using a microSD card (up to 32 GB capacity, FAT32 or FAT12 format) and a USB adaptor, insert them into your desktop. Once recognized, just drag and drop the firmware `.dfu` file onto the microSD card. Then safely eject the microSD card.

<p align="center">
  <img width="425" height="212" src="Assets/IMG_6248.JPG">
  <img width="425" height="296" src="Assets/Firmware15.png">
</p>

Turn the ColdCard over and insert the microSD card into the slot until it clicks in place. 

<p align="center">
<img width="900" height="675" src="Assets/IMG_6249.JPG">
</p>

You should still be in the `Advanced` menu, then scroll down to `Upgrade Firmware` then `From MicroSD` then select the firmware file. This will take a moment to automatically load, verify and upgrade. 

<p align="center">
  <img width="403" height="302" src="Assets/FromMicroSD.JPG">
  <img width="403" height="302" src="Assets/PickFirmWare.jpg">
</p>

<p align="center">
  <img width="403" height="302" src="Assets/FirmwareFile.JPG">
  <img width="403" height="302" src="Assets/Loading.JPG">
</p>

With the firmware now upgraded, you're ready to move on and set your PIN number. 

## Setting up a PIN
Make careful considerations with your PIN number. You don't want to use one that is easy to guess. Your PIN will have two parts, a prefix and suffix. The idea is that once you enter the prefix, you will be presented with two anti-phishing words. If the words are the same as the words that were originally presented to you at initial startup, then you know that your ColdCard has not been tampered with since the last time you accessed it. 

First, select `Choose PIN Code`, then you will see a brief description of how the PIN code works. Each part of your PIN code can be between 2 and 6 digits. There is absolutely no way to access a forgotten or lost PIN. Also, if you enter a PIN incorrectly too many times, it will brick your ColdCard as a security feature.

<p align="center">
  <img width="605" height="454" src="Assets/Choose PIN.jpg">
</p>

After hitting `OK` you will get one more warning about the risk of losing or forgetting your PIN. After reading that, you can enter your PIN prefix. Use the included notecard to write down your PIN prefix then hit `OK`. 

<p align="center">
  <img width="454" height="341" src="Assets/EnterPreFix.jpg">
  <img width="454" height="341" src="Assets/EnterPreFix2.jpg">
</p>

Next you will be presented with your two anti-phishing words. Write these down on your notecard.

<p align="center">
  <img width="605" height="454" src="Assets/AntiPhishingWords.jpg">
</p>

Next, enter your PIN suffix, then write it down on the notecard and hit `OK`.

<p align="center">
  <img width="454" height="341" src="Assets/EnterSuffix.jpg">
  <img width="454" height="341" src="Assets/EnterSuffix2.jpg">
</p>

Then you will be asked to re-enter your PIN prefix, confirm the two anti-phishing words, and enter your PIN suffix. The ColdCard will save that information and then open up the wallet where you can generate your test seed phrase for verifying the dice roll math before generating your real seed phrase.

## Verifying the dice roll math
In this section you will see how to verify that the ColdCard dice roll math is doing what it purports to be doing. Understanding that it is not advisable to use your actual dice rolls to validate the dice-roll math is important. Meaning that a user only should enter a few dice rolls, write them down, and generate the list of 24-words and then verify that information. This is only to satisfy one's curiosity that the ColdCard is producing a list of seed words that accurately represent the random dice rolls that the user entered. Once that curiosity has been satisfied, then the process should be repeated without typing the dice rolls into a computer. This could potentially result in loss of funds if any of the user's computer systems have been compromised. Typing seed words or dice rolls for an actual wallet that the user plans to fund is a bad idea. Simply use this information as a guide to understand that the ColdCard is doing what it purports to be doing and then do the actual wallet creation with information that is never typed into the computer. Another resource for the dice roll math verification can be found [here](https://coldcardwallet.com/docs/verifying-dice-roll-math).

First, navigate to `Import Existing` then `Dice Rolls`.

<p align="center">
  <img width="454" height="341" src="Assets/IMG_E4804.JPG">
  <img width="454" height="341" src="Assets/IMG_E4805.JPG">
</p>

Once there, the "0 rolls" screen will always be displayed with the hash value, `e3b0c... 27ae4... b855` since that is sha256 over an empty string. The keys 1-6 on the ColdCard can be used to enter the values that correspond to the results of each dice roll.

<p align="center">
  <img width="605" height="454" src="Assets/IMG_E4806.JPG">
</p>

Write down each dice roll as it is entered into the ColdCard. Do as many rolls as it takes to satisfy your curiosity. In this example, 100 dice rolls. 

<p align="center">
  <img width="605" height="454" src="Assets/IMG_E4812.JPG">
</p>

With a pen & notepad, start rolling the dice, writing down the number 1-6, and entering the number on the ColdCard. Repeat 50 times for 128 bits of entropy or 99 times for 256 bits of entropy. Entropy is calculated by using log2(6^99) = 255.9.

Now that the dice rolls have been copied to the notebook and entered into the ColdCard, see what 24-word seed phrase the ColdCard comes up with by selecting `OK` on the ColdCard, the list of 24-words should then be presented. Also write these along with the dice rolls.

<p align="center">
  <img width="900" height="644" src="Assets/DiceRollTest.png">
</p>

I did the following on a RaspberryPi in the CLI shell. The idea with the following command is to verify the sha256 has value of the entered dice roll. In my example, my dice roll was 100 numbers in length and the resulting hash value was a match compared to the one displayed on the ColdCard when I reached 100 rolls. So enter the following command in your terminal replacing `123456` with the dice rolls your wrote down. 

`$ echo -n 123456 | sha256sum`

<p align="center">
  <img width="687" height="112" src="Assets/DiceRollTest1.png">
  <img width="900" height="430" src="Assets/DiceRollTest1.png">
</p>

Now it has been verified that resulting hash value displayed on the ColdCard does in deed represent the numbers from the entered dice rolls. But how do we know the hash value really generates the same 24 words?

The ideal environment to perform this checking is a computer running Tails - [The Amnesic Incognito Live System](https://tails.boum.org/), preferable without any network connection and no hard drives. Do not use your actual dice rolls on a normal desktop system as that will completely comprise the security of your ColdCard!

Simply navigate to: https://coldcardwallet.com/docs/rolls.py and save the script. From the command line terminal, change directories to where you saved it. Once there, run the following command with same dice rolls used on the first command, again replacing '123456' with the dice rolls you wrote down.

`$ echo 123456 | python3 rolls.py`

The returned data will be a list of 24 words that should match the ones written in the notebook.

<p align="center">
  <img width="691" height="516" src="Assets/DiceRollSeed.png">
</p>

Now the 24-word seed phrase has been independently verified and the ColdCard can be trusted to be doing what it purports to be doing. Once your curiosity has been satisfied that everything is working as expected and advertised, now repeat the process with you actual dice rolls on the ColdCard and do not enter them into the computer when you're done.

## Generating a seed phrase
There are a couple considerations you may want to make when creating a seed phrase. For example, ColdCard will generate a seed phrase for you by default, as shown in the [Ultra Quick guide](https://github.com/econoalchemist/ColdCard-UltraQuick). However, maybe you don't trust the True Random Number Generator (TRNG) in your ColdCard, you can introduce some of your own randomness using a six sided dice and combine that with the ColdCard's TRNG entropy as demonstrated in the [Middle Ground guide](https://github.com/econoalchemist/ColdCard-MiddleGround). In this guide though, you'll see how to generate a full 256 bits of entropy with dice rolls now that you know the ColdCard is not up to any funny business.

Starting at the ColdCard main menu. Select `New Wallet` and after a moment you will be presented with 24 words. However, to add some of your own dice roll randomness, scroll down to the bottom of the word list and select `4` to add some dice rolls.

<p align="center">
  <img width="454" height="341" src="Assets/NewWallet.jpg">
  <img width="454" height="341" src="Assets/AddEntropy.jpg">
</p>

Entropy is calculated by using: log2(6) = 2.58. Where the 6 is the number of sides on the dice. For reference, it would take the world's most powerful super computer trillions of years to brute force a 256 bit key. Roll the dice and enter the corresponding number for each roll. Repeat this process at least 99 times for the full 256 bits of entropy.

<p align="center">
  <img width="804" height="605" src="Assets/ZeroRolls.jpg">
  <img width="804" height="605" src="Assets/NintyNinerolls.jpg">
</p>  

Now you will be presented with a new list of 24 words. Write these words down on your notecard. Then double check your work. 

<p align="center">
  <img width="454" height="341" src="Assets/SaveWords1.jpg">
  <img width="454" height="341" src="Assets/SaveWords2.jpg">
</p>

Next, you will be asked to take a test to prove you wrote the words down correctly. 

<p align="center">
  <img width="806" height="605" src="Assets/Test.jpg">
</p>  

After passing the test, you will be at the ColdCard's main menu. Your ColdCard is ready to start receiving deposits, next we'll set it up as a "watch-only" wallet in Sparrow Wallet and demonstrate how to transact in an air-gapped fashion. If you are interested in adding the additional security of a passphrase to your ColdCard wallet, then check out the [Paranoid guide](https://github.com/econoalchemist/ColdCard-Paranoid).

## Connecting ColdCard to Sparrow Wallet
Sparrow Wallet is a Bitcoin wallet designed to be connected with your own node and ran from your desktop or laptop computer. This is a user-friendly wallet with an intuitive interface and many advanced features for a range of capabilities. To learn more about Sparrow Wallet and for installation instructions, visit the [Sparrow Wallet website](https://www.sparrowwallet.com/).

In this guide you will see how to connect your ColdCard to Sparrow Wallet using a your own BitcoinCore node. If you don't have your own Bitcoin node, you can use reputable public Electrum servers as demonstrated in the [UltraQuick guide](https://github.com/econoalchemist/ColdCard-UltraQuick). However, there are privacy tradeoffs that come with using the convenience of a public Electrum server. Luckily there are a number of resources avilable to help you spin up your own Bitcoin node, to learn more check out:

- [Bitcoin.org](https://bitcoin.org/en/bitcoin-core/)
- [Ministry of Nodes](https://www.ministryofnodes.com.au/) 
- [Soarrow Wallet Documentation](https://www.sparrowwallet.com/docs/connect-node.html)  
