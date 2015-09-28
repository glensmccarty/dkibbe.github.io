<script src="https://cdn.rawgit.com/google/code-prettify/master/loader/run_prettify.js?lang=css&amp;skin=sunburst"></script>

<h1 id="here-docs">Here Docs</h1>

<p>Sometimes you need to output some text to the command line to inform the user of a script. a <em>here doc</em> lets you do that easily.</p>



<h2 id="a-basic-here-doc">A Basic here doc</h2>



<pre class="prettyprint"><code class="language-bash">$ cat &lt;&lt; EOF
&gt; This is a basic here doc.
&gt; EOF
This is a basic here doc.</code></pre>

<p>The <strong>EOF</strong> delimiter can be anything that is not likely to appear in the script. EOF (End Of File) is a good choice. You should keep your here docs short.</p>



<h2 id="here-docs-and-functions">Here Docs and Functions</h2>

<p>You can easily wrap a here doc in a function and call the function whenever needed.</p>



<pre class="prettyprint"><code class="language-bash">#!/usr/bin/env bash

usage ()
{
cat &lt;&lt; EOF
No postional parameter given.
EOF
}

right ()
{
cat &lt;&lt; EOF
You did it right.
EOF
}

if
[[ $# -lt 1 ]]
then
usage
else
right
fi</code></pre>



<h2 id="resources">Resources</h2>

<ul>
<li><a href="http://mywiki.wooledge.org/BashGuide/InputAndOutput#Heredocs_And_Herestrings">Greg’s Bash Guide</a></li>
<li><a href="http://www.ibm.com/developerworks/aix/library/au-unixtext/">Introduction to text manipulation on UNIX-based systems</a></li>
</ul>

<blockquote>
  <p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>