---
title: Unit Tests Cheatsheet
category: appendix
layout: post
---

# Unit Tests Cheatsheet

## XCTestCase

Estructura Base

```swift
class Tests: XCTestCase {
    override func setUp() {
        super.setUp()
        // initialize variables
    }

    override func tearDown() {
        // deinitialize variables
        super.tearDown()
    }

    func testMyTestName() {
       // test code
    }
}
```

#### setUp()
Se ejecuta antes de cada prueba

#### tearDown()
Se ejecuta despues de cada prueba

#### test_______()
Los metodos de prueba comienzan con la palabra `test`

## Assertions
Una aserción un metodo de que evalua el cumplimiento de un resultado dado un valor esperado

- XCTAssert
- XCTAssertTrue
- XCTAssertFalse
- XCTAssertNil
- XCTAssertNotNil
- XCTAssertThrowsError
- XCTAssertNotThrows
- XCTAssertEqual
- XCTAssertNotEqual
- XCTAssertGreaterThan
- XCTAssertGreaterThanOrEqual
- XCTAssertLessThan
- XCTAssertLessThanOrEqual

### Test Async

```swift
    func testIndexSuccess() {
        let session = Session(cassetteName: "index.success")
        let service = buildService(for: session)
        let exp = expectation(description: "Successfull index")
        service.index { response in
            exp.fulfill()
            XCTAssertNotNil(response)
        }

        waitForExpectations(timeout: 2, handler: nil)
    }

```
