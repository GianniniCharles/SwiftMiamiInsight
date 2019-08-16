#IOS App Performance

Why you should use final class: https://developer.apple.com/swift/blog/?id=27

if you turn on internal class that will turn any internal to static dispatch (same thing that final achieves)

internal is the default value if you don’t put anything


"My defaults are every class is final and every property/function is fileprivate and go from there"

"Private > fileprivate"

"I believe it used to be the opposite"


"Yep I haven’t had to use fileprivate since Swift 3"

"That’s not to say it doesn’t have its uses, but a lot of the ACL crap got cleared up in 4."


"I never use private. What’s the difference?"


"Private restricts the use to the object"

"That’s what I thought. So if I have an extension in one file with a private method then I can access it from both files. That’s normally not what I want so I use fileprivate."


"I hide as much as possible from the interface. I declare functions inside of functions too if only the function needs it and the rest of the file doesn’t."


"fileprivate makes stuff private to everything, except other classes/extensions that happen to reside in the same file (edited)"


"private makes stuff private to everything outside of the class/struct, regardless of where they reside (edited)"


"so in my experience private is what you really want to be using — and once in a while you may need to resort to fileprivate. (edited)"


"in earlier versions of Swift, private would make stuff private even to extensions — this was not great if you use extensions to group chunks of code, so it got reverted."

"how do you test functions that are private?
in the past we had to make everything internal to test it?"

"Cant necessarily test the function but if the function sets a variable you could use mirror"


"example?"

"If you can trigger whatever needs to be triggered to set the internal state of the var you’re testing you can then call Mirror(reflecting: yourObj).children.first(where: { $0.label == "varNameYouWant" } ) as? Type and then see if the var was set correctly (edited) "


"awesome, thanks"

https://stackoverflow.com/a/37421807

"There’s a lot to be said for that approach"

"Love it, but no examples makes it very open to interpretation"

"Yep, it’s a different approach for sure. I do often wish for a way to test private methods without having to declare them as internal which i find gross, as often all the code resides in the same module which makes it available.

This means having to move it out to an external framework which is a lot of work “just” for testing and not making things available to folks that shouldn’t have access.
"

"I agree that if it’s well made code that just testing the public interface is the way to go but as we all know…often we live in a less than ideal world."

"100% ^"

"oh indeed"

"Private methods don’t need to be tested because something public is using them. Just test your public interface and make sure it does what you need.

You don’t care how it works, you only care that it works"

https://www.raywenderlich.com/2752-25-ios-app-performance-tips-tricks


"I was recently in a similar discussion in the Kotlin lang slack about a method annotation that exist in the Android Framework called @VissibleForTesting. The discussion was if it was a bad practice to extensively use this annotation.
Knowledgable people advice that using it low is handy now if you see that 40% of the class methods are using it @VissibleForTesting. Then you should probably depend on an interface/protocol that enforce these methods and inject it from the outside. Then test the interface itself separate.
On my personal experience I tend to agree... :arrow_down:
Private methods don’t need to be tested because something public is using them …"