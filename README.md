The repository contains two branches<br>
 -- [__contracts__]( https://github.com/DarkLord017/DTSLA.SOL) ALL DTSLA Contracts , libraries , functions and deployment stuff<br>
 -- [__Application__](https://github.com/DarkLord017/DTSLA.SOL/tree/Application) All frontend and etherjs stuff<br>

 [__Project Video__](https://drive.google.com/file/d/1cSY8fMghlA_PpNdL13cskqJiq02Lhdxf/view?usp=sharing)<br>

 __Description__<br>
 DTSLA is a ERC-20 token that is pegged to real TSLA stocks of company's alpaca account.<br>
 Features
 ![image](https://github.com/DarkLord017/DTSLA.SOL/assets/136801346/d5bfa351-4031-4204-8522-4d0da7d8e8bf)<br>
 How does it work?<br>
 ![image](https://github.com/DarkLord017/DTSLA.SOL/assets/136801346/f5236bc0-891a-44c5-baa5-84e4704312f5)<br>
 We are integrating real world tesla stocks in blockchain it reduces centralization risks as it is written in smart contracts and Chainlink functions<br>

 __Technical Description__<br>
     --Contracts<br>
               --[Dtsla.sol](https://github.com/DarkLord017/DTSLA.SOL/blob/contracts/src/dTSLA.sol)<br>
                 This file contains the functions of creating a new token , view functions for price and balance calculations , sending of mint request to the <br>
                 chainlink functions and fulfilling it.<br>
                 send Mint Request - an internal function which initiates the request for minitng by encoding the secrets and creating a request.<br>
                 fulfill Request - function to be clicked automatically by chainlink when the request execution is completed, it checks if the portfolio balance is <br>                                    correct or not and then mints the required amount to the user.<br>
                 Rest are view functions for Usdc to usd , Tsla to Usd , functions to get tesla and usdc prices and to calculate the total value that we have 
                 minted.<br>
     
next<br>
          [DtslaRouter.sol](https://github.com/DarkLord017/DTSLA.SOL/blob/contracts/src/dTSLARouter.sol)<br>
                  This file contains the part with which user will interact.This also stores the contract USDC balance<br>
                  mint - takes the USDC amount from the user , check if its accurate and then calls dtsla's mint request<br>
                  redeem- calls the redeem contract by passing amount to redeem and address of the user<br>
                  getCollateralforRwaTesla -- if the portfolio balance is low company can use it to buy new TSLA stocks<br>
                  mint , burn , send USDC to user -- OnlyRedeem only redeem contract can click this more on redeem part<br>
                  withdraw - calls the dtslaRedeem to get user's fund<br>

next<br>
                  --[DtslaRedeem.sol](https://github.com/DarkLord017/DTSLA.SOL/blob/contracts/src/dTSLARedeem.sol)<br>
                    This file contains the redeem implementation.<br>
                    WHY IN A DIFFERENT CONTRACT?<br>
                    because we were having callback gaslimit exceded issue while doing it in the same contract , so to reduce gas we are doing it in different<br>
                    contract.<br>
next<br>
                    sendredeemrequest - updates the mapping of user => usdc , burns the token and send the request to chainlink functions to execute it.<br>
                    fulfillRequest - if it fails mint again the burnt amount and change the mapping which we did earlier<br>
                    is_redeemactive - to reduce reentrancy<br>
                    withdraw - sends request to dtsla router to transfer the USDC tokens into user's account<br>
next<br>
                   --[TslaPriceFeed.sol](https://github.com/DarkLord017/DTSLA.SOL/blob/contracts/src/TslaPriceFeed.sol)<br>
                     Price feed for tsla using chainlink get requests<br>
                     (as chainlink didn't had one)<br>
next<br>
                    --Constants.sol - constant and errors required by the contracts<br>

[__Chainlink functions__](https://github.com/DarkLord017/DTSLA.SOL/tree/contracts/functions/sources)<br>

   sell.js - converts a string with 10**18 to a string with decimals without 10**18 then checks if the stock market is open if yes then it sells TSLA from the 
   account<br>
   alpacaBalance.js - gets the balance of TSLA stock in dollars in alpaca account<br>
   tslaPrice.js - returns the current price of tsla tokens<br>

   Simulators and sources are to test if they are working properly or not<br>

   Frontend technical documentation can be found in that readme<br>

   __Challenges Faced__<br>
    1. Callback gas limit issue while doing it on the same contract then chenaged mint and redeem in differnet contracts.<br>
    2. Decimal changing for js request back to normal , for usdc 6 , for others 18.<br>
    3. Had to test after broadcasting as chainlink functions can't run in anvil or genache<br>
    4. Tried implementing stock market chart but time ended<br>

   __Individual Contribution__<br>
      Sambhav - <br>
         1. DtslaRedeem , DtslaRouter n some part of dtsla contract.<br>
         2. Frontend Home page animation and TryNow.js and LoginDialog.js file.<br>
         3. sell and alpacaBalance chainlink function

 Shorya -<br>
        1. TslaPriceFeed and dtsla contract.<br>
        2. Frontend Home Page<br>
        3. tslaprice chainlink function<br>

  __Learning from this hackathon__ <br>
       1. Created frontend in a hackathon by myself firsttime <br>
       2. Chainlink function<br>
       3. How to integrate accross different contracts<br>
       4. Something about stocks<br>
       
        
        
        

         

         

   
   

      
                    
              
                
                 
                 






 
 

 
