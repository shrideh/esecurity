B.4
```python
print (chars//16+1)*32
```

C.4
```python
print (chars//16+1)*16
```

Commands in Section A:

* openssl list-cipher-commands
* openssl version
* openssl prime –hex 1111
* openssl enc -aes-256-cbc -in myfile.txt -out encrypted.bin
* openssl enc -aes-256-cbc -in myfile.txt -out encrypted.bin –base64
* openssl enc -d -aes-256-cbc -in encrypted.bin -pass pass:napier -base64

B.2

```python
from Crypto.Cipher import AES
import hashlib
import sys
import binascii
import Padding

val='hello'
password='hello'

plaintext=val

def encrypt(plaintext,key, mode):
	encobj = AES.new(key,mode)
	return(encobj.encrypt(plaintext))

def decrypt(ciphertext,key, mode):
	encobj = AES.new(key,mode)
	return(encobj.decrypt(ciphertext))

key = hashlib.sha256(password).digest()


plaintext = Padding.appendPadding(plaintext,blocksize=Padding.AES_blocksize,mode='CMS')
print "After padding (CMS): "+binascii.hexlify(bytearray(plaintext))

ciphertext = encrypt(plaintext,key,AES.MODE_ECB)
print "Cipher (ECB): "+binascii.hexlify(bytearray(ciphertext))

plaintext = decrypt(ciphertext,key,AES.MODE_ECB)
plaintext = Padding.removePadding(plaintext,mode='CMS')
print "  decrypt: "+plaintext


plaintext=val


plaintext = Padding.appendPadding(plaintext,blocksize=Padding.AES_blocksize,mode='ZeroLen')
print "\nAfter padding (Bit): "+binascii.hexlify(bytearray(plaintext))

ciphertext = encrypt(plaintext,key,AES.MODE_ECB)
print "Cipher (ECB): "+binascii.hexlify(bytearray(ciphertext))

plaintext = decrypt(ciphertext,key,AES.MODE_ECB)
plaintext = Padding.removePadding(plaintext,blocksize=Padding.AES_blocksize,mode='ZeroLen')
print "  decrypt: "+plaintext


plaintext=val

plaintext = Padding.appendPadding(plaintext,blocksize=Padding.AES_blocksize,mode='Space')
print "\nAfter padding (Null): "+binascii.hexlify(bytearray(plaintext))

ciphertext = encrypt(plaintext,key,AES.MODE_ECB)
print "Cipher (ECB): "+binascii.hexlify(bytearray(ciphertext))

plaintext = decrypt(ciphertext,key,AES.MODE_ECB)
plaintext = Padding.removePadding(plaintext,blocksize=Padding.AES_blocksize,mode='Space')
print "  decrypt: "+plaintext


plaintext=val

plaintext = Padding.appendPadding(plaintext,blocksize=Padding.AES_blocksize,mode='Random')
print "\nAfter padding (Random): "+binascii.hexlify(bytearray(plaintext))

ciphertext = encrypt(plaintext,key,AES.MODE_ECB)
print "Cipher (ECB): "+binascii.hexlify(bytearray(ciphertext))

plaintext = decrypt(ciphertext,key,AES.MODE_ECB)
plaintext = Padding.removePadding(plaintext,mode='Random')
print "  decrypt: "+plaintext
```

C.2

```python
from Crypto.Cipher import DES
import hashlib
import sys
import binascii
import Padding

val='hello'
password='hello'

plaintext=val


def encrypt(plaintext,key, mode):
	encobj = DES.new(key,mode)
	return(encobj.encrypt(plaintext))

def decrypt(ciphertext,key, mode):
	encobj = DES.new(key,mode)
	return(encobj.decrypt(ciphertext))


print "\nDES"
key = hashlib.sha256(password).digest()[:8]

plaintext = Padding.appendPadding(plaintext,blocksize=Padding.DES_blocksize,mode='CMS')
print "After padding (CMS): "+binascii.hexlify(bytearray(plaintext))

ciphertext = encrypt(plaintext,key,DES.MODE_ECB)
print "Cipher (ECB): "+binascii.hexlify(bytearray(ciphertext))

plaintext = decrypt(ciphertext,key,DES.MODE_ECB)
plaintext = Padding.removePadding(plaintext,mode='CMS')
print "  decrypt: "+plaintext
```

D.1
```python
from Crypto.Cipher import AES
import hashlib
import sys
import binascii
import Padding

val='hello'
password='hello'

plaintext=val

def encrypt(plaintext,key, mode):
	encobj = AES.new(key,mode)
	return(encobj.encrypt(plaintext))

def decrypt(ciphertext,key, mode):
	encobj = AES.new(key,mode)
	return(encobj.decrypt(ciphertext))

key = hashlib.sha256(password).digest()


plaintext = Padding.appendPadding(plaintext,blocksize=Padding.AES_blocksize,mode='CMS')
print "After padding (CMS): "+binascii.hexlify(bytearray(plaintext))

ciphertext = encrypt(plaintext,key,AES.MODE_ECB)
print "Cipher (ECB): "+binascii.hexlify(bytearray(ciphertext))

plaintext = decrypt(ciphertext,key,AES.MODE_ECB)
plaintext = Padding.removePadding(plaintext,mode='CMS')
print "  decrypt: "+plaintext


plaintext=val
```

Possible solution for E.1:

```python
from Crypto.Cipher import AES
import hashlib
import sys
import binascii
import Padding

val='fox'
password='hello'
cipher=''

import sys

if (len(sys.argv)>1):
	cipher=(sys.argv[1])
if (len(sys.argv)>2):
	password=(sys.argv[2])

plaintext=val

def encrypt(plaintext,key, mode):
	encobj = AES.new(key,mode)
	return(encobj.encrypt(plaintext))

def decrypt(ciphertext,key, mode):
	encobj = AES.new(key,mode)
	return(encobj.decrypt(ciphertext))

key = hashlib.sha256(password).digest()


ciphertext=binascii.unhexlify(cipher)

plaintext = decrypt(ciphertext,key,AES.MODE_ECB)
print plaintext
plaintext = Padding.removePadding(plaintext,mode='CMS')
print "  decrypt: "+plaintext


plaintext=val
```

F.1

```python
try:
	plaintext = Padding.removePadding(plaintext,mode='CMS')
	print "  decrypt: "+plaintext
except:
	print("Error!")
```

G.1 Node.js code:

```javascript
    var Chacha20KeySize = 32;
    var Chacha20NonceSize = 8;


    key = '0000000000000000000000000000000000000000000000000000000000000000';

    nce = '0000000000000000';

   document.getElementById("val1").innerHTML = nce;
   document.getElementById("key").innerHTML = key;

    go();


    function go() {

        n = document.getElementById('val1').value;
        k = document.getElementById('key').value;

       document.getElementById("encrypted").innerHTML = "Key:\t" + k;
              document.getElementById("encrypted").innerHTML += "\nNouce:\t" + n;

              n = from_Hex(n);
              k = from_Hex(k);


        var ctx, out;

        out = new Array(k.length);

        ctx = chacha20_init(k, n);

        chacha20_keystream(ctx, out, out, k.length);

        document.getElementById("encrypted").innerHTML += "\n---\nKey generation: " + bytes2hex(out);


    }
  



    var Chacha20Ctx = function () {
        this.input = new Array(16);
    };

    function load32(x, i) {
        return x[i] | (x[i + 1] << 8) | (x[i + 2] << 16) | (x[i + 3] << 24);
    }

    function store32(x, i, u) {
        x[i] = u & 0xff; u >>>= 8;
        x[i + 1] = u & 0xff; u >>>= 8;
        x[i + 2] = u & 0xff; u >>>= 8;
        x[i + 3] = u & 0xff;
    }

    function rotl32(v, c) {
        return (v << c) | (v >>> (32 - c));
    }

    function chacha20_round(x, a, b, c, d) {
        x[a] += x[b]; x[d] = rotl32(x[d] ^ x[a], 16);
        x[c] += x[d]; x[b] = rotl32(x[b] ^ x[c], 12);
        x[a] += x[b]; x[d] = rotl32(x[d] ^ x[a], 8);
        x[c] += x[d]; x[b] = rotl32(x[b] ^ x[c], 7);
    }

    function chacha20_init(key, nonce) {
        var x = new Chacha20Ctx();

        x.input[0] = 1634760805;
        x.input[1] = 857760878;
        x.input[2] = 2036477234;
        x.input[3] = 1797285236;
        x.input[12] = 0;
        x.input[13] = 0;
        x.input[14] = load32(nonce, 0);
        x.input[15] = load32(nonce, 4);

        for (var i = 0; i < 8; i++) {
            x.input[i + 4] = load32(key, i * 4);
        }
        return x;
    }

    function chacha20_keystream(ctx, dst, src, len) {
        var x = new Array(16);
        var buf = new Array(64);
        var i = 0, dpos = 0, spos = 0;

        while (len > 0) {
            for (i = 16; i--;) x[i] = ctx.input[i];
            for (i = 20; i > 0; i -= 2) {
                chacha20_round(x, 0, 4, 8, 12);
                chacha20_round(x, 1, 5, 9, 13);
                chacha20_round(x, 2, 6, 10, 14);
                chacha20_round(x, 3, 7, 11, 15);
                chacha20_round(x, 0, 5, 10, 15);
                chacha20_round(x, 1, 6, 11, 12);
                chacha20_round(x, 2, 7, 8, 13);
                chacha20_round(x, 3, 4, 9, 14);
            }
            for (i = 16; i--;) x[i] += ctx.input[i];
            for (i = 16; i--;) store32(buf, 4 * i, x[i]);

            ctx.input[12] += 1;
            if (!ctx.input[12]) {
                ctx.input[13] += 1;
            }
            if (len <= 64) {
                for (i = len; i--;) {
                    dst[i + dpos] = src[i + spos] ^ buf[i];
                }
                return;
            }
            for (i = 64; i--;) {
                dst[i + dpos] = src[i + spos] ^ buf[i];
            }
            len -= 64;
            spos += 64;
            dpos += 64;
        }
    }

    //--------------------------- test -----------------------------//
    function bytes2hex(blk, dlm) {
        return Array.prototype.map.call(new Uint8Array(blk.buffer || blk),
        function (s) { return ('00' + s.toString(16)).slice(-2); }).join(dlm || '');
    }
    function from_Hex(h) {

        h.replace(' ', '');
        var out = [], len = h.length, w = '';
        for (var i = 0; i < len; i += 2) {
            w = h[i];
            if (((i + 1) >= len) || typeof h[i + 1] === 'undefined') {
                w += '0';
            } else {
                w += h[i + 1];
            }
            out.push(parseInt(w, 16));
        }
        return out;
    }

    function bytesEqual(a, b) {
        var dif = 0;
        if (a.length !== b.length) return 0;
        for (var i = 0; i < a.length; i++) {
            dif |= (a[i] ^ b[i]);
        }
        dif = (dif - 1) >>> 31;
        return (dif & 1);
    }
```    

Sample answers

A possible answer for Section E is:

```python
from Crypto.Cipher import AES
import hashlib
import sys
import binascii
import Padding

val='hello'
password='hello'


cipher=raw_input('Enter cipher:')
password=raw_input('Enter password:')

plaintext=val

def encrypt(plaintext,key, mode):
	encobj = AES.new(key,mode)
	return(encobj.encrypt(plaintext))

def decrypt(ciphertext,key, mode):
	encobj = AES.new(key,mode)
	return(encobj.decrypt(ciphertext))

key = hashlib.sha256(password).digest()


ciphertext = binascii.unhexlify(cipher)

print "Cipher (ECB): "+binascii.hexlify(bytearray(ciphertext))

plaintext = decrypt(ciphertext,key,AES.MODE_ECB)
plaintext = Padding.removePadding(plaintext,mode='CMS')
print "  decrypt: "+plaintext
```

A sample code for Section F is:

```python
pw = ["hello","ankle","changeme","123456"]

for password in pw:

	try:
		key = hashlib.sha256(password).digest()
		cipherhex = base64.decodestring(cipher).encode('hex')

		ciphertext = binascii.unhexlify(cipherhex)

		print "Cipher (ECB): "+binascii.hexlify(bytearray(ciphertext))

		plaintext = decrypt(ciphertext,key,AES.MODE_ECB)
		plaintext = Padding.removePadding(plaintext,mode='CMS')
		print "  decrypt: "+plaintext
		print "  Key found"+password

	except:	
		print(".")
 ```