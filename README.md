# SSL-TLS-ANALYZER
Detailed Summary of  SSL Analyzer Website
1. User Input (Domain Check)

A user enters a website domain (e.g., example.com).
It analyzer connects to that server over SSL/TLS.
It retrieves the certificate chain and analyzes it.
Output is displayed either on the console or on the web page (Flask UI).

2. Server Certificate Information

For the main server certificate, it tool extracts:
✅ Subject / Common Name (CN) – The domain name the certificate is issued for.

✅ SANs (Subject Alternative Names) – Other valid domains/subdomains.

✅ Serial Number – Unique certificate identifier.

✅ Validity Period – Start & Expiry dates, along with time remaining.

✅ Issuer Information – Which CA (Certificate Authority) issued it.

✅ Public Key Info – Key algorithm (RSA/EC), size (e.g., 2048-bit), strength check.

✅ Signature Algorithm – Like SHA256withRSA, and if considered weak/strong.

✅ Extensions – OCSP Must-Staple, Certificate Transparency, etc.

3. Intermediate Certificate Handling

It analyzer checks whether all required intermediate certificates are provided.
If not, it tries to download missing intermediates automatically via AIA fetching.
Shows whether the chain is complete or broken.

4. Certification Path Validation
   
Builds the full chain of trust:
Server Certificate → Intermediate(s) → Root CA
Checks if the Root CA is trusted in system/browser stores.
Detects untrusted/self-signed certificates.

5. Revocation Status

Extracts CRL (Certificate Revocation List) and OCSP URLs from the certificate.
Performs OCSP checks live to see if the certificate is revoked or valid.
Flags revoked or unknown certificates.

6. Protocol & Cipher Analysis (Vulnerabilities Section)

It analyzer can test the server against known SSL/TLS weaknesses:

🔐 Protocol Support

Detects which versions are supported: SSL 2.0, SSL 3.0, TLS 1.0, 1.1, 1.2, 1.3.
Warns if old/insecure versions are enabled.

🔐 Cipher Suite Strength

Checks if weak ciphers (RC4, 3DES, EXPORT, NULL) are offered.
Verifies forward secrecy support (ECDHE/DHE).

🔐 Known Vulnerabilities

BEAST Attack (affects TLS 1.0 with CBC).

POODLE Attack (affects SSL 3.0).

Heartbleed (OpenSSL bug test).

ROBOT Attack (RSA key exchange vulnerability).

Compression / CRIME vulnerability.

Session Resumption / Ticketbleed checks.

TLS Fallback / Downgrade protection detection.

7. DNS CAA Records

Queries DNS for CAA records to see which CAs are authorized to issue certificates for the domain.
Helps prevent mis-issuance of fake certificates.

8. Overall SSL/TLS Rating

Based on all checks, your analyzer can provide a rating (like SSL Labs: A+, A, B, F).
Example criteria:

✅ Strong TLS version (1.2/1.3 only)

✅ Strong ciphers only

✅ Certificate valid & trusted

❌ No weak protocols (SSL 3.0, TLS 1.0/1.1)

❌ No known vulnerabilities
