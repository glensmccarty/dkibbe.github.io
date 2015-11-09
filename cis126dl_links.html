<h1 id="links-hard-and-soft">Links: Hard and Soft</h1>



<h2 id="linux-file-types">Linux File Types</h2>

<p>There are seven basic types of file types in Linux.</p>

<table>
<thead>
<tr>
  <th>Symbol</th>
  <th>File Type</th>
</tr>
</thead>
<tbody><tr>
  <td>– (dash)</td>
  <td>Ordinaly file</td>
</tr>
<tr>
  <td>d</td>
  <td>Directory</td>
</tr>
<tr>
  <td>l</td>
  <td>Symbolic Link</td>
</tr>
<tr>
  <td>c</td>
  <td>Character Device</td>
</tr>
<tr>
  <td>b</td>
  <td>Block device</td>
</tr>
<tr>
  <td>s</td>
  <td>Local socket</td>
</tr>
<tr>
  <td>p</td>
  <td>Named pipe</td>
</tr>
</tbody></table>


<p>The <code>ls</code> command is used to show information about a file.</p>

<pre class="prettyprint"><code class=" hljs lasso">$ touch foo
$ ls <span class="hljs-attribute">-l</span> foo
<span class="hljs-attribute">-rwxrwxr</span><span class="hljs-attribute">-x</span> <span class="hljs-number">1</span> ubuntu ubuntu <span class="hljs-number">0</span> Feb <span class="hljs-number">13</span> <span class="hljs-number">2012</span> foo</code></pre>

<p>The listing shows:</p>

<ul>
<li>File type (-, d-, l, etc.)</li>
<li>User, Group, Other permissions</li>
<li>User ID and Group ID</li>
<li>Link counter</li>
<li>Size in bytes</li>
<li>Date last modified</li>
<li>File name</li>
</ul>

<h1 id="inode">Inode</h1>

<p>An inode points to where the data is on disk.</p>



<pre class="prettyprint"><code class=" hljs lasso">$ ls <span class="hljs-attribute">-il</span> foo
<span class="hljs-number">16914416</span> <span class="hljs-attribute">-rwxrwxr</span><span class="hljs-attribute">-x</span> <span class="hljs-number">1</span> ubuntu ubuntu <span class="hljs-number">0</span> Feb <span class="hljs-number">13</span> <span class="hljs-number">2012</span> foo</code></pre>

<p>As long as there is at least one pointer to the inode of a file the file still exist. When the pointer counter is zero the data is still there but the file is not accessible.</p>

<p>The inode of the symbolic link is different from the file it points to. If the original file is deleted the link is broken.</p>

<pre class="prettyprint"><code class=" hljs brainfuck"><span class="hljs-comment">$</span> <span class="hljs-comment">ls</span> <span class="hljs-literal">-</span><span class="hljs-comment">il</span> <span class="hljs-comment">/media/Debian/README</span><span class="hljs-string">.</span><span class="hljs-comment">txt</span>
<span class="hljs-comment">1355</span> <span class="hljs-literal">-</span><span class="hljs-comment">r</span><span class="hljs-literal">-</span><span class="hljs-literal">-</span><span class="hljs-comment">r</span><span class="hljs-literal">-</span><span class="hljs-literal">-</span><span class="hljs-comment">r</span><span class="hljs-literal">-</span><span class="hljs-literal">-</span> <span class="hljs-comment">1</span> <span class="hljs-comment">dennisk</span> <span class="hljs-comment">dennisk</span> <span class="hljs-comment">5512</span> <span class="hljs-comment">Jun</span> <span class="hljs-comment">15</span> <span class="hljs-comment">16:06</span> <span class="hljs-comment">/media/Debian/README</span><span class="hljs-string">.</span><span class="hljs-comment">txt</span></code></pre>

<h1 id="the-ln-command">The <code>ln</code> command</h1>

<p>Files with multiple pointers have multiple hard links to the same data.</p>

<p>The <code>ln</code> or link command creates multiple pointer to the data.</p>

<pre class="prettyprint"><code class=" hljs lasso">$ ls <span class="hljs-attribute">-il</span> foo
<span class="hljs-number">16914416</span> <span class="hljs-attribute">-rwxrwxr</span><span class="hljs-attribute">-x</span> <span class="hljs-number">1</span> ubuntu ubuntu <span class="hljs-number">0</span> Feb <span class="hljs-number">13</span> <span class="hljs-number">2012</span> foo

$ ln foo cpuhog

$ ls <span class="hljs-attribute">-il</span> cpuhog<span class="hljs-subst">*</span>
<span class="hljs-number">16914416</span> <span class="hljs-attribute">-rwxrwxr</span><span class="hljs-attribute">-x</span> <span class="hljs-number">2</span> ubuntu ubuntu <span class="hljs-number">0</span> Feb <span class="hljs-number">13</span>  <span class="hljs-number">2012</span> cpuhog
<span class="hljs-number">16914416</span> <span class="hljs-attribute">-rwxrwxr</span><span class="hljs-attribute">-x</span> <span class="hljs-number">2</span> ubuntu ubuntu <span class="hljs-number">0</span> Feb <span class="hljs-number">13</span>  <span class="hljs-number">2012</span> foo</code></pre>

<h2 id="symbolic-links">Symbolic Links</h2>

<p><img src="https://s3.amazonaws.com/CIS126DL/Images/link-soft.png" alt="Diagram showing soft file link" title="soft link"></p>

<p>Symbolic or Soft links can span file systems and can link to directories.</p>

<pre class="prettyprint"><code class=" hljs avrasm">$ ln -s /media/Debian/README<span class="hljs-preprocessor">.txt</span> /home/dennisk
$ ls -il README<span class="hljs-preprocessor">.txt</span>
<span class="hljs-number">16914528</span> lrwxrwxrwx <span class="hljs-number">1</span> dennisk dennisk <span class="hljs-number">38</span> Oct  <span class="hljs-number">2</span> <span class="hljs-number">13</span>:<span class="hljs-number">53</span> README<span class="hljs-preprocessor">.txt</span> -&gt; /media/Debian <span class="hljs-number">7.1</span><span class="hljs-number">.0</span> amd64 <span class="hljs-number">1</span>/README<span class="hljs-preprocessor">.txt</span></code></pre>

<h2 id="hard-links">Hard Links</h2>

<p><img src="https://s3.amazonaws.com/CIS126DL/Images/link-hard.png" alt="Diagram showing hard file link" title="hard link"></p>

<p>Either file name can be deleted and the data will still be accessible.</p>

<pre class="prettyprint"><code class=" hljs lasso">$ ls <span class="hljs-attribute">-il</span> cpuhog<span class="hljs-subst">*</span>
<span class="hljs-number">16914416</span> <span class="hljs-attribute">-rwxrwxr</span><span class="hljs-attribute">-x</span> <span class="hljs-number">2</span> ubuntu ubuntu <span class="hljs-number">401</span> Feb <span class="hljs-number">13</span> <span class="hljs-number">2012</span> cpuhog
<span class="hljs-number">16914416</span> <span class="hljs-attribute">-rwxrwxr</span><span class="hljs-attribute">-x</span> <span class="hljs-number">2</span> ubuntu ubuntu <span class="hljs-number">401</span> Feb <span class="hljs-number">13</span> <span class="hljs-number">2012</span> foo

$ rm foo
$ ls <span class="hljs-attribute">-il</span> cpuhog
<span class="hljs-number">16914416</span> <span class="hljs-attribute">-rwxrwxr</span><span class="hljs-attribute">-x</span> <span class="hljs-number">1</span> ubuntu ubuntu <span class="hljs-number">401</span> Feb <span class="hljs-number">13</span> <span class="hljs-number">2012</span> cpuhog</code></pre>

<h3 id="hard-links-limitations">Hard Links Limitations</h3>

<p>Hard links can not be made across file systems or to directories.</p>

<pre class="prettyprint"><code class=" hljs avrasm">$ ln /media/Debian/README<span class="hljs-preprocessor">.txt</span> /home/dennisk
<span class="hljs-label">ln:</span> failed to create hard link 
./README<span class="hljs-preprocessor">.txt</span> =&gt; /media/Debian/README<span class="hljs-preprocessor">.txt</span>: Invalid cross-device link

$ ls -il /media/Debian/README<span class="hljs-preprocessor">.txt</span>
<span class="hljs-number">1355</span> -r--r--r-- <span class="hljs-number">1</span> dennisk dennisk <span class="hljs-number">5512</span> Jun <span class="hljs-number">15</span> <span class="hljs-number">16</span>:<span class="hljs-number">06</span> /media/Debian/README<span class="hljs-preprocessor">.txt</span></code></pre>



<h3 id="hard-links-and-backups">Hard Links and Backups</h3>

<p>The files in blue are unchanged so a hard link in used to save disk space.</p>

<p><img src="https://s3.amazonaws.com/CIS126DL/Images/link-backup.png" alt="Diagram showing hard file link used for backups" title="Using hard links for backup"></p>



<h2 id="what-to-submit">What to Submit</h2>

<p>Change to the <code>/tmp</code> directory and create a file named <code>foo</code> with the <code>touch</code> command. Link <code>foobar</code> symbolically to <code>foo</code> and link <code>foo2</code> as a hard link to <code>foo</code>. Submit a screenshot of the <code>ls -li foo*</code> command showing that the inodes of <code>foo</code> and <code>foo2</code> are the same and that <code>foobar</code> is linked to <code>foo</code>.</p>

<h1 id="resources">Resources</h1>

<ul>
<li><p><a href="http://www.ibm.com/developerworks/aix/library/au-speakingunix14/" title="Speaking UNIX: It is all about the inode">Speaking UNIX: It is all about the inode</a></p></li>
<li><p><a href="http://www.linux-mag.com/id/8658/" title="What is an inode?">What’s an inode?</a></p></li>
</ul>

<!-- Links -->

<blockquote>
  <p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>