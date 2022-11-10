# HTML NFTs on Solana
Patterns, guidelines, and example HTML projects with a focus in creating interactive NFT art.

The inspiration behind this project comes from wanting the ability to generate interactive NFT artworks and experiences on [Solana](https://solana.com/)/[Exchange.art](https://exchange.art/). I want to share my findings in hopes of inspiring other creators as well.

![bitsweeper demo](/doc/bitsweeper.gif)

**Disclaimer:** HTML NFTs will only be interactive on platforms that support them such as Exchange.art. You can provide a fallback image/gif to be played on unsupported platforms such as when viewing in wallet.

## Support
- 🐤[Twitter](https://twitter.com/_qudo)
- 💬[Discord](https://discord.gg/Uxnskhy6yd)

## Demos
- [Bitsweeper](https://exchange.art/series/Bitsweeper/nfts): An HTML NFT game I created. Notice the GIFs playing on the first page, but once you click into the NFT you can play the game right on the NFT itself.
- [Code Dreams](https://exchange.art/series/Bitsweeper/nfts): Randomly generated visuals that you can manipulate.

## ❔FAQ
### Is this gonna be difficult?
Not too bad, this guide will be high level concepts using HTML/CSS/JS. The goal of this project is to inspire creators to try new things and make some of the complicated things around interactive NFTs more simple. You can always take it further and build something next level or ask questions in the community if you get stuck.

### Is this guide only for NFTs?
Nope, not at all. While this guide will give you a great launch pad for deploying your art as an NFT, the output is nothing more than a normal `.html` file you can use for anything.

# ✅ Getting Started
Before you dive in any deeper, make sure you understand what HTML is and how to create an HTML file and open it in a browser. At minimum you'll need very basic HTML/CSS knowledge to produce visuals.

### Learn HTML/CSS/JavaScript
A good place to start is [FreeCodeCamp](https://www.freecodecamp.org/). You can also join the Discord for additional resources.

## Computer Setup
If you don't already have it, download and install [VSCode](https://code.visualstudio.com/download) to make life easier. It's a lightweight text editor that makes code files look pretty.

## New Project Setup
Here's how you can setup a new HTML project from scratch.
1. Wherever you keep projects on your computer, make a new folder for your project. It can be empty for now.
2. Launch VSCode, click File -> Open Folder... and open the folder you just made.
3. Once the folder is open in VSCode, click the add file icon at the top of the left sidebar and add a new file called `index.html`.
4. Copy/paste one of the example templates at the bottom of this page into `index.html`.

**Note:** Make sure you save your changes (Ctrl or Cmd + S). If a file has a white dot on its tab at the top of VSCode then that means you have unsaved changes.

## Preview Project
The easiest way to preview your `index.html` would be to find it on your computer and double click it which opens it in your default web browser.

**Note:** When you save changes in VSCode, you will have to refresh the web browser page in to see them.

# 🚀 Mint/Deploy
## Exchange.art
- When ready to deploy your art as an NFT, visit [Exchange.art](https://exchange.art/) and setup an account.
- Click the "Create" menu at the top and when asked to pick a file, select your `index.html` file as the main NFT file.
- Exchange.art will then prompt you to select a fallback/cover file. I usually take a screen recording of my HTML experience and then use this [video to GIF](https://www.onlineconverter.com/video-to-gif) to produce a gif to upload.

### Things to Consider
- Ensure your HTML project looks good even on as small as 300x300px screen size.
- When your NFT is in review you will not see the HTML preview, you'll only see the cover image. Once approved, your NFT will be viewable as the HTML version.

# Generative Art
This is potentially a way to create a [Candy Machine](https://docs.metaplex.com/programs/candy-machine/) like experience on Exchange.art without having to generate and upload all of your artwork and metadata ahead of time. Instead, the NFT generates itself in real time based on its own mint address as users load it.

![tweet](/doc/tweet.png)
I recently reached out to Exchange.art requesting a feature and they responded quickly. Thanks [@tiboprea](https://twitter.com/tiboprea)!

## General Concept
A mint address on Solana will look something like...
```
GTtbMPejvDUWjwzyDuf4maw3D3pu6R228u63rGWjiaB6
```

### How do we turn that into attributes? 
I am sure there's many ways to do this (please let me know more) but here's what I am thinking...

Say we have the following PFP project and attributes.
|Face|Body|Color|
|-|-|-|
|Happy|Big|Red|
|Mad|Small|Green|
|Sad||Blue|

1. Slice up the mint address into as many chunks as number of attributes.
   
![mint slice](/doc/mint-sliced.png)

1. Convert characters to their corresponding UTF-16 character code.
   
![mint slice](/doc/mint-codes.png)

1. Sum up each chunk of character codes.
   
![mint slice](/doc/mint-sum.png)

1. Now we need to create a scale for each chunk that starts at 0 and ends at the highest possible number. From there we can see where each attribute chunk falls on the scale. We can create the upper bounds of the scale by multiplying the highest possible character code by the amount of characters in a chunk. So in this case, `14 * 122`. From there we can do `Characer Sum (step 3) / Highest Possible Sum = Result`.
   
![mint slice](/doc/result.png)

## 
And there we go! We have determined a set of attributes from a list based on a particular mint address. To see a JavaScript implementation of this concept check out the **Generative Art** template below. 

# 🛠 Templates
## My First HTML Page
A simple example of the general structure of a HTML file.
 - The stuff in `<body></body>` is what shows up on the page. Here's a [HTML cheat sheet](https://htmlcheatsheet.com/).
 - The stuff in `<style></style>` is CSS, and it's used to select things in the HTML and style it. Here's a [CSS cheat sheet](https://htmlcheatsheet.com/css/).
 - The stuff in `<script></script>` is JavaScript. This is logic and things to do when users perform actions. This example shows a message. Here's a [JS cheat sheet](https://htmlcheatsheet.com/js/).
 - Stuff that looks like `<!-- some words -->` is a comment and won't show up.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <!-- Add a font from https://fonts.google.com/ -->
    <link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk&display=swap" rel="stylesheet">    

    <!-- Add styles -->
    <style>
        body,
        html {
            margin: 0;
        }

        html {
            --green: #00FF75;
            --white: #e7e7e7;
            --black: #080808;
        }

        body {
            background: var(--black);
            color: var(--white);
            font-family: 'Space Grotesk', sans-serif;
        }

        main {
            max-width: 400px;
            margin: 0 auto;
            display: flex;
            align-items: center;
            flex-direction: column;
            padding: 2rem;
        }

        button {
            appearance: none;
            border: 1px solid var(--white);
            border-radius: 1rem;
            padding: 0.5rem 1rem;
            background: var(--white);
            cursor: pointer;
        }

        .icon {
            width: 25%;
        }
    </style>
</head>

<!-- HTML to show on the page -->
<body>
    <main>
        <svg class="icon" viewBox="0 0 539 555" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path fill-rule="evenodd" clip-rule="evenodd" d="M393.397 231.528C396.788 236.846 395.35 244.038 390.162 247.53L340.752 280.922C338.843 282.217 336.732 282.819 334.598 282.819C330.96 282.819 327.366 280.992 325.21 277.616C321.796 272.274 323.256 265.105 328.422 261.613L377.855 228.198C383.02 224.706 390.005 226.139 393.397 231.528ZM253.206 171.518L278.158 116.365C280.763 110.538 287.456 108.04 293.071 110.746C298.686 113.451 301.156 120.296 298.506 126.101L273.554 181.277C271.645 185.463 267.602 187.937 263.38 187.937L258.641 186.85C253.026 184.191 250.578 177.299 253.206 171.518ZM194.273 185.694C225.199 124.366 227.602 67.6638 201.415 17.205C197.417 9.50438 202.897 0.23125 211.319 0.23125C215.295 0.23125 219.202 2.42812 221.246 6.33625C251.117 63.9175 248.759 127.835 214.194 196.354C212.195 200.309 208.287 202.575 204.222 202.575C202.47 202.575 200.718 202.159 199.056 201.28C193.554 198.343 191.398 191.359 194.273 185.694ZM539 313.482C539 321.622 531.117 327.08 523.93 324.351C460.864 300.579 405.929 305.366 360.628 338.481C358.652 339.938 356.384 340.631 354.115 340.631C350.634 340.631 347.175 338.943 344.997 335.775C341.403 330.595 342.571 323.357 347.625 319.68C399.303 281.824 461.246 276.113 531.633 302.637C536.193 304.348 539 308.788 539 313.482ZM168.781 253.173L233.127 427.003L182.639 449.296L120.808 275.581L138.282 225.261L168.781 253.173ZM253.79 417.915L205.098 286.403L317.956 389.61L253.79 417.915ZM68.0516 427.604L90.2638 490.019L38.4503 512.889L68.0516 427.604ZM108.995 309.597L161.954 458.407L110.949 480.908L79.8652 393.564L108.995 309.597ZM0 555L359.281 396.524L128.332 185.231L0 555ZM459.517 193.579L471.914 177.531L478.225 196.979L496.889 204.124L480.875 216.334L480.022 236.823L463.784 224.891L444.604 230.394L450.623 210.831L439.595 193.741L459.517 193.579ZM428.433 214.045L414.082 260.734L459.921 247.599L498.641 276.043L500.64 227.134L538.91 198.043L494.329 180.953L479.236 134.518L449.702 172.859L402.133 173.253L428.433 214.045ZM379.764 117.059C393.082 116.041 400.516 113.798 403.885 109.774C407.838 105.057 408.961 94.8125 407.591 76.6363C407.074 70.2538 411.701 64.6806 417.9 64.1719C424.121 63.8019 429.466 68.3344 429.96 74.7169C431.375 93.3556 431.285 112.179 420.932 124.574C411.297 136.114 395.553 138.496 381.403 139.536C365.637 140.739 365.233 145.156 364.02 159.84C362.762 175.334 360.606 200.17 322.695 204.541C299.854 207.2 290.511 212.172 291.768 249.773C291.948 256.132 287.119 257.289 280.898 257.289H280.539C274.497 257.289 269.511 256.78 269.309 250.559C268.209 216.774 273.599 189.163 320.179 183.798C339.809 181.508 340.393 174.455 341.65 159.008C342.863 144.323 344.907 119.695 379.764 117.059ZM497.989 46.5737C508.186 46.5737 516.473 55.13 516.473 65.6288C516.473 76.1275 508.186 84.6606 497.989 84.6606C487.793 84.6606 479.483 76.1275 479.483 65.6288C479.483 55.13 487.793 46.5737 497.989 46.5737ZM497.989 107.786C520.583 107.786 538.933 88.8925 538.933 65.6288C538.933 42.365 520.583 23.4719 497.989 23.4719C475.373 23.4719 457.024 42.365 457.024 65.6288C457.024 88.8925 475.373 107.786 497.989 107.786ZM308.298 23.1019C320.696 23.1019 330.758 33.485 330.758 46.2038C330.758 58.9456 320.696 69.3056 308.298 69.3056C295.901 69.3056 285.839 58.9456 285.839 46.2038C285.839 33.485 295.901 23.1019 308.298 23.1019ZM308.298 92.4306C333.071 92.4306 353.194 71.7106 353.194 46.2038C353.194 20.6969 333.071 0 308.298 0C283.503 0 263.38 20.6969 263.38 46.2038C263.38 71.7106 283.503 92.4306 308.298 92.4306Z" fill="var(--green)"/>
        </svg>
        <h1>
            My HTML Page
        </h1>
        <button id="someButton">
            Click Dis
        </button>
    </main>
</body>

<!-- JavaScript to run on the page -->
<script>
    // Find the button element on the page
    const buttonElement = document.getElementById("someButton");

    // Make it do something when you click it. In this case, trigger an alert.
    buttonElement.addEventListener("click", () => alert("Cool! It worked!"));
</script>
</html>
```