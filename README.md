<div align="center">

## PHP Ping


</div>

### Description

Learn how to send a valid ping to another network device (with a correct ICMP checksum).
 
### More Info
 


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Philip Birk\-Jensen](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/philip-birk-jensen.md)
**Level**          |Advanced
**User Rating**    |4.8 (24 globes from 5 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Internet/ Browsers/ HTML](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/internet-browsers-html__8-9.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/philip-birk-jensen-php-ping__8-1786/archive/master.zip)





### Source Code

<style type="text/css">
a {
 text-decoration: none;
 border-bottom: 1px dashed #000000;
}
a:hover {
 color: #bb7722;
}
.aSnap {
 font-family: 'Lucida Console', monospace;
 font-size: 85%;
}
.aList {
 font-size: 85%;
 border: 1px solid #000000;
}
.lHeader {
 font-weight: bold;
 border-bottom: 1px solid #000000;
 background-color: #cccccc;
}
.lText-1 {
 background-color: #eeeeee;
}
.lText-2 {
 background-color: #dddddd;
}
.inLine {
 font-size: 85%;
 font-family: 'Lucida Console', monospace;
 line-height: 95%;
}
.aCode {
 background-color: #eeeeee;
 border: 1px solid #aaaaaa;
 padding: 5px;
 font-size: 85%;
 margin-left: 50px;
 margin-top: 0px;
 margin-bottom: 10px;
 line-height: 100%;
 font-family: 'Lucida Console', monospace;
 overflow: auto;
}
.cTitle {
 font-style: italic;
 font-size: 85%;
 margin-left: 75px;
 margin-top: 2px;
}
.cPHP     { color: #000077; }
.cFunction  { color: #dd0000; }
.cVariable  { color: #005599; }
.cConstant  { color: #666666; }
.cComment   { color: #009900; }
.cText    { color: #999900; }
.cReserved  { color: #000099; }
.cOwnFunction { color: #770000; }
.cOutput {
 margin: 0px;
 border: 1px solid #000000;
 padding: 3px;
 background-color: #ddddff;
 font-size: 85%;
}
.coTitle {
 font-style: italic;
 color: #0000ff;
 padding-left: 10px;
}
.aBody {
 font-family: sans-serif;
 font-size: 90%;
}
.aHead1 {
 background-color: #ccccff;
 border: 1px solid #000000;
 font-family: serif;
 font-size: 150%;
 padding-left: 15px;
 margin-top: 20px;
}
.aHead2 {
 background-color: #ccccff;
 border: 1px solid #000000;
 font-size: 110%;
 padding-left: 10px;
 margin-top: 5px;
}
.aSection {
 padding: 3px;
 padding-left: 10px;
 padding-bottom: 5px;
 line-height: 125%;
 border-left: 1px solid #cccccc;
 margin-bottom: 8px;
}
.aSubSection {
 padding: 3px;
 padding-left: 10px;
 padding-bottom: 5px;
 line-height: 125%;
 border-left: 1px solid #cccccc;
 margin-bottom: 8px;
}
.author {
 font-style: italic;
 font-size: 90%;
 text-align: center;
 letter-spacing: 1px;
}
.title {
 font-style: italic;
 font-size: 250%;
 text-align: center;
 letter-spacing: 2px;
 font-family: serif;
}
q {
 font-style: italic;
}
.printable {
 border: 1px solid #000000;
 width: 100px;
 text-align: center;
 font-size: 85%;
 font-family: sans-serif;
 background-color: #eeeeee;
 margin: 0px;
}
.txtSmall {
 font-size: 75%;
 line-height: 55%;
 margin-bottom: 3px;
}
ul {
 margin: 0;
 padding-left: 10px;
 list-style: none;
}
.binary {
 font-family: monospace;
 border-bottom: 1px dashed #999999;
}
</style>
<div class="aBody">
   <div class="title">PHP Ping</div>
   <div class="aHead1">Index</div>
   <div class="aSection">
    1) Introduction
    <div style="padding-left: 10px; padding-bottom: 5px;">
     1.1) Echo Message
    </div>
    2) Sockets<br />
    <div style="padding-left: 10px; padding-bottom: 5px;">
     2.1) Socket functions
    </div>
    3) The Package<br />
    <div style="padding-left: 10px; padding-bottom: 5px;">
     3.1) Calculating the checksum<br />
     3.2) Checksum source code
    </div>
    4) Conclusion
    <div style="padding-left: 10px; padding-bottom: 5px;">
     4.1) A code example<br />
    </div>
    <div style="font-size: 75%; margin-top: 5px;">
     a. Sources
     b. Understanding this article
    </div>
   </div>
   <div class="aHead1">1. Introduction</div>
   <div class="aSection">
    <em>Notice:</em> I will change between binary, decimal and hexadecimal notations, but if you let your mouse rest above the number, the 2 other notations will apear. Try moving your mouse over this number: <span class="binary" title="(Hex: a1 - Dec: 161)">1010 0001</span><br /><br />
    Before you start, let me warn you, that this may seem as some heavy reading, but hang in there :)<br />
    Remember you have to enable socket programming, if you're not sure how this is done, referer to the PHP manual, on installing<sup>[1]</sup> PHP.
    This article will walk you through creating a valid ping function in PHP. And in this process I will be covering network programming (shortly, you can always read about that somewhere else) and working with bitwise operations<sup>[2]</sup>. First off we'll be discussing how a valid ping (or Echo message, of the Internet Control Message Protocol).
    <div class="aHead2">1.1 Echo Message</div>
    <div class="aSubSection">
     To make a valid ping to another network device, it's important you follow the ICMP standard, they can be found in RFC-792<sup>[3]</sup>. And yes you're absolutly right RFC documents are just as boring as the dictionary, but sometimes they come in handy. I've decided to run through the standard quickly, so we can move on.<br />
     It's build up by 6 fields, which looks like the following:
     <table border="1" cellspacing="0" width="550" align="center" style="text-align: center;">
      <tr>
       <td width="25%">Type<div class="txtSmall">(8 bit)</div></td>
       <td width="25%">Code<div class="txtSmall">(8 bit)</div></td>
       <td width="50%">Checksum<div class="txtSmall">(16 bit)</div></td>
      </tr>
      <tr>
       <td width="50%" colspan="2">Identifier<div class="txtSmall">(16 bit)</div></td>
       <td width="50%">Sequence Number<div class="txtSmall">(16 bit)</div></td>
      </tr>
      <tr>
       <td width="100%" colspan="3">Data<div class="txtSmall">(... bit)</div></td>
      </tr>
     </table>
     Yep, it might seem a little confusing I know, but it's not that hard to understand. It's nothing but a single line of bits, starting with type and ending with data, now let me explain them a little deeper:
     <ul>
      <li><strong>Type:</strong> This defines what kind of message we whish to send. What we want to send is an <em>Echo Request</em>, which has the type <span class="binary" title="(Hex: 8 - Dec: 8)">1000</span>, there's a long list<sup>[4]</sup> of different messages, and their purpose.</li>
      <li><strong>Code:</strong> In our case we set the code to <span class="binary" title="(Hex: 0 - Dec: 0)">0000</span>, because the echo message dosn't have any other options. You can compare the Type with the function and the Code with the parameters.</li>
      <li><strong>Checksum:</strong> The checksum<sup>[5]</sup> is calculated when then package is assembled, to start with we set the checksum to <span class="binary" title="(Hex: 00 - Dec: 0)">0000 0000</span>. Then later the checksum is calculated by one's Complement. If you're not use to binary operations, this will be hard to explain, and there's no easy reading on the net, try to google it<sup>[6]</sup>.</li>
      <li><strong>Identifier:</strong> In the original ping program, this is the UNIX process ID, but in our ping it can be anything. Normaly I just set it to <span class="binary" title="(Hex: 00 - Dec: 0)">0000 0000</span>, but it's all up to you. In some cases it could be smart to make it unique so you can recongnize your ICMP package.</li>
      <li><strong>Sequence Number:</strong> Again just a number, in our case it's <span class="binary" title="(Hex: 00 - Dec: 0)">0000 0000</span> as the Identifier. But a good use for this, is to increment it if you run more than 1 ping at a time.</li>
      <li><strong>Data:</strong> This can be any data. In our case, we use: <em title="8 byte long">"Scarface"</em></li>
     </ul>
     So basicly that is the package we wish to make, for our ping to be correct. The hard thing here is the checksum, we will work with this later on in the article.
    </div>
   </div>
   <div class="aHead1">2. Sockets</div>
   <div class="aSection">
    Before we start designing our package (well talking about calculating the checksum), lets talk a little about network programming.<br />
    Normally when people talk about network programming, they're talking about TCP/IP or UDP/IP protocols. But we are going to use the ICMP protocol. But enough about that, let's start looking at the functions we'll be using.
    <div class="aHead2">2.1 Socket functions</div>
    <div class="aSubSection">
     Working with sockets are much like working with a file or a database. So if you're used to working with a database (like MySQL, I know that probably a lot of you are), this wont be that new to you. To start with, I'm going to make a table over the socket functions we'll be using and an equel (well almost) function in MySQL and Filesystem functions (mainly consult the filesystem, but I included MySQL because I'm convinced more people are familiar with those functions):
     <table width="100%" cellspacing="0" cellpadding="0">
      <tr>
       <td width="15%"><strong>Socket</strong></td>
       <td width="15%"><strong>MySQL</strong></td>
       <td width="15%"><strong>File</strong></td>
       <td width="55%"><strong>Description</strong></td>
      </tr>
      <tr style="height: 1px; background-color: #999999;">
       <td width="15%"></td>
       <td width="15%"></td>
       <td width="15%"></td>
       <td width="55%"></td>
      </tr>
      <tr valign="top" style="background-color: #eeeeee">
       <td width="15%">socket_create()</td>
       <td width="15%">-</td>
       <td width="15%">-</td>
       <td width="55%" style="font-size: 90%;">This function creates a socket, that we can use to connect to other network devices.</td>
      </tr>
      <tr valign="top">
       <td width="15%">socket_connect()</td>
       <td width="15%">mysql_connect()</td>
       <td width="15%">fopen()</td>
       <td width="55%" style="font-size: 90%;">Make a connection to a host. This needs the resource from the socket_create() function.</td>
      </tr>
      <tr valign="top" style="background-color: #eeeeee">
       <td width="15%">socket_write()</td>
       <td width="15%">mysql_query()</td>
       <td width="15%">fwrite()</td>
       <td width="55%" style="font-size: 90%;">Send a string to the other network device, like writing to a fileor using INSERT INTO in an SQL query.</td>
      </tr>
      <tr valign="top">
       <td width="15%">socket_read()</td>
       <td width="15%">mysql_fetch_??()</td>
       <td width="15%">fread()</td>
       <td width="55%" style="font-size: 90%;">Read a string send by the other network device..</td>
      </tr>
      <tr valign="top" style="background-color: #eeeeee">
       <td width="15%">socket_close()</td>
       <td width="15%">mysql_close()</td>
       <td width="15%">fclose()</td>
       <td width="55%" style="font-size: 90%;">Closes the socket resource created with the socket_create function.</td>
      </tr>
     </table>
     <br />
     There is a lot of other network functions, that comes in handy when you'r network programming, but we will only be using the ones above. This article isn't as much a socket article, as it's an article about learning the Internet checksum and how to assemble an easy ICMP package. And to be honest, this article is written for people who already knows a little about network programming (but if you don't, hey it dosn't matter just keep reading, you might learn something).
    </div>
    Lets pretend we've made our package already, so all we need to do is make the connection, send the package and wait for it to return (just as easy as it sounds, try saying that out loud a couple times).
    <div class="cTitle">Socket programming</div>
    <pre class="aCode"><span class="cPHP">&lt;?php</span>
<span class="cVariable">$socket</span> = <span class="cFunction">socket_create</span>(<span class="cConstant">AF_INET</span>, <span class="cConstant">SOCK_RAW</span>, 1);
<span class="cFunction">socket_connect</span>(<span class="cVariable">$socket</span>, <span class="cText">"www.google.com"</span>, <span class="cConstant">null</span>);
<span class="cComment">// If you're using below PHP 5, see the manual for the microtime_float
// function. Instead of just using the microtime() function.</span>
<span class="cVariable">$startTime</span> = <span class="cFunction">microtime</span>(<span class="cConstant">true</span>);
<span class="cFunction">socket_send</span>(<span class="cVariable">$socket</span>, <span class="cVariable">$package</span>, <span class="cFunction">strLen</span>(<span class="cVariable">$package</span>), 0);
if (<span class="cFunction">socket_read</span>(<span class="cVariable">$socket</span>, 255)) {
  <span class="cFunction">echo</span> <span class="cFunction">round</span>(<span class="cFunction">microtime</span>(<span class="cConstant">true</span>) - <span class="cVariable">$startTime</span>, 4);
}
<span class="cFunction">socket_close</span>(<span class="cVariable">$socket</span>);
<span style="color: #000077;" class="cPHP">?&gt;</span></pre>
   We start by creating a new socket. This socket uses IPv4(<span class="inLine">AF_INET</span>), and the data is all handled by the user(<span class="inLine">SOCK_RAW</span>) using the ICMP protocol(the last <span class="inLine">1</span> represents the ICMP protocol).<br />
   Next up we choose an addresse to ping, I've selected google because we can be almost sertain that it's online (and if it's not it's easy to check). The <span class="inLine">microtime()</span> is just to get a response time.<br />
   Then we send our package, and wait for it to return, and if it returns we post the response time (in seconds). Last up we close the socket we created.
   </div>
   <div class="aHead1">3. The Package</div>
   <div class="aSection">
    Now we come to the hard part. This is a bit more difficult (hehe, notice a <em>bit</em> I'm so funny), because it's not only PHP here, you also need to know something about working with binary numbers. Scroll a bit upwards, and take a look at the 2 links [5] &amp; [6], or well click them here. But lets start with the easy part, making the package with the checksum set to <span class="binary" title="(Hex: 00 - Dec: 0)">0000 0000</span>:
    <div class="cTitle">Package (before checksum calculation)</div>
    <pre class="aCode"><span class="cPHP">&lt;?php</span>
<span class="cVariable">$type</span>    = <span class="cText">"\x08"</span>;
<span class="cVariable">$code</span>    = <span class="cText">"\x00"</span>;
<span class="cVariable">$checksum</span>  = <span class="cText">"\x00\x00"</span>;
<span class="cVariable">$identifier</span> = <span class="cText">"\x00\x00"</span>;
<span class="cVariable">$seqNumber</span> = <span class="cText">"\x00\x00"</span>;
<span class="cVariable">$data</span>    = <span class="cText">"Scarface"</span>;
<span class="cVariable">$package</span> = <span class="cVariable">$type</span>.<span class="cVariable">$code</span>.<span class="cVariable">$checksum</span>.<span class="cVariable">$identifier</span>.<span class="cVariable">$seqNumber</span>.<span class="cVariable">$data</span>;
<span style="color: #000077;" class="cPHP">?&gt;</span></pre>
   Notice that I use <span class="inLine">"\x08"</span> instead of <span class="inLine">ord(8)</span>, use what you like but using <span class="inLine">ord(8)</span> can sometimes make it harder to understand the whole working with bitwise operations thing. But lets move on to the big nasty checksum.
   <div class="aHead2">3.1 Calculating the checksum</div>
    <div class="aSubSection">
     As I mentioned earlier the checksum is <em>1's Complement</em> of the whole package. This is done with the following steps (I must admit, that I'm not very good at explaining this):
     <ul>
      <li><strong>1)</strong> If the length of the string is an odd number, add a <span class="binary" title="(Hex: 00 - Dec: 0)">0000</span>.</li>
      <li><strong>2)</strong> We devide the whole string, 2-by-2 (16 bit, or 2 characters).</li>
      <li><strong>3)</strong> Add them all together so you get just a single sum.</li>
      <li><strong>4)</strong> If the sum of the string is more than 16bit, then just add the carrys.</li>
      <li><strong>5)</strong> Now do the complemented (exchange all the 1's with 0's and vice versa, also called NOT).</li>
     </ul><br />
     <strong>1)</strong> I got a string of 6 bytes (guess what it says):<br />
     <center><span class="binary" title="(Hex: 70 - Dec: 120)">0111 0000</span> | <span class="binary" title="(Hex: 68 - Dec: 104)">0110 1000</span> | <span class="binary" title="(Hex: 69 - Dec: 105)">0110 1001</span> | <span class="binary" title="(Hex: 6c - Dec: 108)">0110 1100</span> | <span class="binary" title="(Hex: 69 - Dec: 105)">0110 1001</span> | <span class="binary" title="(Hex: 70 - Dec: 120)">0111 0000</span></center><br />
     <strong>2)</strong> To make it easier for myself, I start by adding them up 2-by-2:<br>
     <table width="50%" align="center" cellspacing="0" cellpadding="0">
      <tr>
       <td width="33%" align="center"><span class="binary" title="(Hex: 70 68 - Dec: 28776)">0111 0000 0110 1000</span></td>
       <td width="33%" align="center"><span class="binary" title="(Hex: 69 6c - Dec: 26988)">0110 1001 0110 1100</span></td>
       <td width="33%" align="center"><span class="binary" title="(Hex: 69 70 - Dec: 26992)">0110 1001 0111 0000</span></td>
      </tr>
     </table>
     <strong>3)</strong> Then we add them together, 1-by-1 so it's easier to understand:<br>
     <table align="center" cellspacing="0" cellpadding="0" width="250">
      <tr>
       <td width="75px">Carrys: </td>
       <td align="right"><span class="binary" style="border-bottom: 0;">11&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;11&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
      </tr>
      <tr>
       <td>1st: </td>
       <td align="right"><span class="binary" title="(Hex: 70 68 - Dec: 28776)">0111 0000 0110 1000</span></td>
      </tr>
      <tr>
       <td>2nd: </td>
       <td align="right"><span class="binary" title="(Hex: 69 6c - Dec: 26988)">0110 1001 0110 1100</span></td>
      </tr>
      <tr>
       <td style="height: 1px; background-color: #000000;"></td>
       <td style="height: 1px; background-color: #000000;"></td>
      </tr>
      <tr>
       <td>Result1: </td>
       <td align="right"><span class="binary" title="(Hex: D9 D4 - Dec: 55764)">1101 1001 1101 0100</span></td>
      </tr>
     </table><br />
     <table align="center" cellspacing="0" cellpadding="0" width="250">
      <tr>
       <td width="75px">Carrys: </td>
       <td align="right"><span class="binary" style="border-bottom: 0;">1&nbsp;111&nbsp;&nbsp;1&nbsp;11&nbsp;111&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
      </tr>
      <tr>
       <td>Result1: </td>
       <td align="right"><span class="binary" title="(Hex: D9 D4 - Dec: 55764)">1101 1001 1101 0100</span></td>
      </tr>
      <tr>
       <td>3rd: </td>
       <td align="right"><span class="binary" title="(Hex: 69 70 - Dec: 26992)">0110 1001 0111 0000</span></td>
      </tr>
      <tr>
       <td style="height: 1px; background-color: #000000;"></td>
       <td style="height: 1px; background-color: #000000;"></td>
      </tr>
      <tr>
       <td>Result2: </td>
       <td align="right"><span class="binary" title="(Hex: 01 43 44 - Dec: 82756)">1 0100 0011 0100 0100</span></td>
      </tr>
     </table><br />
     <strong>4)</strong> Now we end up with a result that is longer than 16bit, so we will take the all above the 16 bits, and add it to the lower bits:
     <table align="center" cellspacing="0" cellpadding="0" width="250">
      <tr>
       <td width="75px">Carrys: </td>
       <td align="right"><span class="binary" style="border-bottom: 0;">1&nbsp;111&nbsp;&nbsp;1&nbsp;11&nbsp;111&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span></td>
      </tr>
      <tr>
       <td>High: </td>
       <td align="right"><span class="binary" title="(Hex: 00 01 - Dec: 1)">0000 0000 0000 0001</span></td>
      </tr>
      <tr>
       <td>Lower: </td>
       <td align="right"><span class="binary" title="(Hex: 43 44 - Dec: 17220)">0100 0011 0100 0100</span></td>
      <tr>
       <td style="height: 1px; background-color: #000000;"></td>
       <td style="height: 1px; background-color: #000000;"></td>
      </tr>
      <tr>
       <td>Result2: </td>
       <td align="right"><span class="binary" title="(Hex: 43 45 - Dec: 17221)">0100 0011 0100 0101</span></td>
      </tr>
     </table><br />
     <strong>5)</strong> And the last thing to do is to take the complemented:
     <table align="center" cellspacing="0" cellpadding="0" width="250">
      <tr>
       <td>Result2: </td>
       <td align="right"><span class="binary" title="(Hex: 43 45 - Dec: 17221)">0100 0011 0100 0101</span></td>
      </tr>
      <tr>
       <td>NOT: </td>
       <td align="right"></td>
      <tr>
       <td style="height: 1px; background-color: #000000;"></td>
       <td style="height: 1px; background-color: #000000;"></td>
      </tr>
      <tr>
       <td>Final: </td>
       <td align="right"><span class="binary" title="(Hex: BC BA - Dec: 48314)">1011 1100 1011 1010</span></td>
      </tr>
     </table><br /><br />
     Okay, well now that's over with you're propably a bit frustrated because you didn't get it, but unfortunatly I can't help you that much. Personally it was a long lasting battle, before I finally got how this whole thing works, the only thing I can suggest is that you try to read some articles and notes about Bitwise operations and about the 1's complemented (but start with bitwise operations).<br />
     The only difference from my example above, is that I have the example in Binary notation, and not hex which most examples are in. And remember to use that you can get the hex and decimal value when you move your mouse over one of the binary numbers.
    </div>
    <div class="aHead2">3.2 Checksum source code</div>
    <div class="aSubSection">
     Now that you've learned how to calculate the 1'st Complemented (or well saved it for later), let's make a function that can calculate this for us. Before I present you with this little wonder of a function, it's a good idea to read up on the following functions (and operators): unpack<sup>[7]</sup>, pack<sup>[8]</sup> and Bitwise Operators<sup>[9]</sup>. But enough talk, on with the show:
     <div class="cTitle">ICMP Checksum calculator</div>
    <pre class="aCode"><span class="cPHP">&lt;?php</span>
<span class="cReserved">function</span> <span class="cOwnFunction">icmpChecksum</span>(<span class="cVariable">$data</span>)
{
  <span class="cReserved">if</span> (<span class="cFunction">strlen</span>(<span class="cVariable">$data</span>)%2)
    <span class="cVariable">$data</span> .= <span class="cText">"\x00"</span>;
  <span class="cVariable">$bit</span> = <span class="cFunction">unpack</span>(<span class="cText">'n*'</span>, <span class="cVariable">$data</span>);
  <span class="cVariable">$sum</span> = <span class="cFunction">array_sum</span>(<span class="cVariable">$bit</span>);
  <span class="cReserved">while</span> (<span class="cVariable">$sum</span> >> 16)
    <span class="cVariable">$sum</span> = (<span class="cVariable">$sum</span> >> 16) + (<span class="cVariable">$sum</span> & 0xffff);
  <span class="cReserved">return</span> <span class="cFunction">pack</span>(<span class="cText">'n*'</span>, ~<span class="cVariable">$sum</span>);
}
<span style="color: #000077;" class="cPHP">?&gt;</span></pre>
     Ya I know, again it's not something you just understand as you read it, but you have to look through it a couple of times. But hey I can help you a little, let's walk it through step by step, as when we did it manually:<br />
     <strong>1)</strong> First off we check if the data is of odd length <span class="inLine">if (strlen($data)%2)</span>, and well if it is we add the <span class="binary" title="(Hex: 00 - Dec: 0)">0000</span> value.<br />
     <strong>2)</strong> The <span class="inLine">unpack()</span> function does all the dirty work here, it splits the string up 2-by-2 (just the way we like it) and throws it into an array.<br />
     <strong>3)</strong> Luckily PHP has the <span class="inLine">array_sum()</span> function so we don't have to make some ugly loop to sum it all up.<br />
     <strong>4)</strong> Our while loop, will take all the bits <em>above</em> the 16<sup>th</sup> bit, and add them to the 16 lower bits.<br />
     <strong>5)</strong> And the last thing we do is to perform the not(<span class="inLine">~</span>) operation. Then the <span class="inLine">pack()</span> function will swap it all back to a string for us.<br /><br />
     Let's do a little testing. Let's try to run our string we calculated manually, and see if the result is the same.
     <div class="cTitle">Calculator test</div>
     <pre class="aCode"><span class="cPHP">&lt;?php</span>
<span class="cComment">// oh ya, and if you haven't checked what the string was yet,
// it was "philip" (ya I know, that's me :))</span>
<span class="cVariable">$chk</span> = <span class="cOwnFunction">icmpChecksum</span>(<span class="cText">"philip"</span>);
<span class="cFunction">echo</span> <span class="cFunction">decbin</span>(<span class="cFunction">ord</span>(<span class="cVariable">$chk</span>[0])) ." ". <span class="cFunction">decbin</span>(<span class="cFunction">ord</span>(<span class="cVariable">$chk</span>[1]));
<span class="cComment">// I've cheated a little bit, so you can move your mouse over the below output,
// and as always get the hex and dec value and character</span>
<span style="color: #000077;" class="cPHP">?&gt;</span>
<div class="cOutput"><span class="coTitle">Output:</span>
<span title="(Hex: BC BA - Dec: 188 186 - Char: &#188; &#186;)">10111100 10111010</span></div></pre>
    </div>
    Well it seemed to work, so jump on down to the conclusion, where I've thrown a short script together, that pings google.
   </div>
   <div class="aHead1">4. Conclusion</div>
   <div class="aSection">
    As promissed here's a little example.
    <div class="aHead2">4.1 A code example</div>
    <div class="aSubSection">
     <div class="cTitle">Ping google</div>
    <pre class="aCode"><span class="cPHP">&lt;?php</span>
<span class="cComment">// Checksum calculation function</span>
<span class="cReserved">function</span> <span class="cOwnFunction">icmpChecksum</span>(<span class="cVariable">$data</span>)
{
  <span class="cReserved">if</span> (<span class="cFunction">strlen</span>(<span class="cVariable">$data</span>)%2)
    <span class="cVariable">$data</span> .= <span class="cText">"\x00"</span>;
  <span class="cVariable">$bit</span> = <span class="cFunction">unpack</span>(<span class="cText">'n*'</span>, <span class="cVariable">$data</span>);
  <span class="cVariable">$sum</span> = <span class="cFunction">array_sum</span>(<span class="cVariable">$bit</span>);
  <span class="cReserved">while</span> (<span class="cVariable">$sum</span> >> 16)
    <span class="cVariable">$sum</span> = (<span class="cVariable">$sum</span> >> 16) + (<span class="cVariable">$sum</span> & 0xffff);
  <span class="cReserved">return</span> <span class="cFunction">pack</span>(<span class="cText">'n*'</span>, ~<span class="cVariable">$sum</span>);
}
<span class="cComment">// Making the package</span>
<span class="cVariable">$type</span>    = <span class="cText">"\x08"</span>;
<span class="cVariable">$code</span>    = <span class="cText">"\x00"</span>;
<span class="cVariable">$checksum</span>  = <span class="cText">"\x00\x00"</span>;
<span class="cVariable">$identifier</span> = <span class="cText">"\x00\x00"</span>;
<span class="cVariable">$seqNumber</span> = <span class="cText">"\x00\x00"</span>;
<span class="cVariable">$data</span>    = <span class="cText">"Scarface"</span>;
<span class="cVariable">$package</span> = <span class="cVariable">$type</span>.<span class="cVariable">$code</span>.<span class="cVariable">$checksum</span>.<span class="cVariable">$identifier</span>.<span class="cVariable">$seqNumber</span>.<span class="cVariable">$data</span>;
<span class="cVariable">$checksum</span> = <span class="cOwnFunction">icmpChecksum</span>(<span class="cVariable">$package</span>); <span class="cComment">// Calculate the checksum</span>
<span class="cVariable">$package</span> = <span class="cVariable">$type</span>.<span class="cVariable">$code</span>.<span class="cVariable">$checksum</span>.<span class="cVariable">$identifier</span>.<span class="cVariable">$seqNumber</span>.<span class="cVariable">$data</span>;
<span class="cComment">// And off to the sockets</span>
<span class="cVariable">$socket</span> = <span class="cFunction">socket_create</span>(<span class="cConstant">AF_INET</span>, <span class="cConstant">SOCK_RAW</span>, 1);
<span class="cFunction">socket_connect</span>(<span class="cVariable">$socket</span>, <span class="cText">"www.google.com"</span>, <span class="cConstant">null</span>);
<span class="cComment">// If you're using below PHP 5, see the manual for the microtime_float
// function. Instead of just using the microtime() function.</span>
<span class="cVariable">$startTime</span> = <span class="cFunction">microtime</span>(<span class="cConstant">true</span>);
<span class="cFunction">socket_send</span>(<span class="cVariable">$socket</span>, <span class="cVariable">$package</span>, <span class="cFunction">strLen</span>(<span class="cVariable">$package</span>), 0);
if (<span class="cFunction">socket_read</span>(<span class="cVariable">$socket</span>, 255)) {
  <span class="cFunction">echo</span> <span class="cFunction">round</span>(<span class="cFunction">microtime</span>(<span class="cConstant">true</span>) - <span class="cVariable">$startTime</span>, 4) .<span class="cText">' seconds'</span>;
}
<span class="cFunction">socket_close</span>(<span class="cVariable">$socket</span>);
<span style="color: #000077;" class="cPHP">?&gt;</span></pre>
    </div>
    And well this time I can conclude, that it sometimes pays to be patient. It's been a true battle making this article, because I started with nothing but an idea for a ping program in PHP. I learned what I've tried to tell all of your guys here, and I think I ded a fair job(it's always easier to understand things when you knwo the right!). It was mainly the bitwise operations that where the trick for me, and I've tried explaining them the best I could.<br /><br />
   </div>
   <div class="aHead1">a. Sources</div>
   <div class="aSection">
    [1] http://www.php.net/manual/en/install.php<br />
    [2] http://en.wikipedia.org/wiki/Bitwise_operations<br />
    [3] http://www.ietf.org/rfc/rfc792.txt<br />
    [4] http://www.iana.org/assignments/icmp-parameters<br />
    [5] http://www.faqs.org/rfcs/rfc1071.html<br />
    [6] http://www.google.com/search?hl=en&q=%22One%27s+Complement%22&btnG=Google+Search<br />
    [7] http://www.php.net/manual/en/function.unpack.php<br />
    [8] http://www.php.net/manual/en/function.pack.php<br />
    [9] http://www.php.net/manual/en/language.operators.bitwise.php<br /><br />
    [*] http://ftp.arl.mil/~mike/ping.html :: The Story of the PING Program
   </div>
   <div class="aHead1">b. Understanding this article</div>
   <div class="aSection">Well the only purpose of this section, is to clearify a little something about this article. And it will just be done in no particular order:<br /><br />
   - I've colored the codes my self, so if there are some color errors, please just leave some feedback, and I'll fix it. If yuo have any complaints about the colors I've used for the different syntax, then I don't want to hear about it, copy the code into your own favorit PHP editor.<br />
   - If you find anything offending, then again don't say a word or I'll get you, and I'll get you good :p<br />
   - Well that was about it, understanding this article. Now remember please leave some feadback, nothing says "sweeeeet" like good feedback.
   </div>
   <div class="author">- Philip Birk-Jensen, January 2005 -</div>
  </div>

