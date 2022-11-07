# Encrypt customer input<a name="encrypt-data"></a>

You can encrypt sensitive data that is collected by flows\. To do this, you need to use public\-key cryptography\. 

When configuring Amazon Connect, you first provide the public key\. This is the key used when encrypting data\. Later, you provide the X\.509 certificate, which includes a signature that proves you possess the private key\. 

In a flow that collects data, you provide an X\.509 certificate to encrypt data that's captured using the **Stored customer input** system attribute\. You must upload the key in `.pem` format to use this feature\. The encryption key is used to verify the signature of the certificate used within the flow\. 

**Note**  
You can have up to two encryption keys active at one time to facilitate rotation\.

To decrypt the data in the **Stored customer input** attribute, use the AWS Encryption SDK\. For more information, see the [AWS Encryption SDK Developer Guide](https://docs.aws.amazon.com/encryption-sdk/latest/developer-guide/)\.

For a detailed walkthrough, see [Creating a secure IVR solution with Amazon Connect](https://aws.amazon.com/blogs/contact-center/creating-a-secure-ivr-solution-with-amazon-connect/)\. It shows how to:
+ Configure Amazon Connect to collect a credit card number\.
+ Encrypt the credit card digits\.
+ Send it to our backend AWS Lambda for decryption, using the customer supplied decryption key\.

It provides two commands using OpenSSL: 
+ One to generate an RSA key pair and a self\-signed X\.509 certificate
+ Another to extract the public key from the RSA key pair

## How to decrypt data encrypted by Amazon Connect<a name="sample-decryption"></a>

The following code sample shows how to decrypt data using the AWS Encryption SDK\. 

```
package com.amazonaws;
 
import com.amazonaws.encryptionsdk.AwsCrypto;
import com.amazonaws.encryptionsdk.CryptoResult;
import com.amazonaws.encryptionsdk.jce.JceMasterKey;
import org.bouncycastle.jce.provider.BouncyCastleProvider;
 
import java.io.IOException;
import java.nio.charset.Charset;
import java.nio.file.Files;
import java.nio.file.Paths;
import java.security.GeneralSecurityException;
import java.security.KeyFactory;
import java.security.Security;
import java.security.interfaces.RSAPrivateKey;
import java.security.spec.PKCS8EncodedKeySpec;
import java.util.Base64;
 
public class AmazonConnectDecryptionSample {
 
    // The Provider 'AmazonConnect' is used during encryption, this must be used during decryption for key
    // to be found
    private static final String PROVIDER = "AmazonConnect";
 
    // The wrapping algorithm used during encryption
    private static final String WRAPPING_ALGORITHM = "RSA/ECB/OAEPWithSHA-512AndMGF1Padding";
 
    /**
     * This sample show how to decrypt data encrypted by Amazon Connect.
     * To use, provide the following command line arguments: [path-to-private-key] [key-id] [cyphertext]
     * Where:
     *  path-to-private-key is a file containing the PEM encoded private key to use for decryption
     *  key-id is the key-id specified during encryption in your flow
     *  cyphertext is the result of the encryption operation from Amazon Connect
     */
    public static void main(String[] args) throws IOException, GeneralSecurityException {
        String privateKeyFile = args[0]; // path to PEM encoded private key to use for decryption
        String keyId = args[1]; // this is the id used for key in your flow
        String cypherText = args[2]; // the result from flow
 
        Security.addProvider(new BouncyCastleProvider());
 
        // read the private key from file
        String privateKeyPem = new String(Files.readAllBytes(Paths.get(privateKeyFile)), Charset.forName("UTF-8"));
        RSAPrivateKey privateKey =  getPrivateKey(privateKeyPem);
 
        AwsCrypto awsCrypto = new AwsCrypto();
        JceMasterKey decMasterKey =
                JceMasterKey.getInstance(null,privateKey, PROVIDER, keyId, WRAPPING_ALGORITHM);
        CryptoResult<String, JceMasterKey> result = awsCrypto.decryptString(decMasterKey, cypherText);
 
        System.out.println("Decrypted: " + result.getResult());
    }
 
    public static RSAPrivateKey getPrivateKey(String privateKeyPem) throws IOException, GeneralSecurityException {
        String privateKeyBase64 = privateKeyPem
                .replace("-----BEGIN RSA PRIVATE KEY-----\n", "")
                .replace("-----END RSA PRIVATE KEY-----", "")
                .replaceAll("\n", "");
        byte[] decoded = Base64.getDecoder().decode(privateKeyBase64);
        KeyFactory kf = KeyFactory.getInstance("RSA");
        PKCS8EncodedKeySpec keySpec = new PKCS8EncodedKeySpec(decoded);
        RSAPrivateKey privKey = (RSAPrivateKey) kf.generatePrivate(keySpec);
        return privKey;
    }
}
```