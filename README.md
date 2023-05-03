Download Link: https://assignmentchef.com/product/solved-cs2040s-recitation-6
<br>
<strong>Problem 1.              To Download or Not to Download</strong>

Alice has a very large collection of digital photos, consisting of several hundred gigabytes of data. In order to ensure that her photos are stored safely, she prudently maintains backup copies of all her photos on <em>Mazonia Storage</em>—a cloud-based server storage service.

Recently, some of Alice’s local photos are lost because her hard drive got infected by <em>Claudius</em>, a computer virus. Worse, Claudius corrupted all of the filenames (overwriting the metadata in the <a href="https://searchwindowsserver.techtarget.com/definition/master-file-table">Master File Table</a><a href="https://searchwindowsserver.techtarget.com/definition/master-file-table">)</a>, replacing them with text from Shakespeare’s <a href="https://en.wikipedia.org/wiki/Hamlet"><em>Hamlet</em></a><a href="https://en.wikipedia.org/wiki/Hamlet">.</a>

Alice’s goal now is to recover her missing photos. It may be helpful to note that since Alice is meticulous in organizing and curating her collection, no photo duplicates exist within it.

Given that Alice has so many photos, it would take a very long time to download all of them from Mazonia Storage’s server. The practical approach is therefore to download only the missing photos, i.e., those that were deleted by the virus.

For this problem, we shall denote the following:

<ul>

 <li>Let <em>n </em>be the original number of photos Alice have <em>remotely</em></li>

 <li>Let <em>m &lt; n </em>be the remaining number of photos Alice have <em>locally</em></li>

 <li>Let <em>r</em><sub>1</sub><em>,…,r<sub>i</sub>,…,r<sub>n </sub></em>be the photos on Alice’s <em>remote </em>cloud server</li>

 <li>Let <em>`</em><sub>1</sub><em>,…,`<sub>i</sub>,…,`<sub>m </sub></em>be the photos on Alice’s <em>local </em>computer</li>

</ul>

Having studied CS2040S, Alice immediately think of using a hash-based signature and proposes the following algorithm:

<ol>

 <li>Pick <em>any </em>hash function <em>h </em>that maps a photograph to an integer in the range [1<em>,n</em>]</li>

 <li>For each photo <em>`<sub>i </sub></em>: <em>i </em>∈ [1<em>,m</em>] on Alice’s <em>local </em>computer,

  <ul>

   <li>Compute its hash value <em>h</em>(<em>`<sub>i</sub></em>)</li>

   <li>Save <em>h</em>(<em>`<sub>i</sub></em>) to a local file <em>H<sub>`</sub></em></li>

  </ul></li>

 <li>For each photo <em>r<sub>i </sub></em>on the <em>remote </em>server:

  <ul>

   <li>Compute its hash value <em>h</em>(<em>r<sub>i</sub></em>)</li>

   <li>Download <em>h</em>(<em>r<sub>i</sub></em>) to Alice’s local computer

    <ul>

     <li>If <em>h</em>(<em>r<sub>i</sub></em>) is not found in <em>H<sub>`</sub></em>, download photo <em>r<sub>i</sub></em></li>

     <li>Else, continue the loop</li>

    </ul></li>

  </ul></li>

</ol>

<strong>Problem 1.a. </strong>What are Alice’s objectives of using a hash function in this scheme? What is the key to success in achieving those objectives?

<strong>Problem 1.b.            </strong>Is <em>H<sub>` </sub></em>a hash table?

<strong>Problem 1.c. </strong>Alice claims that this scheme will efficiently restore <em>all </em>the missing photos to her computer. Is she right? Explain why or why not.

<strong>Problem 1.d. </strong>What if Alice modified her solution by adding separate chaining to <em>H<sub>`</sub></em>? What would be stored in each bucket? Would this serve as an effective solution?

Alice also propose a second scheme where she randomly picks a hash function until she finds one that fits her criteria:

<ol>

 <li>Let <em>k </em>be some integer (which may depend on <em>n </em>and <em>m</em>)</li>

 <li>Repeat:

  <ul>

   <li><em>Randomly </em>pick a hash function <em>h </em>that maps a photograph to an integer in the range</li>

  </ul></li>

</ol>

[1<em>,k</em>]

<ul>

 <li>For each photo <em>`<sub>i </sub></em>: <em>i </em>∈ [1<em>,m</em>] on Alice’s <em>local </em>computer

  <ul>

   <li>Compute its hash value <em>h</em>(<em>`<sub>i</sub></em>)</li>

   <li>Save <em>h</em>(<em>`<sub>i</sub></em>) to a local file <em>H<sub>`</sub></em></li>

  </ul></li>

 <li>For each photo <em>r<sub>i </sub></em>: <em>i </em>∈ [1<em>,n</em>] on the <em>remote </em>server

  <ul>

   <li>Compute its hash value <em>h</em>(<em>r<sub>i</sub></em>)</li>

   <li>Save <em>h</em>(<em>r<sub>i</sub></em>) to remote file <em>H<sub>r</sub></em></li>

  </ul></li>

 <li>Download <em>H<sub>r </sub></em>to Alice’s local computer</li>

 <li>If (|<em>H<sub>r</sub></em>| − |<em>H<sub>`</sub></em>|) = (<em>n </em>− <em>m</em>),

  <ul>

   <li>Download the photos <em>r<sub>i </sub></em>whose hash value <em>h</em>(<em>r<sub>i</sub></em>) is in <em>H<sub>r </sub></em>but not in <em>H<sub>`</sub></em></li>

   <li>Terminate the repeat loop</li>

  </ul></li>

 <li>Else, continue the loop to look for a better hash function</li>

</ul>

<strong>Problem 1.e. </strong>An interesting criteria for picking the random hash function is stated in Step 2.5.. Why didn’t Alice simply chose the condition to be |<em>H<sub>r</sub></em>| = <em>n </em>&amp;&amp; |<em>H<sub>`</sub></em>| = <em>m</em>?

<strong>Problem 1.f. </strong>If we think about <em>H<sub>r </sub></em>and <em>H<sub>` </sub></em>respectively as the set of hash values <em>before </em>and <em>after </em>a set of deletion operations, what is the “invariance” in the desired hash function here?

<strong>Problem 1.g. </strong>In the second scheme, what is Alice’s objective of using a hash function? <em>Hint: </em>look at the invariance. Why does the criteria (|<em>H<sub>r</sub></em>| − |<em>H<sub>`</sub></em>|) = (<em>n </em>− <em>m</em>) satisfy this objective? Show that when the loop terminates, it means Alice has correctly downloaded all the missing photos.

After some investigation, Alice learnt that the virus had only erased a single consecutive block of photos. Given that her photos were stored on her local hard drive in sequence, the virus simply deleted a contiguous subsequence of photos of length <em>δ</em>. This is illustrated as follows.

<table width="340">

 <tbody>

  <tr>

   <td width="106"><em>`</em><sub>1</sub><em>,`</em><sub>2</sub><em>,…,`<sub>j</sub></em>−<sub>1</sub></td>

   <td width="111"><em>`</em><em>j</em><em>,…,`<sub>j</sub></em>+<em>δ</em>−1</td>

   <td width="123"><em>`<sub>j</sub></em>+<em>δ</em><em>,…,`<sub>n</sub></em>−1<em>,`<sub>n</sub></em></td>

  </tr>

 </tbody>

</table>

Deleted photos

Realize the value of <em>δ </em>can be simply calculated as the difference between the number of remote photos and local photos.

Unfortunately, Alice has no idea which photos were deleted. Moreover, Alice’s internet connection is very slow, so much so that even transmitting a file containing <em>n </em>hash values will take too long! To make matters worst, Mazonia charges its clients for every bit transmitted to and fro the server.

Due to these reasons, Alice is forced to limit the amount of communication with the remote server as much as possible. Fortunately, all is not lost because in this time Alice cleverly devised a <em>perfect hash function h </em>which will not produce any collisions on her original set of <em>n </em>photos. She already uploaded this function so it is now available on both the server and her local computer.

<strong>Problem 1.h.    </strong>Given the new findings, design two variants of algorithms to help Alice identify the deleted photos:

Variant 1: Hash values are only computed on individual photos

Variant 2: Hash values are also computed over contiguous subsequences of photos Meanwhile, your algorithms must satisfy the following efficiency constraints:

Constraint 1: Transmit at most <em>O</em>(log<em>n</em>) hash values and a constant number of additional integer values to and fro the Mazonia server

Constraint 2: Incur only an additional <em>O</em>(1) space

For now, you may assume that hash value computation with <em>h </em>is <em>O</em>(1). Explain why your algorithms work and give their running times.

<strong>Problem 2.              Putting the Sum in DimSum</strong>

You have an unsorted array <em>A </em>containing <em>n </em>integers where each element represents an <em>item price </em>on the menu at <em>Dim-Sum Dollars</em>—your favorite dim sum restaurant, and its index representing the <em>item number </em>on the menu. Having <em>x </em>dollars on hand in cash and wanting to avoid loose change, you seek to purchase two items such that their price sums up to <em>exactly x</em>.

For example, given the following menu:

<table width="311">

 <tbody>

  <tr>

   <td width="39">$30</td>

   <td width="39">$8</td>

   <td width="39">$15</td>

   <td width="39">$18</td>

   <td width="39">$23</td>

   <td width="39">$20</td>

   <td width="39">$25</td>

   <td width="39">$1</td>

  </tr>

 </tbody>

</table>

#1       #2       #3       #4       #5       #6       #7       #8

If your cash on hand is <em>x </em>= $33, then there are two possible item pairs whose values sum up to that amount, namely pairing #2 ($8) with #7 ($25) and pairing #3 ($15) with #4 ($18).

Your task is therefore to propose algorithms which will find you <em>any </em>such winning pairs of dim sum items on the menu.

<strong>Problem 2.a. </strong>Come up with an algorithm which finds a valid pair of item <em>numbers </em>if it exists. For instance in the given example above, either (#2<em>,</em>#7) or (#3<em>,</em>#4) will be a valid pair. your solution must only incur <em>O</em>(1) space. What is its time complexity?

<strong>Problem 2.b. </strong>Now come up with an algorithm which finds a valid pair of item <em>prices </em>if it exists. For instance in the given example above, either ($8<em>,</em>$25) or ($15<em>,</em>$18) will be a valid pair. Your solution must only incur <em>O</em>(log<em>n</em>) extra space. What is its time complexity?

How might you then modify your solution to return a valid pair of item <em>numbers </em>instead and what are the additional overheads (if any) due to your modification?

<strong>Problem 2.c. </strong>Finally, come up with the <em>fastest </em>algorithm which finds a valid pair of item <em>numbers </em>if it exists. For instance in the given example above, either (#2<em>,</em>#7) or (#3<em>,</em>#4) will be a valid pair. Your solution may now incur Θ(<em>n</em>) extra space. What is its time complexity?

How might you modify your solution to cater for duplicate prices?

Depending on your solution proposed, you might have introduced a subtle caveat. <em>Hint: </em>What happens when target sum is an even number?

<strong>Problem 2.d. </strong>How might you minimally modify the previous 3 algorithms such that instead of just finding one valid pair, <em>all valid pairs </em>will be returned by the algorithm?

<strong>Problem 2.e. </strong>What if instead of two, now you want to find <em>three </em>elements <em>a,b,c </em>in the array that sum to <em>x</em>. Can you generalize the previous solutions to solve this variant?

<em>Did you know? </em>This is the classic <a href="https://en.wikipedia.org/wiki/3SUM">3SUM</a> problem! It turns out that there exists many important problems which either reduces to this form or entails a subproblem that does. There is actually a lot of ongoing research trying to understand the best possible solution for 3SUM!