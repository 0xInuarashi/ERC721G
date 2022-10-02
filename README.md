# ERC721G
ERC721G is the all-in-one batch minting and staking smart contract created by 0xInuarashi for Gangster All Star, and open-sourced to the public to build upon.

Verbose @dev comments are marked within the smart contract itself detailing what you need to know within each function.
It is HIGHLY RECOMMENDED that any developer who wants to implement ERC721G into their contracts read through the entire smart contract and comments before attempting any implementation.

Now that that's done, here is a simplified decision tree that you must make while implementing ERC721G

CONSTRUCTOR
Contructor receives 4 arguments (ERC721 is 2 arguments)
- Name (Token Name)
- Symbol (Token Symbol)
- Start ID (First ID of the Collection, generally 0 or 1)
- Max Batch Size (Max batch size, recommended 5-20 only)

BATCH MINTING
Built-in functionality, you do not have to decide anything.
Note: ERC721G only supports INCREMENTAL token IDs.
The difference of _mint() in ERC721G and other batch minting implementations is as follows:
_mint(to, amount) vs _mint(to, tokenId)
In ERC721G and other batch minting implementations, you must pass in AMOUNT to _mint. 
In normal ERC721 (Such as OpenZeppelin or Solmate), you pass in the TOKEN ID to _mint.
PASS IN AMOUNT, NOT TOKENID.

TRANSFER TIME TRACKING
Also Built-in functionality. You do not have to decide anything. It is automatic on transfer and almost consumes no gas to record as it is the same SSTORE slot.

BATCH MINT AND STAKE
Internally, it is included by default but is not called by any function, thus you must interface this to your
interited contract yourself. If you do choose to use these inheritances, MAKE SURE STAKE / UNSTAKE / STAKED TIME TRACKING FEATURES ARE ENABLED
otherwise you risk that YOUR TOKENS CAN BE STAKED AND LOCKED FOREVER.

STAKING / UNSTAKE / STAKED TIME TRACKING
These are OPTIONAL functions that are currently DISABLED BY DEFAULT consisting of a few optional functions
1/ Built-in Stake and Unstake (Public) Functions
These functions are enabled by default without any administrative disable or enable function
You do not have to use these as you can interface with the internal _stake and _unstake yourself
to create your own desired behaviors

2/ Built-in Staking Helper Functions
These are very useful functions for ERC721G that has STAKE / UNSTAKE enabled because it helps you have additional
metrics to be pulled from front-end and also lets you view the full balance of a user with staked + unstaked tokens in one
and more. Consult the smart contract code for more info.

STAKED TIME TRACKING
Built-in functionality that is activated on STAKE / UNSTAKE functions thus you don't have to do anything here

OPTIONAL ADDITIONAL HELPER FUNCTIONS
These are optional additional helper functions that you can enable to be able to retrieve batch ownerOf or _trueOwnerOf for around 1.5k cheaper gas
per batch inquiry. Not required. But it helps if you have some use for it.

Feel free to contribute, send feedback, or anything to our open-source repository!

DISCLAIMER: ALL SMART CONTRACT AND FILES HERE ARE OFFERED AS-IS AND OPEN-SOURCE. THE DEVELOPERS OF THIS REPOSITORY ARE NOT RESPONSIBLE FOR ANY ERRORS, BUGS, IMPLEMENTATION FAILURES, 
AND ANY OTHER DAMAGES THAT CAN BE CAUSED BY THIS CODE. WE HOLD NO RESPONSIBILITY AND YOU MUST USE THESE SMART CONTRACTS AT YOUR OWN RISK.
