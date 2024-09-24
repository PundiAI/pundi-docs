# Beta Walkthrough

## 3.1 Connect Wallet&#x20;

Connect your MetaMask or f(x)Wallet to get started.

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXfx9R9Myo5LBqTnfA-YT9-F4dkDEqdV44MJoAHAZh\_2pKcjHe3jqu5NgVRnuVSaEkBRw\_nWHJReTcTVB0afFf1eooe2RAhKNDKivXZ4tJPk0RJySouh3RFOnTLunWeGAG-uPqPWeIVUKjPeoBmPVJTnL5U?key=GY4Km3NohmikbGyIxPcjWQ)

## 3.2 Add New Dataset&#x20;

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXdrtOyaRT38W5J8I3VNRKhmtWQbek9ZXFb8TedlPLhCEC7JfYXral08C91vEh5eqs95BqXqGmJIVoNNNsxSGescqu6MLaYHM0aldPIUW4PrJjAedINa27Sf23gVHDcg96nb\_zLfyQVVstZtrNt7RbkmSkU?key=GY4Km3NohmikbGyIxPcjWQ)

\


<table data-header-hidden><thead><tr><th width="307"></th><th></th></tr></thead><tbody><tr><td>Supported method(s)</td><td>Upload local files</td></tr><tr><td>Content type</td><td><ul><li>Text</li><li>Image</li></ul></td></tr><tr><td>Uploading requirement</td><td>Files must be in .csv, .json, .txt, or .zip format.</td></tr><tr><td><p><br><br><br><br><br></p><p>Supported dataset types<br>(Single choice)</p></td><td><ul><li>News Categorization</li><li>Sentiment Analysis</li><li>Named Entity Recognition</li><li>Part-of-Speech Tagging </li><li>Summarization</li><li>Human Activity Recognition</li><li>Scenery Classification</li><li>Bounding Box Annotation</li></ul></td></tr><tr><td><p><br></p><p>Accessiblity </p></td><td>Accessible to the Dataset Owner only</td></tr></tbody></table>

{% hint style="danger" %}
Using a dataset from Marketplace is not available in beta

A dataset can be sold and traded by transferring the ownership NFT from the Owner to the buyer. Pundi AIData Beta doesn’t provide Dataset Market and Buy Datasets option for users to gain ownership of an existing dataset.
{% endhint %}

## 3.3 Create New Labeling Task

Dataset is the foundation of a labeling task. It is required to add at least one dataset to get started. It is required to add instructions(“Task Requirements”) for your task to help labelers annotate.

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXcKxGMNGcLSgunj4HGTm1lXRM7YD4Yw5U\_wAF5OQAB19jtn5qq9LMAEkDXJ3l7okYLRLnYArUPsu0ZHKeFewKub4y-6UHTt3G4p1qAgo10yiRbqCYetOa3D1ntRpwGr9basDidLeVPaQNw93v2DhRFBJ0U?key=GY4Km3NohmikbGyIxPcjWQ)

### Supported Annotation Types&#x20;

**Text Classification**

| <p><br></p>        | Explanation                                                                                        |
| ------------------ | -------------------------------------------------------------------------------------------------- |
| Sentiment Analysis | Understand and classify the sentiment of the given text                                            |
| Key Phrase Tagging | Locate and tag keywords or phrases in the given text and classify them into predefined categories  |
| Entity Annotation  | Identify and label named entities in the given text at both the word and phrase level.             |



**Image Annotation**

| <p><br></p>             | Explanation                                                                         |
| ----------------------- | ----------------------------------------------------------------------------------- |
| Sentiment Analysis      | Understand and classify the sentiment of the given image                            |
| Image Classification    | Classify the given image into predefined categories according to its visual content |
| Bounding Box Annotation | Draw and label bounding boxes around the objects of interest in the given image     |

### Task Types

| Data Type               | Supported Annotation Type        | Task Type                         |
| ----------------------- | -------------------------------- | --------------------------------- |
| Text                    | Sentiment Analysis               | Single-label Text Classification  |
| Key Phrase Tagging      | Multi-label Text Classification  |                                   |
| Entity Annotation       | Entity Annotation                |                                   |
| Image                   | Sentiment Analysis               | Single-label Image Classification |
| Image Classification    | Multi-label Image Classification |                                   |
| Bounding Box Annotation | Bounding Box Annotation          |                                   |



### Provide Task Rewards

Token Reward is designed to prevent spam and award data processors.&#x20;

In Beta, to create a labeling task, the Task Owner is required to provide Token Rewards in $USDT with the task. The minimum amount of provided $USDT is allowed to be 0.&#x20;



* **Average Hourly Earning**&#x20;

Once created, all active tasks will be presented with total reward and an estimated hourly earning. In Beta, Hourly earning =  Task reward / number of data rows \* 1200 (supposed 3 seconds to label a data row)

### Task Accessibility&#x20;

Once a labeling task is created, it is accessible to all users on Pundi AIData Beta. Everyone is allowed to contribute to the labeling work for the task.\


## 3.4 Label Data

Browse the active tasks list, select a task and tap Join In to enter the labeling editor and start data labeling for this task.&#x20;

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXdDU35\_y4rNXV\_P5IMqZ5cA93cErcXLg6zPwJD7k1ygLdsiWZmeC9SAIXOiMhbZMch7tzDLO38bbGROYdeO5RBQ7XLqn6WUlYskTzAIYs31TMkQDAo18SAz7p4FlWx2E74BXXVF4KMHapOypzS\_BnWw-rWk?key=GY4Km3NohmikbGyIxPcjWQ)



### **Labeling Editors**

Single-label Classification&#x20;

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXeGnwAdyTn5HeOUWCpmLq1m9adaRCu8brviVd09IfoU0I85VwwI1fmm36BCcCZBJZaHqTMpXnFDg4-3RBrbKj27BOVOp0jyzkzi6d0m\_BoZ3vHwpWtog6HthepNKy8X5iJzCX6Hp9CiQRzQTjwZOQLNYVgZ?key=GY4Km3NohmikbGyIxPcjWQ)\


Multi-label Classification

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXcr8TgCKbHm1ALDMyYsiiaOxi9UFwsVXELGIFVvB6-UvrhjU8lOIuJasqtMPqMpIl75H5oH2A34M-10Gf6VmD54EOvaEdYQ9UWdP\_wYjxuvwrj53VbBym4jfhx11mVQT4usVrO2PBFEQVK0w46pOVY8590u?key=GY4Km3NohmikbGyIxPcjWQ)\


(Text) Entity Annotation

Create an entity by clicking the desired starting character and dragging to select a sequence of characters in the given text. Then tag the entity.

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXdHv\_HQrvwqtd5rxiraw4VtuVdTKlBtQeSt\_\_336KxvvvnGtS2bIQANJCbr35B3oC-Ss4GTFjngKqQ07kGfhxYEYG3IVgqETbCMWO3kysTXXzMJyzjy6LY9yu2oGtCgJweuMje5FnSiHVu\_ibmlqUlezXBg?key=GY4Km3NohmikbGyIxPcjWQ)&#x20;

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXcNagFpAKHLgiWdzr9pI7cRUKelrB78aA\_1ZZVCr0\_\_kQ5Qnfyz6iGdzw1df91yxCBgq1fmO\_0eixMUGp1IHnWbAPlLgstji8cWJw6SKAODpfKFeOeDoROumRQDxwDwh536hU9XwpS9BoBImP\_Uy0B3aym5?key=GY4Km3NohmikbGyIxPcjWQ)\


(Image) Bounding Box

Create a bounding box by starting at one corner and dragging your cursor to create the shape around an object in the image.

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXdPQpxOQ97vMfWrqthl2N0H6Yhwu8B4a2XdI911hLfVeHKr7U8ZUCvZAUFLr\_gL4HNkvbCGhxBB0VQwVulKU6a-XaRrRFnxOZYd98XM-Nqx6mIy4FTXC4S4lLBXnaFK5BsibhaoXdV2uud4EUF2s4zREirp?key=GY4Km3NohmikbGyIxPcjWQ)



## 3.5 Receive Task Rewards

![](https://lh7-rt.googleusercontent.com/docsz/AD\_4nXcAL6IYz55b7xZGrRFH2wJyi9god5d-u2ZXq8Nfs78PKHyBJ2zSc5OcuIL952kpk4SXHB6mBVT\_JNMUgODBRzI63O\_uHma6SgQXc15HsuxB9DM3aii\_pU048MV2U51t1psJtGpR\_ps2YC-87qX2jsJh7U8H?key=GY4Km3NohmikbGyIxPcjWQ)



**Calculation**

In Beta, labels are paid a fixed piece rate for each data row labeled, regardless of time.

Piece Rate = Task Reward / Total data rows



**Distribution**

Task reward will not be settled and distributed to labelers’ wallet addresses until the labeling work of this task is all done. \
