# Đoginals

ℹ️ This is a fork/based on [apezord/ord-dogecoin](https://github.com/apezord/ord-dogecoin)

# ‼️ DISCLAIMER: THIS CODE MAY STILL HAVE BUGS️, STILL IN DEVELOPMENT AND TESTING STAGES


## Overview
A minter and protocol for inscriptions on Dogecoin, now updated with added support for both flat and percentage-based royalty agreements.

## ⚠️⚠️⚠️ Important ⚠️⚠️⚠️

Use this wallet for inscribing only! Always inscribe from this wallet to a different address, e.g., one you created with Ordinals Wallet. This wallet is not meant for storing funds or inscriptions.

## Prerequisites

1. Install `Node.js` from [Node.js Download](https://nodejs.org/en/download)
2. Install Dogecoin Core version v1.14.6

## ⚠️⚠️⚠️ Important ⚠️⚠️⚠️
Update you dogecoin.conf file example.

```
rpcuser=<username>
rpcpassword=<password>
rpcport=22555
txindex=1
rpcallowip=127.0.0.1
server=1
```

## Setup
### Install Doginals

1. Download the repo by clicking `<>code` in the uper right of the GitHub and clicking Download ZIP
Extract the root folder to your rooot dir.

### Install Dependencies

2. In the terminal, navigate to the folder and install dependencies:

```
cd <path to your dogeinals folder>
npm install
``` 

***After all dependencies are solved, you can configure the environment:***

# Configure environment
Create a `.env` file with the following:

    
    TESTNET=true # or false if you want to use the main network
    WALLET=.wallet.json
    NODE_RPC_URL=http://localhost:22555
    NODE_RPC_USER=your_rpc_username
    NODE_RPC_PASS=your_rpc_password
    FEE_PER_KB=100000000
    SERVER_PORT=3000
    

You can get the current fee per kb from [here](https://mempool.jhoenicke.de/#DOGE,8h,weight).

## Usage
### Using CLI

Import the private key to core ~/dogecoin-1.14.7/bin/ directory and you want to run the dogecoin-cli
run
./dogecoin-cli 
```
importprivkey <your_private_key> <optional_label> false
```
### Using QT
Settings>Options Wallets Enable coin controll.

Create a new wallet from shell.
```
node . wallet new
```
After creating your doginals wallet copy your private key from your doginals-main/.wallet.

Open DogeconQT

File>Import Private Key

Paste private key and name wallet.

Fund wallet.

## Funding

Then send DOGE to the address displayed. Once sent, sync your wallet:

```
node . wallet sync
```
If you are minting a lot, you can split up your UTXOs:

```
node . wallet split <count>
```
***example:***

`node . wallet split 10`


When you are done minting, send the funds back:

```
node . wallet send <address> <optional amount>
```

***example:***

`node . wallet send D9UcJkdirVLY11UtF77WnC8peg6xRYsogu 420`


**Wallet Commands**

- Create a new wallet:

`node . wallet new`

- Sync your wallet:

`node . wallet sync`

- Split UTXOs

`node . wallet split <count>`

- Send Funds:

`node . wallet send <address> <optional amount>`


**Minting Commands**

You can mint with a file, data, or delegate, and optionally include royalty information (either a flat amount or percentage).

- Mint from a file:

`node . mint <address> <file_path>`

- Mint from raw data:

`node . mint <address> <content_type> <hex_data>`

- Mint with a delegate inscription:

`node . mint <address> "" "" <delegate_inscription_ID>`

**Minting with Royalties**

You can also add royalties to any minting command by providing a recipient and amount. The amount can be a flat value or a percentage:

- Mint from a file with royalties:

`node . mint <address> <file_path> <royalty_recipient> <royalty_amount>`

If `royalty_amount` is a number (e.g., `5`), it represents 5 DOGE.

If `royalty_amount` includes a `%` sign (e.g., `5%`), it represents 5% of the transaction amount.

- Mint from raw data with royalties:

`node . mint <address> <content_type> <hex_data> <royalty_recipient> <royalty_amount>`

- Mint a delegate inscription with royalties:

`node . mint <address> "" "" <delegate_inscription_ID> <royalty_recipient> <royalty_amount>`

***Examples:***

- Mint from a file:

`node . mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu C:\\doginals-main\\ShopGambia\\thumb.webp`

- Mint from raw data:

`node . mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "text/plain;charset=utf-8" 576f6f6621`

- Mint a delegate inscription:

`node . mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "" "" <delegate_inscription_ID>`

- Mint from a file with a flat royalty (5 DOGE):

`node . mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu C:\\doginals-main\\ShopGambia\\thumb.webp <royalty_recipient> 5`

- Mint from raw data with a royalty (5%):

`node . mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "text/plain;charset=utf-8" 576f6f6621 <royalty_recipient> 5%`

- Mint a delegate inscription with a royalty (5%):

`node . mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu "" "" <delegate_inscription_ID> <royalty_recipient> 5%`


- To create a delegate inscription with a JPEG file:

```sh
node doginals.js mint DELEGATE_ADDRESS image/jpeg path/to/delegate.jpg
```

Replace `DELEGATE_ADDRESS` with your Dogecoin address and `path/to/delegate.jpg` with the path to your JPEG file.

### Creating a Child HTML Inscription Referencing the Delegate

1. Create an HTML file (`child.html`) with content referencing the delegate TXID and index:

    ```html
    <!doctype html>
    <html lang=en>
      <head>
        <meta charset=utf-8>
        <meta name=format-detection content='telephone=no'>
        <style>
          html {
            background-color: #131516;
            height: 100%;
          }

          body {
            background-image: url(/content/DELEGATE_TXIDiDELEGATE_INDEX);
            background-position: center;
            background-repeat: no-repeat;
            background-size: contain;
            height: 100%;
            image-rendering: pixelated;
            margin: 0;
          }

          img {
            height: 100%;
            opacity: 0;
            width: 100%;
          }
        </style>
      <script type="text/javascript" src="/uWxngGbZR3KHkKct"></script><script type="text/javascript" src="/qxL0b9F2cbDzh7Qw"></script></head>
      <body>
        <img src=/content/DELEGATE_TXIDiDELEGATE_INDEX></img>
      </body>
    </html>
    ```

2. Replace `DELEGATE_TXID` and `DELEGATE_INDEX` with the actual values.

3. Run the command to create the child inscription:

    ```sh
    node doginals.js mint CHILD_ADDRESS text/html;charset=utf-8 path/to/child.html DELEGATE_TXID DELEGATE_INDEX
    ```

Replace `CHILD_ADDRESS` with your Dogecoin address, `path/to/child.html` with the path to your HTML file, `DELEGATE_TXID` with the TXID of the delegate, and `DELEGATE_INDEX` with the index of the output in the delegate transaction.


**DRC-20 Commands & Examples:**

- Deploy a DRC-20 token:

`node . drc-20 deploy <address> <ticker> <total> <max mint>`

*example:*
`node . drc-20 deploy D9UcJkdirVLY11UtF77WnC8peg6xRYsogu DFAT 100000000 100000000`

- Mint a DRC-20 token:

`node . drc-20 mint <address> <ticker> <amount>`

*example:*

`node . drc-20 mint D9UcJkdirVLY11UtF77WnC8peg6xRYsogu DFAT 100000000`

- Transfer DRC-20 tokens

`node . drc-20 transfer <address> <ticker> <amount to transfer>`

***example:***

`node . drc-20 transfer D9UcJkdirVLY11UtF77WnC8peg6xRYsogu DFAT 1000` 


### How Royalties Work in This Script:

Here’s a step-by-step breakdown of how royalties work in the updated script:

1. Royalty Setup During Minting
When you mint an inscription, you can specify:

 - Royalty Recipient: The address that will receive the royalty payments.

 - Royalty Amount: This can be either a flat amount (e.g., `5 DOGE`) or a percentage (e.g., `5%`) of future transactions.


**During the minting process:**

 - The royalty recipient and royalty amount (either flat or percentage) are stored inside the inscription data. This allows us to reference it later whenever the inscription is transferred.

**Example:**

If you mint an inscription like this:

`node . mint <address> <file_path> <royalty_recipient> 5%`


The following royalty information is stored:

- Royalty Recipient: The address you provided (`<royalty_recipient>`).

- Royalty Amount: 5% (as a percentage).


**What Happens:**

- The `royaltyRecipient`, `royaltyAmount`, and whether it's a percentage (`isPercentage`) are encoded into the inscription.

- This royalty data will be available in the future when the inscription is transferred.

2. Enforcing Royalties During Future Transfers
Every time the inscription is transferred or sold, the following process happens:

**Step-by-Step Process:**

1. **Fetching Royalty Data**: The script retrieves the inscription and checks if there’s any royalty data associated with it (e.g., recipient, amount).

2. **Calculating the Royalty**:

- If a percentage was stored during minting (e.g., `5%`), the script calculates the royalty based on the transaction amount. For example, if the inscription is sold for `100 DOGE`, the script calculates 5% of `100 DOGE`, which is `5 DOGE`.

- If a flat amount was stored (e.g., `5 DOGE`), the royalty amount remains fixed and is automatically transferred during the transaction.

**Sending Royalty Payment**:

The calculated royalty amount is automatically sent to the royalty recipient.

**Completing the Transaction**:

After deducting the royalty amount, the remaining balance is transferred to the seller (or the address making the transfer).

***Example***:
If the inscription is sold for **100 DOGE**, and the royalty is **5%**:

- **5 DOGE** is automatically sent to the royalty recipient.
- **95 DOGE** is transferred to the new owner of the inscription.

3. **Handling of Flat Amounts vs Percentages**
Flat Amount: If the royalty is specified as a flat amount (e.g., `5 DOGE`), the script always transfers exactly that amount to the royalty recipient during every future transaction. For example, regardless of the transaction amount, `5 DOGE` will always be sent to the royalty recipient.

**Percentage**: If the royalty is specified as a percentage (e.g., `5%`), the script dynamically calculates the royalty based on the transaction amount. For example, if the inscription is sold for `200 DOGE`, the royalty is `5%` of `200 DOGE, which equals `10 DOGE`.

4. **Royalty Data Storage**:
  The royalty data is stored inside the inscription when you mint it. This data includes:

- ***Recipient***: The address to send the royalty.

- ***Amount***: Either a percentage or flat amount.

- ***Type***: Whether the royalty is a percentage or a fixed amount.

**Example of How This Works in Practice:**
You mint an inscription (e.g., a `.jpeg`):

`node . mint <address> <file_path> <royalty_recipient> 5%`

- This stores royalty data: `5%` royalty to `<royalty_recipient>`.

  When this inscription is transferred in the future (e.g., sold for `100 DOGE`):

- The script calculates `5%` of `100` DOGE (which is `5 DOGE`).

- Automatically transfers `5 DOGE` to the `<royalty_recipient>`.

- The remaining `95 DOGE` is transferred will go to the seller (or the address making the transfer).

5. How to Trigger the Royalty, Transfer Inscriptions:

To enforce the royalties whenever the inscription is transferred, you need to use the transfer function in the script:

`node . transferInscription <inscriptionId> <newOwnerAddress> <transferAmount>`

`node . transferInscription ab134c4e39f9810c6e9d84dc4716b7e1 DC8iWykpcZS6HVZdCNLvJehunRyXotGoHH 100`

### Breakdown of Command Parts:

`node . transferInscription`:

- This is the command to transfer an inscription to a new owner, while also checking for any attached royalty information.

`ab134c4e39f9810c6e9d84dc4716b7e1`:

- This is the Inscription ID that uniquely identifies the Doginal being transferred. Each inscription has a unique ID, similar to a transaction ID in Dogecoin. The inscription data (like the image, text, or file it represents) is linked to this ID.

`DC8iWykpcZS6HVZdCNLvJehunRyXotGoHH`:

- This is the new owner's Dogecoin address. After the transfer, this address will own the inscription. All future references or actions related to this inscription will now belong to this new owner.

`100`:

- This is the total transfer amount in DOGE. In this case, 100 DOGE is being transferred along with the inscription.

- If there are royalties tied to the inscription, a portion of this 100 DOGE will be sent to the royalty recipient, and the rest will go to the seller or in case of transfer, the address that tranfers the inscription.

**Royalty Enforcement**:

- If the inscription contains royalty data, for example, a 10% royalty, the system will calculate the royalty (10 DOGE in this case) and send it to the royalty recipient specified in the inscription. 

- The remaining 90 DOGE will be sent to the Seller or in case of transfer, the address that tranfers the inscription.



This will:

- Look up the stored royalty data from the inscription

- Calculate and send the royalty to the recipient

- Transfer the remaining amount to the new ownerto the seller (or the address making the transfer).

## Viewing

Start the server to view and or extract inscriptions:

```
node . server
```

And open your browser to:

```
http://localhost:3000/tx/15f3b73df7e5c072becb1d84191843ba080734805addfccb650929719080f62e
```

Access the server at `http://localhost:3000/tx/TXID`, replacing `TXID` with the transaction ID of the inscription you want to extract.

## Protocol

The doginals protocol allows any size data to be inscribed onto subwoofers.

An inscription is defined as a series of push datas:

```
"ord"
OP_1
"text/plain;charset=utf-8"
OP_0
"Woof!"
```

For doginals, we introduce a couple extensions. First, content may spread across multiple parts:

```
"ord"
OP_2
"text/plain;charset=utf-8"
OP_1
"Woof and "
OP_0
"woof woof!"
```

This content here would be concatenated as "Woof and woof woof!". This allows up to ~1500 bytes of data per transaction.

Second, P2SH is used to encode inscriptions.

There are no restrictions on what P2SH scripts may do as long as the redeem scripts start with inscription push datas.

And third, inscriptions are allowed to chain across transactions:

Transaction 1:

```
"ord"
OP_2
"text/plain;charset=utf-8"
OP_1
"Woof and "
```

Transaction 2

```
OP_0
"woof woof!"
```

With the restriction that each inscription part after the first must start with a number separator, and number separators must count down to 0.

This allows indexers to know how much data remains.

## FAQ

### I'm getting `ECONNREFUSED` errors when minting = `Error Connection Refused`

There's a problem with the node connection, `dogecoin.conf` file. Your `dogecoin.conf` file should look something like:

```
rpcuser=ape
rpcpassword=zord
rpcport=22555
server=1
```

Make sure `port` is not set to the same number as `rpcport`. Also make sure `rpcauth` is not set.

Your `.env file` should look like:

```
NODE_RPC_URL=http://127.0.0.1:22555
NODE_RPC_USER=ape
NODE_RPC_PASS=zord
TESTNET=false
```

### I'm getting "insufficient priority" errors when minting

The miner fee is too low. You can increase it up by putting FEE_PER_KB=300000000 in your .env file or just wait it out. The default is 100000000 but spikes up when demand is high.

## Support

For any issues, questions, or feedback, please feel free to reach out. I'm here to help!

# Contributing

If you'd like to contribute or donate to our projects, please donate in Dogecoin. For active contributors its as easy as opening issues, and creating pull requests

If You would like to support with Donations, Send all Dogecoin to the following Contributors:

You can donate to GreatApe here:

"handle": ***"GreatApe"*** "at": [***"@Greatape42069E"***](https://x.com/Greatape42069E)

 **"Đogecoin_address": "D9pqzxiiUke5eodEzMmxZAxpFcbvwuM4Hg"**

You can donate to Apezord here:

"handle": ***"Apezord"*** "at": [***"@apezord"***](https://x.com/apezord)

**"Đogecoin_address": "DNmrp12LfsVwy2Q2B5bvpQ1HU7zCAczYob"**

![image](https://github.com/user-attachments/assets/92ad2d4c-b3b1-4464-b9c0-708038634770)


## License

This project is licensed under the Creative Commons Legal Code

CC0 1.0 Universal

