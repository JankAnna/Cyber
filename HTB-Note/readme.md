# HackTheBox
## Linux Fundamentals
<div class="training-module">
<h1>Network Services</h1>
<hr>
<p>When we work with Linux, we also have to deal with different network services. The competence to work with these network services is essential for many reasons. Among other things, we need this knowledge and ability to communicate with other computers over the network, connect, transfer files, analyze network traffic, and learn how to configure such services to identify potential vulnerabilities in our later penetration tests. This knowledge also pushes our understanding of network security as we learn what options each service and its configuration entails.</p>
<p>Let's imagine that we are performing a penetration test and come across a Linux host that we are probing for vulnerabilities. Listening to the network, we can see that a user from this Linux host connects to another server via an unencrypted FTP server. Accordingly, we can detect the credentials of the user in clear text. Of course, the likelihood of this scenario occurring would be much lower if the user knew that FTP does not encrypt the connections and the data sent. And as a Linux administrator, this could be a fatal error, as it tells us not only a lot about the security measures on the network but also about the administrator(s) who are responsible for the security of their network.</p>
<p>We will not be able to cover all network services, but we will focus on and cover the most important ones. Because not only from the perspective of an administrator and user, it is of great benefit but also as a penetration tester for the interaction between other hosts and our machine.</p>
<hr>
<h2>SSH</h2>
<p>Secure Shell (<code>SSH</code>) is a network protocol that allows the secure transmission of data and commands over a network. It is widely used to securely manage remote systems and securely access remote systems to execute commands or transfer files. In order to connect to our or a remote Linux host via SSH, a corresponding SSH server must be available and running.</p>
<p>The most commonly used SSH server is the OpenSSH server. OpenSSH is a free and open-source implementation of the Secure Shell (SSH) protocol that allows the secure transmission of data and commands over a network.</p>
<p>Administrators use OpenSSH to securely manage remote systems by establishing an encrypted connection to a remote host. With OpenSSH, administrators can execute commands on remote systems, securely transfer files, and establish a secure remote connection without the transmission of data and commands being intercepted by third parties.</p>
<h4>Install OpenSSH</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install OpenSSH</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> openssh-server -y</span></span>
</code></pre></div></div>
<p>To check if the server is running, we can use the following command:</p>
<h4>Server Status</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Server Status</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">systemctl status <span class="token function">ssh</span></span></span>

<span class="token output">● ssh.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/system/system/ssh.service; enabled; vendor preset: enabled)
     Active: active (running) since Sun 2023-02-12 21:15:27 GMT; 1min 22s ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 7740 (sshd)
      Tasks: 1 (limit: 9458)
     Memory: 2.5M
        CPU: 236ms
     CGroup: /system.slice/ssh.service
             └─7740 sshd: /usr/sbin/sshd -D [listener] 0 of 10-100 startups
</span></code></pre></div></div>
<p>As penetration testers, we use OpenSSH to securely access remote systems when performing a network audit. To do this, we can use the following command:</p>
<h4>SSH - Logging In</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">SSH - Logging In</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">ssh</span> cry0l1t3@10.129.17.122</span></span>

<span class="token output">The authenticity of host '10.129.17.122 (10.129.17.122)' can't be established.
ECDSA key fingerprint is SHA256:bKzhv+n2pYqr2r...Egf8LfqaHNxk.

Are you sure you want to continue connecting (yes/no/[fingerprint])? yes

Warning: Permanently added '10.129.17.122' (ECDSA) to the list of known hosts.

cry0l1t3@10.129.17.122's password: ***********
</span></code></pre></div></div>
<p>OpenSSH can be configured and customized by editing the file <code>/etc/ssh/sshd_config</code> with a text editor. Here we can adjust settings such as the maximum number of concurrent connections, the use of passwords or keys for logins, host key checking, and more. However, it is important for us to note that changes to the OpenSSH configuration file must be done carefully.</p>
<p>For example, we can use SSH to securely log in to a remote system and execute commands or use tunneling and port forwarding to tunnel data over an encrypted connection to verify network settings and other system settings without the possibility of third parties intercepting the transmission of data and commands.</p>
<hr>
<h2>NFS</h2>
<p>Network File System (<code>NFS</code>) is a network protocol that allows us to store and manage files on remote systems as if they were stored on the local system. It enables easy and efficient management of files across networks. For example, administrators use NFS to store and manage files centrally (for Linux and Windows systems) to enable easy collaboration and management of data. For Linux, there are several NFS servers, including NFS-UTILS (<code>Ubuntu</code>), NFS-Ganesha (<code>Solaris</code>), and OpenNFS (<code>Redhat Linux</code>).</p>
<p>It can also be used to share and manage resources efficiently, e.g., to replicate file systems between servers. It also offers features such as access controls, real-time file transfer, and support for multiple users accessing data simultaneously. We can use this service just like FTP in case there is no FTP client installed on the target system, or NFS is running instead of FTP.</p>
<p>We can install NFS on Linux with the following command:</p>
<h4>Install NFS</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install NFS</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> nfs-kernel-server -y</span></span>
</code></pre></div></div>
<p>To check if the server is running, we can use the following command:</p>
<h4>Server Status</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Server Status</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">systemctl status nfs-kernel-server</span></span>

<span class="token output">● nfs-server.service - NFS server and services
     Loaded: loaded (/lib/system/system/nfs-server.service; enabled; vendor preset: enabled)
     Active: active (exited) since Sun 2023-02-12 21:35:17 GMT; 13s ago
    Process: 9234 ExecStartPre=/usr/sbin/exportfs -r (code=exited, status=0/SUCCESS)
</span><span class="token info punctuation">    Process<span class="token punctuation">:</span><span class="token path"> 9235 ExecStart=/usr/sbin/rpc.nfsd </span></span><span class="token command"><span class="token shell-symbol important">$</span><span class="token bash language-bash">RPCNFSDARGS <span class="token punctuation">(</span>code<span class="token operator">=</span>exited, <span class="token assign-left variable">status</span><span class="token operator">=</span><span class="token number">0</span>/SUCCESS<span class="token punctuation">)</span></span></span>
<span class="token output">   Main PID: 9235 (code=exited, status=0/SUCCESS)
        CPU: 10ms
</span></code></pre></div></div>
<p>We can configure NFS via the configuration file <code>/etc/exports</code>. This file specifies which directories should be shared and the access rights for users and systems. It is also possible to configure settings such as the transfer speed and the use of encryption. NFS access rights determine which users and systems can access the shared directories and what actions they can perform. Here are some important access rights that can be configured in NFS:</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th><strong>Permissions</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>rw</code></td>
<td>Gives users and systems read and write permissions to the shared directory.</td>
</tr>
<tr>
<td><code>ro</code></td>
<td>Gives users and systems read-only access to the shared directory.</td>
</tr>
<tr>
<td><code>no_root_squash</code></td>
<td>Prevents the root user on the client from being restricted to the rights of a normal user.</td>
</tr>
<tr>
<td><code>root_squash</code></td>
<td>Restricts the rights of the root user on the client to the rights of a normal user.</td>
</tr>
<tr>
<td><code>sync</code></td>
<td>Synchronizes the transfer of data to ensure that changes are only transferred after they have been saved on the file system.</td>
</tr>
<tr>
<td><code>async</code></td>
<td>Transfers data asynchronously, which makes the transfer faster, but may cause inconsistencies in the file system if changes have not been fully committed.</td>
</tr>
</tbody>
</table></div>
<p>For example, we can create a new folder and share it temporarily in NFS. We would do this as follows:</p>
<h4>Create NFS Share</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Create NFS Share</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">mkdir</span> nfs_sharing</span></span>
<span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token builtin class-name">echo</span> <span class="token string">'/home/cry0l1t3/nfs_sharing hostname(rw,sync,no_root_squash)'</span> <span class="token operator">&gt;&gt;</span> /etc/exports</span></span>
<span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">cat</span> /etc/exports <span class="token operator">|</span> <span class="token function">grep</span> -v <span class="token string">"#"</span></span></span>

<span class="token output">/home/cry0l1t3/nfs_sharing hostname(rw,sync,no_root_squash)
</span></code></pre></div></div>
<p>If we have created an NFS share and want to work with it on the target system, we have to mount it first. We can do this with the following command:</p>
<h4>Mount NFS Share</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Mount NFS Share</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">mkdir</span> ~/target_nfs</span></span>
<span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">mount</span> <span class="token number">10.129</span>.12.17:/home/john/dev_scripts ~/target_nfs</span></span>
<span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">tree ~/target_nfs</span></span>

<span class="token output">target_nfs/
├── css.css
├── html.html
├── javascript.js
├── php.php
└── xml.xml

0 directories, 5 files
</span></code></pre></div></div>
<p>So we have mounted the NFS share (<code>dev_scripts</code>) from our target (<code>10.129.12.17</code>) locally to our system in the mount point <code>target_nfs</code> over the network and can view the contents just as if we were on the target system. There are even some methods that can be used in specific cases to escalate our privileges on the remote system using NFS.</p>
<hr>
<h2>Web Server</h2>
<p>As penetration testers, we need to understand how web servers work because they are a critical part of web applications and often serve as targets for us to attack. A web server is a type of software that provides data and documents or other applications and functions over the Internet. They use the Hypertext Transfer Protocol (HTTP) to send data to clients such as web browsers and receive requests from those clients. These are then rendered in the form of Hypertext Markup Language (HTML) in the client's browser. This type of communication allows the client to create dynamic web pages that respond to the client's requests. Therefore, it is important that we understand the various functions of the web server in order to create secure and efficient web applications and also ensure the security of the system. Some of the most popular web servers for Linux servers are Apache, Nginx, Lighttpd, and Caddy. Apache is one of the most popular and widely used web servers and is available on a variety of operating systems, including Ubuntu, Solaris, and Redhat Linux.</p>
<p>As penetration testers, we can use web servers for a variety of purposes. For example, we can use a web server to perform file transfers, allowing us to log in and interact with a target system through an incoming HTTP or HTTPS port. Finally, we can use a web server to perform phishing attacks by hosting a copy of the target page on our own server and then attempting to steal user credentials. In addition, there is a variety of other possibilities.</p>
<p>Apache web server has a variety of features that allow us to host a secure and efficient web application. Moreover, we can also configure logging to get information about the traffic on our server, which helps us analyze attacks. We can install Apache using the following command:</p>
<h4>Install Apache Web Server</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install Apache Web Server</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> apache2 -y</span></span>
</code></pre></div></div>
<p>For Apache2, to specify which folders can be accessed, we can edit the file <code>/etc/apache2/apache2.conf</code> with a text editor. This file contains the global settings. We can change the settings to specify which directories can be accessed and what actions can be performed on those directories.</p>
<h4>Apache Configuration</h4>
<div class="window_container"><div class="window_content"><div class="window_top">Code: <span class="text-success">txt</span></div><pre class=" language-txt"><code class=" language-txt">&lt;Directory /var/www/html&gt;
        Options Indexes FollowSymLinks
        AllowOverride All
        Require all granted
&lt;/directory&gt;
</code></pre></div></div>
<p>This section specifies that the default <code>/var/www/html</code> folder is accessible, that users can use the <code>Indexes</code> and <code>FollowSymLinks</code> options, that changes to files in this directory can be overridden with <code>AllowOverride All</code>, and that <code>Require all granted</code> grants all users access to this directory. For example, if we want to transfer files to one of our target systems using a web server, we can put the appropriate files in the <code>/var/www/html</code> folder and use <code>wget</code> or <code>curl</code> or other applications to download these files on the target system.</p>
<p>It is also possible to customize individual settings at the directory level by using the <code>.htaccess</code> file, which we can create in the directory in question. This file allows us to configure certain directory-level settings, such as access controls, without having to customize the Apache configuration file. We can also add modules to get features like <code>mod_rewrite</code>, <code>mod_security</code>, and <code>mod_ssl</code> that help us improve the security of our web application.</p>
<p>Python Web Server is a simple, fast alternative to Apache and can be used to host a single folder with a single command to transfer files to another system. To install Python Web Server, we need to install Python3 on our system and then run the following command:</p>
<h4>Install Python &amp; Web Server</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install Python &amp; Web Server</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> python3 -y</span></span>
<span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">python3 -m http.server</span></span>
</code></pre></div></div>
<p>When we run this command, our Python Web Server will be started on the <code>TCP/8000</code> port, and we can access the folder we are currently in. We can also host another folder with the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install Python &amp; Web Server</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">python3 -m http.server --directory /home/cry0l1t3/target_files</span></span>
</code></pre></div></div>
<p>This will start a Python web server on the <code>TCP/8000</code> port, and we can access the <code>/home/cry0l1t3/target_files</code> folder from the browser, for example. When we access our Python web server, we can transfer files to the other system by typing the link in our browser and downloading the files. We can also host our Python web server on a port other than the default port by using the <code>-p</code> option:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install Python &amp; Web Server</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">python3 -m http.server <span class="token number">443</span></span></span>
</code></pre></div></div>
<p>This will host our Python web server on port 443 instead of the default <code>TCP/8000</code> port. We can access this web server by typing the link in our browser.</p>
<hr>
<h2>VPN</h2>
<p>Virtual Private Network (<code>VPN</code>) is a technology that allows us to connect securely to another network as if we were directly in it. This is done by creating an encrypted tunnel connection between the client and the server, which means that all data transmitted over this connection is encrypted.</p>
<p>VPNs are mainly used by companies to provide their employees with secure access to the internal network without having to be physically located at the corporate network. This allows employees to access the internal network and its resources and applications from any location. In addition, VPNs can also be used to anonymize traffic and prevent outside access.</p>
<p>Some of the most popular VPN servers for Linux servers are OpenVPN, L2TP/IPsec, PPTP, SSTP, and SoftEther. OpenVPN is a popular open-source VPN server available for various operating systems, including Ubuntu, Solaris, and Redhat Linux. OpenVPN is used by administrators for various purposes, including enabling secure remote access to the corporate network, encrypting network traffic, and anonymizing traffic.</p>
<p>OpenVPN can also be used by us as a penetration tester to connect to internal networks. It can happen that a VPN access is created by the customer so that we can test the internal network for security vulnerabilities. This is an alternative for cases when the penetration tester is too far away from the customer. OpenVPN provides us with a variety of features, including encryption, tunneling, traffic shaping, network routing, and the ability to adapt to dynamically changing networks. We can install the server and client with the following command:</p>
<h4>Install OpenVPN</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install OpenVPN</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> openvpn -y</span></span>
</code></pre></div></div>
<p>OpenVPN can be customized and configured by editing the configuration file <code>/etc/openvpn/server.conf</code>. This file contains the settings for the OpenVPN server. We can change the settings to configure certain features such as encryption, tunneling, traffic shaping, etc.</p>
<p>If we want to connect to an OpenVPN server, we can use the <code>.ovpn</code> file we received from the server and save it on our system. We can do this with the following command on the command line:</p>
<h4>Connect to VPN</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Connect to VPN</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> openvpn --config internal.ovpn</span></span>
</code></pre></div></div>
<p>After the connection is established, we can communicate with the internal hosts on the internal network.</p>
<div id="screen" style="height: 600px; border: 1px solid;">
<div class="screenPlaceholder" style="display: none;">
<div class="instanceLoading" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Instance is starting...</div>
</div>
<div class="instanceTerminating" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Terminating instance...</div>
</div>
<div class="row instanceStart max-width-canvas" style="display: none;">
<div class="col-4"></div>
<div class="col-4">
<button class="startInstanceBtn btn btn-primary btn-lg btn-block " style="margin-top: 270px;">Start Instance
</button>
<p class="text-center mt-2 font-size-13 font-secondary">
<span class="text-success spawnsLeft">
0
</span> / 1 spawns left
</p>
</div>
<div class="col-4"></div>
</div>
</div>
<div style="display: flex; width: 100%; height: 100%; overflow: auto; background: rgb(40, 40, 40);"><canvas width="388" height="598" tabindex="-1" style="margin: auto; outline: none; flex-shrink: 0; cursor: none; width: 388px; height: 598px;"></canvas></div></div>
<div class="row align-center justify-center my-4">
<div class="col-5 justify-start">
<button style="" target="_blank" class="instance-button fullScreenBtn btn btn-light btn-sm float-left "><i class="fad fa-expand text-success mr-1"></i> &nbsp;Full Screen
</button>
<button style="" class="instance-button terminateInstanceBtn btn btn-light btn-sm ml-2"><i class="fad fa-times text-danger"></i> &nbsp;Terminate
</button>
<button style="" class="instance-button resetInstanceBtn btn btn-light btn-sm ml-1"><i class="fad fa-sync text-warning mr-2"></i> &nbsp;Reset
</button>
<div class="btn-group " role="group">
<button style="cursor: default;" class="instance-button extendInstanceBtn btn btn-light btn-sm ml-1">Life Left:
<span class="lifeLeft">110</span>m
</button>
</div>
</div>
<div id="statusText" class="col-7 justify-end pt-2 pr-2 font-size-small text-right">Connected to htb-ogtp8tnbcu.htb-cloud.com:1 (htb-ac-261147)</div>
</div>
</div>

<div class="training-module">
<h1>Backup and Restore</h1>
<hr>
<p>Linux systems offer a variety of software tools for backing up and restoring data. These tools are designed to be efficient and secure, ensuring that data is protected while also allowing us to easily access the data we need.</p>
<p>When backing up data on an Ubuntu system, we can utilize tools such as:</p>
<ul>
<li>Rsync</li>
<li>Deja Dup</li>
<li>Duplicity</li>
</ul>
<p>Rsync is an open-source tool that allows us to quickly and securely back up files and folders to a remote location. It is particularly useful for transferring large amounts of data over the network, as it only transmits the changed parts of a file. It can also be used to create backups locally or on remote servers. If we need to back up large amounts of data over the network, Rsync might be the better option.</p>
<p>Duplicity is another graphical backup tool for Ubuntu that provides users with comprehensive data protection and secure backups. It also uses Rsync as a backend and additionally offers the possibility to encrypt backup copies and store them on remote storage media, such as FTP servers, or cloud storage services, such as Amazon S3.</p>
<p>Deja Dup is a graphical backup tool for Ubuntu that simplifies the backup process, allowing us to quickly and easily back up our data. It provides a user-friendly interface to create backup copies of data on local or remote storage media. It uses Rsync as a backend and also supports data encryption.</p>
<p>In order to ensure the security and integrity of backups, we should take steps to encrypt their backups. Encrypting backups ensures that sensitive data is protected from unauthorized access. Alternatively, we can encrypt backups on Ubuntu systems by utilizing tools such as GnuPG, eCryptfs, and LUKS.</p>
<p>Backing up and restoring data on Ubuntu systems is an essential part of data protection. By utilizing the tools discussed, we can ensure that our data is securely backed up and can be easily restored when needed.</p>
<p>In order to install Rsync on Ubuntu, we can use the <code>apt</code> package manager:</p>
<h4>Install Rsync</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install Rsync</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> <span class="token function">rsync</span> -y</span></span>
</code></pre></div></div>
<p>This will install the latest version of Rsync on the system. Once the installation is complete, we can begin using the tool to back up and restore data. To backup an entire directory using <code>rsync</code>, we can use the following command:</p>
<h4>Rsync - Backup a local Directory to our Backup-Server</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Rsync - Backup a local Directory to our Backup-Server</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">rsync</span> -av /path/to/mydirectory user@backup_server:/path/to/backup/directory</span></span>
</code></pre></div></div>
<p>This command will copy the entire directory (<code>/path/to/mydirectory</code>) to a remote host (<code>backup_server</code>), to the directory <code>/path/to/backup/directory</code>. The option <code>archive</code> (<code>-a</code>) is used to preserve the original file attributes, such as permissions, timestamps, etc., and using the <code>verbose</code> (<code>-v</code>) option provides a detailed output of the progress of the <code>rsync</code> operation.</p>
<p>We can also add additional options to customize the backup process, such as using compression and incremental backups. We can do this like the following:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Rsync - Backup a local Directory to our Backup-Server</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">rsync</span> -avz --backup --backup-dir<span class="token operator">=</span>/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory</span></span>
</code></pre></div></div>
<p>With this, we back up the <code>mydirectory</code> to the remote <code>backup_server</code>, preserving the original file attributes, timestamps, and permissions, and enabled compression (<code>-z</code>) for faster transfers. The <code>--backup</code> option creates incremental backups in the directory <code>/path/to/backup/folder</code>, and the <code>--delete</code> option removes files from the remote host that is no longer present in the source directory.</p>
<p>If we want to restore our directory from our backup server to our local directory, we can use the following command:</p>
<h4>Rsync - Restore our Backup</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Rsync - Restore our Backup</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">rsync</span> -av user@remote_host:/path/to/backup/directory /path/to/mydirectory</span></span>
</code></pre></div></div>
<hr>
<h2>Encrypted Rsync</h2>
<p>To ensure the security of our <code>rsync</code> file transfer between our local host and our backup server, we can combine the use of SSH and other security measures. By using SSH, we are able to encrypt our data as it is being transferred, making it much more difficult for any unauthorized individual to access it. Additionally, we can also use firewalls and other security protocols to ensure that our data is kept safe and secure during the transfer. By taking these steps, we can be confident that our data is protected and our file transfer is secure. Therefore we tell <code>rsync</code> to use SSH like the following:</p>
<h4>Secure Transfer of our Backup</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Secure Transfer of our Backup</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">rsync</span> -avz -e <span class="token function">ssh</span> /path/to/mydirectory user@backup_server:/path/to/backup/directory</span></span>
</code></pre></div></div>
<p>The data transfer between our local host and the backup server occurs over the encrypted SSH connection, which provides confidentiality and integrity protection for the data being transferred. This encryption process ensures that the data is protected from any potential malicious actors who would otherwise be able to access and modify the data without authorization. The encryption key itself is also safeguarded by a comprehensive set of security protocols, making it even more difficult for any unauthorized person to gain access to the data. In addition, the encrypted connection is designed to be highly resistant to any attempts to breach security, allowing us to have confidence in the protection of the data being transferred.</p>
<hr>
<h2>Auto-Synchronization</h2>
<p>To enable auto-synchronization using <code>rsync</code>, you can use a combination of <code>cron</code> and <code>rsync</code> to automate the synchronization process. Scheduling the cron job to run at regular intervals ensures that the contents of the two systems are kept in sync. This can be especially beneficial for organizations that need to keep their data synchronized across multiple machines. Furthermore, setting up auto-synchronization with <code>rsync</code> can be a great way to save time and effort, as it eliminates the need for manual synchronization. It also helps to ensure that the files and data stored in the systems are kept up-to-date and consistent, which helps to reduce errors and improve efficiency.</p>
<p>Therefore we create a new script called <code>RSYNC_Backup.sh</code>, which will trigger the <code>rsync</code> command to sync our local directory with the remote one.</p>
<h4>RSYNC_Backup.sh</h4>
<div class="window_container"><div class="window_content"><div class="window_top">Code: <span class="text-success">bash</span></div><pre class=" language-bash"><code class=" language-bash"><span class="token shebang important">#!/bin/bash</span>

<span class="token function">rsync</span> -avz -e <span class="token function">ssh</span> /path/to/mydirectory user@backup_server:/path/to/backup/directory
</code></pre></div></div>
<p>Then, in order to ensure that the script is able to execute properly, we must provide the necessary permissions. Additionally, it's also important to make sure that the script is owned by the correct user, as this will ensure that only the correct user has access to the script and that the script is not tampered with by any other user.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">RSYNC_Backup.sh</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">chmod</span> +x RSYNC_Backup.sh</span></span>
</code></pre></div></div>
<p>After that, we can create a crontab that tells <code>cron</code> to run the script every hour at the 0th minute. We can adjust the timing to suit our needs. To do so, the crontab needs the following content:</p>
<h4>Auto-Sync - Crontab</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Auto-Sync - Crontab</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output">0 * * * * /path/to/RSYNC_Backup.sh
</span></code></pre></div></div>
<p>With this setup, <code>cron</code> will be responsible for executing the script at the desired interval, ensuring that the <code>rsync</code> command is run and the contents of the local directory are synchronized with the remote host.</p>
<div id="screen" style="height: 600px; border: 1px solid;">
<div class="screenPlaceholder">
<div class="instanceLoading" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Instance is starting...</div>
</div>
<div class="instanceTerminating" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Terminating instance...</div>
</div>
<div class="row instanceStart max-width-canvas">
<div class="col-4"></div>
<div class="col-4">
<button class="startInstanceBtn btn btn-primary btn-lg btn-block " style="margin-top: 270px;">Start Instance
</button>
<p class="text-center mt-2 font-size-13 font-secondary">
<span class="text-success spawnsLeft">
0
</span> / 1 spawns left
</p>
</div>
<div class="col-4"></div>
</div>
</div>
</div>
<div class="row align-center justify-center my-4">
<div class="col-5 justify-start">
<button style="display:none;" target="_blank" class="instance-button fullScreenBtn btn btn-light btn-sm float-left "><i class="fad fa-expand text-success mr-1"></i> &nbsp;Full Screen
</button>
<button style="display:none;" class="instance-button terminateInstanceBtn btn btn-light btn-sm ml-2"><i class="fad fa-times text-danger"></i> &nbsp;Terminate
</button>
<button style="display:none;" class="instance-button resetInstanceBtn btn btn-light btn-sm ml-1"><i class="fad fa-sync text-warning mr-2"></i> &nbsp;Reset
</button>
<div class="btn-group " role="group">
<button style="display:none;cursor: default;" class="instance-button extendInstanceBtn btn btn-light btn-sm ml-1">Life Left:
<span class="lifeLeft"></span>m
</button>
</div>
</div>
<div id="statusText" class="col-7 justify-end pt-2 pr-2 font-size-small text-right">Waiting to
start...
</div>
</div>

</div>

<div class="training-module">
<h1>File System Management</h1>
<hr>
<p>File system management on Linux is a complex process that involves organizing and maintaining the data stored on a disk or other storage device. Linux is a powerful operating system that supports a wide range of file systems, including ext2, ext3, ext4, XFS, Btrfs, NTFS, and more. Each of these file systems offers unique features and benefits, and the best choice for any given situation will depend upon the specific requirements of the application or user. For example, ext2 is suitable for basic file system management tasks, while Btrfs offers robust data integrity and snapshot capabilities. Additionally, NTFS is useful when compatibility with Windows is required. No matter the situation, it is important to properly analyze the needs of the application or user before selecting a file system.</p>
<p>The Linux file system is based on the Unix file system, which is a hierarchical structure that is composed of various components. At the top of this structure is the inode table, the basis for the entire file system. The inode table is a table of information associated with each file and directory on a Linux system. Inodes contain metadata about the file or directory, such as its permissions, size, type, owner, and so on. The inode table is like a database of information about every file and directory on a Linux system, allowing the operating system to quickly access and manage files. Files can be stored in the Linux file system in one of two ways:</p>
<ul>
<li>Regular files</li>
<li>Directories</li>
</ul>
<p>Regular files are the most common type of file, and they are stored in the root directory of the file system. Directories are used to store collections of files. When a file is stored in a directory, the directory is known as the parent directory for the files. In addition to regular files and directories, Linux also supports symbolic links, which are references to other files or directories. Symbolic links can be used to quickly access files that are located in different parts of the file system. Each file and directory needs to be managed in terms of permissions. Permissions control who has access to files and directories. Each file and directory has an associated set of permissions that determines who can read, write, and execute the file. The same permissions apply to all users, so if the permissions of one user are changed, all other users will also be affected.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title"></span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">ls</span> -il</span></span>

<span class="token output">total 0
10678872 -rw-r--r--  1 cry0l1t3  htb  234123 Feb 14 19:30 myscript.py
10678869 -rw-r--r--  1 cry0l1t3  htb   43230 Feb 14 11:52 notes.txt
</span></code></pre></div></div>
<hr>
<h2>Disks &amp; Drives</h2>
<p>Disk management on Linux involves managing physical storage devices, including hard drives, solid-state drives, and removable storage devices. The main tool for disk management on Linux is the <code>fdisk</code>, which allows us to create, delete, and manage partitions on a drive. It can also display information about the partition table, including the size and type of each partition. Partitioning a drive on Linux involves dividing the physical storage space into separate, logical sections. Each partition can then be formatted with a specific file system, such as ext4, NTFS, or FAT32, and can be mounted as a separate file system. The most common partitioning tool on Linux is also <code>fdisk</code>, <code>gpart</code>, and <code>GParted</code>.</p>
<h4>Fdisk</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Fdisk</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">fdisk</span> -l</span></span>

<span class="token output">Disk /dev/vda: 160 GiB, 171798691840 bytes, 335544320 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x5223435f

Device     Boot     Start       End   Sectors  Size Id Type
/dev/vda1  *         2048 158974027 158971980 75.8G 83 Linux
/dev/vda2       158974028 167766794   8792767  4.2G 82 Linux swap / Solaris

Disk /dev/vdb: 452 KiB, 462848 bytes, 904 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
</span></code></pre></div></div>
<hr>
<h2>Mounting</h2>
<p>Each logical partition or drive needs to be assigned to a specific directory on Linux. This process is called mounting. Mounting involves attaching a drive to a specific directory, making it accessible to the file system hierarchy. Once a drive is mounted, it can be accessed and manipulated just like any other directory on the system. The <code>mount</code> tool is used to mount file systems on Linux, and the <code>/etc/fstab</code> file is used to define the default file systems that are mounted at boot time.</p>
<h4>Mounted File systems at Boot</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Mounted File systems at Boot</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">cat</span> /etc/fstab</span></span>

<span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">/etc/fstab: static <span class="token function">file</span> system information.</span></span>
<span class="token output">#
</span><span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">Use <span class="token string">'blkid'</span> to print the universally unique identifier <span class="token keyword">for</span> a device<span class="token punctuation">;</span> this may</span></span>
<span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">be used with <span class="token assign-left variable">UUID</span><span class="token operator">=</span> as a <span class="token function">more</span> robust way to name devices that works even <span class="token keyword">if</span></span></span>
<span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">disks are added and removed. See fstab<span class="token punctuation">(</span><span class="token number">5</span><span class="token punctuation">)</span>.</span></span>
<span class="token output">#
</span><span class="token command"><span class="token shell-symbol important">#</span><span class="token bash language-bash"> </span></span><span class="token output">&lt;file system&gt;                      &lt;mount point&gt;  &lt;type&gt;  &lt;options&gt;  &lt;dump&gt;  &lt;pass&gt;
UUID=3d6a020d-...SNIP...-9e085e9c927a /              btrfs   subvol=@,defaults,noatime,nodiratime,nodatacow,space_cache,autodefrag 0 1
UUID=3d6a020d-...SNIP...-9e085e9c927a /home          btrfs   subvol=@home,defaults,noatime,nodiratime,nodatacow,space_cache,autodefrag 0 2
UUID=21f7eb94-...SNIP...-d4f58f94e141 swap           swap    defaults,noatime 0 0

</span></code></pre></div></div>
<p>To view the currently mounted file systems, we can use the "mount" command without any arguments. The output will show a list of all the currently mounted file systems, including the device name, file system type, mount point, and options.</p>
<h4>List Mounted Drives</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">List Mounted Drives</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">mount</span></span></span>

<span class="token output">sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)
proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)
udev on /dev type devtmpfs (rw,nosuid,relatime,size=4035812k,nr_inodes=1008953,mode=755,inode64)
devpts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)
tmpfs on /run type tmpfs (rw,nosuid,nodev,noexec,relatime,size=814580k,mode=755,inode64)
/dev/vda1 on / type btrfs (rw,noatime,nodiratime,nodatasum,nodatacow,space_cache,autodefrag,subvolid=257,subvol=/@)
</span></code></pre></div></div>
<p>To mount a file system, we can use the <code>mount</code> command followed by the device name and the mount point. For example, to mount a USB drive with the device name <code>/dev/sdb1</code> to the directory <code>/mnt/usb</code>, we would use the following command:</p>
<h4>Mount a USB drive</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Mount a USB drive</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">mount</span> /dev/sdb1 /mnt/usb</span></span>
<span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token builtin class-name">cd</span> /mnt/usb <span class="token operator">&amp;&amp;</span> <span class="token function">ls</span> -l</span></span>

<span class="token output">total 32
drwxr-xr-x 1 root root   18 Oct 14  2021 'Account Takeover'
drwxr-xr-x 1 root root   18 Oct 14  2021 'API Key Leaks'
drwxr-xr-x 1 root root   18 Oct 14  2021 'AWS Amazon Bucket S3'
drwxr-xr-x 1 root root   34 Oct 14  2021 'Command Injection'
drwxr-xr-x 1 root root   18 Oct 14  2021 'CORS Misconfiguration'
drwxr-xr-x 1 root root   52 Oct 14  2021 'CRLF Injection'
drwxr-xr-x 1 root root   30 Oct 14  2021 'CSRF Injection'
drwxr-xr-x 1 root root   18 Oct 14  2021 'CSV Injection'
drwxr-xr-x 1 root root 1166 Oct 14  2021 'CVE Exploits'
...SNIP...
</span></code></pre></div></div>
<p>To unmount a file system in Linux, we can use the <code>umount</code> command followed by the mount point of the file system we want to unmount. The mount point is the location in the file system where the file system is mounted and is accessible to us. For example, to unmount the USB drive that was previously mounted to the directory <code>/mnt/usb</code>, we would use the following command:</p>
<h4>Unmount</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Unmount</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">umount</span> /mnt/usb</span></span>
</code></pre></div></div>
<p>It is important to note that we must have sufficient permissions to unmount a file system. We also cannot unmount a file system that is in use by a running process. To ensure that there are no running processes that are using the file system, we can use the <code>lsof</code> command to list the open files on the file system.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Unmount</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">lsof</span> <span class="token operator">|</span> <span class="token function">grep</span> cry0l1t3</span></span>

<span class="token output">vncserver 6006        cry0l1t3  mem       REG      0,24       402274 /usr/bin/perl (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24      1554101 /usr/lib/locale/aa_DJ.utf8/LC_COLLATE (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24       402326 /usr/lib/x86_64-linux-gnu/perl-base/auto/POSIX/POSIX.so (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24       402059 /usr/lib/x86_64-linux-gnu/perl/5.32.1/auto/Time/HiRes/HiRes.so (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24      1444250 /usr/lib/x86_64-linux-gnu/libnss_files-2.31.so (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24       402327 /usr/lib/x86_64-linux-gnu/perl-base/auto/Socket/Socket.so (path dev=0,26)
vncserver 6006        cry0l1t3  mem       REG      0,24       402324 /usr/lib/x86_64-linux-gnu/perl-base/auto/IO/IO.so (path dev=0,26)
...SNIP...
</span></code></pre></div></div>
<p>If we find any processes that are using the file system, we need to stop them before we can unmount the file system. Additionally, we can also unmount a file system automatically when the system is shut down by adding an entry to the <code>/etc/fstab</code> file. The <code>/etc/fstab</code> file contains information about all the file systems that are mounted on the system, including the options for automatic mounting at boot time and other mount options. To unmount a file system automatically at shutdown, we need to add the <code>noauto</code> option to the entry in the <code>/etc/fstab</code> file for that file system. This would like, for example, like following:</p>
<h4>Fstab File</h4>
<div class="window_container"><div class="window_content"><div class="window_top">Code: <span class="text-success">txt</span></div><pre class=" language-txt"><code class=" language-txt">/dev/sda1 / ext4 defaults 0 0
/dev/sda2 /home ext4 defaults 0 0
/dev/sdb1 /mnt/usb ext4 rw,auto,user 0 0
192.168.1.100:/nfs /mnt/nfs nfs defaults 0 0
</code></pre></div></div>
<hr>
<h2>SWAP</h2>
<p>Swap space is a crucial aspect of memory management in Linux, and it plays an important role in ensuring that the system runs smoothly, even when the available physical memory is depleted. When the system runs out of physical memory, the kernel transfers inactive pages of memory to the swap space, freeing up physical memory for use by active processes. This process is known as swapping.</p>
<p>Swap space can be created either during the installation of the operating system or at any time afterward using the <code>mkswap</code> and <code>swapon</code> commands. The <code>mkswap</code> command is used to set up a Linux swap area on a device or in a file, while the <code>swapon</code> command is used to activate a swap area. The size of the swap space is a matter of personal preference and depends on the amount of physical memory installed in the system and the type of usage the system will be subjected to. When creating a swap space, it is important to ensure that it is placed on a dedicated partition or file, separate from the rest of the file system. This helps to prevent fragmentation of the swap space and ensures that the system has adequate swap space available when it is needed. It is also important to ensure that the swap space is encrypted, as sensitive data may be stored in the swap space temporarily.</p>
<p>In addition to being used as an extension of physical memory, swap space can also be used for hibernation, which is a power management feature that allows the system to save its state to disk and then power off instead of shutting down completely. When the system is later powered on, it can restore its state from the swap space, returning to the state it was in before it was powered off.</p>
<div id="screen" style="height: 600px; border: 1px solid;">
<div class="screenPlaceholder">
<div class="instanceLoading" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Instance is starting...</div>
</div>
<div class="instanceTerminating" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Terminating instance...</div>
</div>
<div class="row instanceStart max-width-canvas">
<div class="col-4"></div>
<div class="col-4">
<button class="startInstanceBtn btn btn-primary btn-lg btn-block " style="margin-top: 270px;">Start Instance
</button>
<p class="text-center mt-2 font-size-13 font-secondary">
<span class="text-success spawnsLeft">
0
</span> / 1 spawns left
</p>
</div>
<div class="col-4"></div>
</div>
</div>
</div>
<div class="row align-center justify-center my-4">
<div class="col-5 justify-start">
<button style="display:none;" target="_blank" class="instance-button fullScreenBtn btn btn-light btn-sm float-left "><i class="fad fa-expand text-success mr-1"></i> &nbsp;Full Screen
</button>
<button style="display:none;" class="instance-button terminateInstanceBtn btn btn-light btn-sm ml-2"><i class="fad fa-times text-danger"></i> &nbsp;Terminate
</button>
<button style="display:none;" class="instance-button resetInstanceBtn btn btn-light btn-sm ml-1"><i class="fad fa-sync text-warning mr-2"></i> &nbsp;Reset
</button>
<div class="btn-group " role="group">
<button style="display:none;cursor: default;" class="instance-button extendInstanceBtn btn btn-light btn-sm ml-1">Life Left:
<span class="lifeLeft"></span>m
 </button>
</div>
</div>
<div id="statusText" class="col-7 justify-end pt-2 pr-2 font-size-small text-right">Waiting to
start...
</div>
</div>
<div class="card" id="questionsDiv">
<div class="card-body">
<div class="row">
<div class="col-9">
<h4 class="card-title mt-0 font-size-medium">Questions</h4>
<p class="card-title-desc font-size-large font-size-15">Answer the question(s) below
to complete this Section and earn cubes!</p>
</div>
<div class="col-3 text-right float-right">
<button class="btn btn-light bg-color-blue-nav mt-2 w-100 d-flex align-items-center" data-toggle="modal" data-target="#cheatSheetModal">
<div><i class="fad fa-file-alt mr-2"></i></div>
<div class="text-center w-100 ml-1">Cheat Sheet</div>
</button>
</div>
</div>
<div>
<div>
<label class="module-question" for="1573"><span class="badge badge-soft-dark font-size-14 mr-2">+ 0 <i class="fad fa-cube text-success"></i></span> What is the size in GiB of the "/dev/sda" disk in our Pwnbox? (Format: 000)
</label>
<div class="row">
<div class="col-lg-12 mb-4">
<input class="form-control text-success" type="text" value="160" disabled="true">
</div>
<div class="d-flex justify-content-end w-100 mr-3">
<div class="mb-4 mr-1">
<button class="btn btn-primary btn-block btnAnswer" id="btnAnswer1573" data-question-id="1573" disabled="true">
<div class="submit-button-text">
<i class="fad fa-flag-checkered mr-2"></i> Submit
</div>
<div class="submit-button-loader mx-4 d-none">
<i class="fa fa-circle-notch fa-spin"></i>
</div>
</button>
</div>
</div>
</div>
<div class=""></div>
</div>
</div>
</div>
</div>
</div>





<div class="col-md-12 col-xl-9 col-xxl-7">
<div class="training-module">
<h1>Containerization</h1>
<hr>
<p>Containerization is a process of packaging and running applications in isolated environments, such as a container, virtual machine, or serverless environment. Technologies like Docker, Docker Compose, and Linux Containers make this process possible in Linux systems. These technologies allow users to create, deploy, and manage applications quickly, securely, and efficiently. With these tools, users can configure their applications in various ways, allowing them to tailor the application to their needs. Additionally, containers are incredibly lightweight, perfect for running multiple applications simultaneously and providing scalability and portability. Containerization is a great way to ensure that applications are managed and deployed efficiently and securely.</p>
<p>Container security is an important aspect of containerization. They provide users a secure environment for running their applications since they are isolated from the host system and other containers. This isolation helps protect the host system from any malicious activities in the container while providing an additional layer of security for the applications running on the containers. Additionally, containers have the advantage of being lightweight, which makes them more difficult to compromise than traditional virtual machines. Furthermore, containers are easy to configure, making them ideal for running applications securely.</p>
<p>In addition to providing a secure environment, containers provide users with many other advantages because they make applications easier to deploy and manage and more efficient for running multiple applications simultaneously. However, methods still exist to escalate our privileges on containers and escape those.</p>
<hr>
<h2>Dockers</h2>
<p>Docker is an open-source platform for automating the deployment of applications as self-contained units called containers. It uses a layered filesystem and resource isolation features to provide flexibility and portability. Additionally, it provides a robust set of tools for creating, deploying, and managing applications, which helps streamline the containerization process.</p>
<h4>Install Docker-Engine</h4>
<p>Installing Docker is relatively straightforward. We can use the following script to install it on a Ubuntu host:</p>
<div class="window_container"><div class="window_content"><div class="window_top">Code: <span class="text-success">bash</span></div><pre class=" language-bash"><code class=" language-bash"><span class="token shebang important">#!/bin/bash</span>

<span class="token comment"># Preparation</span>
<span class="token function">sudo</span> <span class="token function">apt</span> update -y
<span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> ca-certificates <span class="token function">curl</span> gnupg lsb-release -y
<span class="token function">sudo</span> <span class="token function">mkdir</span> -m 0755 -p /etc/apt/keyrings
<span class="token function">curl</span> -fsSL https://download.docker.com/linux/ubuntu/gpg <span class="token operator">|</span> <span class="token function">sudo</span> gpg --dearmor -o /etc/apt/keyrings/docker.gpg
<span class="token builtin class-name">echo</span> <span class="token string">"deb [arch=<span class="token variable"><span class="token variable">$(</span>dpkg --print-architecture<span class="token variable">)</span></span> signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu <span class="token variable"><span class="token variable">$(</span>lsb_release -cs<span class="token variable">)</span></span> stable"</span> <span class="token operator">|</span> <span class="token function">sudo</span> <span class="token function">tee</span> /etc/apt/sources.list.d/docker.list <span class="token operator">&gt;</span> /dev/null

<span class="token comment"># Install Docker Engine</span>
<span class="token function">sudo</span> <span class="token function">apt</span> update -y
<span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

<span class="token comment"># Add user htb-student to the Docker group</span>
<span class="token function">sudo</span> <span class="token function">usermod</span> -aG docker htb-student
<span class="token builtin class-name">echo</span> <span class="token string">'[!] You need to log out and log back in for the group changes to take effect.'</span>

<span class="token comment"># Test Docker installation</span>
docker run hello-world
</code></pre></div></div>
<p>The Docker engine and specific Docker images are needed to run a container. These can be obtained from the <a href="%5Bhttps://hub.docker.com/%5D(https://hub.docker.com/)" target="_blank" rel="noopener nofollow">Docker Hub</a>, a repository of pre-made images, or created by the user. The Docker Hub is a cloud-based registry for software repositories or a library for Docker images. It is divided into a <code>public</code> and a <code>private</code> area. The public area allows users to upload and share images with the community. It also contains official images from the Docker development team and established open-source projects. Images uploaded to a private area of the registry are not publicly accessible. They can be shared within a company or with teams and acquaintances.</p>
<p>Creating a Docker image is done by creating a <a href="%5Bhttps://docs.docker.com/engine/reference/builder/%5D(https://docs.docker.com/engine/reference/builder/)" target="_blank" rel="noopener nofollow">Dockerfile</a>, which contains all the instructions the Docker engine needs to create the container. We can use Docker containers as our “file hosting” server when transferring specific files to our target systems. Therefore, we must create a <code>Dockerfile</code> based on Ubuntu 22.04 with <code>Apache</code> and <code>SSH</code> server running. With this, we can use <code>scp</code> to transfer files to the docker image, and Apache allows us to host files and use tools like <code>curl</code>, <code>wget</code>, and others on the target system to download the required files. Such a <code>Dockerfile</code> could look like the following:</p>
<h4>Dockerfile</h4>
<div class="window_container"><div class="window_content"><div class="window_top">Code: <span class="text-success">bash</span></div><pre class=" language-bash"><code class=" language-bash"><span class="token comment"># Use the latest Ubuntu 22.04 LTS as the base image</span>
FROM ubuntu:22.04

<span class="token comment"># Update the package repository and install the required packages</span>
RUN <span class="token function">apt-get</span> update <span class="token operator">&amp;&amp;</span> <span class="token punctuation">\</span>
    <span class="token function">apt-get</span> <span class="token function">install</span> -y <span class="token punctuation">\</span>
        apache2 <span class="token punctuation">\</span>
        openssh-server <span class="token punctuation">\</span>
        <span class="token operator">&amp;&amp;</span> <span class="token punctuation">\</span>
    <span class="token function">rm</span> -rf /var/lib/apt/lists/*

<span class="token comment"># Create a new user called "student"</span>
RUN <span class="token function">useradd</span> -m docker-user <span class="token operator">&amp;&amp;</span> <span class="token punctuation">\</span>
    <span class="token builtin class-name">echo</span> <span class="token string">"docker-user:password"</span> <span class="token operator">|</span> chpasswd

<span class="token comment"># Give the htb-student user full access to the Apache and SSH services</span>
RUN <span class="token function">chown</span> -R docker-user:docker-user /var/www/html <span class="token operator">&amp;&amp;</span> <span class="token punctuation">\</span>
    <span class="token function">chown</span> -R docker-user:docker-user /var/run/apache2 <span class="token operator">&amp;&amp;</span> <span class="token punctuation">\</span>
    <span class="token function">chown</span> -R docker-user:docker-user /var/log/apache2 <span class="token operator">&amp;&amp;</span> <span class="token punctuation">\</span>
    <span class="token function">chown</span> -R docker-user:docker-user /var/lock/apache2 <span class="token operator">&amp;&amp;</span> <span class="token punctuation">\</span>
    <span class="token function">usermod</span> -aG <span class="token function">sudo</span> docker-user <span class="token operator">&amp;&amp;</span> <span class="token punctuation">\</span>
    <span class="token builtin class-name">echo</span> <span class="token string">"docker-user ALL=(ALL) NOPASSWD: ALL"</span> <span class="token operator">&gt;&gt;</span> /etc/sudoers

<span class="token comment"># Expose the required ports</span>
EXPOSE <span class="token number">22</span> <span class="token number">80</span>

<span class="token comment"># Start the SSH and Apache services</span>
CMD <span class="token function">service</span> <span class="token function">ssh</span> start <span class="token operator">&amp;&amp;</span> /usr/sbin/apache2ctl -D FOREGROUND
</code></pre></div></div>
<p>After we have defined our Dockerfile, we need to convert it into an image. With the <code>build</code> command, we take the directory with the Dockerfile, execute the steps from the <code>Dockerfile</code>, and store the image in our local Docker Engine. If one of the steps fails due to an error, the container creation will be aborted. With the option <code>-t</code>, we give our container a tag, so it is easier to identify and work with later.</p>
<h4>Docker Build</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Docker Build</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">docker build -t FS_docker</span></span>
</code></pre></div></div>
<p>Once the Docker image has been created, it can be executed through the Docker engine, making it a very efficient and easy way to run a container. It is similar to the virtual machine concept, based on images. Still, these images are read-only templates and provide the file system necessary for runtime and all parameters. A container can be considered a running process of an image. When a container is to be started on a system, a package with the respective image is first loaded if unavailable locally. We can start the container by the following command <a href="%5Bhttps://docs.docker.com/engine/reference/commandline/run/%5D(https://docs.docker.com/engine/reference/commandline/run/)" target="_blank" rel="noopener nofollow">docker run</a>:</p>
<h4>Docker Run - Syntax</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Docker Run - Syntax</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">docker run -p </span></span><span class="token output">&lt;host port&gt;:&lt;docker port&gt; -d &lt;docker container name&gt;
</span></code></pre></div></div>
<h4>Docker Run</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Docker Run</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">docker run -p <span class="token number">8022</span>:22 -p <span class="token number">8080</span>:80 -d FS_docker</span></span>
</code></pre></div></div>
<p>In this case, we start a new container from the image <code>FS_docker</code> and map the host ports 8022 and 8080 to container ports 22 and 80, respectively. The container runs in the background, allowing us to access the SSH and HTTP services inside the container using the specified host ports.</p>
<h4>Docker Management</h4>
<p>When managing Docker containers, Docker provides a comprehensive suite of tools that enable us to easily create, deploy, and manage containers. With these powerful tools, we can list, start and stop containers and effectively manage them, ensuring seamless execution of applications. Some of the most commonly used Docker management commands are:</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th><strong>Command</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>docker ps</code></td>
<td>List all running containers</td>
</tr>
<tr>
<td><code>docker stop</code></td>
<td>Stop a running container.</td>
</tr>
<tr>
<td><code>docker start</code></td>
<td>Start a stopped container.</td>
</tr>
<tr>
<td><code>docker restart</code></td>
<td>Restart a running container.</td>
</tr>
<tr>
<td><code>docker rm</code></td>
<td>Remove a container.</td>
</tr>
<tr>
<td><code>docker rmi</code></td>
<td>Remove a Docker image.</td>
</tr>
<tr>
<td><code>docker logs</code></td>
<td>View the logs of a container.</td>
</tr>
</tbody>
</table></div>
<p>It is worth noting that these commands, used in Docker, can be combined with various options to provide additional functionality. For example, we can specify which ports to expose, mount volumes, or set environment variables. This allows us to customize our Docker containers to suit our needs and requirements. When working with Docker images, it's important to note that any changes made to an existing image are not permanent. Instead, we need to create a new image that inherits from the original and includes the desired changes.</p>
<p>This is done by creating a new Dockerfile that starts with the <code>FROM</code> statement, which specifies the base image, and then adds the necessary commands to make the desired changes. Once the Dockerfile is created, we can use the <code>docker build</code> command to build the new image, tagging it with a unique name to help identify it. This process ensures that the original image remains intact while allowing us to create a new image with the desired changes.</p>
<p>It is important to note that Docker containers are designed to be immutable, meaning that any changes made to a container during runtime are lost when the container is stopped. Therefore, it is recommended to use container orchestration tools such as Docker Compose or Kubernetes to manage and scale containers in a production environment.</p>
<hr>
<h2>Linux Containers</h2>
<p>Linux Containers (<code>LXC</code>) is a virtualization technology that allows multiple isolated Linux systems to run on a single host. It uses resource isolation features, such as <code>cgroups</code> and <code>namespaces</code>, to provide a lightweight virtualization solution. LXC also provides a rich set of tools and APIs for managing and configuring containers, contributing to its popularity as a containerization technology. By combining the advantages of LXC with the power of Docker, users can achieve a fully-fledged containerization experience in Linux systems.</p>
<p>Both LXC and Docker are containerization technologies that allow for applications to be packaged and run in isolated environments. However, there are some differences between the two that can be distinguished based on the following categories:</p>
<ul>
<li>Approach</li>
<li>Image building</li>
<li>Portability</li>
<li>Easy of use</li>
<li>Security</li>
</ul>
<p>LXC is a lightweight virtualization technology that uses resource isolation features of the Linux kernel to provide an isolated environment for applications. In LXC, images are manually built by creating a root filesystem and installing the necessary packages and configurations. Those containers are tied to the host system, may not be easily portable, and may require more technical expertise to configure and manage. LXC also provides some security features but may not be as robust as Docker.</p>
<p>On the other hand, Docker is an application-centric platform that builds on top of LXC and provides a more user-friendly interface for containerization. Its images are built using a Dockerfile, which specifies the base image and the steps required to build the image. Those images are designed to be portable so they can be easily moved from one environment to another. Docker provides a more user-friendly interface for containerization, with a rich set of tools and APIs for managing and configuring containers with a more secure environment for running applications.</p>
<p>To install LXC on a Linux distribution, we can use the distribution's package manager. For example, on Ubuntu, we can use the <code>apt</code> package manager to install LXC with the following command:</p>
<h4>Install LXC</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Install LXC</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt-get</span> <span class="token function">install</span> lxc lxc-utils -y</span></span>
</code></pre></div></div>
<p>Once LXC is installed, we can start creating and managing containers on the Linux host. It is worth noting that LXC requires the Linux kernel to support the necessary features for containerization. Most modern Linux kernels have built-in support for containerization, but some older kernels may require additional configuration or patching to enable support for LXC.</p>
<h4>Creating an LXC Container</h4>
<p>To create a new LXC container, we can use the <code>lxc-create</code> command followed by the container's name and the template to use. For example, to create a new Ubuntu container named <code>linuxcontainer</code>, we can use the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Creating an LXC Container</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> lxc-create -n linuxcontainer -t ubuntu</span></span>
</code></pre></div></div>
<h4>Managing LXC Containers</h4>
<p>When working with LXC containers, several tasks are involved in managing them. These tasks include creating new containers, configuring their settings, starting and stopping them as necessary, and monitoring their performance. Fortunately, there are many command-line tools and configuration files available that can assist with these tasks. These tools enable us to quickly and easily manage our containers, ensuring they are optimized for our specific needs and requirements. By leveraging these tools effectively, we can ensure that our LXC containers run efficiently and effectively, allowing us to maximize our system's performance and capabilities.</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th>Command</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><code>lxc-ls</code></td>
<td>List all existing containers</td>
</tr>
<tr>
<td><code>lxc-stop -n &lt;container&gt;</code></td>
<td>Stop a running container.</td>
</tr>
<tr>
<td><code>lxc-start -n &lt;container&gt;</code></td>
<td>Start a stopped container.</td>
</tr>
<tr>
<td><code>lxc-restart -n &lt;container&gt;</code></td>
<td>Restart a running container.</td>
</tr>
<tr>
<td><code>lxc-config -n &lt;container name&gt; -s storage</code></td>
<td>Manage container storage</td>
</tr>
<tr>
<td><code>lxc-config -n &lt;container name&gt; -s network</code></td>
<td>Manage container network settings</td>
</tr>
<tr>
<td><code>lxc-config -n &lt;container name&gt; -s security</code></td>
<td>Manage container security settings</td>
</tr>
<tr>
<td><code>lxc-attach -n &lt;container&gt;</code></td>
<td>Connect to a container.</td>
</tr>
<tr>
<td><code>lxc-attach -n &lt;container&gt; -f /path/to/share</code></td>
<td>Connect to a container and share a specific directory or file.</td>
</tr>
</tbody>
</table></div>
<p>As penetration testers, we may encounter situations where we must test software or systems with dependencies or configurations that are difficult to reproduce on our machines. This is where Linux containers come in handy. Since a Linux container is a lightweight, standalone executable package containing all the necessary dependencies and configuration files to run a specific software or system, it provides an isolated environment that can be run on any Linux machine, regardless of the host's configuration.</p>
<p>Containers are useful, especially because they allow us to quickly spin up an isolated environment specific to our testing needs. For example, we might need to test a web application requiring a specific database or web server version. Rather than setting up these components on our machine, which can be time-consuming and error-prone, we can create a container that contains the exact configuration we need.</p>
<p>We can also use them to test exploits or malware in a controlled environment where we create a container that simulates a vulnerable system or network and then use that container to safely test exploits without risking damaging our machines or networks. However, it is important to configure LXC container security to prevent unauthorized access or malicious activities inside the container. This can be achieved by implementing several security measures, such as:</p>
<ul>
<li>Restricting access to the container</li>
<li>Limiting resources</li>
<li>Isolating the container from the host</li>
<li>Enforcing mandatory access control</li>
<li>Keeping the container up to date</li>
</ul>
<p>LXC containers can be accessed using various methods, such as SSH or console. It is recommended to restrict access to the container by disabling unnecessary services, using secure protocols, and enforcing strong authentication mechanisms. For example, we can disable SSH access to the container by removing the <code>openssh-server</code> package or by configuring SSH only to allow access from trusted IP addresses. Those containers also share the same kernel as the host system, meaning they can access all the resources available on the system. We can use resource limits or quotas to prevent containers from consuming excessive resources. For example, we can use <code>cgroups</code> to limit the amount of CPU, memory, or disk space that a container can use.</p>
<h4>Securing LXC</h4>
<p>Let us limit the resources to the container. In order to configure <code>cgroups</code> for LXC and limit the CPU and memory, a container can create a new configuration file in the <code>/usr/share/lxc/config/&lt;container name&gt;.conf</code> directory with the name of our container. For example, to create a configuration file for a container named <code>linuxcontainer</code>, we can use the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Securing LXC</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">vim</span> /usr/share/lxc/config/linuxcontainer.conf</span></span>
</code></pre></div></div>
<p>In this configuration file, we can add the following lines to limit the CPU and memory the container can use.</p>
<div class="window_container"><div class="window_content"><div class="window_top">Code: <span class="text-success">txt</span></div><pre class=" language-txt"><code class=" language-txt">lxc.cgroup.cpu.shares = 512
lxc.cgroup.memory.limit_in_bytes = 512M
</code></pre></div></div>
<p>When working with containers, it is important to understand the <code>lxc.cgroup.cpu.shares</code> parameter. This parameter determines the CPU time a container can use in relation to the other containers on the system. By default, this value is set to 1024, meaning the container can use up to its fair share of CPU time. However, if we set this value to 512, for example, the container can only use half of the CPU time available on the system. This can be a useful way to manage resources and ensure all containers have the necessary access to CPU time.</p>
<p>One of the key parameters in controlling the resource allocation of a container is the <code>lxc.cgroup.memory.limit_in_bytes</code> parameter. This parameter allows you to set the maximum amount of memory a container can use. It's important to note that this value can be specified in a variety of units, including bytes, kilobytes (K), megabytes (M), gigabytes (G), or terabytes (T), allowing for a high degree of granularity in defining container resource limits. After adding these two lines, we can save and close the file by typing:</p>
<ul>
<li>
<code>[Esc]</code>
</li>
<li>
<code>:</code>
</li>
<li>
<code>wq</code>
</li>
</ul>
<p>To apply these changes, we must restart the LXC service.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Securing LXC</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> systemctl restart lxc.service</span></span>
</code></pre></div></div>
<p>LXC use <code>namespaces</code> to provide an isolated environment for processes, networks, and file systems from the host system. Namespaces are a feature of the Linux kernel that allows for creating isolated environments by providing an abstraction of system resources.</p>
<p>Namespaces are a crucial aspect of containerization as they provide a high degree of isolation for the container's processes, network interfaces, routing tables, and firewall rules. Each container is allocated a unique process ID (<code>pid</code>) number space, isolated from the host system's process IDs. This ensures that the container's processes cannot interfere with the host system's processes, enhancing system stability and reliability. Additionally, each container has its own network interfaces (<code>net</code>), routing tables, and firewall rules, which are completely separate from the host system's network interfaces. Any network-related activity within the container is cordoned off from the host system's network, providing an extra layer of network security.</p>
<p>Moreover, containers come with their own root file system (<code>mnt</code>), which is entirely different from the host system's root file system. This separation between the two ensures that any changes or modifications made within the container's file system do not affect the host system's file system. However, it is important to remember that while namespaces provide a high level of isolation, they do not provide complete security. Therefore, it is always advisable to implement additional security measures to further protect the container and the host system from potential security breaches.</p>
<p>Here are 9 optional exercises to practice LXC:</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td>1</td>
<td>Install LXC on your machine and create your first container.</td>
</tr>
<tr>
<td>2</td>
<td>Configure the network settings for your LXC container.</td>
</tr>
<tr>
<td>3</td>
<td>Create a custom LXC image and use it to launch a new container.</td>
</tr>
<tr>
<td>4</td>
<td>Configure resource limits for your LXC containers (CPU, memory, disk space).</td>
</tr>
<tr>
<td>5</td>
<td>Explore the <code>lxc-*</code> commands for managing containers.</td>
</tr>
<tr>
<td>6</td>
<td>Use LXC to create a container running a specific version of a web server (e.g., Apache, Nginx).</td>
</tr>
<tr>
<td>7</td>
<td>Configure SSH access to your LXC containers and connect to them remotely.</td>
</tr>
<tr>
<td>8</td>
<td>Create a container with persistence, so changes made to the container are saved and can be reused.</td>
</tr>
<tr>
<td>9</td>
<td>Use LXC to test software in a controlled environment, such as a vulnerable web application or malware.</td>
</tr>
</tbody>
</table></div>
<div id="screen" style="height: 600px; border: 1px solid;">
<div class="screenPlaceholder">
<div class="instanceLoading" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Instance is starting...</div>
</div>
<div class="instanceTerminating" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Terminating instance...</div>
</div>
<div class="row instanceStart max-width-canvas">
<div class="col-4"></div>
<div class="col-4">
<button class="startInstanceBtn btn btn-primary btn-lg btn-block " style="margin-top: 270px;">Start Instance
</button>
<p class="text-center mt-2 font-size-13 font-secondary">
 <span class="text-success spawnsLeft">
0
</span> / 1 spawns left
</p>
</div>
<div class="col-4"></div>
</div>
</div>
</div>
<div class="row align-center justify-center my-4">
<div class="col-5 justify-start">
<button style="display:none;" target="_blank" class="instance-button fullScreenBtn btn btn-light btn-sm float-left "><i class="fad fa-expand text-success mr-1"></i> &nbsp;Full Screen
</button>
<button style="display:none;" class="instance-button terminateInstanceBtn btn btn-light btn-sm ml-2"><i class="fad fa-times text-danger"></i> &nbsp;Terminate
</button>
<button style="display:none;" class="instance-button resetInstanceBtn btn btn-light btn-sm ml-1"><i class="fad fa-sync text-warning mr-2"></i> &nbsp;Reset
</button>
<div class="btn-group " role="group">
<button style="display:none;cursor: default;" class="instance-button extendInstanceBtn btn btn-light btn-sm ml-1">Life Left:
<span class="lifeLeft"></span>m
</button>
</div>
</div>
<div id="statusText" class="col-7 justify-end pt-2 pr-2 font-size-small text-right">Waiting to
start...
</div>
</div>
</div>
<div class="card bg-color-blue-nav" style="margin: 30px 0">
<div class="card-body">
<a href="https://academy.hackthebox.com/module/18/section/2096" class="btn btn-light module-button py-2" style="float: left"><i class="fa fa-arrow-alt-left mr-1"></i> Previous</a>
<form action="https://academy.hackthebox.com/module" method="POST" class="form-inline" id="completeForm" style="float: right">
<input type="hidden" name="module_id" value="18">
<input type="hidden" name="page_id" value="24">
<input type="hidden" name="completed" value="1">
<button id="completeBtn" class="btn btn-outline-success" style="">
<div id="complete-button-text">
<i class="fa fa-check-circle"></i> Mark Complete &amp; Next
</div>
<div id="complete-button-loader" class="mx-5 d-none">
<i class="fa fa-circle-notch fa-spin"></i>
</div>
</button>
</form>
<a href="https://academy.hackthebox.com/module/18/section/2098" class="btn btn-light ml-2 module-button py-2" style="float: left">Next <i class="ml-1 fa fa-arrow-alt-right"></i></a>
</div>
</div>
</div>

<div class="training-module">
<h1>Network Configuration</h1>
<hr>
<p>As a penetration tester, one of the key skills required is configuring and managing network settings on Linux systems. This skill is valuable in setting up testing environments, controlling network traffic, or identifying and exploiting vulnerabilities. By understanding Linux's network configuration options, we can tailor our testing approach to suit our specific needs and optimize our results.</p>
<p>One of the primary network configuration tasks is configuring network interfaces. This includes assigning IP addresses, configuring network devices such as routers and switches, and setting up network protocols. It is essential to thoroughly understand the network protocols and their specific use cases, such as TCP/IP, DNS, DHCP, and FTP. Additionally, we should be familiar with different network interfaces, including wireless and wired connections, and be able to troubleshoot connectivity issues.</p>
<p>Network access control is another critical component of network configuration. As a penetration testers, we should be familiar with the importance of NAC for network security and the different NAC technologies available. These include:</p>
<ul>
<li>Discretionary access control (DAC)</li>
<li>Mandatory access control (MAC)</li>
<li>Role-based access control (RBAC)</li>
</ul>
<p>We should also understand the different NAC enforcement mechanisms and know how to configure Linux network devices for NAC. This includes setting up SELinux policies, configuring AppArmor profiles, and using TCP wrappers to control access.</p>
<p>Monitoring network traffic is also an essential part of network configuration. Therefore, we should know how to configure network monitoring and logging and be able to analyze network traffic for security purposes. Tools such as syslog, rsyslog, ss, lsof, and the ELK stack can be used to monitor network traffic and identify security issues.</p>
<p>Moreover, good knowledge of network troubleshooting tools is crucial for identifying vulnerabilities and interacting with other networks and hosts. In addition to the tools we mentioned, we can use ping, nslookup, and nmap to diagnose and enumerate networks. These tools can provide valuable insight into network traffic, packet loss, latency, DNS resolution, etc. By understanding how to use these tools effectively, we can quickly pinpoint the root cause of any network problem and take the necessary steps to resolve it.</p>
<hr>
<h2>Configuring Network Interfaces</h2>
<p>When working with Ubuntu, you can configure local network interfaces using the <code>ifconfig</code> or the <code>ip</code> command. These powerful commands allow us to view and configure our system's network interfaces. Whether we're looking to make changes to our existing network setup or need to check on the status of our interfaces, these commands can greatly simplify the process. Moreover, developing a firm grasp on the intricacies of network interfaces is an essential ability in the modern, interconnected world. With the rapid advancement of technology and the increasing reliance on digital communication, having a comprehensive knowledge of how to work with network interfaces can enable you to navigate the diverse array of networks that exist nowadays effectively.</p>
<p>One way to obtain information regarding network interfaces, such as IP addresses, netmasks, and status, is by using the <code>ifconfig</code> command. By executing this command, we can view the available network interfaces and their respective attributes in a clear and organized manner. This information can be particularly useful when troubleshooting network connectivity issues or setting up a new network configuration. It should be noted that the <code>ifconfig</code> command has been deprecated in newer versions of Linux and replaced by the <code>ip</code> command, which offers more advanced features. Nevertheless, the <code>ifconfig</code> command is still widely used in many Linux distributions and continues to be a reliable tool for network management.</p>
<h4>Network Settings</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Network Settings</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">ifconfig</span></span></span>

<span class="token output">eth0: flags=4163&lt;UP,BROADCAST,RUNNING,MULTICAST&gt;  mtu 1500
        inet 178.62.32.126  netmask 255.255.192.0  broadcast 178.62.63.255
        inet6 fe80::88d9:faff:fecf:797a  prefixlen 64  scopeid 0x20&lt;link&gt;
        ether 8a:d9:fa:cf:79:7a  txqueuelen 1000  (Ethernet)
        RX packets 7910  bytes 717102 (700.2 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7072  bytes 24215666 (23.0 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163&lt;UP,BROADCAST,RUNNING,MULTICAST&gt;  mtu 1500
        inet 10.106.0.66  netmask 255.255.240.0  broadcast 10.106.15.255
        inet6 fe80::b8ab:52ff:fe32:1f33  prefixlen 64  scopeid 0x20&lt;link&gt;
        ether ba:ab:52:32:1f:33  txqueuelen 1000  (Ethernet)
        RX packets 14  bytes 1574 (1.5 KiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15  bytes 1700 (1.6 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73&lt;UP,LOOPBACK,RUNNING&gt;  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10&lt;host&gt;
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 15948  bytes 24561302 (23.4 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 15948  bytes 24561302 (23.4 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0


</span><span class="token info punctuation"><span class="token user">cry0l1t3@htb</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">ip</span> addr</span></span>

<span class="token output">1: lo: &lt;LOOPBACK,UP,LOWER_UP&gt; mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: eth0: &lt;BROADCAST,MULTICAST,UP,LOWER_UP&gt; mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 8a:d9:fa:cf:79:7a brd ff:ff:ff:ff:ff:ff
    altname enp0s3
    altname ens3
    inet 178.62.32.126/18 brd 178.62.63.255 scope global dynamic eth0
       valid_lft 85274sec preferred_lft 85274sec
    inet6 fe80::88d9:faff:fecf:797a/64 scope link 
       valid_lft forever preferred_lft forever
3: eth1: &lt;BROADCAST,MULTICAST,UP,LOWER_UP&gt; mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether ba:ab:52:32:1f:33 brd ff:ff:ff:ff:ff:ff
    altname enp0s4
    altname ens4
    inet 10.106.0.66/20 brd 10.106.15.255 scope global dynamic eth1
       valid_lft 85274sec preferred_lft 85274sec
    inet6 fe80::b8ab:52ff:fe32:1f33/64 scope link 
       valid_lft forever preferred_lft forever
</span></code></pre></div></div>
<p>When it comes to activating network interfaces, <code>ifconfig</code> and <code>ip</code> commands are two commonly used tools. These commands allow users to modify and activate settings for a specific interface, such as <code>eth0</code>. We can adjust the network settings to suit our needs by using the appropriate syntax and specifying the interface name.</p>
<h4>Activate Network Interface</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Activate Network Interface</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">ifconfig</span> eth0 up     <span class="token comment"># OR</span></span></span>
<span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">ip</span> <span class="token function">link</span> <span class="token builtin class-name">set</span> eth0 up</span></span>
</code></pre></div></div>
<p>One way to allocate an IP address to a network interface is by utilizing the <code>ifconfig</code> command. We must specify the interface's name and IP address as arguments to do this. This is a crucial step in setting up a network connection. The IP address serves as a unique identifier for the interface and enables the communication between devices on the network.</p>
<h4>Assign IP Address to an Interface</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Assign IP Address to an Interface</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">ifconfig</span> eth0 <span class="token number">192.168</span>.1.2</span></span>
</code></pre></div></div>
<p>To set the netmask for a network interface, we can run the following command with the name of the interface and the netmask:</p>
<h4>Assign a Netmask to an Interface</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Assign a Netmask to an Interface</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">ifconfig</span> eth0 netmask <span class="token number">255.255</span>.255.0</span></span>
</code></pre></div></div>
<p>When we want to set the default gateway for a network interface, we can use the <code>route</code> command with the <code>add</code> option. This allows us to specify the gateway's IP address and the network interface to which it should be applied. By setting the default gateway, we are designating the IP address of the router that will be used to send traffic to destinations outside the local network. Ensuring that the default gateway is set correctly is important, as incorrect configuration can lead to connectivity issues.</p>
<h4>Assign the Route to an Interface</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Assign the Route to an Interface</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> route <span class="token function">add</span> default gw <span class="token number">192.168</span>.1.1 eth0</span></span>
</code></pre></div></div>
<p>When configuring a network interface, it is often necessary to set Domain Name System (<code>DNS</code>) servers to ensure proper network functionality. DNS servers translate domain names into IP addresses, allowing devices to connect with each other on the internet. By setting those, we can ensure that their devices can communicate with other devices and access websites and other online resources. Without proper DNS server configuration, devices may experience network connectivity issues and be unable to access certain online resources. This can be achieved by updating the <code>/etc/resolv.conf</code> file with the appropriate DNS server information. The <code>/etc/resolv.conf</code> file is a plain text file containing the system's DNS information. The system can properly resolve domain names to IP addresses by adding the required DNS servers to this file. It is important to note that any changes made to this file will only apply to the current session and must be updated if the system is restarted or the network configuration is changed.</p>
<h4>Editing DNS Settings</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Editing DNS Settings</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">vim</span> /etc/resolv.conf</span></span>
</code></pre></div></div>
<h4>/etc/resolv.conf</h4>
<div class="window_container"><div class="window_content"><div class="window_top">Code: <span class="text-success">txt</span></div><pre class=" language-txt"><code class=" language-txt">nameserver 8.8.8.8
nameserver 8.8.4.4
</code></pre></div></div>
<p>After completing the necessary modifications to the network configuration, it is essential to ensure that these changes are saved to persist across reboots. This can be achieved by editing the <code>/etc/network/interfaces</code> file, which defines network interfaces for Linux-based operating systems. Thus, it is vital to save any changes made to this file to avoid any potential issues with network connectivity.</p>
<h4>Editing Interfaces</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Editing Interfaces</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">vim</span> /etc/network/interfaces</span></span>
</code></pre></div></div>
<p>This will open the <code>interfaces</code> file in the vim editor. We can add the network configuration settings to the file like this:</p>
<h4>/etc/network/interfaces</h4>
<div class="window_container"><div class="window_content"><div class="window_top">Code: <span class="text-success">txt</span></div><pre class=" language-txt"><code class=" language-txt">auto eth0
iface eth0 inet static
  address 192.168.1.2
  netmask 255.255.255.0
  gateway 192.168.1.1
  dns-nameservers 8.8.8.8 8.8.4.4
</code></pre></div></div>
<p>By setting the <code>eth0</code> network interface to use a static IP address of <code>192.168.1.2</code>, with a netmask of <code>255.255.255.0</code> and a default gateway of <code>192.168.1.1</code>, we can ensure that your network connection remains stable and reliable. Additionally, by specifying DNS servers of <code>8.8.8.8</code> and <code>8.8.4.4</code>, we can ensure that our computer can easily access the internet and resolve domain names. Once we have made these changes to the configuration file, saving the file and exiting the editor is important. After that, we must restart the networking service to apply the changes.</p>
<h4>Restart Networking Service</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Restart Networking Service</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> systemctl restart networking</span></span>
</code></pre></div></div>
<hr>
<h2>Network Access Control</h2>
<p>Network access control (NAC) is a crucial component of network security, especially in today's era of increasing cyber threats. As a penetration tester, it is vital to understand the significance of NAC in protecting the network and the various NAC technologies that can be utilized to enhance security measures. NAC is a security system that ensures that only authorized and compliant devices are granted access to the network, preventing unauthorized access, data breaches, and other security threats. By implementing NAC, organizations can be confident in their ability to protect their assets and data from cybercriminals who always seek to exploit system vulnerabilities. The following are the different NAC technologies that can be used to enhance security measures:</p>
<ul>
<li>Discretionary access control (DAC)</li>
<li>Mandatory access control (MAC)</li>
<li>Role-based access control (RBAC)</li>
</ul>
<p>These technologies are designed to provide different levels of access control and security. Each technology has its unique characteristics and is suitable for different use cases. As a penetration tester, it is essential to understand these technologies and their specific use cases to test and evaluate the network's security effectively.</p>
<h4>Discretionary Access Control</h4>
<p>DAC is a crucial component of modern security systems as it helps organizations provide access to their resources while managing the associated risks of unauthorized access. It is a widely used access control system that enables users to manage access to their resources by granting resource owners the responsibility of controlling access permissions to their resources. This means that users and groups who own a specific resource can decide who has access to their resources and what actions they are authorized to perform. These permissions can be set for reading, writing, executing, or deleting the resource.</p>
<h4>Mandatory Access Control</h4>
<p>MAC is used in infrastructure that provides more fine-grained control over resource access than DAC systems. Those systems define rules that determine resource access based on the resource's security level and the user's security level or process requesting access. Each resource is assigned a security label that identifies its security level, and each user or process is assigned a security clearance that identifies its security level. Access to a resource is only granted if the user's or process's security level is equal to or greater than the security level of the resource. MAC is often used in operating systems and applications that require a high level of security, such as military or government systems, financial systems, and healthcare systems. MAC systems are designed to prevent unauthorized access to resources and minimize the impact of security breaches.</p>
<h4>Role-based Access Control</h4>
<p>RBAC assigns permissions to users based on their roles within an organization. Users are assigned roles based on their job responsibilities or other criteria, and each role is granted a set of permissions that determine the actions they can perform. RBAC simplifies the management of access permissions, reduces the risk of errors, and ensures that users can access only the resources necessary to perform their job functions. It can restrict access to sensitive resources and data, limit the impact of security breaches, and ensure compliance with regulatory requirements. Compared to Discretionary Access Control (DAC) systems, RBAC provides a more flexible and scalable approach to managing resource access. In an RBAC system, each user is assigned one or more roles, and each role is assigned a set of permissions that define the user's actions. Resource access is granted based on the user's assigned role rather than their identity or ownership of the resource. RBAC systems are typically used in environments with many users and resources, such as large organizations, government agencies, and financial institutions.</p>
<hr>
<h2>Monitoring</h2>
<p>Network monitoring involves capturing, analyzing, and interpreting network traffic to identify security threats, performance issues, and suspicious behavior. The primary goal of analyzing and monitoring network traffic is identifying security threats and vulnerabilities. For example, as penetration testers, we can capture credentials when someone uses an unencrypted connection and tries to log in to an FTP server. As a result, we will obtain this user’s credentials that might help us to infiltrate the network even further or escalate our privileges to a higher level. In short, by analyzing network traffic, we can gain insights into network behavior and identify patterns that may indicate security threats. Such analysis includes detecting suspicious network activity, identifying malicious traffic, and identifying potential security risks. However, we cover this vast topic in the <a href="%5Bhttps://academy.hackthebox.com/module/details/81%5D(https://academy.hackthebox.com/module/details/81)" target="_blank" rel="noopener nofollow">Intro to Network Traffic Analysis</a> module, where we use several tools for network monitoring on Linux systems like Ubuntu and Windows systems, like Wireshark, tshark, and Tcpdump.</p>
<hr>
<h2>Troubleshooting</h2>
<p>Network troubleshooting is an essential process that involves diagnosing and resolving network issues that can adversely affect the performance and reliability of the network. This process is critical for ensuring the network operates optimally and avoiding disruptions that could impact business operations during our penetration tests. It also involves identifying, analyzing, and implementing solutions to resolve problems. Such problems include connectivity problems, slow network speeds, and network errors. Various tools can help us identify and resolve issues regarding network troubleshooting on Linux systems. Some of the most commonly used tools include:</p>
<ol>
<li>Ping</li>
<li>Traceroute</li>
<li>Netstat</li>
<li>Tcpdump</li>
<li>Wireshark</li>
<li>Nmap</li>
</ol>
<p>By using these tools and others like them, we can better understand how the network functions and quickly diagnose any issues that may arise. For example, <code>ping</code> is a command-line tool used to test connectivity between two devices. It sends packets to a remote host and measures the time to return them. To use <code>ping</code>, we can enter the following command:</p>
<h4>Ping</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Ping</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">ping</span> </span></span><span class="token output">&lt;remote_host&gt;
</span></code></pre></div></div>
<p>For example, pinging the Google DNS server will send ICMP packets to the Google DNS server and display the response times.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Ping</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">ping</span> <span class="token number">8.8</span>.8.8</span></span>

<span class="token output">PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=119 time=1.61 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=119 time=1.06 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=119 time=0.636 ms
64 bytes from 8.8.8.8: icmp_seq=4 ttl=119 time=0.685 ms
^C
--- 8.8.8.8 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3017ms
rtt min/avg/max/mdev = 0.636/0.996/1.607/0.388 ms
</span></code></pre></div></div>
<p>Another tool is the <code>traceroute</code>, which traces the route packets take to reach a remote host. It sends packets with increasing Time-to-Live (TTL) values to a remote host and displays the IP addresses of the devices that the packets pass through. For example, to trace the route to the Google DNS server, we would enter the following command:</p>
<h4>Traceroute</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Traceroute</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">traceroute</span> www.inlanefreight.com</span></span>

<span class="token output">traceroute to www.inlanefreight.com (134.209.24.248), 30 hops max, 60 byte packets
 1  * * *
 2  10.80.71.5 (10.80.71.5)  2.716 ms  2.700 ms  2.730 ms
 3  * * *
 4  10.80.68.175 (10.80.68.175)  7.147 ms  7.132 ms 10.80.68.161 (10.80.68.161)  7.393 ms
</span></code></pre></div></div>
<p>This will display the IP addresses of the devices that the packets pass through to reach the Google DNS server. The output of a traceroute command shows how it is used to trace the path of packets to the website <a href="http://www.inlanefreight.com/" target="_blank" rel="noopener nofollow">www.inlanefreight.com</a>, which has an IP address of 134.209.24.248. Each line of the output contains valuable information.</p>
<p>When setting up a network connection, it's important to specify the destination host and IP address. In this example, the destination host is 134.209.24.248, and the maximum number of hops allowed is 30. This ensures that the connection is established efficiently and reliably. By providing this information, the system can route traffic to the correct destination and limit the number of intermediate stops the data needs to make.</p>
<p>The second line shows the first hop in the traceroute, which is the local network gateway with the IP address 10.80.71.5, followed by the next three columns show the time it took for each of the three packets sent to reach the gateway in milliseconds (2.716 ms, 2.700 ms, and 2.730 ms).</p>
<p>Next, we see the second hop in the traceroute. However, there was no response from the device at that hop, indicated by the three asterisks instead of the IP address. This could mean the device is down, blocking ICMP traffic, or a network issue caused the packets to drop.</p>
<p>In the fourth line, we can see the third hop in the traceroute, consisting of two devices with IP addresses 10.80.68.175 and 10.80.68.161, and again the next three columns show the time it took for each of the three packets to reach the first device (7.147 ms, 7.132 ms, and 7.393 ms).</p>
<h4>Netstat</h4>
<p><code>Netstat</code> is used to display active network connections and their associated ports. It can be used to identify network traffic and troubleshoot connectivity issues. To use <code>netstat</code>, we can enter the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Netstat</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">netstat</span> -a</span></span>

<span class="token output">Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 localhost:5901          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:sunrpc          0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:http            0.0.0.0:*               LISTEN     
tcp        0      0 0.0.0.0:ssh             0.0.0.0:*               LISTEN
...SNIP...
</span></code></pre></div></div>
<p>We can expect to receive detailed information about each connection when using this tool. This includes the protocol used, the number of bytes received and sent, IP addresses, port numbers of both local and remote devices, and the current connection state. The output provides valuable insights into the network activity on the system, highlighting four specific connections currently active and listening on specific ports. These connections include the VNC remote desktop software, the Sun Remote Procedure Call service, the HTTP protocol for web traffic, and the SSH protocol for secure remote shell access. By knowing which ports are used by which services, users can quickly identify any network issues and troubleshoot accordingly. The most common network issues we will encounter during our penetration tests include the following:</p>
<ul>
<li>Network connectivity issues</li>
<li>DNS resolution issues (it's always DNS)</li>
<li>Packet loss</li>
<li>Network performance issues</li>
</ul>
<p>Each issue, along with common causes that may include misconfigured firewalls or routers, damaged network cables or connectors, incorrect network settings, hardware failure, incorrect DNS server settings, DNS server failure, misconfigured DNS records, network congestion, outdated network hardware, incorrectly configured network settings, unpatched software or firmware, and lack of proper security controls. Understanding these common network issues and their causes is important for effectively identifying and exploiting vulnerabilities in network systems during our testing.</p>
<hr>
<h2>Hardening</h2>
<p>Several mechanisms are highly effective in securing Linux systems in keeping our and other companies' data safe. Three such mechanisms are SELinux, AppArmor, and TCP wrappers. These tools are designed to safeguard Linux systems against various security threats, from unauthorized access to malicious attacks, especially while conducting a penetration test. There is almost no worse scenario than when a company is compromised due to a penetration test. By implementing these security measures and ensuring that we set up corresponding protection against potential attackers, we can significantly reduce the risk of data leaks and ensure our systems remain secure. While these tools share some similarities, they also have important differences.</p>
<p>SELinux is a MAC system that is built into the Linux kernel. It is designed to provide fine-grained access control over system resources and applications. SELinux works by enforcing a policy that defines the access controls for each process and file on the system. It provides a higher level of security by limiting the damage that a compromised process can do.</p>
<p>AppArmor is also a MAC system that provides a similar level of control over system resources and applications, but it works slightly differently. AppArmor is implemented as a Linux Security Module (LSM) and uses application profiles to define the resources that an application can access. AppArmor is typically easier to use and configure than SELinux but may not provide the same level of fine-grained control.</p>
<p>TCP wrappers are a host-based network access control mechanism that can be used to restrict access to network services based on the IP address of the client system. It works by intercepting incoming network requests and comparing the IP address of the client system to the access control rules. These are useful for limiting access to network services from unauthorized systems.</p>
<p>Regarding similarities, the three security mechanisms share the common goal of ensuring the safety and security of Linux systems. In addition to providing extra protection, they can restrict access to resources and services, thus reducing the risk of unauthorized access and data breaches. It's also worth noting that these mechanisms are readily available as part of most Linux distributions, making them accessible to us to enhance their systems' security. Furthermore, these mechanisms can be easily customized and configured using standard tools and utilities, making them a convenient choice for Linux users.</p>
<p>In terms of differences, SELinux and AppArmor are both MAC systems that provide fine-grained access control over system resources but work in different ways. SELinux is built into the kernel and is more complex to configure and use, while AppArmor is implemented as a module and is typically easier to use. On the other hand, TCP wrappers are a host-based network access control mechanism designed to restrict access to network services based on the IP address of the client system. It is a simpler mechanism than SELinux and AppArmor but is useful for limiting access to network services from unauthorized systems.</p>
<hr>
<h2>Setting Up</h2>
<p>As we navigate the world of Linux, we inevitably encounter a wide range of technologies, applications, and services that we need to become familiar with. This is a crucial skill, particularly if we work in cybersecurity and strive to improve our expertise continuously. For this reason, we highly recommend dedicating time to learning about configuring important security measures such as <code>SELinux</code>, <code>AppArmor</code>, and <code>TCP wrappers</code> on your own. By taking on this (optional but highly efficient) challenge, you'll deepen your understanding of these technologies, build up your problem-solving skills, and gain valuable experience that will serve you well in the future. We highly recommend to use a personal VM and make snapshots before making changes.</p>
<p>When it comes to implementing cybersecurity measures, there is no one-size-fits-all approach. It is important to consider the specific information you want to protect and the tools you will use to do so. However, you can practice and implement several optional tasks with others in the Discord channel to increase your knowledge and skills in this area. By taking advantage of the helpfulness of others and sharing your own expertise, you can deepen your understanding of cybersecurity and help others do the same. Remember, explaining concepts to others is essential to teaching and learning.</p>
<h4>SELinux</h4>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td>1.</td>
<td>Install SELinux on your VM.</td>
</tr>
<tr>
<td>2.</td>
<td>Configure SELinux to prevent a user from accessing a specific file.</td>
</tr>
<tr>
<td>3.</td>
<td>Configure SELinux to allow a single user to access a specific network service but deny access to all others.</td>
</tr>
<tr>
<td>4.</td>
<td>Configure SELinux to deny access to a specific user or group for a specific network service.</td>
</tr>
</tbody>
</table></div>
<h4>AppArmor</h4>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td>5.</td>
<td>Configure AppArmor to prevent a user from accessing a specific file.</td>
</tr>
<tr>
<td>6.</td>
<td>Configure AppArmor to allow a single user to access a specific network service but deny access to all others.</td>
</tr>
<tr>
<td>7.</td>
<td>Configure AppArmor to deny access to a specific user or group for a specific network service.</td>
</tr>
</tbody>
</table></div>
<h4>TCP Wrappers</h4>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td>8.</td>
<td>Configure TCP wrappers to allow access to a specific network service from a specific IP address.</td>
</tr>
<tr>
<td>9.</td>
<td>Configure TCP wrappers to deny access to a specific network service from a specific IP address.</td>
</tr>
<tr>
<td>10.</td>
<td>Configure TCP wrappers to allow access to a specific network service from a range of IP addresses.</td>
</tr>
</tbody>
</table></div>
<div id="screen" style="height: 600px; border: 1px solid;">
<div class="screenPlaceholder">
<div class="instanceLoading" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Instance is starting...</div>
</div>
<div class="instanceTerminating" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Terminating instance...</div>
</div>
<div class="row instanceStart max-width-canvas">
<div class="col-4"></div>
<div class="col-4">
<button class="startInstanceBtn btn btn-primary btn-lg btn-block " style="margin-top: 270px;">Start Instance
</button>
<p class="text-center mt-2 font-size-13 font-secondary">
<span class="text-success spawnsLeft">
0
</span> / 1 spawns left
</p>
</div>
<div class="col-4"></div>
</div>
 </div>
</div>
<div class="row align-center justify-center my-4">
<div class="col-5 justify-start">
<button style="display:none;" target="_blank" class="instance-button fullScreenBtn btn btn-light btn-sm float-left "><i class="fad fa-expand text-success mr-1"></i> &nbsp;Full Screen
</button>
<button style="display:none;" class="instance-button terminateInstanceBtn btn btn-light btn-sm ml-2"><i class="fad fa-times text-danger"></i> &nbsp;Terminate
</button>
<button style="display:none;" class="instance-button resetInstanceBtn btn btn-light btn-sm ml-1"><i class="fad fa-sync text-warning mr-2"></i> &nbsp;Reset
</button>
<div class="btn-group " role="group">
<button style="display:none;cursor: default;" class="instance-button extendInstanceBtn btn btn-light btn-sm ml-1">Life Left:
<span class="lifeLeft"></span>m
</button>
</div>
</div>
<div id="statusText" class="col-7 justify-end pt-2 pr-2 font-size-small text-right">Waiting to
start...
</div>
</div>
</div>

<div class="training-module">
<h1>Remote Desktop Protocols in Linux</h1>
<hr>
<p>Remote desktop protocols are used in Windows, Linux, and macOS to provide graphical remote access to a system. The administrators can utilize remote desktop protocols in many scenarios like troubleshooting, software or system upgrading, and remote systems administration. The administrator needs to connect to the remote system they will administer remotely, and therefore, they use the appropriate protocol accordingly. In addition, they can log in using different protocols if they want to install an application on their remote system. The most common protocols for this usage are RDP (Windows) and VNC (Linux).</p>
<hr>
<h2>XServer</h2>
<p>The XServer is the user-side part of the <code>X Window System network protocol</code> (<code>X11</code> / <code>X</code>). The <code>X11</code> is a fixed system that consists of a collection of protocols and applications that allow us to call application windows on displays in a graphical user interface. X11 is predominant on Unix systems, but X servers are also available for other operating systems. Nowadays, the XServer is a part of almost every desktop installation of Ubuntu and its derivatives and does not need to be installed separately.</p>
<p>When a desktop is started on a Linux computer, the communication of the graphical user interface with the operating system happens via an X server. The computer's internal network is used, even if the computer should not be in a network. The practical thing about the X protocol is network transparency. This protocol mainly uses TCP/IP as a transport base but can also be used on pure Unix sockets. The ports that are utilized for X server are typically located in the range of <code>TCP/6001-6009</code>, allowing communication between the client and server. When starting a new desktop session via X server the <code>TCP port 6000</code> would be opened for the first X display <code>:0</code>. This range of ports enables the server to perform its tasks such as hosting applications, as well as providing services to clients. They are often used to provide remote access to a system, allowing users to access applications and data from anywhere in the world. Additionally, these ports are also essential for the secure sharing of files and data, making them an integral part of the Open X Server. Thus an X server is not dependent on the local computer, it can be used to access other computers, and other computers can use the local X server. Provided that both local and remote computers contain Unix/Linux systems, additional protocols such as VNC and RDP are superfluous. VNC and RDP generate the graphical output on the remote computer and transport it over the network. Whereas with X11, it is rendered on the local computer. This saves traffic and a load on the remote computer. However, X11's significant disadvantage is the unencrypted data transmission. However, this can be overcome by tunneling the SSH protocol.</p>
<p>For this, we have to allow X11 forwarding in the SSH configuration file (<code>/etc/ssh/sshd_config</code>) on the server that provides the application by changing this option to <code>yes</code>.</p>
<h4>X11Forwarding</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">X11Forwarding</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">cat</span> /etc/ssh/sshd_config <span class="token operator">|</span> <span class="token function">grep</span> X11Forwarding</span></span>

<span class="token output">X11Forwarding yes
</span></code></pre></div></div>
<p>With this we can start the application from our client with the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">X11Forwarding</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">ssh</span> -X htb-student@10.129.23.11 /usr/bin/firefox</span></span>

<span class="token output">htb-student@10.129.14.130's password: ********
&lt;SKIP&gt;
</span></code></pre></div></div>
<p><img src="https://academy.hackthebox.com/storage/modules/18/xserver.png" alt="image"></p>
<h4>X11 Security</h4>
<p>X11 is not a secure protocol without suitable security measures since X11 communication is entirely unencrypted. A completely open X server lets anyone on the network read the contents of its windows, for example, and this goes unnoticed by the user sitting in front of it. Therefore, it is not even necessary to sniff the network. This standard X11 functionality is realized with simple X11 tools like <code>xwd</code> and <code>xgrabsc</code>. In short, as penetration testers, we could read users' keystrokes, obtain screenshots, move the mouse cursor and send keystrokes from the server over the network.</p>
<p>A good example is several security vulnerabilities found in XServer, where a local attacker can exploit vulnerabilities in XServer to execute arbitrary code with user privileges and gain user privileges. The operating systems affected by these vulnerabilities were UNIX and Linux, Red Hat Enterprise Linux, Ubuntu Linux, and SUSE Linux. These vulnerabilities are known as CVE-2017-2624, CVE-2017-2625, and CVE-2017-2626.</p>
<hr>
<h2>XDMCP</h2>
<p>The <code>X Display Manager Control Protocol</code> (<code>XDMCP</code>) protocol is used by the <code>X Display Manager</code> for communication through UDP port 177 between X terminals and computers operating under Unix/Linux. It is used to manage remote X Window sessions on other machines and is often used by Linux system administrators to provide access to remote desktops. XDMCP is an insecure protocol and should not be used in any environment that requires high levels of security. With this, it is possible to redirect an entire graphical user interface (<code>GUI</code>) (such as KDE or Gnome) to a corresponding client. For a Linux system to act as an XDMCP server, an X system with a GUI must be installed and configured on the server. After starting the computer, a graphical interface should be available locally to the user.</p>
<p>One potential way that XDMCP could be exploited is through a man-in-the-middle attack. In this type of attack, an attacker intercepts the communication between the remote computer and the X Window System server, and impersonates one of the parties in order to gain unauthorized access to the server. The attacker could then use the server to run arbitrary commands, access sensitive data, or perform other actions that could compromise the security of the system.</p>
<hr>
<h2>VNC</h2>
<p><code>Virtual Network Computing</code> (<code>VNC</code>) is a remote desktop sharing system based on the RFB protocol that allows users to control a computer remotely. It allows a user to view and interact with a desktop environment remotely over a network connection. The user can control the remote computer as if sitting in front of it. This is also one of the most common protocols for remote graphical connections for Linux hosts.</p>
<p>VNC is generally considered to be secure. It uses encryption to ensure the data is safe while in transit and requires authentication before a user can gain access. Administrators make use of VNC to access computers that are not physically accessible. This could be used to troubleshoot and maintain servers, access applications on other computers, or provide remote access to workstations. VNC can also be used for screen sharing, allowing multiple users to collaborate on a project or troubleshoot a problem.</p>
<p>There are two different concepts for VNC servers. The usual server offers the actual screen of the host computer for user support. Because the keyboard and mouse remain usable at the remote computer, an arrangement is recommended. The second group of server programs allows user login to virtual sessions, similar to the terminal server concept.</p>
<p>Server and viewer programs for VNC are available for all common operating systems. Therefore, many IT services are performed with VNC. The proprietary TeamViewer, and RDP have similar uses.</p>
<p>Traditionally, the VNC server listens on TCP port 5900. So it offers its <code>display 0</code> there. Other displays can be offered via additional ports, mostly <code>590[x]</code>, where <code>x</code> is the display number. Adding multiple connections would be assigned to a higher TCP port like 5901, 5902, 5903, etc.</p>
<p>For these VNC connections, many different tools are used. Among them are for example:</p>
<ul>
<li>
<a href="https://tigervnc.org/" target="_blank" rel="noopener nofollow">TigerVNC</a>
</li>
<li>
<a href="https://www.tightvnc.com/" target="_blank" rel="noopener nofollow">TightVNC</a>
</li>
<li>
<a href="https://www.realvnc.com/en/" target="_blank" rel="noopener nofollow">RealVNC</a>
</li>
<li>
<a href="https://uvnc.com/" target="_blank" rel="noopener nofollow">UltraVNC</a>
</li>
</ul>
<p>The most used tools for such kinds of connections are UltraVNC and RealVNC because of their encryption and higher security.</p>
<p>In this example, we set up a <code>TigerVNC</code> server, and for this, we need, among other things, also the <code>XFCE4</code> desktop manager since VNC connections with GNOME are somewhat unstable. Therefore we need to install the necessary packages and create a password for the VNC connection.</p>
<h4>TigerVNC Installation</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">TigerVNC Installation</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">htb-student@ubuntu</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt</span> <span class="token function">install</span> xfce4 xfce4-goodies tigervnc-standalone-server -y</span></span>
<span class="token info punctuation"><span class="token user">htb-student@ubuntu</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">vncpasswd </span></span>

<span class="token output">Password: ******
Verify: ******
Would you like to enter a view-only password (y/n)? n
</span></code></pre></div></div>
<p>During installation, a hidden folder is created in the home directory called <code>.vnc</code>. Then, we have to create two additional files, <code>xstartup</code> and <code>config</code>. The <code>xstartup</code> determines how the VNC session is created in connection with the display manager, and the <code>config</code> determines its settings.</p>
<h4>Configuration</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Configuration</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">htb-student@ubuntu</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">touch</span> ~/.vnc/xstartup ~/.vnc/config</span></span>
<span class="token info punctuation"><span class="token user">htb-student@ubuntu</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">cat</span> </span></span><span class="token output">&lt;&lt;EOT &gt;&gt; ~/.vnc/xstartup

</span><span class="token command"><span class="token shell-symbol important">#</span><span class="token bash language-bash"><span class="token operator">!</span>/bin/bash</span></span>
<span class="token output">unset SESSION_MANAGER
unset DBUS_SESSION_BUS_ADDRESS
/usr/bin/startxfce4
[ -x /etc/vnc/xstartup ] &amp;&amp; exec /etc/vnc/xstartup
</span><span class="token info punctuation">[ -r </span><span class="token command"><span class="token shell-symbol important">$</span><span class="token bash language-bash"><span class="token environment constant">HOME</span>/.Xresources <span class="token punctuation">]</span> <span class="token operator">&amp;&amp;</span> xrdb <span class="token environment constant">$HOME</span>/.Xresources</span></span>
<span class="token output">x-window-manager &amp;
EOT
</span></code></pre></div></div>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Configuration</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">htb-student@ubuntu</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">cat</span> </span></span><span class="token output">&lt;&lt;EOT &gt;&gt; ~/.vnc/config

geometry=1920x1080
dpi=96
EOT
</span></code></pre></div></div>
<p>Additionally, the <code>xstartup</code> executable needs rights to be started by the service.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Configuration</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">htb-student@ubuntu</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">chmod</span> +x ~/.vnc/xstartup</span></span>
</code></pre></div></div>
<p>Now we can start the VNC server.</p>
<h4>Start the VNC server</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Start the VNC server</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">htb-student@ubuntu</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">vncserver</span></span>

<span class="token output">New 'linux:1 (htb-student)' desktop at :1 on machine linux

Starting applications specified in /home/htb-student/.vnc/xstartup
Log file is /home/htb-student/.vnc/linux:1.log

Use xtigervncviewer -SecurityTypes VncAuth -passwd /home/htb-student/.vnc/passwd :1 to connect to the VNC server.
</span></code></pre></div></div>
<p>In addition, we can also display the entire sessions with the associated ports and the process ID.</p>
<h4>List Sessions</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">List Sessions</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token info punctuation"><span class="token user">htb-student@ubuntu</span><span class="token punctuation">:</span><span class="token path">~</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">vncserver -list</span></span>

<span class="token output">TigerVNC server sessions:

</span><span class="token info punctuation">X DISPLAY </span><span class="token command"><span class="token shell-symbol important">#</span>     <span class="token bash language-bash">RFB PORT <span class="token comment">#      PROCESS ID</span></span></span>
<span class="token output">:1              5901            79746
</span></code></pre></div></div>
<p>To encrypt the connection and make it more secure, we can create an SSH tunnel over which the whole connection is tunneled. How tunneling works in detail we will learn in the <a href="https://academy.hackthebox.com/module/details/158" target="_blank" rel="noopener nofollow">Pivoting, Tunneling, and Port Forwarding</a> module.</p>
<h4>Setting Up an SSH Tunnel</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Setting Up an SSH Tunnel</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">ssh</span> -L <span class="token number">5901</span>:127.0.0.1:5901 -N -f -l htb-student <span class="token number">10.129</span>.14.130</span></span>

<span class="token output">htb-student@10.129.14.130's password: *******
</span></code></pre></div></div>
<p>Finally, we can connect to the server through the SSH tunnel using the <code>xtightvncviewer</code>.</p>
<h4>Connecting to the VNC Server</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Connecting to the VNC Server</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">xtightvncviewer localhost:5901</span></span>

<span class="token output">Connected to RFB server, using protocol version 3.8
Performing standard VNC authentication

Password: ******

Authentication successful
Desktop name "linux:1 (htb-student)"
VNC server default format:
  32 bits per pixel.
  Least significant byte first in each pixel.
  True colour: max red 255 green 255 blue 255, shift red 16 green 8 blue 0
Using default colormap which is TrueColor.  Pixel format:
  32 bits per pixel.
  Least significant byte first in each pixel.
  True colour: max red 255 green 255 blue 255, shift red 16 green 8 blue 0
Same machine: preferring raw encoding
</span></code></pre></div></div>
<p><img src="https://academy.hackthebox.com/storage/modules/18/vncviewer.png" alt="image"></p>
</div>

<div class="training-module">
<h1>Linux Security</h1>
<hr>
<p>All computer systems have an inherent risk of intrusion. Some present more of a risk than others, such as an internet-facing web server hosting multiple complex web applications. Linux systems are also less prone to viruses that affect Windows operating systems and do not present as large an attack surface as Active Directory domain-joined hosts. Regardless, it is essential to have certain fundamentals in place to secure any Linux system.</p>
<p>One of the Linux operating systems' most important security measures is keeping the OS and installed packages up to date. This can be achieved with a command such as:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title"></span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">apt</span> update <span class="token operator">&amp;&amp;</span> <span class="token function">apt</span> dist-upgrade</span></span>
</code></pre></div></div>
<p>If firewall rules are not appropriately set at the network level, we can use the Linux firewall and/or <code>iptables</code> to restrict traffic into/out of the host.</p>
<p>If SSH is open on the server, the configuration should be set up to disallow password login and disallow the root user from logging in via SSH. It is also important to avoid logging into and administering the system as the root user whenever possible and adequately managing access control. Users' access should be determined based on the principle of least privilege. For example, if a user needs to run a command as root, then that command should be specified in the <code>sudoers</code> configuration instead of giving them full sudo rights. Another common protection mechanism that can be used is <code>fail2ban</code>. This tool counts the number of failed login attempts, and if a user has reached the maximum number, the host that tried to connect will be handled as configured.</p>
<p>It is also important to periodically audit the system to ensure that issues do not exist that could facilitate privilege escalation, such as an out-of-date kernel, user permission issues, world-writable files, and misconfigured cron jobs, or misconfigured services. Many administrators forget about the possibility that some kernel versions have to be updated manually.</p>
<p>An option for further locking down Linux systems is <code>Security-Enhanced Linux</code> (<code>SELinux</code>) or <code>AppArmor</code>. This is a kernel security module that can be used for security access control policies. In SELinux, every process, file, directory, and system object is given a label. Policy rules are created to control access between these labeled processes and objects and are enforced by the kernel. This means that access can be set up to control which users and applications can access which resources. SELinux provides very granular access controls, such as specifying who can append to a file or move it.</p>
<p>Besides, there are different applications and services such as <a href="https://www.snort.org/" target="_blank" rel="noopener nofollow">Snort</a>, <a href="http://www.chkrootkit.org/" target="_blank" rel="noopener nofollow">chkrootkit</a>, <a href="https://packages.debian.org/sid/rkhunter" target="_blank" rel="noopener nofollow">rkhunter</a>, <a href="https://cisofy.com/lynis/" target="_blank" rel="noopener nofollow">Lynis</a>, and others that can contribute to Linux's security. In addition, some security settings should be made, such as:</p>
<ul>
<li>Removing or disabling all unnecessary services and software</li>
<li>Removing all services that rely on unencrypted authentication mechanisms</li>
<li>Ensure NTP is enabled and Syslog is running</li>
<li>Ensure that each user has its own account</li>
<li>Enforce the use of strong passwords</li>
<li>Set up password aging and restrict the use of previous passwords</li>
<li>Locking user accounts after login failures</li>
<li>Disable all unwanted SUID/SGID binaries</li>
</ul>
<p>This list is incomplete, as safety is not a product but a process. This means that specific steps must always be taken to protect the systems better, and it depends on the administrators how well they know their operating systems. The better the administrators are familiar with the system, and the more they are trained, the better and more secure their security precautions and security measures will be.</p>
<hr>
<h2>TCP Wrappers</h2>
<p>TCP wrapper is a security mechanism used in Linux systems that allows the system administrator to control which services are allowed access to the system. It works by restricting access to certain services based on the hostname or IP address of the user requesting access. When a client attempts to connect to a service the system will first consult the rules defined in the TCP wrappers configuration files to determine the IP address of the client. If the IP address matches the criteria specified in the configuration files, the system will then grant the client access to the service. However, if the criteria are not met, the connection will be denied, providing an additional layer of security for the service. TCP wrappers use the following configuration files:</p>
<ul>
<li>
<p><code>/etc/hosts.allow</code></p>
</li>
<li>
<p><code>/etc/hosts.deny</code></p>
</li>
</ul>
<p>In short, the <code>/etc/hosts.allow</code> file specifies which services and hosts are allowed access to the system, whereas the <code>/etc/hosts.deny</code> file specifies which services and hosts are not allowed access. These files can be configured by adding specific rules to the files.</p>
<h4>/etc/hosts.allow</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">/etc/hosts.allow</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">cat</span> /etc/hosts.allow</span></span>

<span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">Allow access to SSH from the <span class="token builtin class-name">local</span> network</span></span>
<span class="token output">sshd : 10.129.14.0/24

</span><span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">Allow access to FTP from a specific <span class="token function">host</span></span></span>
<span class="token output">ftpd : 10.129.14.10

</span><span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">Allow access to Telnet from any <span class="token function">host</span> <span class="token keyword">in</span> the inlanefreight.local domain</span></span>
<span class="token output">telnetd : .inlanefreight.local
</span></code></pre></div></div>
<h4>/etc/hosts.deny</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">/etc/hosts.deny</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">cat</span> /etc/hosts.deny</span></span>

<span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">Deny access to all services from any <span class="token function">host</span> <span class="token keyword">in</span> the inlanefreight.com domain</span></span>
<span class="token output">ALL : .inlanefreight.com

</span><span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">Deny access to SSH from a specific <span class="token function">host</span></span></span>
<span class="token output">sshd : 10.129.22.22

</span><span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash">Deny access to FTP from hosts with IP addresses <span class="token keyword">in</span> the range of <span class="token number">10.129</span>.22.0 to <span class="token number">10.129</span>.22.255</span></span>
<span class="token output">ftpd : 10.129.22.0/24
</span></code></pre></div></div>
<p>It is important to remember that the order of the rules in the files is important. The first rule that matches the requested service and host is the one that will be applied. It is also important to note that TCP wrappers are not a replacement for a firewall, as they are limited by the fact that they can only control access to services and not to ports.</p>
</div>

<div class="training-module">
<h1>Firewall Setup</h1>
<hr>
<p>The primary goal of firewalls is to provide a security mechanism for controlling and monitoring network traffic between different network segments, such as internal and external networks or different network zones. Firewalls play a crucial role in protecting computer networks from unauthorized access, malicious traffic, and other security threats. Linux, being a popular operating system used in servers and other network devices, provides built-in firewall capabilities that can be used to control network traffic. In other words, they can filter incoming and outgoing traffic based on pre-defined rules, protocols, ports, and other criteria to prevent unauthorized access and mitigate security threats. The specific goal of a firewall implementation can vary depending on the specific needs of the organization, such as ensuring the confidentiality, integrity, and availability of network resources.</p>
<p>An example from the history of Linux firewalls is the development of the iptables tool, which replaced the earlier ipchains and ipfwadm tools. The iptables utility was first introduced in the Linux 2.4 kernel in 2000 and provided a flexible and efficient mechanism for filtering network traffic. iptables became the de facto standard firewall solution for Linux systems, and it has been widely adopted by many organizations and users.</p>
<p>The iptables utility provided a simple yet powerful command-line interface for configuring firewall rules, which could be used to filter traffic based on various criteria such as IP addresses, ports, protocols, and more. iptables was designed to be highly customizable and could be used to create complex firewall rulesets that could protect against various security threats such as denial-of-service (DoS) attacks, port scans, and network intrusion attempts.</p>
<p>In Linux, the firewall functionality is typically implemented using the Netfilter framework, which is an integral part of the kernel. Netfilter provides a set of hooks that can be used to intercept and modify network traffic as it passes through the system. The iptables utility is commonly used to configure the firewall rules on Linux systems.</p>
<hr>
<h2>Iptables</h2>
<p>The iptables utility provides a flexible set of rules for filtering network traffic based on various criteria such as source and destination IP addresses, port numbers, protocols, and more. There also exist other solutions like nftables, ufw, and firewalld. <code>Nftables</code> provides a more modern syntax and improved performance over iptables. However, the syntax of nftables rules is not compatible with iptables, so migration to nftables requires some effort. <code>UFW</code> stands for “Uncomplicated Firewall” and provides a simple and user-friendly interface for configuring firewall rules. UFW is built on top of the iptables framework like nftables and provides an easier way to manage firewall rules. Finally, FirewallD provides a dynamic and flexible firewall solution that can be used to manage complex firewall configurations, and it supports a rich set of rules for filtering network traffic and can be used to create custom firewall zones and services. It consists of several components that work together to provide a flexible and powerful firewall solution. The main components of iptables are:</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th><strong>Component</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Tables</code></td>
<td>Tables are used to organize and categorize firewall rules.</td>
</tr>
<tr>
<td><code>Chains</code></td>
<td>Chains are used to group a set of firewall rules applied to a specific type of network traffic.</td>
</tr>
<tr>
<td><code>Rules</code></td>
<td>Rules define the criteria for filtering network traffic and the actions to take for packets that match the criteria.</td>
</tr>
<tr>
<td><code>Matches</code></td>
<td>Matches are used to match specific criteria for filtering network traffic, such as source or destination IP addresses, ports, protocols, and more.</td>
</tr>
<tr>
<td><code>Targets</code></td>
<td>Targets specify the action for packets that match a specific rule. For example, targets can be used to accept, drop, or reject packets or modify the packets in another way.</td>
</tr>
</tbody>
</table></div>
<h4>Tables</h4>
<p>When working with firewalls on Linux systems, it is important to understand how tables work in iptables. Tables in iptables are used to categorize and organize firewall rules based on the type of traffic that they are designed to handle. These tables are used to organize and categorize firewall rules. Each table is responsible for performing a specific set of tasks.</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th><strong>Table Name</strong></th>
<th><strong>Description</strong></th>
<th><strong>Built-in Chains</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>filter</code></td>
<td>Used to filter network traffic based on IP addresses, ports, and protocols.</td>
<td>INPUT, OUTPUT, FORWARD</td>
</tr>
<tr>
<td><code>nat</code></td>
<td>Used to modify the source or destination IP addresses of network packets.</td>
<td>PREROUTING, POSTROUTING</td>
</tr>
<tr>
<td><code>mangle</code></td>
<td>Used to modify the header fields of network packets.</td>
<td>PREROUTING, OUTPUT, INPUT, FORWARD, POSTROUTING</td>
</tr>
</tbody>
</table></div>
<p>In addition to the built-in tables, iptables provides a fourth table called the raw table, which is used to configure special packet processing options. The raw table contains two built-in chains: PREROUTING and OUTPUT.</p>
<h4>Chains</h4>
<p>In iptables, chains organize rules that define how network traffic should be filtered or modified. There are two types of chains in iptables:</p>
<ul>
<li>Built-in chains</li>
<li>User-defined chains</li>
</ul>
<p>The built-in chains are pre-defined and automatically created when a table is created. Each table has a different set of built-in chains. For example, the filter table has three built-in chains:</p>
<ul>
<li>INPUT</li>
<li>OUTPUT</li>
<li>FORWARD</li>
</ul>
<p>These chains are used to filter incoming and outgoing network traffic, as well as traffic that is being forwarded between different network interfaces. The nat table has two built-in chains:</p>
<ul>
<li>PREROUTING</li>
<li>POSTROUTING</li>
</ul>
<p>The PREROUTING chain is used to modify the destination IP address of incoming packets before the routing table processes them. The POSTROUTING chain is used to modify the source IP address of outgoing packets after the routing table has processed them. The mangle table has five built-in chains:</p>
<ul>
<li>PREROUTING</li>
<li>OUTPUT</li>
<li>INPUT</li>
<li>FORWARD</li>
<li>POSTROUTING</li>
</ul>
<p>These chains are used to modify the header fields of incoming and outgoing packets and packets being processed by the corresponding chains.</p>
<p><code>User-defined chains</code> can simplify rule management by grouping firewall rules based on specific criteria, such as source IP address, destination port, or protocol. They can be added to any of the three main tables. For example, if an organization has multiple web servers that all require similar firewall rules, the rules for each server could be grouped in a user-defined chain. Another example is when a user-defined chain could filter traffic destined for a specific port, such as port 80 (HTTP). The user could then add rules to this chain that specifically filter traffic destined for port 80.</p>
<h4>Rules and Targets</h4>
<p>Iptables rules are used to define the criteria for filtering network traffic and the actions to take for packets that match the criteria. Rules are added to chains using the <code>-A</code> option followed by the chain name, and they can be modified or deleted using various other options.</p>
<p>Each rule consists of a set of criteria or matches and a target specifying the action for packets that match the criteria. The criteria or matches match specific fields in the IP header, such as the source or destination IP address, protocol, source, destination port number, and more. The target specifies the action for packets that match the criteria. They specify the action to take for packets that match a specific rule. For example, targets can accept, drop, reject, or modify the packets. Some of the common targets used in iptables rules include the following:</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th><strong>Target Name</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>ACCEPT</code></td>
<td>Allows the packet to pass through the firewall and continue to its destination</td>
</tr>
<tr>
<td><code>DROP</code></td>
<td>Drops the packet, effectively blocking it from passing through the firewall</td>
</tr>
<tr>
<td><code>REJECT</code></td>
<td>Drops the packet and sends an error message back to the source address, notifying them that the packet was blocked</td>
</tr>
<tr>
<td><code>LOG</code></td>
<td>Logs the packet information to the system log</td>
</tr>
<tr>
<td><code>SNAT</code></td>
<td>Modifies the source IP address of the packet, typically used for Network Address Translation (NAT) to translate private IP addresses to public IP addresses</td>
</tr>
<tr>
<td><code>DNAT</code></td>
<td>Modifies the destination IP address of the packet, typically used for NAT to forward traffic from one IP address to another</td>
</tr>
<tr>
<td><code>MASQUERADE</code></td>
<td>Similar to SNAT but used when the source IP address is not fixed, such as in a dynamic IP address scenario</td>
</tr>
<tr>
<td><code>REDIRECT</code></td>
<td>Redirects packets to another port or IP address</td>
</tr>
<tr>
<td><code>MARK</code></td>
<td>Adds or modifies the Netfilter mark value of the packet, which can be used for advanced routing or other purposes</td>
</tr>
</tbody>
</table></div>
<p>Let us illustrate a rule and consider that we want to add a new entry to the INPUT chain that allows incoming TCP traffic on port 22 (SSH) to be accepted. The command for that would look like the following:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Rules and Targets</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> iptables -A INPUT -p tcp --dport <span class="token number">22</span> -j ACCEPT</span></span>
</code></pre></div></div>
<h4>Matches</h4>
<p><code>Matches</code> are used to specify the criteria that determine whether a firewall rule should be applied to a particular packet or connection. Matches are used to match specific characteristics of network traffic, such as the source or destination IP address, protocol, port number, and more.</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th><strong>Match Name</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>-p</code> or <code>--protocol</code></td>
<td>Specifies the protocol to match (e.g. tcp, udp, icmp)</td>
</tr>
<tr>
<td><code>--dport</code></td>
<td>Specifies the destination port to match</td>
</tr>
<tr>
<td><code>--sport</code></td>
<td>Specifies the source port to match</td>
</tr>
<tr>
<td><code>-s</code> or <code>--source</code></td>
<td>Specifies the source IP address to match</td>
</tr>
<tr>
<td><code>-d</code> or <code>--destination</code></td>
<td>Specifies the destination IP address to match</td>
</tr>
<tr>
<td><code>-m state</code></td>
<td>Matches the state of a connection (e.g. NEW, ESTABLISHED, RELATED)</td>
</tr>
<tr>
<td><code>-m multiport</code></td>
<td>Matches multiple ports or port ranges</td>
</tr>
<tr>
<td><code>-m tcp</code></td>
<td>Matches TCP packets and includes additional TCP-specific options</td>
</tr>
<tr>
<td><code>-m udp</code></td>
<td>Matches UDP packets and includes additional UDP-specific options</td>
</tr>
<tr>
<td><code>-m string</code></td>
<td>Matches packets that contain a specific string</td>
</tr>
<tr>
<td><code>-m limit</code></td>
<td>Matches packets at a specified rate limit</td>
</tr>
<tr>
<td><code>-m conntrack</code></td>
<td>Matches packets based on their connection tracking information</td>
</tr>
<tr>
<td><code>-m mark</code></td>
<td>Matches packets based on their Netfilter mark value</td>
</tr>
<tr>
<td><code>-m mac</code></td>
<td>Matches packets based on their MAC address</td>
</tr>
<tr>
<td><code>-m iprange</code></td>
<td>Matches packets based on a range of IP addresses</td>
</tr>
</tbody>
</table></div>
<p>In general, matches are specified using the '-m' option in iptables. For example, the following command adds a rule to the 'INPUT' chain in the 'filter' table that matches incoming TCP traffic on port 80:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Matches</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> iptables -A INPUT -p tcp -m tcp --dport <span class="token number">80</span> -j ACCEPT</span></span>
</code></pre></div></div>
<p>This example rule matches incoming TCP traffic (<code>-p tcp</code>) on port 80 (<code>--dport 80</code>) and jumps to the accept target (<code>-j ACCEPT</code>) if the match is successful.</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th></th>
<th></th>
</tr>
</thead>
<tbody>
<tr>
<td>1.</td>
<td>Launch a web server on TCP/8080 port on your target and use iptables to block incoming traffic on that port.</td>
</tr>
<tr>
<td>2.</td>
<td>Change iptables rules to allow incoming traffic on the TCP/8080 port.</td>
</tr>
<tr>
<td>3.</td>
<td>Block traffic from a specific IP address.</td>
</tr>
<tr>
<td>4.</td>
<td>Allow traffic from a specific IP address.</td>
</tr>
<tr>
<td>5.</td>
<td>Block traffic based on protocol.</td>
</tr>
<tr>
<td>6.</td>
<td>Allow traffic based on protocol.</td>
</tr>
<tr>
<td>7.</td>
<td>Create a new chain.</td>
</tr>
<tr>
<td>8.</td>
<td>Forward traffic to a specific chain.</td>
</tr>
<tr>
<td>9.</td>
<td>Delete a specific rule.</td>
</tr>
<tr>
<td>10.</td>
<td>List all existing rules.</td>
</tr>
</tbody>
</table></div>
<div id="screen" style="height: 600px; border: 1px solid;">
<div class="screenPlaceholder">
<div class="instanceLoading" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Instance is starting...</div>
</div>
<div class="instanceTerminating" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Terminating instance...</div>
</div>
<div class="row instanceStart max-width-canvas">
<div class="col-4"></div>
<div class="col-4">
<button class="startInstanceBtn btn btn-primary btn-lg btn-block " style="margin-top: 270px;">Start Instance
</button>
<p class="text-center mt-2 font-size-13 font-secondary">
<span class="text-success spawnsLeft">
0
</span> / 1 spawns left
</p>
</div>
<div class="col-4"></div>
</div>
</div>
</div>
<div class="row align-center justify-center my-4">
<div class="col-5 justify-start">
<button style="display:none;" target="_blank" class="instance-button fullScreenBtn btn btn-light btn-sm float-left "><i class="fad fa-expand text-success mr-1"></i> &nbsp;Full Screen
</button>
<button style="display:none;" class="instance-button terminateInstanceBtn btn btn-light btn-sm ml-2"><i class="fad fa-times text-danger"></i> &nbsp;Terminate
</button>
<button style="display:none;" class="instance-button resetInstanceBtn btn btn-light btn-sm ml-1"><i class="fad fa-sync text-warning mr-2"></i> &nbsp;Reset
</button>
<div class="btn-group " role="group">
<button style="display:none;cursor: default;" class="instance-button extendInstanceBtn btn btn-light btn-sm ml-1">Life Left:
<span class="lifeLeft"></span>m
</button>
</div>
</div>
<div id="statusText" class="col-7 justify-end pt-2 pr-2 font-size-small text-right">Waiting to
start...
</div>
</div>
</div>

<div class="training-module">
<h1>System Logs</h1>
<hr>
<p>System logs on Linux are a set of files that contain information about the system and the activities taking place on it. These logs are important for monitoring and troubleshooting the system, as they can provide insights into system behavior, application activity, and security events. These system logs can be a valuable source of information for identifying potential security weaknesses and vulnerabilities within a Linux system as well. By analyzing the logs on our target systems, we can gain insights into the system's behavior, network activity, and user activity and can use this information to identify any abnormal activity, such as unauthorized logins, attempted attacks, clear text credentials, or unusual file access, which could indicate a potential security breach.</p>
<p>We, as penetration testers, can also use system logs to monitor the effectiveness of our security testing activities. By reviewing the logs after performing security testing, we can determine if our activities triggered any security events, such as intrusion detection alerts or system warnings. This information can help us refine our testing strategies and improve the overall security of the system.</p>
<p>In order to ensure the security of a Linux system, it is important to configure system logs properly. This includes setting the appropriate log levels, configuring log rotation to prevent log files from becoming too large, and ensuring that the logs are stored securely and protected from unauthorized access. In addition, it is important to regularly review and analyze the logs to identify potential security risks and respond to any security events in a timely manner. There are several different types of system logs on Linux, including:</p>
<ul>
<li>Kernel Logs</li>
<li>System Logs</li>
<li>Authentication Logs</li>
<li>Application Logs</li>
<li>Security Logs</li>
</ul>
<h4>Kernel logs</h4>
<p>These logs contain information about the system's kernel, including hardware drivers, system calls, and kernel events. They are stored in the <code>/var/log/kern.log</code> file. For example, kernel logs can reveal the presence of vulnerable or outdated drivers that could be targeted by attackers to gain access to the system. They can also provide insights into system crashes, resource limitations, and other events that could lead to a denial of service or other security issues. In addition, kernel logs can help us identify suspicious system calls or other activities that could indicate the presence of malware or other malicious software on the system. By monitoring the <code>/var/log/kern.log</code> file, we can detect any unusual behavior and take appropriate action to prevent further damage to the system.</p>
<h4>System logs</h4>
<p>These logs contain information about system-level events, such as service starts and stops, login attempts, and system reboots. They are stored in the <code>/var/log/syslog</code> file. By analyzing login attempts, service starts and stops, and other system-level events, we can detect any possible access or activities on the system. This can help us identify any vulnerabilities that could be exploited and help us recommend security measures to mitigate these risks. In addition, we can use the <code>syslog</code> to identify potential issues that could impact the availability or performance of the system, such as failed service starts or system reboots. Here is an example of how such <code>syslog</code> file could look like:</p>
<h4>Syslog</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Syslog</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output">Feb 28 2023 15:00:01 server CRON[2715]: (root) CMD (/usr/local/bin/backup.sh)
Feb 28 2023 15:04:22 server sshd[3010]: Failed password for htb-student from 10.14.15.2 port 50223 ssh2
Feb 28 2023 15:05:02 server kernel: [  138.303596] ata3.00: exception Emask 0x0 SAct 0x0 SErr 0x0 action 0x6 frozen
Feb 28 2023 15:06:43 server apache2[2904]: 127.0.0.1 - - [28/Feb/2023:15:06:43 +0000] "GET /index.html HTTP/1.1" 200 13484 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/80.0.3987.149 Safari/537.36"
Feb 28 2023 15:07:19 server sshd[3010]: Accepted password for htb-student from 10.14.15.2 port 50223 ssh2
Feb 28 2023 15:09:54 server kernel: [  367.543975] EXT4-fs (sda1): re-mounted. Opts: errors=remount-ro
Feb 28 2023 15:12:07 server systemd[1]: Started Clean PHP session files.
</span></code></pre></div></div>
<h4>Authentication logs</h4>
<p>These logs contain information about user authentication attempts, including successful and failed attempts. They are stored in the <code>/var/log/auth.log</code> file. It is important to note that while the <code>/var/log/syslog</code> file may contain similar login information, the <code>/var/log/auth.log</code> file specifically focuses on user authentication attempts, making it a more valuable resource for identifying potential security threats. Therefore, it is essential for penetration testers to review the logs stored in the <code>/var/log/auth.log</code> file to ensure that the system is secure and has not been compromised.</p>
<h4>Auth.log</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Auth.log</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output">Feb 28 2023 18:15:01 sshd[5678]: Accepted publickey for admin from 10.14.15.2 port 43210 ssh2: RSA SHA256:+KjEzN2cVhIW/5uJpVX9n5OB5zVJ92FtCZxVzzcKjw
Feb 28 2023 18:15:03 sudo:   admin : TTY=pts/1 ; PWD=/home/admin ; USER=root ; COMMAND=/bin/bash
Feb 28 2023 18:15:05 sudo:   admin : TTY=pts/1 ; PWD=/home/admin ; USER=root ; COMMAND=/usr/bin/apt-get install netcat-traditional
Feb 28 2023 18:15:08 sshd[5678]: Disconnected from 10.14.15.2 port 43210 [preauth]
Feb 28 2023 18:15:12 kernel: [  778.941871] firewall: unexpected traffic allowed on port 22
Feb 28 2023 18:15:15 auditd[9876]: Audit daemon started successfully
Feb 28 2023 18:15:18 systemd-logind[1234]: New session 4321 of user admin.
Feb 28 2023 18:15:21 CRON[2345]: pam_unix(cron:session): session opened for user root by (uid=0)
Feb 28 2023 18:15:24 CRON[2345]: pam_unix(cron:session): session closed for user root
</span></code></pre></div></div>
<p>In this example, we can see in the first line that a successful public key has been used for authentication for the user <code>admin</code>. Additionally, we can see that this user is in the <code>sudoers</code> group because he can execute commands using <code>sudo</code>. The kernel message indicates that unexpected traffic was allowed on port 22, which could indicate a potential security breach. After that, we see that a new session was created for user "admin" by <code>systemd-logind</code> and that a <code>cron</code> session opened and closed for the user <code>root</code>.</p>
<h4>Application logs</h4>
<p>These logs contain information about the activities of specific applications running on the system. They are often stored in their own files, such as <code>/var/log/apache2/error.log</code> for the Apache web server or <code>/var/log/mysql/error.log</code> for the MySQL database server. These logs are particularly important when we are targeting specific applications, such as web servers or databases, as they can provide insights into how these applications are processing and handling data. By examining these logs, we can identify potential vulnerabilities or misconfigurations. For example, access logs can be used to track requests made to a web server, while audit logs can be used to track changes made to the system or to specific files. These logs can be used to identify unauthorized access attempts, data exfiltration, or other suspicious activity.</p>
<p>Besides, access and audit logs are critical logs that record information about the actions of users and processes on the system. They are crucial for security and compliance purposes, and we can use them to identify potential security issues and attack vectors.</p>
<p>For example, <code>access logs</code> keep a record of user and process activity on the system, including login attempts, file accesses, and network connections. <code>Audit logs</code> record information about security-relevant events on the system, such as modifications to system configuration files or attempts to modify system files or settings. These logs help track potential attacks and activities or identify security breaches or other issues. An example entry in an access log file can look like the following:</p>
<h4>Access Log Entry</h4>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Access Log Entry</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output">2023-03-07T10:15:23+00:00 servername privileged.sh: htb-student accessed /root/hidden/api-keys.txt
</span></code></pre></div></div>
<p>In this log entry, we can see that the user <code>htb-student</code> used the <code>privileged.sh</code> script to access the <code>api-keys.txt</code> file in the <code>/root/hidden/</code> directory. On Linux systems, most common services have default locations for access logs:</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th><strong>Service</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>Apache</code></td>
<td>Access logs are stored in the /var/log/apache2/access.log file (or similar, depending on the distribution).</td>
</tr>
<tr>
<td><code>Nginx</code></td>
<td>Access logs are stored in the /var/log/nginx/access.log file (or similar).</td>
</tr>
<tr>
<td><code>OpenSSH</code></td>
<td>Access logs are stored in the /var/log/auth.log file on Ubuntu and in /var/log/secure on CentOS/RHEL.</td>
</tr>
<tr>
<td><code>MySQL</code></td>
<td>Access logs are stored in the /var/log/mysql/mysql.log file.</td>
</tr>
<tr>
<td><code>PostgreSQL</code></td>
<td>Access logs are stored in the /var/log/postgresql/postgresql-version-main.log file.</td>
</tr>
<tr>
<td><code>Systemd</code></td>
<td>Access logs are stored in the /var/log/journal/ directory.</td>
</tr>
</tbody>
</table></div>
<h4>Security logs</h4>
<p>These security logs and their events are often recorded in a variety of log files, depending on the specific security application or tool in use. For example, the Fail2ban application records failed login attempts in the <code>/var/log/fail2ban.log</code> file, while the UFW firewall records activity in the <code>/var/log/ufw.log</code> file. Other security-related events, such as changes to system files or settings, may be recorded in more general system logs such as <code>/var/log/syslog</code> or <code>/var/log/auth.log</code>. As penetration testers, we can use log analysis tools and techniques to search for specific events or patterns of activity that may indicate a security issue and use that information to further test the system for vulnerabilities or potential attack vectors.</p>
<p>It is important to be familiar with the default locations for access logs and other log files on Linux systems, as this information can be useful when performing a security assessment or penetration test. By understanding how security-related events are recorded and stored, we can more effectively analyze log data and identify potential security issues.</p>
<p>All these logs can be accessed and analyzed using a variety of tools, including the log file viewers built into most Linux desktop environments, as well as command-line tools such as the <code>tail</code>, <code>grep</code>, and <code>sed</code> commands. Proper analysis of system logs can help identify and troubleshoot system issues, as well as detect security breaches and other events of interest.</p>
<div id="screen" style="height: 600px; border: 1px solid;">
<div class="screenPlaceholder">
<div class="instanceLoading" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Instance is starting...</div>
</div>
<div class="instanceTerminating" style="display: none;">
<h1 class="text-center" style="margin-top: 270px;"><i class="fa fa-circle-notch fa-spin"></i></h1>
<div class="text-center">Terminating instance...</div>
</div>
<div class="row instanceStart max-width-canvas">
<div class="col-4"></div>
<div class="col-4">
<button class="startInstanceBtn btn btn-primary btn-lg btn-block " style="margin-top: 270px;">Start Instance
</button>
<p class="text-center mt-2 font-size-13 font-secondary">
<span class="text-success spawnsLeft">
0
</span> / 1 spawns left
</p>
</div>
<div class="col-4"></div>
</div>
</div>
</div>
<div class="row align-center justify-center my-4">
<div class="col-5 justify-start">
<button style="display:none;" target="_blank" class="instance-button fullScreenBtn btn btn-light btn-sm float-left "><i class="fad fa-expand text-success mr-1"></i> &nbsp;Full Screen
</button>
<button style="display:none;" class="instance-button terminateInstanceBtn btn btn-light btn-sm ml-2"><i class="fad fa-times text-danger"></i> &nbsp;Terminate
</button>
<button style="display:none;" class="instance-button resetInstanceBtn btn btn-light btn-sm ml-1"><i class="fad fa-sync text-warning mr-2"></i> &nbsp;Reset
</button>
<div class="btn-group " role="group">
<button style="display:none;cursor: default;" class="instance-button extendInstanceBtn btn btn-light btn-sm ml-1">Life Left:
<span class="lifeLeft"></span>m
</button>
</div>
</div>
<div id="statusText" class="col-7 justify-end pt-2 pr-2 font-size-small text-right">Waiting to
start...
</div>
</div>
</div>

<div class="training-module">
<h1>Solaris</h1>
<hr>
<p>Solaris is a Unix-based operating system developed by Sun Microsystems (later acquired by Oracle Corporation) in the 1990s. It is known for its robustness, scalability, and support for high-end hardware and software systems. Solaris is widely used in enterprise environments for mission-critical applications, such as database management, cloud computing, and virtualization. For example, it includes a built-in hypervisor called <code>Oracle VM Server for SPARC</code>, which allows multiple virtual machines to run on a single physical server. Overall, it is designed to handle large amounts of data and provide reliable and secure services to users and is often used in enterprise environments where security, performance, and stability are key requirements.</p>
<p>The goal of Solaris is to provide a highly stable, secure, and scalable platform for enterprise computing. It has built-in features for high availability, fault tolerance, and system management, making it ideal for mission-critical applications. It is widely used in the banking, finance, and government sectors, where security, reliability, and performance are paramount. It is also used in large-scale data centers, cloud computing environments, and virtualization platforms. Companies such as Amazon, IBM, and Dell use Solaris in their products and services, highlighting its importance in the industry.</p>
<hr>
<h2>Linux Distributions vs Solaris</h2>
<p>One of the main differences between Solaris and Linux distributions is that Solaris is a proprietary operating system. This means that it is developed and owned by Oracle Corporation, and its source code is not available to the general public. In contrast, most Linux distributions are open-source and have their source code available for anyone to modify and use and the use of the Zettabyte File System (<code>ZFS</code>) file system. ZFS is a highly advanced file system that provides features such as data compression, snapshots, and high scalability. Another key difference is the use of a Service Management Facility (<code>SMF</code>) in Solaris, which is a highly advanced service management framework that provides better reliability and availability for system services.</p>
<div class="table-responsive"><table class="table table-striped text-left">
<thead>
<tr>
<th><strong>Directory</strong></th>
<th><strong>Description</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><code>/</code></td>
<td>The root directory contains all other directories and files in the file system.</td>
</tr>
<tr>
<td><code>/bin</code></td>
<td>It contains essential system binaries that are required for booting and basic system operations.</td>
</tr>
<tr>
<td><code>/boot</code></td>
<td>The boot directory contains boot-related files such as boot loader and kernel images.</td>
</tr>
<tr>
<td><code>/dev</code></td>
<td>The dev directory contains device files that represent physical and logical devices attached to the system.</td>
</tr>
<tr>
<td><code>/etc</code></td>
<td>The etc directory contains system configuration files, such as system startup scripts and user authentication data.</td>
</tr>
<tr>
<td><code>/home</code></td>
<td>Users’ home directories.</td>
</tr>
<tr>
<td><code>/kernel</code></td>
<td>This directory contains kernel modules and other kernel-related files.</td>
</tr>
<tr>
<td><code>/lib</code></td>
<td>Directory for libraries required by the binaries in /bin and /sbin directories.</td>
</tr>
<tr>
<td><code>/lost+found</code></td>
<td>This directory is used by the file system consistency check and repair tool to store recovered files.</td>
</tr>
<tr>
<td><code>/mnt</code></td>
<td>Directory for mounting file systems temporarily.</td>
</tr>
<tr>
<td><code>/opt</code></td>
<td>This directory contains optional software packages that are installed on the system.</td>
</tr>
<tr>
<td><code>/proc</code></td>
<td>The proc directory provides a view into the system's process and kernel status as files.</td>
</tr>
<tr>
<td><code>/sbin</code></td>
<td>This directory contains system binaries required for system administration tasks.</td>
</tr>
<tr>
<td><code>/tmp</code></td>
<td>Temporary files created by the system and applications are stored in this directory.</td>
</tr>
<tr>
<td><code>/usr</code></td>
<td>The usr directory contains system-wide read-only data and programs, such as documentation, libraries, and executables.</td>
</tr>
<tr>
<td><code>/var</code></td>
<td>This directory contains variable data files, such as system logs, mail spools, and printer spools.</td>
</tr>
</tbody>
</table></div>
<p>Solaris has a number of unique features that set it apart from other operating systems. One of its key strengths is its support for high-end hardware and software systems. It is designed to work with large-scale data centers and complex network infrastructures, and it can handle large amounts of data without any performance issues.</p>
<p>In terms of package management, Solaris uses the Image Packaging System (<code>IPS</code>) package manager, which provides a powerful and flexible way to manage packages and updates. Solaris also provides advanced security features, such as Role-Based Access Control (<code>RBAC</code>) and mandatory access controls, which are not available in all Linux distributions.</p>
<hr>
<h2>Differences</h2>
<p>Let's dive deeper into the differences between Solaris and Linux distributions. One of the most important differences is that the source code is not open source and is only known in closed circles. This means that unlike Ubuntu or many other distributions, the source code cannot be viewed and analyzed by the public. In summary, the main differences can be grouped into the following categories:</p>
<ul>
<li>Filesystem</li>
<li>Process management</li>
<li>Package management</li>
<li>Kernel and Hardware support</li>
<li>System monitoring</li>
<li>Security</li>
</ul>
<p>To better understand the differences, let's take a look at a few examples and commands.</p>
<h4>System Information</h4>
<p>On Ubuntu, we use the <code>uname</code> command to display information about the system, such as the kernel name, hostname, and operating system. This might look like this:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">System Information</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">uname</span> -a</span></span>

<span class="token info punctuation">Linux ubuntu 5.4.0-1045 </span><span class="token command"><span class="token shell-symbol important">#</span><span class="token bash language-bash"><span class="token number">48</span>-Ubuntu SMP Fri Jan <span class="token number">15</span> <span class="token number">10</span>:47:29 UTC <span class="token number">2021</span> x86_64 x86_64 x86_64 GNU/Linux</span></span>
</code></pre></div></div>
<p>On the other hand, in Solaris, the <code>showrev</code> command can be used to display system information, including the version of Solaris, hardware type, and patch level. Here is an example output:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">System Information</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">showrev -a</span></span>

<span class="token output">Hostname: solaris
Kernel architecture: sun4u
OS version: Solaris 10 8/07 s10s_u4wos_12b SPARC
Application architecture: sparc
Hardware provider: Sun_Microsystems
Domain: sun.com
Kernel version: SunOS 5.10 Generic_139555-08
</span></code></pre></div></div>
<p>The main difference between the two commands is that <code>showrev</code> provides more detailed information about the Solaris system, such as the patch level and hardware provider, while <code>uname</code> only provides basic information about the Linux system.</p>
<h4>Installing Packages</h4>
<p>On Ubuntu, the <code>apt-get</code> command is used to install packages. This could look like the following:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Installing Packages</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">apt-get</span> <span class="token function">install</span> apache2</span></span>
</code></pre></div></div>
<p>However, in Solaris, we need to use <code>pkgadd</code> to install packages like <code>SUNWapchr</code>.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Installing Packages</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">pkgadd -d SUNWapchr</span></span>
</code></pre></div></div>
<p>The main difference between the two commands is the syntax, and the package manager used. Ubuntu uses the Advanced Packaging Tool (APT) to manage packages, while Solaris uses the Solaris Package Manager (SPM). Also, note that we do not use <code>sudo</code> in this case. This is because Solaris used the <code>RBAC</code> privilege management tool, which allowed the assignment of granular permissions to users. However, <code>sudo</code> has been supported since Solaris 11.</p>
<h4>Permission Management</h4>
<p>On Linux systems like Ubuntu but also on Solaris, the <code>chmod</code> command is used to change the permissions of files and directories. Here is an example command to give read, write, and execute permissions to the owner of the file:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Permission Management</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">chmod</span> <span class="token number">700</span> filename</span></span>
</code></pre></div></div>
<p>To find files with specific permissions in Ubuntu, we use the <code>find</code> command. Let us take a look at an example of a file with the SUID bit set:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Permission Management</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">find</span> / -perm <span class="token number">4000</span></span></span>
</code></pre></div></div>
<p>To find files with specific permissions, like with the SUID bit set on Solaris, we can use the find command, too, but with a small adjustment.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Permission Management</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">find</span> / -perm -4000</span></span>
</code></pre></div></div>
<p>The main difference between these two commands is the use of the <code>-</code> before the permission value in the Solaris command. This is because Solaris uses a different permission system than Linux.</p>
<h4>NFS in Solaris</h4>
<p>Solaris has its own implementation of NFS, which is slightly different from Linux distributions like Ubuntu. In Solaris, the NFS server can be configured using the <code>share</code> command, which is used to share a directory over the network, and it also allows us to specify various options such as read/write permissions, access restrictions, and more. To share a directory over NFS in Solaris, we can use the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">NFS in Solaris</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">share -F nfs -o rw /export/home</span></span>
</code></pre></div></div>
<p>This command shares the <code>/export/home</code> directory with read and writes permissions over NFS. An NFS client can mount the NFS file system using the <code>mount</code> command, the same way as with Ubuntu. To mount an NFS file system in Solaris, we need to specify the server name and the path to the shared directory. For example, to mount an NFS share from a server with the IP address <code>10.129.15.122</code> and the shared directory <code>/nfs_share</code>, we use the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">NFS in Solaris</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">mount</span> -F nfs <span class="token number">10.129</span>.15.122:/nfs_share /mnt/local</span></span>
</code></pre></div></div>
<p>In Solaris, the configuration for NFS is stored in the <code>/etc/dfs/dfstab</code> file. This file contains entries for each shared directory, along with the various options for NFS sharing.</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">NFS in Solaris</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token command"><span class="token shell-symbol important">#</span> <span class="token bash language-bash"><span class="token function">cat</span> /etc/dfs/dfstab</span></span>

<span class="token output">share -F nfs -o rw /export/home
</span></code></pre></div></div>
<h4>Process Mapping</h4>
<p>Process mapping is an essential aspect of system administration and troubleshooting. The <code>lsof</code> command is a powerful utility that lists all the files opened by a process, including network sockets and other file descriptors that we can use in Debian distributions like Ubuntu. We can use <code>lsof</code> to list all the files opened by a process. For example, to list all the files opened by the Apache web server process, we can use the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Process Mapping</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">lsof</span> -c apache2</span></span>
</code></pre></div></div>
<p>In Solaris, the <code>pfiles</code> command can be used to list all the files opened by a process. For example, to list all the files opened by the Apache web server process, we can use the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Process Mapping</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">pfiles <span class="token variable"><span class="token variable">`</span>pgrep httpd<span class="token variable">`</span></span></span></span>
</code></pre></div></div>
<p>This command lists all the files opened by the Apache web server process. The output of the <code>pfiles</code> command is similar to the output of the <code>lsof</code> command and provides information about the type of file descriptor, the file descriptor number, and the file name.</p>
<h4>Executable Access</h4>
<p>In Solaris, <code>truss</code> is used, which is a highly useful utility for developers and system administrators who need to debug complex software issues on the Solaris operating system. By tracing the system calls made by a process, <code>truss</code> can help identify the source of errors, performance issues, and other problems but can also reveal some sensitive information that may arise during application development or system maintenance. The utility can also provide detailed information about system calls, including the arguments passed to them and their return values, allowing users to better understand the behavior of their applications and the underlying operating system.</p>
<p><code>Strace</code> is an alternative to <code>truss</code> but for Ubuntu, and it is an essential tool for system administrators and developers alike, helping them diagnose and troubleshoot issues in real-time. It enables users to analyze the interactions between the operating system and applications running on it, which is especially useful in highly complex and mission-critical environments. With <code>truss</code>, users can quickly identify and isolate issues related to application performance, network connectivity, and system resource utilization, among others.</p>
<p>For example, to trace the system calls made by the Apache web server process, we can use the following command:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Executable Access</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token output"><span class="text-gray">Anna-19@htb</span><span class="text-success">[/htb]</span></span><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash"><span class="token function">sudo</span> <span class="token function">strace</span> -p <span class="token variable"><span class="token variable">`</span>pgrep apache2<span class="token variable">`</span></span></span></span>
</code></pre></div></div>
<p>Here's an example of how to use <code>truss</code> to trace the system calls made by the <code>ls</code> command in Solaris:</p>
<div class="window_container"><div class="window_content">
                <div class="window_top">
                    <span class="window_dot bg-danger"></span>
                    <span class="window_dot bg-warning"></span>
                    <span class="window_dot bg-success"></span>
                    <span class="window_title">Executable Access</span>
                </div>
            <pre class=" language-shell-session" style="line-height: 0px;"><code class=" language-shell-session"><span class="token command"><span class="token shell-symbol important">$</span> <span class="token bash language-bash">truss <span class="token function">ls</span></span></span>

<span class="token output">execve("/usr/bin/ls", 0xFFBFFDC4, 0xFFBFFDC8)  argc = 1
...SNIP...
</span></code></pre></div></div>
<p>The output is similar to <code>strace</code>, but the format is slightly different. One difference between <code>strace</code> and <code>truss</code> is that <code>truss</code> can also trace the signals sent to a process, while <code>strace</code> cannot. Another difference is that <code>truss</code> has the ability to trace the system calls made by child processes, while <code>strace</code> can only trace the system calls made by the process specified on the command line.</p>
</div>

<div class="training-module">
<h1>Shortcuts</h1>
<hr>
<p>There are many shortcuts that we can use to make working with Linux easier and faster. After we have familiarized ourselves with the most important of them and have made them a habit, we will save ourselves much typing. Some of them will even help us to avoid using our mouse in the terminal.</p>
<hr>
<h4>Auto-Complete</h4>
<p><code>[TAB]</code> - Initiates auto-complete. This will suggest to us different options based on the <code>STDIN</code> we provide. These can be specific suggestions like directories in our current working environment, commands starting with the same number of characters we already typed, or options.</p>
<hr>
<h4>Cursor Movement</h4>
<p><code>[CTRL] + A</code> - Move the cursor to the <code>beginning</code> of the current line.</p>
<p><code>[CTRL] + E</code> - Move the cursor to the <code>end</code> of the current line.</p>
<p><code>[CTRL] + [←]</code> / <code>[→]</code> - Jump at the beginning of the current/previous word.</p>
<p><code>[ALT] + B</code> / <code>F</code> - Jump backward/forward one word.</p>
<hr>
<h4>Erase The Current Line</h4>
<p><code>[CTRL] + U</code> - Erase everything from the current position of the cursor to the <code>beginning</code> of the line.</p>
<p><code>[Ctrl] + K</code> - Erase everything from the current position of the cursor to the <code>end</code> of the line.</p>
<p><code>[Ctrl] + W</code> - Erase the word preceding the cursor position.</p>
<hr>
<h4>Paste Erased Contents</h4>
<p><code>[Ctrl] + Y</code> - Pastes the erased text or word.</p>
<hr>
<h4>Ends Task</h4>
<p><code>[CTRL] + C</code> - Ends the current task/process by sending the <code>SIGINT</code> signal. For example, this can be a scan that is running by a tool. If we are watching the scan, we can stop it / kill this process by using this shortcut. While not configured and developed by the tool we are using. The process will be killed without asking us for confirmation.</p>
<hr>
<h4>End-of-File (EOF)</h4>
<p><code>[CTRL] + D</code> - Close <code>STDIN</code> pipe that is also known as End-of-File (EOF) or End-of-Transmission.</p>
<hr>
<h4>Clear Terminal</h4>
<p><code>[CTRL] + L</code> - Clears the terminal. An alternative to this shortcut is the <code>clear</code> command you can type to clear our terminal.</p>
<hr>
<h4>Background a Process</h4>
<p><code>[CTRL] + Z</code> - Suspend the current process by sending the <code>SIGTSTP</code> signal.</p>
<hr>
<h4>Search Through Command History</h4>
<p><code>[CTRL] + R</code> - Search through command history for commands we typed previously that match our search patterns.</p>
<p><code>[↑]</code> / <code>[↓]</code> - Go to the previous/next command in the command history.</p>
<hr>
<h4>Switch Between Applications</h4>
<p><code>[ALT] + [TAB]</code> - Switch between opened applications.</p>
<hr>
<h4>Zoom</h4>
<p><code>[CTRL] + [+]</code> - Zoom in.</p>
<p><code>[CTRL] + [-]</code> - Zoom out.</p>
</div>