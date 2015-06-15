# Linio Standards
This repository serves to hold all of the documentation and utilities that Linio developers use to perform their duties.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in RFC 2119.

## Security
### GitHub
Linio uses GitHub for it's code hosting. For security purposes, all developers MUST enable 2FA (Two-Factor Authentication) on GitHub.

If you do not currently have a OTP (One time password) client, such as [Authy](https://www.authy.com), or Google Authenticator, please take a look at [Authy](https://www.authy.com). It's available on Android, iOS, and Chrome.

## Warnings
Included in the standards directory are multiple documents which MUST be adhered to. Straying away from these standards MAY result in disciplinary action.

## Directories
### git-hooks
This directory includes commit hooks that SHOULD be used in all code repositories. 

To use them, simply copy the contents of this directory to .git/hooks inside your repository. Remember to make sure that each file is executable. You can make them executable by issuing the 
following command:

```
$ chmod +x .git/hooks/*
```

### phpstorm
The .jar file included in this direcotry MUST be imported into PhpStorm. When done, it will configure PhpStorm to the Linio code standards.

### php-cs-fixer
The included .php_cs file in this directory MUST be copied to the root of each and every code repository. It instructs php-cs-fixer to fix your code according to the Linio code standards. The only 
thing that MAY be changed is the directory inclusion section.

### standards
This directory includes the misc. standards documents that all Linio developers must adhere to.

### tools
This directory contains misc. configuration files for various utilities such as PHP Code Sniffer, PHPUnit, etc.

## Standards

### [Commit Standards](standards/commit-standard.md)
This file documents standards that all Linio developers MUST adhere to for the utilization of Git.

### [PHP Coding Standards](standards/php-coding-standard.md)
This file documents standards that ALL Linio PHP code MUST adhere to.
