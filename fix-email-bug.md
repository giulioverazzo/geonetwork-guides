# How to fix Geonetwork email configuration problems

When configuring Geonetwork to send feedback emails, it may happen that the configuration although being correct gives an error. This is because of some deprecated cipher algorithms being disabled in the JVM.  

To fix this problem open the `java.security` file and look for the line with `jdk.tls.disabledAlgorithms`.

The value of this attribute is a list of (as the name says) disabled algorithms. Remove TLSv1.0 and TLSv1.1 from the list and save the file.

Restart Geonetwork and the error should be gone.

PS: In my case, `java.security` file was at this location:

`/usr/local/openjdk-8/jre/lib/security/java.security`
