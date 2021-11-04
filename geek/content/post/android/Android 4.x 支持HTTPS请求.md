---
title: Android 4.x 支持HTTPS请求
date: 2021-11-03 10:10:00
tags: [android]
---



定义 SSLSocketFactoryCompat，在创建 Socket 的时候如果是 4.x 的设备则启用 TLSv1.2

```
import android.os.Build;

import java.io.IOException;
import java.net.InetAddress;
import java.net.Socket;
import java.security.KeyManagementException;
import java.security.NoSuchAlgorithmException;

import javax.net.ssl.SSLContext;
import javax.net.ssl.SSLSocket;
import javax.net.ssl.SSLSocketFactory;

public class SSLSocketFactoryCompat extends SSLSocketFactory{
    private static final String[] TLS_V12_ONLY = {"TLSv1.2"};

    private final SSLSocketFactory delegate;

    public SSLSocketFactoryCompat() throws KeyManagementException, NoSuchAlgorithmException {
        SSLContext sc = SSLContext.getInstance("TLS");
        sc.init(null, null, null);
        delegate = sc.getSocketFactory();
    }

    public SSLSocketFactoryCompat(SSLSocketFactory delegate) {
        if (delegate == null) {
            throw new NullPointerException();
        }
        this.delegate = delegate;
    }
    
    @Override
    public String[] getDefaultCipherSuites() {
        return delegate.getDefaultCipherSuites();
    }

    @Override
    public String[] getSupportedCipherSuites() {
        return delegate.getSupportedCipherSuites();
    }

    private Socket enableTls12(Socket socket) {
        if (Build.VERSION.SDK_INT >= 16 && Build.VERSION.SDK_INT < 20) {
            if (socket instanceof SSLSocket) {
                ((SSLSocket) socket).setEnabledProtocols(TLS_V12_ONLY);
            }
        }
        return socket;
    }

    @Override
    public Socket createSocket(Socket s, String host, int port, boolean autoClose) throws IOException {
        return enableTls12(delegate.createSocket(s, host, port, autoClose));
    }

    @Override
    public Socket createSocket(String host, int port) throws IOException {
        return enableTls12(delegate.createSocket(host, port));
    }

    @Override
    public Socket createSocket(String host, int port, InetAddress localHost, int localPort) throws IOException {
        return enableTls12(delegate.createSocket(host, port, localHost, localPort));
    }

    @Override
    public Socket createSocket(InetAddress host, int port) throws IOException {
        return enableTls12(delegate.createSocket(host, port));
    }

    @Override
    public Socket createSocket(InetAddress address, int port, InetAddress localAddress, int localPort) throws IOException {
        return enableTls12(delegate.createSocket(address, port, localAddress, localPort));
    }
}
```



如果客户端自己有提供 SSLSocketFactory 的情况（比如，客户端加载自己的证书会提供 SSLSocketFactory），则使用 SSLSocketFactoryCompat 包裹自身的 SSLSocketFactory 然后进行设置，如果没有的话，则使用 SSLSocketFactoryCompat 的无参构造函数。



上述类可以用于 OkHttp，也可用于其他 HTTPS 需要设置 SSLSocketFactory 的情况。



OkHttp 使用



```
// 自己不提供额外证书的情况
public static OkHttpClient getOkHttpClient() {
    OkHttpClient.Builder builder = new OkHttpClient.Builder();
    try {
        SSLSocketFactory factory = new SSLSocketFactoryCompat();
        builder.sslSocketFactory(factory);
    } catch (KeyManagementException e) {
        e.printStackTrace();
    } catch (NoSuchAlgorithmException e) {
        e.printStackTrace();
    }
    return builder.build();
}
```



提供额外证书的情况：



```
// 测试在assets目录下包含了gank.cer证书，你可以根据自己的情况处理
private static OkHttpClient getOkHttpClientSSL() {
    OkHttpClient.Builder builder = new OkHttpClient.Builder();
    InputStream cerInputStream;
    try {
        cerInputStream = App.getInstance().getAssets().open("gank.cer");
        SSLSocketFactory socketFactory = getSocketFactory(cerInputStream);
        builder.sslSocketFactory(new SSLSocketFactoryCompat(socketFactory));
    } catch (IOException e) {
        e.printStackTrace();
    }
    return builder.build();
}

// 根据证书生成SSLSocketFactory，支持多个证书
private static SSLSocketFactory getSocketFactory(InputStream... certificates) {
    KeyStore keyStore;
    try {
        CertificateFactory certificateFactory = CertificateFactory.getInstance("X.509");
        keyStore = KeyStore.getInstance(KeyStore.getDefaultType());
        keyStore.load(null);
        int index = 0;
        for (InputStream certificate : certificates) {
            String certificateAlias = Integer.toString(index++);
            keyStore.setCertificateEntry(certificateAlias, certificateFactory.generateCertificate(certificate));
        }
        SSLContext sslContext = SSLContext.getInstance("TLS");
        TrustManagerFactory trustManagerFactory =
                TrustManagerFactory.getInstance(TrustManagerFactory.getDefaultAlgorithm());
        trustManagerFactory.init(keyStore);
        sslContext.init(null, trustManagerFactory.getTrustManagers(), new SecureRandom());
        return sslContext.getSocketFactory();
    } catch (KeyStoreException e) {
        e.printStackTrace();
    } catch (CertificateException e) {
        e.printStackTrace();
    } catch (NoSuchAlgorithmException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    } catch (KeyManagementException e) {
        e.printStackTrace();
    } finally {
        for (InputStream certificate : certificates) {
            try {
                certificate.close();
            } catch (IOException e) {
                e.printStackTrace();
            }
        }
    }
    return null;
}
```



HttpsURLConnection 简单测试



```
new Thread(new Runnable() {
    @Override
    public void run() {
        try {
            URL url = new URL("https://gank.io/api/today");
            HttpsURLConnection connection = (HttpsURLConnection) url.openConnection();
            connection.setSSLSocketFactory(new SSLSocketFactoryCompat());
            InputStream inputStream = connection.getInputStream();
            String result = IoUtils.readAllChars(new InputStreamReader(inputStream));
            LogUtils.json(result);
            inputStream.close();
        } catch (MalformedURLException e) {
            e.printStackTrace();
        } catch (IOException e) {
            e.printStackTrace();
        } catch (NoSuchAlgorithmException e) {
            e.printStackTrace();
        } catch (KeyManagementException e) {
            e.printStackTrace();
        }
    }
}).start();
```