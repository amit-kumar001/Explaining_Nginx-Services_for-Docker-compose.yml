# Explaining_Nginx-Services_for-Docker-compose.yml
### Nginx
<ol>
Create an app.conf file with the service configuration in the ~/project_directory/nginx/conf.d/ folder.</br>

<li><strong>server:</strong> block defines the configuration for the Nginx web server with the following directives:  </li>
<strong>server { </strong>
 
<li><strong>listen:</strong> This directive defines the port on which the server will listen to incoming requests.</li>
<strong>
    listen 80;</br>
    index index.php index.html;</strong>

<li><strong>error_log and access_log:</strong> These directives define the files for writing logs.</li>
<strong>
    error_log  /var/log/nginx/error.log;</br>
    access_log /var/log/nginx/access.log;</strong>

<li><strong>root:</strong> This directive sets the root folder path, forming the complete path to any requested file on the local file system.</li>

    <strong>root /var/www/public;</strong></br>


<li>In PHP location block, the fastcgi_pass instruct that the app service listening on a TCP socket on port 9000.</br>
FastCGI proxying within Nginx is generally used to translate client requests for an application server that does not or should not handle client requests directly. FastCGI is a protocol based on the earlier CGI, or common gateway interface, protocol meant to improve performance by not running each request as a separate process.</br>
In general, proxying requests involves the proxy server, in this case Nginx, forwarding requests from clients to a backend server. The directive that Nginx uses to define the actual server to proxy to using the FastCGI protocol is fastcgi_pass.</br>
This makes the PHP-FPM server listen over the network rather than on a Unix socket. Though a Unix socket has a slight advantage in speed over a TCP socket, it does not have a network protocol and thus skips the network stack. </br>
TCP socket offers the advantage of allowing you to connect to distributed services. </li>


```
    location ~ \.php$ {
        try_files $uri =404; common tricks to overcome a particular script injection exploit by ensuring the PHP file is a real file before sending the URL to the upstream interpreter.
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }

    location / {
        try_files $uri $uri/ /index.php?$query_string;
        gzip_static on;
    }
}

```
</br>
any changes you make inside the nginx/conf.d/ folder will be directly reflected inside the webserver container.

</ol>

