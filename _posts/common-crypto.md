---
title: CommonCrypto
category: core library
layout: post
---

# CommonCrypto

La libreria CommonCrypto soporta encriptacion simetrica, mensajes basados en codigos de authenticacion hash, y sumatorias de comprobacion.

## Bridge

Al ser una libreria de objective-c es necesario incluir un Bridge en el proyecto para asi tener
acceso en swift. Para crearlo de manera automatica solo es nececsaro incluir un archivo `.m`  y XCode preguntara si se desea agregar un Brige, con el cual incluira al proceso de compilacion de proyecto.

Ya teniendo nuestro archivo Brige, agregamos esta `CommonDigest.h` para acceder a dependencias para construir sumatorias de comprobacion

```objective-c
#import <CommonCrypto/CommonDigest.h>
```

## MD5


#### Objective-C
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

#### Swift
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

#### Objective-C
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

#### Swift
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

#### Objective-C
```objective-c
-(NSString *) sha256String: (NSString *)input{
    const char* str = [input UTF8String];
    unsigned char result[CC_SHA256_DIGEST_LENGTH];
    CC_SHA256(str, strlen(str), result);

    NSMutableString *ret = [NSMutableString stringWithCapacity:CC_SHA256_DIGEST_LENGTH*2];
    for(int i = 0; i<CC_SHA256_DIGEST_LENGTH; i++)
    {
        [ret appendFormat:@"%02x",result[i]];
    }
    return ret;
}
```

#### Swift
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

#### Objective-C
```objective-c
-(NSString *) base64String: (NSString *)input{
    NSData *data = [input dataUsingEncoding:NSUTF8StringEncoding];
    return [data base64EncodedStringWithOptions:0];
}

- (NSString *) base64Image:(UIImage *)image {
    return [UIImagePNGRepresentation(image) base64EncodedStringWithOptions:NSDataBase64Encoding64CharacterLineLength];
}
```

#### Swift
```swift
func base64(string: String) -> String {
    return String(data: Data(string.utf8).base64EncodedData(), encoding: .utf8) ?? ""
}

func base64(image: UIImage) -> String {
    return base64(data: image.pngData())
}

func base64(data: Data?) -> String {
    return data.base64EncodedString(options: .lineLength64Characters) ?? ""
}

```

## Data extension

Al utilizar data en cada una de las sumatorias de comprobacion se puede hacer una
extension a data, de esta forma los metodos siempre estaran accesibles a instancias de
objeto Data


```swift
extension Data {
    func base64() -> String {
        return self.base64EncodedString(options: .lineLength64Characters)
    }

    func sha1() -> String {
        var digest = [UInt8](repeating: 0, count: Int(CC_SHA1_DIGEST_LENGTH))
        self.withUnsafeBytes {
            _ = CC_SHA1($0, CC_LONG(self.count), &digest)
        }
        return digest.map { String(format: "%02hhx", $0) }.joined()
    }

    func sha256() -> String {
        var hashData = Data(count: Int(CC_SHA256_DIGEST_LENGTH))
        _ = hashData.withUnsafeMutableBytes { digestBytes in
            self.withUnsafeBytes { messageBytes in
                CC_SHA256(messageBytes, CC_LONG(self.count), digestBytes)
            }
        }
        return hashData.map { String(format: "%02hhx", $0) }.joined()
    }
}
```
