by m45t3r.1ee7

#web #businesslogic #arithmetic #novalidation
# Bug Bank Writeup

## Task Title:

Bug Bank

## Task Category:

Web

## Task Description:

Welcome to BugBank, the world's premier banking application for trading bugs! In this new era, bugs are more valuable than gold, and we have built the ultimate platform for you to handle your buggy assets. Trade enough bugs and you have the chance to become a premium member. And in case you have any questions, do not hesitate to contact your personal assistant. Happy trading!

## Goal:

Find a vulnerability in trading bugs to become a premium member.

## Walkthrough:

I singup on the given website using credentials:

Username: bbw

Password: bbw

![singup image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/SignupAccount.png)

After signing up, a home page loaded. I observed few things on home page:

- An account id
- Bugs (initially 0)
- Transfer Bugs Button
- Settings Button
- Logout Button
- Transaction History

![home page image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/home-page.png)

The Transfer Bugs and Settings buttons seemed interesting to me, so I decided to explore them.

#### Transfer Bugs:

After clicking transfer bugs button, a popup showed up.

![transfer bugs popup image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/transfer-bugs-button.png)

In order to make a transfer, I need recipient id, amount and description.

#### Settings:

After clicking settings button, a settings page loaded.

![settings page image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/settings1.png)

![settings page image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/settings2.png)

This page contains functionalities for updating user details and upgrading to premium features. To access the premium features, we require 10,000 bugs in our account.

Having explored both functionalities, I aim to discover a vulnerability in the 'transfer bugs' feature. Exploiting this vulnerability will allow me to increase my account balance to 10,000 bugs, enabling me to upgrade to premium features.

#### Basic Transfer Logic:

```
    sender_balance = sender_balance - transfer_amount

    receiver_balance = receiver_balance + transfer_amount
```

If there is no check on transfer_amount (like transfer amount should be greater than zero), then negative transfer amount will increase sender's balance and decrease receiver's balance according to above logic.

In order to test negative transfer, I need a recipient's account id. So, I created one more account using credentials:

Username: bbw2

Password: bbw2

![bbw2 home page image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/bbw2.png)

I copied the account id of bbw2.

**c0c2d396-df8b-46ab-a5a7-839b00e7c065**

I logged in again into account of bbw. I tried to transfer negative -10,000 bug from bbw to bbw2.

![successful transfer image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/transfer3.png)

Now there was 10,000 bug in bbw account.

![bbw balance image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/balance2.png)

I opened the settings page and click the upgrade button. After clicking the upgrade button, I got the flag.

![upgraded image](https://raw.githubusercontent.com/M786453/Bug-Bank-Writeup/main/upgraded.png)