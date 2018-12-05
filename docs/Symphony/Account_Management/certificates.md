# Certificates

# Importing a Certificate

To enable secure communication (HTTPS protocol) between the outside consumer and certain services, you will need to specify an SSL certificate that you have already imported into your domain. The following steps explain how to import an SSL certificate into Symphony.

**Importing an SSL Certificate into Symphony**

1.  On the **Menu** > **Account Management** > **Certificates** view, click **Import**.  
    This accesses the Import Certificate dialog.
    
2.  Name - Enter the name of the certificate.
    
3.  Certificate - Either Drop the certificate file in the designated area or Browse for it.  
    **Note**: The certificate file is the end-user certificate for your domain which you received from the certificate authority.
4.  Private Key - Either Drop the private key file in the designated area or Browse for it.  
    **Note**: The private key file is the file which contains the private key which matches your certificate.
5.  Certificate Chain (optional) - Either Drop the certificate chain file in the designated area or Browse for it.  
    **Note**: The Certificate Chain file includes all of the intermediate certificates, if any, and the root certificate.
6.  Click  **OK**.  
    You have now imported an SSL certificate which can be used by services which require secure communication.

# Symphony-supported AWS – ACM APIs and Parameters

**Authentication note**

Symphony supports AWS Signature Version 4.

Below is a list of the AWS - ACM APIs that Symphony supports, together with their supported Required and Optional request parameters.

Click on the API name to access the complete AWS documentation for that action.

<table style="border-collapse: collapse; width: 100%;" border="1"><tbody><tr style="height: 24px;"><td style="width: 33.3333%; height: 24px;"><strong>Name</strong></td><td style="width: 33.3333%; height: 24px;"><strong>Required parameters</strong></td><td style="width: 33.3333%; height: 24px;"><strong>Optional parameters</strong></td></tr><tr style="height: 24px;"><td style="width: 33.3333%; height: 24px;"><a href="https://docs.aws.amazon.com/acm/latest/APIReference/API_DeleteCertificate.html">DeleteCertificate</a></td><td style="width: 33.3333%; height: 24px;">CertificateArn</td><td style="width: 33.3333%; height: 24px;"></td></tr><tr style="height: 24px;"><td style="width: 33.3333%; height: 24px;"><a href="https://docs.aws.amazon.com/acm/latest/APIReference/API_DescribeCertificate.html">DescribeCertificate</a></td><td style="width: 33.3333%; height: 24px;">CertificateArn</td><td style="width: 33.3333%; height: 24px;"></td></tr><tr style="height: 24px;"><td style="width: 33.3333%; height: 24px;"><a href="https://docs.aws.amazon.com/acm/latest/APIReference/API_GetCertificate.html">GetCertificate</a></td><td style="width: 33.3333%; height: 24px;">CertificateArn</td><td style="width: 33.3333%; height: 24px;"></td></tr><tr style="height: 24px;"><td style="width: 33.3333%; height: 24px;"><a href="https://docs.aws.amazon.com/acm/latest/APIReference/API_ImportCertificate.html">ImportCertificate</a></td><td style="width: 33.3333%; height: 24px;">Certificate<br> PrivateKey</td><td style="width: 33.3333%; height: 24px;">CertificateChain</td></tr><tr style="height: 24px;"><td style="width: 33.3333%; height: 24px;"><a href="https://docs.aws.amazon.com/acm/latest/APIReference/API_ListCertificates.html">ListCertificates</a></td><td style="width: 33.3333%; height: 24px;"></td><td style="width: 33.3333%; height: 24px;"></td></tr></tbody></table>

