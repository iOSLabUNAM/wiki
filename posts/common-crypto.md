--
title: CommonCrypto
category: ios
--

# CommonCrypto

la libreria CommonCrypto soporta encriptacion simetrica, mensajes basados en codigos de authenticacion hash, y sumatorias de comprobacion.

## Bridge

```objective-c
#import <CommonCrypto/CommonDigest.h>
```

## MD5

```objective-c
- (NSString *) md5:(NSString *) input
{
    const char *cStr = [input UTF8String];
    unsigned char digest[CC_MD5_DIGEST_LENGTH];
    CC_MD5( cStr, strlen(cStr), digest ); // This is the md5 call

    NSMutableString *output = [NSMutableString stringWithCapacity:CC_MD5_DIGEST_LENGTH * 2];

    for(int i = 0; i < CC_MD5_DIGEST_LENGTH; i++)
    [output appendFormat:@"%02x", digest[i]];

    return  output;
}
```


```swift
func MD5(string: String) -> Data {
    let messageData = string.data(using:.utf8)!
    var digestData = Data(count: Int(CC_MD5_DIGEST_LENGTH))

    _ = digestData.withUnsafeMutableBytes {digestBytes in
        messageData.withUnsafeBytes {messageBytes in
            CC_MD5(messageBytes, CC_LONG(messageData.count), digestBytes)
        }
    }

    return digestData
}
```


## SHA1

```objective-c
-(NSString *) sha1String: (NSString *)input {
    NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
    uint8_t digest[CC_SHA1_DIGEST_LENGTH];
    CC_SHA1(data.bytes, (CC_LONG)data.length, digest);
    NSMutableString *output = [NSMutableString stringWithCapacity:CC_SHA1_DIGEST_LENGTH * 2];
    for (int i = 0; i < CC_SHA1_DIGEST_LENGTH; i++) {
        [output appendFormat:@"%02x", digest[i]];
    }
    return output;
}
```

```swift
func sha1(string: String) -> String {
    let data = string.data(using: String.Encoding.utf8)!
    let digest = sha1(data: data)
    return digest.map { String(format: "%02hhx", $0) }.joined()
}

func sha1(data: Data) -> [UInt8] {
    var digest = [UInt8](repeating: 0, count: Int(CC_SHA1_DIGEST_LENGTH))
    data.withUnsafeBytes {
        _ = CC_SHA1($0, CC_LONG(data.count), &digest)
    }
    return digest
}
```

## SHA256

```objective-c
-(NSString *) sha256String: (NSString *)input{
    const char *data = [input cStringUsingEncoding:NSASCIIStringEncoding];
    NSData *keyData = [NSData dataWithBytes:data length:strlen(data)];
    uint8_t digest[CC_SHA256_DIGEST_LENGTH] = {0};
    CC_SHA256(keyData.bytes, (CC_LONG)(keyData.length), digest);
    NSData *out = [NSData dataWithBytes:digest length:CC_SHA256_DIGEST_LENGTH];
    NSString *hash = [out description];
    hash = [hash stringByReplacingOccurrencesOfString:@" " withString:@""];
    hash = [hash stringByReplacingOccurrencesOfString:@"<" withString:@""];
    hash = [hash stringByReplacingOccurrencesOfString:@">" withString:@""];
    return hash;
}
```

```swift
func sha256(string: String) -> String {
    let data = string.data(using: String.Encoding.utf8)!
    guard let digest = sha256(data: data) else { return "" }
    return digest.map { String(format: "%02hhx", $0) }.joined()
}

func sha256(data: Data) -> Data? {
    var hashData = Data(count: Int(CC_SHA256_DIGEST_LENGTH))
    _ = hashData.withUnsafeMutableBytes {digestBytes in
        data.withUnsafeBytes {messageBytes in
            CC_SHA256(messageBytes, CC_LONG(data.count), digestBytes)
        }
    }
    return hashData
}
```


## Base64

```objective-c
-(NSString *) base64String: (NSString *)input{
    NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
    return [data base64EncodedStringWithOptions:0];
}

- (NSString *) base64Image:(UIImage *)image {
    return [UIImagePNGRepresentation(image) base64EncodedStringWithOptions:NSDataBase64Encoding64CharacterLineLength];
}
```

```swift
func base64(string: String) -> String {
    return String(data: Data(string.utf8).base64EncodedData(), encoding: .utf8) ?? ""
}

func base64(image: UIImage) -> String {
    return base64(data: image.pngData())
}
```
