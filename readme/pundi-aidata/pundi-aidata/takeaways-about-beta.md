# Takeaways About Beta

To use Pundi AIData Beta, users need to connect to their decentralized wallet first.

<table data-header-hidden><thead><tr><th width="345"></th><th></th></tr></thead><tbody><tr><td><strong>Blockchain</strong></td><td><p>Pundi AIFX chain Testnet</p><p>Omnichain Testnet</p></td></tr><tr><td><strong>Supported Wallets</strong></td><td><ul><li>MetaMask</li><li>f(x)Wallet</li></ul></td></tr><tr><td><strong>Cryptocurrency needed</strong></td><td><p>$USDT (testcoin)</p><p>$FX (testcoin)</p></td></tr></tbody></table>

**Things on-chain**

<table data-header-hidden><thead><tr><th width="178"></th><th></th></tr></thead><tbody><tr><td>Datasets</td><td><ul><li>After a dataset is uploaded, it is stored &#x26; managed on-chain. An NFT is minted as the unique certificate of ownership of the dataset, and sent to the Dataset Owner’s wallet address.</li><li>[not available in beta] A dataset can be sold and traded by transferring the ownership NFT from the Owner to the buyer.</li></ul></td></tr><tr><td>Labeled data</td><td><ul><li>Labeled data rows will be auto submitted on a batch base, and recorded into the blockchain.</li><li>In the beta version, each batch submission contains 100 labeled data rows.</li></ul></td></tr><tr><td>Task Rewards</td><td><ul><li>Task rewards are kept and distributed by Smart Contract.</li><li>Task reward will not be settled and distributed to labelers’ wallet addresses until the labeling work of this task is all done.</li></ul></td></tr></tbody></table>

## Roles

There are 3 types of roles on Pundi AIData Beta

<table><thead><tr><th width="204">Role</th><th>What they can do</th></tr></thead><tbody><tr><td><strong>Dataset Owner</strong></td><td><ul><li>Upload datasets</li><li>[not available in beta] Sell owned datasets for money.</li><li>[not available in beta] Trade datasets.</li></ul></td></tr><tr><td><strong>Task Owner</strong></td><td><ul><li>Upload datasets;</li><li>[not available in beta] Buy an existing dataset;</li><li>Create data-labeling tasks based on selected dataset;</li><li>Label the data rows of the task;</li><li>Provide rewards to connect to labelers to review and process large amounts of data quickly.</li></ul></td></tr><tr><td><strong>Labeler</strong></td><td><ul><li>Participate in the data-labeling tasks to gain token rewards by completing labeling work</li></ul></td></tr></tbody></table>

<mark style="color:red;">2 more roles will be available in the official release</mark>

<table><thead><tr><th width="153">Role</th><th>What they do</th></tr></thead><tbody><tr><td><mark style="color:red;">Reviewer</mark></td><td><ul><li><mark style="color:red;">Check on the quality of the annotations to gain token rewards</mark></li></ul></td></tr><tr><td><mark style="color:red;">Supervisor</mark></td><td><ul><li><mark style="color:red;">A small group of assigned personnel to prevent malicious acts and measure consensus</mark></li><li><mark style="color:red;">Perform cross-checks by labeling part of data rows of a task</mark></li><li><mark style="color:red;">Share the task rewards by doing the work</mark></li></ul></td></tr></tbody></table>

## Outline Workflow

1. Add a dataset

Dataset is the foundation of a labeling task. It is required to add at least one dataset to get started. Pundi AIData Beta supports text and image data.

2. Create a labeling task

On Pundi AIData Beta, to create a task, the Task Owner is required to provide token rewards in $USDT with the task. This is designed to prevent spam and award data processors. The minimum amount of provided $USDT is allowed to be 0.

Once created, all active tasks will be presented with total reward and an estimated hourly earning. Hourly earning = Task reward / number of data rows \* 1200. (3 seconds to label a data row)

3. Contribute to the labeling work

Once a labeling task is created, it is accessible to all users on Pundi AIData Beta. Everyone is allowed to contribute to the labeling work for any task of in progress status.

The final earning of each labeler is decided by the number of valid labeled data rows they have done.

4. Receive the task rewards

When the labeling work of this task is all done, task reward will be settled and distributed to labelers’ wallet addresses by smart contrat.

5. <mark style="color:red;">Download the labeled data (not available in beta)</mark>

<mark style="color:red;">After the labeling work is done, the Task Owner can download all labeled data.</mark>

<mark style="color:red;">Data Download is not available on Pundi AIData Beta.</mark>
