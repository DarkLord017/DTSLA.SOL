The repository contains two branches 
 -- [__contracts__]( https://github.com/DarkLord017/DTSLA.SOL) ALL DTSLA Contracts , libraries , functions and deployment stuff
 -- [__Application__](https://github.com/DarkLord017/DTSLA.SOL/tree/Application) All frontend and etherjs stuff

 [__Project Video__](https://drive.google.com/file/d/1cSY8fMghlA_PpNdL13cskqJiq02Lhdxf/view?usp=sharing)

 __Description__
 DTSLA is a ERC-20 token that is pegged to real TSLA stocks of company's alpaca account.
 Features
 ![image](https://github.com/DarkLord017/DTSLA.SOL/assets/136801346/d5bfa351-4031-4204-8522-4d0da7d8e8bf)
 How does it work?
 ![image](https://github.com/DarkLord017/DTSLA.SOL/assets/136801346/f5236bc0-891a-44c5-baa5-84e4704312f5)
 We are integrating real world tesla stocks in blockchain it reduces centralization risks as it is written in smart contracts and Chainlink functions

 __Technical Description__
     --Contracts
               --[Dtsla.sol](https://github.com/DarkLord017/DTSLA.SOL/blob/contracts/src/dTSLA.sol)
                 This file contains the functions of creating a new token , view functions for price and balance calculations , sending of mint request to the 
                 chainlink functions and fulfilling it.
                 send Mint Request - an internal function which initiates the request for minitng by encoding the secrets and creating a request.
                 fulfill Request - function to be clicked automatically by chainlink when the request execution is completed, it checks if the portfolio balance is                                    correct or not and then mints the required amount to the user.
                 Rest are view functions for Usdc to usd , Tsla to Usd , functions to get tesla and usdc prices and to calculate the total value that we have 
                                   minted.

                --[DtslaRouter.sol](https://github.com/DarkLord017/DTSLA.SOL/blob/contracts/src/dTSLARouter.sol)
                  This file contains the part with which user will interact.This also stores the contract USDC balance
                  mint - takes the USDC amount from the user , check if its accurate and then calls dtsla's mint request 
                  redeem- calls the redeem contract by passing amount to redeem and address of the user
                  getCollateralforRwaTesla -- if the portfolio balance is low company can use it to buy new TSLA stocks
                  mint , burn , send USDC to user -- OnlyRedeem only redeem contract can click this more on redeem part
                  withdraw - calls the dtslaRedeem to get user's fund

                  --[DtslaRedeem.sol](https://github.com/DarkLord017/DTSLA.SOL/blob/contracts/src/dTSLARedeem.sol)
                    This file contains the redeem implementation.
                    WHY IN A DIFFERENT CONTRACT?
                    because we were having callback gaslimit exceded issue while doing it in the same contract , so to reduce gas we are doing it in different 
                    contract.

                    sendredeemrequest - updates the mapping of user => usdc , burns the token and send the request to chainlink functions to execute it.
                    fulfillRequest - if it fails mint again the burnt amount and change the mapping which we did earlier
                    is_redeemactive - to reduce reentrancy
                    withdraw - sends request to dtsla router to transfer the USDC tokens into user's account

                   --[TslaPriceFeed.sol](https://github.com/DarkLord017/DTSLA.SOL/blob/contracts/src/TslaPriceFeed.sol)
                     Price feed for tsla using chainlink get requests
                     (as chainlink didn't had one)

                    --Constants.sol - constant and errors required by the contracts

                    
              
                
                 
                 






 
 

 
