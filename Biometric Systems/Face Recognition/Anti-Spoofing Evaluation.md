The anti-spoofing evaluation aims to measure the ability of the system to recognize a fake probe.

One possible measure is the Spoof False Acceptance Rate (SFAR), that is the number of spoof attacks that are falsely accepted.

We have to consider also how many times we have a false rejection over a genuine attempt that was misclassified as a spoof for the SFAR.

There are two other measures that are:

- **FLR - False Living Rate**: percentage of spoofing attacks miscalssified as real;
- **FFR - False Fake Rate**: percentage of real access misclassified as spoofing.

Sometimes is a good idea to fuse recognition and anti-spoofing into a single system with a single accept-reject response.

## FATCHA

FATCHA is a variation of the CAPTCHA, that require the user to perform a face gesture or pose in order for the system to verify if the user is human or is a bot. It’s more simple since it allows the user to perform an action instead of recognizing a word difficult to read.