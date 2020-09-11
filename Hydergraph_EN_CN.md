# Hydergraph &mdash; Decentralized Graph Database using Hybrid API

We may define generations of Free Software Revolutions as follow:

- Free Software Revolution 1.0: Decentralization of Code &mdash; GNU / Linux
- Free Software Revolution 1.5: Blockchain and Cryptocurrencies
- Free Software Revolution 2.0: Decentralization of Data &mdash; Hydergraph

Scifi fans may recognize Hyde as one Mr Hyde &mdash; the distant ancestor of Dr. Bruce Banner & the Incredible Hulk. "Hy" is taken from "Hybrid API", "de" from "decentralized" and "graph" from graph database. The Hulk analogy is meant to imply that Hydergraph will transform the seemingly powerless user's desktop computers and mobile devices into something that can rival MAGA+F (Microsoft Apple Google Amazon Facebook).

We added an "R" between Hyde and Graph to make Hydergraph easier to pronounce.

There are at least 3 fundamental paradigm shifts that are required to make this happen -- graph database, decentralized user authentication, hybrid programming language API -- which may explain why it has not been achieved so far, as the likelihood of finding someone or a group of programmers mastering all 3 fields would be infinitesimal.



### I: Graph Database

- A json file is part of a graph database.

This is the first paradigm shift and practical understanding that we wish to impart in order to convince programmers they can contribute to something bigger than MAGA+F.
Academics would not be interested in this debate. 





### II: Decentralized User Authentication

The term "decentralized" has been "hijacked and abused" by blockchain advocates in the past few years with some notable, but limited, progress. We adopted this term largely due to the fact that our framework has a common root with blockchain in asymmetric cryptography, and it modifies significantly one of the most fundamental step in network computing: user authentication.

Blockchain is just a very clumsy way to do decentralized data base. 

Hydergraph overcomes many design flaws in block chain and cryptocurrencies from the most fundamental level.


### III: Hybrid Programming Language API

Web based software architectures in the past few decades have remained fragmented, where different programming languages are needed for different environments. Although JavaScript has recently emerged as the choice of cross platform programming language, legacy codebase in different programming languages that exist in different environments cannot be meaningfully unified, unless a Hybrid API scheme as proposed in this article is implemented.

Phoscript, a Reverse Polish Notation / Stack Machine script derived from the Forth programming language, can serve as a "universal interface script" within a host programming language, such as Python, JavaScript, PHP etc., as we shall demonstrate below. As such, the caller function is written in Phoscript while the callee function is written in a host programming language such as Python, JavaScript, PHP etc., hence the term "hybrid API".


## Decentralized User Authentication

We have initially demonstrated decentralized user authentication (DUA) with "Greeting with A Secret Phrase" (GASP) protocol in the following link:

中文： 我们最初在以下网页， 示范了通过 “传送密令授权法” "Greeting with A Secret Phrase" (GASP) 实现 “去中心化用户识别” decentralized user authentication (DUA)：

- https://github.com/udexon/XIDT/blob/master/Greet_Secret_Phrase.md

The example above employed Websocket messaging. In applications where SSH tunnel is required, Websocket is problematic. As such, we are implementing GASP over basic AJAX as shown below:

中文： 以上范例使用了 WebSocket 传信。 在使用 SSH Tunnel (SSH 隧道) 的应用里， WebSocket 会造成困难。 因此， 在本文， 我们使用 AJAX 实现了 “传送密令授权法”。

1. The source code for Hydergraph AJAX demo is available here:

中文： 本文使用的源码储存在：

- https://github.com/udexon/Hydergraph/tree/master/phos

2. The following commands are entered via the browser console:

中文： 在 Browser Console （浏览器终端）输入以下指令：

```js
c=new JSEncrypt()
F("nxhr: phos.php xo: xsqrh:")
F('a b c s: 9 3 + s: '+ btoa(c.getPublicKey()) 
+' b64d: 4 orpb: hex: dup2: enc: b64e: s:',"je: xsend:")
```

(The HTML web page is an older example (hence some deprecated terms) which briefly describes the principles of Phoscript &mdash; a Forth-like script that can act as a wrapper shell in almost all known programming languages, including Python, JavaScript and PHP.)

i. `c=new JSEncrypt()` initializes （初始化） a `JSEncrypt` object for asymmetric cryptography.

ii. `F("nxhr: phos.php xo: xsqrh:")` initializes （初始化） the AJAX connection （接口）.

iii. `F('a b c s: 9 3 + s: '+ btoa(c.getPublicKey()) 
+' b64d: 4 orpb: hex: dup2: enc: b64e: s:',"je: xsend:")`

- sends the public key of `c` (`btoa(c.getPublicKey())`) to the back-end; 把 `c`的公钥发到后端。
- `b64d:` decodes the public key by calling `base64_decode()` in PHP; 呼叫 PHP `base64_decode()` 解码公钥。
- `4 orpb:` generates a 4-byte random number by calling `openssl_random_pseudo_bytes()`; 呼叫 `openssl_random_pseudo_bytes()` 生成 4 字节的随机数。
- `hex:` converts the random number into hexadecimal notation (string); 把随机数转成 16 进位数字。
- `dup2:` duplicates 2 items at the top of the stack, so that we may compare the hexadecimal random number in the back-end with the decrypted results in the front-end; 复制堆栈最顶端的 2 个数据， 以便可以在前端和后端对照结果。
- `enc:` encrypts the random number using `openssl_public_encrypt()`; 呼叫 `openssl_public_encrypt()` 加密随机数。
- `b64e:` converts the encrypted message by calling `base64_encode()` so that the results are human readable; 呼叫 `base64_encode()` 使密文转成人眼能看的文字。
- `s:` displays all items on the stack; 显示堆栈的所有数据。

iv. Finally, the encrypted base64 message is decrypted at the front-end manually using `c.decrypt()`. 

中文： 人为手动呼叫 `c.decrypt()` 解开密文。

Stack item index [6] `5c4b74da` matches with the result of `c.decrypt()` at the bottom of figure 1.

中文： 堆栈序号 [6] 数据 `5c4b74da` 符合 `c.decrypt()` 的结果 （见图 1 底部）。

- Figure 1
<img src="https://github.com/udexon/Hydergraph/blob/master/Hydergraph/GASP.png" width=400>

iv. Obviously, in production mode, we must disable the ability of user to inspect the raw value of the random number generated by the back-end.

中文： 

The front-end module is supposed to be able to decrypt the encrypted random number generated by the back tend to prove that the user is the legitimate owner of the private key, whose public key was given to the back-end earlier.

3. The link below demonstrates a simple HTTP POST example on updating a JSON file, which can be used as the foundation of a graph database:

- https://github.com/udexon/Multiweb/blob/master/Reddit_anon_comment.md

Together with the decentralized user authentication (DUA) mechanism shown above, we now have the building blocks for Hydergraph:

- decentralized user authentication
- graph database
- hybrid API

4. In the next tutorial, we shall demonstrate using Python Selenium to save the public and private keys generated by JSEncrypt to a local file, as these will be used to identify the user over a period of time.

With Hybrid API across 3 most common programming languages (Python, JavaScript, PHP), it makes learning programming much easier for novice, i.e. having to learn only Phoscript plus entry level knowledge of the host programming languages, instead of mastering all three.

Hybrid API also allows senior programmers to specialize on developing language specific callee function libraries. It is much easier to find 3 senior programmers specializing in one programming language each, instead of one senior programmer specializing in 3 programming languages.

The scenario described here is applicable in general to other software development environments.

Benefits of Hybrid API, too many programming languages.

Further, the user may change his (her) private and public keys _ANYTIME_. The chain of keypairs, together with the period of validity of the keypairs, will be unique enough to identify all human population and devices on Earth in the foreseeable future. As the user has the right to change his (her) keypairs anytime, this is known as Transient Key Cryptography (TKC).

5. From the example above, we show that DUA have fundamentally changed the mechanism of conventional user authentication from being server-centric to user-centric.

As user authentication is one of the most if not the most important mechanism in computer applications, a paradigm shift towards DUA may just create a new segment in the computing industry that may be worth the _EQUIVALENT_ of the industry segment based on server-centric (centralized) user authentication.

6. Get search results in a web spreadsheet, which itself is programmable.

To summarize this article with an easy to understand application example:

- Imagine the ubiquitous Google search box is turned into a spreadsheet application, where users have total read/write access to the database, and may write their own customized search algorithms, as well as write code to modify the user interface of the application.

<img src="https://github.com/udexon/Hydergraph/blob/master/Hydergraph/Google-Search-Spreadsheet.png" width=600>

Thousands of user-programmers ("usegrammers") may now share their code to produce the best and ever improving search algorithms, instead of relying on Google in-house programmers, whose direction will be filtered by layers upon layers of bureaucracies, notwithstanding "national security", the biggest threat to personal privacy.

With Hypergraph, what only MAGA+F can do in-house previously, all programmers can do now, producing MAGA+F clones, and perhaps better.


### Epilogue

Some readers may associate Hydergraph with HYDRA .... _But you really shoudn't_ ....
