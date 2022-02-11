## Generating a seed phrase with 256 bit of entropy by dice rolls
There are a couple considerations you may want to make when creating a seed phrase. For example, COLDCARD will generate a seed phrase for you by default, as demonstrated in the [Ultra Quick guide](https://github.com/econoalchemist/ColdCard-UltraQuick). However, maybe you don't trust the True Random Number Generator (TRNG) in your COLDCARD, you can introduce some of your own randomness using a six sided dice and combine that with the COLDCARD's TRNG entropy as demonstrated in the [Middle Ground guide](https://github.com/econoalchemist/ColdCard-MiddleGround). In this guide though, you'll see how to generate a full 256 bits of entropy with dice rolls now that you have verified the dice roll math is doing what it purports to be doing.

Starting at the COLDCARD main menu. Select `Import Existing` > `Dice Rolls` Once there, the `0 rolls` screen will always be displayed with the sha256 hash value of an empty string, `e3b0c... 27ae4... b855`. The keys 1-6 can be used to enter the values that correspond to the results of each dice roll.

<p align="center">
  <img width="450" src="Assets/IMG_4804.jpg">
  <img width="450" src="Assets/IMG_4805.jpg">
</p>

Entropy is calculated by using: `log2(6) = 2.58`. Where the `6` is the number of sides on the dice. For reference, it would take the world's most powerful super computer trillions of years to brute force a 256 bit key. Start rolling the dice and enter the corresponding number for each roll. Repeat this process at least 99 times for the full 256 bits of entropy.

<p align="center">
 <img width="450" src="Assets/IMG_4806.jpg">
 <img width="450" src="Assets/IMG_4812.jpg">
</p>  

Once you are satisfied with the number of rolls hit <kbd>OK</kbd>. Now you will be presented with a new list of 24 words. Write these words down in order on your notecard. Then double check your work. 

<p align="center">
  <img width="454" height="341" src="Assets/SaveWords1.jpg">
  <img width="454" height="341" src="Assets/SaveWords2.jpg">
</p>

Next, you will be asked to take a test to prove you wrote the words down correctly. 

<p align="center">
  <img width="806" height="605" src="Assets/Test.jpg">
</p>  

After passing the test, you will be at the COLDCARD's main menu, and that's it, you have generated a random 256 bit key that was used to calculate your 24-word seed phrase. Best practice at this point is to test your backup information before depositing any bitcoin. The basic idea is to use only your written backup information in an attempt to restore your wallet. If all of your backup information is correct and you successfully restore your wallet then you know that you can recover any bitcoin deposited to that wallet with that backup information. First you need a way to identify your wallet. Your newly generated wallet has a unique fingerprint which you can find from the main menu by navigating to `Advanced` > `View Identity`. You will find a unique 8-character fingerprint such as `99E870EF`. Write that fingerprint down. Now you can destroy the seed on your COLDCARD by again navigating to `Advanced` then `Danger Zone` > `Seed Functions` > `Destroy Seed`. Then you will be presented with a couple of warnings, after confirming, your seed will be destroyed and you will be brought back to the login page where you enter your PIN. Log back into your COLDCARD and from the main menu navigate to `Import Existing` > `24 words` and then start entering your seed words in order from your backup card. Start by scrolling down until you see the first letter of your word, then scroll down to the next nearest part of the word, and keep narrowing down the search until you arrive at the word you need. For example, `t` > `th` > `thr` > `throw` then hit <kbd>OK</kbd> and repeat the process for the next word. If you make a mistake, you can hit <kbd>Cancel</kbd> to go back and reselect a word. After you enter the 23rd word, COLDCARD will compute a list of 8 possible options for your 24th word. Select your 24th word from that list. If you do not see your 24th word on that list then you either made a mistake entering the first 23 words or you wrote down your backup information incorrectly. After selecting the 24th word and hitting <kbd>OK</kbd> the seed will be applied and then you can navigate back to `Advanced` > `View Identity` and confirm the fingerprint is correct. 

Once you are confident in your backup information, you can add a passphrase to your 24-words for additional security. 

