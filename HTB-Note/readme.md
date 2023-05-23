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