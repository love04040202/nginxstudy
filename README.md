# nginxstudy
利用Nginx访问、下载本机目录文件
  使用Nginx时，如果要让一些附件比如 txt,pdf,doc等不直接在浏览器打开，而弹出另存为的对话框（也就是下载）
  则可以在nginx的加上头配置如下：
  windows 官方文档 http://nginx.org/en/docs/windows.html
  `  
              #user  nobody;
              worker_processes  1;



              events {
                  worker_connections  1024;
              }


              http {
                  include       mime.types;
                  default_type  application/octet-stream;
                  sendfile        on;
                  keepalive_timeout  65;
                  gzip  on;

                  server {
                      listen       8090;
                      server_name  localhost;
                      charset utf8;
                  location /tools/ {
                          alias   D:/;
                          allow all;
                    #root D:/;
                          autoindex on;
                    autoindex_exact_size off;
                    autoindex_localtime on;
                    #add_header Content-Disposition: 'attachment;';
                      }

                      error_page   500 502 503 504  /50x.html;
                      location = /50x.html {
                          root   html;
                      }


                  }
              }

  `
 #Nginx的alias的用法及与root的区别

  http://nginx.org/en/docs/http/ngx_http_core_module.html#alias 
  http://nginx.org/en/docs/http/ngx_http_core_module.html#root
以前只知道Nginx的location块中的root用法，用起来总是感觉满足不了自己的一些想法。然后终于发现了alias这个东西。

  先看toot的用法

  location /request_path/image/ {
      root /local_path/image/;
  }
  这样配置的结果就是当客户端请求 /request_path/image/cat.png 的时候， 
  Nginx把请求映射为/local_path/image/request_path/image/cat.png

  再看alias的用法

  location /request_path/image/ {
      alias /local_path/image/;
  }

  这时候，当客户端请求 /request_path/image/cat.png 的时候， 
  Nginx把请求映射为/local_path/image/cat.png 
  对比root就可以知道怎么用了吧~~ :)


