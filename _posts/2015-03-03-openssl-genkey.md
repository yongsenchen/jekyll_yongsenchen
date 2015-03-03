---
layout: post
category : security
tags : [openssl]
---

Generate RSA Key Pair: http://en.wikibooks.org/wiki/Cryptography/Generate_a_keypair_using_OpenSSL

U-boot http://lists.denx.de/pipermail/u-boot/2013-January/143409.html

	struct rsa_public_key {
		uint len;		/* Length of modulus[] in number of uint32_t */
		uint32_t n0inv;		/* -1 / modulus[0] mod 2^32 */
		uint32_t *modulus;	/* modulus as little endian array */
		uint32_t *rr;		/* R^2 as little endian array */
	};

OpenSSL Encryption/Decryption: http://yuanshuilee.blog.163.com/blog/static/21769727520140942826137/
