# TLSv12_cifras_fortes

**Tomcat 9:**

Linhas de configuração no arquivo **server.xml** do webserver Tomcat:

<Connector <br>
        port="443" protocol="org.apache.coyote.http11.Http11AprProtocol" maxThreads="150"  <br>
        SSLEnabled="true" scheme="https" secure="true" defaultSSLHostConfigName="localhost"&gt;    <br>                    
        &lt;UpgradeProtocol className="org.apache.coyote.http2.Http2Protocol" /&gt; <br>        
        &lt;SSLHostConfig hostName="localhost" protocols="TLSv1.2" ciphers="TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384"&gt; <br>
                   <Certificate certificateKeyFile="conf/cert.key" certificateFile="conf/cert.pem" certificateChainFile="conf/cert_FULLCHAIN.pem" type="RSA" /&gt; <br>
        &lt;/SSLHostConfig&gt; <br>
&lt;/Connector&gt; <br>


**Apache 2:**

Linhas de configuração no arquivo **httpd.conf** do webserver Apache:

SSLProtocol -All +TLSv1.2 +TLSv1.3

SSLCipherSuite ECDHE-RSA-AES128-GCM-SHA256:ECDHE-RSA-AES256-GCM-SHA384

SSLHonorCipherOrder on

SSLEngine on

SSLCertificateFile /etc/httpd/conf.d/certificates/cert.crt

SSLCertificateKeyFile /etc/httpd/conf.d/certificates/cert.key

SSLCertificateChainFile /etc/httpd/conf.d/certificates/cert_CHAIN.crt



**IIS 10:**

Criar as duas chaves de registro, TLS 1.0 e TLS 1.1 e subkeys Client e Server. Criar DWORD Enabled e configurar valor 0 Dentro de:<br>
Computer\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\ <br>

Para as cifras, abrir gpedit.msc e navegar até Computer Configuration\Administrative Templates\Network\SSL Configuration Settings. <br>
Utilizar as mesmas cifras listadas acima para os outros webservers.

Como testar:

https://www.ssllabs.com/ssltest/index.html
