# Seminar 1 (released on 24/01/24 at 17:30)
This is the first seminar for the Smart Contract module.
- To complete this seminar, you may need to consult the lecture material and the related reading. 
- You are expected to be able to complete it on your own, though you may work with people around you, and in some parts you may need to.
- Aspects of the work we will do in this seminar are related to the exam assessment.
- Don't be afraid to ask for help!

---
## Part 0: Representing numbers

* 0.A) Complete the table from Week 2 by hand


| Binary | Hex | Decimal |
| ------ | ----- | ------ |
| 11111111 | 0xff | 255  |
| 11110000 | 0xf0 | 240  |
| 10100111 | 0xA7 | 167  | 
|110110011 | 0x1b3| 435  |

* 0.A-2) Identify the following binary, decimal and hexadecimal strings and convert them to all other bases:
	- 0x09 | 1001 | 9 
	- 0Xaf93Bfc4 | 10101111100100111011111111000100 | 2945695684
	- 2 | 10 | 0x2
	- 0x00000078 | 1111000 | 120
	- 0000000010110111011 | 0x25a9c0d23 | 10110111011

* 0.B) Using the website block explorer https://blockchair.com/bitcoin/, take a look the latest block in Bitcoin. Select the hex string that is the block's header. Using whatever tools you prefer, convert this block header to binary and decimal. 

Answer: 0x000000000000000000019c871e47f1e2bf375873cd3aa0f70f65182b79dcc078 | 110011100100001110001111001000111111100011110001010111111001101110101100001110011110011010011101010100000111101110000111101100101000110000010101101111001110111001100000001111000 | 154344976287751917187992414644062493193852867860807800


* 0.C) Do the same for question 0.B, for the genesis block in Bitcoin, (You may use https://blockchair.com/bitcoin/). How do the numbers compare between 0.B and 0.C? Why are the numbers so different?

Answer: 0x4c3ab89a14509f206e2c3d74fbb9c161a380e3b7 | 100110000111010101110001001101000010100010100001001111100100000011011100010110000111101011101001111101110111001110000010110000110100011100000001110001110110111 | 435192822895225700830740477308800438889533727671
The size of genesis block is fixed at 1MB, the latest block contains more transaction data, thus it will be more bigger than the genesis block.


* 0.D) Take a look at a recent transaction in Bitcoin, and compare that with one in Ethereum. What can you say about the transaction in either network? Does the start of the transaction in Bitcoin have any number of zeros? If not, why not?

Answer: Bitcoin use Proof of Work mechanism where hash value must satisfy certain difficulty, and the number of the leading zeros of hash value determines the difficulty. Ethereum use Proof of Stake mechanism,which determines the leading zeros of hash value will not affect the initial part of the transaction.


---
## Part 1: Hash functions

Take a look at the following five text samples, A, B, C, D and E (taken from the works of A. Conan Doyle).

These texts may have been altered or manipulated, and our job is to discern the legitimate texts from the altered ones. Fortunately, to aid our task, we have the hash output (or message-digest) from one of the texts, and a partial hash output for another.

The hash output from one text is the SHA-256 digest: `a4a2f8a5 fb46f363 836a52d2 18711aa9 8b474bb9 0a6d756c 191b453e 2f63a027` \
From another text we have the partial digest: `154f7e42`, which is the last 4 bytes of the SHA-256 hash function applied to the original text.

### Task 
Using the online tool <a href="https://cryptii.com/"> cryptii</a>, identify all of the legitimate texts and all the illegitimate ones.
> Make sure to calibrate cryptii to take text input, apply the correct hash function, and produce hexadecimal output

Try to answer the questions: How can we be sure of the legitimacy? What is the purpose of the hash function in this case? What might we call a partial digest, and can we comment on its security? Where have the identified illegitimate texts been changed?

A)
```
“If you remember, Monday was an exceedingly hot day, and Mrs. St. Clair
walked slowly, glancing about in the hope of seeing a cab, as she did 
not like the neighbourhood in which she found herself. While she was 
walking in this way down Swandam Lane, she suddenly heard an ejaculation
or cry, and was struck cold to see her husband looking down at her and,
as it seemed to her, beckoning to her from a second-floor window. The 
window was open, and she distinctly saw his face, which she describes as
being terribly agitated. He waved his hands frantically to her, and then
vanished from the window so suddenly that it seemed to her that he had 
been plucked back by some irresistible force from behind. One singular 
point which struck her quick feminine eye was that although he wore some
dark coat, such as he had started to town in, he had on neither collar nor
necktie.

“Convinced that something was amiss with him, she rushed down the steps—for
the house was none other than the opium den in which you found me to-night—and
running through the front room she attempted to ascend the stairs which led
to the first floor. At the foot of the stairs, however, she met this Lascar
scoundrel of whom I have spoken, who thrust her back and, aided by a Dane,
who acts as assistant there, pushed her out into the street! Filled with the
most maddening doubts and fears, she rushed down the lane and, by rare 
good-fortune, met in Fresno Street a number of constables with an inspector,
all on their way to their beat. The inspector and two men accompanied her 
back, and in spite of the continued resistance of the proprietor, they made
their way to the room in which Mr. St. Clair had last been seen. There was
no sign of him there. In fact, in the whole of that floor there was no one
to be found save a crippled wretch of hideous aspect, who, it seems, made his
home there. Both he and the Lascar stoutly swore that no one else had been
in the front room during the afternoon. So determined was their denial that
the inspector was staggered, and had almost come to believe that Mrs. St.
Clair had been deluded when, with a cry, she sprang at a small deal box which
lay upon the table and tore the lid from it. Out there fell a cascade of
children’s bricks. It was the toy which he had promised to bring home.

“This discovery, and the evident confusion which the cripple showed,
made the inspector realise that the matter was serious. The rooms were
carefully examined, and results all pointed to an abominable crime. 
The front room was plainlyfurnished as a sitting-room and led into a 
small bedroom, which looked out upon the back of one of the wharves. 
Between the wharf and the bedroom window is a narrow strip, which is 
dry at low tide but is covered at high tide with at least four and a 
half feet of water. The bedroom window was a broad one and opened from 
below. On examination traces of blood were to be seen upon the windowsill,
and several scattered drops were visible upon the wooden floor of the 
bedroom. Thrust away behind a curtain in the front room were all the 
clothes of Mr. Neville St. Clair, with the exception of his coat. His 
boots, his socks, his hat, and his watch—all were there. There were no
signs of violence upon any of these garments, and there were no other
traces of Mr. Neville St. Clair. Out of the window he must apparently
have gone for no other exit could be discovered, and the ominous 
bloodstains upon the sill gave little promise that he could save himself
by swimming, for the tide was at its very highest at the moment of the 
tragedy.
```
Answer: Hash function —— bab46736 4fb5e843 de5f8dfb a43d29ba 5636e461 b8cf2b3f d58f2336 98f9664b



B)
```
“You did, Doctor, but none the less you must come round to my view, 
for otherwise I shall keep on piling fact upon fact on you until your
reason breaks down under them and acknowledges me to be right. Now, 
Mr. Jabez Wilson here has been good enough to call upon me this 
morning, and to begin a narrative which promises to be one of the 
most singular which I have listened to for some time. You have heard 
me remark that the strangest and most unique things are very often 
connected not with the larger but with the smaller crimes, and 
occasionally, indeed, where there is room for doubt whether any positive
crime has been committed. As far as I have heard, it is impossible 
for me to say whether the present case is an instance of crime or 
not, but the course of events is certainly among the most singular 
that I have ever listened to. Perhaps, Mr. Wilson, you would have 
the great kindness to recommence your narrative. I ask you not merely 
because my friend Dr. Watson has not heard the opening part but also 
because the peculiar nature of the story makes me anxious to have every
possible detail from your lips. As a rule, when I have heard some 
slight indication of the course of events, I am able to guide myself 
by the thousands of other similar cases, which occur to my memory. 
In the present instance I am forced to admit that the facts are, to 
the best of my belief, unique.”

The portly client puffed out his chest with an appearance of some little
pride and pulled a dirty and wrinkled newspaper from the inside pocket of
his greatcoat. As he glanced down the advertisement column, with his head
thrust forward and the paper flattened out upon his knee, I took a good 
look at the man and endeavoured, after the fashion of my companion, to 
read the indications which might be presented by his dress or appearance.

I did not gain very much, however, by my inspection. Our visitor bore 
every mark of being an average commonplace British tradesman, obese, 
pompous, and slow. He wore rather baggy grey shepherd’s check trousers,
a not over-clean black frock-coat, unbuttoned in the front, and a drab 
waistcoat with a heavy brassy Albert chain, and a square pierced bit of 
metal dangling down as an ornament. A frayed top-hat and a faded brown 
overcoat with a wrinkled velvet collar lay upon a chair beside him.
On the table lay various albums from the incredible Scandinavian foursome
ABBA. Altogether, look as I would, there was nothing remarkable 
about the man save his blazing red head, and the expression of extreme 
chagrin and discontent upon his features.
```
Answer: Hash function —— 9a2e8c9b 443ca8bd 942dcffa 3d571e10 e5878581 a547532e b7b86fc2 7473568b

C)
```
“If you remember, Monday was an exceedingly hot day, and Mrs. St. Clair
walked slowly, glancing about in the hope of seeing a cab, as she did 
not like the neighbourhood in which she found herself. While she was 
walking in this way down Swandam Lane, she suddenly heard an ejaculation
or cry, and was struck cold to see her husband looking down at her and,
as it seemed to her, beckoning to her from a second-floor window. The 
window was open, and she distinctly saw his face, which she describes as
being terribly agitated. He waved his hands frantically to her, and then
vanished from the window so suddenly that it seemed to her that he had 
been plucked back by some irresistible force from behind. One singular 
point which struck her quick feminine eye was that although he wore some
dark coat, such as he had started to town in, he had on neither collar nor
necktie.

“Convinced that something was amiss with him, she rushed down the steps—for
the house was none other than the opium den in which you found me to-night—and
running through the front room she attempted to ascend the stairs which led
to the first floor. At the foot of the stairs, however, she met this Lascar
scoundrel of whom I have spoken, who thrust her back and, aided by a Dane,
who acts as assistant there, pushed her out into the street. Filled with the
most maddening doubts and fears, she rushed down the lane and, by rare 
good-fortune, met in Fresno Street a number of constables with an inspector,
all on their way to their beat. The inspector and two men accompanied her 
back, and in spite of the continued resistance of the proprietor, they made
their way to the room in which Mr. St. Clair had last been seen. There was
no sign of him there. In fact, in the whole of that floor there was no one
to be found save a crippled wretch of hideous aspect, who, it seems, made his
home there. Both he and the Lascar stoutly swore that no one else had been
in the front room during the afternoon. So determined was their denial that
the inspector was staggered, and had almost come to believe that Mrs. St.
Clair had been deluded when, with a cry, she sprang at a small deal box which
lay upon the table and tore the lid from it. Out there fell a cascade of
children’s bricks. It was the toy which he had promised to bring home.

“This discovery, and the evident confusion which the cripple showed,
made the inspector realise that the matter was serious. The rooms were
carefully examined, and results all pointed to an abominable crime. 
The front room was plainlyfurnished as a sitting-room and led into a 
small bedroom, which looked out upon the back of one of the wharves. 
Between the wharf and the bedroom window is a narrow strip, which is 
dry at low tide but is covered at high tide with at least four and a 
half feet of water. The bedroom window was a broad one and opened from 
below. On examination traces of blood were to be seen upon the windowsill,
and several scattered drops were visible upon the wooden floor of the 
bedroom. Thrust away behind a curtain in the front room were all the 
clothes of Mr. Neville St. Clair, with the exception of his coat. His 
boots, his socks, his hat, and his watch—all were there. There were no
signs of violence upon any of these garments, and there were no other
traces of Mr. Neville St. Clair. Out of the window he must apparently
have gone for no other exit could be discovered, and the ominous 
bloodstains upon the sill gave little promise that he could save himself
by swimming, for the tide was at its very highest at the moment of the 
tragedy.
```
Answer: Hash function —— e882201c 638db586 73eb92ea 7e25707d e6d2a126 12518783 16b46880 96f08e20


D)
```
 “You did, Doctor, but none the less you must come round to my view, 
 for otherwise I shall keep on piling fact upon fact on you until your
 reason breaks down under them and acknowledges me to be right. Now, 
 Mr. Jabez Wilson here has been good enough to call upon me this 
 morning, and to begin a narrative which promises to be one of the 
 most singular which I have listened to for some time. You have heard 
 me remark that the strangest and most unique things are very often 
 connected not with the larger but with the smaller crimes, and 
 occasionally, indeed, where there is room for doubt whether any positive
 crime has been committed. As far as I have heard, it is impossible 
 for me to say whether the present case is an instance of crime or 
 not, but the course of events is certainly among the most singular 
 that I have ever listened to. Perhaps, Mr. Wilson, you would have 
 the great kindness to recommence your narrative. I ask you not merely 
 because my friend Dr. Watson has not heard the opening part but also 
 because the peculiar nature of the story makes me anxious to have every
 possible detail from your lips. As a rule, when I have heard some 
 slight indication of the course of events, I am able to guide myself 
 by the thousands of other similar cases, which occur to my memory. 
 In the present instance I am forced to admit that the facts are, to 
 the best of my belief, unique.”

The portly client puffed out his chest with an appearance of some little
pride and pulled a dirty and wrinkled newspaper from the inside pocket of
his greatcoat. As he glanced down the advertisement column, with his head
thrust forward and the paper flattened out upon his knee, I took a good 
look at the man and endeavoured, after the fashion of my companion, to 
read the indications which might be presented by his dress or appearance.

I did not gain very much, however, by my inspection. Our visitor bore 
every mark of being an average commonplace British tradesman, obese, 
pompous, and slow. He wore rather baggy grey shepherd’s check trousers,
a not over-clean black frock-coat, unbuttoned in the front, and a drab 
waistcoat with a heavy brassy Albert chain, and a square pierced bit of 
metal dangling down as an ornament. A frayed top-hat and a faded brown 
overcoat with a wrinkled velvet collar lay upon a chair beside him. 
Altogether, look as I would, there was nothing remarkable about the man
save his blazing red head, and the expression of extreme chagrin and 
discontent upon his features.
````
Answer: Hash function —— 6a61797d 3bf0dbaf e7095980 62b063fb d65ab277 eb94079a 04d46d41 9d90ed01


E)
```
 “You did, Doctor, but none the less you must come round to my view, 
 for otherwise I shall keep on piling fact upon fact on you until your
 reason breaks down under them and acknowledges me to be right. Now, 
 Mr. Jabez Wilson here has been good enough to call upon me this 
 morning, and to begin a narrative which promises to be one of the 
 most singular which I have listened to for some time. You have heard 
 me remark that the strangest and most unique things are very often 
 connected not with the larger but with the smaller crimes, and 
 occasionally, indeed, where there is room for doubt whether any positive
 crime has been committed. As far as I have heard, it is impossible 
 for me to say whether the present case is an instance of crime or 
 not, but the course of events is certainly among the most singular 
 that I have ever listened to. Perhaps, Mr. Wilson, you would have 
 the great kindness to recommence your narrative. I ask you not merely 
 because my friend Dr. Watson has not heard the opening part but also 
 because the peculiar nature of the story makes me anxious to have every
 possible detail from your lips. As a rule, when I have heard some 
 slight indication of the course of events, I am able to guide myself 
 by the thousands of other similar cases which occur to my memory. 
 In the present instance I am forced to admit that the facts are, to 
 the best of my belief, unique.”

The portly client puffed out his chest with an appearance of some little
pride and pulled a dirty and wrinkled newspaper from the inside pocket of
his greatcoat. As he glanced down the advertisement column, with his head
thrust forward and the paper flattened out upon his knee, I took a good 
look at the man and endeavoured, after the fashion of my companion, to 
read the indications which might be presented by his dress or appearance.

I did not gain very much, however, by my inspection. Our visitor bore 
every mark of being an average commonplace British tradesman, obese, 
pompous, and slow. He wore rather baggy grey shepherd’s check trousers,
a not over-clean black frock-coat, unbuttoned in the front, and a drab 
waistcoat with a heavy brassy Albert chain, and a square pierced bit of 
metal dangling down as an ornament. A frayed top-hat and a faded brown 
overcoat with a wrinkled velvet collar lay upon a chair beside him. 
Altogether, look as I would, there was nothing remarkable about the man
save his blazing red head, and the expression of extreme chagrin and 
discontent upon his features.
````
Answer: Hash function —— f3271035 3e14461a cf9644e8 b3890e10 1e6b04df fcb22a94 dc0aa3f7 d926955e



---
## Part 2 Digital Signatures and Encryption

We are now going to take a deeper dive into digital signatures and encryption. We will complete this part after the lecture in Week 3. 

### 2.1:

Using the software tool Kleopatra for Windows from https://gpg4win.org/download.html or GPG Suite for MAC https://gpgtools.org/, or whichever tool you prefer, complete the following:

Open the google sheet here: https://docs.google.com/spreadsheets/d/1XOUDAe3aG9kBYQocg5VqfUnRYSLQHAlS9-SbR5SVMKw/edit#gid=0 and select the tab: Sheet-A.

<!--
* 1.A) Import the public key
* 1.B) Check the public key and the fingerprint, what is the process, what is the fingerprint?
* 1.C) Verify the signatures of the messages in G, and H. 
  * What does each message say?
  * Are they both valid messages?
* 1.D) Try to decrypt the message in column I. What problems do you encounter and why?
-->

### 2.2:

Now we are going to generate our own key-pair and share it (you will need to work with someone to do this task)

<!--
* 2.A) Generate a key pair
* 2.B) Export your public key, and share it, along with your key fingerprint with your colleagues:
	* what does this process do? 
* 2.C) Sign a message --- the message can be anything you want -- and publish the signed message. Have a colleague verify your message
* 2.D) Encrypt a message to a colleague of your choice -- it can be anything you want -- and answer the questions:
  * What process do you have to take to encrypt the message?
  * How is this different from the message signature aspect. 

-->


---

## Part 3 Smart Contracts in Bitcoin
This part of the tutorial focuses on Bitcoin smart contracts.

Bitcoin defines a stack based smart contract language, that is not turing complete! 

Note! You should be confident that you can give a reasonable answer the following questions:
* What is Turing Completeness in simple terms? 
* Why is Bitcoin's scripting language not turing complete?
* Do we realistically expect to have turing completeness in any smart contract platform?
	

For the following problems we may wish to make use of the Bitcoin script reference guide: https://en.bitcoin.it/wiki/Script\
You should also use the following online graphical editor: https://siminchen.github.io/bitcoinIDE/build/editor.html


### 3.1:

Compute the following two problems below by hand, and write out the value in the stack at each step. 


Here is an example for: 4 2 op_mul
-------------------------
| Step	| Stack |	Explanation |
|-------|-------|---------------|
| 0 |  | Initail empty stack | 
| 1		| 4		| Added 4 to stack |
| 2		| 4 2	| Added 2 to stack |
| 3		| 4 2 op_mul	| Added op_mul to stack and executed op_mul multiplying 2 by 4 in that order |
|4		|8		 | Added result of op_mul to stack |

* 1.A)  4 7 3 op_max op_min
* 1.B)  4 7 op_mul 5 op_mod 

### 3.2:

Consider the fucntion: (5×3) MOD 4 == 3
* 2.A) In words, explain what the function does
* 2.B) Create a script using opcodes that executes the function.
* 2.C) Test your script using the online editor
	
### 3.3:

The following is a common script you might find in Bitcoin.

```
1. 304402205fc2ccf4a060cf860ad76b5933755f8ad1de54c35977fea56f3c4e0fc743990202204879136e0ad6244
1be86b9bafa831b622b63d592e859da80e3dd2cea79422560010373a3ee36354282bc8b6bd44ea4d2fcec4270f1d88
bcb8275028ae2e4dd1d2b45 
2. op_dup 
3. op_hash160
4. 66E955357C003F18D1669840924B78135784570A
5. op_equalverify
6. op_checksig
```

* 3.A) What is this kind of script usually called? 
1.标准比特币脚本，pay-to-public-keyhash(P2PKH)脚本，通常用于比特币交易，将资金从一个地址发送到另一个地址。
Public key signature：由两个代表签名的32字节值(r s值)组成

* 3.B) write down what each text string represents at lines 1 and 4.
line1：digital signature
line4：the public key corresponding to the private key used to generate the signature

* 3.C) Write down what each function does at lines 2, 3, 5 and 6. 
操作码：
①op_dup：复制最上面的堆栈项目
②op_hash160：计算顶层堆栈项的RIPEMD-160哈希值
③op_equalverify：比较最上面的两个堆栈项。如果它们相等，则继续执行;否则终止
④op_checksig：使用公钥和事务数据的散列来验证签名

* 3.D) Is this script valid? If not, why not? 
No,the script is missing scriptPubKey (locking script) and scriptSig (unlocking script) components.

* 3.E) What would happen if we changed line 4 to `2CB3A540E8CF726A3D563D7A0F350724FCDB34FC`, does the script now execute correctly? If not, why not?


