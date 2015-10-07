<h1 id="links-hard-and-soft">Links: Hard and Soft</h1>



<h2 id="linux-file-types">Linux File Types</h2>

<p>There are seven basic types of file types in Linux.</p>

<p></p><br><br><br><br><br><br><br><br><br><table border="1" cellpadding="3" cellspacing="3"> 
  <tbody><tr><th>Symbol</th><th>File Type</th> 
  </tr><tr><td>-</td><td>Regular Files</td></tr> 
  <tr><td>d</td><td>Directories</td></tr> 
  <tr><td>l</td><td>Symbolic Links</td></tr> 
  <tr><td>c</td><td>Character Device Files</td></tr> 
  <tr><td>b</td><td>Block Device Files</td></tr> 
  <tr><td>s</td><td>Local Domain Sockets</td></tr> 
  <tr><td>p</td><td>Named Pipes</td></tr> 
  </tbody></table><p></p>

<p>The <code>ls</code> command is used to show information about a file.</p>

<pre><code>$ ls -l cpuhog.sh
-rwxrwxr-x 1 dennisk dennisk 401 Feb 13 2012 cpuhog.sh
</code></pre>

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

<pre><code>$ ls -il cpuhog.sh
16914416 -rwxrwxr-x 1 dennisk dennisk 401 Feb 13 2012 cpuhog.sh
</code></pre>

<p>As long as there is at least one pointer to the inode of a file the file still exist. When the pointer counter is zero the data is still there but the file is not accessible.</p>

<p>The inode of the symbolic link is different from the file it points to. If the original file is deleted the link is broken.</p>

<pre><code>$ ls -il /media/Debian/README.txt
1355 -r--r--r-- 1 dennisk dennisk 5512 Jun 15 16:06 /media/Debian/README.txt
</code></pre>



<h1 id="the-ln-command">The <code>ln</code> command</h1>

<p>Files with multiple pointers have multiple hard links to the same data.</p>

<p>The <code>ln</code> or link command creates multiple pointer to the data.</p>

<pre><code>$ ls -il cpuhog.sh
16914416 -rwxrwxr-x 1 dennisk dennisk 401 Feb 13 2012 cpuhog.sh

$ ln cpuhog.sh cpuhog

$ ls -il cpuhog*
16914416 -rwxrwxr-x 2 dennisk dennisk 401 Feb 13  2012 cpuhog
16914416 -rwxrwxr-x 2 dennisk dennisk 401 Feb 13  2012 cpuhog.sh
</code></pre>



<h2 id="symbolic-links">Symbolic Links</h2>

<p><img src="https://s3.amazonaws.com/CIS126DL/Images/link-soft.png" alt="Diagram showing soft file link" title="soft link"></p>

<p>Symbolic or Soft links can span file systems and can link to directories.</p>

<pre><code>$ ln -s /media/Debian/README.txt /home/dennisk
$ ls -il README.txt
16914528 lrwxrwxrwx 1 dennisk dennisk 38 Oct  2 13:53 README.txt -&gt; /media/Debian 7.1.0 amd64 1/README.txt
</code></pre>



<h2 id="hard-links">Hard Links</h2>

<p><img src="https://s3.amazonaws.com/CIS126DL/Images/link-hard.png" alt="Diagram showing hard file link" title="hard link"></p>

<p>Either file name can be deleted and the data will still be accessible.</p>

<pre><code>$ ls -il cpuhog*
16914416 -rwxrwxr-x 2 dennisk dennisk 401 Feb 13 2012 cpuhog
16914416 -rwxrwxr-x 2 dennisk dennisk 401 Feb 13 2012 cpuhog.sh

$ rm cpuhog.sh
$ ls -il cpuhog
16914416 -rwxrwxr-x 1 dennisk dennisk 401 Feb 13 2012 cpuhog
</code></pre>



<h3 id="hard-links-limitations">Hard Links Limitations</h3>

<p>Hard links can not be made across file systems or to directories.</p>

<pre><code>$ ln /media/Debian/README.txt /home/dennisk
ln: failed to create hard link 
./README.txt =&gt; /media/Debian/README.txt: Invalid cross-device link

$ ls -il /media/Debian/README.txt
1355 -r--r--r-- 1 dennisk dennisk 5512 Jun 15 16:06 /media/Debian/README.txt
</code></pre>

<p>### Hard Links and Backups</p>

<p>The files in blue are unchanged so a hard link in used to save disk space.</p>

<p><img src="https://s3.amazonaws.com/CIS126DL/Images/link-backup.png" alt="Diagram showing hard file link used for backups" title="Using hard links for backup"></p>



<h1 id="resources">Resources</h1>

<ul>
<li><p><a href="http://www.ibm.com/developerworks/aix/library/au-speakingunix14/" title="Speaking UNIX: It is all about the inode">Speaking UNIX: It is all about the inode</a></p></li>
<li><p><a href="http://www.linux-mag.com/id/8658/" title="What is an inode?">What’s an inode?</a></p></li>
</ul>

<!-- Links -->

<blockquote>
  <p>Written with <a href="https://stackedit.io/">StackEdit</a>.</p>
</blockquote>