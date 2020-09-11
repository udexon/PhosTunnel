## "Greet with a Secret Phrase" (GASP) Cryptographic Protocol

We suppose the concept of ID-less transactions is both a novel procedure and yet has many links to the long history of cryptography, perhaps predating electronic computers.

In this article, we shall illustrate one of the most fundamental, if not the most fundamental operation that can be performed with ID-less transaction, called "Greet-with-a-Secret-Phrase" (GASP), which readers may compare to various legends concerning cryptography, and could be used as a building block for more sophiticated operations.

We believe many communities worldwide would have folk legends similar this of Chinese origin:

- Agents of secret societies would greet each other with secret phrases, thus authenticating their identities.

In this example, we use 2 tabs of Firefox browser to simulate two persons -- Alice and Chris -- communicating via websocket.

The source code this example can be found [here](https://github.com/udexon/XIDT/tree/master/XIDT). We assume the readers have basic knowledge of running apache2 or any other web server, and installing node modules. Start by running the websocket server with the following command:

```
node server.js
```

1. Each of Alice and Chris loads a web page, which contains JavaScript libraries for RSA encryption and WebSocket messaging:

http://localhost/XIDT/client.html

<img src="https://github.com/udexon/XIDT/blob/master/png/01_start.png" width=600>

Most of the input and output will be performed in the browser consoles, shown on the right side of the screenshot.

2. Alice and Chris execute a user initialisation script in the browser console, respectively:

中文： Alice (爱丽丝) 与 Chirs (克里斯) 执行了用户初始化脚本：

```js
Alice: F("Alice iu:")
```
```js
Chris: F("Chris iu:")
```

(We shall leave the detailed explanations for the Phos script and stack machine to [another article (here)](https://github.com/udexon/GOEHDOM/blob/master/PMSM.md), just to not clutter this entry level article.)

Alice and Chris then examine the stack which contains the results of executing the script, as shown in the link and screenshot below:

https://github.com/udexon/XIDT/blob/master/png/02_S.js

In the file above, we can see that there are 3 items on the stack in Alice's browser console:

中文： 在上述的文件里， Alice 的堆栈 (stack) 上有以下的数据：

`0`: Chris' JSON string （字串）, containing （含有） Chris' public key （公钥）(PBKC). 

`1`: Alice's public （公钥） and private key （私钥） pairs (stored （储存为） as an JavaScript object ).

`2`: Alice's JSON string （字串）, containing Alice's public key （公钥） (PBKA).

Similar items exist in the stack in Chris' browser console.

中文： 类似的数据在 Chris 的堆栈 (stack) 里也有。

<img src="https://github.com/udexon/XIDT/blob/master/png/02_init_user.png" width=600>

In this simple example, we merely copied a websocket broadcast example from elsewhere (all clients will receive the same message, including the sender). The crucial modification we made was line 22 in [`client.js`](https://github.com/udexon/XIDT/blob/master/XIDT/client.js), where the received message is pushed on to the stack:

```js
 S.push(event.data);
 ```

3. Chris imports public key of Alice (PBKA) and encrypts a secret phrase ("chris_love_cookie"), and sends the encrypted message to Alice.

中文： Chris 输入 Alice 的公钥， 加密一密令 ("chris_love_cookie" 克里斯爱曲奇饼)， 把密文发给 Alice。

```js
F("jd: pbk ix: imkey: .")
F("chris_loves_cookies ecr: wss:")

// jd: JSON.parse(), inherited from PHP json_decode(), input is top of stack (TOS)
// pbk ix: pick item with index pbk, ie. public key
// imkey: import key (works for both public key or private key)
// ecr: encrypt TOS
// wss: send message via web socket
```


<img src="https://github.com/udexon/XIDT/blob/master/png/03_chris_encrypt.png" width=600>

<img src="https://github.com/udexon/XIDT/blob/master/png/03_alice_S.png" width=600>

<img src="https://github.com/udexon/XIDT/blob/master/png/03_alice_S_highlight.png" width=600>


4. Alice decrypts the message using her own private key (PVKA).

中文： Alice 用自己的私钥解密密文。

```js
F("dcr:")
```

<img src="https://github.com/udexon/XIDT/blob/master/png/04_alice_decrypt.png" width=600>


5. Alice imports public key of Chris (PBKC) to encrypt the same message and sends it back to Chris.

中文： Alice 输入 Chris 的公钥， 把以解密的密文再加密 ("chris_love_cookie" 克里斯爱曲奇饼)， 再把密文发给 Chris。

```js
F("3 pick: jd: pbk ix: imkey: .")

// 3 pick: pick 3rd item below top of stack, duplicate it and push it at the top of stack
```

<img src="https://github.com/udexon/XIDT/blob/master/png/05_alice_encrypt.png" width=600>


6. Chris reimports his own public and private keys saved on the stack earlier.

中文： Chris 输入刚才储存在堆栈上的公钥和私钥。

```js
F("3 pick: pbk ix: imkey: pvk ix: imkey: .")

// . pops remaining object containing pbk/pvk
```

<img src="https://github.com/udexon/XIDT/blob/master/png/06_chris_pvk.png" width=600>

<img src="https://github.com/udexon/XIDT/blob/master/png/07_chris_imkey.png" width=600>



7. Chris decrypts the message with his own private key (PVKC). The result is shown by examining the stack object (array) `S`, where the top of stack (TOS) (last element in the array) is the decrypted secret phrase `chris_loves_cookies`.

中文： Chris 把密文解密。 堆栈变量 `S` 显示原来发出去的密令 `chris_loves_cookies`。

```js
F("dcr:")
```

<img src="https://github.com/udexon/XIDT/blob/master/png/07_chris_decrypt.png" width=600>
