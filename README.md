Should
======

An Objective-C expectation framework based on the 'should' terminology.

All arguments and return types must be provided as objects. This has been made significantly easier by the introduction of literals for the most common data types.

This library is a work in progress, and so the API may be subject to simplification and potentially drastic change.

Expectations
============

Matchers
--------

Beehive provides matchers in the format of [[subject should] ...], allowing for more readable examples. The default matchers provided by Beehive are as follows:

    // Existence:
    [object shouldBeNil];
    
    // Equality:
    [[@(1+2) should] be:@3]; // Equivalent to beEqualTo:
    [[@(1+2) should] beEqualTo:@3];
    [[object should] beIdenticalTo:anotherObject];
    
    // Booleans:
    [[@true should] beTrue];
    [[@false should] beFalse];
    [[@YES should] beYes];
    [[@NO should] beNo];
    
    // Numbers:
    [[@0 should] beZero];
    [[@1 should] bePositive];
    [[@(-1) should] beNegative];
    [[@6 should] beGreaterThan:@5];
    [[@5 should] beLessThan:@6];
    [[@6 should] beGreaterThanOrEqualTo:@5];
    [[@5 should] beLessThanOrEqualTo:@6];
    [[@5 should] beBetween:@1 and:@10];
    
    // Objects:
    [[object should] beKindOfClass:[NSObject class]];
    [[object should] beMemberOfClass:[NSObject class]];
    [[object should] conformToProtocol:@protocol(NSCoding)];
    [[object should] respondToSelector:@selector(description)];
    
    // Collections:
    [[pets should] beEmpty];
    [[pets should] contain:cat];
    [[pets should] contain:@[cat, dog]];
    
    // Collections by associations:
    [[[person should] have:2] pets];
    [[[person should] haveAtLeast:2] pets];
    [[[person should] haveAtMost:2] pets];

In order to negate a matcher, either of the following is valid:

    [[@(1+1) shouldNot] beEqualTo:@3];
    [[[@(1+1) should] not] beEqualTo:@3];
    
Use whichever you prefer.

Some of the matchers listed above work based on the dynamic behaviour of Beehive - if no matcher exists with the provided selector, Beehive will attempt to realize the behaviour that you intended, based on convention. If the matcher provided begins with 'be', Beehive will swap 'be' out for 'is' and attempt to call a method with the generated selector on the subject. For example, 'beEqualTo:' calls 'isEqualTo:' has no matcher – instead, Beehive calls 'beEqualTo:' on the subject, providing the expected behaviour.

If you have a method such as -isGreen on your object, you don't need to write a matcher in order for the following to be valid:

    [[object should] beGreen];

License
=======

This project is available under the MIT license. See the LICENSE file for details.
