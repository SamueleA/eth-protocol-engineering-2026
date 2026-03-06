# Daily Journal
# 05/03/2026
I watched the lecture on the code tour of Reth. I got an understanding somewhat but I still think I need to do my own deepdive on the codebase to fully understand it. An interesting subject I researched was BAL (eip-7928). I gained an understanding as to how this EIP scales Ethereum. Essentially, all data locations that might be modified by the transactions in a block is passed in the header which will allow not touching eachother's data to be passed in parallel. I want to learn more about this subject so I plan on reading the EIP and explore the Reth codebase from these lens.

# 04/03/2026
I listened to today's lecture about the EVM and got a high level view as to how it works. This would be something I'd like to dig deeper into.
I've also started looking at the Reth exex example repo. I have spent the day updating the dependencies and will make a PR to the repo.

# 03/03/2026
Learn about the engine API at a high level. Started reading the Reth book. I do intend to learn more about Reth and particularly Reth exex have caught my attention as something I might want to play more with for the purpose of making projects and learning Ethereum more deeply.

# 02/03/2026
I followed a libp2p explainer today. It was insightful, but I put the task of fully reading the libp2p docs in my todo list. I do enjoy what I am learning in the Ethereum Protocol Study Group, but I am also craving more depth and I think this will only come by my digging deeper in specs, docs and codebases.

As such, I read some guide about Kurtosis in the official repo and found it didn't work. After digging deeper, it turned out that the guide was relying on outdates packages. I opened a PR to remove the guide since there was already another one covering the same subject that wasn't outdated in the same repo.

# 01/03/2026
I did a bit of lighter day today. I covered a few lessons from the Ethereum protocol study group and did a few rustlings.

# 28/02/2026
I went through the lesson on Consensus mechanism today. I do feel like there are some details that could be fleshed out in my mental model related to Casper FFG (why do we have justified VS finalized) and various slashing conditions. Eventually, I will address them as I get through th eth2book.

# 27/02/2026
Today I ran an ethereum composed of Reth on the EL and Lighthouse on the CL. I ran into problems trying to connect to Ephemery since Reth doesn't have default configs for Ephemery which meant I had to fix the Reth configuration. In the end, I fixed the issue, got some Eth and queries that I indeed had received that eth through a JSON-RPC call. I documented my code on discord and updated the documentation on the ephemery-scripts repository.
Then, I went ahead and learned about Kurtosis and played with it. Finally, I did the rustlings on tests.

# 26/02/2026
Today was focused on learning how testing works in the Ethereum ecosystem. I got to generate tests in the Ethereum Specs repo. Working on that also gave me an idea for a small improvement to the repo. I also completed a few rustlings exercises just so I can keep on making progress on the Rust front.

# 25/02/2026
I focused on the lesson about EL and CL Specs Overview. As part of the exercises, I got the chance to create a python scripts which interacts with the specs.
I learned that the CL specs starts from markdown and compiles to python code, while the execution specs does the opposite. I feel that at some point I want to take some time to do a deep dive into the specs, the codebases and the test cases.

I also took some time to do a little bit of Rust by completed some Rustlings exercises.

# 24/02/2026
I opened a PR which clarifies some comments in the ethereum-specs related to gas limits. I noticed the discrepancy while studying EIP-7935,7825 and 1559. Let's see how that will go!

In addition to that, I completed a few rustlings exercises, but the majority of the time was spend on the Lecture 3 of the Ethereum protocol studies. I haven't had the time to also run my own node as was suggested. I will keep this for later as I will have to do it eventually, and I would like to continue through the lessons for the study group.

# 23/02/2026
Today was the kickoff for the Ethereum Protocol Study group. The next two weeks will include intense study of the Ethereum protocol.

I also have studies chapter 15 of the study Rust book today in addition to some rustling exercises. Finally, I opened PRs with minor fixes to the EPF wiki. As weeks progress, I will be looking to making more meaningful contributions to the wiki.

# 22/02/2026
Started the Rust book chapter 15 about smart pointers. Learn about the Deref trait which allows structs to act as pointers and the Drop which frees up associated memory when a smart pointer is dropped.

Also, finished chapter 1 of the zk book. Learned about how boolean circuits creates a polynomial-time-verified proof system to which a witness can be supplied to eventually create a zk proof. Also, a discussion of P VS NP and how a problems needs to be P or NP for a boolean circuit to even be possible.

## 21/02/2026
Today I completed chapter 14 of the Rust book, which was a quick and easy chapter. I read the Upgrading Ethereum book and read the chapter about LMD GHOST. I do feel like a lot fell into place reading that chapter. The short discussion of incentives and disincentives (slashing) provided a lot of insight. I am excited to read the next chapter about CASPER FFG.

I also started reading the ZK book by Rareskills. I read chapter 1 part 1, which discussed the P VS NP problem. The ZK book is very theoretical but the subject seems very important for the future of Ethereum and I feel like I need to get a good understand of it. In the short term, I would like to have finished at least the first 9 chapters so that I can have a good foundation in the math.

## 20/02/2026
I completed chapter 13 of the rust book, which wasn't too difficult. I made some improvements to the minigrep project so that it may make good use of iterators. Finally, I started reading Ben Edgington's book Upgrading Ethereum and wrote a summary of the chapters on preliminaries. I'm finding that this study method of doing a first pass, taking some notes and writing things now at a later time in my summary journal to be an efficient study method.

With the eth2book, I found I enjoyed the discussion regarding safety and liveness and how various concepts related to it such as Casper FFG, LMD GHOST, protocols like PBFT and Tendermint.

## 19/02/2026
Today I completed chapter 12 of the Rust book and the same time I completed the minigrep project. This was a good revision of the content of previous lessons including lifetimes, code organization and struct implementations.