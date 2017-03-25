Lastpass Java Client
========

This is a java client for [lastpass](http://lastpass.com). Efforts have been made to choose dependencies which are compatible with android applications.

Status
--------
Reads password information from lastpass (name, URL, username, password) and supports OTP prompting.  
Does not support saving back to lastpass or offline logins (i.e. cached logins)

Building
--------
`mvn install`

Usage
--------
	Lastpass lastPass = new LastPassImpl();
	PasswordStoreBuilder builder = lastPass.getPasswordStoreBuilder("user", "password", cacheFile);
	PasswordStore store;
	try {
		store = builder.getPasswordStore();
	} catch (GoogleAuthenticatorRequired req) {
		// Prompt user for one-time password
		store = builder.getPasswordStore(userProvidedOtp);
	}
	
	// Get passwords for a hostname
	Collection<? extends PasswordInfo> passwords = store.getPasswordsByHostname("google.com");
	// Get all passwords
	Collection<? extends PasswordInfo allPasswords = store.getPasswords();

Issues
------

If you get an error in the unit tests:
```
initializationError(com.nhinds.lastpass.encryption.AES256DecryptionProviderTest):
java.security.InvalidKeyException: Illegal key size
```

You might need to install the [unlimited strength jurisdiction policy](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html) as
explained in this [stack overflow](http://stackoverflow.com/questions/3862800/invalidkeyexception-illegal-key-size) post.


License
--------
`lastpass-java` is released under the [MIT license](LICENSE)



