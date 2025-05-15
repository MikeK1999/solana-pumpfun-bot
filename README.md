![](readme/solana-pumpfun-bot.png)

**Solana PumpFun Bot** that listens to new Pump.Fun && Raydium pools and buys tokens for a fixed amount in WSOL.
Depending on the speed of the RPC node, the purchase usually happens before the token is available on UI for swapping. This program took me two months to complete, and I hope it will be helpful to everyone looking to snipe tokens on Solana!

Note: Even for testing, besides using WSOL as the exchange token, it’s important to keep more SOL for transaction fees. The configuration example is: "1 SOL / 0.1 WSOL / QUOTE_AMOUNT=0.01" You can adjust it according to your own situation.

- `WSOL Snipe`
- `Auto-Sell`
- `TP/SL`
- `Min Liq`
- `Burn/Lock Check`
- `Renounce Check`
- `Fast Buy`

> [!NOTE]
> This is provided as is, for learning purposes.

## SETUP
To run the script you need to:
1. Download and extract the repository files: Use the command "git clone https://github.com/SolMemeLabs/solana-pumpfun-bot" or click the green "Code" button and select "Download ZIP".
2. Install the Node.js environment on your computer : https://nodejs.org/en
3. The runtime environment should be a terminal or VSCode. Detailed steps are provided below, please read carefully.
4. Convert some SOL into WSOL for trading. Note: Even if you only want to run the test for one hour, you still need to retain enough SOL, as gas fees are paid in SOL. For example (10 SOL) : (1 WSOL) : (QUOTE_AMOUNT=0.1) +-

`Jupiter Wrap` : https://jup.ag/

Click “MANUAL” to set “Use wSOL”, and finally click “Manage” to convert part of SOL to WSOL.

![](readme/jupiterwrap.png)

## CONFIG
1. Configure the script by updating `.env.example` file (**remove the .example from the file name when done**).
2. `PRIVATE_KEY` (your wallet private key)
3. `RPC_ENDPOINT` (https RPC endpoint) 
4. `RPC_WEBSOCKET_ENDPOINT` (websocket RPC endpoint)
5. `QUOTE_MINT` (Use WSOL by default)
6. `QUOTE_AMOUNT` (amount used to buy each new token)
7. `COMMITMENT_LEVEL` (No modification required)
8. `CHECK_IF_IS_BURNED` (liquidity burn check)
9. `CHECK_IF_IS_LOCKED` (liquidity lock check)
10. `USE_SNIPE_LIST` (buy only tokens listed in snipe-list.txt)
11. `SNIPE_LIST_REFRESH_INTERVAL` (how often snipe list should be refreshed in milliseconds)
12. `CHECK_IF_MINT_IS_RENOUNCED` (script will buy only if mint is renounced)
13. `MIN_POOL_SIZE` (script will buy only if pool size is greater than specified amount)
14. `TAKE_PROFIT=50` (in %)
15. `STOP_LOSS=30` (in %)
16. `BIRDEYE_API_KEY=` (TP/SL, Burn/Lock) You can use the default link in the .env file, it works fine and does not need to be changed. Go here if you want to generate it yourself : https://docs.birdeye.so/docs/authentication-api-keys

**Don't forget to check Birdeye API, if API key is not working, some bot functions such as TP/SL, Min/Max Liquidity etc may not work correctly or not work at all. If you follow the instructions there should be no errors.

![](readme/birdeye.png)

![](readme/env.png)
  
## INSTALL
1. Install dependencies by typing: `npm install`
2. Run the script by typing: `npm run buy` in terminal

![](readme/preview.png)

## TAKE PROFIT

> [!NOTE]
> By default, 50 % 

## STOP LOSS

> [!NOTE]
> By default, 30 %

## AUTO SELL
By default, auto sell is enabled. If you want to disable it, you need to:
1. Change variable `AUTO_SELL` to `false`
2. Update `MAX_SELL_RETRIES` to set the maximum number of retries for selling token
3. Update `AUTO_SELL_DELAY` to the number of milliseconds you want to wait before selling the token (this will sell the token after the specified delay. (+- RPC node speed)).

If you set AUTO_SELL_DELAY to 0, token will be sold immediately after it is bought.
There is no guarantee that the token will be sold at a profit or even sold at all. The developer is not responsible for any losses incurred by using this feature.

![](readme/token.png)

## SNIPE LIST
By default, script buys each token which has a new liquidity pool created and open for trading.
There are scenarios when you want to buy one specific token as soon as possible during the launch event.
To achieve this, you'll have to use snipe list.
1. Change variable `USE_SNIPE_LIST` to `true` 
2. Add token mint addresses you wish to buy in `snipe-list.txt` file (add each address as a new line).

This will prevent script from buying everything, and instead it will buy just listed tokens.
You can update the list while script is running. Script will check for new values in specified interval (`SNIPE_LIST_REFRESH_INTERVAL`).

Pool must not exist before the script starts.
It will buy only when new pool is open for trading. If you want to buy token that will be launched in the future, make sure that script is running before the launch.

![](readme/snipelist.png)


## COMMON ISSUES

> [!IMPORTANT]
> If you have an error which is not listed here, please create a new issue in this repository.
> To collect more information on an issue, please change `LOG_LEVEL` to `debug`.
> 
> ### EMPTY TRANSACTION
> If you see empty transactions on SolScan most likely fix is to change commitment level to `finalized`.
> 
> ### UNSOPPORTED RPC NODE
> If you see following error in your log file:  
> `Error: 410 Gone:  {"jsonrpc":"2.0","error":{"code": 410, "message":"The RPC call or parameters have been disabled."}, "id": "986f3599-b2b7-47c4-b951-074c19842bad"}`  
> It means your RPC node doesn't support methods needed to execute script.
> FIX: Change your RPC node. You can use Shyft, Helius or Quicknode. 
> 
> ### NO TOKEN ACCOUNT
> If you see following error in your log file:  
> `Error: No SOL token account found in wallet:`  
> it means that wallet you provided doesn't have USDC/WSOL token account.
> FIX: Go to dex and swap some SOL to USDC/WSOL. When you swap sol to wsol you should see it in wallet.

## CONTACT

The program has undergone multiple audits and tests, demonstrating strong profitability. If you have any suggestions, please contact:

Discord: `@mikek_1999`

- If this program is helpful to you, please click the sponsor button to give your love!

## DISCLAIMER

> [!IMPORTANT]
> Use this script at your own risk.
