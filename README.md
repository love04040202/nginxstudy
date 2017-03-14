# nginxstudy
利用Nginx访问、下载本机目录文件
  使用Nginx时，如果要让一些附件比如 txt,pdf,doc等不直接在浏览器打开，而弹出另存为的对话框（也就是下载）
  则可以在nginx的加上头配置如下：

  if ($request_filename ~* ^.*?\.(txt|pdf|doc|xls)$){  
      add_header Content-Disposition: 'attachment;';  
  }  
