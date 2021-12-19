# ColdCard Paranoid Guide
A paranoid guide for advanced users with a focus on security, privacy, & verification to ensure their self-custodied cold storage wallet is ready for adversarial environments. 

<p align="center">
  <img width="756" height="406" src="Assets/ParanoidTitleImage-M.png">
</p>

This guide covers:
- Checking the tamper-evident bag
- Verifying & updating firmware
- Setting up a PIN
- Generating a seed phrase with 256 bit of entropy by dice rolls
- Creating a passphrase
- Verifying the dice roll math
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

Even the firmware can be upgraded air-gapped by utilizing the microSD card. These steps will show you how to do that and verify the integrity of the firmware file on a Windows desktop using Kleopatra OpenPGP from the [GPG4win](https://www.gpg4win.org/download.html) bundle. The basic process here is to save the PGP signed hash value of the .dfu firmware file and verify it with [Doc Hex's PGP public key](https://twitter.com/dochex) and then calculate your own hash value on the firmware to confirm. 

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

At this point, you have verified that the PGP signed message containing the hash values for the firmware files was in fact signed by Doc Hex. But you now need to verify that the .dfu firmware file does in fact return the same hash value as the one in the signed message. 

To do this, a freeware hex editing program called [HxD](https://mh-nexus.de/en/hxd/) is an easy to use tool. Simply navigate to "File" then select "Open" and navigate to the file path where you have the firmware .dfu file saved. Once opened, then navigate to "Analysis" then "Checksums" then scroll down to "SHA-256" and hit "OK". Then the software will return the calculated Sha256 hash value on the firmware file you downloaded. Visually compare this returned hash value with the hash value that you can look at in the signed message by opening it with a text editor.  

## Setting up a PIN
Make careful considerations with your PIN number. You don't want to use one that is easy to guess. Your PIN will have two parts, a prefix and suffix. The idea is that once you enter the prefix, you will be presented with two anti-phishing words. If the words are the same as the words that were originally presented to you at initial startup, then you know that your ColdCard has not been tampered with since the last time you accessed it. 

First, select "Choose PIN Code", then you will see a brief description of how the PIN code works. Each part of your PIN code can be between 2 and 6 digits. There is absolutely no way to access a forgotten or lost PIN. Also, if you enter a PIN incorrectly too many times, it will brick your ColdCard as a security feature.

<p align="center">
  <img width="605" height="454" src="Assets/Choose PIN.jpg">
</p>

After hitting "OK" you will get one more warning about the risk of losing or forgetting your PIN. After reading that, you can enter your PIN prefix. Use the included notecard to write down your PIN prefix then hit "OK". 

<p align="center">
  <img width="454" height="341" src="Assets/EnterPreFix.jpg">
  <img width="454" height="341" src="Assets/EnterPreFix2.jpg">
</p>

Next you will be presented with your two anti-phishing words. Write these down on your notecard.

<p align="center">
  <img width="605" height="454" src="Assets/AntiPhishingWords.jpg">
</p>

Next, enter your PIN suffix, then write it down on the notecard and hit "OK".

<p align="center">
  <img width="454" height="341" src="Assets/EnterSuffix.jpg">
  <img width="454" height="341" src="Assets/EnterSuffix2.jpg">
</p>

Then you will be asked to re-enter your PIN prefix, confirm the two anti-phishing words, and enter your PIN suffix. The ColdCard will save that information and then open up the wallet where you can generate your seed phrase.

## Generating a seed phrase
There are a couple considerations you may want to make when creating a seed phrase. For example, ColdCard will generate a seed phrase for you by default, as shown in the [Ultra Quick guide](https://github.com/econoalchemist/ColdCard-UltraQuick). However, maybe you don't trust the True Random Number Generator (TRNG) in your ColdCard, you can introduce some of your own randomness using a six sided dice and combine that with the ColdCard's TRNG entropy as demonstrated in the [Middle Ground guide](https://github.com/econoalchemist/ColdCard-MiddleGround). In this guide though, you'll see how to generate a full 256 bits of entropy with dice rolls and also verify the dice roll math.

After setting up the PIN, you should be at the ColdCard main menu. Select "New Wallet" and after a moment you will be presented with 24 words. However, to add some of your own dice roll randomness, scroll down to the bottom of the word list and select "4" to add some dice rolls.

<p align="center">
  <img width="454" height="341" src="Assets/NewWallet.jpg">
  <img width="454" height="341" src="Assets/AddEntropy.jpg">
</p>

Entropy is calculated by using: log2(6) = 2.58. Where the 6 is the number of sides on the dice. For reference, it would take the world's most powerful super computer trillions of years to brute force a 256 bit key. So roll the dice and enter the corresponding number for each roll. Repeat this process as much as you want. If you roll less than 50 times then the ColdCard will add the remaining necessary entropy with the TRNG. Then hit "OK".

<p align="center">
  <img width="804" height="605" src="Assets/ZeroRolls.jpg">
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
