Download Link: https://assignmentchef.com/product/solved-cs3750-homework2-encryption-and-decryption
<br>
<strong>Task I  Write two Java* programs, one for encryption and the other for decryption, to implement TEA </strong>

(modified from Textbook): Perhaps the simplest “serious” symmetric block          <strong><sup>L</sup></strong><strong><sup>0                    </sup></strong><strong><sup>R</sup></strong><strong><sup>0 </sup></strong>encryption algorithm is the Tiny Encryption Algorithm (TEA). TEA operates on 64- bit blocks of plaintext using a 128- bit key. The <strong><em>plaintext </em></strong>is divided into two 32- bit blocks <strong>(<em>L</em><sub>0</sub>, <em>R</em><sub>0</sub>)</strong>, and the <strong><em>key</em></strong> is divided into four 32-bit blocks <strong>(<em>K</em><sub>0</sub>, <em>K</em><sub>1</sub>, <em>K</em><sub>2</sub>, <em>K</em><sub>3</sub>)</strong>. As shown in the diagram, encryption involves repeated application of a pair of rounds, defined as follows for rounds <em>i</em> and <em>i</em> + 1 (<em>i</em> starts with 1):

<em>L<sub>i</sub> = R<sub>i</sub></em><sub>-1</sub><em>                            R<sub>i</sub></em> = <em>L<sub>i-</sub></em><sub>1</sub> ⽥ F(<em>R<sub>i</sub></em><sub>-1</sub>, <em>K</em><sub>0</sub>, <em>K</em><sub>1</sub>, δ<em><sub>i</sub></em>) <em> </em>

<em>L<sub>i</sub></em><sub>+1</sub> = <em>R<sub>i</sub></em>                             <em>R<sub>i</sub></em><sub>+1</sub> = <em>L<sub>i</sub></em> ⽥ F(<em>R<sub>i</sub></em>, <em>K</em><sub>2</sub>, <em>K</em><sub>3</sub>, δ<em><sub>i</sub></em><sub>+1</sub>) where F is defined as

F(<em>X</em>, <em>K<sub>m</sub></em>, <em>K<sub>n</sub></em>, δ<em><sub>y</sub></em>) = (( <em>X</em> &lt;&lt; 4) ⽥ <em>K<sub>m</sub></em>)  Å ( (<em>X</em> &gt;&gt; 5) ⽥ <em>K<sub>n</sub></em>) Å (<em>X</em> ⽥ δ<em><sub>y</sub></em>)

and where the logical left shift of x by y bits is denoted by x &lt;&lt; y; the logical <strong><sub>R</sub></strong><strong><sub>1 </sub></strong>right shift of x by y bits is denoted by x &gt;&gt; y; δ<em><sub>i</sub></em> (Delta<em><sub>i</sub></em>) is a sequence of predetermined constants; and ⽥ denotes addition-mod-2<sup>32</sup>.

<ol start="2">

 <li>If only one <strong><em>pair</em></strong> of rounds, i.e., rounds 1 and 2, is used, then <strong><em>the ciphertext is the 64- bit block (L<sub>2</sub>, R<sub>2</sub>).</em></strong> You may express the <strong><em>encryption</em></strong> algorithm by representing <em>L</em><sub>2</sub> as a function of <em>L</em><sub>0</sub>, <em>R</em><sub>0</sub>, <em>K</em><sub>0</sub>, <em>K</em><sub>1</sub>, and δ<sub>1</sub>, and representing <em>R</em><sub>2</sub> as a function of <em>L</em><sub>2</sub>, <em>R</em><sub>0</sub>,<em> K</em><sub>2</sub>, <em>K</em><sub>3</sub>, and δ<sub>2</sub>.</li>

</ol>




<ol>

 <li>The <strong><em>decryption</em></strong> algorithm is given as below. You may verify it by reverting the calculation in the <strong><em>block diagram</em></strong>.</li>

</ol>

<em>R</em><sub>0</sub> = <em>R</em><sub>2</sub> ⽈ [[(<em>L</em><sub>2</sub> &lt;&lt; 4) ⽥ <em>K</em><sub>2</sub>] Å [<em>L</em><sub>2</sub> ⽥ δ<sub>2</sub>] Å [(<em>L</em><sub>2</sub> &gt;&gt; 5) ⽥ <em>K</em><sub>3</sub>]] <em>L</em><sub>0</sub> = <em>L</em><sub>2</sub> ⽈ [[(<em>R</em><sub>0</sub> &lt;&lt; 4) ⽥ <em>K</em><sub>0</sub>] Å [<em>R</em><sub>0</sub> ⽥ δ<sub>1</sub>] Å [(<em>R</em><sub>0</sub> &gt;&gt; 5) ⽥ <em>K</em><sub>1</sub>]] where  ⽈ denotes subtraction-mod-2<sup>32</sup>.

<strong> </strong>

<strong>Program TEA_Encryption</strong>: Write a Java program to implement TEA <strong><em>Encryption</em></strong> including only one <em>pair</em> of rounds: rounds 1 and 2 •   Data and inputs:  o           declare a constant <strong><em>int</em></strong> DeltaOne with a hex value of 0x11111111 o       declare a constant <strong><em>int</em></strong> DeltaTwo with a hex value of 0x22222222

o    declare an <strong><em>int </em></strong>array with 4 elements: K[0], K[1], K[2], and K[3], get their values via user inputs in Hex strings

For each element K[<em>i</em>], where <em>i</em> = 0, 1, 2, or 3, display the following prompt message, read the user input as a String, and then convert the user input String into an integer by treating it as a Hex value, and assign this integer to K[<em>i</em>]. E.g., if the user input is “F3579BD1” for K[0], then K[0] = 0xF3579BD1.

<strong>Please input K[i] in Hex String (without “0x”):</strong> o declare two <strong><em>int</em></strong> arrays L[ ] and R[ ], each having a size of <strong>3</strong>.

MSU Denver, M&amp;CS                                           CS 3750: Computer and Network Security, Fall 2019                                              Dr. Weiying Zhu

For each of <strong>L[0]</strong> and <strong>R[0]</strong>, display a prompt message like the following one for L[0], read the user input as a String, and then convert the user input String into an integer by treating it as a Hex value, and assign this integer to L[0] or R[0]. E.g., if the user input is “2468ACE0” for L[0], then L[0] = 0x2468ACE0.

<strong>Please input L[0] in Hex String (without “0x”):</strong>

Initialize <strong>L[1]</strong>, <strong>L[2]</strong>, <strong>R[1]</strong>, and <strong>R[2]</strong> as 0x00000000’s.

<ul>

 <li>The program and outputs: o Implement the <strong>encryption</strong> algorithm to calculate L[1] and R[1] first, and then L[2] and R[2]

  <ul>

   <li>Display the hex values of L[<em>i</em>] and R[<em>i</em>], where <em>i</em> = 0, 1, and 2, in Hex strings. E.g., assuming L[0] = 0x2468ACE0,</li>

  </ul></li>

</ul>

<strong>L[0] = 2468ACE0      R[0] = …… L[1] = ……            R[1] = …… </strong>

<strong>L[2] = ……            R[2] = ……</strong>




<strong>Program TEA_Decryption</strong>: Write a Java program to implement TEA <strong><em>Decryption</em></strong> including only one <em>pair</em> of rounds: rounds 1 and 2 •   Data and inputs:  o           declare a constant <strong><em>int</em></strong> DeltaOne with a hex value of 0x11111111 o       declare a constant <strong><em>int</em></strong> DeltaTwo with a hex value of 0x22222222

<ul>

 <li>declare an <strong><em>int </em></strong>array with 4 elements: K[0], K[1], K[2], and K[3], get their values via user inputs in Hex strings</li>

</ul>

For each element K[<em>i</em>], where <em>i</em> = 0, 1, 2, or 3, display the following prompt message, read the user input as a String, and then convert the user input String into an integer by treating it as a Hex value, and assign this integer to K[<em>i</em>]. E.g., if the user input is “F3579BD1” for K[0], then K[0] = 0xF3579BD1.

<strong>Please input K[i] in Hex String (without “0x”):</strong> o declare two <strong><em>int</em></strong> arrays L[ ] and R[ ], each having a size of <strong>3</strong>.

For each of <strong>L[2]</strong> and <strong>R[2]</strong>, display a prompt message like the following one for L[2], read the user input as a String, and then convert the user input String into an integer by treating it as a Hex value, and assign this integer to L[2] or R[2]. E.g., if the user input is “2468ACE0” for L[2], then L[2] = 0x2468ACE0.

<strong>Please input L[2] in Hex String (without “0x”):</strong>

Initialize <strong>L[0]</strong>, <strong>L[1]</strong>, <strong>R[0]</strong>, and <strong>R[1]</strong> as 0x00000000’s.

<ul>

 <li>The program and outputs: o Implement the <strong>decryption</strong> algorithm to calculate L[1] and R[1] first, and then L[0] and R[0]

  <ul>

   <li>Display the hex values of L[<em>i</em>] and R[<em>i</em>], where <em>i</em> = 2, 1, and 0, in Hex strings. E.g., assuming L[2] = 0x2468ACE0,</li>

  </ul></li>

</ul>

<strong>L[2] = 2468ACE0      R[2] = …… L[1] = ……            R[1] = …… L[0] = ……            R[0] = ……</strong>




<strong>Task II (10%)</strong>:<strong> Test your program on the virtual server.  </strong>

<table width="63">

 <tbody>

  <tr>

   <td width="63">  <strong>Warning</strong>:</td>

  </tr>

 </tbody>

</table>

to complete this part, especially when you work at home, you must first (1) <strong>connect to the MSUDenver VPN</strong> using

your student VPN account (please read “<strong>how to set up VPN for … for students</strong>” at <u>https://msudenver.edu/vpn/</u>); then (2) <strong>connect to the virtual server cs3750a.msudenver.edu</strong> using <strong><em>sftp</em></strong> and <strong><em>ssh</em></strong> command on MAC/Linux or <strong><em>PUTTY</em></strong> and <strong><em>PSFTP</em></strong> on Windows.  For details, you may refer to <strong>Lab 1, Part I. </strong>

<ol>

 <li>MAKE a directory “<strong>HW02</strong>” under your home directory on <strong>msdenver.edu</strong>.</li>

 <li>UPLOAD, COMPILE, and TEST your both programs under “<strong>HW02</strong>” on <strong>msdenver.edu</strong>.</li>

 <li>SAVE two <strong><em>files named</em></strong> “<strong><em>txt” and “tst_Decryption.txt”</em></strong> under “<strong>HW02</strong>” on <strong>cs3750a.msudenver.edu</strong>, which captures the outputs of your programs as a proof that you have tested both programs on cs3750a. You can use the following commands to redirect the standard output (stdout) to a <strong>file</strong> on UNIX, Linux, or Mac, and view the contents of the file</li>

</ol>

<strong>javac prog_name.java    //compile .java file into byte code into .class file java prog_name_args | tee tst_Encryption.txt  //copy stdout to the given .txt file cat file-name      //display the file’s contents.</strong>

<ol start="4">

 <li>If you work in a team of two students, you must put a <strong><em>txt</em></strong> file including both team members’ names under your HW2/ on cs3750a (both team members are required to complete Task II under their own home directories on cs3750a). For grading, I will randomly pick the submission in one of the two <em>home directories</em> of the team members on cs3750a, and then give both team members the same grade.</li>

</ol>


