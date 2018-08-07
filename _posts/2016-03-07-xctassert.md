---
id: 574
title: XCTAssert
date: 2016-03-07T21:35:37+00:00
author: Marco Betschart
layout: post
guid: https://marco.betschart.name/?p=574
permalink: /xctassert/
thumb_image: uploads/2015/12/code-1084923-256x256.png
tags:
  - Technologie
---
### Overview

  *  [XCTAssert](#XCTAssert)
  *  [XCTAssertEqual](#XCTAssertEqual)
  *  [XCTAssertEqualObjects](#XCTAssertEqualObjects)
  *  [XCTAssertEqualWithAccuracy](#XCTAssertEqualWithAccuracy)
  *  [XCTAssertFalse](#XCTAssertFalse)
  *  [XCTAssertNotEqual](#XCTAssertNotEqual)
  *  [XCTAssertNotEqualObjects](#XCTAssertNotEqualObjects)
  *  [XCTAssertNotEqualWithAccuracy](#XCTAssertNotEqualWithAccuracy)
  *  [XCTAssertNoThrow](#XCTAssertNoThrow)
  *  [XCTAssertNoThrowSpecific](#XCTAssertNoThrowSpecific)
  * [XCTAssertNoThrowSpecificNamed](#XCTAssertNoThrowSpecificNamed)
  *  [XCTAssertNotNil](#XCTAssertNotNil)
  *  [XCTAssertThrows](#XCTAssertThrows)
  *  [XCTAssertThrowsSpecific](#XCTAssertThrowsSpecific)
  *  [XCTAssertThrowsSpecificNamed](#XCTAssertThrowsSpecificNamed)
  *  [XCTAssertTrue](#XCTAssertTrue)
  *  [XCTFail](#XCTFail) 

### Detail

<pre id="XCTAssert">XCTAssert(expression, format…)</pre>

Generates a failure when expression evaluates to false.

&nbsp;

<pre id="XCTAssertEqual">XCTAssertEqual(a1, a2, format…)</pre>

Generates a failure when a1 is not equal to a2. This test is for C scalars, structs and unions.

&nbsp;

<pre id="XCTAssertEqualObjects">XCTAssertEqualObjects(a1, a2, format…)</pre>

Generates a failure when !{ [a1 isEqual:a2] } is false (or one is nil and the other is not).

&nbsp;

<pre id="XCTAssertEqualWithAccuracy">XCTAssertEqualWithAccuracy(a1, a2, accuracy, format…)</pre>

Generates a failure when a1 is not equal to a2 within + or &#8211; accuracy. This test is for scalars such as floats and doubles, where small differences could make these items not exactly equal, but works for all scalars.

&nbsp;

<pre id="XCTAssertFalse">XCTAssertFalse(expression, format…)</pre>

Generates a failure when the expression evaluates to true.

&nbsp;

<pre id="XCTAssertNotEqual">XCTAssertNotEqual(a1, a2, format…)</pre>

Generates a failure when \a1 is not nil.

&nbsp;

<pre id="XCTAssertNotEqualObjects">XCTAssertNotEqualObjects(a1, a2, format…)</pre>

Generates a failure when { [a1 isEqual:a2] } is false (or both are nil).

&nbsp;

<pre id="XCTAssertNotEqualWithAccuracy">XCTAssertNotEqualWithAccuracy(a1, a2, accuracy, format…)</pre>

Generates a failure when a1 is equal to a2 within + or &#8211; accuracy. This test is for scalars such as floats and doubles, where small differences could make these items not exactly equal, but works for all scalars.

<pre id="XCTAssertNoThrow">XCTAssertNoThrow(expression, format…)</pre>

Generates a failure when expression does throw an exception.

&nbsp;

<pre id="XCTAssertNoThrowSpecific">XCTAssertNoThrowSpecific(expression, specificException, format…)</pre>

Generates a failure when expression does throw an exception of the specified class. Any other exception is okay (i.e. does not generate a failure).

&nbsp;

<pre id="XCTAssertNoThrowSpecificNamed">XCTAssertNoThrowSpecificNamed(expression, specificException, exception_name, format…)</pre>

Generates a failure when expression does throw an exception of a specific class with a specific name. Useful for those frameworks like AppKit or Foundation that throw generic NSException w/specific names (NSInvalidArgumentException, etc).

&nbsp;

<pre id="XCTAssertNotNil">XCTAssertNotNil(a1, format…)</pre>

Generates a failure when a1 is nil.

&nbsp;

<pre id="XCTAssertThrows">XCTAssertThrows(expression, format…)</pre>

Generates a failure when expression does not throw an exception.

&nbsp;

<pre id="XCTAssertThrowsSpecific">XCTAssertThrowsSpecific(expression, specificException, format…)</pre>

Generates a failure when expression does not throw an exception of a specific class.

&nbsp;

<pre id="XCTAssertThrowsSpecificNamed">XCTAssertThrowsSpecificNamed(expression, specificException, exception_name, format…)</pre>

Generates a failure when expression does not throw an exception of a specific class with a specific name. Useful for those frameworks like AppKit or Foundation that throw generic NSException w/specific names (NSInvalidArgumentException, etc).

&nbsp;

<pre id="XCTAssertTrue">XCTAssertTrue(expression, format…)</pre>

Generates a failure when expression evaluates to false.

&nbsp;

<pre id="XCTFail">XCTFail</pre>

Generates a failure unconditionally.

&nbsp;

And the oscar goes to &#8230; [Harry Hornreich!](http://appleprogramming.com/blog/2013/12/26/xctest-assertions-documentation/){.broken_link} &#8211; Thank you!