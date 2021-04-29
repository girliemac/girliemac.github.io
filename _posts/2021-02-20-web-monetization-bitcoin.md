---
title: Support Web Monetization and HODL! — How to receive micropayment in $BTC (or $Ɖoge) on your website
author: Tomomi Imura
layout: post
description: Web Monetization is a web platform API that allows websites to request micropayments from users facilitated by the browser
images:
  - assets/images/articles/2021/02/doge-web-monetization-1000x420.jpg
categories:
  - bitcoin
  - cryptocurrency
  - blockchain
  - dev
  - web
  - W3C
  - api
  - monetization
---

As I am writing this on Feb 20, 2021, Bitcoin ([CRYPTO:BTC](https://www.fool.com/quote/crypto/bitcoin/btc/)) has hit a $1 trillion market cap. Investors who thought it was a joke have started jumped into the cryptocurrencies frenzy. 

Although the ideas of decentralized market and blockchain are fascinating, I didn’t think the value of BTC would increase much, so I have spent them on things like yoga pants and flights to Europe. I try not to think about how much worth it in today's rate. There are just too many what-if scenarios in my life. (BTW, the economy-class ticket I got was about 1.3 BTC. I let you figure it out.)

Now friends are asking me about advice on cryptocurrency and [Coinbase referrals](https://www.coinbase.com/join/girlie_mac), however, because I can be the worst financial advisor to ruin your life, I am not going to tell you how to invest, or even how to mine in this article, instead, I am going to tell you about **Web Monetization** and how to receive micropayments in $BTC and other currencies including various cryptocurrencies, like $DOGE if you want, through your website.

I may sound like I am selling you snake oil, but I just thought this may be a good opportunity to talk about the web standard topic. 

![doge meme](/assets/images/articles/2021/02/doge-web-monetization-1000x420.jpg)


## Web Monetization & Interledger

According to the draft submitted to W3C, [Web Monetization](https://webmonetization.org/specification.html) is an API that allows websites to request small payments from users facilitated by the browser and the user's Web Monetization provider.

In a nutshell, Web Monetization is an open web API, consists of HTML, JavaScript API, and uses the [Interledger protocol](https://interledger.org/), an open protocol for moving money and enabling payments. 

## Implementing Web Monetization 

Although implementation for browsers is straight-forward, it requires some prerequisits as currently, you need (1) a Web Monetization service provider and (2) an Interledger Protocol-enabled wallet to monetize on web.

The services I personally use to implement Web Monetization are:

1. [Coil](https://coil.com) - Web Monetization service provider
2. [Uphold](https://uphold.com/signup?referral=5f261fb476) - ILP-enabled wallet

How **Coil** works is that is checks if the website is web monetized, and if it does, stream the payment to the site. A small amount is paid by Coil members, who pay a flat fee to access exclusive content and ad-free experiences. Coil provides browser extensions for browsers including Chrome, Edge, and Firefox, while [**Puma browser**](https://www.pumabrowser.com/) is natively powered on Coil and supports Web Monetization API out of the box.

And **Uphold** is a digital wallet that allows you to receive payments with an Interledger payment pointer. This is where you can receive the payment also sell, buy, and trade.

### Setting up Your Wallet

Coil supports multiple wallets, but I am using Uphold to generate your Interledger payment pointer here.

First, open an [Uphold](https://uphold.com/signup?referral=5f261fb476) account. 

Once you signed up and all, you are going to generate an ILP address (Interledger payment pointer). 

Go to **Transact**, then from the **Anything to Anything** (Right pane), select **From** dropdown menu:

![Screenshot - Uphold 1](/assets/images/articles/2021/02/uphold-transact-01.png)

Select **Interledger**: 

![Screenshot - Uphold 2](/assets/images/articles/2021/02/uphold-transact-02.png)

Then pick a currency of your choice— USD, BTC, ETH, XRP, DOGE… there are 27 fiat currencies and
34 Cryptocurrencies to choose from:

![Screenshot - Uphold 3](/assets/images/articles/2021/02/uphold-transact-03.png)

Copy the address that looks like `$ilp.uphold.com/SoMethIngLiKEthis0`:

![Screenshot - Uphold 4](/assets/images/articles/2021/02/uphold-transact-04.png)

You will need the address in Coil (the next step) and in your HTML code later.


### Setting up Coil

There are two membership types— [Coil membership](https://coil.com/signup) to support web-monetized content and [creator membership](https://coil.com/creator) for you to monetize. I am walking you through the latter—

First, sign up for a [**Coil creator account**](https://coil.com/creator) and click **Start monetizing. It's free** button.

Once you created your account (and verified your email etc.), you will need to set up your payout wallet. 

Go to [**Payout**](https://coil.com/settings/payouts), click **Setup** under **Uphold** (unless you chose Gatehub as your wallet):

![Screenshot - Coil 1](/assets/images/articles/2021/02/coil-payouts-01.png)

and enter the ILP address that you generated at Uphold and save:

![Screenshot - Coil 2](/assets/images/articles/2021/02/coil-payouts-02.png)

Next, you are going to include a meta tag with the information on your website to finalize.

## Monetizing Your Web

If you already have some website or web apps, you are ready to monetize. All you need is to include the `<meta>` in your head of HTML:

```html
<html>
 <head>
   <title>Welcome to My Homepage</title>
   <meta
     name="monetization"
     content="$ilp.uphold.com/6NxbkHNq9N84">
 </head>
</html>
```

Make sure to use your own ILP address as the meta content, unless you want me to receive all of your payment. Then, deploy your web and you are ready to monetize 💰

### Monetizing Your Content on Dev.to

Even if you don’t have your own websites, some content platforms do support Web Monetization. Take a look at the [list of providers](https://help.coil.com/docs/monetize/content/platforms).

For example, if you write some technical content on Dev.to like I do, you can include your ILP address to monetize your content there too. 

Sign in and go to the [**Settings**](https://dev.to/settings/misc) > **Extensions** > **Web monetization**, and enter your ILP address there and save.

![devto](/assets/images/articles/2021/02/devto-monetize.png)

That’s it. 
Now all you need is to wait to get paid in BTC (or whatever you picked) and HODL ;-)

I hope you enjoyed the article. Web platform to the moon 🚀🌕
