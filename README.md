Download Link: https://assignmentchef.com/product/solved-cop5536-project-huffman-coding
<br>
In computer science and information theory, a Huffman code is a particular type of optimal prefix code that is commonly used for lossless data compression. In this project, you will implement the Huffman encoder and decoder with the following details.

<h1>1.   Huffman Coding</h1>

The first step in this project is to develop a program that generates Huffman codes. The algorithm for this was discussed in Lecture 7. For this project, you need to evaluate which of the following priority queue structures gives best performance: Binary Heap, 4-way cache optimized heap (lecture 10 slides 23 and 24), and Pairing Heap (lecture 15). Write code to generate Huffman trees using these three data structures and then measure run time using input data of <strong><em>sample_input_large.txt</em></strong>. Use the following code as reference (this is in C++, use a similar approach if you are using some other programming language):




<table width="719">

 <tbody>

  <tr>

   <td width="24"> </td>

   <td width="695">clock_t start_time; // binary heap start_time = clock();for(int i = 0; i &lt; 10; i++){                          //run 10 times on given data set          build_tree_using_binary_heap(freq_table);} cout &lt;&lt; “Time using binary heap (microsecond):  ” &lt;&lt; (clock() – start_time)/10 &lt;&lt; endl; // 4-way heap start_time = clock();for(int i = 0; i &lt; 10; i++){                          //run 10 times on given data set          build_tree_using_4way_heap(freq_table);} cout &lt;&lt; “Time using 4-way heap (microsecond):  ” &lt;&lt; (clock() – start_time)/10 &lt;&lt; endl; // pairing heap start_time = clock();for(int i = 0; i &lt; 10; i++){                          //run 10 times on given data set          build_tree_using_pairing_heap(freq_table);}cout &lt;&lt; “Time using pairing heap (microsecond):  ” &lt;&lt; (clock() – start_time)/10 &lt;&lt; endl; </td>

  </tr>

 </tbody>

</table>




Once you have determined which data structure gives the best performance, finalize your Huffman code program using that data structure. The finalized Huffman code program will take as input a frequency table and output a code table. Include the timings and conclusions in your report. Once the Huffman code program is finalized, you should proceed to write the encoder and decoder.<strong>  </strong>

<h1>2.   Encoder</h1>

The encoder reads an input file that is to be compressed and generates two output files – the compressed version of the input file and the code table. Your encoder can follow this diagram:




<h2>Input format</h2>

Input file name will be given as a command line argument. This file can have up to 100,000,000 lines and each line will contain an integer in the range of 0 to 999,999. Consider the following input for the rest of the document:

<table width="719">

 <tbody>

  <tr>

   <td colspan="2" width="719">&lt;input_file&gt;</td>

  </tr>

  <tr>

   <td width="25"> </td>

   <td width="695">0224509999992245002245224534446  34446349999992</td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<h2>Building frequency table</h2>

First step towards Huffman encoding is to build the frequency table for each value in input. As values will be within 0 to 999999, an array can be used for storing frequency for each value. Frequency mapping for the given input file is:

0 ==&gt; 4

2245 ==&gt; 4

999999 ==&gt; 2

34 ==&gt; 3

446 ==&gt; 2

2 ==&gt; 1

<h2>Build Huffman tree and code table</h2>

Use the data structure with best timing from section 1 to build the Huffman code table. For the sample input given, one possible Huffman tree and corresponding code table mapping is given below. The code table can be built from the Huffman tree by doing a traversal of the tree.

<table width="414">

 <tbody>

  <tr>

   <td width="247"></td>

   <td width="167">


    <table width="135">

     <tbody>

      <tr>

       <td width="135">2 ==&gt; 000999999 ==&gt; 0010 ==&gt; 012245 ==&gt; 10446 ==&gt; 11034 ==&gt; 111</td>

      </tr>

     </tbody>

    </table></td>

  </tr>

 </tbody>

</table>

<strong><em>Huffman tree                 </em></strong><sup>                                                                                                                                                                     </sup><strong><em>code table  </em></strong>







<h2>Encode data</h2>

Once the code table is built, it can be used to encode the original input file by replacing each input value by its code. Please note that the values are not ASCII characters, rather <strong>binary values</strong>. You can use “ios::binary” flag in C++, or OutputStream in Java.

0110010011001011010111110111110111001000




<h2>Output format</h2>

Encoder program has two output files. One is encoded message in <strong>binary format</strong>. It must be saved as <strong>“encoded.bin”</strong>. As mentioned in <u>Encode Data</u> phase, output encoded.bin for given data will be:

<table width="719">

 <tbody>

  <tr>

   <td colspan="2" width="719"><strong>encoded.bin</strong></td>

  </tr>

  <tr>

   <td width="24"> </td>

   <td width="695">0110010011001011010111110111110111001000</td>

  </tr>

 </tbody>

</table>




Second output is the code table. Each line in this output file will contain value of a leaf node of Huffman tree, and its code separated by a space. It must be saved as <strong>“code_table.txt”</strong>.

<table width="719">

 <tbody>

  <tr>

   <td colspan="2" width="719"><strong>code</strong><strong>_</strong><strong>table.txt</strong></td>

  </tr>

  <tr>

   <td width="25"> </td>

   <td width="695">2 000999999 0010 012245 10446 11034 111</td>

  </tr>

 </tbody>

</table>




<strong><em> </em></strong>

<strong><em><u>Note:</u> Both “encoded.bin” and “code_table.txt” are NOT unique. They will not be used for grading directly. However, the size of “encoded.bin” is unique, so this size will be used for grading purpose. “code_table.txt” will be used by your decoder program to decompress the encoded file. </em></strong>

<h1>3.   Decoder</h1>

The decoder reads two input files – encoded message and code table. The decoder first constructs the decode tree using the code table. Then the decoded message can be generated from the encoded message using the decode tree. <strong>Your report should include a description of the algorithm used to construct the decode tree from the code table together with the complexity of this algorithm. </strong>

<strong> </strong>

<strong> </strong>

<h2>Input format</h2>

The decoder takes two input files – encoded message and code table. File names will be given as command line arguments. The format of these files is the same as the output format of the encoder, so that the output files of the encoder program can be directly used by the decoder program. <strong>Note that the input encoded message will be in binary format, not ASCII characters. You can use ios::binary flag for C++ or InputStream for Java.</strong>

<h2>Output format</h2>

Output of decoder program is the decoded message. It should be saved as <strong>“decoded.txt”</strong>. The format of this file is same as the input format for the encoder. For any sample input, the following scenario should be true:

<strong> </strong>

<table width="719">

 <tbody>

  <tr>

   <td colspan="2" width="133">&lt;input_file&gt;</td>

   <td rowspan="2" width="443">  </td>

   <td colspan="2" width="144"><strong>decoded.txt </strong></td>

  </tr>

  <tr>

   <td width="25"> </td>

   <td width="108">0224509999992245002245224534446  34446349999992</td>

   <td width="29"> </td>

   <td width="114">022450999999224500224522453444634446349999992</td>

  </tr>

  <tr>

   <td width="24"></td>

   <td width="108"></td>

   <td width="445"></td>

   <td width="29"></td>

   <td width="113"></td>

  </tr>

 </tbody>

</table>

<strong> </strong>

<strong>             </strong>

<h1>4.   Files provided in elearning</h1>

<table width="561">

 <tbody>

  <tr>

   <td width="264">  sample1/..i. sample_input_small.txt  ii. encoded.bin  iii.code_table.txt iv.decoded.txt</td>

   <td width="297">;inputs/outputs mentioned in this document</td>

  </tr>

  <tr>

   <td width="264">  sample2/..</td>

   <td width="297">;large inputs/outputs set</td>

  </tr>

  <tr>

   <td width="264"> i. sample_input_large.txt  ii. encoded.bin  iii.code_table.txt iv.decoded.txt</td>

   <td width="297">;use this file for performance measurement</td>

  </tr>

  <tr>

   <td width="264">  COP5536_FA20_Project.pdf</td>

   <td width="297">;this file</td>

  </tr>

 </tbody>

</table>

<h1>5.   Run environment</h1>

Your code must be able to run in the linux environment. You can test your program either on CISE <strong>storm.cise.ufl.edu</strong> or <strong>thunder.cise.ufl.edu</strong> server (for which you need to login using your CISE account).  Write a Makefile so that we can build your code using following command at terminal:

<strong>     $ make </strong>

This command should produce two binary files: <strong>encoder</strong> and <strong>decoder. </strong>

As mentioned before, <strong>encoder</strong> should take one input file. We will run it using following command:

<strong>     $ ./encoder &lt;input_file_name&gt;                             [For C++] </strong>

<strong>     $ java encoder &lt;input_file_name&gt;                          [For Java] </strong>

Running <strong>encoder</strong> program must produce the output files with exact name <strong>“encoded.bin”</strong> and <strong>“code_table.txt”. </strong>On the other hand, <strong>decoder</strong> will take two input files. We will run it using following command:

<strong>$ ./decoder &lt;encoded_file_name&gt; &lt;code_table_file_name&gt;   [For C++]  </strong>

<strong>     $ java decoder &lt;encoded_file_name&gt; &lt;code_table_file_name&gt; [For Java] </strong>

Running <strong>decoder</strong> program must produce output file with exact name <strong>“decoded.txt”. </strong>